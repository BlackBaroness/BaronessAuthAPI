## API для плагина аутентификации BaronessAuth

Обзор / купить: https://market.baronessdev.ru/shop/baronessauth.1/

JavaDoc: https://blackbaroness.github.io/BaronessAuthAPI/

### Добавление библиотеки в проект

Для скачивания свежего артефакта можно использовать этот скрипт:

```
#!/bin/bash

rm BaronessAuthAPI.jar
wget https://github.com/BlackBaroness/BaronessAuthAPI/releases/latest/download/BaronessAuthAPI.jar
echo "Latest API jar downloaded"

exit 0;
```

После этого, вы можете добавить библиотеку в проект любым удобным способом. Например, через Maven:

```
<dependency>
    <groupId>ru.baronessdev.paid.auth</groupId>
    <artifactId>BaronessAuthAPI</artifactId>
    <version>LATEST</version>
    <scope>system</scope>
    <systemPath>${project.basedir}/BaronessAuthAPI.jar</systemPath>
</dependency>
```

### Использование ACF

Для добавления субкоманд рекомендуется использование ACF (https://github.com/aikar/commands).

Имейте в виду, что зависимость ACF в вашем проекте не должна быть использована в качестве компонента субкоманды. То есть
для любых ACF классов вы должны использовать пакет `ru.baronessdev.paid.auth.lib.acf`, который поставляется в артефакте
API.

## Примеры взаимодействия (для большего читайте JavaDoc)

### Получение данных игрока

```
PlayerProfile profile = BaronessAuthAPI.getDataManager().getProfile("nickname");
if (profile == null) {
    System.out.println("Игрок не зарегистрирован");
    return;
}

System.out.println("Игрок зарегистрирован с IP адреса " + profile.getFirstIP());
```

### Заморожен ли игрок

```
QueryType query = BaronessAuthAPI.getQueryManager().getQuery(player);
System.out.println((query == null) 
    ? "Игрок не заморожен"
    : "Игрок заморожен с запросом " + query.name()
);
```