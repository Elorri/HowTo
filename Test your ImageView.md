
Given I have an ImageView set up as follow

	android:width="wrap_content" <- avoid setting a fix size here, and make your asset at theexact wanted size (for performance)
	android:height="wrap_content"
	android:maxWidth="40dp"
	android:maxHeight="40dp"
	android:adjustViewBounds="true"	 (will use maxWidth, maxHeight and minWidth, minHeight)
	
And I have an asset whose size in the drawable/mdpi is 32pixels x 32px (= 32dp x 32dp in the case of mdpi resolution)
When I display the image in any device (phone, tablet,...)
the imageView width and height should be 32dp x 32 dp.

Other possible test : 

	test that adjustViewBounds is specified


Old Notes : 

if your assets have the correct 
	Feat : Try to have an image (=asset) that already have the requiered size, to avoid calculation and for better performance.
		Si l'image est déjà à la taille en dp demandée par le designer, il n'est pas necessaire de donner une taille à l'imageView, use wrap_content.
		Comment savoirsi c'est la même taille ? aller dans drawable/mdpi (la + petite resolution) et regarder la taille de l'image. si elle fait 32pixels x 32px alors elle est 32dp x 32 dp.	
	Test : Create a test that test that your ImageView has the requiered lenght and height
	
	Feat : for performance specify the limit size of an image
		maxWidth
		maxHeight
		adjustViewBounds (will use maxWidth, maxHeight and minWidth, minHeight)
	Test : the limit is specified