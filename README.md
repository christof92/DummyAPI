# DummyAPI

Тестирование сервиса DummyAPI

## Оглавление
1. [Описание проекта](#Описание-проекта)
   1. [USER](#USER)
      1. [PUT /user/:id (Update User)](#PUT-user-id-Update-User)
      2. [DELETE /user/:id (Delete User)](#DELETE-user-id-Delete-User)
   2. [POST](#POST)
      1. [GET /post (Get List)](#GET-post-Get-List)
      2. [POST /post/create (Create Post)](#POST-post-create-Create-Post)
   3. [COMMENT](#COMMENT)
      1. [POST /comment/create (Create Comment)](#POST-comment-create-Create-Comment)
      2. [DELETE /comment/:id (Delete Comment)](#DELETE-comment-id-Delete-Comment)
   4. [TAG](#TAG)
      1. [GET /tag (Get List)](#GET-tag-Get-List)
2. [Майнд-карта](#Майнд-карта)
3. [Тест-кейсы](#Тест-кейсы)
4. [Баг-репорты](#Баг-репорты)
   1. [Баг-репорт №1](#Баг-репорт-№1)
   2. [Баг-репорт №2](#Баг-репорт-№2)
   3. [Баг-репорт №3](#Баг-репорт-№3)
5. [Коллекции и окружение Postman](#Коллекции-и-окружение-Postman)    

## Описание проекта

https://dummyapi.io/ 
Данный сайт представляет собой сервис для тестирования API. Для выполнения запросов необходим app-id, который можно получить автоматически после регистрации на сайте. Были протестированы объекты: **User** (Update и Delete User), **Post** (Get List и Create Post), **Comment** (Create и Delete Comment), **Tag** (Get List).

### USER
___
#### PUT /user/:id (Update User)
Обновляет пользователя по id, возвращает обновленные данные пользователя. В теле запроса указываются пользовательские данные, только поля, которые необходимо обновить (электронная почта запрещена к обновлению).

**Request Body**

**User Full**
```javascript
{
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
gender: string("male", "female", "other", "")
email: string(email)
dateOfBirth: string(ISO Date - value: 1/1/1900 - now)
phone: string(phone number - any format)
picture: string(url)
location: object(Location)
}
```

**Location**
```javascript
{
street: string(length: 5-100)
city: string(length: 2-30)
state: string(length: 2-30)
country: string(length: 2-30)
timezone: string(Valid timezone value ex. +7:00, -1:00)
}
```

**Response Body**

**User Full**
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
gender: string("male", "female", "other", "")
email: string(email)
dateOfBirth: string(ISO Date - value: 1/1/1900 - now)
registerDate: string(autogenerated)
phone: string(phone number - any format)
picture: string(url)
location: object(Location)
}
```

#### DELETE /user/:id (Delete User)
Удаляет пользователя по id, возвращает id удаленного пользователя.

**Response Body** string

### POST
___
#### GET /post (Get List)
Возвращает список постов, отсортированных по дате создания.
- доступен query params для вывода определенной страницы и отображения числа постов на странице
- доступен query params для вывода постов, созданных под собственным app-id

**Response Body** List(Post Preview)

**List**
```javascript
{
data: Array(Model)
total: number(total items in DB)
page: number(current page)
limit: number(number of items on page)
}
```

**Post Preview**
```javascript
{
id: string(autogenerated)
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```

**User Preview**
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
picture: string(url)
}
```

#### POST /post/create (Create Post)
Создает новый пост, возвращает данные созданного поста. В теле запроса указывается id пользователя и данные поста (обязательны для заполнения).

**Request Body**

**Post Create**
```javascript
{
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
owner: string(User id)
}
```

**Response Body**

**Post**
```javascript
{
id: string(autogenerated)
text: string(length: 6-1000)
image: string(url)
likes: number(init value: 0)
link: string(url, length: 6-200)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```

**User Preview**
```javascript
{
id: string(autogenerated)
title: string("mr", "ms", "mrs", "miss", "dr", "")
firstName: string(length: 2-50)
lastName: string(length: 2-50)
picture: string(url)
}
```

### COMMENT
___
#### POST /comment/create (Create Comment)
Создает новый комментарий, возвращает данные созданного комментария. В теле запроса указывается id пользователя и данные комментария (обязательны для заполнения).

**Request Body**

**Comment Create**
```javascript
{
message: string(length: 2-500)
owner: string(User Id)
post: string(Post Id)
}
```

**Response Body**

**Comment**
```javascript
{
id: string(autogenerated)
message: string(length: 2-500)
owner: object(User Preview)
post: string(Post Id)
publishDate: string(autogenerated)
}
```

#### DELETE /comment/:id (Delete Comment)
Удаляет комментарий по id, возвращает id удаленного комментария.

**Response Body** string

### TAG
___
#### GET /tag (Get List)
Возвращает список тегов.

**Response Body** List(string)


## Майнд-карта
Данная МК представляет собой набор тестов для тестирования объектов сервиса DummyAPI. Подробная проверка расписана для **Update** и **Delete** объекта **User**.
![Alt-текст](https://i.imgur.com/nG4q4Ch.png "МК")

Полную майнд-карту для просмотра объектов **Post**, **Comment**, **Tag** можно скачать [здесь.](https://github.com/christof92/DummyAPI/blob/main/DummyAPI_Map.png)

## Тест-кейсы

## Баг-репорты
В процессе тестирования объектов были обнаружены баги. На некоторые из них оформлены баг-репорты с помощью инструмента Redmine.

#### Баг-репорт №1
![Alt-текст](https://i.imgur.com/5lFuuJL.jpeg "1")

#### Баг-репорт №2
![Alt-текст](https://i.imgur.com/y6ileTO.jpeg "2")

#### Баг-репорт №3
![Alt-текст](https://i.imgur.com/5wdGoqT.jpeg "3")



## Коллекции и окружение Postman
Для просмотра всех запросов в Postman можно скачать коллекиции и окружение (окружение обязательно для корректной работы запросов).

#### 




