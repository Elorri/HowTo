# Make sure all components are focusable and reachable if using

## D-pads
## trackballs
## keyboard
## navigation gestures

# Make sure audio app feedback have non audio equivalent like

## notification
## haptic feedback
## visual feedback


# Add Talback

## Set content descriptions 

### for user interface components that do not have visible text. eg: ImageButton, Button, checkbox, ImageView

minimum to add 

	android:contentDescription
	setContentDescription("book cover");
	setContentDescription(null)  -> graphics are only decorative and don't add infos.
	
to allow focus on the image

    android:focusable="true"
	
if use of focusable attribute in ListView add

    android:descendantFocusability="blocksDescendants"
	
in the root view of the item_layout otherwise the onItemClicked method won't work.
	
### for custom views

need to implement accessibility interfaces

### for widgets

Content Descriptions for RemoteViews were only added in ICS MR1

            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.ICE_CREAM_SANDWICH_MR1) {
                setRemoteContentDescription(views, description);
            }
			
			@TargetApi(Build.VERSION_CODES.ICE_CREAM_SANDWICH_MR1)
			private void setRemoteContentDescription(RemoteViews views, String description) {
				views.setContentDescription(R.id.widget_icon, description);
			}

## Turn on TalkBack an check

Parametres>Accessibility>Acces Direct> TalkBack + Accessibilité
+
Parametres>Accessibility>Vue> TalkBack

Pour desactiver

Ecran d'acceuil > Appli > Settings > Accessibility>Vue> TalkBack

# Add Text-to-speech
# Add Haptic feedback
# Add Gesture Navigation
# Add Trackball
# Add Directional Pad Navigation



