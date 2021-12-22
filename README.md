# Easy NSD

The EasyNSD library allows for easy integration of network service discovery into your app. 

----


## How to Use 

### Setup

Include the below dependencies in your `build.gradle` project.

```gradle
buildscript {
    repositories {
        google()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local" }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:7.0.4'
        classpath 'com.newtronlabs.android:plugin:5.0.2'
    }
}

allprojects {
    repositories {
        google()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local" }
    }
}

subprojects {
    apply plugin: 'com.newtronlabs.android'
}
```

In the `build.gradle` for your app.

```gradle
dependencies {
    compileOnly 'com.newtronlabs.easynsd:easynsd:1.0.1-alpha01'
}
```


### EasyNsd - Service Discovery
In order to discover services we obtain a cient and call discoverServices with the service type to discover.

```java
// Search for services for 5 seconds
EasyNsd.with(this).discoverServices(serviceType = "_ipp._tcp.", timeout = 5 * 1000L).await()
```

### EasyNsd - Registration
To register a service.

```java
val serviceInfoNsd = EasyNsdServiceInfo().apply {
    setServiceName("EasyNsd")
    setServiceType("_ipp._tcp.")
    setPort(1234)
}

// Note: This is a blocking call, user the callback if async behavior is desired.
val serviceInfo = EasyNsd.with(this@MainActivity).registerService(serviceInfoNsd).await()
```
### EasyNsd - Service resolution
Once a service is found it can be resolved by calling resolveService with the service information object found.
```java
val resolvedService = EasyNsd.with(this@MainActivity).resolveService(foundServiceInfoNsd).await()
```

---

## Support Us
Please support the continued development of these libraries. We host and develop these libraries for free. Any support is deeply appriciated. Thank you!

<p align="center">
  <img src="https://drive.google.com/uc?id=1rbY8qjxvWU8GQgaqDrOY4-fYOWobQKk3" width="200" height="200" title="Support us" alt="Support us">
</p>

<p align="center">
  <strong>BTC Address:</strong> 39JmAfnNhaEPKz5wjQjQQj4jcv9BM11NQb
</p>

---

## License
https://gist.github.com/NewtronLabs/216f45db2339e0bc638e7c14a6af9cc8


## Contact

solutions@newtronlabs.com

