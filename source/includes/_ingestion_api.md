# Ingestion API

## Introduction

Ingestion API lets you ingest data to deep.bi analytics engine. In this simple way you can measure your KPIs by tracking any event that people or machines generate, for example:

* purchases
* app downloads
* web page impressions
* signups
* location data from beacons
* data from wearables
* clicks in marketing campaign
* social media events, like twitter posts
* ... or any custom event you need.

deep.bi Ingestion API is a HTTP REST API and it accepts data in JSON format.

## Authentication

To send your data you'll need two keys: `STREAM_ID WRITE_API_KEY`

`STREAM_ID` determines where your data will be stored. You can have any number of streams you want, for example for different stores, projects or your clients (if you provide analytics to your customers).

`WRITE_API_KEY` is your authorization key related to your accunt, that allows you to send data.

To get these keys please refer http://deep.bi/admin page.

## Basic Example

> Example JSON with buyer and purchase item data

```json
{
    "event_type": "purchase",
    "user_id": "12345",
    "user_email": "john.doe@awesomemail.com",
    "item": "67890",
    "price": 175.00,
    "currency": "USD"
}
```
> Sending event

```shell
curl "https://api.deep.bi/v1/streams/STREAM_ID/events/data?accessKey=WRITE_API_KEY" \
  -H "Content-Type: application/json" -d @event1.json
```  

Let's start with the simple case of tracking a transaction in an online store.

JSON objects are represented by keys and values. In deep.bi keys will become dimensions or metrics, depending on how do you would like your data to be interpreted. The cool thing is that you can don't have to make the decision while ingesting data. Just send it like it is, and decide later, while querying your data for analysis.

Now we will send this event via API using a POST request. In this example we are using <a href="https://curl.haxx.se/">cURL</a>, a command line tool. You can use any programming language you want.

<aside class="notice">
Make sure to use the correct STREAM_ID and WRITE_API_KEY.
</aside>

<aside class="success">And that's it! If you have received 204 return code then your event went to deep.bi correctly.
</aside>

## More complex events: nested data and custom event time

>Example JSON

```json
{
  "event_type": "purchase",
  "event_time": "2015-10-12T14:42:15.123Z",
  "user_id": "12345",
  "user_email": "john.doe@awesomemail.com",
  "item": {
    "id": "67890",
    "url": "http://www.myshop.com/item/1234565",
    "name": "Nike Air Zoom Structure 19 Flash iD",
    "categories": ["clothing", "shoes", "athlete shoes"],
    "brand": "Nike",
    "color": "graphite",
    "size": 9
  },
  "price": 175.00,
  "currency": "USD"
}
```

> Sending event with getEventTime

```shell
curl "https://api.deep.bi/v1/streams/STREAM_ID/events/data?getEventTime=purchaseTime" \
  -H "Authorization: Bearer WRITE_API_KEY" \
  -H "Content-Type: application/json" -d @event2.json
```

Values of event dimensions can be a string, a number or an array of strings or numbers. You can also nest objects to group dimensions under a single key.

This time we'd like to provide mora data about the item, like its name, page url, item's categories and parameters.

In the previous event we did not provide transaction timestamp, so the API has assigned the time when our server received your data. Now we want to send the time when the user actually purchased item. To do it just add a dimension containing that time and tell our API where we should look for it using the `getEventTime` parameter.