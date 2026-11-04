# Velitask SDK

[English](README.md)

Публичный SDK для разработки плагинов к [Телеметрическому видеоредактору Velitask](https://velitask.com) (TVE) — видеоредактору, который синхронизирует видео и телеметрию. Создавайте собственные индикаторы, фигуры и источники данных для приложений Velitask на Java 21 и JavaFX.

## Подключение к проекту плагина

Добавьте репозиторий JitPack и зависимость SDK в ваш `build.gradle`:

```gradle
repositories {
    mavenCentral()
    maven { url 'https://jitpack.io' }
}

dependencies {
    compileOnly 'com.github.velitask:velitask-sdk:1.1.+'
    compileOnly 'org.json:json:20250107'
}
```

SDK содержит всё, что есть только у Velitask. Сторонняя библиотека `org.json` (её класс `JSONObject` встречается в API SDK) подключается обычной зависимостью из Maven Central.

Для конкретной версии замените `1.1.+` на тег (например, `1.1.131-beta`). Список всех версий — на странице [Releases](https://github.com/velitask/velitask-sdk/releases).

## Быстрый старт

Готовый шаблон плагина — в репозитории [github.com/velitask/plugin-example](https://github.com/velitask/plugin-example):

```bash
git clone https://github.com/velitask/plugin-example
cd plugin-example
./gradlew jar
```

Получившийся `build/libs/*.jar` положите в папку плагинов Velitask (`~/.velitask/telemitri/plugins/`) — приложение его подхватит.

## Создать плагин с нуля

1. Создайте Java 21 Gradle-проект.
2. Добавьте зависимость SDK (см. выше).
3. Реализуйте `com.velitask.sdk.IPlagin` и свои индикаторы / фигуры / источники.
4. Укажите точку входа в манифесте jar-файла:

   ```gradle
   jar {
       manifest {
           attributes(
               'Velitask-Plugin-Class': 'com.example.MyPlugin'
           )
       }
   }
   ```

5. Соберите `./gradlew jar` и скопируйте результат в `~/.velitask/telemitri/plugins/`.

## Лицензия

Распространяется под [Apache License 2.0](LICENSE).

Apache License 2.0 покрывает **публичный API** этого SDK (пакеты `com.velitask.sdk.**`). Внутренние классы реализации, упакованные и обфусцированные внутри JAR-файла (под непубличными именами пакетов), остаются проприетарными и не подлежат отдельному использованию, модификации или извлечению.

## Issues и контрибьюции

- Баги и фича-реквесты — через [GitHub Issues](https://github.com/velitask/velitask-sdk/issues).
- Pull request'ы приветствуются: документация, примеры, улучшения SDK.
- Исходники самого SDK поддерживаются в приватном репозитории; в этот репозиторий зеркалируются только бинарные релизы.

---

© 2026 Velitask
