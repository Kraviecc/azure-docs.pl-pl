---
title: Co to jest interfejs API wyszukiwania niestandardowego Bing?
titleSuffix: Azure Cognitive Services
description: Interfejs API wyszukiwania niestandardowego Bing umożliwia tworzenie dostosowanych funkcji wyszukiwania dla interesujących Cię tematów.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-custom-search
ms.topic: overview
ms.date: 12/18/2019
ms.author: aahi
ms.openlocfilehash: e70d4d83fcd9641fa86f013688b5a3a6e3652919
ms.sourcegitcommit: 9eda79ea41c60d58a4ceab63d424d6866b38b82d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2020
ms.locfileid: "96338405"
---
# <a name="what-is-the-bing-custom-search-api"></a>Co to jest interfejs API wyszukiwania niestandardowego Bing?

> [!WARNING]
> Interfejsy API wyszukiwania Bing są przenoszone z Cognitive Services do usług Wyszukiwanie Bing. Od **30 października 2020** wszystkie nowe wystąpienia wyszukiwanie Bing muszą być obsługiwane zgodnie z procesem opisanym [tutaj](/bing/search-apis/bing-web-search/create-bing-search-service-resource).
> Interfejsy API wyszukiwania Bing obsługa administracyjna przy użyciu Cognitive Services będzie obsługiwana przez kolejne trzy lata lub do końca Umowa Enterprise, w zależności od tego, co nastąpi wcześniej.
> Instrukcje dotyczące migracji znajdują się w temacie [wyszukiwanie Bing Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource).

Interfejs API wyszukiwania niestandardowego Bing umożliwia tworzenie dostosowanych funkcji wyszukiwania dla interesujących Cię tematów bez wyświetlania reklam. Możesz określać domeny i strony internetowe do wyszukiwania w usłudze Bing, a także przypinać, podnosić lub obniżać określoną zawartość, aby tworzyć niestandardowe widoki internetowe i ułatwiać użytkownikom szybkie znajdowanie odpowiednich wyników wyszukiwania. 

## <a name="features"></a>Funkcje

|Cechy  |Opis  |
|---------|---------|
|[Sugestie dotyczące wyszukiwania niestandardowego w czasie rzeczywistym](define-custom-suggestions.md)     | Podaj sugestie dotyczące wyszukiwania, które mogą być wyświetlane jako lista rozwijana podczas wpisywania przez użytkowników.       | 
|[Środowiska niestandardowego wyszukiwania obrazów](get-images-from-instance.md)     | Pozwól użytkownikom wyszukiwać obrazy z domen i witryn internetowych określonych w Twoim wystąpieniu wyszukiwania niestandardowego.        |        
|[Środowiska niestandardowego wyszukiwania wideo](get-videos-from-instance.md)     | Pozwól użytkownikom wyszukiwać filmy wideo z domen i witryn określonych w Twoim wystąpieniu wyszukiwania niestandardowego.        |    
|[Udostępnianie wystąpienia wyszukiwania niestandardowego](share-your-custom-search.md)     | Edytuj i testuj wystąpienie wyszukiwania zespołowo, udostępniając je członkom Twojego zespołu.        | 
|[Konfigurowanie interfejsu użytkownika dla aplikacji i witryn internetowych](hosted-ui.md)     | Udostępnia hostowany interfejs użytkownika, który można łatwo zintegrować ze stronami sieci Web i aplikacjami internetowymi jako fragment kodu JavaScript.        | 
## <a name="workflow"></a>Przepływ pracy

Używając [portalu wyszukiwania niestandardowego Bing](https://customsearch.ai), możesz utworzyć wystąpienie wyszukiwania dostosowanego. Portal umożliwia utworzenie wystąpienia wyszukiwania niestandardowego, określającego domeny, witryny i strony internetowe, które będą lub nie będą przeszukiwane przez usługę Bing. Portal umożliwia również: wyświetlanie podglądu środowiska wyszukiwania, dostosowywanie rankingów wyszukiwania udostępnianych przez interfejs API oraz opcjonalnie konfigurowanie interfejsu użytkownika z możliwością wyszukiwania, aby można było renderować go w Twoich witrynach internetowych i aplikacjach.

Po utworzeniu wystąpienia wyszukiwania możesz zintegrować je (opcjonalnie także interfejs użytkownika) z witryną internetową lub aplikacją, wywołując interfejs API wyszukiwania niestandardowego Bing:

![Obraz pokazujący, że możesz nawiązać połączenie z wyszukiwaniem niestandardowym Bing za pośrednictwem interfejsu API](media/BCS-Overview.png "Jak działa wyszukiwanie niestandardowe Bing.")


## <a name="next-steps"></a>Następne kroki

Aby szybko rozpocząć pracę, zobacz [Tworzenie pierwszego wystąpienia usługi wyszukiwania niestandardowego Bing](quick-start.md).

Aby uzyskać szczegółowe informacje na temat dostosowywania wystąpienia wyszukiwania, zobacz [Define a custom search instance (Definiowanie wystąpienia wyszukiwania niestandardowego)](define-your-custom-view.md).

Pamiętaj o przeczytaniu [wymagań dotyczących używania i wyświetlania usługi Bing](../bing-web-search/use-display-requirements.md) w celu korzystania z wyników wyszukiwania w Twoich usługach i aplikacjach.

Odwiedź [stronę centrum interfejsu API wyszukiwanie Bing](../bing-web-search/overview.md) , aby poznać inne dostępne interfejsy API.

Zapoznaj się z dokumentacją poszczególnych punktów końcowych wyszukiwania niestandardowego. Dokumentacja zawiera listę punktów końcowych, nagłówków i parametrów zapytań, które są stosowane w żądaniach wyników wyszukiwania. Zawiera także definicje obiektów odpowiedzi.

[!INCLUDE [cognitive-services-bing-url-note](../../../includes/cognitive-services-bing-url-note.md)]

- [Interfejs API wyszukiwania niestandardowego](/rest/api/cognitiveservices-bingsearch/bing-custom-search-api-v7-reference)
- [Interfejs API wyszukiwania niestandardowego obrazów](/rest/api/cognitiveservices-bingsearch/bing-custom-images-api-v7-reference)
- [Niestandardowy interfejs API wideo](/rest/api/cognitiveservices-bingsearch/bing-custom-videos-api-v7-reference)
- [Interfejs API niestandardowego automatycznego sugerowania](/rest/api/cognitiveservices-bingsearch/bing-custom-autosuggest-api-v7-reference)