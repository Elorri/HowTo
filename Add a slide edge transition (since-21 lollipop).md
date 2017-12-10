##  slide edge transition(Android 4.4 api 21)	: slide the view out of the top of the screen

		Slide slide=new Slide();
		slide.setSlideEdge(Gravity.TOP);
		ViewGroup root=(ViewGroup)findViewById(android.R.id.content);
		TransitionManager.beginDelayedTransition(root, slide);  //start state is captured here. (start state for all the views of the viewgroup)
		imageView.setVisibility(View.INVISIBLE); //just after the beginDelayedTransition we set the end state we want of anyview of the viewgroup
		
Github sample : L4_06_Q min 21

	master_detail view, the detail view is slide in, and the master view is fade
	combined with a shared element trasition
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
Github sample : TransitionDemo min 21. 

	Example of Slide edge transition
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	
Github sample : Unsplash min 21

	beautiful picture from unsplash Free (do whatever you want) high-resolution photos.
	example of shared element trasition with arc motion for the selected picture
	others elements disapear by explosion "explose"
	status bar and navigation bar are excluded in mainactivity grid
	top slide edge transition when reentering mainactivity grid (means elements are reentering the grid from top, override the default implode in this case)
	no transition the first time we enter mainactivity grid
	interesting custom ForegroundImageView
	interesting custom ThreeTwoImageView
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master