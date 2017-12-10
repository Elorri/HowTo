	ldpi = low density devices 120 dpi (dot per inch), 1dp=0.75px  <-very small screen, in most case don't implement them
	mdpi = medium density devices 160dpi, 1dp=1px
	hdpi = high density devices 240dpi, 1dp=1.5px
	xhdpi = extra high density devices 320dpi, 1dp=2px
	xxhdpi = extra extra high density devices 480dpi, 1dp=3px
	xxxhdpi = extra extra extra high density devices 640dpi, 1dp=4px    <-very big screen, in most case don't implement them
	
to access sdk assets ex:

	android:drawableLeft="@android:drawable/ic_menu_share"
	
to create your own. On part de l'image/asset la moins dense mdpi et on cree des images de + en + dense. why mdpi ? because 1 dp = 1pixel at that density. Following thoses rules if we start with a net image of lets say 48x48px in the mdpi directory, we need images of the follwing sizes in drawables folders.
		mdpi = 48x48dp
		hdpi = 72x72px
		xhdpi = 96x96px
		xxhdpi = 144x144px
		xxxhdpi =  192x192px
	
in most case just create assets for 

		mdpi
		hdpi
		xhdpi
		xxhdpi
		
you can even create only for them ... and android will deduce the smaller resolution (android downscaling algorithm is optimize for speed not perfect scaling), but it's not ideal. if you have to choose provide the higher density.

		xhdpi
		xxhdpi

drawables folders

	in drawable only for xml drawables
	in drawable-nodpi folder, images that shouldn't scale like background.
	in drawable-mdpi-ja/location.png for japanese graphic asset			
		
Common assets sizes

	launch icon in mipmap : 
	mdpi = 48x48dp
	hdpi = 72x72px
	xhdpi = 96x96px
	xxhdpi = 144x144px
	xxxhdpi =  192x192px

	icons in drawable : 
	mdpi = 144x144px
	hdpi = 216x216px
	xhdpi = 288x288px
	xxhdpi = 432x432px
	xxxhdpi =  non defini

	notification icones in drawable : 
	mdpi = 32x32px
	hdpi = 48x48px
	xhdpi = 64x64px
	xxhdpi = 96x96px
	xxxhdpi = non defini

	title icon avec ecriture en blanc tranparent (seul la hauteur compte 32px)
	mdpi = 143x32px
	hdpi = 215x48px
	xhdpi = 287x64px
	xxhdpi = 430x96px
	xxxhdpi = non defini
		
to create assets for all resolutions use

	Tool : Use Android studio ImageAsset 
	https://romannurik.github.io/AndroidAssetStudio/