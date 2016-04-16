# Data Attributes

All collected events will be automatically enriched by a whole set of additional dimensions in the following areas:

* Event Context
* Video / Audio Context
* Page Context
* User Location Context, 
* User Internet Provider Context
* User Device Context


## Event Context

<table>
<tr>
<th width="15%">Variable name</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>event.type</td>
<td>Type of event - see chapter 3 (e.g. video_play)</td>
</tr>
<tr>
<td>event.timestamp</td>
<td>Timestamp of the event</td>
</tr>
<tr>
<td>event.localtime.year</td>
<td>Year, e.g. 2016</td>
</tr>
<tr>
<td>event.localtime.month</td>
<td>Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec</td>
</tr>
<tr>
<td>event.localtime.monthno</td>
<td>Number of the month: 1, 2, … 12, where 1 is January, 12 is December</td>
</tr>
<tr>
<td>event.localtime.day</td>
<td>Day of the month: 1, 2, … [28 | 29 | 30 | 31] </td>
</tr>
<tr>
<td>event.localtime.hour</td>
<td>Hour of the day: 0, 1, 2, … 23</td>
</tr>
<tr>
<td>event.localtime.minute</td>
<td>Minute of the hour: 0, 1, 2, … 59</td>
</tr>
<tr>
<td>event.localtime.weekday</td>
<td>Sun, Mon, Tue, Wed, Thu, Fri, Sat</td>
</tr>
<tr>
<td>event.localtime.weekdayno</td>
<td>0, 1, … 6, where 0 is Sunday, and 6 is Saturday</td>
</tr>
<tr>
<td>event.localtime.utcoffset</td>
<td>Local timezone offset in minutes from UTC.</td>
</tr>
<tr>
<td>event.pingseq</td>
<td>Sequence number of page ping event. This is a technical parameter that is used for track detailed active user engagement (Attention Time Spent) in accordance to the public <a href="https://chartbeat.com/public-release-methodology/">Chartbeat methodology.<a></td>
</tr>
</table>

## Page Context

Page context characterizes the place on the web where users are browsing an article, watching a video and where they came from.

There are two high level groups of parameters: page and referrer.  

**Page** is a web page (URL)  where the video was loaded from. 

**Referrer** is a URL of a web page that a user had visited before he or she came to the page.
<aside class="notice">
Remarks: Referrer is registered when referrer page is linking to the visited page.
</aside>

The colours in the table corresponds with the example below.

<table>
<tr>
<th width="20%">Event Type</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>page.domain</td>
<td>This should be set explicitly by client’s script.</td>
</tr>
<tr>
<td>page.title</td>
<td>HTML head <i>title</i> of the page</td>
</tr>
<tr>
<td>page.protocol</td>
<td>Usually http or https</td>
</tr>
<tr>
<td>page.host</td>
<td>Domain with page.port e.g. www.nytimes.com:8222</td>
</tr>
<tr>
<td>page.hostname</td>
<td>Domain, e.g. www.nytimes.com</td>
</tr>
<tr>
<td>page.port</td>
<td>HTTP protocol port. When a page use the default http port 80, the field is empty.</td>
</tr>
<tr>
<td>page.path</td>
<td>Part of the URL, excluding page.protcol, page.host, page.search  and page.hash</td>
</tr>
<tr>
<td>page.href</td>
<td>URL of the page where the video was loaded from, without parameters (page.protocol + page.host + page.path)</td>
</tr>
<tr>
<td>page.search</td>
<td>Parameter string in the URL starting after “?” character</td>
</tr>
<tr>
<td>page.query.[parameter]</td>
<td>Parsed search parameter (see above) where [parameter] is the parameter name. 
For example URL:
'http://deep.bi/?utm_source=google&utm_medium=cpc
page.query.utm_source=”google”
page.query.utm_medium=”cpc”'</td>
</tr>
<tr>
<td>page.hash</td>
<td>Parameter string in the URL starting after “#” character</td>
</tr>
<tr>
<td>page.loadTime</td>
<td>Time to load the page in milliseconds (page-open events only)</td>
</tr>
<tr>
<td>referrer.protocol</td>
<td>Usually http or https</td>
</tr>
<tr>
<td>referrer.host</td>
<td>Domain with page.port e.g. www.nytimes.com:8222</td>
</tr>
<tr>
<td>referrer.hostname</td>
<td>Domain, e.g. www.nytimes.com</td>
</tr>
<tr>
<td>referrer.port</td>
<td>HTTP protocol port. When a page use the default http port 80, the field is empty.</td>
</tr>
<tr>
<td>referrer.path</td>
<td>Part of the URL, excluding page.protcol, page.host, page.search  and page.hash</td>
</tr>
<tr>
<td>referrer.href</td>
<td>URL of the page where the video was loaded from, without parameters (page.protocol + page.host + page.path)</td>
</tr>
<tr>
<td>referrer.search</td>
<td>Parameter string in the URL starting after “?” character</td>
</tr>
<tr>
<td>referrer.query.[parameter]</td>
<td>Parsed search parameter (see above) where [parameter] is the parameter name.
'http://deep.bi/?utm_source=google&utm_medium=cpc
page.query.utm_source=”google”
page.query.utm_medium=”cpc”</td>'
</tr>
<tr>
<td>referrer.hash</td>
<td>Parameter string in the URL starting after “#” character</td>
</tr>
</table>

