## Add a content transition (since-21 lollipop): how individual views enter and exit.(the use of content transitions turn off the default window animation)
	ActivityA calls ActivityB : we can call 2 transition exitA enterB
	ActivityB back to ActivityA : we call 2 transition returnB followed by re-enterA
	
add an exit transition in xml in res/transition/exitA.xml

	<explode xlmns=.../>   <-means the views on ActivityA will diseapears by moving outwards like an explosion
	
in res/values/slyles.xml

	<style name="AppTheme.Home">
		<item name="android:widowContentTransition">true</item>		<-this is only needed if your theme does not inherit from AppCompat or Material
		<item name="android:widowExitTransition">@transition/exitA</item>
	</style>
	
in  ActivityA.java

	Bundle bundle= ActivityOptions.makeSceneTransitionAnimation(this).toBundle();
	context.startActivty(intent,bundle);

add an enterB transition from code. You can achieve the samewith xml. 

	Slide slide=new Slide(Gravity.BOTTOM);    	//we want our textview to appear from bottom
	slide.addTarget(R.id.description);			//the id of ourtextview
	slide.setInterpolator(AnimationUtils.loadInterpolator(this, android.R.interpolator
			.linear_out_slow_in));
	slide.setDuration(slideDuration);
	getWindow().setEnterTransition(slide);
	
using code is short but not easilly reusable in other apps and a check for the correct api must be done like so

	if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP){

	}
	
using xml easilly reusable 

	res/transition-v21/exitA
	res/values-v21/styles.xml
	
you can use a mixte approach and load a transition in code

    TransitionInflater.from(this).inflateTransition(R.transition.exitA));
	
when clicking back button 

	transitions by default are reversed
	the explode will become an implode (re-enterA)
	
if you want to customise the default 

	<style name="AppTheme.Home">
		<item name="android:widowContentTransition">true</item>		<-this is only needed if your theme does not inherit from AppCompat or Material
		<item name="android:widowExitTransition">@transition/exitA</item>
		<item name="android:widowReenterTransition">@transition/reenterA</item>
	</style>
