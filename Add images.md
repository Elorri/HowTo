# Create a drawable of replacement in case image can't be downloaded

Add TextDrawable and Glide libraries

    compile 'com.amulyakhare:com.amulyakhare.textdrawable:1.0.1'
	compile 'com.github.bumptech.glide:glide:3.6.1'
	
Then whenever you do imageView.setImage() do this instead

        ColorGenerator generator = ColorGenerator.MATERIAL; // or use DEFAULT
        int noImageColor = generator.getRandomColor();
        TextDrawable noImage = TextDrawable.builder()
                .beginConfig()
                .fontSize((int) context.getResources().getDimension(R.dimen.bookTextSizePx))
                .textColor(Color.BLACK)
                .endConfig().buildRect(errorMsg.substring(0,1), //will display first letter title
                        noImageColor);
        Glide.with(context)
                .load(imgUrl)
                .error(noImage)
                .crossFade()
                .into(imageView);
				

If image load from url : add adjustViewBounds in ImageView xml file. This will make the image adjust itself to the container like does local images
                <ImageView
                    android:id="@+id/bookCover"
                    android:adjustViewBounds="true"
                    tools:src="@android:color/darker_gray"/>


If image displayed in notifications there is some more work to do

see https://github.com/udacity/Advanced_Android_Development/compare/4.00_Libraries...4.01_Basic_Gliding