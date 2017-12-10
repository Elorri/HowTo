## Create the widget layout xml file

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		xmlns:tools="http://schemas.android.com/tools"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:orientation="vertical"
		android:padding="@dimen/widget_margin">

		<FrameLayout
			android:id="@+id/widget_item"
			android:layout_width="match_parent"
			android:layout_height="@dimen/abc_action_bar_default_height_material"
			android:background="@color/primary">
			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:layout_gravity="center"
				android:textColor="@android:color/white"
				android:textSize="@dimen/widget_text_title"
				android:text="@string/today"/>
		</FrameLayout>
		<FrameLayout
			android:layout_width="match_parent"
			android:layout_height="0dp"
			android:layout_weight="1"
			android:background="@android:color/white">
			<ListView
				android:id="@+id/widget_list"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:divider="@null"
				android:dividerHeight="0dp"
				tools:listitem="@layout/widget_item"/>
			<TextView
				android:id="@+id/widget_empty"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:fontFamily="sans-serif-condensed"
				android:gravity="center"
				android:text="@string/empty_widget_list"
				android:textAppearance="?android:textAppearanceLarge"/>
		</FrameLayout>
	</LinearLayout>

## Create the widget item xml file

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		android:id="@+id/widget_item"
		xmlns:android="http://schemas.android.com/apk/res/android"
		xmlns:tools="http://schemas.android.com/tools"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:background="@android:color/white"
		android:orientation="horizontal"
		android:padding="8dp">
		<ImageView
			android:id="@+id/home_crest"
			android:layout_width="0dp"
			android:layout_height="match_parent"
			android:layout_gravity="center"
			android:layout_weight="1"
			tools:src="@drawable/aston_villa"/>
		<LinearLayout
			android:layout_width="0dp"
			android:layout_height="match_parent"
			android:layout_weight="1"
			android:orientation="vertical">
			<TextView
				android:id="@+id/score_textview"
				android:layout_width="wrap_content"
				android:layout_height="0dp"
				android:layout_gravity="center"
				android:layout_weight="1"
				android:gravity="center"
				android:textSize="@dimen/Score"
				tools:text="@string/scores_tool"/>
			<TextView
				android:id="@+id/time_textview"
				android:layout_width="wrap_content"
				android:layout_height="0dp"
				android:layout_gravity="center"
				android:layout_weight="1"
				android:gravity="center"
				tools:text="@string/time"/>
		</LinearLayout>
		<ImageView
			android:id="@+id/away_crest"
			android:layout_width="0dp"
			android:layout_height="match_parent"
			android:layout_gravity="center"
			android:layout_weight="1"
			tools:src="@drawable/leicester_city_fc_hd_logo"/>
	</LinearLayout>

	
## Add the widget dimen files in res/values and res/values-v14 (idem "Add a widget")

## Create the AppWidgetProviderInfo.xml in the res/xml directory

	<appwidget-provider
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:initialLayout="@layout/widget_list"
		android:initialKeyguardLayout="@layout/widget_list"
		android:minHeight="@dimen/widget_list_height"
		android:minWidth="@dimen/widget_list_width"
		android:previewImage="@drawable/widget_list_preview"
		android:updatePeriodMillis="0"
		android:widgetCategory="home_screen|keyguard"/>

## Create a RemoteViewsService and fill the RemoteViewsFactory methods (kind of CursorAdapter)

	@TargetApi(Build.VERSION_CODES.HONEYCOMB)
	public class WidgetListRemoteViewsService extends RemoteViewsService {
		@Override
		public RemoteViewsFactory onGetViewFactory(Intent intent) {
			return new RemoteViewsFactory() {
				private Cursor data = null;
				@Override
				public void onCreate() {
					// Nothing to do
				}
				@Override
				public void onDataSetChanged() {
					Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
					if (data != null) {
						data.close();
					}
					// This method is called by the app hosting the widget (e.g., the launcher)
					// However, our ContentProvider is not exported so it doesn't have access to the
					// data. Therefore we need to clear (and finally restore) the calling identity so
					// that calls use our process and permission
					final long identityToken = Binder.clearCallingIdentity();
					String now = Utilities.getToday();
					data = getContentResolver().query(
							ScoresContract.ScoreEntry.buildScoreByDate(now),
							ScoresFragment.MATCHES_COLUMNS,
							null,
							null,
							null);
					Binder.restoreCallingIdentity(identityToken);
				}
				@Override
				public void onDestroy() {
					if (data != null) {
						data.close();
						data = null;
					}
				}
				@Override
				public int getCount() {
					return data == null ? 0 : data.getCount();
				}
				@Override
				public RemoteViews getViewAt(int position) {
					Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
					if (position == AdapterView.INVALID_POSITION ||
							data == null || !data.moveToPosition(position)) {
						return null;
					}
					RemoteViews views = new RemoteViews(getPackageName(),
							R.layout.widget_item);

					// Extract the data from the Cursor
					Context context=getApplicationContext();
					int homeCrest=Utilities.getTeamCrestByTeamName(context,
							data.getString(ScoresFragment.COL_HOME));
					int awayCrest=Utilities.getTeamCrestByTeamName(context,
							data.getString(ScoresFragment.COL_AWAY));
					String scores =Utilities.getScores(context,
							data.getInt(ScoresFragment.COL_HOME_GOALS),
							data.getInt(ScoresFragment.COL_AWAY_GOALS));
					String time =data.getString(ScoresFragment.COL_MATCHTIME);

					// Add the data to the RemoteViews
					views.setImageViewResource(R.id.home_crest, homeCrest);
					views.setImageViewResource(R.id.away_crest, awayCrest);
					views.setTextViewText(R.id.score_textview, scores);
					views.setTextViewText(R.id.time_textview, time);

					// Create an Intent to launch DetailActivity
					final Intent fillInIntent = new Intent();
					Uri detailUri= ScoresContract.ScoreEntry.buildScoreByDate(Utilities.getToday());
					fillInIntent.setData(detailUri);
					views.setOnClickFillInIntent(R.id.widget_item, fillInIntent);
					return views;
				}
				@Override
				public RemoteViews getLoadingView() {
					return new RemoteViews(getPackageName(), R.layout.widget_item);
				}
				@Override
				public int getViewTypeCount() {
					return 1;
				}
				@Override
				public long getItemId(int position) {
					if (data.moveToPosition(position))
						return data.getLong(ScoresFragment.COL_MATCH_ID);
					return position;
				}
				@Override
				public boolean hasStableIds() {
					return true;
				}
			};
		}
	}


