# Add a Mock Data Widget

## Create the widget layout xml file with mock data

- Avertissement (caveat) : with widget margin behavior change.
	- before icecream sandwitch : widget needs to provide their own margins so that widget would appear huge next to the app icon already on the home screen
	- since icecream sandwitch :margins are automatically applied, you shouldn't had some.
- To make the widget compatible : we wrap our widget in a framelayout that include the padding foreach api level


		<?xml version="1.0" encoding="utf-8"?>
		<FrameLayout
			xmlns:android="http://schemas.android.com/apk/res/android"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			android:padding="@dimen/widget_margin">
			<LinearLayout
				android:id="@id/widget"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:background="@android:color/white"
				android:orientation="horizontal"
				android:paddingTop="5dp">
				<ImageView
					android:id="@id/home_crest"
					android:layout_width="0dp"
					android:layout_height="match_parent"
					android:layout_gravity="center"
					android:layout_weight="1"
					android:src="@drawable/aston_villa"/>
				<LinearLayout
					android:layout_width="0dp"
					android:layout_height="match_parent"
					android:layout_weight="1"
					android:orientation="vertical">
					<TextView
						android:id="@id/score_textview"
						android:layout_width="wrap_content"
						android:layout_height="0dp"
						android:layout_gravity="center"
						android:layout_weight="1"
						android:gravity="center"
						android:text="@string/scores_tool"
						android:textSize="@dimen/Score"/>
					<TextView
						android:id="@id/time_textview"
						android:layout_width="wrap_content"
						android:layout_height="0dp"
						android:layout_gravity="center"
						android:layout_weight="1"
						android:gravity="center"
						android:text="@string/time"/>
				</LinearLayout>
				<ImageView
					android:id="@id/away_crest"
					android:layout_width="0dp"
					android:layout_height="match_parent"
					android:layout_gravity="center"
					android:layout_weight="1"
					android:src="@drawable/leicester_city_fc_hd_logo"/>
			</LinearLayout>
		</FrameLayout>
	

	
## Add the widget dimen files in res/values and res/values-v14

res/values

		<?xml version="1.0" encoding="utf-8"?>
		<resources>
			<dimen name="widget_margin">8dp</dimen>
		</resources>

res/values-v14

		<?xml version="1.0" encoding="utf-8"?>
		<resources>
			<dimen name="widget_margin">0dp</dimen>
		</resources>


## Create the AppWidgetProviderInfo.xml in the res/xml directory

		<appwidget-provider
			xmlns:android="http://schemas.android.com/apk/res/android"
			android:initialLayout="@layout/widget_today"
			android:initialKeyguardLayout="@layout/widget_today" --> seems important when phone is locked, could be ignore
			android:minHeight="@dimen/widget_height"
			android:minWidth="@dimen/widget_width"
			android:widgetCategory="home_screen|keyguard"  --> mention keyguard if use of it
			android:updatePeriodMillis="0"/>


## Create the AppWidgetProvider.java class

		public class FootballWidgetProvider extends AppWidgetProvider {

			@Override
			public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
				// Perform this loop procedure for each widget
				for (int appWidgetId : appWidgetIds) {
					RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.widget_next_match);

					// Add the data to the RemoteViews
					views.setImageViewResource(R.id.home_crest, R.drawable.burney_fc_hd_logo);
					views.setImageViewResource(R.id.away_crest, R.drawable.everton_fc_logo1);
					views.setTextViewText(R.id.home_name, "Stoke City FC My");
					views.setTextViewText(R.id.away_name, "Norwish City FC My");
					views.setTextViewText(R.id.score_textview, "2 - 1");
					views.setTextViewText(R.id.time_textview, "20:50");

					// Create an Intent to launch MainActivity
					Intent launchIntent = new Intent(context, MainActivity.class);
					PendingIntent pendingIntent = PendingIntent.getActivity(context, 0, launchIntent, 0);
					views.setOnClickPendingIntent(R.id.widget, pendingIntent);

					// Tell the AppWidgetManager to perform an update on the current app widget
					appWidgetManager.updateAppWidget(appWidgetId, views);
				}
			}
		}

NB : if need to setContentDescriptions

            // Content Descriptions for RemoteViews were only added in ICS MR1
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.ICE_CREAM_SANDWICH_MR1) {
                setRemoteContentDescription(views, description);
            }
			
