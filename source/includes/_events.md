# Events

Various events are sent when handling media that are embedded in HTML documents using the `<audio>` and `<video>` elements; this section lists them and provides some helpful information about using them. Moreover, DMA collect automatically web events like opening a page, page load time, page bounce etc.

## Website Events

<table>
<tr>
<th width="15%">Event Type</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>page-open</td>
<td>User opened a page</td>
</tr>
<tr>
<td>page-ping</td>
<td>Page-ping event is sent after each 15 seconds of user activity. Each event in user session has its number in sequence, starting from 1 (dimension: pingSeq). That means that DMA customers can easily and flexibly define custom event like Page View 30s+ with pingSeq = 2.</td>
</tr>
</table>

## Media Events (Audio & Video)

<aside class="notice"><b>[Available in Q2 2016]</b></aside>

Media companies can use the  HTML `<video>` element to embed video content in a document. The video element contains one or more video sources. To specify a video source, use either the src attribute or the `<source>` element; the browser will choose the most suitable one.

The HTML `<audio>` element is used to embed sound content in documents. It may contain one or more audio sources, represented using the src attribute or the `<source>` element; the browser will choose the most suitable one.

Below you’ll see the list of events that are gathered automatically by DMA script. You will see in your data “audio” or “video” prefix accordingly, depending of the media event type.

For example, instead of [media]-play, we will capture audio-play or video-play event.

<table>
<tr>
<th width="20%">Event Type</th>
<th width="80%">Description</th>
</tr>
<tr>
<td>[media]-abort</td>
<td>Sent when playback is aborted; for example, if the media is playing and is restarted from the beginning, this event is sent.</td>
</tr>
<tr>
<td>[media]-canplay</td>
<td>Sent when enough data is available that the media can be played, at least for a couple of frames.  This corresponds to the HAVE_ENOUGH_DATA readyState.</td>
</tr>
<tr>
<td>[media]-canplaythrough</td>
<td>Sent when the ready state changes to CAN_PLAY_THROUGH, indicating that the entire media can be played without interruption, assuming the download rate remains at least at the current level. Note: Manually setting thecurrentTime will eventually fire a canplaythrough event in firefox. Other browsers might not fire this event.</td>
</tr>
<tr>
<td>[media]-durationchange</td>
<td>The metadata has loaded or changed, indicating a change in duration of the media.  This is sent, for example, when the media has loaded enough that the duration is known.</td>
</tr>
<tr>
<td>[media]-emptied</td>
<td>The media has become empty; for example, this event is sent if the media has already been loaded (or partially loaded), and the load() method is called to reload it.</td>
</tr>
<tr>
<td>[media]-encrypted</td>
<td>The user agent has encountered initialization data in the media data.</td>
</tr>
<tr>
<td>[media]-ended</td>
<td>Sent when playback completes.</td>
</tr>
<tr>
<td>[media]-error</td>
<td>Sent when an error occurs.  The element's error attribute contains more information. See Error handling for details.</td>
</tr>
<tr>
<td>[media]-interruptbegin</td>
<td>Sent when audio playing on a Firefox OS device is interrupted, either because the app playing the audio is sent to the background, or audio in a higher priority audio channel begins to play. See Using the AudioChannels API for more details.</td>
</tr>
<tr>
<td>[media]-interruptend</td>
<td>Sent when previously interrupted audio on a Firefox OS device commences playing again — when the interruption ends. This is when the associated app comes back to the foreground, or when the higher priority audio finished playing. See Using the AudioChannels API for more details.</td>
</tr>
<tr>
<td>[media]-loadeddata</td>
<td>The first frame of the media has finished loading.</td>
</tr>
<tr>
<td>[media]-loadedmetadata</td>
<td>The media's metadata has finished loading; all attributes now contain as much useful information as they're going to.</td>
</tr>
<tr>
<td>[media]-loadstart</td>
<td>Sent when loading of the media begins.</td>
</tr>
<tr>
<td>[media]-mozaudioavailable</td>
<td>Sent when an audio buffer is provided to the audio layer for processing; the buffer contains raw audio samples that may or may not already have been played by the time you receive the event.</td>
</tr>
<tr>
<td>[media]-pause</td>
<td>Sent when playback is paused.</td>
</tr>
<tr>
<td>[media]-play</td>
<td>Sent when playback of the media starts after having been paused; that is, when playback is resumed after a prior pause event.</td>
</tr>
<tr>
<td>[media]-playing</td>
<td>Sent when the media begins to play (either for the first time, after having been paused, or after ending and then restarting).</td>
</tr>
<tr>
<td>[media]-progress</td>
<td>Sent periodically to inform interested parties of progress downloading the media. Information about the current amount of the media that has been downloaded is available in the media element's buffered attribute.</td>
</tr>
<tr>
<td>[media]-ratechange</td>
<td>Sent when the playback speed changes.</td>
</tr>
<tr>
<td>[media]-seeked</td>
<td>Sent when a seek operation completes.</td>
</tr>
<tr>
<td>[media]-seeking</td>
<td>Sent when a seek operation begins.</td>
</tr>
<tr>
<td>[media]-stalled</td>
<td>Sent when the user agent is trying to fetch media data, but data is unexpectedly not forthcoming.</td>
</tr>
<tr>
<td>[media]-suspend</td>
<td>Sent when loading of the media is suspended; this may happen either because the download has completed or because it has been paused for any other reason.</td>
</tr>
<tr>
<td>[media]-timeupdate</td>
<td>The time indicated by the element's currentTime attribute has changed.</td>
</tr>
<tr>
<td>[media]-volumechange</td>
<td>Sent when the audio volume changes (both when the volume is set and when the muted attribute is changed).</td>
</tr>
<tr>
<td>[media]-waiting</td>
<td>Sent when the requested operation (such as playback) is delayed pending the completion of another operation (such as a seek).</td>
</tr>
</table>