## Create the AppWidgetProvider.java class

	public class WidgetListProvider extends AppWidgetProvider {
		public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
			Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
			// Perform this loop procedure for each App Widget that belongs to this provider
			for (int appWidgetId : appWidgetIds) {
				RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.widget_list);

				// Create an Intent to launch MainActivity
				Intent intent = new Intent(context, MainActivity.class);
				PendingIntent pendingIntent = PendingIntent.getActivity(context, 0, intent, 0);
				views.setOnClickPendingIntent(R.id.widget_item, pendingIntent);

				// Set up the collection
				if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.ICE_CREAM_SANDWICH) {
					setRemoteAdapter(context, views);
				} else {
					setRemoteAdapterV11(context, views);
				}
				Intent clickIntentTemplate = new Intent(context, MainActivity.class);
				PendingIntent clickPendingIntentTemplate = TaskStackBuilder.create(context)
						.addNextIntentWithParentStack(clickIntentTemplate)
						.getPendingIntent(0, PendingIntent.FLAG_UPDATE_CURRENT);
				views.setPendingIntentTemplate(R.id.widget_list, clickPendingIntentTemplate);
				views.setEmptyView(R.id.widget_list, R.id.widget_empty);

				// Tell the AppWidgetManager to perform an update on the current app widget
				appWidgetManager.updateAppWidget(appWidgetId, views);
			}
		}

		@Override
		public void onReceive(@NonNull Context context, @NonNull Intent intent) {
			Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
			super.onReceive(context, intent);
			if (ScoresSyncAdapter.ACTION_DATA_UPDATED.equals(intent.getAction())) {
				AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
				int[] appWidgetIds = appWidgetManager.getAppWidgetIds(
						new ComponentName(context, getClass()));
				//This method will trigger WidgetListRemoteViewsService RemoteViewsFactory
				// .onDataChanged() and update the widget UI
				appWidgetManager.notifyAppWidgetViewDataChanged(appWidgetIds, R.id.widget_list);
			}
		}

		/**
		 * Sets the remote adapter used to fill in the list items
		 * @param views RemoteViews to set the RemoteAdapter
		 */
		@TargetApi(Build.VERSION_CODES.ICE_CREAM_SANDWICH)
		private void setRemoteAdapter(Context context, @NonNull final RemoteViews views) {
			views.setRemoteAdapter(R.id.widget_list,
					new Intent(context, WidgetListRemoteViewsService.class));
		}

		/**
		 * Sets the remote adapter used to fill in the list items
		 * @param views RemoteViews to set the RemoteAdapter
		 */
		@SuppressWarnings("deprecation")
		private void setRemoteAdapterV11(Context context, @NonNull final RemoteViews views) {
			views.setRemoteAdapter(0, R.id.widget_list,
					new Intent(context, WidgetListRemoteViewsService.class));
		}
	}

## Add a constant action in the SyncAdapter and send broadcast when data is updated (idem "Add a widget" - can use same method if several widgets)

## Add entry in the manifest

        <receiver
            android:name=".widget.WidgetListProvider"
            android:label="@string/title_widget_list">
            <intent-filter>
                <action android:name="android.appwidget.action.APPWIDGET_UPDATE"/>
                <action android:name="footballscores.barqsoft.ACTION_DATA_UPDATED"/>
            </intent-filter>
            <meta-data android:name="android.appwidget.provider"
                       android:resource="@xml/widget_provider_list_info"/>
        </receiver>
        <service
            android:name=".widget.WidgetListRemoteViewsService"
            android:exported="false"
            android:permission="android.permission.BIND_REMOTEVIEWS"/>

		


