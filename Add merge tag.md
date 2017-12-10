##	MergeTag : Don't use FrameLayout as a root for another Layout if there is only one child (in an include) : use merge tag. The merge tag will be eliminated when compilation start and replace by the child.

	Note we can avoid using include by using a merge tag.
	<merge xmlns:android="http://schemas.android.com/apk/res/android">
	With include you can only have layout parametters, not elevation