# Activity

- use them to represent a page
- use them for correct backstack

# Fragment
- use them whenever a piece of info on the page will be replaced by another

# Custom View
- use them whenever a piece of info on the page will be replaced by another


# Best practices
- Always have 1 Activity and it's corresponding Fragment embedded inside activity. ActivityA - FragmentA.
- Use activities for backstack management.
- Prefer fragments over custom views

# Why ?

## Why have ActivityA and FragmentA ?
- To make it easy to put FragmentA on ActivityB ou ActivityC if needed in the future.
- Because one day the best practice will change and we will have only 1 Activity and several Fragments

## Why use activities for backstack management and not fragment ?
- because the getSupportFragmentManager().getChildFragmentManager() is not always working perfectly and we have to recreate the backstack by hand at the moment.
- it's still easier to use activities.
- fragment are not added to the manifest and the tags we put here for navigation does not exists.

## Why prefer fragments over custom views ?
- custom views were what we were using before existance of fragments. Bigest problem was to save their current state on orientation change and recreate them. Note: custom views have an onSaveInstanceStateMethod but nothing issaved automatically.
- with customiews nothing is keeping track of the history of views and their states
- fragments save their state automatically on orientation change
- even better, By using Fragment.setRetainInstance(true) you can bypass Fragment.onDestroy(), i.e. can keep fragment data on configuration changes but fragment view structure is still destroyed/recreated.
- whenever you do add or replace you the app take a screenshot of the state of what was in the container if you need to access it later on.


# Stack Management
- every activity should have their parents declared in the manifest.


# if launch mode not specified it's in standard mode

## android:launchMode="standard"
The system will recreate the activity even if already existing in the task stack.

## android:launchMode="singleTop"
The system will recreate the activity ONLY if it's NOT already existing in the task stack.

https://developer.android.com/guide/topics/manifest/activity-element.html#lmode



Task is a stack of activities (some of them can come from others app).
A new task is created by launching an app. The first activity launched is called bootstrap and isthe first on the task.
We can create several task if we launch several apps, but there always 1 single current task, the one in the foreground.
The task stack can have several instances of the same activity.
Also, two instances of the same activity may run in two different tasks.


Best tuto http://blog.akquinet.de/2010/04/15/android-activites-and-tasks-series-intent-flags/
Best apk http://www.spree.de/blog/android_activities_and_tasks/IntentFlagsTool-v1.apk
https://github.com/akquinet/android-intent-flags-tool


A intent consist of : 
- an action : this action is just a constant, either a pre-defined one from Android, or a custom one that we can define ourselves
- some data : 

An intent can only be received by (the callee):
- an activity
- a service
- a broadcast receiver


# The caller

## Start external activity

		Intent intent = new Intent(action, data);
		
		Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("http://www.akquinet.com/")
		startActivity(intent);

Note that any activity can be declared capable of handling certain intent action by defining intent filters in the application’s AndroidManifest.xml file.

intent tags


# The callee

launch modes and affinities in manifest

	
