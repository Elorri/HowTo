## Fab for Lolipop devices

	in layout.xml using design library

		<android.support.design.widget.FloatingActionButton
		app:fabSize="normal"  			<-"normal=56dp"  "mini=40dp"
		app:elevation="6dp"				<-resting elevation	
		app:layout_gravity="end"
		app:pressedTranslationZ="12dp"	<-pressed elevation
			
		android:id="@+id/fab"
		android:src="@drawable/fab_plus"
			
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_margin="16dp"/>
		
		
	to use this you need the appcompat theme, and elevation should work

		<style name="AppTheme" parent="Theme.AppCompat.Light"></style>
		
	it won't work with the old paradoxally (yes i know it's strange)

		<style name="AppTheme" parent="android:Theme.Material.Light"></style>



Github sample : FabDemo min 21

	Fab with imagebutton or librariry fab with raise (shadow) and ripple effect, if the vector is replaced by a png it could be available for api < 21. 
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master