and 

			@TargetApi(Build.VERSION_CODES.ICE_CREAM_SANDWICH_MR1)
			private void setRemoteContentDescription(RemoteViews views, String description) {
				views.setContentDescription(R.id.widget_icon, description);
			}
	

	
## Add entry in the manifest

Nb : APPWIDGET_UDDATE will call the AppWidgetProvider onUpdate 

        <!-- Next Matches Widget -->
        <receiver
            android:name=".widget.FootballWidgetProvider"
            android:label="@string/title_widget_next_match">
            <intent-filter>
                <action android:name="android.appwidget.action.APPWIDGET_UPDATE"/>
            </intent-filter>
            <meta-data android:name="android.appwidget.provider"
                       android:resource="@xml/football_widget_provider_info"/>
        </receiver>

# Fill widget with data from db

## Add a constant action in the SyncAdapter and send broadcast when data is updated

   public static final String ACTION_DATA_UPDATED ="footballscores.barqsoft.ACTION_DATA_UPDATED";
   
   ...
   //end sync
   updateWidgets();
   
       private void updateWidgets() {
        Context context = getContext();
        // Setting the package ensures that only components in our app will receive the broadcast
        Intent dataUpdatedIntent = new Intent(ACTION_DATA_UPDATED)
                .setPackage(context.getPackageName());
        context.sendBroadcast(dataUpdatedIntent);
    }
	
## Tell manifest widget that he needs to listen to this intent

		<action android:name="footballscores.barqsoft.ACTION_DATA_UPDATED" />
	
	    <!-- Next Matches Widget -->
        <receiver
            android:name=".widget.FootballWidgetProvider"
            android:label="@string/title_widget_next_match">
            <intent-filter>
                <action android:name="android.appwidget.action.APPWIDGET_UPDATE"/>
				<action android:name="footballscores.barqsoft.ACTION_DATA_UPDATED" />
            </intent-filter>
            <meta-data android:name="android.appwidget.provider"
                       android:resource="@xml/football_widget_provider_info"/>
        </receiver>

## Because call calling db can't be done on UI thread move AppWidgetProvider.onUpdate code to an IntentService.onHandleIntent() class.

public class FootballWidgetIntentService extends IntentService {
    public FootballWidgetIntentService() {
        super("FootballWidgetIntentService");
    }
    @Override
    protected void onHandleIntent(Intent intent) {
        // Retrieve all of the Today widget ids: these are the widgets we need to update
        AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(this);
        int[] appWidgetIds = appWidgetManager.getAppWidgetIds(new ComponentName(this,
                FootballWidgetProvider.class));

        // Get now's data from the ContentProvider
        String now = Utilities.getNow();
        Cursor cursor = getContentResolver().query(
                ScoresContract.ScoreEntry.buildScoreByDate(now),
                ScoresFragment.MATCHES_COLUMNS,
                null,
                null,
                null);
        if (cursor == null) {
            return;
        }
        if (!cursor.moveToFirst()) {
            cursor.close();
            return;
        }
        // Extract the data from the Cursor
        Context context=getApplicationContext();
        int homeCrest=Utilities.getTeamCrestByTeamName(context,
                cursor.getString(ScoresFragment.COL_HOME));
        int awayCrest=Utilities.getTeamCrestByTeamName(context,
                cursor.getString(ScoresFragment.COL_AWAY));
        String scores =Utilities.getScores(context,
                cursor.getInt(ScoresFragment.COL_HOME_GOALS),
                cursor.getInt(ScoresFragment.COL_AWAY_GOALS));
        String time =cursor.getString(ScoresFragment.COL_MATCHTIME);
        cursor.close();

        // Perform this loop procedure for each widget
        for (int appWidgetId : appWidgetIds) {
            RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.widget_next_match);

            // Add the data to the RemoteViews
            views.setImageViewResource(R.id.home_crest, homeCrest);
            views.setImageViewResource(R.id.away_crest, awayCrest);
            views.setTextViewText(R.id.score_textview, scores);
            views.setTextViewText(R.id.time_textview, time);

            // Create an Intent to launch MainActivity
            Intent launchIntent = new Intent(context, MainActivity.class);
            PendingIntent pendingIntent = PendingIntent.getActivity(context, 0, launchIntent, 0);
            views.setOnClickPendingIntent(R.id.widget, pendingIntent);

            // Tell the AppWidgetManager to perform an update on the current app widget
            appWidgetManager.updateAppWidget(appWidgetId, views);
        }
    }
}

