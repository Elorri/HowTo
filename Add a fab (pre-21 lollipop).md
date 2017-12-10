# Fab

	56dp or 40dp diameter
	resting elevation 6dp
	pressed elevation 12dp
	

	
## Fab for Pre-Lolipop devices
		
	to make your own fab you need an ImageButton

		<ImageButton
			android:layout_width="56dp"
			android:layout_height="56dp"
			android:background="@drawable/oval_shape"
			android:src="@drawable/fab_plus"
			android:elevation="6dp"        />

	an oval drawable oval_shape.xml

		<shape
			xmlns:android="http://schemas.android.com/apk/res/android"
			android:shape="oval">
			<solid android:color="?attr/colorAccent"/>
		</shape>

	a plus vector

		<vector
			xmlns:android="http://schemas.android.com/apk/res/android"
			android:height="24dp"
			android:width="24dp"
			android:viewportHeight="24"
			android:viewportWidth="24">
			<path
				android:fillColor="#FFF"
				android:pathData="M19,13H13V19H11V13H5V11H11V5H13V11H19V13Z"/>
		</vector>
		
	feedback in response to touch is done by 2 effects

		ripple effect
		rising effect 

	if you want the ripple effect, change your oval_shape to a ripple

		<ripple
			xmlns:android="http://schemas.android.com/apk/res/android"
			android:color="?android:colorControlHighlight">
			<shape    android:shape="oval">
				<solid android:color="?attr/colorAccent"/>
			</shape>
		</ripple>
		
	to make the button raise when the user touch the button. Note that we use attribute tranlationZ instead of elevation. android will add current value of translation z and the base elevtion we set in code to calculate the next elevation

			<ImageButton
				android:layout_width="56dp"
				android:layout_height="56dp"
				android:background="@drawable/oval_shape"
				android:src="@drawable/fab_plus"
				android:elevation="6dp"
				android:stateListAnimator="@anim/fab_raise"
			/>
			<selector xmlns:android="http://schemas.android.com/apk/res/android">
				<item android:state_enabled="true" android:state_pressed="true">
					<objectAnimator
						android:duration="@android:integer/config_shortAnimTime"
						android:propertyName="tranlationZ"
						android:valueTo="8dp"
						android:valueType="floatType"/>
				</item>

				<item>
					<objectAnimator
						android:duration="@android:integer/config_shortAnimTime"
						android:propertyName="tranlationZ"
						android:valueTo="0dp"
						android:valueType="floatType"/>
				</item>
			</selector>