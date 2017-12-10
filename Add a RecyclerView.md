# RecyclerView: let you scroll through a list of items

 material design list item animations add a significant change in the way adapters works.
 Animations are great for deleting an item.
 
For the list item use it's good to use

	android:minHeight="?android:attr/listPreferredItemHeight" permet d'assurer que l'on peut appuyer avec le doigt dessus.
	
# RecyclerView
 was added tothe support livbrary 
 perform many of the fonctions the listview does.
 the listview code was exceptionnaly complicated and unflexible but handled many things : 
	Layout
	Recycling
	Selection
	Decorating like dividers
	Scrolling
	Empty view
only recycle.
but others things can be handle with managers
	Layout LayoutManager
	Recycling RecyclerView
	Selection ???
	Decorating like dividers ItemDecorator
	Scrolling SmoothScroller
	Empty view ???
LayoutManagers allows us to create different pluggable experiences.
	vertical list
	horizontal list (cool no ?)
	grid layout
	staggered grid layout with laout childrensof different size.
		horizontal or vertical
		can layout children in reverse order

ListView works with 
CursorAdapter
CursorLoader
ViewHolder (optionnal)
OnItemClickListener

RecyclerView works with 
Adapter (no CursorAdapter but we can handle the work ourselves, by calling notifyDataSetChanged).
CursorLoader
ViewHolder (requierred)
but no OnItemClickListener : so what to use ?
	OnItemTouchListener along with a gesture detector of cliked but it's more common to
	have theViewHolder implements OnItemClickListener for the individuals views that it's holding
		the ViewHolder have access to the item position that is beeing clicked
is set so that a single Adapter can drive multiple recycler views
onScrolled method return the x and y of the scroll and not the item position, wihth is actually better.

How to handle RecyclerView item selection and choice
1-use the class ItemChoiceManager which was made with parts of Listview code
2https://www.udacity.com/course/viewer#!/c-ud855-nd/l-3940839262/m-4331460093
Note that RecyclerView will evolve and ecome easier




# RecyclerView useful methods

index
position in adapter will correspond to an index of attached child in a recycler view

Recycled view : A view previously used to display data for a specific adapter position may be placed in a cache for later reuse to display the same type of data again later. This can drastically improve performance by skipping initial layout inflation.
Scraped view : Is detached from parent but temporary. Can be re-used.
Scraped view dirty: Is detached from parent but temporary. Can be re-used but need rebind.
Scrapped view :view attached to parent but marked for removal or reuse
Dirty view : Is attaced to parent but need rebind
ChildView : a regular view of the recycler view
AnimatingView : its a childview attached to layout but invisible, purely usefull for animations

