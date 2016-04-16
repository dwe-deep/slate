# Advanced Integration Guide

## Tracking Custom Events

DMA allows you to add custom attributes to automatically collected events or collect your own events with their custom attributes.
Examples of custom events:

* preloading ad
* watching ad
* skipping ad
* placing order
* sign up

Examples of custom dimensions (attributes):

* video title
* video author
* video tags
* user id
* user email
* order id
* product name
* product price

### Adding custom attributes to automatically collected events

> Example: Add custom dimensions (attributes) to all video events

```html
<video
    data-title="Rick Astley"
    data-author="Never Gonna Give You Up"
    data-tags="musicvideo pop youtube redhead baddancing"
    width="640" height="360" autoplay controls loop
  src="http://web.advertine.com/video/Rick_Astley_Never_Gonna_Give_You_Up_medium.mp4">
</video>
```

If the DMA main script is loaded you can easily add custom attributes to automatically collected events. To create your own attribute follow this schema:

`data-yourcustomattribute="your custom data"`

DMA will automatically replace “data-” part with an appropriate context. For example, if you place your custom attribute inside `<video>` tag DMA will recognize the video context and your data will look like this:

`video.yourcustomattribute="your custom data"`

<aside class="notice">
Please remember, that the custom attribute will be added to all automatically collected events in the context where the attribute is present.
</aside>


## Collecting custom events with custom attributes

> Example: Register an event when an ad has been watched

```javascript
deep.event({"event.type": "ad-watched"});
```

> Example: Register user sign up event

```javascript
deep.event({"event.type": "signup", "user.id.email": "john.doe@yahoo.com"}}});

> OR

deep.event({event: {type: "signup"}, user: {id: {email: "john.doe@yahoo.com"}}});
```

> Example result:

```
event.type: "signup"
event.timestamp: exact time of an event
user.id.email: "john.doe@yahoo.com"
```

> Example: Register leaving a comment by registered user event

```javascript
deep.event({
	"event.type": "user-comment-added",
	userComment: {
		from: deep.hash("some.user@mail.com"),
 	inReplyTo: deep.hash("other.user@mail.com")
}
});
```

Deep Media Analytics also allows you to collect custom events with custom attributes. To trigger DMA to register an event you can use previously defined global function deep (see Chapter 2). It takes as a parameter your data in JSON format. 

As a result you’ll see in your analytics this data:

`
event.type: "ad-watched"
event.timestamp: exact time of an event
`

As a result you’ll see in your analytics this data:





If event.type property is not specified it defaults to “custom-event”.

## Custom server-side transformations

```javascript
	var published = new Date(2016, 3, 12, 23, 31, 33);
	deep({"published.date": published}});
	deep.transform({dateSplit: {
	fromField: "published.date",
	toField: "published",
	mode: "merge"}
	});
```

> As a result you’ll see in your analytics this data:

```
	published.date: "2016-04-12T21:31:33.000Z"
	published.year: 2016
	published.month: April
	published.monthno: 4
	published.day: 12
	published.hour: 21
	published.minute: 31
	published.second: 33
	published.weekday: “Mon”
	published.weekdayno: 1
	published.utcoffset: 0
```

Deep Media Analytics also allows you to specify custom transformations (see Transformation API Documentation).

# Examples of Custom Data Tracking

## Subdomains & Mobile Domains

Usually Publisher employ various types of subdomains:

* special purpose, “technical” subdomains like: www.yoursite.com, ww1.yoursite.com, ww2.yoursite.com
* subject related subdomains, e.g.: technology.yoursite.com, fashion.yoursite.com, etc.
* mobile subdomains: m.yoursite.com

To track traffic from all subdomains you’ll need obviously to deploy DMA code across all pages. By default our system treats every subdomain as a separate site, however there are simple ways to reconfigure it to your convenience.

In the Tracking Settings you can configure default prefixes that let system know which domains should be treated separately and which data should be integrated. For example there’s a common practise to setup prefixes like “www.”, “ww2.” or “m.” to be consolidated with the main domain.

The second method to consolidate data into one main domain from other subdomains (or even completely different domains!) is to overwrite an original page domain with the one you’ll want to. 

To do this just put the simple line of code on the website that should be consolidated (e.g. mobileversion.yoursite.com, mobileversionofyoursite.com etc.):

`
deep({"page.domain": "yoursite.com"});
`

## Canonical links

Does your site use query parameters for various tracking purposes, (e.g. seeing people who came from an email newsletter)? Or does your site have multiple URL structures for the same page/article (e.g. domain.com/section/artcle vs m.domain.com/12345)?

By default, DMA is configured to use either the raw path or canonical links (when available). We strongly encourage implementing canonical links to ensure consistent tracking of pages and to prevent seeing multiple listings of the same page in the DMA Dashboard. If you're not familiar with canonical links, check out Google's Guide to Canonical Links.

