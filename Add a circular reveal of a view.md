## Add a circular reveal of a view (since-21 lollipop)
	note: the list item is a rectangle, so the radius (rayon) will have to start at 0 and stop at rectangleSize/2 + a little bit more, thats why we take the hypothenuse

				int finalRadius = (int)Math.hypot(view.getWidth()/2, view.getHeight()/2);

				if (isVeggie) {
					text1.setText(baconTitle);
					text2.setText(baconText);
					view.setBackgroundColor(white);
				} else {
					Animator anim = ViewAnimationUtils.createCircularReveal(view, (int) view.getWidth()/2, (int) view.getHeight()/2, 0, finalRadius);
					text1.setText(veggieTitle);
					text2.setText(veggieText);
					view.setBackgroundColor(green);
					anim.start();  <-this should be done last
				}
				
				
Github sample : SimplePaperTransformations. 

	Same app as ApplyPaletteDemo or ScrollEventsDemo but with circular reveal of the list item
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master