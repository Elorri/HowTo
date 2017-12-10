# Collapsing toolbar
	
	<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
		xmlns:app="http://schemas.android.com/apk/res-auto"  <-needed
		android:layout_width="match_parent"
		android:layout_height="match_parent">

		<android.support.design.widget.AppBarLayout
			android:id="@+id/app_bar_layout"
			android:layout_width="match_parent"
			android:layout_height="168dp"
			android:background="?colorPrimary">

			<android.support.design.widget.CollapsingToolbarLayout    <-this will draw the title if there is one
				android:id="@+id/collapsing_toolbar_layout"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				app:collapsedTitleTextAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse"
				app:expandedTitleTextAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse"
				app:expandedTitleMarginStart="72dp"
				app:layout_scrollFlags="scroll|exitUntilCollapsed">			<-scroll off the screen until it reaches the collapsing size

				<android.support.v7.widget.Toolbar    <-this will draw the icons
					android:id="@+id/app_bar"
					android:layout_width="match_parent"
					android:layout_height="?actionBarSize"				<-small size we want to collapse to
					android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
					app:navigationIcon="@drawable/ic_menu"
					app:contentInsetStart="72dp"
					app:layout_collapseMode="pin" />

			</android.support.design.widget.CollapsingToolbarLayout>
		</android.support.design.widget.AppBarLayout>

		<android.support.v7.widget.RecyclerView
			android:id="@+id/recyclerview"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			app:layout_behavior="@string/appbar_scrolling_view_behavior" />   <-special predifine behavior that triggers app_bar scrolling when recycler view is scroll

	</android.support.design.widget.CoordinatorLayout>
	
to achive the same effect with a textview instead of a recycler view. to make the toolbar scroll unitl its collapse size when the user scroll the textview you need this line (with a recyclerview or listview there is no need, because by default they are capable of nested scrolling, appbarlayout look for items with this line) ... used with CoordinatorLayout in the scrollayout of the textview

		android:nestedScrollingEnabled="true"
		
In the end it should be someting like that (but I haven't tested it).

	<?xml version="1.0" encoding="utf-8"?>
	<android.support.design.widget.CoordinatorLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		xmlns:app="http://schemas.android.com/apk/res-auto"
		android:layout_width="match_parent"
		android:layout_height="match_parent">

		<android.support.design.widget.AppBarLayout
			android:id="@+id/app_bar_layout"
			android:layout_width="match_parent"
			android:layout_height="168dp"
			android:background="?colorPrimary">

			<android.support.design.widget.CollapsingToolbarLayout
				android:id="@+id/collapsing_toolbar_layout"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				app:collapsedTitleTextAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse"
				app:expandedTitleMarginStart="72dp"
				app:expandedTitleTextAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse"
				app:layout_scrollFlags="scroll|exitUntilCollapsed">
				
				<ImageView
					android:layout_width="match_parent"
					android:layout_height="match_parent"
					android:scaleType="centerCrop"
					android:src="@drawable/eclairs"
					app:layout_collapseMode="parallax"			<-this effect goes well with this kindof patterns.
					/>

				<android.support.v7.widget.Toolbar
					android:id="@+id/app_bar"
					android:layout_width="match_parent"
					android:layout_height="?actionBarSize"
					android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
					app:contentInsetStart="72dp"
					app:layout_collapseMode="pin"
					app:navigationIcon="@drawable/ic_menu"/>

			</android.support.design.widget.CollapsingToolbarLayout>
		</android.support.design.widget.AppBarLayout>

	<ScrollView 
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:nestedScrollingEnabled="true"
		app:layout_behavior="android.support.design.widget.AppBarLayout">
		
		<TextView
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginTop="16dp"
			android:textAppearance="@style/Base.TextAppearance.AppCompat"
			android:layout_marginRight="16dp"
			android:layout_marginLeft="16dp"
			/>
	</ScrollView>

	</android.support.design.widget.CoordinatorLayout>



Github sample : DynamicSurfacesDemo

	collapsing toolbar with image. try it on phone please.
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master