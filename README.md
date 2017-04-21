# SSLPoke

Test of java SSL / keystore / cert setup. Came from https://confluence.atlassian.com/download/attachments/117455/SSLPoke.java

Use Gradle to build standalone JAR file:
 
```
./gradlew clean jar
```

Usage:

1. Negative test SSL connection: 

    ```java -jar SSLPoke-0.0.1-SNAPSHOT.jar <server> 443```

    you should get exception like this:
    
    ```
    javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
    ```

1. Create new empty keystore and add exported certificate from server:

    ```
    keytool -import -file certificate.cert -alias certificate -keystore trustStore.keystore
    ```
    
1. Do the test again and specify trustStore with password:
 
    ```java -Djavax.net.ssl.trustStore=trustStore.keystore -Djavax.net.ssl.trustStorePassword=changeit -jar SSLPoke-0.0.1-SNAPSHOT.jar <server> 443```

    you should get positive answer:
    
    ```Successfully connected```