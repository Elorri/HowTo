# Comon configs

- No matter wihch config you choose, you need to make sure there is a layout for each cell of the table
- There is 2 tendancies in choosing those config
	- combining width with height (ex : ABC with EFG like above): tend to be complex and more use in the future
	- combining smallest width with port and land (ex : ABC with EFG like above) : simple and very often used
- port and land are secondary options
	
## Combining width with height common config


|    /    |  <  |  '>= w600dp  |  '>=w720dp  |
|:------:|:---:|:-----------:|:----------:|
|    <   |     |             |            |
|  h1024dp  |    |           |            |

## Combining smallest width with port and land

|    /    |  <  |  '>= sw600dp  |  '>=sw720dp  |
|:------:|:---:|:-----------:|:----------:|
|   Land  |     |             |            |
|  Port  |    |           |            |

## Sunshine config

|    /    |  <       |  '>= sw600dp  | 
|:------:|:--------:|:----------------:|
|  Land  |  Land   |     sw600dp-Default     |
|  Port  |  Default      |     sw600dp-port  |

device will look at sw600dp-port or sw600dp-land then at sw600dp and then a land or portrait.

## Sunshine others possible config with same number of files

|     /   |  <  |  '>= sw600dp  | 
|:------:|:---:|:-----------:|
|  Land  |  D    |     sw600dp-D     |
|  Port  |  port    |     sw600dp-port  |

or 

|   /    |  sw600dp<  |  '>= sw600dp  | 
|:------:|:-------:|:-----------:|
|  Land  |  land    |     sw600dp-land     |
|  Port  |  D    |     sw600dp-D  |

# Choose your xml layout you need

choose your config. Ex : 

|    /    |  sw600dp<  |  '>= sw600dp  | 
|:------:|:-------:|:-----------:|
|  Land  |  layout-land    |     layout-sw600dp-land     |
|  Port  |  layout    |     layout-sw600dp  |

# Make a list of layout xml to write

## Make a list of screen you have for phone

ex : 
- about screen
- list screen
- add screen
- detail screen

## Draw or name with a long-desc-name how it will look like for each layout and each layout
Desc Name rule : from most general features to specialize

- layout
	- about-colored-toolbar-with-title-about
	- list-colored-toolbar-with-title-colored-search-view-list
	- detail-colored-toolbar-with-title-with_shared_button_detail 
	- add-colored-toolbar-with-title-colored-search-add  
- layout-land
	- about-colored-toolbar-with-title-about
	- list-colored-Ushape-toolbar-with-title-white-search-view-transparent-list
	- detail-colored-toolbar-with-title-with_shared_button_detail 
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add
- layout-sw600dp 
	- about-colored-toolbar-without-title-white-card-with-title-about
	- list-colored-Ushape-toolbar-with-title-white-search-view-transparent-list
	- detail-colored-Ushape-toolbar-with-title-white-card-with_shared_button_detail 
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add
- layout-sw600dp-land
	- about-colored-Ushape-toolbar-without-title-white-card-with-title-about
	- list-detail-colored-toolbar-with_title-colored-search-view-list-white-toolbar-with-share-button-detail
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add


## if we remove pairs

	- 	colored-Ushape-toolbar-without-AboutTitle-white-card-with-AboutTitle                                        
	- 	colored-toolbar-with-AboutTitle                                                                      
	- 	colored-toolbar-with-AddTitle-colored-searchview-add                                                 
	- 	colored-Ushape-toolbar-with-Addtitle-white-searchview-transparent-add                                
	- 	colored-Ushape-toolbar-with-DetailTitle-white-card-with_sharedbutton-detail                                 
	- 	colored-toolbar-with-DetailTitle-with_sharedbutton_detail                                            
	- 	colored-toolbar-with-ListTitle-colored-searchview-list                                               
	- 	colored-Ushape-toolbar-with-ListTitle-white-searchview-transparent-list                              
	- 	colored-toolbar-with-ListTitle-colored-searchview-list-white-toolbar-with-sharebutton-detail         



## what will be their controller ?

