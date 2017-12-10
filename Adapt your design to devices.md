# Adaptive design

checklist

	balanced use of space
	reading comfort : 45 to 75 characters max per line don't exceed this
	image quality
	maintaing context
	aesthetic

break points

	choose them based on the content they will have is better approach than based on the devices out there
	
change number of gridview column when on phone or tablet

	<GridView android:numColumns="@integer/grid_columns">
	res/values/integers.xml <integer name="grid_columns">1</interger>
	res/values-w600dp/integers.xml <integer name="grid_columns">3</interger>
	
to have a dimen match parent in res/values/dimens.xml
	<dimen name="button_width">@dimen/match_parent</dimen>
	<item name="match_parent" format="integer" type="dimen">-1</item>
	
how to know witch layout to inflate ?

	put a boolean in the dimen ressource
	
and use it as follow

	int layoutToInflate = getRessources().getBoolean(R.bool.multicolumn) ? R.layout.item_tile : R.layout.item_card;
	
keylines for phones

	keyline1=16dp
	keyline2=72dp	
	
keylines for tablettes

	keyline1=24dp
	keyline2=80dp	
	
very useful for the toolbar
	
	<Toolbar contentInsetStart="@keyline2">
	
if you want an activity to appear in a dialog on tablet but not on phone to do that we create a theme and in res/values/styles.xml we put

	<resources>
		<style name="MyTheme" parent="BaseTheme">
			<!-Customize your theme here. -->
		</style>
		<style name="BaseTheme" parent="Theme.AppCompat"/>
	</resources>

this allow us to put this for tablet in res/values-sw600dp/styles.xml

	<resources>
		<style name="BaseTheme" parent="Theme.AppCompat.Dialog"/>
	</resources>
	
list of popular devices

	https://design.google.com/devices/
	
best approach for removing unwanted space

	https://www.udacity.com/course/viewer#!/c-ud862-nd/l-4964230471/m-4904228662
	
show additional content on the screen

	master on small device
	master_detail view on larger device

or 
	
	offscreen navigation drawer on small device
	pinned navigation drawer on larger device
	
reflow content switch from ... on small device

	one column grid
	item grid card backgroud completely colored = tile
	small appbar height hamburger, title, and action menu on the same row

to ...  on larger device
	
	multiple columns
	item grid card background half colored, text below = card
	raised appbar height, keep hamburger and action menu on top, but title below
	
reflow on same device from ...

	in portrait put a top image with a 3:2 aspect ratio
	fab on the edge of the image and detail
	
to ...

	in landscape mode put a left image width of 1/3 of the total width of the screen
	fab on the bottom right corner
	
expand from ...  on phone

	a big toolbar
	with text below
	
to 

	a big toolbar
	with text inside layout with a max width (like a piece of paper) or margin, like a white piece of paper
	rest of space being transparent or filled with a full bleed image+++