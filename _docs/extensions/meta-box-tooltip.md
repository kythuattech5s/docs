---
title: Meta Box Tooltip
---

{% include installation.html %}

## Usage

**Make sure you know how to [register meta boxes](/registering-meta-boxes/) and [define fields](/field-settings/) before continuing!**

To add a tooltip to a meta field, simply add `tooltip` parameter for that field. You can define tooltip in one of following formats:

- `'tooltip' => 'Tooltip content',`
- `'tooltip' => array( 'icon' => 'info', 'position' => 'top', 'content' => 'Tooltip content' )`

e.g. if the `tooltip` is a string, the plugin will use icon info and take the string as the tooltip content. If the `tooltip` is an array, then it accepts the following parameters:

Parameter|Description
---|---
`icon`|The tooltip icon. It can be `info` (default), `help` or *URL to custom icon image*. Since version 0.1.1, you can *use any Dashicons* for the icon by specifying its name, for example `dashicons-email`. For full list of Dashicons, please read [this page](https://developer.wordpress.org/resource/dashicons/).
`position`|The tooltip position. Can be `top` (default), `bottom`, `left` or `right`. Optional.
`content`|Tooltip content.

This code below adds tooltip to 3 fields:

```php
add_filter( 'rwmb_meta_boxes', 'meta_box_tooltip_demo_register' );
function meta_box_tooltip_demo_register( $meta_boxes ) {
	$meta_boxes[] = array(
		'title'  => __( 'Meta Box Tooltip Demo', 'meta-box' ),
		'fields' => array(
			array(
				'name'    => __( 'Default', 'meta-box' ),
				'id'      => 'name',
				'type'    => 'text',

				// Add tooltip to field label, in one of following formats
				// 1) 'tooltip' => 'Tooltip Content'
				// 2) 'tooltip' => array( 'icon' => 'info', 'content' => 'Tooltip Content', 'position' => 'top' )
				// 3) 'tooltip' => array( 'icon' => 'https://url-to-icon-image.png', 'content' => 'Tooltip Content', 'position' => 'top' )
				//
				// In 1st format, icon will be 'info' by default
				// In 2nd format, icon can be 'info' (default), 'help' or any Dashicons (see https://developer.wordpress.org/resource/dashicons/)
				// In 3rd format, icon can be URL to custom icon image
				//
				// 'position' is optional. Value can be 'top' (default), 'bottom', 'left', 'right'
				'tooltip' => __( 'Info icon, top position', 'meta-box' ),
			),
			array(
				'name'    => __( 'Help icon', 'meta-box' ),
				'id'      => 'job',
				'type'    => 'text',
				'tooltip' => array(
					'icon'     => 'help',
					'content'  => __( 'Right position', 'meta-box' ),
					'position' => 'right',
				),
			),
			array(
				'name'    => __( 'Dashicon', 'meta-box' ),
				'id'      => 'email',
				'type'    => 'text',
				'tooltip' => array(
					'icon'     => 'dashicons-email',
					'content'  => __( 'Dashicon', 'meta-box' ),
					'position' => 'right',
				),
			),
			array(
				'name'    => __( 'Custom image', 'meta-box' ),
				'id'      => 'email',
				'type'    => 'text',
				'tooltip' => array(
					'icon'     => 'https://i.imgur.com/ZQI2DNx.png',
					'content'  => __( 'Custom icon', 'meta-box' ),
					'position' => 'right',
				),
			),
		),
	);
	return $meta_boxes;
}
```

## Adding tooltip for inputs

The default behavior adds tootips for field labels. Since version 1.1, the plugin supports adding tooltips for field inputs. Because of variation in the UI, the plugin supports only these fields: date time fields, text input fields (`text`, `url`, `email`, `number`, `password`) and select fields.

The option for this feature is `tooltip_input`, which accepts the same parameters as for `tooltip`.