|Screen                                                                                               | Activity     | Fragment            |
| :-------------------------------------------------------------------------------------------------  | :-----------:| :---------------:  |
| no_layout_it_s_a_launcher                                                                           |MainActivity  |                     | 
|colored-Ushape-toolbar-without-AboutTitle-white-card-with-AboutTitle                                 |AboutActivity  | AboutFragment       |
|colored-toolbar-with-AboutTitle                                                                      |AboutActivity  | AboutFragment       |
|colored-toolbar-with-AddTitle-colored-searchview-add                                                 |AddActivity    | AddFragment       |
|colored-Ushape-toolbar-with-Addtitle-white-searchview-transparent-add                                |AddActivity     | AddFragment       |
|colored-Ushape-toolbar-with-DetailTitle-white-card-with_sharedbutton_detail                          |DetailActivity  | DetailFragment       |
|colored-toolbar-with-DetailTitle-with_sharedbutton_detail                                            |DetailActivity  | DetailFragment       |
|colored-toolbar-with-ListTitle-colored-searchview-list                                               |ListActivity  | ListFragment       |
|colored-Ushape-toolbar-with-ListTitle-white-searchview-transparent-list                              |ListActivity  | ListFragment       |
|colored-toolbar-with-ListTitle-colored-searchview-list-white-toolbar-with-sharebutton-detail         |ListActivity  | ListFragment   DetailFragment    |


	
## Best place to be

### AboutActivity

- in AboutActivity we have 
	- 	colored-Ushape-toolbar-without-AboutTitle-white-card-with-AboutTitle                                        
	- 	colored-toolbar-with-AboutTitle
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			-colored-Ushape-toolbar-                                       
			-colored-toolbar
		- programatically
			- nothing to be set	

### AboutFragment
	
- in AboutFragment we have
	- without-AboutTitle-white-card-with-AboutTitle                                        
	- with-AboutTitle
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			-without-AboutTitle-white-card-with-AboutTitle                                        
			-with-AboutTitle
		- programatically
			- setTitle only if we haven't inflated activity  "colored-Ushape-toolbar-without-AboutTitle-white-card-with-AboutTitle" (see directory check later)
			
### AddActivity

- in AddActivity we have 
	- 	colored-toolbar-with-AddTitle-colored-searchview-add                                      
	- 	colored-Ushape-toolbar-with-AddTitle-white-searchview-transparent-add
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			-colored-Ushape-toolbar-                                       
			-colored-toolbar
		- programatically
			- nothing to be set	

			
### AddFragment
	
- in AddFragment we have
	- 	with-AddTitle-colored-searchview-add                                      
	- 	with-AddTitle-white-searchview-transparent-add
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			- with-AddTitle-colored-searchview-add                                      
			- with-AddTitle-white-searchview-transparent-add
		- programatically
			- setTitle
			

### DetailActivity

- in DetailActivity we have 
	- colored-Ushape-toolbar-with-DetailTitle-white-card-with_sharedbutton_detail                                  
	- colored-toolbar-with-DetailTitle-with_sharedbutton_detail
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			-colored-Ushape-toolbar-                                       
			-colored-toolbar
		- programatically
			- nothing to be set	

### DetailFragment
	
- in DetailFragment we have
	- with-DetailTitle-white-card-with_sharedbutton_detail                                  
	- with-DetailTitle-with_sharedbutton_detail
	- with-white-toolbar-with-sharebutton-detail (2 pane)
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			- with-DetailTitle-white-card-with_sharedbutton_detail                                  
			- with-DetailTitle-with_sharedbutton_detail
		- programatically
			- setTitle on activity toolbar if we have instantiated "with-DetailTitle-with_sharedbutton_detail" otherwise on card toolbar.

			
### ListActivity

- in ListActivity we have 
	- colored-toolbar-with-1-fragment-with-ListTitle-colored-searchview-list        	
	- colored-Ushape-toolbar-with-1-fragment-with-ListTitle-white-searchview-transparent-list
	- colored-toolbar-with-2-fragments-with-ListTitle-colored-searchview-list-white-toolbar-with-sharebutton-detail
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			-colored-toolbar-with-1-fragment                                       
			-colored-Ushape-toolbar-with-1-fragment
			-colored-toolbar-with-2-fragments
		- programatically
			- nothing to be set	
			

### ListFragment
	
