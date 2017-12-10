the start and end state are called scenes and they are simple xml layout.

	scene1.xml with an info imagebutton
	scene2.xml with a close info cross imagebutton
	
now in the onClick handler. Note that android by default will fade elements, and ove elements if they stay on screen when you use that, which iscool
	
	TransitionManager.go(
			Scene.getSceneForLayout((ViewGroup)findViewById(android.R.id.content),
					R.layout.activity_main_scene_info, //change the current scene by this one
					MainActivity.this));
					
to customise the transition that not everything happend all at once add TransitionInflater

        TransitionManager.go(
                Scene.getSceneForLayout((ViewGroup) findViewById(android.R.id.content),
                        R.layout.activity_main_scene_info, //change the current scene by this one
                        MainActivity.this));

        TransitionInflater.from(this)
                .inflateTransition(R.transition.defaultToInfo));

and add an the defaultToInfo.xml

	<transitionSet xmlns:android="http://schemas.android.com/apk/res/android">
		<changeBounds android:duration="250">
			<targets>
				<target android:targetId="@id/image"/>
			</targets>
		</changeBounds>
		<fade android:startDelay="300" android:duration="250">
			<target android:targetId="@id/description"/>
			<target android:targetId="@id/close_button"/>
		</fade>
	</transitionSet>