# Find a view : Méthod that return a Matcher<View>

## CoreMatcher

	allOf :ET 
	anyOf :OU
	both
	either
	describedAs
	everyItem :return a matcher that match the given criteria from the list of matcher
	is : assertThat(cheese, is(smelly)) = assertThat(cheese, is(equalTo(smelly)))
	isA : assertThat(cheese, isA(Cheddar.class))
	anything : Creates a matcher that always matches, regardless of the examined object.
	hasItem : assertThat(Arrays.asList("foo", "bar"), hasItem("bar"))
	hasItems : assertThat(Arrays.asList("foo", "bar", "baz"), hasItems("baz", "foo"))
	equalTo : assertThat("foo", equalTo("foo"));
	any
	instanceOf
	not : assertThat(cheese, is(not(equalTo(smelly))))
	nullValue
	notNullValue
	sameInstance
	theInstance
	containsStrings
	startsWith
	endsWith

## ViewMatchers

	isAssignableFrom
	withClassName : Returns a matcher that matches Views with class name matching the given matcher.
	isDisplayed : Returns a matcher that matches {@link View}s that are currently displayed on the screen to the user.
	isCompletelyDisplayed
	isDisplayingAtLeast
	isEnabled : return a matcher that match only enabled views
	isFocusable
	hasFocus
	isSelected
	hasSibling
	withContentDescription
	withId
	withResourceName
	withTagKey
	withTagValue
	withText
	withCharSequence
	withHint
	isChecked 
	isNotChecked
	withCheckBoxState
	hasContentDescription :return all views that matches with any content description
	hasDescendant
	isClickable
	isDescendantOfA
	withEffectiveVisibility
	withParent
	withChild
	isRoot
	supportsInputMethods
	hasImeAction
	hasLinks
	assertThat
	withSpinnerText
	isJavascriptEnabled
	hasErrorText
	withInputType

## CursorMatcher

	withRowShort
	withRowInt
	withRowLong
	withRowFloat
	withRowDouble
	withRowString
	withRowBlob

## LayoutMatchers

	hasEllipsizedText
	hasMultilineText

## PreferenceMatchers

	withSummary
	withSummaryText
	withTitle
	withTitleText
	isEnabled
	withKey

## OrderingComparison (it extends matcher class like others)

	comparesEqualTo(T value) 
	greaterThan(T value) 
	greaterThanOrEqualTo(T value) 
	lessThan(T value) 
	lessThanOrEqualTo(T value) 
	
