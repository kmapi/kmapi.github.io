---
layout: page
title: "User Management"
description: "User management"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [create a new user](#user-create)
* [delete a user](#user-delete)
* [update user](#user-update)
* [get all users](#get-all-users)

-----------------

### <a id="user-create">&nbsp;</a>Creating a new user



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/user' \
		-d email=xxxxxx@xxxxxx.com \
		-d name_display=John+Smith \
		-d password=p@S$w0rD \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="user-update">&nbsp;</a>Updating a user's info



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

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="user-delete">&nbsp;</a>Removing user from the system



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/user/[user_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="get-all-users">&nbsp;</a>Getting all users


request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/user/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>