- in DetailFragment we have
	- with-ListTitle-colored-searchview-list        	
	- with-ListTitle-white-searchview-transparent-list
	- with-ListTitle-colored-searchview-list- (two-pane)
- are there several files ?
	- do they look very different ? if yes make separate xml files
	- do they look similar ? if yes make one xml file and set the differences progratically.
	- your choice
		- xml : 2 separate  files
			- with-ListTitle-colored-searchview-list        	
			- with-ListTitle-white-searchview-transparent-list
		- programatically
			- setTitle


## copy/paste the directory with long-desc-name layout above

- layout
	- about-colored-toolbar-with-title-about
	- list-colored-toolbar-with-title-colored-search-view-list
	- detail-colored-toolbar-with-title-with_shared_button_detail 
	- add-colored-toolbar-with-title-colored-search-add  
- layout-land
	- about-colored-toolbar-with-title-about
	- list-colored-Ushape-toolbar-with-title-white-search-view-transparent-list
	- detail-colored-toolbar-with-title-with_shared_button_detail 
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add
- layout-sw600dp 
	- about-colored-toolbar-without-title-white-card-with-title-about
	- list-colored-Ushape-toolbar-with-title-white-search-view-transparent-list
	- detail-colored-Ushape-toolbar-with-title-white-card-with_shared_button_detail 
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add
- layout-sw600dp-land
	- about-colored-Ushape-toolbar-without-title-white-card-with-title-about
	- list-detail-colored-toolbar-colored-toolbar-2fragments-with_title-colored-search-view-list-white-toolbar-with-share-button-detail
	- add-colored-Ushape-toolbar-with-title-white-search-view-transparent-add
	
## Remove anything that has to do with fragments

- layout
	- colored-toolbar
	- colored-toolbar
	- colored-toolbar
	- colored-toolbar
- layout-land
	- colored-toolbar
	- colored-Ushape-toolbar
	- colored-toolbar
	- colored-Ushape-toolbar
- layout-sw600dp 
	- colored-toolbar
	- colored-Ushape-toolbar
	- colored-Ushape-toolbar
	- colored-Ushape-toolbar
- layout-sw600dp-land
	- colored-Ushape-toolbar
	- colored-toolbar-2fragments
	- colored-Ushape-toolbar

## Remove pairs

- layout
	- colored-toolbar
- layout-land
	- colored-toolbar
	- colored-Ushape-toolbar
- layout-sw600dp 
	- colored-toolbar
	- colored-Ushape-toolbar
- layout-sw600dp-land
	- colored-Ushape-toolbar
	- colored-toolbar-2fragments
	
## Remove anything that can be found in a less specialized directory. layout-sw600dp-land>layout-sw600dp>layout and layout-land>layout

- layout
	- colored-toolbar
- layout-land
	- colored-Ushape-toolbar
- layout-sw600dp 
	- colored-Ushape-toolbar
- layout-sw600dp-land
	- colored-toolbar-2fragments
	
# You have your activity_layouts. Now do the same for fragments. Copy/Paste. Remove activity stuff.

- layout
	- with-title-about
	- with-title-colored-search-view-list
	- with-title-with_shared_button_detail 
	- with-title-colored-search-add  
- layout-land
	- with-title-about
	- with-title-white-search-view-transparent-list
	- with-title-with_shared_button_detail 
	- with-title-white-search-view-transparent-add
- layout-sw600dp 
	- without-title-white-card-with-title-about
	- with-title-white-search-view-transparent-list
	- with-title-white-card-with_shared_button_detail 
	- with-title-white-search-view-transparent-add
- layout-sw600dp-land
	- without-title-white-card-with-title-about
	- with_title-colored-search-view-list-white-toolbar-with-share-button-detail
	- with-title-white-search-view-transparent-add



- layout
	- with-title-about
	- with-title-colored-search-view-list
	- with-title-with_shared_button_detail 
	- with-title-colored-search-add  
- layout-land
	- with-title-white-search-view-transparent-list
	- with-title-white-search-view-transparent-add
- layout-sw600dp 
	- without-title-white-card-with-title-about
	- with-title-white-search-view-transparent-list
	- with-title-white-card-with_shared_button_detail 
	- with-title-white-search-view-transparent-add
