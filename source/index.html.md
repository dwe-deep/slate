---
title: Developer Guide

language_tabs:
  - javascript

toc_footers:
  - <a href='http://www.deep.bi/'>Sign Up for a DeepBI account</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - advanced_integration
  - events
  - data_attributes

search: true
---

# Introduction

The Deep Media Analytics (DMA) is a part of the Deep.BI platform. It allows to track users’ interactions with web content using JavaScript snippets or REST API. 

Deep Media Analytics supports:

* web events,
* mobile events,
* HTML native video players,
* HTML native audio players,
* any other data send via REST API in JSON format.

The goal of this document is to assist the developer responsible for integration of Deep.BI. This document describes integration with JavaScript, but integration can be done with REST API. 

The DMA JavaScript code is fully asynchronous in order to not slow down publisher’s site. Once loaded, DMA code works like most other analytics services — it triggers the loading of a beacon image, which returns a 1x1 pixel image.

# Quick Start Guide

## Implementation

> To implement DMA tracking script, past this code into head section:

```javascript
<script type="text/javascript">//<![CDATA[
/* Deep Media Analytics (c) 2016-04-15 v1.2.0 */
!function(){function b(a,b){"function"!=typeof f[a]&&(f[a]=b)}function e(c,d,e,f,a){var b=function(b){Object.freeze&&freeze(b);var j=e.push(b),h=g[f];if(h)for(var i=0;i<h.length;++i)h[i](d,b,c[5],j);return a};return a||(a=b),b}function n(d){var c,b=a[l]("script");for(b.type="text/javascript",b.async=!0,b.src="http"+("https:"===a.location.protocol?"s:":":")+d;!(c=a[i](h)[0]);)a[i]("html")[0][k](a[l](h));c[k](b)}var a,m=new Date,j=new Function("return this;")(),c=j.top;try{a=c.document}catch(o){}void 0===a&&(c=j,a=c.document);var f=c.DeepTrack||(c.DeepTrack={}),d={},g={};b("hash",function(a){function hash(){return a}return hash}),b("each",function(c,a){a||(a=1);for(var e in d)for(var f=d[e],h=f[a],i=f[5],b=0;b<h.length;++b)c(e,h[b],i,b);var j=g[a]||(g[a]=[]);j.push(c)}),b("getInitTime",function(){return m}),b("options",function(a){return d[a][0].options}),b("track",function(c,g){var a,h,i,j,k,b=d[c];return b?(a=b[0],g&&(b[5]=g)):(d[c]=b=[0,h=[],i=[],j=[],k=[],g],b[0]=a=e(b,c,h,1),a.event=e(b,c,i,2,a),a.transform=e(b,c,j,3,a),a.newpage=e(b,c,k,4,a),a.hash=f.hash,a.options={}),a});var l="createElement",i="getElementsByTagName",k="appendChild",h="head";n("//api.deep.bi/scripts/v1/track.js")}();//]]>
</script>)
```

Installing DMA JavaScript code should be as easy as pasting this snippet inside the `<head>` tag, preferably right after the opening:

## Authorization

To send data you need to obtain two authorization keys:

* Stream ID
* Write Key

You can set a global variable containing your authorization keys or send them every time you send data. 

For the first option put an authorization snippet below the main loading script.

```javascript
<script type="text/javascript">
var deep = DeepTrack.track("YOUR_STREAM_KEY", "YOUR_WRITE_KEY");
</script>
```

<aside class="notice">
You must replace <code>YOUR_STREAM_KEY</code> and <code>YOUR_WRITE_KEY_KEY</code> with your account credentials.
</aside>

## Sending data

To start collecting data put the following script in the place where it should be fired:

In most cases it can be anywhere in the <body> section of a page. The script will gather automatically pre-defined type of events - see Section 3.

If you’d like to gather other events you should put additional, custom lines of the script in a place where these events occur adding to it some custom parameters. For more details see Section 5.

```javascript
<script type="text/javascript">
deep({});
</script>
```

