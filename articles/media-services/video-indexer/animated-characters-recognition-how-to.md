---
title: Wykrywanie znaków animowanych za pomocą Video Indexer jak
titleSuffix: Azure Media Services
description: W tym artykule przedstawiono sposób korzystania z wykrywania animowanych znaków w Video Indexer.
services: media-services
author: Juliako
manager: femila
ms.service: media-services
ms.subservice: video-indexer
ms.custom: references_regions
ms.topic: how-to
ms.date: 12/07/2020
ms.author: juliako
ms.openlocfilehash: 9effac182acdea6fcb41ed26faf6c2f6535a5cbf
ms.sourcegitcommit: 80c1056113a9d65b6db69c06ca79fa531b9e3a00
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "96906169"
---
# <a name="use-the-animated-character-detection-preview-with-portal-and-api"></a>Używanie wykrywania znaków animowanych (wersja zapoznawcza) z portalem i interfejsem API 

Azure Media Services Video Indexer obsługuje wykrywanie, grupowanie i rozpoznawanie znaków w animowanej zawartości, ta funkcja jest dostępna w Azure Portal i za pomocą interfejsu API. Zapoznaj się z tym tematem [przeglądu](animated-characters-recognition.md) .

W tym artykule pokazano, jak używać wykrywania animowanych znaków z Azure Portal i Video Indexer API.

## <a name="use-the-animated-character-detection-with-portal"></a>Używanie wykrywania animowanych znaków z portalem 

W tej sekcji opisano kroki, które należy wykonać, aby rozpocząć korzystanie z modelu wykrywania animowanych znaków. 

Ze względu na to, że na kontach wersji próbnej integracja Custom Vision jest zarządzana przez Video Indexer, możesz rozpocząć tworzenie i Używanie modelu "animowane znaki" i pominąć następującą sekcję ("Łączenie konta Custom Vision").

### <a name="connect-your-custom-vision-account-paid-accounts-only"></a>Połącz konto Custom Vision (tylko płatne konta)

Jeśli masz konto płatne Video Indexer, musisz najpierw połączyć konto Custom Vision. Jeśli nie masz już konta Custom Vision, utwórz je. Aby uzyskać więcej informacji, zobacz [Custom Vision](../../cognitive-services/custom-vision-service/overview.md).

> [!NOTE]
> Oba konta muszą znajdować się w tym samym regionie. Integracja Custom Vision nie jest obecnie obsługiwana w regionie Japonii.

#### <a name="connect-a-custom-vision-account-with-api"></a>Łączenie konta Custom Vision z interfejsem API 

Wykonaj następujące kroki, aby nawiązać połączenie z Custom Vision kontem Video Indexer lub zmienić konto Custom Vision, które jest obecnie połączone z Video Indexer:

