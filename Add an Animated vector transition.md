## Add a Animated vector transition :good to animate icons


what you can animate

	translate
	scale
	rotate
	opacity
	color
	path				--> one restriction the shapes needs to have the same number of drawing commands to interpolate between the 2 states
	trim start/end		--> to take only one part of the path
	clip-path			--> apply a clip region to your drawing see https://github.com/udacity/ud862-samples/tree/master/HeartFill
	

### first create 2 drawable. Note : to get the path use ink scape and copy paste the path here

	<vector
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:height="24dp"
		android:width="24dp"
		android:viewportHeight="24"
		android:viewportWidth="24">
		<path
			android:name="cross"
			android:pathData="M6.4,6.4 L17.6,17.6 M6.4,17.6 L17.6,6.4"  <-space separated drawing command which use a subset of the SVG path data spec. M means move and draw a line from thispoint to the next. L means lift and don't draw a line
			android:strokeWidth="2dp"
			android:strokeLineCap="square"
			android:strokeColor="#999"			
			/>
	</vector>	
	
one for the tick

	<vector xmlns:android="http://schemas.android.com/apk/res/android"
			android:width="120dp"
			android:height="120dp"
			android:viewportWidth="@integer/viewport_width"
			android:viewportHeight="@integer/viewport_height">

		<group
			android:name="@string/groupTickCross"
			android:pivotX="@integer/viewport_center_x"
			android:pivotY="@integer/viewport_center_y">

			<path
				android:name="@string/tick"
				android:pathData="@string/path_tick"
				android:strokeWidth="@integer/stroke_width"
				android:strokeLineCap="square"
				android:strokeColor="@color/stroke_color"/>
		</group>
	</vector>	

one for the cross

	<vector xmlns:android="http://schemas.android.com/apk/res/android"
			android:width="120dp"
			android:height="120dp"
			android:viewportWidth="@integer/viewport_width"
			android:viewportHeight="@integer/viewport_height">
		<group
			android:name="@string/groupTickCross"
			android:pivotX="@integer/viewport_center_x"
			android:pivotY="@integer/viewport_center_y">
			<path
				android:name="@string/cross"
				android:pathData="@string/path_cross"
				android:strokeWidth="@integer/stroke_width"
				android:strokeLineCap="square"
				android:strokeColor="@color/stroke_color"/>
		</group>
	</vector>
	
create the ressource tickcross that will keep all animation data together

	<resources>

		<!-geometry -->
		<integer name="viewport_width">24</integer>
		<integer name="viewport_height">24</integer>
		<integer name="viewport_center_x">12</integer>
		<integer name="viewport_center_y">12</integer>
		<!--<string name="path_tick">M19.6,7 L10.4,16.2 M4.8,13.4 L9,17.6</string>-->
		<string name="path_tick">M4.8,13.4 L9,17.6 M10.4,16.2 L19.6,7</string>
		<!--<string name="path_cross">M17.6,6.4 L6.4,17.6 M6.4,6.4 L17.6,17.6</string>-->
		<string name="path_cross">M6.4,6.4 L17.6,17.6 M6.4,17.6 L17.6,6.4</string>
		<integer name="stroke_width">2</integer>

		<!-names -->
		<string name="tick">tick</string>
		<string name="cross">cross</string>
		<string name="groupTickCross">groupTickCross</string>

		<!-drawing -->
		<color name="stroke_color">#999</color>

		<!-timing -->
		<integer name="duration">450</integer>

	</resources>
	
create animators for each of the changing step res/animator/cross_to_tick.xml

	<objectAnimator
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:propertyName="pathData"
		android:valueFrom="@string/path_cross"
		android:valueTo="@string/path_tick"
		android:duration="@integer/duration"
		android:interpolator="@android:interpolator/fast_out_slow_in"
		android:valueType="pathType" />
		
tick to cross

	<objectAnimator
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:propertyName="pathData"
    android:valueFrom="@string/path_tick"
    android:valueTo="@string/path_cross"
    android:duration="@integer/duration"
    android:interpolator="@android:interpolator/fast_out_slow_in"
    android:valueType="pathType"/>
	
rotate cross to tick

	<objectAnimator
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:propertyName="rotation"
		android:valueFrom="-180"
		android:valueTo="0"
		android:duration="@integer/duration"
		android:interpolator="@android:interpolator/fast_out_slow_in" />
	
rotate tick to cross

	<objectAnimator
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:propertyName="rotation"
		android:valueFrom="0"
		android:valueTo="180"
		android:duration="@integer/duration"
		android:interpolator="@android:interpolator/fast_out_slow_in" />

last create an animated-vector in drawable/avd_cross_to_tick.xml wihch will connect the image to the animator

	<animated-vector
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:drawable="@drawable/ic_cross">

		<target
			android:name="@string/cross"  <-target the crosspath
			android:animation="@animator/cross_to_tick" /> <-specify an animator to run on it

		<target
			android:name="@string/groupTickCross"
			android:animation="@animator/rotate_cross_to_tick" />

	</animated-vector>
	
res/drawable/avd_tick_to_cross.xml

	<animated-vector
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:drawable="@drawable/ic_tick">

		<target
			android:name="@string/tick"
			android:animation="@animator/tick_to_cross" />


		<target
			android:name="@string/groupTickCross"
			android:animation="@animator/rotate_tick_to_cross" />

	</animated-vector>
	

finally in MainActivity.java

	AnimatedVectorDrawable crossToTick = (AnimatedVectorDrawable) getDrawable(R.drawable.avd_tick_to_cross);
	imageView.setImageDrawable(crossToTick);
	crossToTick.start();
	
Github sample: TickCross

	https://github.com/udacity/ud862-samples/tree/master/TickCross
	
Github sample : AndroidDesignTrimPath min 21. 

	use animated vectors, sembling a hand writing, the word "Android Design" is divided in different paths and asigned an effect.
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
	
Github sample : HeartFill min 21

	Fill or empty the heart, and we can see the heart being filled like a glass of water. Could be useful for open bee lab.
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
	
Github sample : TickCross min 21. 

	Very simillar to HeartFill, but tranform one vector to another
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
