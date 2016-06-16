---
layout: page
title: "User Networking"
description: "User networking"
group: 'tutorial'
---
{% include JB/setup %}




-----------------

* [follow a user](#follow-create)
* [stop following a user](#follow-delete)
* [get relationships](#get-relationships)

-----------------

### <a id="follow-create">&nbsp;</a>Follow another user



request:

	curl -X POST 'https://api-stage.kitchenmonki.com/v2/user/[user_id]/following/[followee_id]' \
		-H "Authorization: Bearer [FOLLOW_TOKEN]"

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------


### <a id="follow-delete">&nbsp;</a>Stop following another user



request:

	curl -X DELETE 'https://api-stage.kitchenmonki.com/v2/user/[user_id]/following/[followee_id]' \
		-H "Authorization: Bearer [FOLLOW_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

-----------------

### <a id="get-relationships">&nbsp;</a>Getting all of user's networking relationships

&nbsp;

#### Getting a user's follows



request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/user/[user_id]/following' \
		-H "Authorization: Bearer [FOLLOW_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>

&nbsp;

#### Getting a user's followers



request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/user/[user_id]/followers' \
		-H "Authorization: Bearer [FOLLOW_TOKEN]" \

successful response:

<a href="/console.html?api_id=" target="blank">full reference</a>

&nbsp;

#### Getting a user's friends



request:

	curl -X GET 'https://api-stage.kitchenmonki.com/v2/user/[user_id]/friends' \
		-H "Authorization: Bearer [FOLLOW_TOKEN]" \

successful response:



<a href="/console.html?api_id=" target="blank">full reference</a>


