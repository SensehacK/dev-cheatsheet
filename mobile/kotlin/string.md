
## Concatenation

```kotlin
public object NetflixAuthConstants {
 public object SVP {

        public const val BASE_URL: String = "session.exp.SVP.eu-2.plex.tv"
        public const val SUBDOMAIN_SVP: String = "exp.SVP"
        public const val PROD: String = "session"
        public const val STAGE: String = "session-stg"
        public const val REGION: String = "eu-1"
        public const val DOMAIN: String = "xcal.tv"
        public val SESSION_PATH_SEGMENTS: List<String> =
            listOf("v1","partners", "Netflix-uk")
        public const val PARTNERS: String = "v1/partners/"
        public const val PARTNER_Netflix: String = "Netflix-uk"
        public const val SESSION: String = "session"
        public val CATALOG_TYPES: List<String> = listOf("device", "cacheProfile", "account", "goes")
        public const val CODE_CHALLENGE_METHOD: String = "S256"
    }
}

fun main() {
    val env = NetflixAuthConstants.SVP.STAGE
    val baseURL = "${NetflixAuthConstants.SVP.SUBDOMAIN_SVP}.${env}."
    println(baseURL)
    val generatedHost = "${baseURL}.${NetflixAuthConstants.SVP.REGION}.${NetflixAuthConstants.SVP.DOMAIN}"
    println(generatedHost)
    
    val baseURL2 = "$NetflixAuthConstants.SVP.SUBDOMAIN_SVP.$env."
    println(baseURL2)
}
```
## Nuances

`$env` works
but `$NetflixAuthConstants.SVP.SUBDOMAIN_SVP` wont

You only have to do curly braces if there is a dot call on it