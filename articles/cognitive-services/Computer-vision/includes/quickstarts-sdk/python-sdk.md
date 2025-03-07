---
title: 'Szybki Start: przetwarzanie obrazówa Biblioteka kliencka dla języka Python'
description: Rozpocznij pracę z biblioteką klienta przetwarzanie obrazów dla języka Python, korzystając z tego przewodnika Szybki Start.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: include
ms.date: 12/15/2020
ms.author: pafarley
ms.openlocfilehash: 1b17173c95f26c622a0021d30eb678fc27b60c2f
ms.sourcegitcommit: 18a91f7fe1432ee09efafd5bd29a181e038cee05
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2021
ms.locfileid: "103622247"
---
<a name="HOLTop"></a>

Użyj biblioteki klienta przetwarzanie obrazów, aby:

* Analizuj obraz pod kątem tagów, opisu tekstu, twarzy, treści dla dorosłych itd.
* Odczytywanie wydrukowanych i odręcznych tekstu za pomocą interfejsu API odczytu.

[Dokumentacja](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision)  |  referencyjna [Kod](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/cognitiveservices/azure-cognitiveservices-vision-computervision)  |  źródłowy biblioteki [Pakiet (PiPy)](https://pypi.org/project/azure-cognitiveservices-vision-computervision/)  |  [Przykłady](https://azure.microsoft.com/resources/samples/?service=cognitive-services&term=vision&sort=0)

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure — [Utwórz ją bezpłatnie](https://azure.microsoft.com/free/cognitive-services/)
* [Python 3.x](https://www.python.org/)
  * Instalacja języka Python powinna obejmować [PIP](https://pip.pypa.io/en/stable/). Aby sprawdzić, czy jest zainstalowany program PIP, należy uruchomić `pip --version` polecenie w wierszu polecenia. Pobierz narzędzie PIP, instalując najnowszą wersję środowiska Python.
* Gdy masz subskrypcję platformy Azure, <a href="https://portal.azure.com/#create/Microsoft.CognitiveServicesComputerVision"  title=" Utwórz zasób przetwarzanie obrazów "  target="_blank"> utwórz zasób przetwarzanie obrazów </a> w Azure Portal, aby uzyskać klucz i punkt końcowy. Po wdrożeniu programu kliknij pozycję **Przejdź do zasobu**.

    * Będziesz potrzebować klucza i punktu końcowego z zasobu, który utworzysz, aby połączyć aplikację z usługą przetwarzanie obrazów. Klucz i punkt końcowy zostaną wklejone do poniższego kodu w dalszej części przewodnika Szybki Start.
    * Możesz użyć warstwy cenowej bezpłatna ( `F0` ) w celu wypróbowania usługi i później przeprowadzić uaktualnienie do warstwy płatnej dla środowiska produkcyjnego.

## <a name="setting-up"></a>Konfigurowanie

### <a name="install-the-client-library"></a>Zainstaluj bibliotekę kliencką

Bibliotekę kliencką można zainstalować za pomocą programu:

```console
pip install --upgrade azure-cognitiveservices-vision-computervision
```

Zainstaluj również bibliotekę Pillow.

```console
pip install pillow
```

### <a name="create-a-new-python-application"></a>Tworzenie nowej aplikacji w języku Python

> [!TIP]
> Chcesz wyświetlić cały plik kodu szybkiego startu jednocześnie? Można je znaleźć w usłudze [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ComputerVision/ComputerVisionQuickstart.py), która zawiera przykłady kodu w tym przewodniku Szybki Start.

Utwórz nowy plik Python &mdash; *QuickStart-File.py*, na przykład. Następnie otwórz go w preferowanym edytorze lub w środowisku IDE.

### <a name="find-the-subscription-key-and-endpoint"></a>Znajdowanie klucza subskrypcji i punktu końcowego

Przejdź do witryny Azure Portal. Jeśli pomyślnie wdrożono zasób przetwarzanie obrazów w sekcji **wymagania wstępne** , kliknij przycisk **Przejdź do zasobu** w obszarze **następne kroki**. Klucz subskrypcji i punkt końcowy można znaleźć na stronie **klucz zasobu i punkt końcowy** w obszarze **Zarządzanie zasobami**. 

Utwórz zmienne dla klucza subskrypcji przetwarzanie obrazów i punktu końcowego. Wklej swój klucz subskrypcji i punkt końcowy do poniższego kodu, gdzie zostało wskazane. Twój punkt końcowy przetwarzanie obrazów ma formularz `https://<your_computer_vision_resource_name>.cognitiveservices.azure.com/` .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_imports_and_vars)]

> [!IMPORTANT]
> Pamiętaj, aby usunąć klucz subskrypcji z kodu, gdy skończysz, i nigdy nie Publikuj go publicznie. W przypadku produkcji należy rozważyć użycie bezpiecznego sposobu przechowywania poświadczeń i uzyskiwania do nich dostępu. Na przykład [Magazyn kluczy platformy Azure](../../../../key-vault/general/overview.md).

> [!div class="nextstepaction"]
> [Konfiguruję klienta,](?success=set-up-client#object-model) który [uruchomił problem](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=set-up-client)

## <a name="object-model"></a>Model obiektów

Poniższe klasy i interfejsy obsługują niektóre główne funkcje zestawu SDK języka Python przetwarzanie obrazów.

|Nazwa|Opis|
|---|---|
|[ComputerVisionClientOperationsMixin](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.operations.computervisionclientoperationsmixin)| Ta klasa bezpośrednio obsługuje wszystkie operacje na obrazach, takie jak analiza obrazu, wykrywanie tekstu i generowanie miniatury.|
| [ComputerVisionClient](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionclient) | Ta klasa jest wymagana dla wszystkich funkcji przetwarzanie obrazów. Tworzysz wystąpienie z informacjami o subskrypcji i używasz ich do tworzenia wystąpień innych klas. Implementuje **ComputerVisionClientOperationsMixin**.|
|[VisualFeatureTypes](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.models.visualfeaturetypes)| To Wyliczenie definiuje różne typy analizy obrazów, które można wykonać przy użyciu standardowej operacji analizy. Należy określić zestaw wartości **VisualFeatureTypes** w zależności od potrzeb. |

## <a name="code-examples"></a>Przykłady kodu

Te fragmenty kodu przedstawiają sposób wykonywania następujących zadań za pomocą biblioteki klienta przetwarzanie obrazów dla języka Python:

* [Uwierzytelnianie klienta](#authenticate-the-client)
* [Analizowanie obrazu](#analyze-an-image)
* [Odczytaj tekst drukowany i odręczny](#read-printed-and-handwritten-text)

## <a name="authenticate-the-client"></a>Uwierzytelnianie klienta

Utwórz wystąpienie klienta z punktem końcowym i kluczem. Utwórz obiekt [CognitiveServicesCredentials](/python/api/msrest/msrest.authentication.cognitiveservicescredentials) z kluczem i użyj go w punkcie końcowym, aby utworzyć obiekt [ComputerVisionClient](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionclient) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_client)]

> [!div class="nextstepaction"]
> [Klient otrzymał uwierzytelnienie](?success=authenticate-client#analyze-an-image) [problemu](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=authenticate-client)

## <a name="analyze-an-image"></a>Analizowanie obrazu

Użyj obiektu klienckiego, aby przeanalizować funkcje wizualizacji obrazu zdalnego. Najpierw Zapisz odwołanie do adresu URL obrazu, który chcesz przeanalizować.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_remoteimage)]

> [!TIP]
> Możesz również analizować obraz lokalny. Zobacz metody [ComputerVisionClientOperationsMixin](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.operations.computervisionclientoperationsmixin) , takie jak **analyze_image_in_stream**. Lub zapoznaj się z przykładowym kodem w witrynie [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ComputerVision/ComputerVisionQuickstart.py) , aby poznać scenariusze dotyczące obrazów lokalnych.

### <a name="get-image-description"></a>Pobierz opis obrazu

Poniższy kod pobiera listę wygenerowanych napisów dla obrazu. Aby uzyskać więcej informacji, zobacz [Opis obrazów](../../concept-describing-images.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_describe)]

### <a name="get-image-category"></a>Pobierz kategorię obrazu

Poniższy kod pobiera wykrytą kategorię obrazu. Aby uzyskać więcej informacji, zobacz [kategoryzowanie obrazów](../../concept-categorizing-images.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_categorize)]

### <a name="get-image-tags"></a>Pobierz Tagi obrazu

Poniższy kod pobiera zestaw wykrytych tagów z obrazu. Aby uzyskać więcej informacji, zobacz [Tagi zawartości](../../concept-tagging-images.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_tags)]

