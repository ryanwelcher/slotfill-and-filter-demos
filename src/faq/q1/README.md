# How do I add a Panel the Document sidebar?

This question has come up multiple times for me.

To be clear, this is the sidebar we are discussing:

![Document Sidebar](../../../../master/assets/images/q1-screenshot.png?raw=true)


# TL;DR Solution

Use a standard meta box to add an item to the bottom of the panel.

# Full Solution

There is no API available in Gutenberg to insert items into the sidebar. It has been [discussed](https://github.com/WordPress/gutenberg/issues/13357) and may be implemented in the future.

The current solution is to use [add_meta_box](https://developer.wordpress.org/reference/functions/add_meta_box/) to register a meta box in PHP and set its context to `side`.
This will add it to the bottom of the panel.


# Code Example

```php
/**
 * Register meta box(es).
 */
function register_meta_boxes() {
	add_meta_box(
		'meta-box-id',
		'Custom Meta Box',
		__NAMESPACE__ . '\render_meta_box',
		'post',
		'side' // this is important
	);
}
add_action( 'add_meta_boxes', __NAMESPACE__ . '\register_meta_boxes' );

/**
 * Meta box display callback.
 *
 * @param \WP_Post $post Current post object.
 */
function render_meta_box( $post ) {
	?>
	<p>Added to the Document Sidebar</p>
	<?php
}

```


