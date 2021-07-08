[![Telegram Bot API](https://img.shields.io/badge/Telegram%20Bot%20API-5.2-blue.svg?style=flat-&logo=telegram)](https://core.telegram.org/bots/api)
[![VK API](https://img.shields.io/badge/Vkontakte%20API-5.131-blue.svg?style=flat-&logo=vk)](https://vk.com/dev/methods)
[![VK GIFS Bot](https://img.shields.io/badge/VK%20GIFS%20Bot-blue.svg?style=flat-&logo=telegram)](https://t.me/VKGIFSBot)


# VK GIFS Bot


![Peek 2021-07-09 01-02](https://user-images.githubusercontent.com/53908805/124996454-9fa07d00-e051-11eb-9fbd-3bd31db4e555.gif)

VKGIFSBot - удобный бот для отправки GIF-изображений из ВКонтакте в Телеграмe. Работает это очень просто: бот получает токен ВКонтакте API и делает запрос `docs.get`, который возвращает доступные документы пользователя.
Происходит отобор GIF-изображений и они возвращаются ботом через Inline. Для токенов я создал своё Standalone-приложение ВКонтакте, которое запрашивает доступ ТОЛЬКО к файлам. Это важно, потому что **бот не лезет куда-то дальше**,
а значит ваши сообщения в безопасности. 

## Поиск
Я добавил функцию поиска гифок, которую можно использовать во время инлайн запроса к боту.

![Peek 2021-07-09 01-11](https://user-images.githubusercontent.com/53908805/124997026-9f54b180-e052-11eb-9367-d3d4be9b86df.gif)

## Отправка GIF в документы ВКонтакте
Для того, чтобы отправить GIF из Телеграма в ВКонтакте воспользуйтесь командой `/backup` и отправьте GIF.
![Peek 2021-07-09 01-41](https://user-images.githubusercontent.com/53908805/124999502-f6f51c00-e056-11eb-9145-66455b8f410c.gif)


## Ограничения
`InlineQuery` в Телеграме может возвращать только 50 элементов, поэтому пришлось добавить кнопку "Следующие 50 GIF". При нажатии на неё пользователь отправляет боту `/start`.

Но на самом деле отправляется `/start next` - это называется Deep linking. Это полезно знать разработчикам ботов для Телеграма, поэтому я оставлю [ссылку](https://core.telegram.org/bots#deep-linking).

Слишком большие GIF-изображения также не отображаются.
### UPD
Оказывается в `InlineQuery` можно передать аргумент `next_offset`, который по сути является оффсетом для инлайн-окна. Другими словами, когда пользователь будет листать инлайн-ответ, еще раз вызовется инлайн-функция, только с оффсетом, который вы указали в `next_offset` и его можно обработать, чтобы вернуть следующие 50 GIF.

## Зачем я использую базу данных?
В проекте предусмотрена база данных для сохранения токенов пользователей в случае неисправности сервера.

## Как запустить?
Введите телеграм токен в dockerfile и выполните:
```sh
docker build -t vkgifsbot .
docker run -d --name vkgifs -v /local/path/to/rep/db:/usr/src/app/db --rm vkgifsbot
```

## TODO
...

Можете поставить звёздочку или [поддержать через Киви](https://qiwi.com/n/WEESCR), мне будет очень приятно! 
