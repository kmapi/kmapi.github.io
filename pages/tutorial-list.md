---
layout: page
title: "Grocery Lists"
description: "How to create a list"
group: 'tutorial'
---
{% include JB/setup %}


Grocery Shopping Lists are a powerful tool with which you can create lists of ingredients you will need
to shop for, the brands and amounts of the ingredients, the stores where you want to shop, and even the
aisles where to find each ingredient!  Lists can be created from a time period on your Meal Planner like,
creating a shopping list of ingredients that are needed to cook all of the meals on the Planner for this
week.  Duplicate ingredients will be combined even if they have different unit types.

-----------------

* [creating a grocery list](#create-list)
* [adding a shopping item](#create-item)
* [batch adding items](#batch-create-item)
* [removing lists](#delete-list)
* [removing an item](#delete-item)
* [get a list](#get-list)
* [get all lists](#get-all-lists)
* [sample list response](#sample-list)

-----------------

### <a id="create-list">&nbsp;</a>Creating a list

The first step is to create a shopping list, no parameters required.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/list' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_list",
		"id":[list_id],
		"data":{
			"id":[list_id],
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

<a href="/console.html?api_id=16" target="blank">full reference</a>

-----------------


### <a id="create-item">&nbsp;</a>Adding an item to the list

Adding ingredients to the list is done with the add list item call.  There are two required fields, the
*ingredient_id* and the *list_id* of the list to add to which you created above.  The other parameters
below help you to specify the brand, quantity and unit type, the store you want to purchase the item,
any notes helpful while shopping for the item, and whether the ingredient is a custom ingredient or not.
For the unit_text parameter, you provide a string.  Kitchen Monki supports most common units of measure
and their abbreviations so "lbs" and "pounds" would map to the same unit of measure.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/list/[list_id]/item' \
		-d ingredient_id=45 \
		-d ingredient_custom=0 \
		-d quantity=5 \
		-d unit_text=lbs \
		-d recipe_id=50763 \
		-d store_id=12 \
		-d brand_item_id=5 \
		-d brand=Darigold \
		-d note=big+size \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"list_item_add",
		"success_message":"Item(s) were added to grocery list",
		"id":[list_item_id]
	}

<a href="/console.html?api_id=19" target="blank">full reference</a>

-----------------


### <a id="batch-create-item">&nbsp;</a>Batch adding an item to the list

As with some other Kitchen Monki API calls where batch processing would be handy, batch adding items to
a list can also be accomplished by providing an array of json objects.  As with the above api call -
adding a singular item, *list_id* and *ingredient_id* are both required.  This example calls the same
api call as above, however the difference is that the parameter "data" is provided, so Kitchen Monki
attempts the batch creation functionality.

data parameter in json format:

	[
		{
			"list_id":"[list_id]"
			"ingredient_id":"[ingredient_id]",
			"ingredient_custom":"0",
			"quantity":"5",
			"unit_text":"lbs",
			"recipe_id":"[recipe_id]",
			"store_id":"[store_id]",
			"brand_item_id":"[brand_item_id]",
			"brand":"Darigold",
			"note":"big size"
		},
		...
	]

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/list/[list_id]/item' \
		-d data=[form encoded json data parameter] \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"list_item_add",
		"success_message":"Item(s) were added to grocery list",
		"id":[list_item_id]
	}

<a href="/console.html?api_id=19" target="blank">full reference</a>

-----------------


### <a id="delete-list">&nbsp;</a>Deleting a list

Deleting a list is similar to other delete api calls on Kitchen Monki and deleting a list will delete
its associated list items from the system as well.

request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/list/[list_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_list",
		"id":"[list_id]"
	}

<a href="/console.html?api_id=18" target="blank">full reference</a>

-----------------

### <a id="delete-item">&nbsp;</a>Deleting list items

To delete a specific list item supply the *list_item_id* to the delete list item call.

request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/list/[list_item_id]/item' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_list_item",
		"id":"[list_id]"
	}

<a href="/console.html?api_id=21" target="blank">full reference</a>

-----------------


### <a id="get-list">&nbsp;</a>Get a list

Retrieving a list is easy, pass the *list_id* to the get list call and you will get back the list object
in the data property of the response which contains all of the list items in the items property of the
list object.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/list/[list_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_grocery_list",
		"user_id":[user_id],
		"data":{
			"id":[list_id],
			"name":null,
			"location_id":0,
			"location":null,
			"created":1363740879,
			"modified":1363740879,
			"items":[
				{
				...
				}
			]
		}
	}

<a href="/console.html?api_id=15" target="blank">full reference</a>

-----------------


### <a id="get-all-lists">&nbsp;</a>Get all lists

To get a list of all of a user's list ids, make the get all lists api call.  No parameters are required.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/list/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"user_id":[user_id],
		"data":[
			{
				"id":[list_id],
				"user_id":[user_id],
				"name":null,
				"created":1366830792,
				"modified":1366830792
			},
			...
		]
	}

<a href="/console.html?api_id=35" target="blank">full reference</a>

-----------------


### <a id="sample-list">&nbsp;</a>Sample list response in json format

Here is a more detailed example of a list response object.

	{
		"success":"get_grocery_list",
		"user_id":[user_id],
		"data":{
			"id":[list_id],
			"name":null,
			"location_id":[location_id],
			"location":null,
			"created":1363740879,
			"modified":1363740879,
			"items":[
				{
					"id":[list_item_id],
					"ingredient":{
						"id":[ingredient_id],
						"name":"Frozen Chicken Wing",
						"name_plural":"Chicken Wings",
						"name_nomenclature":"Chicken, Frozen Wing",
						"measure_type_id":[unit_id],
						"custom":false,
						"category_id":[category_id]
					},
					"ingredient_formatted":"12 oz brand4 Frozen Chicken Wing,",
					"recipe_id":[],
					"store_id":[store_id],
					"brand_item_id":[brand_item_id],
					"brand_item":{
						"id":[brand_item_id],
						"brand_family_id":[brand_family_id],
						"user_id":1,
						"brand_text":"",
						"brand_family":{
							"id":[brand_family_id],
							"name":"brand4"
						}
					},
					"brand":"",
					"note":null,
					"quantity":12,
					"unit_text":"oz",
					"aisle":{
						"id":"[aisle_id]",
						"name":"Frozen Foods"
					}
				},
				...
			],
			"stores":[
				[...]
			]
		}
	}
