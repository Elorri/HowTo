# Add elevations

	Shadow comes in lolipop as elevation
		view with higher z values cast higher and softer shadows on lower views. Plus hautes et floues.
		view with higher z values occludes views with lower z values.
		z value does not affect the view size.
		z elevation is relative to the parent
	Elevation z is for static views.
	Elevation and Transition are uselly used to respond to touch.
	
	Resting elevations does not vary from one app to another but can vary across platforms and devices (phone/tablet, TV, desktop)
		
	to see all standard elevations go
	
		https://www.google.com/design/spec/what-is-material/elevation-shadows.html#
		
	if you need to control shadow behavior you can use a custom outline provider shadow

		http://developer.android.com/training/material/shadows-clipping.html
		
	
# Components

Dialog

	resting elevation 24dp
	dynamic elevation 

Picker

	resting elevation 24dp
	dynamic elevation 


Nav drawer

	resting elevation 16dp
	dynamic elevation 


Right drawer

	resting elevation 16dp
	dynamic elevation 


Modal bottom Sheet

	resting elevation 16dp
	dynamic elevation 

Floating action button 

	resting elevation 6dp
	dynamic elevation 12dp

Sub menu

	resting elevation 9dp (+1dp for each sub menu)
	dynamic elevation 

Bottom navigation bar

	resting elevation 8dp
	dynamic elevation 

Menu

	resting elevation 8dp
	dynamic elevation 

Card

	resting elevation 2dp
	dynamic elevation 8dp

Raised button

	resting elevation 0dp
	dynamic elevation 2dp

Snackbar

	resting elevation 6dp
	dynamic elevation 

App Bar

	resting elevation 4dp
	dynamic elevation 

Refresh indicator

	resting elevation 3dp
	dynamic elevation 


Quick entry / Search bar 

	resting elevation  2dp
	dynamic elevation (scrolled state) 3dp

Switch

	resting elevation 1dp
	dynamic elevation 
	
	
# Avoiding elevation interference

	Components with responsive elevations may encounter other components as they move between their resting elevations and dynamic elevation offsets. Because material cannot pass through other material, components avoid interfering with one another any number of ways, whether on a per-component basis or using the entire app layout.
	On a component level, components can move or be removed before they cause interference. For example, a floating action button (FAB) can disappear or move off-screen before a user picks up a card, or it can move if a snackbar appears.
	On the layout level, design your app layout to minimize opportunities for interference. For example, position the FAB to one side of stream of a cards so the FAB won’t interfere when a user tries to pick up one of cards.





		
