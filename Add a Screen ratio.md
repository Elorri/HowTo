# Add a Screen ratio / balanced use of space
	
	Use the 1,5 ratio when 2 panel screen displaying important infos and additional infos. important infos should be 1,5 time the additional infos.
	
	
	Exemple for an imageView : to inforce an imageView of certain aspect ratio (could be useful when device change and we want to be sure the ratio will be keep). Let say we want the height to always be 2/3 (3:2 ratio) of the device height

		public class ThreeTwoImageView extends ImageView {
			public ThreeTwoImageView(Context context){
				super(context);
			}
			public ThreeTwoImageView(Context context, AttributeSet attrs){
				super(context, attrs);
			}		
			public ThreeTwoImageView(Context context, AttributeSet attrs, int defStyle){
				super(context, attrs, defStyle);
			}
		}
		
		@Override
		protected void onMeasure(int widthSpec, int heightSpec){
			int threeTwoHeight = MeasureSpec.getSize(widthSpec)* 2 / 3;
			int threeTwoHeightSpec = MeasureSpec.getMeasureSpec(threeTwoHeight, MeasureSpec.EXACTLY);
			super.onMeasure(widthSpec, threeTwoHeightSpec);
		}
		
	to use our custom class

		<your.package.ThreeTwoImageView
			android:layout_width="match_parent"
			android:layout_height="0dp"  //because the view will calculte that when it measure itself
			android:scaleType="centerCrop" />
			
			
Github sample : Unsplash min 21

	beautiful picture from unsplash Free (do whatever you want) high-resolution photos.
	example of shared element trasition with arc motion for the selected picture
	others elements disapear by explosion "explose"
	status bar and navigation bar are excluded in mainactivity grid
	top slide edge transition when reentering mainactivity grid (means elements are reentering the grid from top, override the default implode in this case)
	no transition the first time we enter mainactivity grid
	interesting custom ForegroundImageView
	interesting custom ThreeTwoImageView
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master