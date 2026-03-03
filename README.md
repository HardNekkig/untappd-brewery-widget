=== Untappd Brewery Widget ===

Requires PHP: 7.4

License: GPL-2.0-or-later

Displays the latest check-ins for a brewery fetched live from the Untappd API.

== Description ==

Untappd Brewery Widget pulls real-time check-in data from the Untappd API and
displays it on your WordPress site. It supports classic widget areas, the block
editor (via the Legacy Widget block), and a shortcode for embedding inside any
page or post content.

Features:

* Live check-in feed for any brewery
* Configurable count (1–25 check-ins)
* Optional display of avatar, username, timestamp, beer label, beer name,
  beer style, star rating, check-in comment, and check-in photo
* Customisable colours and border radius
* API response caching (configurable TTL, default 5 minutes)
* Theme-adaptive — inherits fonts and colours from your active theme
* Dark mode aware via prefers-color-scheme

== Requirements ==

* WordPress 5.8 or later
* PHP 7.4 or later
* A free Untappd API application (Client ID + Client Secret)
* Your brewery's Untappd Brewery ID

== Installation ==

1. Upload the `untappd-brewery-widget` folder to `/wp-content/plugins/`.
2. Activate the plugin through **Plugins → Installed Plugins**.
3. Go to **Settings → Untappd Widget** and enter your API credentials
   (see "Getting your API credentials" below).
4. Place the widget using one of the three methods described in "Usage".

== Getting your API credentials ==

You need a free Untappd API application to use this plugin.

1. Sign in to Untappd, then visit https://untappd.com/api/register.
2. Fill in the application form (the Callback URL can be your site's homepage).
3. After approval (usually instant) you will receive a **Client ID** and a
   **Client Secret**. Copy both values into **Settings → Untappd Widget**.

Finding your Brewery ID:

1. Open your brewery's page on Untappd in a browser.
2. The URL will look like: https://untappd.com/brewery/431566
3. The number at the end (e.g. `431566`) is your Brewery ID.

== Configuration ==

All global options live in **Settings → Untappd Widget**:

= API Credentials =
* **Brewery ID** — The numeric ID from your brewery's Untappd URL.
* **Client ID** — From your registered Untappd API application.
* **Client Secret** — From your registered Untappd API application.

= Fetch Settings =
* **Number of check-ins** — How many check-ins to display (1–25).
* **Cache duration** — How long (in minutes) to cache the API response before
  fetching fresh data. Default: 5 minutes. Range: 1–1440 (24 hours).

= Display Fields =
Toggle which parts of each check-in are shown:
* User avatar
* User name
* Check-in time (displayed as "X minutes ago")
* Beer label image
* Beer name (links to the check-in on Untappd)
* Beer style
* Rating (five-star display)
* Check-in comment
* Check-in photo

= Colours =
* **Star / accent colour** — Used for filled and half-filled stars.
  Default: `#f5a623` (Untappd amber). Supports a colour picker.
* **Border colour** — Outer border of each check-in card.
* **Separator colour** — Divider between check-in cards.
* **Hover background** — Background highlight when hovering a card.
* **Border radius** — Corner rounding for cards (any valid CSS length, e.g. `8px`).

Tip: All colours support `rgba()` values for transparency, which works well
on both light and dark themes.

= Cache =
Click **Flush Cache Now** to force a fresh API fetch immediately (e.g. after
a notable check-in you want to appear right away). The cache is also flushed
automatically whenever you save the settings.

== Usage ==

= Option 1: Classic widget area =

1. Go to **Appearance → Widgets**.
2. Find **Untappd Brewery Check-ins** in the available widgets list.
3. Drag it into any sidebar or footer widget area.
4. Optionally set a custom **Widget Title** or a per-widget **Brewery ID**
   override (useful if you run multiple breweries on one site).
5. Click **Save**.

= Option 2: Block editor / Full Site Editing =

1. Open any page, post, or template in the block editor.
2. Add a new block and search for **Legacy Widget**.
3. In the Legacy Widget block, select **Untappd Brewery Check-ins** from the
   dropdown.
4. Optionally set a custom Widget Title or Brewery ID override.
5. Save the page or template.

= Option 3: Shortcode =

Embed the widget inside any page, post, or text widget using:

    [untappd_checkins]

This uses all values from **Settings → Untappd Widget**. You can override
individual settings per-shortcode:

    [untappd_checkins brewery_id="431566" count="10" title="Fresh Pours"]

Shortcode attributes:

| Attribute    | Description                                    | Default            |
|--------------|------------------------------------------------|--------------------|
| brewery_id   | Brewery ID to display (overrides global)       | Global setting     |
| count        | Number of check-ins to show (1–25)             | Global setting     |
| title        | Heading displayed above the check-in list      | "Latest Check-ins" |

Display fields and colours are always taken from the global settings page and
cannot be overridden per shortcode.

== Frequently Asked Questions ==

= I get a blank widget. What is wrong? =

If you are logged in as an administrator you will see an error message instead
of a blank area. Common causes:

* Missing or incorrect Client ID / Client Secret — double-check the values in
  Settings → Untappd Widget against your API application page.
* Invalid Brewery ID — make sure it is the numeric ID from the URL, not the
  brewery's name.
* Untappd API is temporarily unavailable — wait a few minutes and flush the
  cache, or check https://status.untappd.com.

= How do I show different breweries on different pages? =

Use the shortcode with a per-instance `brewery_id`:

    Page A: [untappd_checkins brewery_id="111"]
    Page B: [untappd_checkins brewery_id="222"]

Or place the widget multiple times with different Brewery ID overrides in the
widget form.

= How do I reduce API requests? =

Increase the **Cache duration** in the settings. A value of 30–60 minutes is
reasonable for most brewery sites; the feed rarely needs to be real-time.

= The styles look wrong on my theme. =

The widget inherits fonts and most colours from your active theme. If something
looks off, try adjusting the **Colours** settings on the settings page. You can
also add custom CSS targeting `.untappd-brewery-widget` in your theme customiser.

= Can I show check-ins from a user instead of a brewery? =

No — this plugin is specifically designed for brewery check-in feeds using the
`/brewery/checkins/{id}` Untappd API endpoint.

= Does this work without a widget area? =

Yes. Use the shortcode (`[untappd_checkins]`) to embed the feed inside any page
or post, even on themes that do not have traditional widget areas (including
headless/block themes).

== Changelog ==

= 1.2.0 =
* Added shortcode support: [untappd_checkins brewery_id="" count="" title=""]
* Fixed CSS not loading when widget is placed via the block editor Legacy Widget block
* Bumped version to 1.2.0

= 1.1.0 =
* Added global Settings page (Settings → Untappd Widget) with API credentials,
  display field toggles, colour customisation, and cache management
* Per-widget brewery ID override
* Configurable cache TTL
* Dark mode support via prefers-color-scheme
* Theme-adaptive styles (inherits fonts and colours)
* Star rating renderer with half-star support

= 1.0.0 =
* Initial release
