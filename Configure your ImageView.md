
they are of 3 classes

	photography : great when you have something very specific
	illustration : abstract concepts or methaphore
	iconography : they show the way
		
attribute explanation

	fit_center : make the image fit entierely inside the view, keep ratio, if the axis don't match the empty space is distributed on both side of the image (top and bottom or left and right)
	fit_start : make the image fit entierely inside the view, keep ratio, if the axis don't match the empty space is distributed after the image (on the bottom)
	fit_end : make the image fit entierely inside the view, keep ratio, if the axis don't match the empty space is distributed before the image (on the top)
	fit_xy : makethe image use the entiere view, change the ratio if necessary. Unless your imageView has a ratio close to the image, using this might be a bad idea
	center : display the image in the view with no scaling at all. If the image is larger than the view we will only see a small portion of it. 
	center_inside : attemps to center the imagein the view, and will scale it down to fit (=fit_center if the image is larger than the view).If the image is smaller than the viewit won't scale it up and the extra space will be homogeneuously distributed around the image. 
	center_crop :scale so that the width and the height exeed the dimensions of the view a little bit and the maximum possible of the image is taken and fit the view. Souvent utilisé pour les photos. Pour avoir des full-bleed images.
	matrix : when nothing fit. And mention translation, scaling, and rotation
	
to understand the different images attributes see this app, doc and video

	https://github.com/udacity/ud862-samples/tree/master/ImmersiveImages
	http://developer.android.com/reference/android/widget/ImageView.ScaleType.html
	https://www.udacity.com/course/viewer#!/c-ud862-nd/l-4816568580/m-4799140510
	
set 

	android:width="wrap_content" <- avoid setting a fix size here, and make your asset at theexact wanted size (for performance)
	android:height="wrap_content"
	android:maxWidth="wrap_content"
	android:maxHeight="wrap_content"
	android:adjustViewBounds="true"	 (will use maxWidth, maxHeight and minWidth, minHeight)
	
Github sample : ImmersivesImages min 15

	Usefull to choose the best image scaleType
	Make use of butterknife annotation to avoid having to do findviewbyid
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master