## CombinableMatcher

    both(Matcher<? super LHS> matcher) {
	either(Matcher<? super LHS> matcher) {
	describedAs(String description, Matcher<T> matcher, Object... values) {
	everyItem(Matcher<U> itemMatcher) {
	is() {
	isA(Class<T> type) {
	anything() {
	hasItem(T item) {
	equalTo(T operand) {
	any(Class<T> type) {
	instanceOf(Class<?> type) {
	not(Matcher<T> matcher) {
	nullValue() {
	notNullValue() {
	sameInstance(T target) {
	theInstance(T target) {
	containsString(String substring) {
	startsWith(String prefix) {
	endsWith(String suffix) {
	array(Matcher... elementMatchers) {
	hasItemInArray(T element) {
	arrayContaining(List<Matcher<? super E>> itemMatchers) {
	arrayContainingInAnyOrder(E... items) {
	arrayWithSize(Matcher<? super Integer> sizeMatcher) {
	arrayWithSize(int size) {
	emptyArray() {
	hasSize(Matcher<? super Integer> sizeMatcher) {
	empty() {
	emptyCollectionOf(Class<E> type) {
	emptyIterable() {
	emptyIterableOf(Class<E> type) {
	contains(Matcher... itemMatchers) {
	containsInAnyOrder(T... items) {
	iterableWithSize(Matcher<? super Integer> sizeMatcher) {
	iterableWithSize(int size) {
	hasEntry(K key, V value) {
	hasKey(Matcher<? super K> keyMatcher) {
	hasKey(K key) {
    hasValue(V value) {
    hasValue(Matcher<? super V> valueMatcher) {
    isIn(Collection<T> collection) {
    isIn(T[] param1) {
    isOneOf(T... elements) {
    closeTo(double operand, double error) {
    closeTo(BigDecimal operand, BigDecimal error) {
    comparesEqualTo(T value) {
    greaterThan(T value) {
    greaterThanOrEqualTo(T value) {
    lessThan(T value) {
    lessThanOrEqualTo(T value) {
    equalToIgnoringCase(String expectedString) {
    equalToIgnoringWhiteSpace(String expectedString) {
    isEmptyString() {
    isEmptyOrNullString() {
    stringContainsInOrder(Iterable<String> substrings) {
    hasToString(Matcher<? super String> toStringMatcher) {
    hasToString(String expectedToString) {
    typeCompatibleWith(Class<T> baseType) {
    eventFrom(Class<? extends EventObject> eventClass, Object source) {
    eventFrom(Object source) {
    hasProperty(String propertyName) {
    hasProperty(String propertyName, Matcher<?> valueMatcher) {
    samePropertyValuesAs(T expectedBean) {
    hasXPath(String xPath, NamespaceContext namespaceContext) {
    hasXPath(String xPath) {
    hasXPath(String xPath, NamespaceContext namespaceContext, Matcher<String> valueMatcher) {
    hasXPath(String xPath, Matcher<String> valueMatcher) {

# Get a view interaction from this view : Methods that return a view interaction (genre de sql select)

	onView : the view has to be part of the  view hierarchy

# Do something on this view interaction

	switch to other window
	check something
	perform an action
	
## switch to other window using inRoot 

	inRoot(withDecorView(not(is(getActivity().getWindow().getDecorView()))))

## Check something with assertions

Assertions can be : 

	ViewAssertions
	LayoutAssertions
	PositionsAssertions
	
### ViewAssertions

	doesNotExist() : the view detetminated by viewMatcher doesnot exist ex: withId(R.id.button1).doesNotExist()
	matches() :the view exist in the hierarchy + match other criterias. onView(withId(R.id.recycler_view)).check(matches(anything()));
	selectedDescendantsMatch() :example  selectedDescendantsMatch(isAssignableFrom(TextView.class), not(hasEllipsizedText()));

### LayoutAssertions

	noEllipsizedText()
	noMultilineButtons()
	noOverlaps()

### PositionsAssertions

	isLeftOf
	isRightOf
	isLeftAlignedWith
	isRightAlignedWith
	isAbove
	isBelow
	isBottomAlignedWith
	isTopAlignedWith

## perform an action

	click()
	swipeLeft()
	swipeRight()
	swipeDown
	swipeUp
	closeSoftKeyboard
	pressImeActionButton
	pressBack
	pressMenuKey
	pressKey
	doubleClick
	longClick
	scrollTo
	typeTextIntoFocusedView
	typeText
	replaceText
	openLinkWithText
	openLinkWithUri
	openLink

# Examples : 

Example : clics

	onView(allOf(withId(R.id.button1), isDescendantOfA(withId(R.id.linear_layout)))).perform(click());
	onView(allOf(withId(R.id.button1), withParent(withId(R.id.linear_layout)))).perform(click());
	onView(withId(R.id.recycler_view)).check(matches(isDisplayed()));
	onView(allOf(withId(R.id.more),
			withParent(
					allOf(withId(R.id.item),
							withChild(allOf(withId(R.id.title), withText("Hello")))))))
			.perform(click());
	//To work properly this method need device to have turned off animation scale
	//see : https://guides.codepath.com/android/UI-Testing-with-Espresso
	onView(withId(R.id.recycler_view)).perform(RecyclerViewActions.actionOnItemAtPosition(1, click()));
	onView(withId(R.id.text)).check(matches(not(isDisplayed())));
	onView(withId(R.id.linear_layout)).check(isDisplayed());
	onData(withId(R.id.linear_layout))
			.onChildView(withId(R.id.button1))
			.perform(click());
	onData(withValue(1))
			.inAdapterView(withId(R.id.list))
			.perform(click());
	onView(withId(R.id.recycler_view)).perform(RecyclerViewActions.actionOnItemAtPosition(1, click()));
	onView(withId(R.id.text)).check(matches(withText("1"))).check(matches(isDisplayed()));
	onView(allOf(withId(R.id.include_one), isDescendantOfA(withId(R.id.button1)))).perform(click());
	onView(allOf(withId(R.id.button1), hasParent(withId(R.id.include_one)))).perform(click());
	
Example using OrderingComparison matcher

	onView(withId(R.id.recycler_view)).check(RecyclerViewAssertions.withItemCount(equalTo(1)));
	onView(withId(R.id.recycler_view)).check(RecyclerViewAssertions.withItemCount(equalTo(1)));
	onView(withId(R.id.recyclerView)).check(new RecyclerViewItemCountAssertion(greaterThan(5));
	onView(withId(R.id.recyclerView)).check(new RecyclerViewItemCountAssertion(lessThan(5));

Example : Checks that what has been typed into EditText is retained after screen rotation

    @Test
    public void whenDeviceRotates_sameTextInputIsRetained() {
        //GIVEN
        onView(ViewMatchers.withId(R.id.test_fragment_edittext)).perform(typeText(SAMPLE_TEXT));
        //WHEN
        rotateDevice();
        //THEN
        onView(withId(R.id.test_fragment_edittext)).check(matches(withText(SAMPLE_TEXT)));
        onView(withId(R.id.test_fragment_edittext)).perform(clearText());
        onView(withId(R.id.test_fragment_edittext)).perform(typeText(exampleText));
        closeSoftKeyboard();
    }

    private void rotateDevice() {
        activityRule.getActivity().setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
    }

Example : Test that clicking on a Navigation Drawer Item will open the correct fragment.

    /**
     * Test that clicking on a Navigation Drawer Item will open the correct fragment.
     * Espresso: openDrawer, onView, withText, perform, click, matches, check, isDisplayed
     */
    @Test
    public void testNavigationDrawerItemClick() {
        openDrawer(R.id.my_drawer_layout);
        onView(withText("Menu One")).perform(click());
        onView(allOf(withId(R.id.navigation_fragment_text), withText("Menu One"))).check(matches(isDisplayed()));
    }

    /**
     * Test opening the Navigation Drawer and pressing the back button.
     * Espresso: openDrawer, pressBack
     */
    @Test
    public void testNavigationDrawerBackButton() {
        openDrawer(R.id.my_drawer_layout);
        pressBack();

        onView(ViewMatchers.withId(R.id.right_text)).check(isRightOf(withId(R.id.left_text)));
    }

Example : View pager swipe
	
    /**
     * Swipe between the first and second pages and back to the first in the ViewPager.
     */
    @Test
    public void testSwipeBetweenFirstSecondAndBackToFirstPage() {
        onView(allOf(withId(R.id.example_text), withText("Test One"))).check(matches(isDisplayed()));
        onView(withId(R.id.pager)).perform(swipeLeft());
        onView(withText("Test Two")).check(matches(isDisplayed()));
        onView(withId(R.id.pager)).perform(swipeRight());
        onView(withText("Test One")).check(matches(isDisplayed()));
    }


Example : matching un item d'une liste view en fonction de sa valeur

    onData(withValue(27))
        .inAdapterView(withId(R.id.list))
        .perform(click());

	public static Matcher<Object> withValue(final int value) {
		return new BoundedMatcher<Object, MainActivity.Item>(MainActivity.Item.class) {
		  @Override
		  public void describeTo(Description description) {
			description.appendText("has value " + value);
		  }
		  @Override
		  public boolean matchesSafely(MainActivity.Item item) {
			return item.toString().equals(String.valueOf(value));
		  }
		};
	}
	
Example: matches views with the given tag
	
    public class TagMatcher implements ViewMatcher {

        private String tag;

        public TagMatcher(String tag){
            this.tag = tag;
        }

        public boolean matches(View v){
            String tag = v.getTag();
            return this.tag.equals(tag);
        }

    }
	
Example: matches views that have visibility GONE

    public class GoneMatcher implements ViewMatcher {

        public boolean matches(View v){
            v.getVisibility() == View.GONE
        }
    }

Exple an arraylist of all matching views

    private static List<View> getMatchingViews(ViewGroup root, ViewMatcher viewMatcher){
        List<View> views = new ArrayList<View>();
        final int childCount = root.getChildCount();
        for (int i = 0; i < childCount; i++) {
            final View child = root.getChildAt(i);
            if (child instanceof ViewGroup) {
                views.addAll(getMatchingViews((ViewGroup) child, viewMatcher));
            }

            if(viewMatcher.matches(child)){
                views.add(child);
            }
        }
        return views;
    }

    public interface ViewMatcher{
        public boolean matches(View v);
    }

Example custom matchers

    public static Matcher<View> withTaskViewName(final String expected) {
        return new TypeSafeMatcher<View>() {
            @Override
            protected boolean matchesSafely(View item) {
                if(item != null && item.findViewById(R.id.task_item_task_name) != null) {
                    TextView taskName = (TextView) item.findViewById(R.id.task_item_task_name);
                    if(TextUtils.isEmpty(taskName.getText())) {
                        return false;
                    } else {
                        return taskName.getText().equals(expected);
                    }
                } else {
                    return false;
                }
            }

            @Override
            public void describeTo(Description description) {
                description.appendText("Looked for " + expected + " in the task_item.xml file");
            }
        };
    }
	
Example custom matchers

    public static Matcher<View> withCompoundDrawable(final int resourceId) {
        return new BoundedMatcher<View, TextView>(TextView.class) {
            @Override
            public void describeTo(Description description) {
                description.appendText("has compound drawable resource " + resourceId);
            }

            @Override
            public boolean matchesSafely(TextView textView) {
                for (Drawable drawable : textView.getCompoundDrawables()) {
                    if (sameBitmap(textView.getContext(), drawable, resourceId)) {
                        return true;
                    }
                }
                return false;
            }
        };
    }

    public static Matcher<View> withImageDrawable(final int resourceId) {
        return new BoundedMatcher<View, ImageView>(ImageView.class) {
            @Override
            public void describeTo(Description description) {
                description.appendText("has image drawable resource " + resourceId);
            }

            @Override
            public boolean matchesSafely(ImageView imageView) {
                return sameBitmap(imageView.getContext(), imageView.getDrawable(), resourceId);
            }
        };
    }

    private static boolean sameBitmap(Context context, Drawable drawable, int resourceId) {
        Drawable otherDrawable = context.getResources().getDrawable(resourceId);
        if (drawable == null || otherDrawable == null) {
            return false;
        }
        if (drawable instanceof StateListDrawable && otherDrawable instanceof StateListDrawable) {
            drawable = drawable.getCurrent();
            otherDrawable = otherDrawable.getCurrent();
        }
        if (drawable instanceof BitmapDrawable) {
            Bitmap bitmap = ((BitmapDrawable) drawable).getBitmap();
            Bitmap otherBitmap = ((BitmapDrawable) otherDrawable).getBitmap();
            return bitmap.sameAs(otherBitmap);
        }
        return false;
    }
}

Example : my own recycler view test functions

  public void add_a_collection()
  {
    //Given that I have an app open with a recycler existing and item count equals 'initialRecyclerViewChildCount'
    RecyclerView recyclerView = (RecyclerView) mActivityRule.getActivity().findViewById(R.id.notebook_list_fragment);
    int initialRecyclerViewChildCount = recyclerView.getChildCount();
    onView(withId(R.id.notebook_list_fragment)).check(matches(anything()));
    onView(withId(R.id.notebook_list_fragment)).check(RecyclerViewAssertions.withItemCount(equalTo(initialRecyclerViewChildCount)));

    //When I run the sequence 'create collection' with name 'collectionA'
    onView(withId(R.id.dms_action_create_content)).perform(click());
    onView(withId(R.id.dms_fab_menu_new_folder_button)).perform(click());
    onView(withId(R.id.collection_title)).perform(clearText());
    onView(withId(R.id.collection_title)).perform(typeText("collectionA"), closeSoftKeyboard());
    onView(withId(button1)).perform(click());

    //Then I should see 'collectionA' among recyclerView items recycler view items should equals 'initialRecyclerViewChildCount + 1'
    onView(CoreMatchers.allOf(withId(R.id.title), withText("collectionA"))).check(matches(isDisplayed()));
    onView(withId(R.id.notebook_list_fragment)).check(RecyclerViewAssertions.withItemCount(equalTo(initialRecyclerViewChildCount + 1)));
  }

	public void delete_a_collection()
	{
		//Given that I have an app open with a recycler view visible, an 'collectionA' visible and item count equals 'initialRecyclerViewChildCount'
		add_a_collection(); //FIXME this is not recommanded to have a test calling another test
		onView(withId(R.id.notebook_list_fragment)).check(matches(isDisplayed()));
		onView(CoreMatchers.allOf(withId(R.id.title), withText("collectionA"))).check(matches(anything()));
		RecyclerView recyclerView = (RecyclerView) mActivityRule.getActivity().findViewById(R.id.notebook_list_fragment);
		int initialRecyclerViewChildCount = recyclerView.getChildCount();
		onView(withId(R.id.notebook_list_fragment)).check(RecyclerViewAssertions.withItemCount(equalTo(initialRecyclerViewChildCount)));

		//When I click the 'delete item' button
		onView(RecyclerViewMatcher.withRecyclerView(R.id.notebook_list_fragment).atPositionOnView(0, R.id.dms_collection_more_menu)).perform(click());
		onView(withId(R.id.dms_collection_menu_delete_button)).perform(click()); //Is it enough ?
		onView(withId(R.id.dms_collection_menu_delete_button)).inRoot(withDecorView(is(not(mActivityRule.getActivity().getWindow().getDecorView())))).perform(click());

		//Then I should not see 'itemA' among recyclerView items and recycler view items should equals '1'
		onView(CoreMatchers.allOf(withId(R.id.title), withText("collectionA"))).check(doesNotExist());
		onView(withId(R.id.notebook_list_fragment)).check(RecyclerViewAssertions.withItemCount(equalTo(0)));
	}

	public void edit_a_collection()
	{
		//Given that I have an app open with a recycler view visible, an 'itemA' visible and item count equals '1'
		add_a_collection(); //FIXME this is not recommanded to have a test calling another test
		onView(withId(R.id.notebook_list_fragment)).check(matches(isDisplayed()));
		onView(CoreMatchers.allOf(withId(R.id.title), withText("collectionA"))).check(matches(anything()));
		onView(withId(R.id.notebook_list_fragment)).check(RecyclerViewAssertions.withItemCount(equalTo(1)));

		//When I click the 'edit_item' button of itemA of position 0
		onView(RecyclerViewMatcher.withRecyclerView(R.id.notebook_list_fragment).atPositionOnView(0, R.id.dms_collection_more_menu)).perform(click());
		onView(withId(R.id.dms_collection_menu_edit_button)).perform(click()); //Is it enough ?
		onView(withId(R.id.collection_title)).perform(typeText("collection1"), closeSoftKeyboard());

		//Then I should see 'collection1' as label of the previous 'collectionA'
		onView(CoreMatchers.allOf(withId(R.id.title), withText("collection1"))).check(matches(anything()));
	}
  
	public void test_add_a_collection()
	{
		//Given that I have a Nebo app with a dms view open and no collection
		//FIXME uncomment those 2 lines and remove the last one
		//onView(withId(R.id.delete_all)).perform(click());
		//    assertEquals(0, recyclerView.getChildCount());
		//assertEquals(2, recyclerView.getChildCount());

		//When I run the sequence 'create collection' with name 'collectionA'
		String collectionA = "collectionA";
		//createCollectionSequence(collectionA);

		//Then I there should be a collection named 'CollectionA' in Dms model
		assertTrue(DMSUtils.hasCollection(context, collectionA));

		//And I should see a collection item named 'collectionA'
		int expectedItemCount = initialRecyclerViewChildCount + 1; //Assuming collection is collapsed
		assertEquals(expectedItemCount, recyclerView.getChildCount());
		View collectionItem = recyclerView.getChildAt(recyclerView.getChildCount() 2);
		RecyclerView.ViewHolder collectionHolder = recyclerView.getChildViewHolder(collectionItem);
		assertTrue(collectionHolder instanceof CollectionItemViewHolder);
		assertEquals((String) ((TextView) collectionHolder.itemView.findViewById(R.id.dms_collection_name)).getText(), collectionA);

		//And I should see a notebook item with a message 'No notebook in this folder'
		View emptyCollectionItem = recyclerView.getChildAt(recyclerView.getChildCount() 1);
		RecyclerView.ViewHolder notebookHolder = recyclerView.getChildViewHolder(emptyCollectionItem);
		assertTrue(notebookHolder instanceof NotebookItemViewHolder);
		assertEquals((String) ((TextView) notebookHolder.itemView.findViewById(R.id.empty_item_textview)).getText(), context.getResources().getString(R.string.dms_empty_collection_message));
	}

	public void test_edit_a_collection()
	{
		Context context = InstrumentationRegistry.getTargetContext();
		MainActivity mainActivity = mActivityRule.getActivity();
		mainActivity.getAllChildren();
		RecyclerView recyclerView = (RecyclerView) mainActivity.findViewById(R.id.notebook_list_fragment);

		int initialRecyclerViewChildCount = recyclerView.getChildCount();

		//Given that I have a Nebo app with a dms view open and a collection named 'collectionA'

		//When I click on collection more menu item named 'edit collection' and enter 'collectionAA' in the dialog asking for new name and valid dialog

		//Then there should be no collection named 'collectionA' in the dms model

		//And I should not see a collection item named 'collectionA'
	}

	public void test_delete_a_collection()
	{
		Context context = InstrumentationRegistry.getTargetContext();
		MainActivity mainActivity = mActivityRule.getActivity();
		mainActivity.getAllChildren();
		RecyclerView recyclerView = (RecyclerView) mainActivity.findViewById(R.id.notebook_list_fragment);

		int initialRecyclerViewChildCount = recyclerView.getChildCount();

		//Given that I have a Nebo app with a dms view open and a collection named 'collectionA'
		//FIXME should be collectionA and the first position '0'
		String collectionA = "__test__";
		int position = 0;
		View collectionItem = recyclerView.getChildAt(position);
		RecyclerView.ViewHolder collectionHolder = recyclerView.getChildViewHolder(collectionItem);
		//onView(withId(R.id.notebook_list_fragment)).perform(RecyclerViewActions.scrollToPosition(0));
		onView(withId(R.id.notebook_list_fragment)).perform(RecyclerViewActions.actionOnItemAtPosition(0, click()));
		onView(allOf(withId(R.id.dms_collection_item_all_layout), withText(collectionA))).check(matches(isDisplayed()));
		assertTrue(collectionHolder instanceof CollectionItemViewHolder);
		assertEquals(collectionA, (String) ((TextView) collectionHolder.itemView.findViewById(R.id.dms_collection_name)).getText());

		//When I click on collection more menu item named 'delete collection'
		onView(allOf(withId(R.id.dms_collection_more_menu), withParent(allOf(withId(R.id.dms_collection_item_all_layout), withText(collectionA))))).perform(click());
		//onView(withRecyclerView(R.id.notebook_list_fragment).atPositionOnView(1, R.id.text2)).perform(click());

		//Then I should see a dialog with message confirm delete message. And yes and No button enabled
		mainActivity.getAllChildren();

		//When I click yes

		//Then I should see

		//And I should not see a collection item named 'collectionA' in the dms view
	}
  
Example : my own recycler view RecyclerViewMatcher

	public class RecyclerViewMatcher
	{
		private final int recyclerViewId;

		public RecyclerViewMatcher(int recyclerViewId) {
			this.recyclerViewId = recyclerViewId;
		}

		public static RecyclerViewMatcher withRecyclerView(final int recyclerViewId) {
			return new RecyclerViewMatcher(recyclerViewId);
		}


		public Matcher<View> atPosition(final int position) {
			return atPositionOnView(position, -1);
		}

		public Matcher<View> atPositionOnView(final int position, final int targetViewId) {

			return new TypeSafeMatcher<View>() {
				Resources resources = null;
				View childView;

				public void describeTo(Description description) {
					String idDescription = Integer.toString(recyclerViewId);
					if (this.resources != null) {
						try {
							idDescription = this.resources.getResourceName(recyclerViewId);
						} catch (Resources.NotFoundException var4) {
							idDescription = String.format("%s (resource name not found)",
									new Object[]{Integer.valueOf
											(recyclerViewId)});
						}
					}

					description.appendText("with id: " + idDescription);
				}

				public boolean matchesSafely(View view) {

					this.resources = view.getResources();

					if (childView == null) {
						RecyclerView recyclerView =
								(RecyclerView) view.getRootView().findViewById(recyclerViewId);
						if (recyclerView != null && recyclerView.getId() == recyclerViewId) {
							childView = recyclerView.findViewHolderForAdapterPosition(position).itemView;
						} else {
							return false;
						}
					}

					if (targetViewId == -1) {
						return view == childView;
					} else {
						View targetView = childView.findViewById(targetViewId);
						return view == targetView;
					}
				}
			};
		}
	}
  
Example : my own recycler view ViewAssertion

	public static class RecyclerViewAssertions implements ViewAssertion
	{
		private final Matcher<Integer> mMatcher;

		private RecyclerViewAssertions(Matcher<Integer> matcher)
		{
		  this.mMatcher = matcher;
		}

		/**
		 * Returns an assert that ensures the view matcher does not find any matching view in the
		 * hierarchy.
		 */
		public static ViewAssertion withItemCount(Matcher<Integer> matcher)
		{
		  return new RecyclerViewAssertions(matcher);
		}

		@Override
		public void check(View view, NoMatchingViewException noViewFoundException)
		{
		  if (noViewFoundException != null)
		  {
			throw noViewFoundException;
		  }
		  RecyclerView recyclerView = (RecyclerView) view;
		  RecyclerView.Adapter adapter = recyclerView.getAdapter();
		  assertThat(adapter.getItemCount(), mMatcher);
		}
	}
 

# Examples links

All thoses links should be removed there is nearly no test there, except maybe Cukeulator

	C:\ProgrammingProjects\AndroidStudioProjects\Examples\EspressoTests
	C:\ProgrammingProjects\AndroidStudioProjects\Examples\RecyclerViewEspresso
	C:\ProgrammingProjects\AndroidStudioProjects\Examples\Cukeulator
	C:\ProgrammingProjects\AndroidStudioProjects\Examples\CucumberOnRail
	https://github.com/Elorri/RecyclerViewEspresso
	https://github.com/Elorri/Cukeulator

those 2 bellow are ok

	https://www.bignerdranch.com/blog/recyclerview-part-2-choice-modes/
	https://github.com/chiuki/espresso-samples/blob/master/list-view-basic/app/src/androidTest/java/com/sqisland/android/espresso/list_view_basic/MainActivityTest.java
