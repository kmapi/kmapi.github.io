---
layout: page
title: "Recipe Api Comparison"
tagline: "How we stack up"
description: ""
group: getting-started
---
{% include JB/setup %}


<style>
	ul.pros-and-cons li {
		font-size: 12px;
		margin-top: -4px;
	}
</style>

##### [Kitchen Monki](#kitchen-monki-api)
<ul class='pros-and-cons'>
	<li>Pros:<br />
		<ul>
			<li>Users can add, update, and delete recipes</li>
			<li>Recipe tools are highly evolved and provide advanced functionality</li>
			<li>Thorough documentation and developer tools</li>
		</ul>
	</li>
	<li>
		Cons:<br />
		<ul>
			<li>Smaller recipe base</li>
		</ul>
	</li>
</ul>

##### [Yummly](#yummly-api)
<ul class='pros-and-cons'>
	<li>Pros:<br />
		<ul>
			<li>Large recipe base</li>
			<li>Gives users access to nutitional facts and calculated flavors</li>
		</ul>
	</li>
	<li>
		Cons:<br />
		<ul>
			<li>Users can not add their own recipes</li>
			<li>Recipes are scraped from other websites around the web, not original content</li>
			<li>Developer resources are lacking</li>
		</ul>
	</li>
</ul>

##### [Big Oven](#big-oven-api)
<ul class='pros-and-cons'>
	<li>Pros:<br />
		<ul>
			<li>Can format responses in JSON or XML</li>
			<li>Usage is free while still in beta</li>
		</ul>
	</li>
	<li>
		Cons:<br />
		<ul>
			<li>Users can not add their own recipes</li>
			<li>Recipe search lacks options</li>
			<li>Recipe tools are currently very limited in functionality</li>
			<li>No live testing or API community pages</li>
		</ul>
	</li>
</ul>

&nbsp;

-----------------


## <a id="kitchen-monki-api">&nbsp;</a><a href='http://kmapi.github.io'>Kitchen Monki API</a>

&nbsp;

#### Pricing
* 4 affordable price plans to choose from

&nbsp;

#### Content
* Over 20k member generated recipes
* All original content not recycled from other websites

&nbsp;

#### API Features
* 60 API calls available
* Users can add new Recipes to the system
* Recipe model is well structured and highly customizable
* Fully integrated Meal Planner
* Automated Grocery List generator
* Support for Geolocated Stores and Locations
* Internal social networking capabilities
* Ingredient Brand support
* Can add Bookmarks
* Recipe Queue
* Extensive list of meta tags to apply to recipes

&nbsp;

#### API Documentation
* Tutorials available for every tool in our API, with detailed instruction of exactly how and why to use each
API call and things to watch for
* Fully functional test console to test each API call live, with complete details for each call including request
parameters, default values, possible error codes with descriptions, and the live response
* cURL command line examples provided for an alternate way to test API calls
* Community discussion forum dedicated to API developers
* Frequently Asked Questions page

&nbsp;

#### Admin
* API Usage Stats - (coming soon)

&nbsp;

#### Technical implementation
* REST API
* OAuth2
* JSON response format

&nbsp;

#### Customer support
* Email and Phone support

-----------------


## <a id="yummly-api">&nbsp;</a><a href='https://developer.yummly.com/#api'>Yummly API</a>

&nbsp;

#### Pricing
* 4 plans - 3 commercial plans, 1 free up to 500 calls per day
* Recipe ads required for cheaper plans
* Attribution required for cheaper plans - url, text, logo, and source
* More expensive plans provide limited recipe caching

&nbsp;

#### Content
* 1 Million recipes aggregated from multiple sources
* 100k+ Classifications based on Food Genome & Yummly Algorithms

&nbsp;

#### API Features
* Only 2 API calls available to developers: users can get and search recipes

##### Recipe Search
* can require or exclude specific ingredients
* can specify recipes to filter by a specific diet or allergy
* can filter meta data based on course, cuisine, or holiday
* can specify the maximum time allowed to cook the recipe
* can specify nutritional values in milligrams for specific nutrients
* can specify desired flavor values based on 6 different flavor types
* can request facet counts for fields such as diet, ingredients
* returns a rating value for each recipe matched

##### Get Recipe
* ingredients returned are lines of text not objects, so no access to fields like unit type, quantity, etc.
* nutrition estimates for the entire recipe are returned as objects and contain unit, value, and description

&nbsp;

#### API Documentation
* Single page with anchors.  Sufficient to describe how to get authentication, full descriptions of request
parameters, sample JSON responses, and specific API requirements

&nbsp;

#### Admin
* API Messages
* API Usage Stats - shows stat metrics graph between dates and choosable interval

&nbsp;

#### Technical implementation
* REST API
* Response format - JSON, JSONP
* Supports gzip compression

&nbsp;

#### Customer support
* Email only

&nbsp;

-----------------


## <a id="big-oven-api">&nbsp;</a><a href='http://api.bigoven.com/'>Big Oven API</a>

&nbsp;

#### Pricing
* Free for now - still in beta
* Clients must accompany Big Oven API results with a provided branded Big Oven logo

&nbsp;

#### Content
* 250k recipes

&nbsp;

#### API Features

* Currently can only get existing recipes not create new ones.
* Basic text search available for recipes, no advanced search options
* Can add reviews to recipes
* Can create grocery lists, but functionality is very limited
* Ability to look up food glossary terms, but not create
* Can flag recipes as "favorites" and "try soons"
* Can not create new users,

&nbsp;

#### API Documentation
* Decent documentation of API calls, however they lack descriptions of why you would use each call.
* Good descriptions of paging, sorting, and filtering
* Easy to find information about the API such as authentication versioning, usage throttling, response codes
* No tutorials, sample responses, live testing tool, forum, or faq

&nbsp;

#### Admin
* None yet as of beta

&nbsp;

#### Technical implementation
* REST API
* Response format - JSON, XML
* HTTP Basic Access Authentication

&nbsp;

#### Customer support
* Email only

&nbsp;








