---
title: Czym jest interfejs API wyszukiwania jednostek Bing?
titleSuffix: Azure Cognitive Services
description: Dowiedz się więcej o interfejs API wyszukiwania jednostek Bing i sposobach wyodrębniania i wyszukiwania jednostek oraz miejsc z zapytań wyszukiwania.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-entity-search
ms.topic: overview
ms.date: 12/18/2019
ms.author: scottwhi
ms.openlocfilehash: 2a3d971ce9a4f89555eb3ffa489f8b19172a4b83
ms.sourcegitcommit: 9eda79ea41c60d58a4ceab63d424d6866b38b82d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2020
ms.locfileid: "96351473"
---
# <a name="what-is-bing-entity-search-api"></a>Czym jest interfejs API wyszukiwania jednostek Bing?

> [!WARNING]
> Interfejsy API wyszukiwania Bing są przenoszone z Cognitive Services do usług Wyszukiwanie Bing. Od **30 października 2020** wszystkie nowe wystąpienia wyszukiwanie Bing muszą być obsługiwane zgodnie z procesem opisanym [tutaj](/bing/search-apis/bing-web-search/create-bing-search-service-resource).
> Interfejsy API wyszukiwania Bing obsługa administracyjna przy użyciu Cognitive Services będzie obsługiwana przez kolejne trzy lata lub do końca Umowa Enterprise, w zależności od tego, co nastąpi wcześniej.
> Instrukcje dotyczące migracji znajdują się w temacie [wyszukiwanie Bing Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource).

Interfejs API wyszukiwania jednostek Bing wysyła zapytanie wyszukiwania do usługi Bing i pobiera wyniki, które zawierają jednostki i miejsca. Wyniki dotyczące miejsc to między innymi restauracje, hotele i inne lokalne firmy. Wyszukiwarka Bing zwraca wyniki dotyczące miejsc, jeśli w zapytaniu określono nazwę lokalnej firmy lub zadano pytanie dotyczące typu firmy (na przykład „restaurants near me” — restauracje w pobliżu). Bing zwraca jednostki, jeśli zapytanie określa dobrze znane osoby, miejsca (turystyczny attractions, Stany, kraje/regiony itp.) lub rzeczy.

|Cechy  |Opis  |
|---------|---------|
|[Sugestie dotyczące wyszukiwania w czasie rzeczywistym](concepts/search-for-entities.md#suggest-search-terms-with-the-bing-autosuggest-api)     | Podaj sugestie dotyczące wyszukiwania, które mogą być wyświetlane jako lista rozwijana podczas wpisywania przez użytkowników.       | 
| [Uściślanie jednostki](concepts/search-for-entities.md#the-bing-entity-search-api-response)  | Uzyskaj wiele jednostek dla zapytań z wieloma możliwymi znaczeniami. |
| [Znajdowanie miejsc](concepts/search-for-entities.md#find-places) | Wyszukaj i zwróć informacje dotyczące lokalnych firm i jednostek  |

## <a name="workflow"></a>Przepływ pracy

Interfejs API wyszukiwania jednostek Bing jest usługą internetową RESTful łatwą do wywołania z dowolnego języka programowania, który może wysyłać żądania HTTP i analizować kod JSON. Możesz użyć tej usługi za pomocą interfejsu API REST lub zestawu SDK.

1. Utwórz [konto interfejsu API usług Cognitive Services](../cognitive-services-apis-create-account.md) z dostępem do interfejsów API wyszukiwania Bing. Jeśli nie masz subskrypcji platformy Azure, możesz [utworzyć konto](https://azure.microsoft.com/free/cognitive-services/) bezpłatnie.
2. Wyślij żądanie do interfejsu API przy użyciu prawidłowego zapytania wyszukiwania.
3. Przetwórz odpowiedź interfejsu API, analizując zwrócony komunikat JSON.

## <a name="next-steps"></a>Następne kroki

* Wypróbuj [interaktywną demonstrację](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) interfejsu API wyszukiwania jednostek Bing. 
* Aby szybko rozpocząć pracę z pierwszym żądaniem, wypróbuj przewodnik [Szybki start](quickstarts/csharp.md).
* Sekcja dokumentacji [interfejsu API wyszukiwania jednostek Bing w wersji 7](/rest/api/cognitiveservices-bingsearch/bing-entities-api-v7-reference).
* [Wymagania dotyczące użycia i wyświetlania Bing](../bing-web-search/use-display-requirements.md) określają dopuszczalne zastosowania zawartości i informacji uzyskanych za pośrednictwem interfejsów API wyszukiwania Bing.
* Odwiedź [stronę centrum interfejsu API wyszukiwanie Bing](../bing-web-search/overview.md) , aby poznać inne dostępne interfejsy API.