1. Przejdź do [www.customvision.AI](https://www.customvision.ai) i zaloguj się.
1. Skopiuj następujące klucze: 

    * Klucz szkoleniowy (dla zasobu szkoleniowego)
    * Klucz predykcyjny (dla zasobu predykcyjnego)
    * Punkt końcowy 
    * Identyfikator zasobu predykcyjnego
    
    > [!NOTE]
    > Aby zapewnić wszystkie klucze, musisz mieć dwa oddzielne zasoby w Custom Vision, jeden do szkolenia i jeden do prognozowania.
1. Przeglądaj i zaloguj się do [Video Indexer](https://vi.microsoft.com/).
1. Kliknij znak zapytania w prawym górnym rogu strony i wybierz pozycję **odwołanie do interfejsu API**.
1. Upewnij się, że masz subskrypcję API Management, klikając pozycję Karta **produkty** . Jeśli masz podłączony interfejs API, możesz przejść do następnego kroku, w przeciwnym razie subskrybować. 
1. W portalu dla deweloperów kliknij **kompletne odwołanie do interfejsu API** i przejdź do **operacji**.  
1. Wybierz pozycję **połącz Custom Vision konto (wersja ZApoznawcza)** , a następnie kliknij przycisk **Wypróbuj**.
1. Wypełnij pola wymagane oraz token dostępu i kliknij przycisk **Wyślij**. 

    Aby uzyskać więcej informacji na temat uzyskiwania Video Indexer tokenu dostępu, przejdź do [portalu dla deweloperów](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-Account-Access-Token?)i zapoznaj się z [odpowiednią dokumentacją](video-indexer-use-apis.md#obtain-access-token-using-the-authorization-api).  
1. Gdy wywołanie zwróci odpowiedź 200 OK, Twoje konto jest połączone.
1. Aby zweryfikować połączenie, przejdź do portalu [Video Indexer](https://vi.microsoft.com/)):
1. Kliknij przycisk **dostosowywania modelu zawartości** w prawym górnym rogu.
1. Przejdź do karty **animowane znaki** .
1. Po kliknięciu przycisku Zarządzaj modelami w Custom Vision "* * nastąpi przeniesienie do konta Custom Vision, które właśnie zostało połączone.

> [!NOTE]
> Obecnie obsługiwane są tylko modele, które zostały utworzone za pośrednictwem Video Indexer. Modele tworzone za poorednictwem Custom Vision nie będą dostępne. Najlepszym rozwiązaniem jest edycja modeli, które zostały utworzone za pomocą Video Indexer tylko za pomocą platformy Video Indexer, ponieważ zmiany wprowadzone przez Custom Vision mogą spowodować niezamierzone wyniki.

### <a name="create-an-animated-characters-model"></a>Utwórz model znaków animowanych

1. Przejdź do witryny internetowej [Video Indexer](https://vi.microsoft.com/) i zaloguj się.
1. Kliknij przycisk dostosowywania modelu zawartości w prawym górnym rogu strony.

    ![Zrzut ekranu przedstawiający stronę "Video Indexer" z przyciskiem "Dostosowywanie modelu zawartości" wybraną w prawym górnym rogu.](./media/animated-characters-recognition/content-model-customization.png)
1. Przejdź do karty **animowane znaki** w sekcji Dostosowywanie modelu.
1. Kliknij pozycję **Dodaj model**.
1. Nazwij model i kliknij przycisk ENTER, aby zapisać nazwę.

> [!NOTE]
> Najlepszym rozwiązaniem jest posiadanie jednego niestandardowego modelu obsługi dla każdej z nich. 

### <a name="index-a-video-with-an-animated-model"></a>Indeksowanie wideo przy użyciu modelu animowanego

1. Kliknij przycisk **Przekaż** w górnym menu.
1. Wybierz wideo do przekazania (z pliku lub adresu URL).
1. Kliknij pozycję **Opcje zaawansowane**.
1. W obszarze **osoby/animowane znaki** wybierz pozycję **modele animacji**.
1. Jeśli masz jeden model, zostanie wybrany automatycznie i jeśli masz wiele modeli, możesz wybrać odpowiednią opcję z menu rozwijanego.
1. Kliknij pozycję Przekaż.
1. Po indeksowaniu wideo zobaczysz wykryte znaki w sekcji **animowane znaki** w okienku **Insights (szczegółowe informacje** ).

> [!NOTE] 
> Przed znakowaniem i uczeniem modelu wszystkie animowane znaki będą nazwane "nieznany #X". Po przeprowadzeniu szkolenia model zostanie również rozpoznany.

### <a name="customize-the-animated-characters-models"></a>Dostosuj modele znaków animowanych

1. Oznacz i Przeszkol model.

    1. Oznacz wykryty znak, edytując jego nazwę. Gdy znak jest przeszkolony do modelu, zostanie rozpoznany jako następne wideo indeksowane z tym modelem. 
    1. Aby oznaczyć animowany znak w filmie wideo, przejdź do karty **szczegółowe informacje** i kliknij przycisk **Edytuj** w prawym górnym rogu okna.
    1. W okienku **szczegółowe informacje** kliknij dowolny z wykrytych animowanych znaków i zmień ich nazwy z "nieznane #X" (lub nazwę, która została wcześniej przypisana do znaku).
    1. Po wpisaniu nowej nazwy kliknij ikonę wyboru obok nowej nazwy. Spowoduje to zapisanie nowej nazwy w modelu w Video Indexer.
    1. Po zakończeniu edycji wszystkich żądanych nazw musisz nauczyć się modelu.

        Otwórz stronę Dostosowywanie i kliknij kartę **animowane znaki** , a następnie kliknij przycisk **uczenie** , aby nauczyć model.
         
        Jeśli masz płatne konto, możesz kliknąć link **Zarządzaj modelami w programie Customer Vision** (jak pokazano poniżej). Następnie zostanie przekierowany do strony modelu w **Custom Vision**.
 
        ![Dostosowywanie modelu zawartości](./media/animated-characters-recognition/content-model-customization-tab.png)

     1. Po przeszkoleniu wszystkie filmy wideo, które będą indeksowane lub ponownego indeksowania przy użyciu tego modelu, będą rozpoznawać przeszkolone znaki. 
    Płatne konta, które mają dostęp do konta Custom Vision, mogą zobaczyć modele i obrazy otagowane. Dowiedz się więcej o [ulepszaniu klasyfikatora w Custom Vision](../../cognitive-services/custom-vision-service/getting-started-improving-your-classifier.md).

1. Usuń animowany znak.

    1. Aby usunąć animowany znak z wglądu w dane wideo, przejdź do karty **szczegółowe informacje** i kliknij przycisk **Edytuj** w prawym górnym rogu okna.
    1. Wybierz animowany znak, a następnie kliknij przycisk **Usuń** w obszarze ich nazwy.

    > [!NOTE]
    > Spowoduje to usunięcie szczegółowych informacji z tego wideo, ale nie wpłynie na model.

1. Usuń model.

    1. Kliknij przycisk **dostosowania modelu zawartości** w górnym menu i przejdź do karty **animowane znaki** .
    1. Kliknij ikonę wielokropka po prawej stronie modelu, który chcesz usunąć, a następnie na przycisku Usuń.
    
    * Płatne konto: model zostanie odłączony od Video Indexer i nie będzie można go ponownie połączyć.
    * Konto wersji próbnej: model zostanie również usunięty z wizji celnej. 
    
        > [!NOTE]
        > W ramach konta próbnego masz tylko jeden model, którego można użyć. Po jego usunięciu nie można szkolić innych modeli.

## <a name="use-the-animated-character-detection-with-api"></a>Używanie wykrywania animowanych znaków z interfejsem API 

1. Połącz konto Custom Vision.

    Jeśli masz konto płatne Video Indexer, musisz najpierw połączyć konto Custom Vision. <br/>
    Jeśli nie masz już konta Custom Vision, utwórz je. Aby uzyskać więcej informacji, zobacz [Custom Vision](../../cognitive-services/custom-vision-service/overview.md).

    [Połącz konto Custom Vision przy użyciu interfejsu API](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Connect-Custom-Vision-Account?tags=&pattern=&groupBy=tag).
1. Utwórz model animowanych znaków.

    Użyj interfejsu API [tworzenia modelu animacji](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Create-Animation-Model?&groupBy=tag) .
1. Indeksuj lub ponownie Indeksuj wideo.

    Użyj interfejsu API [ponownego indeksowania](https://api-portal.videoindexer.ai/docs/services/operations/operations/Re-Index-Video?) . 
1. Dostosuj modele znaków animowanych.

    Użyj interfejsu API [modelu animacji uczenia](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Train-Animation-Model?&groupBy=tag) .

### <a name="view-the-output"></a>Wyświetlanie danych wyjściowych

Zobacz animowane znaki w wygenerowanym pliku JSON.

```json
"animatedCharacters": [
    {
    "videoId": "e867214582",
    "confidence": 0,
    "thumbnailId": "00000000-0000-0000-0000-000000000000",
    "seenDuration": 201.5,
    "seenDurationRatio": 0.3175,
    "isKnownCharacter": true,
    "id": 4,
    "name": "Bunny",
    "appearances": [
        {
            "startTime": "0:00:52.333",
            "endTime": "0:02:02.6",
            "startSeconds": 52.3,
            "endSeconds": 122.6
        },
        {
            "startTime": "0:02:40.633",
            "endTime": "0:03:16.6",
            "startSeconds": 160.6,
            "endSeconds": 196.6
        },
    ]
    },
]
```

## <a name="limitations"></a>Ograniczenia

* Obecnie funkcja "Identyfikacja animacji" nie jest obsługiwana w regionie East-Asia.
* Znaki, które wydaje się być małe lub daleko w wideo, mogą nie być poprawnie identyfikowane, jeśli jakość wideo jest niska.
* Zalecenie polega na użyciu modelu na zestaw animowanych znaków (na przykład dla serii animowanej).

## <a name="next-steps"></a>Następne kroki

[Omówienie usługi Video Indexer](video-indexer-overview.md)
