#Add a transition
1. add a transition xml ressource
	2. put the duration
	3. put the fade tag : it will fade everything, so specify in there what you don't want to fade using targets excludeId.
	4. put the tag slide for toolbar and detail with the source direction in attribute. To make animation slide in from thetop :slideEdge="Top"
5. apply for theme in the style file (it's better than doing from code directly)
	6. Add item content transition
	7. Add your ressource transitions as items
	8. add the theme in the manifest
8. In the activity startActivity enable the scene transition
	9. call startActivity with a Bundle
		ActivityOptionsCompat activityOptions = ActivityOptionsCompat.makeSceneTransitionAnimation(this);
        ActivityCompat.startActivity(this, intent, activityOptions.toBundle());
		
# Add transition
		
Add add a res/transition/grid_enter xml ressource

	<slide
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:slideEdge="top"
		android:duration="3000"
		android:interpolator="@android:interpolator/linear_out_slow_in">

	</slide>
	
create a new style theme with the transition

    <style name="AppTheme.Home">
        <item name="android:windowEnterTransition">@transition/grid_enter</item>
    </style>
	
add the theme in the manifest

        <activity
           android:name=".ArticleListActivity"
           android:theme="@style/AppTheme.Home">
		   
in the activity onCreate, create a transition bundle

	final Bundle bundle= ActivityOptions.makeSceneTransitionAnimation(getActivity()).toBundle();
	
start the next activity with a transition

	getActivity().startActivity(new Intent(getContext(), ArticleDetailActivity.class), bundle);

# Add shared element

in xml android:transitionName="@string/keep"
in onCreate 

+                    final Bundle bundle= ActivityOptions.makeSceneTransitionAnimation(
 +                            getActivity(),
 +                            view,
 +                            getResources().getString(R.string.keep))
 +                            .toBundle();
		  
	
