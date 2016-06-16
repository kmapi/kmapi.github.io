---
layout: page
title: "Authentication"
description: ""
group: getting-started
---
{% include JB/setup %}

## Getting an access token

All api calls require an access_token parameter. Access is done through OAuth2.

In order to get an access token, you need to use client credentials (a client is the party making the api calls).

The file api_helper.php is a simple file that will construct links to make requesting a token easier for testing purposes. Add the client credentials to the top of the file and update the redirect uri. (The redirect uri is the page that a user will come back to after authorizing your app to use their data)

For the examples below, replace CLIENTID and CLIENTSECRET with your client id and client secret

--------------------

### Getting an access token via client credentials

Your client credentials are associated with a Kitchen Monki user, therefore any access token generated with this method will be associated with that same user.

This url:

	https://api-stage.kitchenmonki.com/v2/token/grant?grant_type=client_credentials&client_id=CLIENTID&client_secret=CLIENTSECRET

will return this json data:

	{
	  access_token: "pn1dEItKs1L5jDLWg4snzYfxx0PNqprElZol-YEyZMe",
	  expires_in: 3600,
	  token_type: "bearer",
	  scope: null,
	  refresh_token: "vPcWhJYgyuXx8VxaNt3k8-y2ZKqwOTMeYiPNATVb5jx"
	}

--------------------

### Getting an access token via authorization from 3rd party user

Enabling api calls for a different user requires that the user authorize the client's application. Access tokens retrieved from this method will be associated with the Kitchen Monki user who granted the authorization code.

--------------------

#### Getting an authorization code

Direct the user to the following url. **DO NOT** include your client secret.

	http://stage.kitchenmonki.com/authorize?client_id=CLIENTID&response_type=code&redirect_uri=https%3A%2F%2Fwww.example.com%2Fapi_helper.php

After the user grants access on that page, it will redirect the user back to your redirect uri

	https://www.example.com/api_helper.html?code=YT0pRFSc1DW9RdRFN93AlbsDnhpFoz3JHSBSybuoh2k

At this point you should capture the code and use it to get an access token

--------------------

#### Getting an access token using the authorization code

Authorization codes expire in 30 seconds. Retrieve the access token from this url, passing the authorization code in the "code" parameter:

	https://api-stage.kitchenmonki.com/v2/token/grant?grant_type=authorization_code&code=YT0pRFSc1DW9RdRFN93AlbsDnhpFoz3JHSBSybuoh2k&client_id=CLIENTID&client_secret=CLIENTSECRET&redirect_uri=https%3A%2F%2Fwww.example.com%2Fapi_helper.php

	{
	  access_token: "jxfBpTsr0GYuF_W1bqgOImHvEgN34_1BqpaNhGTFDLs",
	  expires_in: 3600,
	  token_type: "bearer",
	  scope: null,
	  refresh_token: "H2fdWAq0ZY4uwuwfSOYigcL_LhBVtYLSfm66ATSwO58"
	}

#### Using a popup

If you want to open the authorization page in a popup window, the "display" parameter should be set to "popup". If set, the authorization code will be sent to the parent opener window instead of the current window.

Javascript popup example:

	var url = 'http://stage.kitchenmonki.com/authorize?display=popup&client_id=CLIENTID&response_type=code&redirect_uri=https%3A%2F%2Fwww.example.com%2Fapi_helper.php';
	window.open(url, "code_popup", "width=500,height=300");

--------------------

### Getting an access token via a refresh token

When getting an access token, a refresh token will also be issued. Access tokens expire in one hour, but refresh tokens do not expire for two weeks. The refresh token can be used to get a new access token, with the same user association, without the user having to authorize again.

Use this url to get a new access token:

	https://api-stage.kitchenmonki.com/v2/token/grant?grant_type=refresh_token&client_id=CLIENTID&client_secret=CLIENTSECRET&refresh_token=H2fdWAq0ZY4uwuwfSOYigcL_LhBVtYLSfm66ATSwO58

A new access token and refresh token is issued. Note that the old refresh token will be invalidated by this call.

	{
	  access_token: "iG2QKFT6Ox1BG7IXN6y2xOvxu9kPUSmOqVmv0VM42cc",
	  expires_in: 3600,
	  token_type: "bearer",
	  scope: null,
	  refresh_token: "0A_ezNiCxR4lwx5tmsRxSzNMCCWV8trHGqj0_0iWg0o"
	}

--------------------

## Making API calls

Once you have an access token, you can make an api call. The API uses a RESTful interface, and returns JSON data. The preferred method to add the access token is as an HTTP Authorization header, but it can also be added as a GET, POST, or PUT parameter.

Including the token in the header:

	GET /v2/queue HTTP/1.0
	Host: https://api-stage.kitchenmonki.com
	Authorization: Bearer iG2QKFT6Ox1BG7IXN6y2xOvxu9kPUSmOqVmv0VM42cc

View the various API methods available, their required parameters, and try them out using the [API Test Console](http://stage.kitchenmonki.com/api_docs/console)



