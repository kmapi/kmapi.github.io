---
layout: page
title: "Bookmarks"
description: "Working with bookmarks"
group: 'tutorial'
---
{% include JB/setup %}


Bookmarks are a convenient way to save a desired recipe for further reference.  Not much to it, they work
exactly like a bookmark should.  You can add them, view them all, and delete them when no longer needed.

-----------------

* [bookmark a recipe](#add-bookmark)
* [remove a bookmark](#delete-bookmark)
* [get all bookmarks](#get-bookmarks)

-----------------

### <a id="add-bookmark">&nbsp;</a>Bookmark a recipe

To add a recipe to your bookmarks, provide the correct *recipe_id* to the add bookmark call and send the
request with the POST method.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/bookmark/[recipe_id]' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"bookmark_add",
		"success_message":"Bookmark has been added",
		"recipe_id":[recipe_id],
		"recipe":{
			"id":[recipe_id],
			"title":"Herb-roasted Lamb",
			"url_perma":"http:\/\/km.local\/view\/55"
		}
	}

<a href="/console.html?api_id=32" target="blank">full reference</a>

-----------------


### <a id="delete-bookmark">&nbsp;</a>Remove a bookmark

Getting rid of a bookmark is done by sending the recipe to be removed's *recipe_id* to the delete bookmark
call via the DELETE method.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/bookmark/[recipe_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"bookmark_delete",
		"success_message":"Bookmark has been deleted",
		"recipe_id":[recipe_id],
		"recipe":{
			"id":[recipe_id],
			"title":"Herb-roasted Lamb",
			"url_perma":"http:\/\/km.local\/view\/55"
		}
	}

<a href="/console.html?api_id=33" target="blank">full reference</a>

-----------------


### <a id="get-bookmarks">&nbsp;</a>Get all bookmarks

This call will return a list of all of the user's bookmarks as recipe objects via the recipe search api
call using the value 1 for the search parameter "mine".  You can also provide limit and offset values
to facilitate pagination, a list of return fields to limit the amount of data returned, and an array_key
to specify the key values in the response data array for the convenience of your application.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/bookmark' \
		-d limit=100 \
		-d offset=1000 \
		-d return_fields=title \
		-d array_key=id \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=11" target="blank">full reference</a>