- layout-sw600dp-land
	- with-title-colored-search-view-transparent-list
	- with-white-toolbar-with-share-button-detail
	
# You've got your fragments. Copy/paste activities and fragments together.

- layout
	- colored-toolbar
	- with-title-about
	- with-title-colored-search-view-list
	- with-title-with_shared_button_detail 
	- with-title-colored-search-add  
- layout-land
	- colored-Ushape-toolbar
	- with-title-white-search-view-transparent-list
	- with-title-white-search-view-transparent-add
- layout-sw600dp 
	- colored-Ushape-toolbar
	- without-title-white-card-with-title-about
	- with-title-white-search-view-transparent-list
	- with-title-white-card-with_shared_button_detail 
	- with-title-white-search-view-transparent-add
- layout-sw600dp-land
	- colored-toolbar-2fragments
	- with-title-colored-search-view-transparent-list
	- with-white-toolbar-with-share-button-detail	

# (A) Using what we noted about controlers ("best place to be"), add possibles names of controller layout in front of thoses long-desc-layouts 


		- layout
			- colored-toolbar										->about_activity, add_activity, detail_activity, list_activity									
			- with-title-about										->about_fragment
			- with-title-colored-search-view-list					->list_fragment
			- with-title-with_shared_button_detail 					->detail_fragment
			- with-title-colored-search-add  						->add_fragment
		- layout-land
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
		- layout-sw600dp 
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- without-title-white-card-with-title-about				->about_fragment
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->list_activity
			- with-title-colored-search-view-transparent-list		->list_fragment
			- with-white-toolbar-with-share-button-detail			->detail_fragment

# We have several activities layouts that share the same long-desc_layout what to do ?

- renaming them in a single activity layout eg main_layout ?
	- NO: doind so, we would lose reference to the list_activity, and we don't want that
	- we will create references for them.
- but first lets create references between the long-desc-layouts

# Copy/Paste the liste (A). Remove single long-desc-layouts keep only those which appears at least twice.

		- layout							
		- layout-land
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
		- layout-sw600dp 
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
		- layout-sw600dp-land
			- with-title-colored-search-view-transparent-list		->list_fragment
			- with-title-white-card-with_shared_button_detail		->detail_fragment


# Replace "layout" by "values", add refs.xml to the directory name, put all items in layout, and keep reference to them in ref

		- layout	
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment
			- with-title-colored-search-view-transparent-list		->list_fragment
	
		- values-land/refs.xml
			- layout/colored-Ushape-toolbar							
			- layout/with-title-white-search-view-transparent-list			
			- layout/with-title-white-search-view-transparent-add			
		- values-sw600dp/refs.xml 
			- layout/colored-Ushape-toolbar							
			- layout/with-title-white-search-view-transparent-list			
			- layout/with-title-white-card-with_shared_button_detail 	
			- layout/with-title-white-search-view-transparent-add		
		- values-sw600dp-land/refs.xml
			- layout/with-title-colored-search-view-transparent-list		
			- layout/with-title-white-card-with_shared_button_detail

# Copy/paste list (A).  Remove items we just put in layout.
			
		- layout
			- colored-toolbar										->about_activity, add_activity, detail_activity, list_activity									
			- with-title-about										->about_fragment
			- with-title-colored-search-view-list					->list_fragment
			- with-title-with_shared_button_detail 					->detail_fragment
			- with-title-colored-search-add  						->add_fragment
		- layout-land
		- layout-sw600dp 
			- without-title-white-card-with-title-about				->about_fragment
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->list_activity

# Add items we just put in layout.Now our res directory look like this.

		- layout
			- colored-toolbar										->about_activity, add_activity, detail_activity, list_activity									
			- with-title-about										->about_fragment
			- with-title-colored-search-view-list					->list_fragment
			- with-title-with_shared_button_detail 					->detail_fragment
			- with-title-colored-search-add  						->add_fragment
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment
			- with-title-colored-search-view-transparent-list		->list_fragment			
		- layout-land
		- layout-sw600dp 
			- without-title-white-card-with-title-about				->about_fragment
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->list_activity

		- values-land/refs.xml
			- layout/colored-Ushape-toolbar							
			- layout/with-title-white-search-view-transparent-list			
			- layout/with-title-white-search-view-transparent-add			
		- values-sw600dp/refs.xml 
			- layout/colored-Ushape-toolbar							
			- layout/with-title-white-search-view-transparent-list			
			- layout/with-title-white-card-with_shared_button_detail 	
			- layout/with-title-white-search-view-transparent-add		
		- values-sw600dp-land/refs.xml
			- layout/with-title-colored-search-view-transparent-list		
			- layout/with-title-white-card-with_shared_button_detail


