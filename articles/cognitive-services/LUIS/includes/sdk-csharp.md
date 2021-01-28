---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: cognitive-services
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.date: 09/01/2020
ms.topic: include
ms.custom: include file, devx-track-dotnet, cog-serv-seo-aug-2020
ms.openlocfilehash: fd47d5df053931c343fd811fe4d93b66f080f225
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2021
ms.locfileid: "98947272"
---
Użyj bibliotek klienta Language Understanding (LUIS) dla platformy .NET, aby:
* Tworzenie aplikacji
* Dodawanie zamiaru, jednostki uczenia maszynowego z przykładem wypowiedź
* Uczenie i publikowanie aplikacji
* Środowisko uruchomieniowe przewidywania zapytania

[Dokumentacja](/dotnet/api/overview/azure/cognitiveservices/client/languageunderstanding)  |  referencyjna Kod źródłowy biblioteki [tworzenia](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/cognitiveservices/Language.LUIS.Authoring) i [przewidywania](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/cognitiveservices/Language.LUIS.Runtime) | [Tworzenie](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.LUIS.Authoring/) i [prognozowanie](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.LUIS.Runtime/) NuGet | [Przykład w języku C#](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/dotnet/LanguageUnderstanding/sdk-3x//Program.cs)

## <a name="prerequisites"></a>Wymagania wstępne

* Bieżąca wersja [platformy .NET Core](https://dotnet.microsoft.com/download/dotnet-core) i [interfejs wiersza polecenia platformy .NET Core](/dotnet/core/tools/).
* Subskrypcja platformy Azure — [Utwórz ją bezpłatnie](https://azure.microsoft.com/free/cognitive-services)
* Gdy masz subskrypcję platformy Azure, [Utwórz zasób tworzenia Language Understanding](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesLUISAllInOne) w Azure Portal, aby uzyskać klucz i punkt końcowy. Zaczekaj na jego wdrożenie i kliknij przycisk **Przejdź do zasobu** .
    * Będziesz potrzebować klucza i punktu końcowego z zasobu [, który tworzysz, aby](../luis-how-to-azure-subscription.md#create-luis-resources-in-the-azure-portal) połączyć aplikację w celu Language Understanding tworzenia. Klucz i punkt końcowy zostaną wklejone do poniższego kodu w dalszej części przewodnika Szybki Start. Aby wypróbować usługę, możesz skorzystać z warstwy cenowej bezpłatna ( `F0` ).

## <a name="setting-up"></a>Konfigurowanie

### <a name="create-a-new-c-application"></a>Utwórz nową aplikację w języku C#

Utwórz nową aplikację platformy .NET Core w preferowanym edytorze lub środowisku IDE.

1. W oknie konsoli (na przykład cmd, PowerShell lub bash) Użyj polecenia dotnet, `new` Aby utworzyć nową aplikację konsolową o nazwie `language-understanding-quickstart` . To polecenie tworzy prosty projekt C# "Hello world" z pojedynczym plikiem źródłowym: `Program.cs` .

    ```dotnetcli
    dotnet new console -n language-understanding-quickstart
    ```

1. Zmień katalog na nowo utworzony folder aplikacji.

    ```dotnetcli
    cd language-understanding-quickstart
    ```

1. Aplikację można skompilować przy użyciu:

    ```dotnetcli
    dotnet build
    ```

    Dane wyjściowe kompilacji nie powinny zawierać ostrzeżeń ani błędów.

    ```console
    ...
    Build succeeded.
     0 Warning(s)
     0 Error(s)
    ...
    ```

### <a name="install-the-nuget-libraries"></a>Instalowanie bibliotek NuGet

W katalogu aplikacji zainstaluj biblioteki klienta Language Understanding (LUIS) dla platformy .NET przy użyciu następujących poleceń:

```dotnetcli
dotnet add package Microsoft.Azure.CognitiveServices.Language.LUIS.Authoring --version 3.2.0-preview.3
dotnet add package Microsoft.Azure.CognitiveServices.Language.LUIS.Runtime --version 3.1.0-preview.1
```

## <a name="authoring-object-model"></a>Model obiektów tworzenia

Klient tworzenia Language Understanding (LUIS) to obiekt [LUISAuthoringClient](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.luisauthoringclient) , który jest uwierzytelniany na platformie Azure, który zawiera klucz tworzenia.

## <a name="code-examples-for-authoring"></a>Przykłady kodu do tworzenia

Po utworzeniu klienta Użyj tego klienta, aby uzyskać dostęp do funkcji, w tym:

* Aplikacje — [Tworzenie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.appsextensions.addasync), [usuwanie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.appsextensions.deleteasync), [Publikowanie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.appsextensions.publishasync)
* Przykład wyrażenia długości — [Dodawanie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.examplesextensions), [usuwanie według identyfikatora](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.examplesextensions.deleteasync)
* Funkcje — zarządzanie [listami fraz](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.featuresextensions.addphraselistasync)
* Model — zarządzanie [intencjami](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.modelextensions) i jednostkami
* [Wzorce — zarządzanie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.patternextensions) wzorcami
* [Uczenie](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.trainextensions.trainversionasync) aplikacji i sondowanie jej pod kątem [stanu szkolenia](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.trainextensions.getstatusasync)
* [Wersje](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.versionsextensions) — zarządzanie przy użyciu klonowania, eksportowania i usuwania

## <a name="prediction-object-model"></a>Model obiektów predykcyjnych

Klient predykcyjny w środowisku uruchomieniowym Language Understanding (LUIS) to obiekt [LUISRuntimeClient](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.luisruntimeclient) , który jest uwierzytelniany na platformie Azure, który zawiera klucz zasobu.

## <a name="code-examples-for-prediction-runtime"></a>Przykłady kodu dla środowiska uruchomieniowego przewidywania

Po utworzeniu klienta Użyj tego klienta, aby uzyskać dostęp do funkcji, w tym:

* Prognozowanie według [miejsca przejściowego lub produkcyjnego](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.predictionoperationsextensions.getslotpredictionasync)
* Prognozowanie według [wersji](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.predictionoperationsextensions.getversionpredictionasync)


[!INCLUDE [Bookmark links to same article](sdk-code-examples.md)]

## <a name="add-the-dependencies"></a>Dodawanie zależności

W katalogu projektu Otwórz plik *program.cs* w preferowanym edytorze lub w środowisku IDE. Zastąp istniejący `using` kod następującymi `using` dyrektywami:

[!code-csharp[Add NuGet libraries to code file](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=Dependencies)]

## <a name="add-boilerplate-code"></a>Dodawanie kodu standardowego

1. Zmień sygnaturę `Main` metody, aby zezwolić na wywołania asynchroniczne:

    ```csharp
    public static async Task Main()
    ```

1. Dodaj resztę kodu z `Main` metody `Program` klasy, chyba że określono inaczej.

## <a name="create-variables-for-the-app"></a>Tworzenie zmiennych dla aplikacji

Utwórz dwa zestawy zmiennych: pierwszy zestaw, który zostanie zmieniony, drugi ustawia się w taki sposób, w jaki pojawia się w przykładowym kodzie. 

1. Utwórz zmienne, aby przechowywać klucze tworzenia i nazwy zasobów.

    [!code-csharp[Variables you need to change](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=VariablesYouChange)]

1. Utwórz zmienne, aby przechowywać punkty końcowe, nazwę aplikacji, wersję i nazwę celu.

    [!code-csharp[Variables you don't need to change](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=VariablesYouDontNeedToChangeChange)]

## <a name="authenticate-the-client"></a>Uwierzytelnianie klienta

Utwórz obiekt [ApiKeyServiceClientCredentials](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.apikeyserviceclientcredentials) z kluczem i użyj go w punkcie końcowym, aby utworzyć obiekt [LUISAuthoringClient](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.luisauthoringclient) .

[!code-csharp[Authenticate the client](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AuthoringCreateClient)]

## <a name="create-a-luis-app"></a>Tworzenie aplikacji usługi LUIS

Aplikacja LUIS zawiera model przetwarzania języka naturalnego (NLP), w tym intencje, jednostki i przykład wyrażenia długości.

Utwórz element [ApplicationCreateObject](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.models.applicationcreateobject). Nazwa i kultura języka są wymagane właściwości. Wywołaj metodę [Apps. addasync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.appsextensions.addasync) . Odpowiedź jest IDENTYFIKATORem aplikacji.

[!code-csharp[Create a LUIS app](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AuthoringCreateApplication)]

## <a name="create-intent-for-the-app"></a>Utwórz cel dla aplikacji
Zamiarem jest obiekt podstawowy w modelu aplikacji LUIS. Cel jest wyrównany do grupy _zamiarów_ wypowiedź użytkownika. Użytkownik może zadać pytanie lub utworzyć instrukcję poszukującą konkretnej _zamierzonej_ odpowiedzi z bot (lub innej aplikacji klienckiej). Przykłady zamiarów polegają na rezerwacji lotu, zaproszeniu o Pogoda w miejscu docelowym i zaproszeniu o informacje kontaktowe dotyczące usługi klienta.

Utwórz [ModelCreateObject](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.models.modelcreateobject) o nazwie unikatowego zamiaru, a następnie Przekaż identyfikator aplikacji, identyfikator wersji i ModelCreateObject do metody [model. AddIntentAsync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.modelextensions.addintentasync) . Odpowiedź jest IDENTYFIKATORem intencji.

`intentName`Wartość jest trwale kodowana `OrderPizzaIntent` jako część zmiennych w sekcji [Tworzenie zmiennych dla aplikacji](#create-variables-for-the-app) .

[!code-csharp[Create intent for the app](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AddIntent)]

## <a name="create-entities-for-the-app"></a>Tworzenie jednostek dla aplikacji

Jednostki, które nie są wymagane, są dostępne w większości aplikacji. Jednostka wyodrębnia informacje z wypowiedź użytkownika, niezbędne do fullfil zamiaru użytkownika. Istnieje kilka typów [wstępnie skompilowanych](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.modelextensions.addprebuiltasync) i niestandardowych jednostek, z których każdy ma własne modele obiektów transformacji danych (DTO).  Typowe wstępnie skompilowane jednostki do dodania do aplikacji obejmują [Number](../luis-reference-prebuilt-number.md), [datetimeV2](../luis-reference-prebuilt-datetimev2.md), [geographyV2](../luis-reference-prebuilt-geographyv2.md), [porządkową](../luis-reference-prebuilt-ordinal.md).

Ważne jest, aby wiedzieć, że jednostki nie są oznaczone zamiarem. Mogą one i zwykle dotyczyć wielu intencji. Tylko przykładowe wyrażenia długości użytkownika są oznaczone dla określonego, pojedynczego zamiaru.

Metody tworzenia dla jednostek są częścią klasy [modelu](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.modelextensions) . Każdy typ jednostki ma własny model obiektów transformacji danych (DTO), zwykle zawierający wyraz `model` w przestrzeni nazw [modeli](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.models) .

Kod tworzenia jednostki tworzy jednostkę uczenia maszynowego z podjednostkami i funkcjami zastosowanymi do `Quantity` podjednostek.

:::image type="content" source="../media/quickstart-sdk/machine-learned-entity.png" alt-text="Zrzut ekranu częściowego z portalu pokazującego utworzoną jednostkę, jednostkę uczenia maszynowego z podjednostkami i funkcjami zastosowanymi do podjednostek &quot;ilooć&quot;.":::

[!code-csharp[Create entities for the app](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AuthoringAddEntities)]

Użyj następującej metody do klasy, aby znaleźć identyfikator podjednostki ilości, aby przypisać funkcje do tej podjednostki.

[!code-csharp[Find subentity id](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AuthoringSortModelObject)]

## <a name="add-example-utterance-to-intent"></a>Dodawanie przykładu wypowiedź do celu

W celu określenia zamiaru i wyodrębnienia jednostek wypowiedź aplikacja wymaga przykładów wyrażenia długości. Przykłady muszą dotyczyć określonego, pojedynczego przeznaczenie i powinny oznaczać wszystkie jednostki niestandardowe. Wstępnie skompilowane jednostki nie muszą być oznaczone.

Dodaj przykład wyrażenia długości, tworząc listę obiektów [ExampleLabelObject](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.models.examplelabelobject) , jeden obiekt dla każdego przykładu wypowiedź. Każdy przykład powinien oznaczać wszystkie jednostki ze słownikiem par nazwa-wartość nazwy jednostki i wartości jednostki. Wartość jednostki powinna być dokładnie taka, jak pojawia się w tekście przykładu wypowiedź.

:::image type="content" source="../media/quickstart-sdk/labeled-example-machine-learned-entity.png" alt-text="Zrzut ekranu przedstawiający przykład wypowiedź w portalu. ":::

Wywołaj [przykłady. addasync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.examplesextensions) z identyfikatorem aplikacji, identyfikatorem wersji i przykładem.

[!code-csharp[Add example utterance to intent](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=AuthoringAddLabeledExamples)]

## <a name="train-the-app"></a>Uczenie aplikacji

Po utworzeniu modelu aplikacja LUIS musi być przeszkolone dla tej wersji modelu. Model przeszkolony może być używany w [kontenerze](../luis-container-howto.md)lub [publikowany](../luis-how-to-publish-app.md) w gniazdach tymczasowych lub produkcyjnych.

Metoda [uczenie. TrainVersionAsync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.trainextensions) wymaga identyfikatora aplikacji i identyfikatora wersji.

Bardzo mały model, taki jak ten przewodnik Szybki Start, będzie przeszkolać się bardzo szybko. W przypadku aplikacji na poziomie produkcyjnym szkolenie aplikacji powinno obejmować wywołanie sondowania metody [GetStatusAsync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.trainextensions.getstatusasync#Microsoft_Azure_CognitiveServices_Language_LUIS_Authoring_TrainExtensions_GetStatusAsync_Microsoft_Azure_CognitiveServices_Language_LUIS_Authoring_ITrain_System_Guid_System_String_System_Threading_CancellationToken_) , aby określić, kiedy lub czy szkolenie zakończyło się pomyślnie. Odpowiedź jest listą obiektów [ModelTrainingInfo](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.models.modeltraininginfo) z osobnym stanem dla każdego obiektu. Aby szkolenie zostało uznane za ukończone, wszystkie obiekty muszą się powieść.

[!code-csharp[Train the app](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=TrainAppVersion)]

## <a name="publish-app-to-production-slot"></a>Publikowanie aplikacji w miejscu produkcyjnym

Opublikuj aplikację LUIS przy użyciu metody [PublishAsync](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring.appsextensions.publishasync) . Spowoduje to opublikowanie aktualnie przeszkolonej wersji do określonego miejsca w punkcie końcowym. Aplikacja kliencka używa tego punktu końcowego do wysyłania wyrażenia długości użytkownika w celu przewidywania założeń i wyodrębniania jednostek.

[!code-csharp[Publish app to production slot](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=PublishVersion)]

## <a name="authenticate-the-prediction-runtime-client"></a>Uwierzytelnianie klienta predykcyjnego środowiska uruchomieniowego

Użyj obiektu [ApiKeyServiceClientCredentials](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.apikeyserviceclientcredentials) z kluczem i użyj go w punkcie końcowym, aby utworzyć obiekt [LUISRuntimeClient](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.luisruntimeclient) .

[!INCLUDE [Caution about using authoring key](caution-authoring-key.md)]

[!code-csharp[Authenticate the prediction runtime client](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=PredictionCreateClient)]


## <a name="get-prediction-from-runtime"></a>Pobierz prognozowanie z środowiska uruchomieniowego

Dodaj następujący kod, aby utworzyć żądanie do środowiska uruchomieniowego predykcyjnego.

Wypowiedź użytkownika jest częścią obiektu [PredictionRequest](/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime.models.predictionrequest) .

Metoda **GetSlotPredictionAsync** wymaga kilku parametrów, takich jak identyfikator aplikacji, nazwa gniazda, obiekt żądania prognozowania w celu spełnienia żądania. Inne opcje, takie jak verbose, pokazują wszystkie intencje i dzienniki są opcjonalne.

[!code-csharp[Get prediction from runtime](~/cognitive-services-quickstart-code/dotnet/LanguageUnderstanding/sdk-3x//Program.cs?name=QueryPredictionEndpoint)]

[!INCLUDE [Prediction JSON response](sdk-json.md)]

## <a name="run-the-application"></a>Uruchamianie aplikacji

Uruchom aplikację za pomocą `dotnet run` polecenia z katalogu aplikacji.

```dotnetcli
dotnet run
```
