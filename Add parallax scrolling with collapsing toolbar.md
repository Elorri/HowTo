## Parallax srolling =  Scrolling in parallel
		= when we have several level of views scrolling at different speed, it's one way to create an illusion of depth in material design and it's possible with RecyclerView for devices abouve HoneyComb, the app will continue to run on Gingerbread without parallax srolling.
		Cad l'ensemble de la detailActivity au lieu de rester figée, va scroller à la 1/2 de lavitesse de scroll de la listview (enfin recycler view).	
## parallax effect in a collapsing toolbar: the foreground move faster than the background, providing a sense of depth to the scene

		<ImageView
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			android:scaleType="centerCrop"
			android:src="@drawable/eclairs"
			app:layout_collapseMode="parallax"
        />
		
Github sample : ApplyPaletteDemo min 15 and ScrollEventsDemo min 15 they are identical

	containt a collapse tool bar without image and a recycler view
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master