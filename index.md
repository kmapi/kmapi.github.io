---
layout: page
tagline: Engage your audience with a Food Community
---
{% include JB/setup %}

## Getting Started

------------
#### Searching and Adding Recipes

Recipes are the central building block to using the Kitchen Monki API...

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

Brands in Kitchen Monki are available for recipe owners to specify the exact brands of ingredients needed
to cook their recipe.  They are completely optional to use with recipe ingredients.  Brand families are
the brand (manufacturer) name like "C&H", while brand items are a specific product (brand and ingredient)
such as "C&H Brown Sugar".  Brand families and items can not be created by end users, however they can
be created by administrators of Kitchen Monki API clients with the use of a client token.

The photo section of the api exists to facilitate adding recipe photos user created recipes.  Kitchen Monki uses
Amazon S3 to store the uploaded images.  Of course multiple images can be uploaded per recipe and there are
options provided on how the image should be cropped and scaled.

------------
#### Using the Recipe Tools

Bookmarks are a convenient way to save a desired recipe for further reference.  Not much to it, they work
exactly like a bookmark should.  You can add them, view them all, and delete them when no longer needed.

The Recipe Queue is basically a temporary holding area to store recipes while browsing and searching.  After
adding a bunch of recipes to it, it is designed for a user to be able to then view the queue and decide whether
or not to add them to different recipe tools.

------------
#### Meal Plans

The Meal Planner is a time saving tool to plan out your meals for the week/month.  Its a calendar setup to easily
add recipes to a specific date and meal.  It is designed to conveniently get meals for a span of dates or a
specific date, grouped by the meal it was specified as and with the amount of servings chosen for that dish.
Also built in to Kitchen Monki is the functionality to generate shopping lists over a span of time and yes the
shopping list items will be grouped if duplicated and the store and location data for them will be included.

------------
#### Grocery Shopping Lists

Grocery Shopping Lists are a powerful tool with which you can create lists of ingredients you will need
to shop for, the brands and amounts of the ingredients, the stores where you want to shop, and even the
aisles where to find each ingredient!  Lists can be created from a time period on your Meal Planner like,
creating a shopping list of ingredients that are needed to cook all of the meals on the Planner for this
week.  Duplicate ingredients will be combined even if they have different unit types.

------------
#### Stores and Locations

Locations and stores are available for users to enhance their shopping experience by allowing them to specify
which stores they would like to purchase grocery list items from.  Users can add new locations to their profile
and Kitchen Monki will use the Google Places API to match stores that lie within the area.  Only stores that the
user chooses will be added to their location and a single store can be set to use as default for convenience.
Once that is setup, the user can dictate where specific grocery list items should be purchased from.


------------
### Recent Posts

<ul class="posts">
  {% for post in site.posts %}
	<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


