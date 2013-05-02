---
layout: page
title: "Locations and Stores"
description: "How to use locations and stores"
group: 'tutorial'
---
{% include JB/setup %}


Locations and stores are available for users to enhance their shopping experience by allowing them to specify
which stores they would like to purchase grocery list items from.  Users can add new locations to their profile
and Kitchen Monki will use the Google Places API to match stores that lie within the area.  Only stores that the
user chooses will be added to their location and a single store can be set to use as default for convenience.
Once that is setup, the user can dictate where specific grocery list items should be purchased from.

-----------------

* [creating a location](#create-location)
* [update a location](#update-location)
* [search stores with text](#search-stores)
* [find store by store_id](#get-store)
* [add a store to a location](#add-store-to-location)
* [set as default store for a location](#set-store-default)
* [removing locations](#delete-location)
* [get a location](#get-location)
* [get all locations](#get-all-locations)

-----------------

### <a id="create-location">&nbsp;</a>Creating a location

The first step in linking shopping items to a store is creating the location.  No parameters are required, this
call simply creates a new location for a user.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/location' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_location",
		"id":[location_id],
		"data":{
			"id":[location_id],
			"user_id":[user_id],
			"name":null,
			"location_id":0,
			"location":null,
			"created":1367017548,
			"modified":1367017548,
			"items":[],
			"stores":[]
		}
	}

<a href="/console.html?api_id=57" target="blank">full reference</a>

-----------------


### <a id="update-location">&nbsp;</a>Updating a location and setting it to active

This call allows the user to modify the location's name (title), locality (string for the Google Places API to
search), and an active flag to enable the location.  The *location_id* of the location being modified must be
provided at the end of the request uri.

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/location/[location_id]' \
		-d name=Pioneer+Square \
		-d locality=98101 \
		-d active=1 \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"update_location",
		"success_message":"Updated location data",
		"location_id":"[location_id]"
	}

<a href="/console.html?api_id=57" target="blank">full reference</a>

-----------------


### <a id="search-stores">&nbsp;</a>Search for stores by text search

The search stores api call executes the procedure to actually query Google's Places API and it returns the data
as store objects in the data parameter.  The text parameter is required and can be any descriptor that is related
to mapping a point or area such as a zip code, neighborhood, city, address, etc.  The radius parameter is available
to constrict or widen the area to search for stores in.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/store' \
		-d text=98101
		-d radius=5000
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"search_stores",
		"data":{
			"[store_id]":{
				"id":[store_id],
				"user_id":null,
				"name":"Pike Place Fish Market Inc",
				"address":"86 Pike Street",
				"city":"Seattle",
				"region":"",
				"lat":"47.608816",
				"lon":"-122.340458"
			},
			...
		}
	}

<a href="/console.html?api_id=52" target="blank">full reference</a>

-----------------


### <a id="get-store">&nbsp;</a>Find a store by store_id

If a *store_id* is known, then the get store by id api call can be used to request the store's complete information.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/store/[store_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_store",
		"id":[store_id],
		"data":{
			"id":[store_id],
			"user_id":null,
			"name":"Uwajimaya",
			"address":"600 5th Avenue South #100",
			"city":"Seattle",
			"region":"",
			"lat":"47.596708",
			"lon":"-122.327013"
		}
	}

<a href="/console.html?api_id=53" target="blank">full reference</a>

-----------------


### <a id="add-store-to-location">&nbsp;</a>Add a store to a location

When you're ready to add stores to a user's location, make the add store to location api call to create the
relationship.  Both parameters *store_id* and *location_id* are required.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/store' \
		-d store_id=[store_id]
		-d location_id=[location_id]
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"store_added"
	}

<a href="/console.html?api_id=55" target="blank">full reference</a>

-----------------


### <a id="set-store-default">&nbsp;</a>Set store as default for a location

When adding shopping list items to a grocery shopping list, its convenient to not have to choose which store to
purchase from.  Use this call to set a location's default store.  If users add shopping list items without
specifying a store where to buy it, then the default store will be chosen.

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/store' \
		-d store_id=[store_id]
		-d location_id=[location_id]
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=55" target="blank">full reference</a>

-----------------


### <a id="delete-location">&nbsp;</a>Deleting a location

To remove a user's created location, use the delete location api call.  Supply the *location_id* to be deleted
to the end of the request uri and make the request with the DELETE method.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/location/[location_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_location",
		"id":"[location_id]"
	}

<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="get-location">&nbsp;</a>Get a location

To get a location's information including all of its associated stores, use the get location api call.  The
*location_id* must be provided to the request uri as usual.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/location/[location_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_location",
		"id":[location_id],
		"data":{
			"id":[location_id],
			"user_id":[user_id],
			"name":"Downtown",
			"locality":"98101",
			"activate":"2013-03-20 01:43:34",
			"stores":{
				"[store_id]":{
					"id":[store_id],
					"user_id":null,
					"name":"Costco Seattle",
					"address":"4401 4th Avenue South",
					"city":"Seattle",
					"region":"",
					"lat":"47.564836",
					"lon":"-122.329695"
				}
			}
		}
	}

<a href="/console.html?api_id=58" target="blank">full reference</a>

-----------------


### <a id="get-all-locations">&nbsp;</a>Get all locations

To get all of a user's locations use the get all locations call.  No parameters required, and all of the store
and location information will be included in the response data parameter.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/location/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_all_locations",
		"ids":[
			"[location_id]",
			...
		],
		"data":{
			"[location_id]":{
				"id":[location_id],
				"user_id":[user_id],
				"name":"Downtown",
				"locality":"98101",
				"activate":"2013-03-20 01:43:34",
				"stores":{
					"[store_id]":{
						"id":[store_id],
						"user_id":null,
						"name":"Costco Seattle",
						"address":"4401 4th Avenue South",
						"city":"Seattle",
						"region":"",
						"lat":"47.564836",
						"lon":"-122.329695"
					}
				},
				...
			},
			...
		}
	}

<a href="/console.html?api_id=56" target="blank">full reference</a>

