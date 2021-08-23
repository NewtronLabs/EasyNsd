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
        jcenter()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local"
            metadataSources {
                artifact()
            }
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.2'
        classpath 'com.newtronlabs.android:plugin:4.0.6-alpha01'
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local"
            metadataSources {
                artifact()
            }
        }
    }
}

subprojects {
    apply plugin: 'com.newtronlabs.android'
}
```

In the `build.gradle` for your app.

```gradle
dependencies {
    compileOnly 'com.newtronlabs.easynsd:easynsd:1.0.0'
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
val serviceInfo = EasyNsd.with(this@MainActivity).registerService(
        serviceInfoNsd
    ).await()
```
### EasyNsd - Service resolution
Once a service is found it can be resolveed by calling resolveService with the service information object found.
```java
val resolvedService =
EasyNsd.with(this@MainActivity).resolveService(foundServiceInfoNsd).await()
```

## License
https://gist.github.com/NewtronLabs/216f45db2339e0bc638e7c14a6af9cc8


## Contact

solutions@newtronlabs.com