### <a name="detect-objects"></a>Wykrywanie obiektów

Poniższy kod wykrywa typowe obiekty w obrazie i drukuje je do konsoli programu. Aby uzyskać więcej informacji, zobacz [wykrywanie obiektów](../../concept-object-detection.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_objects)]        

### <a name="detect-brands"></a>Wykrywanie marek

Poniższy kod wykrywa marki i logo firmy w obrazie i drukuje je do konsoli programu. Aby uzyskać więcej informacji, zobacz [wykrywanie marki](../../concept-brand-detection.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_brands)]

### <a name="detect-faces"></a>Wykrywanie twarzy

Poniższy kod zwraca wykryte twarze na obrazie ze współrzędnymi prostokątów i wybierz atrybuty twarzy. Aby uzyskać więcej informacji, zobacz [wykrywanie czołowe](../../concept-detecting-faces.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_faces)]

### <a name="detect-adult-racy-or-gory-content"></a>Wykrywanie zawartości dla dorosłych, erotycznej lub gorii

Poniższy kod drukuje wykryte obecność treści dla dorosłych w obrazie. Aby uzyskać więcej informacji, zobacz [erotycznej, gorii Content](../../concept-detecting-adult-content.md) .

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_adult)]

### <a name="get-image-color-scheme"></a>Pobierz schemat kolorów obrazu

