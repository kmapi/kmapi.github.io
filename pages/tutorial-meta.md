---
layout: page
title: "Meta Tags"
description: "Finding meta tags and totals"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [get all meta tags](#get-all-metas)
* [get meta totals](#get-meta-totals)

-----------------


### <a id="get-all-metas">&nbsp;</a>Get a list of all meta tags



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/meta/tags' \
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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#42" target="blank">full reference</a>

-----------------


### <a id="get-meta-totals">&nbsp;</a>Getting meta totals



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/meta/totals' \
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

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#41" target="blank">full reference</a>

