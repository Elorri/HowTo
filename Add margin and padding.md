components are design/drawn using 8dp cell grid --> padding marging should be multiple of 8. more infos :https://www.google.com/design/spec/resources/sticker-sheets-icons.html#
if you want your press area to be large, better use padding

use standard

	@dimen/abc_list_item_padding_horizontal_material

or use custom

	<!-- Margin and padding -->
    <dimen name="spacing_small">8dp</dimen>
    <dimen name="spacing_normal">16dp</dimen>
    <dimen name="spacing_medium">24dp</dimen>
    <dimen name="spacing_large">32dp</dimen>
    <dimen name="spacing_xlarge">40dp</dimen>
    <dimen name="spacing_xxlarge">60dp</dimen>
    <dimen name="spacing_xxxlarge">90dp</dimen>
    <dimen name="spacing_xxxxlarge">120dp</dimen>