# Guidelines

	Material can change shape.
	Material grows and shrinks only along its plane.
	Material never bends or folds.
	https://material.google.com/what-is-material/material-properties.html#material-properties-transforming-material
	


	

## Add a shared element transition (since-21 lollipop): an element present on 2 screens transitions smoothly between them

	Motion design shared element to guide the user eyes to the right place.
	
	Motion design can guide the user eyes to the right place :
	shared element = views that contains content that is shared beetween activities. Dans sunshine on fait en sorte que le nuage ou le soleil reste à l écran (càd ne soit pas effacé puis remis) et bouge à sa nouvelle place. L'utilisateur peut voir clairement le nuage glisser de son ancienne positon à la nouvelle position.
	how to tell android which is a shared element ?
		1 add a transition name in the shared view in the destination layout
		2 add the unique (unique in the RecyclerView) transition name in hard code in the controller of that shared view destination layout, so that when rotating the device it can apply the transition again. To make the transition name unique, use the position of the adapter. 
		3 add supportPostPonedEnterTransition if the activity create a fragment, load data from the db etc
		4 add supportStartPostPonedEnterTransition tell it's time to do the transition
		CAUTION : between those 2 methods, everything we do is not going to work well like going to the network
	see : https://www.udacity.com/course/viewer#!/c-ud855-nd/l-3940839262/e-4328770429/m-4328770431	

first add the transitionName attribute in the layouts of the different activities, in gridItem.xml

	<ImageView android:transitionName="@string/transition_photo"/>

and in layoutItem.xml note we use the same string ressource transition_photo

	<ImageView android:transitionName="@string/transition_photo"/>

in the GridActivity.java

	Bundle bundle= ActivityOptions.makeSceneTransitionAnimation(this, sharedView, sharedView.getTransitionName()).toBundle();  <-this function let also declare severals sharedViews
	context.startActivty(intent,bundle);
	
the getTransitionName return a string because that you can have use shared element between different applications if they have the same name. Note that by default the share element transition use a built in transition called move.xml

	<transitionSet xmlns:android="http://schemas.android.com/apk/res/android">
		<changeBounds />  <-moves and resize elements
		<changeTransform/> <-if you want to change the transformation applied
		<changeClipBounds/> <-if you want to change the clip applied
		<changeImageTransform/>
	</transitionSet>
	
if you want to use your custom_transition.xml either specify it in xml like that

	<style name="AppTheme.Home">
		<item name="android:widowContentTransition">true</item>		<-this is only needed if your theme does not inherit from AppCompat or Material
		<item name="android:widowSharedElementEnterTransition">@transition/custom_transition</item>
	</style>
	
or in the mainActivity

	getWindow().setSharedElementEnterTransition(TransitionInflater.from(this).inflateTransition(R.transition.custom_transition)));
	Bundle bundle= ActivityOptions.makeSceneTransitionAnimation(this, sharedView, sharedView.getTransitionName()).toBundle();  <-this function let also declare severals sharedViews
	context.startActivty(intent,bundle);
	
in the mainFragment onInflate and onActivityCreated

    @Override
    public void onInflate(Activity activity, AttributeSet attrs, Bundle savedInstanceState) {
        super.onInflate(activity, attrs, savedInstanceState);
        TypedArray a = activity.obtainStyledAttributes(attrs, R.styleable.ForecastFragment,
                0, 0);
        mHoldForTransition = a.getBoolean(R.styleable.ForecastFragment_sharedElementTransitions, false);
        a.recycle();
    }
	
	@Override
    public void onActivityCreated(Bundle savedInstanceState) {
        // We hold for transition here just in-case the activity
        // needs to be re-created. In a standard return transition,
        // this doesn't actually make a difference.
        if ( mHoldForTransition ) {
            getActivity().supportPostponeEnterTransition();
        }
        getLoaderManager().initLoader(FORECAST_LOADER, null, this);
        super.onActivityCreated(savedInstanceState);
    }
	
in the mainFragment onLoadFinished

	if ( data.getCount() == 0 ) {
            getActivity().supportStartPostponedEnterTransition();
        } else {
            mRecyclerView.getViewTreeObserver().addOnPreDrawListener(new ViewTreeObserver.OnPreDrawListener() {
                @Override
                public boolean onPreDraw() {
                    // Since we know we're going to get items, we keep the listener around until
                    // we see Children.
                    if (mRecyclerView.getChildCount() > 0) {
                        mRecyclerView.getViewTreeObserver().removeOnPreDrawListener(this);
                        if ( mHoldForTransition ) {
                            getActivity().supportStartPostponedEnterTransition();
                        }
                        return true;
                    }
                    return false;
                }
            });
        }
	
in the values/attrs

	<resources>
		<declare-styleable name="mainFragment">
			<attr name="sharedElementTransitions" format="boolean"/>
		</declare-styleable>
	</resources>
	
	
could be useful in the detailActivity onCreate

	Bundle arguments = new Bundle();
	arguments.putBoolean(DetailFragment.DETAIL_TRANSITION_ANIMATION, true);

	// Being here means we are in animation mode
	supportPostponeEnterTransition();
	
in the detailFragment class
	
	static final String DETAIL_TRANSITION_ANIMATION = "DTA";

in the detailFragment onCreateView

        Bundle arguments = getArguments();
        if (arguments != null) {
            mTransitionAnimation = arguments.getBoolean(DetailFragment.DETAIL_TRANSITION_ANIMATION, false);
        }
		

in the detailFragment onLoadFinished

        // We need to start the enter transition after the data has loaded
        if ( mTransitionAnimation ) {
            activity.supportStartPostponedEnterTransition();
			
in the adapter onBindViewHolder

        // this enables better animations. even if we lose state due to a device rotation,
        // the animator can use this to re-find the original view
        ViewCompat.setTransitionName(forecastAdapterViewHolder.mIconView, "iconView" + position);
		

	
## instructive motion. Faire un peu bouger un element pour que l'utilisateur en prenne note. 

	Example : scroller un peu le textview en dessous de la collapsed image toolbar
	https://www.udacity.com/course/viewer#!/c-ud862-nd/l-4969789009/m-4908328931

in layout/main.xml

	FrameLayout
		ImageView layout_heigt=400dp
		ScrollView paddingTop=400dp
			LinearLayout elevtion=8dp  <-to make it clear that it's a distinct surface
				TextView
				TextView
				TextView
			
in MainActivity.java all we need to do is animatethe scroll position to a position that shows more ofthe text content
	
    @Override
    public void onEnterAnimationComplete() {  <-when entering here any animation set on the activity/window is finished
        super.onEnterAnimationComplete();
        final int startScrollPos = getResources().getDimensionPixelSize(R.dimen
                .init_scoll_up_distance);
        Animator animator=ObjectAnimator.ofInt(
                mScrollView,
                "scrollY",		<-tell to animate the scrollY property of the scrollview, we also could have use the scrollToMethod 
                startScrollPos).setDuration(300);
        animator.start();
    }
	
	
Github sample : L4_06_Q min 21

	master_detail view, the detail view is slide in, and the master view is fade
	combined with a shared element trasition
	https://github.com/udacity/ud862-samples links also copied in C:\Users\Elorri\Dropbox\Udacity\Classes\9 Material Design\ud862-samples-master
	