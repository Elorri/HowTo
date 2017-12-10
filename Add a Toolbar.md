# Add action bar in settings

in AndroidManifest.xml add ... in the SettingsActivity

	android:theme="@style/SettingsTheme"

## Add ActionBar on Settings for pre-lolipop devices 

in values/styles.xml add 

    <!-- Settings activity theme. -->
    <style name="SettingsTheme" parent="@android:style/Theme.Holo.Light.DarkActionBar">
        <item name="android:actionBarStyle">@style/ActionBar.PreLollipop.PopularMovies.NoTitle</item>
    </style>

    <!-- Settings activity action bar styles -->
    <style name="ActionBar.PreLollipop.PopularMovies.NoTitle"
           parent="@android:style/Widget.Holo.Light.ActionBar.Solid.Inverse">
        <item name="android:background">@color/primary</item>
        <item name="android:height">56dp</item>
    </style>

## Add ActionBar on Settings for lolipop devices 

in values-v21/styles.xml add

	<?xml version="1.0" encoding="utf-8"?>
	<resources>
		<!-- Settings activity theme. -->
		<style name="SettingsTheme" parent="@android:style/Theme.Material.Light.DarkActionBar">
			<item name="android:colorPrimary">@color/primary</item>
			<item name="android:colorPrimaryDark">@color/primary_dark</item>
		</style>
	</resources>
	
# Add action bar everywhere else

in gradle add dependencie 

    compile 'com.android.support:appcompat-v7:23.1.1'

in values/styles.xml make sure the AppTheme has no action bar

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
    </style>


## create a style for your toolbar widget

	<!-- Toolbar style -->
    <style name="Toolbar" parent="Widget.AppCompat.Toolbar">
        <item name="android:background">?attr/colorPrimary</item>
        <item name="popupTheme">@style/Theme.AppCompat.Light</item>
    </style>
	
## Add a toolbar item in the app theme
    <style name="AppTheme" parent="@style/Theme.AppCompat.Light.NoActionBar">
		<item name="toolbarStyle">@style/Toolbar</item>
    </style>
	
## Create a toolbar.xml layout

	<android.support.v7.widget.Toolbar
		android:id="@+id/toolbar"
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:layout_width="match_parent"
		android:layout_height="?attr/actionBarSize"
		android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar" />
		
## Add toolbar in every xml screens layout

with include

    <include layout="@layout/toolbar" />
	
or with tag

	<android.support.v7.widget.Toolbar.../>
	
note : Toobar shouldn't be split with another piece of material. Wich means we often need multiple toobars.
	
## customise your Toolbar by adding an image

Note : The ImageView layout_width should be wrap_content otherwise the it will not take into account the overflow menu.
	
    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
        >
        <ImageView
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:src="@drawable/ic_logo"
            android:scaleType="center"/>
        </android.support.v7.widget.Toolbar>	
		
## example of phone main layout layout/activity_main.xml

	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		xmlns:tools="http://schemas.android.com/tools"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:orientation="vertical">

		<android.support.v7.widget.Toolbar
			android:id="@+id/toolbar"
			android:layout_width="match_parent"
			android:layout_height="?attr/actionBarSize"
			android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">
			<ImageView
				android:layout_width="wrap_content"
				android:layout_height="match_parent"
				android:src="@drawable/ic_logo"
				android:scaleType="center"/>
			</android.support.v7.widget.Toolbar>

		<fragment
			android:id="@+id/fragment_forecast"
			android:name="com.example.android.sunshine.app.ForecastFragment"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			tools:context="com.example.android.sunshine.app.ForecastFragment"
			tools:layout="@android:layout/list_content" />
	</LinearLayout>
	
## example of tablette main layout layout-sw600dp/activity_main.xml

		<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
			xmlns:tools="http://schemas.android.com/tools"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			android:orientation="vertical">

			<android.support.v7.widget.Toolbar
				android:id="@+id/toolbar"
				android:layout_width="match_parent"
				android:layout_height="?attr/actionBarSize"
				android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
				>
				<ImageView
					android:layout_width="wrap_content"
					android:layout_height="match_parent"
					android:src="@drawable/ic_logo"
					android:scaleType="center"/>
				</android.support.v7.widget.Toolbar>

			<LinearLayout
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:baselineAligned="false"
				android:divider="?android:attr/dividerHorizontal"
				android:orientation="horizontal"
				tools:context="com.example.android.sunshine.app.MainActivity">

				<!--
				This layout is a two-pane layout for the Items master/detail flow.
				-->

				<fragment
					android:id="@+id/fragment_forecast"
					android:name="com.example.android.sunshine.app.ForecastFragment"
					android:layout_width="0dp"
					android:layout_height="match_parent"
					android:layout_weight="2"
					tools:layout="@android:layout/list_content" />

				<FrameLayout
					android:id="@+id/weather_detail_container"
					android:layout_width="0dp"
					android:layout_height="match_parent"
					android:layout_weight="4" />

			</LinearLayout>
		</LinearLayout>
		
## Inflate toolbar and make it work like an action bar in every java layout controller classes.

	Toolbar toolbar=(Toolbar)findviewById(R.id.toolbar);
	setSupportActionBar(toolbar);
	setDisplayHomeAsUpEnabled(true);
	setDisplayShowTitleEnabled(false);
	
	setHomeButtonEnabled() ??
	setDisplayShowHomeEnabled() ??

### Those 2 lines alones

        Toolbar toolbar=(Toolbar)findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
		
will show the title and the action menu if one is inflated

### Those 2 lines alones

        Toolbar toolbar=(Toolbar)findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        getSupportActionBar().setDisplayShowTitleEnabled(false);
		
won't show title

### Those 3 lines alones
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);

will display hamburger or arrow, but clicling on it won't pop the backstack. To make it pop the back stack, you need to declare a parent activity in the manifest. like that : 

        <activity android:name=".ActivityA" android:label="ActivityA"
                  android:parentActivityName=".MainActivity">
            <meta-data
                android:name="android.support.PARENT_ACTIVITY"
                android:value=".MainActivity"/>
        </activity>

Or like that

        <activity android:name=".ActivityA" android:label="ActivityA"   android:parentActivityName=".MainActivity"/>

Meta data is for newer API


### Don't know

Thoses lines

        getSupportActionBar().setHomeButtonEnabled(true);
		getSupportActionBar().setDefaultDisplayHomeAsUpEnabled(true);
		getSupportActionBar().setDisplayShowHomeEnabled(true);
		
tested as follow

        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        the_line_I_dont_know_what_it_does

exemple

        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        getSupportActionBar().setHomeButtonEnabled(true);
	
don't seems to be doing anything. Doesn't show arrow or hamburger. Doesn't activate arrow or hamburger button.






# Toolbar

	don't use the toolbar available in the theme, use the toolbar widget.
	See "Add a Toolbar"

	Toobar shouldn't be split with another piece of material. Wich means we often need multiple toobars.
	Toolbars have transparent background defaults.
	The imageview inside thetoolbar should be wrap_content width otherwise the it will not take into account the overflow menu.
	
	It's a viewgroup so we can add childrens to it, for example you can use a spinner control for navigation
	when you want an enlarge toolbar, use a multiple of a standard height
	
	?attr/actionBarSize
	style="?attr/buttonBarButtonStyle"




	
	
	

