---
title: Обменник криптовалюты
description: Приложение для покупки и обмена криптовалюты, созданное с помощью
  React.js и Socket.IO.
year: 2023
sort: 5
tags:
  - React.js
published: true
seoDescription: Проект криптовалютного обменника с использованием React.js,
  React Router, TypeScript, Socket.IO и Docker для эффективных обменных
  операций.
color: "#5077FF"
icon: doodles:sphere
layout: project
link: https://deswop.com
image: /image/flyid.jpg
---

## Введение

Довольно интересный проект, над которым я работал. Используя **React.js**, я создал сайт, который позволяет пользователям обменивать криптовалюту. Интерфейс был создан с помощью Tailwind CSS, а связь с бэкендом осуществляется в основном с помощью обмена сообщениями Socket.io. Также проект имеет довольно простую интернационализацию. В этом проекте я работал только над Frontend и немного над DevOps.

## Ссылки

- Git-репозиторий: **NDA**

## Выбор React.js

Сайт довольно простой, глобально он состоит из компонента криптовалютной биржи и минималистичных контентных страниц, поэтому я выбрал React.js. Также я решил использовать TypeScript в этом проекте, чтобы упростить работу будущих разработчиков и защитить клиента от непредвиденных ошибок.

## Ход работы

Проект был закончен довольно быстро, за время работы я освоил работу с Socket.io, укрепил свои знания о докеризации проектов и о маршрутизации в React.js. И самое главное - я познакомился с Vite.

## Интересные детали реализации

Я решил полностью типизировать входящие и исходящие сообщения Socket.io, но, как оказалось, в официальной документации об этом не так много информации.

Входящие сообщения:

- _ticker_ - содержит либо данные о курсе валют, либо данные о текущем ордере
- _order_ - содержит данные о созданном, запрошенном ордере.

А вот исходящие сообщения. Они сложнее, так как со стороны бэкенда все эти сообщения были получены с одним идентификатором «order».

- _currencies_ - запрос данных о валюте.
- _order_data_ - запрос данных о заказе.
- _change_ - создать запрос на обмен валюты.
- _rate_ - оценить работу сервиса, был ли выполнен заказ (или нет).

Я написал следующий код, который полностью покрыл мои потребности в данной типизации и работает просто идеально.

::prose-code

```ts
interface ServerToClientEvents {
  ticker: (
    message: SocketCurrenciesMessage | SocketExchangeRateMessage
  ) => void;
  order: (res: OrderResponse) => void;
}

export interface ClientSocket extends Socket<ServerToClientEvents> {
  emit(event: "order", type: "currencies"): this;
  emit(event: "order", type: "order_data", dto: GetOrderDto): this;
  emit(event: "order", type: "change", dto: CreateOrderDto): this;
  emit(event: "order", type: "rate", dto: OrderRateDto): this;
}
```

::

## Скриншоты

::gallery
---
alts:
  - Компонент для обмена валюты
  - Страница оплаты
  - Раздел преимуществ
images:
- /image/cases/dswp/image-1.jpg
- /image/cases/dswp/image-3.jpg
- /image/cases/dswp/image-2.jpg
---
::
