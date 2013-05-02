---
layout: page
title: "Ingredients"
description: "Finding ingredients"
group: 'tutorial'
---
{% include JB/setup %}


Kitchen Monki Ingredients are standardized ingredient objects used as the basis of creating recipe
ingredients or making a shopping list.  The difference between ingredients and recipe ingredients is that
recipe ingredients are data specific to a recipe containing data such as brand, unit type, quantity, etc.
Ingredients are just the pure ingredient data containing the name and category of the ingredient, for
instance "Chicken Wing".  Ingredient objects are nested inside of recipe ingredient objects and the ids
*recipe_ingredient_id* and *ingredient_id* do not belong to the same model.  The ability to group
recipe ingredients by their nested ingredients allows Kitchen Monki to group line items in grocery
shopping lists and other tools which combine multiple recipes.

There are thousands of pre-existing ingredients in the Kitchen Monki database, and where at all possible
these ingredients should be used.  However, should the user not find the exact ingredient they are looking
for, the ability to add custom ingredients to the system is available.  Custom ingredients added to the
system will not be added to the standardized data, but will be added to the system as a custom ingredient
associated with the recipe it was created with.

-----------------

* [search ingredients](#search-ingredients)
* [find an ingredient by id](#get-ingredient)

-----------------


### <a id="search-ingredients">&nbsp;</a>Search ingredients

Due to the sheer amount of pre-existing ingredients available, it is recommended to make some sort of
autocomplete form control which uses ajax to call the search ingredient api call as the user types input
with their keyboard.  Using the limit param will allow your application to make choosing an ingredient
a user friendly and efficient process.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/ingredient/search' \
		-d text=rice \
		-d limit=100 \
		-d offset=1000 \
		-d array_key=id \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"ingredient_search",
		"total":4381,
		"limit":20,
		"offset":0,
		"data":[
			{
				"id":[ingredient_id],
				"name":"Brown Rice",
				"name_plural":"",
				"name_nomenclature":"Rice, Brown",
				"category_id":[category_id]
			},
			...
		]
	}

<a href="/console.html?api_id=29" target="blank">full reference</a>

-----------------


### <a id="get-ingredient">&nbsp;</a>Find an ingredient by ingredient_id

If the *ingredient_id* is known, for example from a recipe ingredient or grocery list item, then you can
get the associated ingredient data with the get ingredient api call.  Just provide the *ingredient_id*
at the end of the request uri and send the request via the GET method.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/ingredient/[ingredient_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"id":[ingredient_id],
		"data":{
			"id":[ingredient_id],
			"name":"Frozen Teriyaki Style Chicken Wing",
			"name_plural":"Teriyaki Style Chicken Wings",
			"name_nomenclature":"Chicken, Frozen Teriyaki Style Wing",
			"category_id":10
		}
	}

<a href="/console.html?api_id=28" target="blank">full reference</a>