Poniższy kod drukuje wykryte atrybuty koloru w obrazie, takie jak kolory dominujące i kolor akcentu. Zobacz [schematy kolorów](../../concept-detecting-color-schemes.md) , aby uzyskać więcej szczegółów.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_color)]

### <a name="get-domain-specific-content"></a>Pobieranie zawartości specyficznej dla domeny

Przetwarzanie obrazów może korzystać z wyspecjalizowanego modelu do dalszej analizy obrazów. Aby uzyskać więcej informacji, zobacz [zawartość specyficzną dla domeny](../../concept-detecting-domain-content.md) . 

Poniższy kod analizuje dane dotyczące wykrytych osobistości w obrazie.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_celebs)]

Poniższy kod analizuje dane dotyczące wykrytych punktów orientacyjnych w obrazie.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_landmarks)]

### <a name="get-the-image-type"></a>Pobierz typ obrazu

Poniższy kod drukuje informacje o typie obrazu, niezależnie od tego, &mdash; czy jest to obiekt clipart czy rysowanie liniowe.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_type)]

> [!div class="nextstepaction"]
> [Po przeanalizowaniu obrazu](?success=analyze-image#read-printed-and-handwritten-text) [pojawił się problem](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=analyze-image)

## <a name="read-printed-and-handwritten-text"></a>Odczytaj tekst drukowany i odręczny

Przetwarzanie obrazów może odczytać widoczny tekst w obrazie i przekonwertować go na strumień znaków. Należy to zrobić w dwóch częściach.

### <a name="call-the-read-api"></a>Wywoływanie interfejsu API odczytu

Najpierw użyj następującego kodu, aby wywołać metodę **Read** dla danego obrazu. Zwraca identyfikator operacji i uruchamia proces asynchroniczny w celu odczytania zawartości obrazu.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_read_call)]

> [!TIP]
> Możesz również odczytać tekst z lokalnego obrazu. Zobacz metody [ComputerVisionClientOperationsMixin](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.operations.computervisionclientoperationsmixin) , takie jak **read_in_stream**. Lub zapoznaj się z przykładowym kodem w witrynie [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ComputerVision/ComputerVisionQuickstart.py) , aby poznać scenariusze dotyczące obrazów lokalnych.

### <a name="get-read-results"></a>Pobierz wyniki odczytu

Następnie Pobierz identyfikator operacji zwrócony z wywołania **odczytu** i użyj go do wysyłania zapytań do usługi w celu uzyskania wyników operacji. Poniższy kod sprawdza operacje w okresach jednego sekundy do momentu zwrócenia wyników. Następnie program drukuje wyodrębnione dane tekstowe do konsoli programu.

[!code-python[](~/cognitive-services-quickstart-code/python/ComputerVision/ComputerVisionQuickstart.py?name=snippet_read_response)]

> [!div class="nextstepaction"]
> [Odczytaję tekst](?success=read-printed-handwritten-text#run-the-application) [, w którym wystąpił problem](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=read-printed-handwritten-text)

## <a name="run-the-application"></a>Uruchamianie aplikacji

Uruchom aplikację za pomocą `python` polecenia w pliku szybkiego startu.

```console
python quickstart-file.py
```

> [!div class="nextstepaction"]
> [Uruchomiono aplikację, której](?success=run-the-application#clean-up-resources) dotyczy [problem](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=run-the-application)

## <a name="clean-up-resources"></a>Czyszczenie zasobów

Jeśli chcesz wyczyścić i usunąć subskrypcję Cognitive Services, możesz usunąć zasób lub grupę zasobów. Usunięcie grupy zasobów spowoduje również usunięcie wszystkich skojarzonych z nią zasobów.

* [Portal](../../../cognitive-services-apis-create-account.md#clean-up-resources)
* [Interfejs wiersza polecenia platformy Azure](../../../cognitive-services-apis-create-account-cli.md#clean-up-resources)

> [!div class="nextstepaction"]
> [Wyczyszczono zasoby](?success=clean-up-resources#next-steps) [, w których wystąpił problem](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=Python&Section=clean-up-resources)

## <a name="next-steps"></a>Następne kroki

W tym przewodniku szybki start pokazano, jak używać biblioteki przetwarzanie obrazów dla języka Python do wykonywania zadań bazowych. Następnie zapoznaj się z dokumentacją referencyjną, aby dowiedzieć się więcej o bibliotece.

> [!div class="nextstepaction"]
>[Odwołanie interfejs API przetwarzania obrazów (Python)](/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision)

* [Czym jest przetwarzanie obrazów?](../../overview.md)
* Kod źródłowy tego przykładu można znaleźć w usłudze [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ComputerVision/ComputerVisionQuickstart.py).
