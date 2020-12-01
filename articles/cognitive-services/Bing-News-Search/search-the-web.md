---
title: Co to jest interfejs API wyszukiwania wiadomości Bing?
titleSuffix: Azure Cognitive Services
description: Dowiedz się, jak używać interfejs API wyszukiwania wiadomości Bing, aby wyszukać w Internecie bieżące nagłówki w różnych kategoriach, w tym o nagłówkach i tematach trendów.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-news-search
ms.topic: overview
ms.date: 12/18/2019
ms.author: scottwhi
ms.custom: seodec2018
ms.openlocfilehash: c6fad3a006d2f3da74638e0680d6ba65f736ab7b
ms.sourcegitcommit: 9eda79ea41c60d58a4ceab63d424d6866b38b82d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2020
ms.locfileid: "96351235"
---
# <a name="what-is-the-bing-news-search-api"></a>Co to jest interfejs API wyszukiwania wiadomości Bing?

> [!WARNING]
> Interfejsy API wyszukiwania Bing są przenoszone z Cognitive Services do usług Wyszukiwanie Bing. Od **30 października 2020** wszystkie nowe wystąpienia wyszukiwanie Bing muszą być obsługiwane zgodnie z procesem opisanym [tutaj](/bing/search-apis/bing-web-search/create-bing-search-service-resource).
> Interfejsy API wyszukiwania Bing obsługa administracyjna przy użyciu Cognitive Services będzie obsługiwana przez kolejne trzy lata lub do końca Umowa Enterprise, w zależności od tego, co nastąpi wcześniej.
> Instrukcje dotyczące migracji znajdują się w temacie [wyszukiwanie Bing Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource).

Interfejs API wyszukiwania wiadomości Bing umożliwia łatwą integrację możliwości poznawczego wyszukiwania wiadomości w usłudze Bing z aplikacjami. Interfejs API udostępnia podobne środowisko jak witryna [Wiadomości Bing](https://www.bing.com/news), umożliwiając wysyłanie zapytań wyszukiwania i odbieranie odpowiadających artykułów z wiadomościami.

Należy pamiętać, że interfejs API wyszukiwania wiadomości Bing udostępnia tylko wyniki wyszukiwania wiadomości. Użyj [interfejsu API wyszukiwania w Internecie Bing](../bing-web-search/overview.md), [interfejsu API wyszukiwania wideo](../bing-video-search/overview.md) i [interfejsu API wyszukiwania obrazów](../bing-image-search/overview.md) dla innych typów zawartości internetowej.

## <a name="bing-news-search-api-features"></a>Funkcje interfejsu API wyszukiwania wiadomości Bing

O ile interfejs API wyszukiwania wiadomości Bing umożliwia przede wszystkim wyszukiwanie artykułów z wiadomościami i zwraca je, to udostępnia także kilka funkcji inteligentnego i ukierunkowanego pobierania wiadomości w Internecie.

|Cechy  |Opis  |
|---------|---------|
|[Sugerowanie i używanie terminów wyszukiwania](concepts/search-for-news.md#suggest-and-use-search-terms)     | Ulepsz środowisko wyszukiwania przy użyciu [interfejsu API automatycznego sugerowania Bing](../bing-autosuggest/get-suggested-search-terms.md), aby wyświetlać sugerowane terminy wyszukiwania w miarę ich wpisywania.         |
|[Uzyskiwanie wiadomości ogólnych](concepts/search-for-news.md#get-general-news)     | Wyszukiwanie wiadomości przez wysłanie zapytania wyszukiwania do interfejsu API wyszukiwania wiadomości Bing i pobieranie w odpowiedzi listy odpowiadających artykułów z wiadomościami.           |
|[Dzisiejsze najważniejsze wiadomości](concepts/search-for-news.md#get-todays-top-news)      | Uzyskiwanie najważniejszych wiadomości z wszystkich kategorii dla bieżącego dnia.       |
|[Wiadomości według kategorii](concepts/search-for-news.md)     | Wyszukiwanie wiadomości w określonych kategoriach.        | 
|[Nagłówki](concepts/search-for-news.md)     | Wyszukiwanie najważniejszych nagłówków we wszystkich kategoriach.         |

## <a name="workflow"></a>Przepływ pracy

Interfejs API wyszukiwania wiadomości Bing jest usługą internetową RESTful łatwą do wywołania z dowolnego języka programowania, który może wysyłać żądania HTTP i analizować kod JSON. Możesz użyć tej usługi za pomocą interfejsu API REST lub zestawu SDK.

1. Utwórz [konto interfejsu API usług Cognitive Services](../cognitive-services-apis-create-account.md) z dostępem do interfejsów API wyszukiwania Bing. Jeśli nie masz subskrypcji platformy Azure, możesz [utworzyć konto](https://azure.microsoft.com/free/cognitive-services/) bezpłatnie.
2. Wyślij żądanie do interfejsu API przy użyciu prawidłowego zapytania wyszukiwania.
3. Przetwórz odpowiedź interfejsu API, analizując zwrócony komunikat JSON.

## <a name="next-steps"></a>Następne kroki

Najpierw wypróbuj [interaktywną demonstrację](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) interfejsu API wyszukiwania wiadomości Bing. Ta demonstracja pokazuje, jak można szybko dostosować zapytanie wyszukiwania i wyszukać wiadomości w Internecie.

Aby szybko rozpocząć pracę z pierwszym żądaniem interfejsu API, wypróbuj przewodnik Szybki start dla [interfejsu API REST](./csharp.md) lub jednego z [zestawów SDK](./quickstarts/client-libraries.md?pivots=programming-language-csharp).

## <a name="see-also"></a>Zobacz też

* Sekcja dokumentacji [interfejsu API wyszukiwania wiadomości Bing w wersji 7](/rest/api/cognitiveservices-bingsearch/bing-news-api-v7-reference) zawiera definicje i informacje dotyczące punktów końcowych, nagłówków, odpowiedzi interfejsu API i parametrów zapytania, których możesz użyć do żądania wyników wyszukiwania na podstawie obrazu.
* [Wymagania dotyczące użycia i wyświetlania Bing](../bing-web-search/use-display-requirements.md) określają dopuszczalne zastosowania zawartości i informacji uzyskanych za pośrednictwem interfejsów API wyszukiwania Bing.
* Odwiedź [stronę centrum interfejsu API wyszukiwanie Bing](../bing-web-search/overview.md) , aby poznać inne dostępne interfejsy API.