To utilize the canonical feature, you'll need to ensure that your site defines canonical links for each page (e.g <link rel='canonical'.../>) and that the pageCanonical option is set to true.

`
deep.options.pageCanonical = true;
`

## Custom path variable

If you are unable or prefer to not use canonical links, you may alternatively set the Path Variable. The path must start with "/" (forward slash) and we highly recommend that you use a real path used to navigate to this page.
The value set for the Path Variable should be generated by your CMS or set to window.location.pathname, so that the same piece of code can be used on all pages.

<b>Examples of setting the Path Variable:</b>

`deep({"page.path": "/some/article/path"});`

`deep({"page.path": cms.path.variable});`

## Custom page titles
By default DMA displays page titles by using the `<title>` tag in your site's header.

You can override the title used for a page in DMA by setting the Title Variable. This can be useful when all pages have a common prefix (e.g. "Publication Name: Story Title"), or when most pages share a common site title.

You can set the title variable manually, or populate it dynamically by tying it to a variable in your CMS.

Here you can set the title like this:

`deep({"page.title": "Story Title"});`

`deep({"page.title": cms.title.variable});`


## Sections & Authors
In DMA you can filter your content by e.g. section or author. In fact it could be any dimension that fits your site’s structure. To implement this feature, you’ll need to set up section and author variables within the DMA code. So if a page is written by Bob Johnson in the section US Politics, you would set:

`
deep({
	section: "US Politics",
	"author.name": "Bob Johnson"
});
`

A page can both be in multiple sections and/or have multiple authors, therefore each variable accepts a comma separated list of values or an array of values. So if a page is co-written by Megan Summers and Kevin Smith in the sections Fashion and Fashion News, you would set:

`
deep({
	section: ["Fashion", "Fashion News"],
	"author.name": ["Megan Summers", "Kevin Smith"]
});
`

The sections variable does not need to reflect real sections on the site, but should be thought of as groupings of pages that can be filtered on. Our suggestion is to populate these fields dynamically by tying them to a variable in your CMS which globally represents your sections and authors, so they can be easily changed.

`
deep({
	section: cms.sections.variable,
	"author.name": cms.authors.variable
});
`

You can also populate these variables by using page metadata, a tag that already exists in your code, or part of your URL structure which contains these values.
E.g. (using jQuery helpers)

`
deep(function(params) {
	params.section = $("#page-info").data("section");
	params["author.name"] = $("#page-info").data("authors");
});
`

The above code assumes that on your page there is HTML Tag with id=”page-info”
E.g.

`<section id="page-info" data-section="Fashion News" data-authors="Kevin Smith">`

## Ajax & infinite scroll
<aside class="notice">[Available in Q2 2016]</aside>

If your site uses infinite scroll, serves up content dynamically via AJAX, or pages change without the URL subsequently changing or the DOM refreshing, you’ll need to do some additional implementation.

Anytime a visitor navigates to a new page or piece of content, you’ll need to call a custom function called page. This function is specifically designed for this kind of page change, and can be attached to click/swipe events, or to a pixel that is used to trigger content changes. Best practice is to make sure that the page function is called whenever you change to a new page of content using AJAX, so they always happen together.

You’ll need to setup logic to handle these lines of code:

`
deep.newpage({
	"page.path":"/newpath",
	title: "New title",
	section: "New Section",
	"author.name": "New Author"
});
`

Simply put, you’re setting the author and section (if they change) ahead of time since we take that data as holdover information when we reload the page with page(). If we are not passed the updated section and author information we’ll continue to register the original sections and authors from the previous page. If the new page has no section or author data, simply set that variable to "null". For example:

`
deep.newpage({
	"page.path":"/newpath",
	"page.title": "New title",
	section: "New Section",
	"author.name": null
});
`

Next, when the page changes we’ll need to populate the path and title for the new page(s) within the page variable, so that the pings will reflect the new page the visitor is on.

<aside class="notice">
<b>Important Note</b>: newpage should never be called when a user initially arrives on a page from an external source, and should only be called when a user navigates to subsequent pages without causing the DOM to be refreshed.
<br><br>
For pages with infinite scroll, any time a visitor is scrolling down to a new page, they will ping on each distinct URL they hit at least once.
</aside>

## Cookies

DMA uses one first-party cookies.

The _dtentr cookie is used to register if a user has visited the domain before and to calculate visitor frequency.

### Disabling Cookies
Customers who are subject to the EU e-Privacy Directive, or who would prefer not to use cookies, can set the following variable to prevent DMA from using cookies

`deep.options.doNotTrack = true;`

<aside class="notice">
Note: By using DMA without cookies, you will be unable to see some user-related metrics.
</aside>