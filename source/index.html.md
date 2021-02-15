---
title: eventrac API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:


includes:
  - errors

search: true
---

# Introduction

Welcome to the eventrac developer API. You can use our API to access Event/Race information and add Participants to a given Race.

To help with development, a collection of API calls are available in postman.  This is using our sandbox environment.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/7b2e5dada17d7ae157fd)

**This is an in development API**

# How it works

This version of the eventrac API uses [jSend](https://metacpan.org/pod/JSON::JSend) as the protocol to communicate between the client and the server
 An example response might look like (see right).

 > A typical successful response:

 ```json

{
    "status": "success",
    "data": {
        "participant": {
            "address_1": "",
            "address_2": "",
            "address_country": "",
            "emergency_name": "",
            "emergency_number": "",
            "id": 44362,
            "race_id": 123,
            "first_name": "Aaron",
            "last_name": "Bird",
            "email": "aaron@eventrac.co.uk",
            "dob": "1992-01-01T00:00:00+00:00",
            "external_reference": "my-external-reference",
            "gender": "m"
        }
    },
    "links": []
}
```

> A typical response with validation errors:

```json
{
    "status": "error",
    "message": "Validation failed",
    "code": 422,
    "data": {
        "external_reference": {
            "unique": "The provided value is invalid"
        }
    }
}
```

# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: yourapikey"
```


> Make sure to replace `yourapikey` with your API key.

eventrac uses API keys to allow access to the API.  To receive an API key, please contact organiser.support@eventrac.co.uk

eventrac expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: yourapikey`

<aside class="notice">
You must replace <code>yourapikey</code> with your personal API key.
</aside>

# Organisers

## Get All Events for an organiser

```shell
curl "https://www.eventrac.co.uk/api/v2/organisers/<ORGANISER_ID>/events"
  -H "Authorization: yourapikey"
```

> The above command returns JSON array of events, structured like this:

```json
[
   {
      "id":59,
      "name":"Thames Meander",
      "description":"<p>A scenic summer run starting from the YMCA Hawker Centre....</p>",
      "url":"https://www.eventrac.co.uk/listed-races/thames-meander",
      "has_future_races": true
   },
   {
      "id":60,
      "name":"Bewl Water",
      "description":"<p>A scenic summer run starting from the YMCA Hawker Centre....</p>",
      "url":"https://www.eventrac.co.uk/listed-races/bewl-water-marathon-and-half-marathon",
      "has_future_races": true
   },
   {
      "id":61,
      "name":"Bewl Water Ultra",
      "description":"<p>A scenic summer run starting from the YMCA Hawker Centre....</p>",
      "url":"https://www.eventrac.co.uk/listed-races/bewl-water-ultra",
      "has_future_races": false
   }
]
```

This endpoint retrieves all events for a given organiser.

### HTTP Request

`GET https://www.eventrac.co.uk/api/v2/organisers/<ORGANISER_ID>/events`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
ORGANISER_ID | The ID of the event organiser

### Response

Parameter | Description
--------- | ------- | -----------
id | The ID of the event
name | The Name of the event
description | A description about the event
url | The URL to the eventrac landing page
has_future_races | Boolean indicating if this event has any races in the future


<aside class="notice">
Please email organiser.support@eventrac.co.uk for details of an organisers id
</aside>

# Events

## Get all future Races for an Event

<aside class="notice">
A "future race" is considered any race with a date in in the future
</aside>


```shell
curl "https://www.eventrac.co.uk/api/v2/events/<EVENT_ID>/races"
  -H "Authorization: yourapikey"
```


> The above command returns a JSON array of race objects:

```json
[
   {
      "id":728,
      "name":"Half Marathon",
      "capacity":500,
      "participant_count":150,
      "date":"2018-05-12T09:00:00+00:00",
      "closing_date":"2018-05-07T23:00:00+00:00",
      "event":{
         "id":60,
         "name":"Bewl Water",
         "url":"https://www.eventrac.co.uk/listed-races/bewl-water-marathon-and-half-marathon",
         "description":"<p>A scenic summer run starting from the YMCA Hawker Centre....</p>",
         "has_future_races": true
      },
      "has_capacity":true,
      "status":"closed",
      "price":{
         "amount":3000,
         "currency":"GBP",
         "booking_fee":150,
         "booking_fee_paid_by":"participant"
      },
      "url":"https://www.eventrac.co.uk/race-course-map/bewl-water-half-marathon-12-05-2018-09-00"
   },
   {
      "id":729,
      "name":"Marathon",
      "capacity":500,
      "participant_count":150,
      "date":"2018-05-12T08:00:00+00:00",
      "closing_date":"2018-05-07T23:00:00+00:00",
      "event":{
         "id":60,
         "name":"Bewl Water",
         "url":"https://www.eventrac.co.uk/listed-races/bewl-water-marathon-and-half-marathon",
         "description":"<p>A scenic summer run starting from the YMCA Hawker Centre....</p>",
         "has_future_races": true
      },
      "has_capacity":true,
      "status":"closed",
      "price":{
         "amount":3800,
         "currency":"GBP",
         "booking_fee":190,
         "booking_fee_paid_by":"participant"
      },
      "url":"https://www.eventrac.co.uk/race-course-map/bewl-water-marathon-12-05-2018-08-00"
   }
]
```

This endpoint retrieves all races (in the future) for a given event

### HTTP Request

`GET https://www.eventrac.co.uk/api/v2/events/<EVENT_ID>/races`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
EVENT_ID | The ID of the event to retrieve

### Response

Parameter | Description
--------- | ------- | -----------
data | An array of races (See getting an individual race)




## Get a Specific Event

```shell
curl "https://www.eventrac.co.uk/api/v2/events/<ID>"
  -H "Authorization: yourapikey"
```


> The above command returns a JSON event object structured like this:

```json

```

This endpoint retrieves a specific event.

<aside class="warning">This endpoint has not yet been implemented</aside>

### HTTP Request

`GET https://www.eventrac.co.uk/api/v2/events/<ID>`

### Request Parameters

Parameter | Description
--------- | -----------
ID | The ID of the event to retrieve

### Event Object

Parameter | Description
--------- | -----------
id | The ID of the event
name | The Name of the event
description | The description of the event as set by the organiser
url | The URL of the event
has_future_races | Boolean indicating if this event has any races in the future

# Races

## Get a Specific Race

```shell
curl "https://www.eventrac.co.uk/api/v2/races/<ID>"
  -H "Authorization: yourapikey"
```


> The above command returns a JSON race object structured like this:

```json
{
   "id":851,
   "name":"Whiteley Village 10Km",
   "capacity":300,
   "participant_count":150,
   "date":"2018-06-10T08:00:00+00:00",
   "closing_date":"2017-06-08T12:00:00+00:00",
   "description": "<p>This is my race description</p>",
   "event":{
      "id":100,
      "name":"Whiteley Village Races",
      "url":"https://www.eventrac.co.uk/listed-races/whiteley-races",
      "description": "<p>This is my event description</p>",
      "has_future_races": true
   },
   "has_capacity":true,
   "status":"closed",
   "price":{
      "amount":1800,
      "currency":"GBP",
      "booking_fee":83,
      "booking_fee_paid_by":"organiser"
   },
   "url":"https://www.eventrac.co.uk/race-course-map/whiteley-village-races-whiteley-village-10km-10-06-2018-08-00"
}
```

This endpoint retrieves a specific race

<aside class="warning">Attention should be given to has_capacity and the status.  These can be considered the criteria to enable new participants to enter</aside>

### HTTP Request

`GET https://www.eventrac.co.uk/api/v2/races/<ID>`

### Request Parameters

Parameter | Description
--------- | -----------
ID | The ID of the race to retrieve

### Race Object

Parameter | Description
--------- | -----------
id | The ID of the race
name | The Name of the race
capacity | The capacity of the race.  Once this is met *has_capacity* will be false
participant_count | The number of confirmed participants.
date | The date of the event in UTC
closing_date | The closing date of the event in UTC
description | The race description as set by the organiser
event | The event object (see event object)
has_capacity | Boolean indicating if the race has capacity for new participants to enter
status | One of "open", "closed", "full" - "open" indicates that participants can enter this race.  "closed", "full" indicates the race cannot be entered at this time
price | A price object describing the entry price and booking fees
 | **amount** - the price of the race as advertised to the participant (without any booking fees)
 | **currency** - the currnecy of any fees
 | **booking_fee** - the eventrac booking fee
 | **booking_fee_paid_by** - who pays the booking fee.  Can be either *organiser* or *participant*.  In the case of *participant*, this should be added to the amount.
url | A url to the eventrac landing page for this race

# Participants

## Retrieve a participant

```shell
curl "https://www.eventrac.co.uk/api/v2/partcipants/<ID>/<EXTERNAL-REFERENCE>"
  -H "Authorization: yourapikey"
```


> The above command returns a JSON participant object structured like this:

```json
{
   "id":44287,
   "race_id":756,
   "first_name":"Aaron",
   "last_name":"Bird",
   "dob":"1986-05-04T00:00:00+00:00",
   "external_reference":"5ac897c6dc7a10001596163b",
   "gender":"m"
}

```

This endpoint retrieves information about a specific participant

<aside class="warning">For privay reasons, the participant's address and contact details will not be returned from this endpoint</aside>

### HTTP Request

`GET https://www.eventrac.co.uk/api/v2/participants/<EXTERNAL-REFERENCE>`

### Request Parameters

Parameter | Description
--------- | -----------
EXTERNAL-REFERENCE | The source booking platforms reference

### Response - Participant Object

Parameter | Description
--------- | -----------
id | The ID of the participant
race_id | The ID of the race they are entered into
first_name | The first name of the participant
last_name | The last name of the participant
dob | The dob of the participant
external_reference | The reference of the external booking agent
gender | The gender of the participant


## Add a single Participant to a Race

```shell
curl -X POST "https://www.eventrac.co.uk/api/v2/races/<ID>/participants"
  -H "Authorization: yourapikey"
  -d {"race_id":123,"first_name":"Aaron","last_name":"Bird","gender":"m","dob":"1992-01-13","external_reference":"123"}

```


> The above command returns a JSON participant object structured like this:

```json
{
   "id":44287,
   "race_id":756,
   "first_name":"Matt",
   "last_name":"Woollard",
   "dob":"1985-01-20T00:00:00+00:00",
   "email": "aaron@eventrac.co.uk",
   "external_reference":"my_reference_123",
   "gender":"m",
   "address_1":"",
   "address_2":"",
   "address_city":"",
   "address_zip_code":"",
   "address_state":"",
   "address_country":"",
   "contact_number":"",
   "emergency_name":"",
   "emergency_number":""
}

```

This endpoint adds a participant to a race

<aside class="notice">The participants address and contact details will only be returned upon a successful response</aside>


### HTTP Request

`POST https://www.eventrac.co.uk/api/v2/races/<ID>/participants`

### Request (POST)  Parameters

Parameter | Required | Description
--------- | ----------- | -----------
ID | true | The ID of the race to add this participant to
external_reference | true | The source booking platforms reference - Must be unique for each participant of the same race
email | true | The participants email address
first_name | false | The participants first name
last_name | false | The participants last name
dob | false | The participants date of birth.  Should be in format **Y-m-d**
gender | false | The participants gender.  Should be one of **f** (female), **m** (male), **nb** (non binary)
address_1 | false | The participants address line 1
address_2 | false | The participants address line 2
address_city | false | The participants address town/city
address_zip_code | false | The participants address post code/zip code
address_state | false | The participants address county/state
address_country | false | The participants address country
contact_number | false | The participants contact number
emergency_name | false | The name of the person to contact in case of emergency
emergency_number | false | The contact number of the person to contact in case of emergency
metadata | false | A set of key/value pairs that you can attach to the participant object.  This can be useful for passing in additional entry form questions i.e. UKA Affiliation Number or a stripe transfer identifier etc..


### Response - Participant Object

Parameter | Description
--------- | -----------
id | The ID of the participant
race_id | The ID of the race they are entered into
first_name | The first name of the participant
last_name | The last name of the participant
dob | The dob of the participant
external_reference | The reference of the external booking agent
gender | The gender of the participant
email | The participants email address
address_1 | The participants address line 1
address_2 | The participants address line 2
address_city | The participants address town/city
address_zip_code | The participants address post code/zip code
address_state | The participants address county/state
address_country | The participants address country
contact_number | The participants contact number
emergency_name | The name of the person to contact in case of emergency
emergency_number | The contact number of the person to contact in case of emergency

## Add multiple Participants to Race(s)

```shell
curl -X POST "https://www.eventrac.co.uk/api/v2/participants"
  -H "Authorization: yourapikey"
  -d {"participants":[{"race_id":123,"first_name":"Aaron","last_name":"Bird","gender":"m","dob":"1992-01-13","external_reference":"123"},{"race_id":123,"first_name":"Aaron","last_name":"Bird","gender":"m","dob":"1992-01-13","external_reference":"123-1","address_zip_code":"1234","metadata":{"hello":"world","another":"day"}}]}

```


> The json request object should look like this

```json
{
   "participants":[
      {
         "race_id":123,
         "first_name":"Aaron",
         "last_name":"Bird",
         "gender":"m",
         "dob":"1986-04-05",
         "external_reference":"123"
      },
      {
         "race_id":456,
         "first_name":"Sarah",
         "last_name":"Harding",
         "gender":"f",
         "dob":"1990-01-13",
         "external_reference":"123-1222"
      }
   ]
}
```

> The above command returns a JSON participant object structured like this:

```json
{
   "status":"success",
   "data":{
      "hasErrors":true,
      "participants":[
         {
            "external_reference":"123",
            "errors":{
               "external_reference":{
                  "unique":"The provided value is invalid"
               }
            }
         },
         {
            "id":44322,
            "race_id":123,
            "first_name":"Aaron",
            "last_name":"Bird",
            "dob":"2018-06-15T00:00:00+00:00",
            "external_reference":"123-1222",
            "email": "aaron@eventrac.co.uk",
            "gender":"m",
            "address_1":"",
            "address_2":"",
            "address_city":"",
            "address_zip_code":"",
            "address_state":"",
            "address_country":"",
            "contact_number":"",
            "emergency_name":"",
            "emergency_number":""
         }
      ]
   },
   "links":[

   ]
}
```

This endpoint adds a participant to a race

### HTTP Request

`POST https://www.eventrac.co.uk/api/v2/races/participants`

This endpoints expects and array of participants

### Request (POST) Parameters

Parameter | Required | Description
--------- | ----------- | -----------
participants[0][email] | true | The participants email
participants[0][external_reference] | true | The source booking platforms reference - Must be unique for each participant of the same race
participants[0][first_name] | false | The participants first name
participants[0][last_name] | false | The participants last name
participants[0][dob] | false | The participants date of birth.  Should be in format **Y-m-d**
participants[0][gender] | false | The participants gender.  Should be one of **f** (female), **m** (male), **nb** (non binary)
... | false | see Adding an individual participant for further options

### Response - Participant Object

Parameter |  Description
--------- | -----------
hasErrors | If any of the participants could not be saved, this will hasErrors = *true*
participants | An array of participants - See the participant response object

## Update a participant

```shell
curl -X PUT "https://www.eventrac.co.uk/api/v2/participants/<EXTERNAL-REFERENCE>"
  -H "Authorization: yourapikey"
  -d {"participant":{"first_name":"Aaron","last_name":"Tweet","gender":"f","dob":"1992-05-14","address_1":"lighthouse"}}

```


> The above command returns a JSON participant object structured like this:

```json
{
   "id":44287,
   "race_id":756,
   "first_name":"Matt",
   "last_name":"Woollard",
   "dob":"1985-01-20T00:00:00+00:00",
   "email": "aaron@eventrac.co.uk",
   "external_reference":"my_reference_123",
   "gender":"m",
   "address_1":"",
   "address_2":"",
   "address_city":"",
   "address_zip_code":"",
   "address_state":"",
   "address_country":"",
   "contact_number":"",
   "emergency_name":"",
   "emergency_number":""
}

```

This endpoint updates a participant

<aside class="notice">The External Reference is required as proof of ownership.  Failure to provide an external reference will result in a 403</aside>


### HTTP Request

`PUT https://www.eventrac.co.uk/api/v2/participants/<EXTERNAL-REFERENCE>`

### Request (PUT)  Parameters

Parameter | Required | Description
--------- | ----------- | -----------
EXTERNAL-REFERENCE | true | The source booking platforms reference
email | false | The participants email address
first_name | false | The participants first name
last_name | false | The participants last name
dob | false | The participants date of birth.  Should be in format **Y-m-d**
gender | false | The participants gender.  Should be one of **f** (female), **m** (male), **nb** (non binary)
external_reference | true | The source booking platforms reference - Must be unique for each participant of the same race
address_1 | false | The participants address line 1
address_2 | false | The participants address line 2
address_city | false | The participants address town/city
address_zip_code | false | The participants address post code/zip code
address_state | false | The participants address county/state
address_country | false | The participants address country
contact_number | false | The participants contact number
emergency_name | false | The name of the person to contact in case of emergency
emergency_number | false | The contact number of the person to contact in case of emergency
metadata | false | A set of key/value pairs that you can attach to the participant object.  This can be useful for passing in additional entry form questions i.e. UKA Affiliation Number or a stripe transfer identifier etc..


### Response - Participant Object

Parameter | Description
--------- | -----------
id | The ID of the participant
race_id | The ID of the race they are entered into
first_name | The first name of the participant
last_name | The last name of the participant
dob | The dob of the participant
external_reference | The reference of the external booking agent
gender | The gender of the participant
email | The participants email address
address_1 | The participants address line 1
address_2 | The participants address line 2
address_city | The participants address town/city
address_zip_code | The participants address post code/zip code
address_state | The participants address county/state
address_country | The participants address country
contact_number | The participants contact number
emergency_name | The name of the person to contact in case of emergency
emergency_number | The contact number of the person to contact in case of emergency

