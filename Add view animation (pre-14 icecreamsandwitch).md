##  object/view animation  (Pre-IceCreamSandwitch api 14)

	AnimationSet animationSet = new AnimationSet(context, null);
	animationSet.addAnimation(new AlphaAnimation(1f,0f)); <-alpha property of the view, as a value between 0 (completely transparent) and 1 (completely opaque). Must be a floating point value.
	animationSet.addAnimation(new TranslateAnimation(0,0,0,-mButton.getHeight()));
	animationSet.setDuration(getRessources().getInteger(android.R.integer.config_shortAnimationTime));
	animationSet.setAnimationListener(new Animation.AnimationListener(){
		@Override
		public void onAnimationEnd(Animation anmation){
			mButton.setVsibility(View.GONE);
			startActivity(new Intent(MainActivity.this, SubActivity.class));
			overridePendingTransition(R.anim.activity_open_enter, R.anim.activity_open_exit)    <-tell how the next activity will appear, and haw thecurrent on disappear
		}
	});
	mButton.startAnimation(animationSet);  <-button will slide and fade as decided by the attributeset
	
You can also define the AnimationSet in xml and inflate it as follow (in the old days)

	<set xmlns:android="http://schemas.android.com/apk/res/android"
		 android:duration="@android:integer/config_shortAnimTime">
		 <translate
			  android:fromYDelta="0%"
			  android:toYDelta="-100%" />
		 <alpha
			 android:fromAlpha="1"
			 android:toAlpha="0"/>
	</set>

	AnimationSet animationSet = new AnimationUtils.loadAnimation(context, R.anim.slideoutbutton)
	animationSet.setAnimationListener(new Animation.AnimationListener(){
		@Override
		public void onAnimationEnd(Animation anmation){
			mButton.setVsibility(View.GONE);
			startActivity(new Intent(MainActivity.this, SubActivity.class));
			overridePendingTransition(R.anim.activity_open_enter, R.anim.activity_open_exit)    <-tell how the next activity will appear, and haw thecurrent on disappear
		}
	});
	mButton.startAnimation(animationSet);  <-button will slide and fade as decided by the attributeset