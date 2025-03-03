# Customize Image Gallery Control

Forked from [xwp](https://github.com/xwp/wp-customize-image-gallery-control)

See [usage](https://make.xwp.co/2016/08/12/image-gallery-control-for-the-customizer/)

Using in [Slow Wheels WP theme](https://github.com/madeslowly/slow-wheels) to select images for footer logos.

Adds Customizer support for image gallery control type.

## Description ##
Adds new Customizer control type `image_gallery` by extending WP_Customize_Control class. Allows choosing multiple images from Media Library, saves the ID-s as an array.
Displays icons of the images in Customizer.

Requires PHP 5.3+

Add functions to theme `function.php`

```PHP
function the_featured_image_gallery( $atts = array() ) {
    $setting_id = 'featured_image_gallery';
    $ids_array = get_theme_mod( $setting_id );
    if ( is_array( $ids_array ) && ! empty( $ids_array ) ) {
        $atts['ids'] = implode( ' ', $ids_array );
        echo gallery_shortcode( $atts );
    }
}
```

Usage `<?php the_featured_image_gallery(); ?>`

Shortcode functionality, add to theme `function.php`

```PHP
function featured_image_gallery_shortcode( $atts ) {
    $ids_array = get_theme_mod( 'featured_image_gallery' );
    if ( is_array( $ids_array ) && ! empty( $ids_array ) ) {
        $ids = implode( ',', $ids_array );
        $atts = ['include' => $ids ];
    }
    return gallery_shortcode( $atts );
}
add_shortcode( 'featured_image_gallery', 'featured_image_gallery_shortcode' );

```

Usage `[featured_image_gallery]`

Shortcode is supposed to accept usual `[gallery]` args but I cant seem to get it to work. [See comment](https://make.xwp.co/2016/08/12/image-gallery-control-for-the-customizer/#comment-24472)