## Video or Audio Context

<aside class="notice">
Available in Q2 2016
</aside>

DMA script collects all available audio or video attributes when an event occurs. In the table below we list those attributes. In data loaded to DMA the [media] will be replaced by video or audio accordingly. If an attribute is present with one kind of events only (audio or video) we put that in the table.

<table>
<tr>
<th width="15%">Variable name</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>[media].autoplay</td>
<td>A Boolean attribute; if specified, the video automatically begins to play back as soon as it can do so without stopping to finish loading the data.Note: Some versions of Chrome only acknowledge autostart, rather than autoplay</td>
</tr>
<tr>
<td>[media].buffered</td>
<td>An attribute you can read to determine the time ranges of the buffered media. This attribute contains a TimeRanges object.</td>
</tr>
<tr>
<td>[media].controls</td>
<td>If this attribute is present, the browser will offer controls to allow the user to control video playback, including volume, seeking, and pause/resume playback.</td>
</tr>
<tr>
<td>video.crossorigin</td>
<td>This enumerated attribute indicates whether to use CORS to fetch the related image. CORS-enabled resources can be reused in the <i>canvas</i> element without being tainted. The allowed values are:
<br><b>anonymous</b><br>
Sends a  cross-origin request without a credential. In other words, it sends the Origin: HTTP header without a cookie, X.509 certificate, or performing HTTP Basic authentication. If the server does not give credentials to the origin site (by not setting the Access-Control-Allow-Origin: HTTP header), the image will betainted, and its usage restricted.
<br><b>use-credentials</b><br>
Sends a  cross-origin request with a credential. In other words, it sends the Origin: HTTP header with a cookie, a certificate, or performing HTTP Basic authentication. If the server does not give credentials to the origin site (throughAccess-Control-Allow-Credentials: HTTP header), the image will be tainted and its usage restricted.
<br><br>When not present, the resource is fetched without a CORS request (i.e. without sending the Origin: HTTP header), preventing its non-tainted used in <i>canvas</i> elements. If invalid, it is handled as if the enumerated keyword anonymous was used. See CORS settings attributes for additional information.</td>
</tr>
<tr>
<td>video.height</td>
<td>The height of the video's display area, in CSS pixels.</td>
</tr>
<tr>
<td>[media].loop</td>
<td>A Boolean attribute; if specified, we will, upon reaching the end of the video, automatically seek back to the start.</td>
</tr>
<tr>
<td>[media].muted</td>
<td>A Boolean attribute which indicates the default setting of the audio contained in the video. If set, the audio will be initially silenced. Its default value is false, meaning that the audio will be played when the video is played.</td>
</tr>
<tr>
<td>[media].played</td>
<td>A TimeRanges object indicating all the ranges of the video that have been played.</td>
</tr>
<tr>
<td>[media].preload</td>
<td>This enumerated attribute is intended to provide a hint to the browser about what the author thinks will lead to the best user experience. It may have one of the following values:
<br><b>none</b>: indicates that the video should not be preloaded.
<br><b>metadata</b>: indicates that only video metadata (e.g. length) is fetched.
<br><b>auto</b>: indicates that the whole video file could be downloaded, even if the user is not expected to use it.
<br><b>the empty string</b>: synonym of the auto value.
<br>If not set, its default value is browser-defined (i.e. each browser may have its default value). The spec advises it to be set to metadata.
<br><br><i>Usage notes:
<br>The autoplay attribute has precedence over preload. If autoplay is specified, the browser would obviously need to start downloading the video for playback.
The specification does not force the browser to follow the value of this attribute; it is a mere hint.</i></td>
</tr>
<tr>
<td>video.poster</td>
<td>A URL indicating a poster frame to show until the user plays or seeks. If this attribute isn't specified, nothing is displayed until the first frame is available; then the first frame is shown as the poster frame.</td>
</tr>
<tr>
<td>[media].src</td>
<td>The URL of the video to embed. This is optional; you may instead use the <source>element within the video block to specify the video to embed.</td>
</tr>
<tr>
<td>video.width</td>
<td>The width of the video's display area, in CSS pixels.</td>
</tr>
<tr>
<td>[media].volume</td>
<td>The playback volume, in the range 0.0 (silent) to 1.0 (loudest).</td>
</tr>

