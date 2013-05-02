---
layout: page
title: "Queues"
description: "Working with queues"
group: 'tutorial'
---
{% include JB/setup %}


The Recipe Queue is basically a temporary holding area to store recipes while browsing and searching.  After
adding a bunch of recipes to it, it is designed for a user to be able to then view the queue and decide whether
or not to add them to different recipe tools.

-----------------

* [adding a recipe to your queue](#queue-recipe)
* [removing a recipe from your queue](#dequeue-recipe)
* [get all queued items](#get-queue)

-----------------

### <a id="queue-recipe">&nbsp;</a>Adding a recipe to your queue

To add a recipe to the queue, use the queue recipe call, supplying the *recipe_id* to the end of the request uri.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/queue/[recipe_id]' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"queue_add",
		"success_message":"Queue item has been added",
		"recipe_id":[recipe_id],
		"recipe":{
			"id":[recipe_id],
			"title":"Herb-roasted Lamb",
			"url_perma":"http:\/\/km.local\/view\/55"
		}
	}

<a href="/console.html?api_id=31" target="blank">full reference</a>

-----------------


### <a id="dequeue-recipe">&nbsp;</a>Removing a recipe from your queue

To remove a recipe from the queue, use the dequeue recipe call as shown in the example below.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/queue/[recipe_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"queue_delete",
		"success_message":"Queue item has been deleted",
		"recipe_id":[recipe_id],
		"recipe":{
			"id":[recipe_id],
			"title":"Herb-roasted Lamb",
			"url_perma":"http:\/\/km.local\/view\/55"
		}
	}

<a href="/console.html?api_id=34" target="blank">full reference</a>

-----------------


### <a id="get-queue">&nbsp;</a>Get all queued items

To return the contents of the queue, use the get queue api call.  There are no required parameters, but you can
specify a limit and offset for pagination or similar function, the return_fields to limit the data fields returned
in the response data, and an array_key to specify the values to be used as the keys in the response array.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/queue' \
		-d limit=100 \
		-d offset=1000 \
		-d return_fields=title \
		-d array_key=id \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=5" target="blank">full reference</a>