## Start the AppWidgetIntentService class in the AppWidgetProvider.onUpdate

		public class FootballWidgetProvider extends AppWidgetProvider {
			@Override
			public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
				Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
				context.startService(new Intent(context, FootballWidgetIntentService.class));
			}

			@Override
			public void onAppWidgetOptionsChanged(Context context, AppWidgetManager appWidgetManager,
												  int appWidgetId, Bundle newOptions) {
				Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
				context.startService(new Intent(context, FootballWidgetIntentService.class));
			}

			@Override
			public void onReceive(@NonNull Context context, @NonNull Intent intent) {
				Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
				super.onReceive(context, intent);
				if (ScoresSyncAdapter.ACTION_DATA_UPDATED.equals(intent.getAction())) {
					Log.e("SuperDuo", Thread.currentThread().getStackTrace()[2] + "");
					context.startService(new Intent(context, FootballWidgetIntentService.class));
				}
			}
		}

## Add AppWidgetIntentService in the manifest

        <service android:name=".widget.TodayWidgetIntentService" />

		
# Add a widget preview

Take 288 pixel for 1 unit. Exple : if widget is 2 x 1, preview is 576px x 288px
- Create a copie of the widget_layout.xml
- Add 576px x 288px width and height
- Add mock data
- Click the camera screenshot button (it takes the whole phone screen).
- Open in paint and remove unwanted areas.
- save in drawable-nodpi folder
- add tag android:previewImage="@drawable/widget_preview" in AppWidgetProviderInfo.xml
- remove widget_layout.xml copie

# Make widget resizable

## Add those methods for width or  height or both in TodayWidgetIntentService

		private int getWidgetWidth(AppWidgetManager appWidgetManager, int appWidgetId) {
			// Prior to Jelly Bean, widgets were always their default size
			if (Build.VERSION.SDK_INT < Build.VERSION_CODES.JELLY_BEAN) {
				return getResources().getDimensionPixelSize(R.dimen.widget_today_default_width);
			}
			// For Jelly Bean and higher devices, widgets can be resized - the current size can be
			// retrieved from the newly added App Widget Options
			return getWidgetWidthFromOptions(appWidgetManager, appWidgetId);
		}

		@TargetApi(Build.VERSION_CODES.JELLY_BEAN)
		private int getWidgetWidthFromOptions(AppWidgetManager appWidgetManager, int appWidgetId) {
			Bundle options = appWidgetManager.getAppWidgetOptions(appWidgetId);
			if (options.containsKey(AppWidgetManager.OPTION_APPWIDGET_MIN_WIDTH)) {
				int minWidthDp = options.getInt(AppWidgetManager.OPTION_APPWIDGET_MIN_WIDTH);
				// The width returned is in dp, but we'll convert it to pixels to match the other widths
				DisplayMetrics displayMetrics = getResources().getDisplayMetrics();
				return (int) TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, minWidthDp,
						displayMetrics);
			}
			return  getResources().getDimensionPixelSize(R.dimen.widget_today_default_width);
		}

## Inflate widget with correct layout in TodayWidgetIntentService

Change line 

        RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.widget_next_match);

By

            int layoutId = R.layout.widget_today_small;
            // Find the correct layout based on the widget's width
            int widgetWidth = getWidgetWidth(appWidgetManager, appWidgetId);
            int defaultWidth = getResources().getDimensionPixelSize(R.dimen.widget_today_default_width);
            int largeWidth = getResources().getDimensionPixelSize(R.dimen.widget_today_large_width);
            int layoutId;
            if (widgetWidth >= largeWidth) {
                layoutId = R.layout.widget_today_large;
            } else if (widgetWidth >= defaultWidth) {
                layoutId = R.layout.widget_today;
            } else {
                layoutId = R.layout.widget_today_small;
            }
             RemoteViews views = new RemoteViews(getPackageName(), layoutId);
			 
# Add attribute in AppWidgetProviderInfo.xml

		android:minResizeHeight="@dimen/widget_today_min_resize_height"
		android:minResizeWidth="@dimen/widget_today_min_resize_width"
		android:resizeMode="horizontal"

to see initial layout when in dev (??)

		xmlns:tools="http://schemas.android.com/tools"
		tools:ignore="UnusedAttribute"

