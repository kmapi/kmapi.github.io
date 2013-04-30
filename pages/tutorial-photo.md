---
layout: page
title: "Photos"
description: "Working with recipe photos"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [adding a recipe photo](#create-photo)
* [updating a photo](#update-photo)
* [removing a photo](#delete-photo)
* [getting a photo](#get-photo)

-----------------

### <a id="create-photo">&nbsp;</a>Adding a recipe photo



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/photo' \
		-d data=[base64 encoded image data] \
		-d recipe_id=[recipe_id] \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:



<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#47" target="blank">full reference</a>

-----------------


### <a id="update-photo">&nbsp;</a>Updating a photo



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/photo/[photo_id]' \
		-d is_main=1 \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:



<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#48" target="blank">full reference</a>

-----------------


### <a id="delete-photo">&nbsp;</a>Removing a photo



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/photo/[photo_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_photo",
		"id":"[photo_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#49" target="blank">full reference</a>

-----------------


### <a id="get-photo">&nbsp;</a>Getting a photo



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/photo/[photo_id]' \
		-d width=100 \
		-d height=100 \
		-d adaptive=1 \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#45" target="blank">full reference</a>


