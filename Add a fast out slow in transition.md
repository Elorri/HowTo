# Add a fast out linear in transition with scale in size or opacity(for objects that leave the screen)

	is good for objects that moves accross the screen.
	section "Standard curve"  https://material.google.com/motion/duration-easing.html#duration-easing-natural-easing-curves
	This is the most common easing curve. Objects quickly accelerate and slowly decelerate between on-screen locations. It applies to growing and shrinking material, among other property changes.
	
	see "Relative Movement" https://material.google.com/motion/movement.html#movement-movement-in-out-of-screen-bounds
	Entering or exiting objects that move other on-screen elements do so along a smooth easing curve, so that they remain minimally disruptive and avoid eye-catching, dramatic movement. The standard curve is used for moving objects both in and out of the bounds of the screen. This curve has a slightly longer duration compared to independent objects.

	
According to Material design guidelines it is more natural to use arc transition or use an axis if a coordinate does not change

	https://material.google.com/motion/material-motion.html#material-motion-how-does-material-move
	see section "Real-world forces, like gravity, inspire an element’s movement along an arc rather than in a straight line." and "Material transformations follow an arc of movement."

Other names

	Standard curve 
	
interpolator

	FastOutSlowInInterpolator	

duration on mobile : 300ms	
	
# moving along an upward arc

	Rising against gravity in the real world requires effort. Elements moving upward on the screen should similarly depict effort during acceleration through a slower upward movement.
	see section "Arc upward" : https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds

# moving along a downward arc

	Falling objects in the real world are accelerated by gravity. Elements moving downward on screen should depict less effort through a faster downward movement.
	see section "Arc downward" : https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds

# moving along an axis

	These movements are simpler and may move at a slightly faster speed.
	see: "When not to arc" https://material.google.com/motion/movement.html#movement-movement-within-screen-bounds



## Add a fast out slow in transition 	is good for objects that moves accross the screen.

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
	
	
	

	
	
# Asymetrical transformation

Asymmetric transformations involve the width and height changes at different rates. 
They work best when multiple elements or position changes are involved.

To expand an object's size, begin transforming the width of an object slightly before transforming the height. To collapse an object's size, begin transforming the height slightly before the width.
Le petit carre devient un rectangle puis un carre again
see "Asymmetric transformations" https://material.google.com/motion/transforming-material.html#transforming-material-rectangular-transformation

Expand

	best start and end of duration for width : 0-280 ms
	best start and end of  duration for height : 50-375 ms

	
Collapse

	best start and end of  duration for width : 50-375 ms
	best start and end of  duration for height : 0-320 ms
	
The content it contain should have a constant aspect ratio to prevent unnatural stretching. See "Content (such as a full-width image) transforms at a constant aspect ratio, even as its container (such as a larger card) transforms asynchronously along a motion curve." https://material.google.com/motion/transforming-material.html#transforming-material-rectangular-transformation


# Symetrical transformation

Symmetrical transformations involve width and height changes occurring at the same rate. 
They are better for changes to a single element that occur along a single axis. Best suited to simple shape changes
Le petit carre reste un carre again.
 These transformations can have slightly shorter durations than asymmetric ones.
see "Symmetric transformations" https://material.google.com/motion/transforming-material.html#transforming-material-rectangular-transformation

Expand

	best start and end of duration for width : 0-300 ms
	best start and end of  duration for height : 0-300 ms

	
Collapse

	best start and end of  duration for width : 0-300 ms
	best start and end of  duration for height : 0-300 ms
	
The content it contain should have a constant aspect ratio to prevent unnatural stretching. See "Containers with full-bleed content (such as a full-bleed image) may expand synchronously." https://material.google.com/motion/transforming-material.html#transforming-material-rectangular-transformation	

# Radial transformation

	see "Radial transformations are symmetrical, circular visualizations that originate from a user’s point of touch. They are commonly used on circular surfaces that morph into other shapes." https://material.google.com/motion/transforming-material.html#transforming-material-rectangular-transformation
	Don’t use a radial transformation when transforming between two rectangular shapes.
	Don’t expand an oval’s width and height asynchronously.
	Don’t transform complex shapes.

Example

	Fab expanding into an arc see "During expansion, the floating action button moves in an arc towards its destination as it expands into a card." https://material.google.com/motion/transforming-material.html#transforming-material-radial-transformation
	
# with shared element transition

	While a surface is expanding, a significant number of elements should remain visible during the transition.
	Complex transitions should keep a single element visible.
	see section "All content elements are shared" https://material.google.com/motion/choreography.html

## with shared element transition with all content shared

put the shared transition on all elements
	
	Expand

		best start and end of incoming non shared content opacity : 75-225 ms
		
	Collapse

		best start and end of outgoing non shared content opacity : 0-75 ms
		
	Le detail s'en va vite mais apparait plus lentement.
	
## with shared element transition with Few or no content elements shared

put the shared transition on only one element.
When multiple elements remain visible during a transition, only the most important ones should be included. Some elements may disappear during the transition but reappear once the transition completes, if they are too distracting during the transition itself. see: "Guide the user’s focus to the next view using the most important shared element." https://material.google.com/motion/choreography.html#choreography-continuity

	Expand
		
		best start and end of incoming non shared element x-position : 0-275 ms
		best start and end of incoming non shared element y-position : 50-375 ms
		best start and end of outgoing non shared content opacity : 0-75 ms		
		best start and end of incoming non shared content opacity : 75-225 ms
		
	Collapse

		best start and end of incoming non shared element x-position : 75-375 ms
		best start and end of incoming non shared element y-position : 0-325 ms
		best start and end of outgoing non shared content opacity : 0-75 ms		
		best start and end of incoming non shared content opacity : 75-225 ms

## with shared element transition with no content elements shared

If there are no shared elements between views, anchor all crossfading elements to the surface’s vertical movement. The surface crops the content within.
put the shared transition on all elements and move them to a border

	Expand
		
		best start and end of incoming non shared element x-position : 0-275 ms
		best start and end of incoming non shared element y-position : 50-375 ms
		best start and end of outgoing non shared content opacity : 0-75 ms		
		best start and end of incoming non shared content opacity : 75-225 ms
		
	Collapse

		best start and end of incoming non shared element x-position : 75-375 ms
		best start and end of incoming non shared element y-position : 0-325 ms
		best start and end of outgoing non shared content opacity : 0-75 ms		
		best start and end of incoming non shared content opacity : 75-225 ms
	
	
# Joining & Dividing transformation

joining

	1. remove shadow
	2. make edges meet and margins overlap before the movement completes.
	
dividing

	1. remove shadow
	2. the pieces begin separation at the start of the movement.
	
see
	
	"Example of material joining and dividing"
	https://material.google.com/motion/transforming-material.html#transforming-material-joining-dividing


	
