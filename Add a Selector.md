### Drawable states list

	are in drawable
	they list the different appearance of a graphic element

states can be

	default
	pressed
	checked
	focus
	a combination of those state
	
exemple checkbox.xml

	<selector xmlns:android="http://schemas.android.com/apk/res/android">
		<item android:state_pressed="true" 
			  android:state_checked="true"  android:drawable="@drawable/box_checked_pressed"/>
		<item android:state_pressed="true"  android:drawable="@drawable/box_pressed"/>
		<item android:state_checked="true"  android:drawable="@drawable/box_checked"/>
		<item android:state_focused="true"  android:drawable="@drawable/box_default"/>
	</selector>

android traverses the selector from top to bottom and stop when it reach the first state that match, means multiple states should be above general ones
