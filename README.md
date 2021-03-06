# Vert.x Guice Extensions
Enable Verticle dependency injection using Guice.  Deploy your verticle with the `java-guice:` prefix to use the `GuiceVerticleFactory`.

[![Build Status](http://img.shields.io/travis/ef-labs/vertx-guice.svg?maxAge=2592000&style=flat-square)](https://travis-ci.org/ef-labs/vertx-guice)
[![Maven Central](https://img.shields.io/maven-central/v/com.englishtown.vertx/vertx-guice.svg?maxAge=2592000&style=flat-square)](https://maven-badges.herokuapp.com/maven-central/com.englishtown.vertx/vertx-guice/)

## License
http://englishtown.mit-license.org/


## Configuration

Either provide a com.englishtown.vertx.guice.BootstrapBinder that implements com.google.inject.Module, or via vert.x config, provide a custom class name.

```json
{
    "guice_binder": "my.custom.bootstrap.Binder"
}
```

## Example

```java
package com.englishtown.vertx.guice;

import com.englishtown.configuration.ConfigValueManager;
import com.englishtown.configuration.OtherBinder1;
import com.englishtown.configuration.OtherBinder2;
import com.englishtown.configuration.impl.PropertiesConfigValueManager;
import com.google.inject.AbstractModule;

import javax.inject.Singleton;

public class BootstrapBinder extends AbstractModule {

    @Override
    protected void configure() {

        // Configure bindings
        bind(ConfigValueManager.class).to(PropertiesConfigValueManager.class).in(Singleton.class);

        // Install other binders
        install(new OtherBinder1(), new OtherBinder2());

    }

}
```