# In value directory add controller called name and where they point

		- values-land/refs.xml
			- about_activity, add_activity, detail_activity, list_activity -> layout/colored-Ushape-toolbar							
			- list_fragment -> layout/with-title-white-search-view-transparent-list			
			- add_fragment -> layout/with-title-white-search-view-transparent-add			
		- values-sw600dp/refs.xml 
			- about_activity, add_activity, detail_activity, list_activity -> layout/colored-Ushape-toolbar							
			- list_fragment -> layout/with-title-white-search-view-transparent-list			
			- detail_fragment -> layout/with-title-white-card-with_shared_button_detail 	
			- add_fragment -> layout/with-title-white-search-view-transparent-add		
		- values-sw600dp-land/refs.xml
			- list_fragment -> layout/with-title-colored-search-view-transparent-list		
			- detail_fragment -> layout/with-title-white-card-with_shared_button_detail

# if several activities add several lines

		- values-land/refs.xml
			- about_activity -> layout/colored-Ushape-toolbar							
			- add_activity -> layout/colored-Ushape-toolbar		
			- detail_activity -> layout/colored-Ushape-toolbar		
			- list_activity -> layout/colored-Ushape-toolbar					
			- list_fragment -> layout/with-title-white-search-view-transparent-list			
			- add_fragment -> layout/with-title-white-search-view-transparent-add			
		- values-sw600dp/refs.xml 
			- about_activity -> layout/colored-Ushape-toolbar							
			- add_activity -> layout/colored-Ushape-toolbar		
			- detail_activity -> layout/colored-Ushape-toolbar		
			- list_activity -> layout/colored-Ushape-toolbar					
			- list_fragment -> layout/with-title-white-search-view-transparent-list			
			- detail_fragment -> layout/with-title-white-card-with_shared_button_detail 	
			- add_fragment -> layout/with-title-white-search-view-transparent-add		
		- values-sw600dp-land/refs.xml
			- list_fragment -> layout/with-title-colored-search-view-transparent-list		
			- detail_fragment -> layout/with-title-white-card-with_shared_button_detail

# Tidy the layout directory

Sort them in real name order

		- layout
			- colored-toolbar										->about_activity, add_activity, detail_activity, list_activity		
			- colored-Ushape-toolbar								->about_activity, add_activity, detail_activity, list_activity			
			- with-title-about										->about_fragment
			- with-title-colored-search-view-list					->list_fragment
			- with-title-white-search-view-transparent-list			->list_fragment
			- with-title-colored-search-view-transparent-list		->list_fragment					
			- with-title-with_shared_button_detail 					->detail_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment			
			- with-title-colored-search-add  						->add_fragment
			- with-title-white-search-view-transparent-add			->add_fragment
		- layout-land
		- layout-sw600dp 
			- without-title-white-card-with-title-about				->about_fragment
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->list_activity

