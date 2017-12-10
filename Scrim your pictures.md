when writing over images that will be downloaded dynamically, if we use white icon and font color and the image is light we won't see it to avoid that
for text adding shadow can make the text harder to read, prefer use a scrim : semi-transparent layout between the image
	gradient scrim example : from 30% opaque at the bottom to complete transparency
	
	to implement this use a gradient drawable place on top of the imageView. in drawable/scrim

		<shape android:shape="rectangle">
			<gradient
				android:angle="-90"
				android:startColor="#00000000"
				android:centerColor="#00000000"
				android:endColor="#4d000000"
				android:type="linear"/>
		</shape>
	
	them use a framelayout

		<FrameLayout >
			<ImageView />
			<View android:background="@drawable/scrim"/>
			<TextView android:text="Courgettes"/>
		</Framelayout>