---
layout: page
title: "Locations and Stores"
description: "How to use locations and stores"
group: 'tutorial'
---
{% include JB/setup %}




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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#57" target="blank">full reference</a>

-----------------


### <a id="update-location">&nbsp;</a>Updating a location and setting it to active



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#57" target="blank">full reference</a>

-----------------


### <a id="search-stores">&nbsp;</a>Search for stores by text search



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#52" target="blank">full reference</a>

-----------------


### <a id="get-store">&nbsp;</a>Find a store by store_id



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#53" target="blank">full reference</a>

-----------------


### <a id="add-store-to-location">&nbsp;</a>Add a store to a location



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/store' \
		-d store_id=[store_id]
		-d location_id=[location_id]
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"store_added"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#55" target="blank">full reference</a>

-----------------


### <a id="set-store-default">&nbsp;</a>Set store as default for a location



request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/store' \
		-d store_id=[store_id]
		-d location_id=[location_id]
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#55" target="blank">full reference</a>

-----------------


### <a id="delete-location">&nbsp;</a>Deleting a location



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/location/[location_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_location",
		"id":"[location_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#" target="blank">full reference</a>

-----------------


### <a id="get-location">&nbsp;</a>Get a location



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#58" target="blank">full reference</a>

-----------------


### <a id="get-all-locations">&nbsp;</a>Get all locations



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#56" target="blank">full reference</a>

