---
layout: post
title: Handling API access token refresh
description: 
summary: 
comments: true
tags: [caffeine, api, access token]
---

There are numerous resources on the Web on how to handle external API access tokens. One thing they have in common is the best practice that consists in storing the token internally in order to avoid unnecessary refreshes. I was recently confronted with this at work. 

Our application needed to make authenticated requests to an external Web API. At first we implemented our client to make a call to the authorization server to retrieve the access token before performing the actual request. We were making unnecessary calls to the auth server. We eventually got a call from the team in charge of the saas, with a suggestion to limit those calls.

We decided to use a cache system to store the access token until it expires.

## Caffeine

We chose [caffeine](https://github.com/ben-manes/caffeine), "a high performance, near optimal caching library". Caffeine is for Java applications and is well integrated with popular frameworks like **Spring**, **Camel**, **Quarkus** ...

Caffeine can be added via Maven : 

```xml
<dependencies>
    <!-- https://mvnrepository.com/artifact/com.github.ben-manes.caffeine/caffeine -->
    <dependency>
        <groupId>com.github.ben-manes.caffeine</groupId>
        <artifactId>caffeine</artifactId>
        <version>2.9.2</version>
    </dependency>
</dependencies>
```

### AccessTokenHandler

We then write a `AccessTokenHandler`which will provide accessToken in order to perform our requests : 

```java
public class AccessTokenHandler {

	private LoadingCache<String, Object> cache;

	private static AccessTokenHandler instance;

	private AccessTokenHandler() {
		cache = Caffeine.newBuilder()
				.maximumSize(1)
				.expireAfterWrite(Duration.ofMinutes(59))
				.build(key -> requestAccessToken());
	}
	
	public static synchronized KyribaAPIauthenticator getInstance() {
		if (instance == null) {
			instance = new KyribaAPIauthenticator();
		}
		return instance;
	}

	public String getAccessToken() {
		return (String) cache.get("external-api-access-token");
	}

	private String requestAccessToken() {
		//TODO Retrieve access token from Auth server	
    }
}
```

`AccessTokenHandler`is a Singleton providing a single access to the token cache.

In the private constructor we build a `LoadingCache` with a `maximumSize`  of 1, which expires 59 minutes after write. The `requestAccessToken()` Function is used to refresh the access token from auth server.

`AccessTokenHandler`provides a `getAccessToken()`method to retrieve the cached access token value. The cache is then used as the main facade and we only call the authentication server after the access token is expired.

