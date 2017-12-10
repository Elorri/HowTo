##  property animation  (IceCreamSandwitch api 14)			

even more you can now animate any property on any object like a button textColor

        ObjectAnimator.ofObject(		//the animator main puropose is to interpolate between start and end state and return a correct object.
                mButton,                //Object we are animating
                "textColor",            //property to animate
                new ArgbEvaluator(),    //interpolation function this tell the mButton what color to set ranging between red and black over the course of 1 second
                Color.BLACK,            //startvalue
                Color.RED)              //endvalue
                .setDuration(1000)
                .start();