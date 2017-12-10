# Add a linear out slow in transition with scale in size or opacity

Deceleration curve (“Easing out”)

Objects enter the screen at full velocity from off-screen and slowly decelerate to a resting point.
During deceleration, objects may scale up either in size (to 100%) or opacity (to 100%). In some cases, when objects enter the screen at 0% opacity, they may slightly shrink from a larger size upon entry.
see section "Deceleration curve" https://material.google.com/motion/duration-easing.html#duration-easing-natural-easing-curves

Other names

	Deceleration curve 
	Easing out curve
	
interpolator

	LinearOutSlowInInterpolator
	
duration

	225ms.
	
According to Material design guidelines it is more natural to use arc transition or use a move along a single axis transition.
see "Objects entering and exiting the screen also move along a single axis." https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds
see "Entering the screen" https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds

	
## Add a linear out slow in transition	is good for objects that enter the screen. means full velocity
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
	
	

	