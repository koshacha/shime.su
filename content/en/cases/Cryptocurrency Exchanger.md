---
description: A cryptocurrency buying and exchanging app created with React.js and Socket.IO.
year: 2023
sort: 5
published: true
tags:
  - React.js
seoDescription: Cryptocurrency exchanger project featuring React.js, React
  Router, TypeScript, Socket.IO, and Docker for efficient exchange operations.
color: "#5077FF"
icon: doodles:sphere
layout: project
link: https://deswop.com
image: /image/flyid.jpg
---

## Introduction

Quite an interesting project I've been working on. Using **React.js**, I created a website that allows users to exchange cryptocurrency. The interface was created using Tailwind CSS, and communication with the backend is mostly done using Socket.io messaging. Also, the project has a pretty simple internationalization. In this project I only worked on Frontend and a little bit on DevOps.

## Links

- Git repository: **not available due to NDA**

## Choosing a React.js

The site is quite simple, globally it consists of a cryptocurrency exchange component and minimalistic content pages, so I chose React.js. I also decided to use TypeScript in this project to simplify the work of future developers and protect the client from unexpected errors.

## Work Progress

The project was finished quite quickly, during the work I mastered working with Socket.io, strengthened my knowledge about dockerization of projects and about routing in React.js. Most importantly, I got to know Vite.

## Interesting realization details

I decided to fully type Socket.io inbound and outbound, but as it turns out, there isn't much information about this in the official documentation.

Incoming messages:

- *ticker* - contains either exchange rate data or current order data
- *order* - contains data about created, requested order.

And here are the outgoing messages. They are more complicated, because from the backend side all these messages were received with a single identifier "order".

- *currencies* - request currency data.
- *order\_data* - request order data.
- *change* - create a request for currency exchange
- *rate* - evaluate the work of the service, whether the order was fulfilled (or not).

I wrote the following code, which completely covered my needs in this typing and works just perfectly.

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

## Screenshots

::gallery
---
alts:
  - Widget
  - Payment page
  - Advantages
images:
  - /image/cases/dswp/image-1.jpg
  - /image/cases/dswp/image-3.jpg
  - /image/cases/dswp/image-2.jpg
---
::
