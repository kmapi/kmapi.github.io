---
layout: page
title: "Brands"
description: "Working with brands"
group: 'tutorial'
---
{% include JB/setup %}


Brands in Kitchen Monki are available for recipe owners to specify the exact brands of ingredients needed
to cook their recipe.  They are completely optional to use with recipe ingredients.  Brand families are
the brand (manufacturer) name like "C&H", while brand items are a specific product (brand and ingredient)
such as "C&H Brown Sugar".  Brand families and items can not be created by end users, however they can
be created by administrators of Kitchen Monki API clients with the use of a client token.

-----------------

##### requires special permission and "client" token
* [creating a brand family](#create-brand-family)
* [creating a brand item](#create-brand-item)
* [removing brands](#deleting-brands)

##### available to end users
* [getting brands](#getting-brands)

-----------------

### <a id="create-brand-family">&nbsp;</a>Creating a brand family

When creating a new brand family, only one parameter is required: name.  The name is the company,
manufacturer, or brand name desired to be added to the Kitchen Monki database.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/brand/family' \
		-d name=Kraft
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_brand_family",
		"id":"[brand_family_id]",
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#62" target="blank">full reference</a>

-----------------


### <a id="create-brand-item">&nbsp;</a>Creating a brand item

When creating a new brand item you must specify the *brand_family_id* of the new brand item and another
parameter - brand_text which is the full label of the brand item.  For instance, "Kraft Mayonnaise".

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/brand/[brand_family_id]/item' \
		-d brand_text=Kraft+Mayonnaise
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_brand_item",
		"id":"[brand_item_id]",
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#63" target="blank">full reference</a>

-----------------


### <a id="deleting-brands">&nbsp;</a>Removing brands

#### Deleting a brand family

Provide the *brand_family_id* to delete using the DELETE method to remove a brand family.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/brand/family/[brand_family_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_brand_family",
		"id":"[brand_family_id]",
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#68" target="blank">full reference</a>

&nbsp;

#### Deleting a brand item

Provide the *brand_item_id* to delete using the DELETE method to remove a brand item.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/brand/item/[brand_item_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_brand_item",
		"id":"[brand_item_id]",
		}
	}


<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#69" target="blank">full reference</a>

-----------------


### <a id="getting-brands">&nbsp;</a>Getting brand data

&nbsp;

#### Get a brand family by *brand_family_id*

Use this call to get a specific brand family with a known *brand_family_id*

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/brand/family' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_brand_family",
		"id":"[brand_family_id]",
		"data":{
			"id":[brand_family_id],
			"name":"Banquet"
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#60" target="blank">full reference</a>

&nbsp;

#### Get a brand item by *brand_item_id*

Use this call to get a specific brand item with a known *brand_item_id*

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/brand/item' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_brand_item",
		"id":"[brand_item_id]",
		"data":{
			"id":[brand_item_id],
			"brand_family_id":[brand_family_id],
			"user_id":0,
			"brand_text":"Banquet Chicken Thighs",
			"brand_family":{
				"id":[brand_family_id],
				"name":"Banquet"
			}
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#67" target="blank">full reference</a>

&nbsp;

#### Get all brand families

This call will return a list of all available brand families available on Kitchen Monki.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/brand/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_all_brands",
		"data":[
			{
				"id":2,
				"name":"Kellogg's"
			},
			...
		]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#61" target="blank">full reference</a>


