when writing over images that will be downloaded dynamically, if we use white icon and font color and the image is light we won't see it to avoid that
	usually used for Icons or text. add shadow behind text for this add a style like this in the textview

    <style name="Shadow">
        <item name="android:shadowColor">@color/secondary_text</item>
        <item name="android:shadowDx">1</item>
        <item name="android:shadowDy">1</item>
        <item name="android:shadowRadius">1</item>
    </style>
	