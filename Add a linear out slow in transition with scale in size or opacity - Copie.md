# Add a fast out linear in transition with scale in size or opacity(for objects that leave the screen)

Objects leave the screen at full velocity. They do not decelerate when off-screen.
They accelerate at the beginning of the animation and may scale down in either size (to 0%) or opacity (to 0%). In some cases, when objects leave the screen at 0% opacity, they may also slightly scale up or down in size.
see section "Acceleration  curve" https://material.google.com/motion/duration-easing.html#duration-easing-natural-easing-curves

Other names

	Acceleration curve 
	Easing in curve
	
interpolator

	FastOutLinearInInterpolator