</table>

## User ID Context

List of user IDs.

<table>
<tr>
<th width="20%">Variable name</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>user.id.deepcookie</td>
<td>Cookie that installed by DMA script</td>
</tr>
<tr>
<td>user.id.ip</td>
<td>User IP number</td>
</tr>
<tr>
<td>user.id.session</td>
<td>Unique session ID used for joining user events within one session</td>
</tr>
<tr>
<td>user.id.fingerprint</td>
<td><b><i>[available Q3 2016]</i></b> Unique user ID based of browser fingerprinting. </td>
</tr>
</table>

## User Attention Context

User attention characteristics.

<table>
<tr>
<th width="20%">Variable name</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>user.attention.active</td>
<td>Active time spent on page in milliseconds</td>
</tr>
<tr>
<td>user.attention.idle</td>
<td>Idle time spent on page in milliseconds</td>
</tr>
<tr>
<td>user.attention.total</td>
<td>Total time spent on page in milliseconds</td>
</tr>
</table>

## User Location Context

<aside class="notice">
Available in Q2 2016
</aside>

User location characterizes physical user location based on user IP address.

<table>
<tr>
<th width="20%">Variable name</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>user.location.country</td>
<td>User country</td>
</tr>
<tr>
<td>user.location.region</td>
<td>User region (state, county, province)</td>
</tr>
<tr>
<td>user.location.city</td>
<td>User City</td>
</tr>
<tr>
<td>user.location.population</td>
<td>City population</td>
</tr>
</table>

## User Internet Provider

<aside class="notice">
Available in Q2 2016
</aside>

This context describes the internet provider a user is using during the web event.

<table>
<tr>
<th width="20%">Variable name</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>user.isp.name</td>
<td>Name of internet service provider</td>
</tr>
</table>

## User Device Context

<aside class="notice">
Available in Q2 2016
</aside>

User device context describes characteristics of the device a user is using.

<table>
<tr>
<th width="20%">Variable name</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>user.device.screen.width</td>
<td>Device screen width</td>
</tr>
<tr>
<td>user.device.screen.height</td>
<td>Device screen height</td>
</tr>
<tr>
<td>user.device.screen.availWidth</td>
<td>Device screen width minus system taskbar</td>
</tr>
<tr>
<td>user.device.screen.availHeight</td>
<td>Device screen height minus system taskbar</td>
</tr>
<tr>
<td>user.device.screen.orientation</td>
<td>Device orientation</td>
</tr>
<tr>
<td>user.device.type</td>
<td>For example: tablet, smartphone, tv, desktop</td>
</tr>
<tr>
<td>user.device.brand</td>
<td>For example: Apple, Samsung</td>
</tr>
<tr>
<td>user.device.model</td>
<td>For example: iPhone 5, Galaxy III</td>
</tr>
<tr>
<td>user.device.browser.producer</td>
<td>For example: Google, Mozilla, Microsoft</td>
</tr>
<tr>
<td>user.device.browser.name</td>
<td>For example: Internet Explorer</td>
</tr>
<tr>
<td>user.device.browser.version</td>
<td>Detailed version of user browser</td>
</tr>
<tr>
<td>user.device.agent</td>
<td>Full user-agent string</td>
</tr>
</table>
