# 1  BASE   API level (1|2)   Version(Android 1.0|Android 1.1) October 2008
# 2  CUPCAKE   API level (3)   Version(Android 1.5) May 2009
# 3  DONUT   API level (4)   Version(Android 1.6) September 2009
# 4  ECLAIR   API level (5|6|7)   Version(Android 2.0|Android 2.1.x) November 2009
# 5  FROYO   API level (8)   Version(Android 2.2.x) June 2010
# 6  GINGERBREAD   API level (9|10)   Version(Android 2.3|Android 2.3.4) November 2010
# 7  HONEYCOMB   API level (11|12|13)   Version(Android 3.0.x|Android 3.2) February 2011
	was the first android release to support tablets
	was the first to support fragments. The fragment by managing the lifecycle like the activities, does a lot of work for us. Exple : remembering state of UI elements.
	Scrolling in parallel =parallax srolling
		= when we have several level of views scrolling at different speed, it's one way to create an illusion of depth in material design and it's possible with RecyclerView for devices abouve HoneyComb, the app will continue to run on Gingerbread without parallax srolling.
		Cad l'ensemble de la detailActivity au lieu de rester figée, va scroller à la 1/2 de lavitesse de scroll de la listview (enfin recycler view).	

# 8  ICE_CREAM_SANDWICH   API level (14|15)   Version(Android 4.0|Android 4.0.4) October 2011

	Roboto : a font design for high density screen and with good peformance.
	Make use of GridLayout introduced in Icecream sandwish realease. API 14 (Material Design Standard)
	Possibility to animate any view with the method builder animate(). (mButton.animate())

# 9  JELLY_BEAN   API level (16|17|18)   Version(Android 4.1, 4.1.1|Android 4.3) June 2012
# 10  KITKAT   API level (19)   Version(Android 4.4) October 2013
	Transitions to move the user attention somewhere android 4.4 and in android L we made them easy to use.
	Add more scene and transitions like slide. Ex to slide the view out of the top of the screen. Slide edge transition.
	Pas d'élévation.
	Pas de setBackgroundTint mais setTint
# 11  KITKAT_WATCH   API level (20)   Version(Android 4.4W) June 2014 November 2014
	AppCompat library can be used but it's uncomplete. (compatible since api v7)
# 12  LOLLIPOP   API level (21|22)   Version(Android 5.0|Android 5.1) 
	AppCompat library is complete. 
	Toolbar Widget introduced in Android 5.0 API 14 (Material Design Standard)
	Lolipop permet l'utilisation de riple : make use of it.
	VectorDrawable (but not available before lolipop)
	library MrVector: replace VectorDrawable a partir d'android v7.
	Use of Cardview for prelolipop devices, elevation instead(Material Design Standard).
	Elevation => shadow. Before Lolipop elevation is not rendered. To solve this problem, we will use Cardview from the support library.
	Permission all at once
	battery life Doze
	fingerprint sensor not uniform
	RAM amount gives quantity used only
	fingerprint unlock phone

# 13  MARSHMALLOW   API level (23)   Version(Android 6.0) 
	runtime permissions : onRequestPermissions
	RAM amount gives max and average
	fingerprint sensor uniform
	fingerprint can be use for purchase	
# 14  NOUGAT   API level (24)   Version(Android 7.0) 
	multitasks - split screen tablettes : manifest with layout attribute
	instant app (possible for jellybeans devices)
	direct reply from notifications
	batterylife: doze is even better
	android studio instant runs