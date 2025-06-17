# URL


## Intro

## Mind Map

[network](/mobile/kotlin/network.md)

[url](/ios/swift/url.md)

## Library

Ktor - KMP / Kotlin library for URL or network requests which has support for coroutines as well



## URL Builder

In Ktor

```kotlin
import io.ktor.http.URLBuilder  
import io.ktor.http.Url  
import io.ktor.http.set

public class xesURLBuilder {    
    public fun urlBuilder(challenge: String?): Url {  
        val builder = URLBuilder()  
        builder.set(scheme = "https")  

        builder.host = skyAuthConstants.XES_REDIRECT_URL  
        builder.pathSegments = skyAuthConstants.XES_AUTHORIZE_PATH_SEGMENTS  
        builder.parameters.append("partner_id", skyAuthConstants.PARTNER_ID)  
        builder.parameters.append("response_type", skyAuthConstants.RESPONSE_TYPE)  
        builder.parameters.append("client_id", skyAuthConstants.XES_CLIENT_ID)  
        builder.parameters.append("redirect_uri", skyAuthConstants.XES_APP_CALLBACK_URL)  
        builder.parameters.append("code_challenge", challenge ?: skyAuthConstants.CODE_CHALLENGE)  
        builder.parameters.append("code_challenge_method", skyAuthConstants.CODE_CHALLENGE_METHOD)  
  
        val url = builder.build()  
        println("********** URL BUilder********")  
        println(url) 
        return url  
    }    
}
```