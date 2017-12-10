# Add a fast out linear in transition with scale in size or opacity(for objects that leave the screen)

Objects leave the screen at full velocity. They do not decelerate when off-screen.
They accelerate at the beginning of the animation and may scale down in either size (to 0%) or opacity (to 0%). In some cases, when objects leave the screen at 0% opacity, they may also slightly scale up or down in size.
see section "Acceleration  curve" https://material.google.com/motion/duration-easing.html#duration-easing-natural-easing-curves

Other names

	Acceleration curve 
	Easing in curve
	
interpolator

	FastOutLinearInInterpolator
	
duration

	195ms


According to Material design guidelines it is more natural to use arc transition or use a move along a single axis transition.
see "Objects entering and exiting the screen also move along a single axis." https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds
see "Permanently leaving the screen" https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds



With material, as objects move their acceleration and deceleration aren't equals. To achieve this you use an interpolator. How to create an interpolator ?

	interpolator=(Interpolator)Class.forName(PACKAGE+interpolatorName).newInstance(); or just new Interpolator()
	textview.animate().setInterpolator(interpolator)
		.setDuration(duration)
		.setStartDelay(500)
		.translationYBy(-metrics.heightPixels)  <-move the animation from the bottom of the screen
		.start();
		
to choose a good transition interpolator use this app

	https://github.com/udacity/ud862-samples/tree/master/InterpolationDemo
	http://developer.android.com/reference/android/view/animation/Interpolator.html
	
Github sample : CoordinatedMotion - how to display new surfaces and element. A menu with the following ... is given. also a good exemple of shared element.
	
	multiple elements (genre de liste view qui apparait)
	multiple incoherent elements
	curved motion
	size changes
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
Github sample : InterpolationDemo min 15

	Help us choose the best interpolator to make an element enter the screen, wheather it's are rebouncing or slow in
	Also Make use of butterknife annotation to avoid having to do findviewbyid
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
	
## Add a fast out linear in transition	is good for objects that leave the screen.
(same instructions "Add a fast out slow in transition" with different interpolator)


Github sample : CoordinatedMotion - how to display new surfaces and element. A menu with the following ... is given. also a good exemple of shared element.
	
	multiple elements (genre de liste view qui apparait)
	multiple incoherent elements
	curved motion
	size changes
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
Github sample : InterpolationDemo min 15

	Help us choose the best interpolator to make an element enter the screen, wheather it's are rebouncing or slow in
	Also Make use of butterknife annotation to avoid having to do findviewbyid
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master