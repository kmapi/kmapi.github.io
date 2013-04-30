---
layout: page
title: "Queues"
description: "Working with queues"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [adding a recipe to your queue](#queue-recipe)
* [removing a recipe from your queue](#dequeue-recipe)
* [get all queued items](#get-queue)

-----------------

### <a id="queue-recipe">&nbsp;</a>Adding a recipe to your queue



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#31" target="blank">full reference</a>

-----------------


### <a id="dequeue-recipe">&nbsp;</a>Removing a recipe from your queue



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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#34" target="blank">full reference</a>

-----------------


### <a id="get-queue">&nbsp;</a>Get all queued items



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/queue' \
		-d limit=100 \
		-d offset=1000 \
		-d return_fields=title \
		-d array_key=id \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#5" target="blank">full reference</a>


