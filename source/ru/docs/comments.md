---
title: Getting Started
description: Getting started with Jigsaw's docs starter template is as easy as 1, 2, 3.
extends: _layouts.documentation.ru
section: main
---


# Комментарии
----------


Комментарии необходимый атрибут для некоторых видов веб-сайтов.
Благодаря им пользователи могут высказывать своё мнение относительно какой-либо записи, 
поддерживать или опровергать высказанные мнения, вести диалог с другими пользователями.


## Создание комментария

Комментарии крепятся к записям ORCHID

```php
use Orchid\Press\Models\Comment;
use Orchid\Press\Models\Post;

// Конкретная запись
$post = Post::find(42);

//Создать комментарий
$comment = Comment::create([
    'post_id'   => $post->id, // номер записи
    'user_id'   => Auth::id(), // номер пользователя
    'parent_id' => 0, // родительский комментарий
    'content'   => 'Моё важное высказывание', // текст коментария
    'approved'  => 1, // одобрен/не одобрен
]);

```


## Отношения


```php

// Получить все комментарии для конкретной записи Post
$comments = Comment::findByPostId(42);


$comment = Comment::find(1);

// Получить связь с Post
$post = $comment->post();

// Получить родительский комментарий
$comment = $comment->original();

// Получить дочерние комментарии
$comment = $comment->replies();

// Получить автора комментария
$comment = $comment->author();

```


## Проверки

```php
$comment = Comment::find(1);


// Проверить опубликован ли комментарий
$comment->isApproved();

// Проверить является ли комментарий ответом на другой комментарий
$comment->isReply();

// Проверить существуют ли у комментария ответы
$comment->hasReplies();
```