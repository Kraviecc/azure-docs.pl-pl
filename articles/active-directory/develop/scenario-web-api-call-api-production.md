---
title: Przenoszenie internetowego interfejsu API wywoływanie interfejsów API sieci Web do środowiska produkcyjnego | Azure
titleSuffix: Microsoft identity platform
description: Dowiedz się, jak przenieść internetowy interfejs API, który wywołuje interfejsy API sieci Web w środowisku produkcyjnym.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 370bedf04dc61e2a637f735580cd4df14061264a
ms.sourcegitcommit: 5cdd0b378d6377b98af71ec8e886098a504f7c33
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2021
ms.locfileid: "98753335"
---
# <a name="a-web-api-that-calls-web-apis-move-to-production"></a>Internetowy interfejs API, który wywołuje interfejsy API sieci Web: Przenieś do środowiska produkcyjnego

Po uzyskaniu tokenu do wywoływania interfejsów API sieci Web można przenieść aplikację do środowiska produkcyjnego.

[!INCLUDE [Move to production common steps](../../../includes/active-directory-develop-scenarios-production.md)]

## <a name="learn-more"></a>Więcej informacji

Teraz, gdy znasz podstawowe informacje o sposobie wywoływania interfejsów API sieci Web z własnego interfejsu API sieci Web, być może zainteresuje Cię Poniższy samouczek, w którym opisano kod używany do tworzenia chronionego internetowego interfejsu API, który wywołuje interfejsy API sieci Web.

| Przykład | Platforma | Opis |
|--------|----------|-------------|
| [Active-Directory-aspnetcore-WebAPI-samouczek](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/2.%20Web%20API%20now%20calls%20Microsoft%20Graph) — rozdział 1 | ASP.NET Core Web API, Desktop (WPF) | ASP.NET Core wywołań interfejsu Web API Microsoft Graph, które są wywoływane z aplikacji WPF przy użyciu platformy tożsamości firmy Microsoft. |
