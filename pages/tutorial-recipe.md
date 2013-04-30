---
layout: page
title: "Recipes"
description: "How to create a recipe"
group: 'tutorial'
---
{% include JB/setup %}


Recipes are the central building block to using the Kitchen Monki API...

-----------------

* [creating a recipe](#create-recipe)
* [updating a recipe](#update-recipe)
* [adding steps and ingredients](#create-step)
* [updating steps and ingredients](#updating-steps)
* [publishing a recipe](#publish-recipe)
* [removing recipes](#delete-recipe)
* [removing a steps and ingredients](#delete-step)
* [sample recipe response](#sample-recipe)

-----------------

### <a id="create-recipe">&nbsp;</a>Creating a recipe

The first step to adding a new recipe to Kitchen Monki is using the create recipe call.  No parameters
are required for this step.  In the response, you will receive a new *recipe_id* which will be your key
to adding all sorts of things to it like a title, steps, and ingredients.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/recipe' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_recipe",
		"id":[recipe_id],
		"data":{
			"id":[recipe_id],
			"title":"",
			...
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#2" target="blank">full reference</a>

-----------------


### <a id="update-recipe">&nbsp;</a>Updating a recipe

Once you have created a recipe, now call the update recipe api call to modify it.  This is done with a
json object as shown below, then it must be form encoded and sent as the parameter "data" in the a PUT
request.  The *recipe_id* received from the create recipe call must be included at the end of the uri as
shown below.

data parameter in json format:

	{
		'title': 'Tuna Casserole',
		'source': 'Food Network',
		'servings': '5',
		'description': 'This is a tuna casserole that even my picky family loves!'
	}

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]' \
		-d data=[form encoded json data parameter] \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"update_recipe",
		"success_message":"Updated recipe data",
		"recipe_id":"[recipe_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#3" target="blank">full reference</a>

-----------------


### <a id="create-step">&nbsp;</a>Adding a step to the recipe

As in the real world, when executing a recipe there are several steps to follow.  Use the add recipe step
call to add new steps to an existing recipe.  The only required parameter for this call is the *recipe_id*
to add the step to.  When adding a step, you can give it a title, a description, and a sequence (the step
number or order in which it should be displayed/performed).  Besides those fields, in the next section we
will show you how to add ingredients to your step.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]/step' \
		-d title=Marinade+the+beef
		-d description=Mix+the+ingredients+and+soak+the+beef+for+1+hour
		-d sequence=3
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"add_step",
		"success_message":"Added a step to recipe [recipe_id]",
		"recipe_id":"[recipe_id]",
		"step":{
			"id":[recipe_step_id],
			"recipe_id":[recipe_id],
			"title":"",
			"description":"xxx",
			"sequence":2,
			"ingredients":[]
		}
	}
<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#2" target="blank">full reference</a>

-----------------


### <a id="create-ingredient">&nbsp;</a>Adding an ingredient to the recipe step

Now that you have created a step describing what to do for that part of the recipe, you will need to add
the ingredients that will be needed during the step.  The Kitchen Monki API has thousands of ingredients
available to choose from, but should you need to add a custom ingredient you can.  Required parameters are
the *recipe_id* and the *ingredient_id* unless you set *ingredient_custom* to 1, then you do not need
to provide the *ingredient_id* instead a new custom ingredient will be added to the Kitchen Monki database.
Also, when cooking with an ingredient you need to know how much to use and whether a specific brand is
desired.  Kitchen Monki has a wide listing of unit measures and brands to specify the requirement for the
cooking step.  Simply provide the proper *unit_id*, *brand_item_id*, and *amount* to the add recipe
ingredient call and Kitchen Monki will take care of the rest.  When using the Recipe Tools such as the
Grocery Shopping list, the system knows how to combine your items for you even if the units don't match.
Note below that *recipe_ingredient_id* is different from *ingredient_id*.  The *recipe_ingredient_id*
is the id of the the ingredient data used in this specific recipe which includes unit, brand, and other
information.  the *ingredient_id* is the id of the generic ingredient data used by all Kitchen Monki users.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]/ingredient' \
		-d title=
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"add_ingredient",
		"success_message":"Added an ingredient to recipe [recipe_id]",
		"recipe_id":"[recipe_id]",
		"step_id":[step_id],
		"ingredient":{
			"id":[recipe_ingredient_id],
			"recipe_id":[recipe_id],
			...
			"ingredient":{
				"id":[ingredient_id],
				...
			},
			"ingredient_id":[ingredient_id],
			"ingredient_custom":0,
			"unit":{
				"id":[unit_id],
				...
			},
			"unit_id":0,
			"brand_item_id":0,
			"brand_item":null
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#2" target="blank">full reference</a>

-----------------


### <a id="updating-steps">&nbsp;</a>Updating and Batch adding recipe steps and ingredients

Notice below that the api call used in this section is the same update recipe call as described above.
This call is very versatile due to the fact that it takes a json object as one of its parameters.  Besides
just updating basic recipe information like title and description, you can update its nested objects
like steps and ingredients.  In fact it is the only way to update them.  Additionally, this api call can
be used to batch add steps or ingredients.

Examine the json below, in the step property is an array of one object which is a recipe step object.
In the object, "id" is specified.  Since the "id" is there, the api will attempt to update the recipe step
with the given *recipe_step_id* given.  If the "id" was not included in the object the api would have
instead created a new step with the given fields for the given *recipe_id*.  This same process applies to
ingredients property array.  If you wanted to, you could update a recipe, update some steps, batch add
some ingredients, etc. all in one call.

data parameter in json format:

	{
		"step":[
			{
				"id":"[recipe_step_id]",
				"title":"bake the chicken",
				"description":"bake at 350 degrees for 30 minutes.",
				"sequence":"4",
			}
		]

		"ingredients":[
			{
				"id":[recipe_ingredient_id],
				"sequence":"1",
				"recipe_step_id":"[recipe_step_id]",
				"ingredient":{
					"id":"[ingredient_id]"
				},
				"quantity":"3",
				"prep":"flour the chicken",
				"unit_id":"[unit_id]",
				"brand_item_id":"[brand_item_id]"
			}
		]
	}

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]' \
		-d data=[form encoded json data parameter] \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"update_recipe",
		"success_message":"Updated recipe data",
		"recipe_id":"[recipe_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#3" target="blank">full reference</a>
-----------------

### <a id="publish-recipe">&nbsp;</a>Publishing a recipe

Once you are ready to let the world view your new recipe then publish it with the publish recipe api call.
Just include the *recipe_id* in the call as shown below and it will be set to live.  One thing to note, if
you have created recipe ingredients which do not have a specified *recipe_step_id* set, then you will
receive an error.  You must use the update recipe call to set the *recipe_step_id* for each recipe
ingredient missing one, then try to republish.

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]/publish' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"publish_recipe",
		"success_message":"Recipe was published",
		"recipe_id":"[recipe_id]",
		"created_time":"2013-04-26 01:19:52",
		"modified_time":"2013-04-26 22:26:06"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#64" target="blank">full reference</a>

-----------------


### <a id="delete-recipe">&nbsp;</a>Deleting a recipe

To discard the recipe, simply call the delete recipe api call as shown below with the DELETE method.
The *recipe_id* received from the create recipe call must be included at the end of the uri.  Removing
a recipe will also remove all of the steps and recipe ingredients associated with the recipe to be deleted.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_recipe",
		"id":"[recipe_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#4" target="blank">full reference</a>

-----------------

### <a id="delete-step">&nbsp;</a>Deleting recipe steps and ingredients

Removing recipe steps and ingredients works nearly the same as removing a recipe as shown below.  When
removing a step or ingredient, you must provide the recipe_step_id or recipe_ingredient_id, and the
corresponding recipe_id.  As recipe ingredients are attached to a step, when deleting a step, its recipe
ingredients will automatically be deleted as well.

&nbsp;

#### Deleting a recipe step

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]/step' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_recipe_step",
		"id":"[recipe_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#40" target="blank">full reference</a>

&nbsp;

#### Deleting a recipe ingredient

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/recipe/[recipe_id]/ingredient' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_ingredient",
		"success_message":"Deleted ingredient [recipe_ingredient_id]",
		"ingredient_id":"[recipe_ingredient_id]",
		"recipe_id":"[recipe_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#66" target="blank">full reference</a>

-----------------












### <a id="sample-recipe">&nbsp;</a>Sample recipe response in json format

Recipe objects come back in the data property of the json response.  Below is an example of recipe
object returned which includes a great amount of useful information.

	{
		"success":"get_recipe",
		"id":55,
		"data":{
			"id":55,
			"title":"Herb-roasted Lamb",
			"title_url":"Herb_Roasted_Lamb",
			"title_url_num":1,
			"url":"http:\/\/km.local\/recipe\/Herb_Roasted_Lamb",
			"url_perma":"http:\/\/km.local\/view\/55",
			"is_published":true,
			"is_public":true,
			"shared_with":[],
			"created":1206538315,
			"modified":1360333352,
			"indexed":1350437606,
			"rating":4,
			"rating_viewer":0,
			"source":"Barefoot Contessa, Family Style",
			"source_link":"",
			"servings":12,
			"scaling_ratio":1,
			"description":"This dish is great for guests...
			"description_snippet":"This dish is great for guests...
			"description_source":"This dish is great for guests...
			"comments_count":1,
			"views":1211,
			"has_photo":false,
			"photo_ids":[],
			"main_photo_id":null,
			"main_photo_url":null,
			"site":null,
			"ingredients":[
				{
					"id":31,
					"recipe_step_id":78,
					"quantity":5,
					"sequence":1,
					"prep":"unpeeled",
					"formatted":"5 pounds Banquet Red Potato, unpeeled",
					"formatted_html":"<span class=\"quantity\">5<\/span>...
					"ingredient":{
						"id":428,
						"name":"Red Potato",
						"name_plural":"Red Potatoes",
						"name_nomenclature":"Potato, Red",
						"custom":false,
						"category_id":179
					},
					"unit":{
						"id":3,
						"name":"pound",
						"name_plural":"pounds",
						"scale":0.453592,
						"measure_type_id":1
					},
					"brand_item":{
						"id":1,
						"brand_family_id":1,
						"user_id":0,
						"brand_text":"",
						"brand_family":{
						"id":1,
						"name":"Banquet"
						}
					}
				},
				...
			],
			"brand_item_ids":[ 1, 2 ],
			"brand_family_ids":[ 1, 2 ],
			"meal_id":0,
			"meal":"",
			"time_id":0,
			"time":"",
			"course_id":0,
			"course":"",
			"cuisine_id":0,
			"cuisine":"",
			"steps":[
				{
					"id":75,
					"description":"Pre-heat oven to 450 degrees, place oven rack in lower...
					"sequence":0,
					"ingredients":[
						{
						"id":501,
						"quantity":16,
						"sequence":3,
						"prep":"",
						"formatted":"16 pounds Whole Leg of Lamb",
						"formatted_html":"<span class=\"quantity\">16<\/span>...
						"ingredient":{
							"id":8,
							"name":"Whole Leg of Lamb",
							"name_plural":"Whole Legs of Lamb",
							"name_nomenclature":"Lamb, Whole Leg",
							"custom":false,
							"category_id":102
						},
						"unit":{
							"id":3,
							"name":"pound",
							"name_plural":"pounds",
							"scale":0.453592,
							"measure_type_id":1
						},
						"brand_item":null
						}
					]
				},
				...
			],
			"tags":[
				{
					"id":52,
					"name":"30-60 Min",
					"parent_id":6,
					"top_parent_id":6,
					"required":true,
					"single":true,
					"sort":null
				},
				...
			],
			"user":{
				"id":3,
				"email":"xxxxxxx@xxxxxxx.com",
				"name_display":"Jane Smith",
				"name_first":"Jane",
				"name_last":"Smith",
				"user_space_id":"1",
				"newemail":"xxxxxxx@xxxxxxx.com",
				"password":"111111222222223333333",
				"code":"xxxxxxxx",
				"timezone":"-8",
				"level_id":"1",
				"profilecat_id":null,
				"enabled":"1",
				"verified":"1",
				"language_id":"1",
				"signupdate":"1219689084",
				"ip_signup":"11.1.1.1",
				"ip_lastactive":"11.111.111.111",
				"logins":"466",
				"invitesleft":"5",
				"dateupdated":"1222797372",
				"search":"1",
				"privacy":"63",
				"comments":"63"
			},
			"comments":[
				{
					"id":"123",
					"user_id":"123",
					"user":{
						...
					},
					"text":"This is fantastic",
					"site":{
						"id":0,
						"name":"Kitchen Monki",
						"url":"http:\/\/km.local"
					},
					"created":1204803450,
					"modified":1204814250
				},
				...
			]
		}
	}




