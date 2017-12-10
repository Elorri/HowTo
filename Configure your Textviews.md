# TextViews

	text characters like letters are design/drawn using 4dp cell grid --> padding marging should be multiple of 4. more infos :https://www.google.com/design/spec/resources/sticker-sheets-icons.html#
	For text with big size, sometimes we dont want to allow it to become bigger (and destroy our desktop) when the user set the system font set to "large".
	In that case : set the textSize with dp value instead of sp.
	Test : Set the system font to large and check if all views are visible.
	
	reading comfort : 45 to 75 characters max per line don't exceed this
	
# Fonts

	Use Roboto (a font design for high density screen and with good peformance) no need to specify that the font is Roboto becuse it's specified in the theme. it's enough to add sans-serif-condensed.
	Use android:textAppearance="?android:textAppearanceSmall" instead of textSize=""
		
	android:fontFamily="sans-serif-light"
	android:fontFamily="sans-serif-condensed"
	
	android:textColor="@android:color/white"
	android:textColor="?textColorSecondary"
	
text type roboto

	has been specifically device for a variety of screens you can use it for your entiere app
	include a bunch of familly : roboto, roboto condensed, roboto slab, roboto mono
	include a bunch of weight : thin (100), light(300), regular(400), medium(500), bold(700), black(900). Not every weight is available in a familly. roboto condensed doesn't includethin and black weight.
	include a bunch of variant : condensed, slab
	include a bunch of style : Normal, italic
	it is a sans-serif fonts means without serif. serif are common in books and are considered confortable for long form reading
	use sans-serif most of the time, and use serif sparingly for large title
	anti-aliasis can make serif look bluerry, so don't use it with small text

	
textview styling

	android:fontFamilly : for familly or weight
	android:textStyle: for weight and style
	prefers to put weight in the fontFamilly attribute because it gives you the possibility to put number instead of words. ex 450 instead of regular
	
example

	<Textview
		android:fontFamilly="sans-serif"
		android:textStyle="italic" />
	<Textview
		android:fontFamilly="sans-serif-light"
		android:textStyle="italic" />
	<Textview
		android:fontFamilly="sans-serif-condensed"
		android:textStyle="italic" />
	<Textview
		android:fontFamilly="sans-serif-thin"
		android:textStyle="italic" />
	<Textview
		android:fontFamilly="sans-serif-medium"
		android:textStyle="italic" />		

	
font-size

	user can use bigger font in accessibility
	16sp=16dp in a 100% scale
	16sp=20dp in a 125% scale
	font with a large x-height tend to be more suitable for body text.
	you can control the leading : textview lineSpacingMultiplier or lineSpacingExtra
	
choosing fonts

	limit font palette to 2 max. 1 for your branding and roboto foreverything else
	try on several density devices if you can. Especially look at the serif
	
to add a font add

	add an assets directory under src/main/ ->src/main/assets

download a font :most of them are available with open sources licences

	https://www.google.com/fonts
	ex: Courgette-regular.ttf
	
to use your front in a fragment, instantiate typeface in the onAttach method. Note: seems that when using with an activity it should be in lower-case, and the file too courgette-regular.ttf

	public void onAttach(Activity activity){
		super.onAttach(activity);
		courgette=Typeface.createFromAsset(getActivity().getAssets(), "Courgette-regular.ttf")
	}
	
and use it in the onCreateView

	aTextView.setTypeFace(courgette);

	
	
# Fonts standards (predifine attribute, try to use them first)

Material design default styles were develop to balance content densities and reading comfort under typical usage conditions.
https://www.google.com/design/spec/style/typography.html#typography-styles

	android:textAppearance="@style/TextApparance.AppCompat.Display4" : Roboto sans-serif-light 112sp
	android:textAppearance="@style/TextApparance.AppCompat.Display3" : Roboto sans-serif-regular 56sp
	android:textAppearance="@style/TextApparance.AppCompat.Display2" : Roboto sans-serif-regular 45sp
	android:textAppearance="@style/TextApparance.AppCompat.Display1" : Roboto sans-serif-regular 34sp
	android:textAppearance="@style/TextApparance.AppCompat.Headline" : Roboto sans-serif-regular 24sp
	android:textAppearance="@style/TextApparance.AppCompat.Title" : Roboto sans-serif-medium 20sp
	android:textAppearance="@style/TextApparance.AppCompat.Subheading" : Roboto sans-serif-regular 16sp (Device), Roboto sans-serif-regular 15sp (Desktop)
	android:textAppearance="@style/TextApparance.AppCompat.Body2" : Roboto sans-serif-medium 14sp (Device), Roboto sans-serif-medium 13sp (Desktop)
	android:textAppearance="@style/TextApparance.AppCompat.Body1" : Roboto sans-serif-regular 14sp (Device), Roboto sans-serif-regular 13sp (Desktop)
	android:textAppearance="@style/TextApparance.AppCompat.Caption" : Roboto sans-serif-regular 12sp 
	android:textAppearance="@style/TextApparance.AppCompat.Button" : Roboto sans-serif-medium all-caps 14sp 
	
	android:textAppearance="?android:textAppearanceLarge" : Roboto 22sp 
	android:textAppearance="?android:textAppearanceMedium" : Roboto 18sp 
	android:textAppearance="?android:textAppearanceSmall" : Roboto 14sp ?textColorSecondary
	

	
# Fonts sizes shouldn't be too much (3 or 4 max)

    <!-- Fonts sizes -->
    <dimen name="text_size_xsmall">11sp</dimen>
    <dimen name="text_size_small">12sp</dimen>
    <dimen name="text_size_normal">14sp</dimen>
    <dimen name="text_size_medium">18sp</dimen>
    <dimen name="text_size_xlarge">20sp</dimen>
    <dimen name="text_size_xxlarge">24sp</dimen>
    <dimen name="text_size_xxxlarge">40sp</dimen>	
	
	Text size micro 12sp
	Text size small 14sp
	Text size medium 18sp
	Text size large 22 sp
	
	
Github sample : MD_Typograhical_Scale min 15. Display all those styles from the biggest to the smallest. Use a custom asset : Courgette-Regular.ttf for the 2 first styles above.

	style="@android:style/TextAppearance.Material.Display4"
	style="@android:style/TextAppearance.Material.Display3"
	style="@android:style/TextAppearance.Material.Display2"
	style="@android:style/TextAppearance.Material.Display1"
	style="@android:style/TextAppearance.Material.Headline"
	style="@android:style/TextAppearance.Material.Title"
	style="@android:style/TextAppearance.Material.Subhead"
	style="@android:style/TextAppearance.Material.Body2"
	style="@android:style/TextAppearance.Material.Body1"
	style="@android:style/TextAppearance.Material.Caption"
	style="@android:style/TextAppearance.Material.Button"
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
