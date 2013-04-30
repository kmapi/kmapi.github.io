---
layout: page
title: "Plans"
description: "A tool to organize your meal planning"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [adding an item to your meal plan](#create-plan-item)
* [adding a note to your meal plan](#create-plan-note)
* [removing items and notes](#delete-plan-item)
* [get a data from your meal plan](#get-plan)

-----------------

### <a id="create-plan">&nbsp;</a>Adding an item to your meal plan



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/plan/item' \
		-d recipe_id=[recipe_id]
		-d meal=dinner
		-d date=2013-04-15
		-d servings=4
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"plan_item_add",
		"success_message":"Item was added to meal plan",
		"data":{
			"id":"[plan_item_id]",
			"recipe":{
				"id":[recipe_id],
				"title":"Herb-roasted Lamb",
				...
			},
			"date":"2013-04-29",
			"meal":"dinner",
			"servings":"4"
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#23" target="blank">full reference</a>

-----------------

### <a id="create-plan">&nbsp;</a>Adding an note to your meal plan



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/plan/note' \
		-d meal=dinner
		-d text=not+too+spicy
		-d date=2013-04-15
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"plan_note_add",
		"success_message":"Note was added to meal plan",
		"data":{
			"id":"[plan_note_id]",
			"date":"2013-04-15",
			"meal":"dinner",
			"text":"not too spicy"
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#36" target="blank">full reference</a>

-----------------

### <a id="delete-plan-item">&nbsp;</a>Deleting items and notes

&nbsp;



#### Deleting an item

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/plan/[plan_item_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"plan_item_delete",
		"success_message":"Meal plan item deleted",
		"id":[plan_item_id]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#37" target="blank">full reference</a>

&nbsp;

#### Deleting a note



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/plan/[plan_note_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"plan_note_delete",
		"success_message":"Meal plan note deleted",
		"id":[plan_note_id]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#38" target="blank">full reference</a>

-----------------


### <a id="get-plan">&nbsp;</a>Get a plan



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/plan/[plan_id]' \
		-d start=2013-04-08 \
		-d end=2013-04-12 \
		-d recipe_return_fields=title,ingredients \
		-d include_list=1 \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_meal_plan",
		"user_id":[user_id],
		"start":"2013-04-29",
		"end":"2013-05-06",
		"data":{
			"items":[
				{
					"id":"[plan_item_id]",
					"recipe":{
						"id":[recipe_id],
						"title":"Herb-roasted Lamb",
						...
					}
					"date":"2013-04-29",
					"meal":"dinner",
					"servings":"4"
				}
			],
			"notes":[
				{
					"id":"[plan_note_id]",
					"date":"2013-04-29",
					"meal":"dinner",
					"text":"not too spicy"
				}
			],
			"dates":{
				"date_2013-04-29":{
					"breakfast":{
						"items":[],
						"notes":[]
					},
					"lunch":{
						"items":[],
						"notes":[]
					},
					"dinner":{
						"items":[
							{
								"id":"[plan_item_id]",
								"recipe":{
									"id":[recipe_id],
									"title":"Herb-roasted Lamb",
									...
								},
								"date":"2013-04-29",
								"meal":"dinner",
								"servings":"4"
							}
						],
						"notes":[
							{
								"id":"[plan_note_id]",
								"date":"2013-04-29",
								"meal":"dinner",
								"text":"not too spicy"
							}
						]
					},
					...
				}
			}
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#22" target="blank">full reference</a>


