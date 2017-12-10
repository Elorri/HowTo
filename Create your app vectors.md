

	Les vecteurs :
	bipmap :quand on les agrandit elles deviennent floues.
	vector : restent joli.


	How to use the VectorDrawable :
	1 convert svg into VectorDrawable xml file. Use this link:
	http://inloop.github.io/svg2android/
	2 copy paste your vector.xml in drawable-v21
	3 in the imageView. Set the background to "@drawable/vector_android"
	4 to modify the color go to vector.xml 
		<vector 
			android:tint=@color/colorBlack>
	5 for prelolippop device, in drawable
		create a vector.xml as a selector pour le moment
			<selector>
				<item android:drawable="@drawable/ic_launcher"/>
			</selector>
	6 go to https://github.com/telly/MrVector
	https://www.youtube.com/watch?v=uenoqUpxgI8

	7 for animated vectors
	https://www.youtube.com/watch?v=JoFkPh3qdM	
	
you can also use vectors and thoses programs, they create svg = Scalable Vector Graphic, newer versions of android can use format similar to svg

	InkScape
	Illustrator
	Sketch
	
to create a Vector in android studio

	Tool : Use Android studio VectorAsset 