---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/04/2018
ms.author: glenga
ms.custom: fasttrack-edit
ms.openlocfilehash: 574544df1ad89b277f2e07103b02b9b591fb3924
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96002401"
---
W tej tabeli przedstawiono powiązania, które są obsługiwane w głównych wersjach środowiska uruchomieniowego Azure Functions:


| Typ | 1.x | 2. x i więcej<sup>1</sup> | Wyzwalacz | Dane wejściowe | Dane wyjściowe |
| ---- | :-: | :-: | :------: | :---: | :----: |
| [Blob Storage](../articles/azure-functions/functions-bindings-storage-blob.md)          |✔|✔|✔|✔|✔|
| [Azure Cosmos DB](../articles/azure-functions/functions-bindings-cosmosdb-v2.md)               |✔|✔|✔|✔|✔|
| [Dapr](https://github.com/dapr/azure-functions-extension)<sup>3</sup>             | |✔|✔|✔|✔|
| [Event Grid](../articles/azure-functions/functions-bindings-event-grid.md)              |✔|✔|✔| |✔|
| [Event Hubs](../articles/azure-functions/functions-bindings-event-hubs.md)              |✔|✔|✔| |✔|
| [Elementy webhook & HTTP](../articles/azure-functions/functions-bindings-http-webhook.md)             |✔|✔|✔| |✔|
| [IoT Hub](../articles/azure-functions/functions-bindings-event-iot.md)             |✔|✔|✔| |✔|
| [Kafka](https://github.com/azure/azure-functions-kafka-extension)<sup>2</sup>             | |✔|✔| |✔|
| [Mobile Apps](../articles/azure-functions/functions-bindings-mobile-apps.md)             |✔| | |✔|✔|
| [Notification Hubs](../articles/azure-functions/functions-bindings-notification-hubs.md) |✔|| | |✔|
| [Queue Storage](../articles/azure-functions/functions-bindings-storage-queue.md)         |✔|✔|✔| |✔|
| [RabbitMQ](https://github.com/azure/azure-functions-rabbitmq-extension)<sup>2</sup>             | |✔|✔| |✔|
| [SendGrid](../articles/azure-functions/functions-bindings-sendgrid.md)                   |✔|✔| | |✔|
| [Service Bus](../articles/azure-functions/functions-bindings-service-bus.md)             |✔|✔|✔| |✔|
| [SignalR](../articles/azure-functions/functions-bindings-signalr-service.md)             | |✔| |✔|✔|
| [Table Storage](../articles/azure-functions/functions-bindings-storage-table.md)         |✔|✔| |✔|✔|
| [Czasomierz](../articles/azure-functions/functions-bindings-timer.md)                         |✔|✔|✔| | |
| [Twilio](../articles/azure-functions/functions-bindings-twilio.md)                       |✔|✔| | |✔|

<sup>1</sup> począwszy od wersji 2. x środowiska uruchomieniowego, wszystkie powiązania z wyjątkiem http i Timer muszą być zarejestrowane. Zobacz [Rejestrowanie rozszerzeń powiązań](../articles/azure-functions/functions-bindings-register.md).

<sup>2</sup> wyzwalacze nie są obsługiwane w planie zużycia. Wymaga [wyzwalaczy sterowanych przez środowisko uruchomieniowe](../articles/azure-functions/functions-networking-options.md#premium-plan-with-virtual-network-triggers).

<sup>3</sup> obsługiwane tylko w Kubernetes, IoT Edge i innych trybach samoobsługowych.
