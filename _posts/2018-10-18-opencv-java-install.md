---
published: false
---
## Варианты установки opencv в проект на java
### Основные моменты
1. Если используется в приложения java framework spring-boot, то существует конфликт подключения вручную библиотеки opencv через System.loadLibrary. Поэтому лучше использовать вариант с maven библиотекой:


```
<dependency>
   <groupId>org.openpnp</groupId>
   <artifactId>opencv</artifactId>
   <version>3.2.0-1</version>
</dependency>
Ater it I remove library from java build path, wich added manualy earlier.

For init library:

OpenCV.loadShared();
```

