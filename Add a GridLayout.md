##	GridLayout and SpaceWidget : is great if you want to align content along multiple axes

GridLayout

	no need to put height or weight, it's wrap content by default
	can use layout_column_span=2 pour avoir qu'une case qui s'étend sur 2 colonnes.
	layout_column_weight : distribute space among all columns, need to be added in all column and each rows.
	layout_gravity : to tell a GridLayout to center a view horizontally within it's cell.
	Because GridLayout is a library add the complete package name
	note that we use the "app" attribute tag app:columnCount="2"
	app:columnCount="2" <is not really necesarry because we can specify the column in it's childrens. But doing so simplify the declaration of each of the childrens.
	nb : giving a marging to the last cell will behave as if the margin were given to all cells of the rows.
	
SpaceWidget : Why use Space widget ? 
	
	because it's light
	because it's part of thegridLayout support library.
	
Exemple : https://github.com/udacity/Advanced_Android_Development/blob/master/app/src/main/res/layout/detail_today_grid.xml

	<android.support.v7.widget.GridLayout
		xmlns:app="http://schemas.android.com/apk/res-auto"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		app:columnCount="2">

		<android.support.v7.widget.Space
			android:layout_height="@dimen/detail_view_padding_vertical"
			app:layout_columnSpan="2"
			app:layout_columnWeight="1"
			app:layout_rowWeight="1" />

		<TextView
			app:layout_columnSpan="2"
			app:layout_columnWeight="1"
			app:layout_gravity="fill_horizontal" />

		<ImageView
			android:layout_width="0dp"
			android:adjustViewBounds="true"
			android:maxHeight="@dimen/today_icon"
			android:maxWidth="@dimen/today_icon"
			app:layout_columnWeight="1"
			app:layout_gravity="fill_horizontal"/>

		<TextView
			android:layout_width="0dp"
			app:layout_columnWeight="1"
			app:layout_gravity="fill_horizontal"/>

		<TextView
			android:layout_width="0dp"
			app:layout_columnWeight="1"/>

		<TextView
			android:layout_width="0dp"
			app:layout_columnWeight="1"/>

		<android.support.v7.widget.Space
			android:layout_height="@dimen/detail_view_padding_vertical"
			app:layout_columnSpan="2"
			app:layout_columnWeight="1"
			app:layout_rowWeight="1" />

	</android.support.v7.widget.GridLayout>
	
