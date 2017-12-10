# Add elevations

https://www.udacity.com/course/viewer#!/c-ud855-nd/l-3940839262/m-4331460077
Before Lolipop elevation is not rendered. To solve this problem, we will use Cardview from the support library.
 Changing the elevation of the card will cast a larger shadow. Elevation in cardview works different from elevation in lolipop
	view with higher elevation obscure view with lower elevation and it's nested childrens
	views with transparent background don't cast shadow.
	views contained in transparents views won't cast shadow neither
	because of that always avoid using LinearLayout and creating hierarchy, use RelativeLayout and SpaceView
 We can also changethe radius of the corners
 A CardView is a layout that draw stuff around others layout, it works differently:
	there is 2 background color attribute: 
		one for the card layout (transparent by default)
		one for the card frame (white by default)
	There is 2 padding
		padding between the card frame and the cardLayout.
		padding between the card content and the card frame.
 Use app:cardPreventCornerOverLap="false" for better rendering.
 By default thecardview hide itself if no content, in sunshine we need not to hide itself, but it's parent.
	
	
	to see all standard elevations go
	
		https://www.google.com/design/spec/what-is-material/elevation-shadows.html#
		
	if you need to control shadow behavior you can use a custom outline provider shadow

		http://developer.android.com/training/material/shadows-clipping.html