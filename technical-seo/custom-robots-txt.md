# Custom robots.txt for WordPress

Examples and recommendations for creating a clean and SEO-friendly robots.txt configuration for WordPress websites.

---

## Basic WordPress robots.txt Example

```txt
User-agent: *

Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php

Disallow: /wp-content/plugins/
Disallow: /wp-content/cache/
Disallow: /cgi-bin/

Disallow: */trackback/
Disallow: */feed/
Disallow: */comments/

Sitemap: https://example.com/sitemap.xml
```
## WooCommerce Example

```txt
User-agent: *

Disallow: /cart/
Disallow: /checkout/
Disallow: /my-account/

Disallow: /*?orderby=
Disallow: /*?filter_
Disallow: /*?rating_filter=

Allow: /wp-admin/admin-ajax.php

Sitemap: https://example.com/sitemap.xml
```
## Recommendations

### Block unnecessary technical pages

Usually there is no reason to allow indexing for:

cart pages
checkout pages
internal search results
filter parameters
tracking parameters

### Be careful with CSS and JavaScript blocking

Modern search engines need access to:

CSS
JavaScript
images

to properly render pages.

Avoid blocking:
```txt
/wp-content/themes/
/wp-content/uploads/
```
unless there is a very specific reason.

### Always add sitemap location

Example:
```txt
Sitemap: https://example.com/sitemap.xml
```
This helps search engines discover URLs faster.

---

## Common Mistakes

### Blocking the entire website
```txt
Disallow: /
```
This completely blocks indexing.

### Blocking uploads directory
```txt
Disallow: /wp-content/uploads/
```
This may negatively affect image indexing and page rendering.

### Over-optimizing robots.txt

Too many unnecessary rules may:

confuse crawlers
block important resources
create indexing issues

Simple configurations are often better.

---

## Testing

After updating robots.txt:

test it in Google Search Console
check page rendering
verify sitemap accessibility
monitor indexation changes

---

## Related Topics

Technical SEO
XML Sitemaps
Crawl Budget Optimization
WordPress SEO
WooCommerce SEO

---

## Author

Bohdan Prytulyak
PBB Design
