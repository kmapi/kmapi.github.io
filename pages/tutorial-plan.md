---
layout: page
title: "Plans"
description: "A tool to organize your meal planning"
group: 'tutorial'
---
{% include JB/setup %}


The Meal Planner is a time saving tool to plan out your meals for the week/month.  Its a calendar setup to easily
add recipes to a specific date and meal.  It is designed to conveniently get meals for a span of dates or a
specific date, grouped by the meal it was specified as and with the amount of servings chosen for that dish.
Also built in to Kitchen Monki is the functionality to generate shopping lists over a span of time and yes the
shopping list items will be grouped if duplicated and the store and location data for them will be included.

-----------------

* [adding an item to your meal plan](#create-plan-item)
* [adding a note to your meal plan](#create-plan-note)
* [removing items and notes](#delete-plan-item)
* [get a data from your meal plan](#get-plan)

-----------------

### <a id="create-plan">&nbsp;</a>Adding an item to your meal plan

To add a recipe to the meal planner, you must send the *recipe_id* to cook and which meal you plan to cook it in.
If the date parameter is omitted, Kitchen Monki will set the date for the plan item to 'today', otherwise send
the date in the format 'YYYY-MM-DD'.  It is highly recommended, but not required to supply the servings parameter
which will be used in any shopping list item quantity calculations.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/plan/item' \
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

<a href="/console.html?api_id=23" target="blank">full reference</a>

-----------------

### <a id="create-plan">&nbsp;</a>Adding an note to your meal plan

The add note to plan api call fill the need for users to attach notes or instructions to any specific meal on a
date of the calendar.  The meal and text parameters for this call are required or you will receive an error.  If
the date is omitted Kitchen Monki will assume the date be set to 'today'.

request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/plan/note' \
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

<a href="/console.html?api_id=36" target="blank">full reference</a>

-----------------

### <a id="delete-plan-item">&nbsp;</a>Deleting items and notes

&nbsp;

To remove items and notes from the plan simply supply the *plan_item_id* or *plan_note_id* to the request uri
and make the api calls as specified in the examples below.

#### Deleting an item

request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/plan/[plan_item_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"plan_item_delete",
		"success_message":"Meal plan item deleted",
		"id":[plan_item_id]
	}

<a href="/console.html?api_id=37" target="blank">full reference</a>

&nbsp;

#### Deleting a note

request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/plan/[plan_note_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"plan_note_delete",
		"success_message":"Meal plan note deleted",
		"id":[plan_note_id]
	}

<a href="/console.html?api_id=38" target="blank">full reference</a>

-----------------


### <a id="get-plan">&nbsp;</a>Get a plan

To retrieve data from the meal plan use the get plan api call.  Start and end date parameters are available to
specify the period of data request, however if they are omitted Kitchen Monki will return all of the data from
'today' to 'seven days from now', so all of the data from now (call execution time) to a week from now.  The
response dataset can become large so the recipe_return_fields parameter is available to narrow down the response
data to specific fields.  Finally the last parameter include_list is available to tell Kitchen Monki whether or
not to return the grocery shopping list along with the other data in the response.

request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/plan/[plan_id]' \
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

<a href="/console.html?api_id=22" target="blank">full reference</a>