Give them a distinct name

		- layout
			- colored-toolbar										->toolbar_normal_activity		
			- colored-Ushape-toolbar								->toolbar_ushape_activity			
			- with-title-about										->about_fragment
			- with-title-colored-search-view-list					->list_fragment
			- with-title-white-search-view-transparent-list			->list_fragment_white_searchview
			- with-title-colored-search-view-transparent-list		->list_fragment_colored_searchview_transparent
			- with-title-with_shared_button_detail 					->detail_fragment
			- with-title-white-card-with_shared_button_detail 		->detail_fragment_white		
			- with-title-colored-search-add  						->add_fragment
			- with-title-white-search-view-transparent-add			->add_fragment_white
		- layout-land
		- layout-sw600dp 
			- without-title-white-card-with-title-about				->about_fragment
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->list_activity

			
# Put thoses new names in the value directory

		- values-land/refs.xml
			- about_activity -> layout/toolbar_ushape_activity							
			- add_activity -> layout/toolbar_ushape_activity	
			- detail_activity -> layout/toolbar_ushape_activity	
			- list_activity -> layout/toolbar_ushape_activity					
			- list_fragment -> layout/list_fragment_white_searchview			
			- add_fragment -> layout/add_fragment			
		- values-sw600dp/refs.xml 
			- about_activity -> layout/toolbar_ushape_activity							
			- add_activity -> layout/toolbar_ushape_activity		
			- detail_activity -> layout/toolbar_ushape_activity		
			- list_activity -> layout/toolbar_ushape_activity					
			- list_fragment -> layout/list_fragment_white_searchview			
			- detail_fragment -> layout/detail_fragment_white	 	
			- add_fragment -> layout/add_fragment_white		
		- values-sw600dp-land/refs.xml
			- list_fragment -> layout/list_fragment_colored_searchview_transparent		
			- detail_fragment -> layout/detail_fragment_white

			
# We are done. Now we have our final res directory and we know what's shoud be set programmatically

		- layout
			- colored-toolbar										->activity_toolbar_normal		
			- colored-Ushape-toolbar								->activity_toolbar_ushape			
			- with-title-about										->fragment_about
			- with-title-colored-search-view-list					->fragment_list
			- with-title-white-search-view-transparent-list			->fragment_list_white_searchview
			- with-title-colored-search-view-transparent-list		->fragment_list_colored_searchview_transparent
			- with-title-with_shared_button_detail 					->fragment_detail
			- with-title-white-card-with_shared_button_detail 		->fragment_detail_white			
			- with-title-colored-search-add  						->fragment_add
			- with-title-white-search-view-transparent-add			->fragment_add_white
		- layout-land
		- layout-sw600dp 
			- without-title-white-card-with-title-about				->fragment_about
		- layout-sw600dp-land
			- colored-toolbar-2fragments							->activity_list

		- values-land/refs.xml
			<resources>		
				<item name="activity_about" type="layout">@layout/toolbar_ushape_activity</item>							
				<item name="activity_add" type="layout">@layout/toolbar_ushape_activity</item>	
				<item name="activity_detail" type="layout">@layout/toolbar_ushape_activity</item>	
				<item name="activity_list" type="layout">@layout/toolbar_ushape_activity</item>					
				<item name="fragment_list" type="layout">@layout/fragment_list_white_searchview</item>			
				<item name="fragment_add" type="layout">@layout/fragment_add</item>	
			</resources>	
		- values-sw600dp/refs.xml 
			<resources>
				<item name="activity_about" type="layout">@layout/toolbar_ushape_activity</item>							
				<item name="activity_add" type="layout">@layout/toolbar_ushape_activity</item>		
				<item name="activity_detail" type="layout">@layout/toolbar_ushape_activity</item>		
				<item name="activity_list" type="layout">@layout/toolbar_ushape_activity</item>					
				<item name="fragment_list" type="layout">@layout/fragment_list_white_searchview</item>			
				<item name="fragment_detail" type="layout">@layout/fragment_detail_white</item>	 	
				<item name="fragment_add" type="layout">@layout/fragment_add_white</item>
			</resources>	
		- values-sw600dp-land/refs.xml
			<resources>
				<item name="fragment_list" type="layout">@layout/fragment_list_colored_searchview_transparent</item>		
				<item name="fragment_detail" type="layout">@layout/fragment_detail_white</item>
			</resources>
			
			
			AboutActivity : nothing to be set	
			AboutFragment : setTitle only if we haven't inflated activity  "colored-Ushape-toolbar-without-AboutTitle-white-card-with-AboutTitle" (see directory check later)	
			AddActivity : nothing to be set	
			AddFragment : setTitle	
			DetailActivity : nothing to be set	
			DetailFragment : setTitle on activity toolbar if we have instantiated "with-DetailTitle-with_sharedbutton_detail" otherwise on card toolbar.
			ListActivity : nothing to be set				
			ListFragment : setTitle
			
			
			





			

