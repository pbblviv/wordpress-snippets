# Disable Unused WordPress Features

Simple ways to disable unnecessary WordPress features for better performance, security and cleaner frontend output.

---

## Why Disable Unused Features?

By default, WordPress loads many features that may not be needed on production websites.

Disabling unnecessary functionality may help:
- improve performance
- reduce HTTP requests
- clean up page source
- improve Core Web Vitals
- reduce plugin conflicts

---

## Disable Emojis

WordPress loads emoji scripts and styles on every page.

### Example

```php
remove_action( 'wp_head', 'print_emoji_detection_script', 7 );
remove_action( 'wp_print_styles', 'print_emoji_styles' );
remove_action( 'admin_print_scripts', 'print_emoji_detection_script' );
remove_action( 'admin_print_styles', 'print_emoji_styles' );
```

## Disable Embeds

Embeds are often unnecessary on business websites.

### Example
```php
function disable_wp_embeds() {
    wp_dequeue_script( 'wp-embed' );
}
add_action( 'wp_footer', 'disable_wp_embeds' );
```

## Disable XML-RPC

If XML-RPC is not used, disabling it may improve security.

### Example
```php
add_filter( 'xmlrpc_enabled', '__return_false' );
```

## Remove Dashicons for Guests

Dashicons are often loaded for non-logged-in users even when not needed.

### Example
```php
function remove_dashicons_frontend() {
    if ( ! is_user_logged_in() ) {
        wp_deregister_style( 'dashicons' );
    }
}
add_action( 'wp_enqueue_scripts', 'remove_dashicons_frontend' );
```

## Disable REST API for Guests (Optional)

Be careful with this optimization because some plugins may require REST API access.

### Example
```php
add_filter( 'rest_authentication_errors', function( $result ) {
    if ( ! empty( $result ) ) {
        return $result;
    }

    if ( ! is_user_logged_in() ) {
        return new WP_Error(
            'rest_not_logged_in',
            'REST API restricted.',
            array( 'status' => 401 )
        );
    }

    return $result;
});
```

## Recommendations

Before disabling features:

- test plugin compatibility
- check WooCommerce functionality
- verify forms and APIs
- monitor frontend errors

Some themes and plugins may depend on:

- REST API
- embeds
- XML-RPC
- WordPress scripts
- Related Topics
- WordPress Performance
-Core Web Vitals
- Technical SEO
- Website Optimization
- WooCommerce Performance
  
## Author

- Bohdan Prytulyak
- PBB Design
- https://pbb.design
