---
layout: page
title: "Photos"
description: "Working with recipe photos"
group: 'tutorial'
---
{% include JB/setup %}


The photo section of the api exists to facilitate adding recipe photos user created recipes.  Kitchen Monki uses
Amazon S3 to store the uploaded images.  Of course multiple images can be uploaded per recipe and there are
options provided on how the image should be cropped and scaled.

-----------------

* [adding a recipe photo](#create-photo)
* [updating a photo](#update-photo)
* [removing a photo](#delete-photo)
* [getting a photo](#get-photo)

-----------------

### <a id="create-photo">&nbsp;</a>Adding a recipe photo

To add a photo to a recipe, you must provide the *recipe_id* of the recipe being added to and the encoded image
data should be passed in the data parameter.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/photo' \
		-d data=[base64 encoded image data] \
		-d recipe_id=[recipe_id] \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:



<a href="/console.html?api_id=47" target="blank">full reference</a>

-----------------


### <a id="update-photo">&nbsp;</a>Updating a photo

After uploading images via the add photo api call, you can set one of them as the main image designed to be used
anytime that the layout expects one image.  When getting image objects back nested in a recipe object, the property
is_main will be set to 1 for the main recipe photo object.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/photo/[photo_id]' \
		-d is_main=1 \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:



<a href="/console.html?api_id=48" target="blank">full reference</a>

-----------------


### <a id="delete-photo">&nbsp;</a>Removing a photo

If no longer needed, photos can be deleted from Kitchen Monki.  Provide the *photo_id* in the request uri to
the delete photo api call.

request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/photo/[photo_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_photo",
		"id":"[photo_id]"
	}

<a href="/console.html?api_id=49" target="blank">full reference</a>

-----------------


### <a id="get-photo">&nbsp;</a>Getting a photo

If the *photo_id* is known, you can request a scaled version of the image from the get photo api call.  Of course
the *photo_id* is required, and also available are options to specify the desired width and height.  The adaptive
parameter set to 1 will get the image with the desired width and height (in pixels) from the center of the image.
If adaptive is set to 0, the response will contain an image that is the complete image, but scaled to the width
and height values in pixels.  If the width and height parameters are omitted from the call, Kitchen Monki will
use width=100px and height=100px as the default values.  By default also adaptive will be set to 1 if omitted.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/photo/[photo_id]' \
		-d width=100 \
		-d height=100 \
		-d adaptive=1 \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=45" target="blank">full reference</a>


