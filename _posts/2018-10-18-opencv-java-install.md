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

2. Если же нужно использовать супер-новую версию opencv, то использовать spring-boot не получится. Тогде процесс установки библиотеки следующий:
- Устанавливаем последнюю версию opencv на сервер. [sh файл](https://github.com/milq/milq/blob/master/scripts/bash/install-opencv.sh), указав нужную версию opencv
- Заливаем файл so в проект (обычно в resources java-проекта заливал) из opencv папки (/usr/local/share/OpenCV/java/libopencv_java330.so)
- Подключаем перед использованием вот так: 

https://github.com/adamheinrich/native-utils


```
try {
            NativeUtils.loadLibraryFromJar("/libopencv_java330.so");
        } catch (Exception e) {
            Logger.trace(e);
        }
```