# Positions
## layout position = LayoutManager position: 
Position of an item in the latest layout calculation (what's displayed).
what user sees on screen.
return position after view is drawn ? (or calculation is done)
ViewHolder#getLayoutPosition()
findViewHolderForLayoutPosition(int)

## adapter position : 
Position of an item in the adapter.
position requested if no layout displayed yet 
or actual position if layout displayed.
return position very quickly
can be null if called just after notifyDataSetChanged (because it iscalculating new positions)
ViewHolder#getAdapterPosition()
findViewHolderForAdapterPosition(int)



   

setHasFixedSize : use it if only the model change but never the number of items

swapAdapter : similar to {@link #setAdapter(Adapter)} but assumes existing adapter and the new adapter uses the same {@link ViewHolder} and does not clear the RecycledViewPool.
setAdapter
getAdapter

setLayoutManager
getLayoutManager

setRecyclerListener : If an application associates expensive or heavyweight data with item views, this may be a good place to release
addOnChildAttachStateChangeListener : Idem setRecyclerListener
removeOnChildAttachStateChangeListener
clearOnChildAttachStateChangeListeners
addOnItemTouchListener
removeOnItemTouchListener

ViewInfoStore mViewInfoStore : store infos needed for animations. see callbacks ViewInfoStore.ProcessCallback mViewInfoProcessCallback
addAnimatingView
removeAnimatingView
setItemAnimator :animation depends on LayoutManager to beenabled
getItemAnimator
isAnimating

ChildHelper mChildHelper;
getChildViewHolder
getChildPosition :note this is basically calling getChildAdapterPosition
getChildAdapterPosition
getChildLayoutPosition : This position may not be equal to Item's adapter position if there are pending changes n the adapter which have not been reflected to the layout yet.
getChildItemId
findViewHolderForPosition
findViewHolderForLayoutPosition
findViewHolderForAdapterPosition
findViewHolderForItemId : must use an Adapter with {@link Adapter#setHasStableIds
findChildViewUnder(float x, float y)
onChildAttachedToWindow
onChildDetachedFromWindow
hasPendingAdapterUpdates

 
getRecycledViewPool
setRecycledViewPool (might be useful for mealplanner)
RecycledViewPool : clear, setMaxRecycledViews, getRecycledView, putRecycledView, attach, detach


Recycler contains : 
scraped view attached
detached view
childviews
setViewCacheSize : maximum number of detached valid views

setViewCacheExtension
setItemViewCacheSize : limited in size. If not enough room it will be added to RecycledViewPool

getBaseline ?

getScrollState
setScrollState
setOnScrollListener
addOnScrollListener
removeOnScrollListener
clearOnScrollListeners
scrollToPosition
smoothScrollToPosition
scrollTo
scrollBy
computeHorizontalScrollOffset
computeHorizontalScrollExtent
computeHorizontalScrollRange
computeVerticalScrollOffset
computeVerticalScrollExtent
computeVerticalScrollRange
smoothScrollBy
stopScroll
offsetChildrenVertical
offsetChildrenHorizontal
onScrolled
onScrollStateChanged


addItemDecoration :will impact the mesurement and drawing ofitemView
removeItemDecoration
invalidateItemDecorations

setChildDrawingOrderCallback

setLayoutFrozen : may be useful when swiping (if samebehavior in viewpager)
isLayoutFrozen

stopScroll
getMinFlingVelocity
getMaxFlingVelocity

focusSearch
requestChildFocus
addFocusables

onAttachedToWindow
onDetachedFromWindow
isAttachedToWindow


isComputingLayout


#Adapter

onCreateViewHolder
onBindViewHolder

getItemViewType

setHasStableIds
hasStableIds
getItemId

getItemCount

onViewRecycled : a view is no longer needed we should release its ressouce. good place to do so. Note : its layout manager that ask for removal
onFailedToRecycleView

onViewAttachedToWindow
onViewDetachedFromWindow

hasObservers
registerAdapterDataObserver
unregisterAdapterDataObserver

onAttachedToRecyclerView : recyclerviews call this
onDetachedFromRecyclerView

notifyDataSetChanged
notifyItemChanged(int)
notifyItemInserted(int)
notifyItemRemoved(int)
notifyItemRangeChanged(int, int)
notifyItemRangeInserted(int, int)
notifyItemRangeRemoved(int, int)

# LayoutManager

setRecyclerView
onLayoutChildren : to read if we want animations
addDisappearingView
addView
removeView
removeViewAt
removeAllViews
findViewByPosition
moveView
detachAndScrapView
removeAndRecycleView
getChildCount : Return the current number of child views attached to the parent RecyclerView. This does not include child views that were temporarily detached and/or scrapped
getFocusedChild
ignoreView
detachAndScrapAttachedViews

onItemsChanged by the adapeter
onItemsAdded 
onItemsRemoved
onItemsUpdated
onItemsMoved

#ViewHolder

getLayoutPosition
getAdapterPosition
getItemId :if adapter has  stable ids
getItemViewType
isScrap
isInvalid
needsUpdate
isBound
isRemoved
hasAnyOfTheFlags
isTmpDetached
isRecyclable
isAdapterPositionUnknown
doesTransientStatePreventRecycling

onEnteredHiddenState
onLeftHiddenState


Quelques observations :

# Initial state

Root childrens : Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 40

RecyclerView childrens : 
View not null and ViewHolder not null : 40

Adapter childrens :
View not null and ViewHolder not null : 40
View null and ViewHolder null : 10

Layout manager childrens with getChildCount :  Imposible d'acceder au viewHolder à moins de tagger la vue
View not null : 40

Layout manager childrens with getItemCount :  Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 40
View null : 10

# After rotation state

Root childrens : Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18

RecyclerView childrens : 
View not null and ViewHolder not null : 18

Adapter childrens :
View not null and ViewHolder not null : 18
View null and ViewHolder null : 32

Layout manager childrens with getChildCount :  Imposible d'acceder au viewHolder à moins de tagger la vue
View not null : 18

Layout manager childrens with getItemCount :  Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18
View null : 32

# After scroll and restoration

Root childrens : Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18

RecyclerView childrens : 
View not null and ViewHolder not null : 18

Adapter childrens :
View not null and ViewHolder NULL : 18
View null and ViewHolder null : 32

Layout manager childrens with getChildCount :  Imposible d'acceder au viewHolder à moins de tagger la vue
View not null : 18

Layout manager childrens with getItemCount :  Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18
View null : 32

# After reduction

Root childrens : Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18

RecyclerView childrens : 
View not null and ViewHolder not null : 18

Adapter childrens :
View not null and ViewHolder NULL : 18
View null and ViewHolder null : 32

Layout manager childrens with getChildCount :  Imposible d'acceder au viewHolder à moins de tagger la vue
View not null : 18

Layout manager childrens with getItemCount :  Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18
View null : 32


# After scroll

Root childrens : Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18

RecyclerView childrens : 
View not null and ViewHolder not null : 18

Adapter childrens :
View not null and ViewHolder NULL : 18 because the view has been visible before view is not, viewHolder hasbeen detached
View null and ViewHolder null : 5
View null (yes) and ViewHolder not null : 18 : strange because thoses views are visibles. Lavue utilisée pour l'affichage est celleutilisés avant. Looks like the if the viewHolder is not null, the view is displayed. Best thing to do would be to bind the viewHolder as the tag of the view. I think. 
View null and ViewHolder null : 9

Layout manager childrens with getChildCount :  Imposible d'acceder au viewHolder à moins de tagger la vue
View not null : 18

Layout manager childrens with getItemCount :  Imposible d'acceder au viewHolder à moins de tagger la vue.
View not null : 18
View null : 32