---
layout: page
title: "Meta Tags"
description: "Finding meta tags and totals"
group: 'tutorial'
---
{% include JB/setup %}


Kitchen Monki has a section in the api for recipe meta tags.  They are an important part of grouping recipes and
searching them.

-----------------

* [get all meta tags](#get-all-metas)
* [get meta totals](#get-meta-totals)

-----------------


### <a id="get-all-metas">&nbsp;</a>Get a list of all meta tags

This api call will return a complete list of tags available to attach to user created recipes.  All of the
pertinent tag information will also be returned in the data parameter as an array of meta objects.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/meta/tags' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"meta_tags",
		"data":[
			{
				"id":[meta_id],
				"name":"1-15 Min",
				"parent_id":[parent_meta_id],
				"top_parent_id":[top_parent_meta_id],
				"required":true,
				"single":true,
				"sort":null
			},
			...
		]
	}

<a href="/console.html?api_id=42" target="blank">full reference</a>

-----------------


### <a id="get-meta-totals">&nbsp;</a>Getting meta totals

The get meta totals call returns a user's information relating to the Kitchen Monki Recipe Tools and other stats
like the number of recipes they have created.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/meta/totals' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"meta_totals",
		"user_id":[user_id],
		"data":{
			"queue":5,
			"bookmark":10,
			"recipes":5,
			"list":1,
			"plan":0
		}
	}

<a href="/console.html?api_id=41" target="blank">full reference</a>

