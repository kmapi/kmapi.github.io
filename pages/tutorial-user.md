---
layout: page
title: "User Management"
description: "User management"
group: 'tutorial'
---
{% include JB/setup %}


User management with the Kitchen Monki API is protected and many of the user api calls require a client token and
special client permissions to perform operations on other users.  Each client on Kitchen Monki has their own
user space and most user api calls are restricted to accessing/modifying data within the client's user space.
Kitchen Monki uses OAuth2 for authentication and more details about obtaining access tokens can be found
[here](/pages/authentication.html).  Special permissions and token types required for specific api calls can
be found by following the "full reference" link at bottom of the api call's section in the tutorial.

-----------------

* [create a new user](#user-create)
* [delete a user](#user-delete)
* [update user](#user-update)
* [get a user's info](#get-user)
* [get all users](#get-all-users)

-----------------

### <a id="user-create">&nbsp;</a>Creating a new user

To create a new user, you must provide all 3 request parameters: email, name_display, and password.  In the
response will be the newly created user's id and access token to save.

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/user' \
		-d email=xxxxxx@xxxxxx.com \
		-d name_display=John+Smith \
		-d password=p@S$w0rD \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"add_user",
		"success_message":"Added a new user ",
		"user":{
			"id":[user_id],
			"access_token":"XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
			"token_client_permissions":"..."
		}
	}

<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="user-update">&nbsp;</a>Updating a user's info

The update user api call uses json to specify new values to set for the provided user_id.  Remember to form
encode the values.

data parameter in json format:

	{
		'email': 'yyyyyy@yyyyyy.com',
		'name_display': 'John+Smythe',
		'password': 'Pa$sWoRd'
	}

request:

	curl -X PUT 'http://devapi.kitchenmonki.com/v2/user/[user_id]' \
		-d data=[form encoded json data parameter] \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"update_user",
		"success_message":"Updated user data",
		"user_id":"[user_id]"
	}

<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="user-delete">&nbsp;</a>Removing user from the system

Deleting a user from Kitchen Monki is only allowed using a client token in the same user space, simply provide
the *user_id* to the delete user api call as shown below.

request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/user/[user_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="get-user">&nbsp;</a>Getting a user's info

You can get all of a user's information by sending the get user api call.  All pertinent user information will be
included in the response.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/user/[user_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_user",
		"id":"[user_id]",
		"data":{
			"id":[user_id],
			"name_display":"John Smith",
			"profile_type_id":0
		}
	}

<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="get-all-users">&nbsp;</a>Getting all users

The get all users api call requires no request parameters and will return all users in the same user space.
If the call is made using a user token, then limited fields will be returned in the response.

request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/user/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_all_users",
		"data":[
			{
				"id":[user_id],
				"email":"",
				"name_display":"",
				"name_first":"",
				"name_last":"",
				"user_space_id":"1",
				"password":"$1$29a0952f$jaA54JbZ5Cd9bv343pAB.\/",
				"code":"29a0952f",
				"timezone":"-8",
				"level_id":"1",
				"profilecat_id":"1",
				"enabled":null,
				"verified":null,
				"language_id":"1",
				"signupdate":"1367523515",
				"ip_signup":"127.0.0.1",
				"ip_lastactive":"127.0.0.1",
				"logins":"1",
				"invitesleft":"5",
				"dateupdated":"1367523515",
				"search":"1",
				"privacy":"63",
				"comments":"63"
			},
			...
		]
	}

<a href="/console.html?api_id=" target="blank">full reference</a>


