---
title: Integracja renderowania zdalnego z aplikacją Holographic języka C++/DirectX11
description: Wyjaśnia, jak zintegrować zdalne renderowanie z aplikacją Holographic w zwykłym języku C++/DirectX11, jak została utworzona przy użyciu Kreatora projektu programu Visual Studio
author: florianborn71
ms.author: flborn
ms.date: 05/04/2020
ms.topic: tutorial
ms.openlocfilehash: a07a8a9c50e0f71daa48f65ebf8c2e7a7f166cc5
ms.sourcegitcommit: f377ba5ebd431e8c3579445ff588da664b00b36b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/05/2021
ms.locfileid: "99594303"
---
# <a name="tutorial-integrate-remote-rendering-into-a-hololens-holographic-app"></a>Samouczek: Integrowanie zdalnego renderowania w aplikacji Holographic HoloLens

Ten samouczek zawiera następujące informacje:

> [!div class="checklist"]
>
> * Tworzenie aplikacji Holographic, którą można wdrożyć w usłudze HoloLens przy użyciu programu Visual Studio
> * Dodawanie niezbędnych fragmentów kodu i ustawień projektu w celu połączenia renderowania lokalnego z zdalnie renderowaną zawartością

Ten samouczek koncentruje się na dodawaniu niezbędnych bitów do `Holographic App` przykładu natywnego w celu połączenia renderowania lokalnego z renderowaniem zdalnym platformy Azure. Jedynym typem informacji zwrotnych o stanie w tej aplikacji jest panel wyjście debugowania w programie Visual Studio, więc zaleca się uruchomienie przykładu z poziomu programu Visual Studio. Dodawanie właściwej opinii w aplikacji wykracza poza zakres tego przykładu, ponieważ Kompilowanie dynamicznego panelu tekstu od podstaw obejmuje wiele kodowania. Dobrym punktem początkowym jest Klasa `StatusDisplay` , która jest częścią [przykładowego projektu odtwarzacza zdalnego w serwisie GitHub](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples/tree/master/player/common/Content). W rzeczywistości wersja tego samouczka w wersji wstępnej jest używa kopii lokalnej tej klasy.

> [!TIP]
> [Repozytorium przykładów ARR](https://github.com/Azure/azure-remote-rendering) zawiera wyniki tego samouczka jako projekt programu Visual Studio, który jest gotowy do użycia. Jest również wzbogacany o poprawne raportowanie błędów i stanu za pomocą klasy interfejsu użytkownika `StatusDisplay` . W ramach tego samouczka wszystkie dodatki specyficzne dla ARR są objęte zakresem `#ifdef USE_REMOTE_RENDERING`  /  `#endif` , dzięki czemu można łatwo zidentyfikować Dodatki renderowania zdalnego.

## <a name="prerequisites"></a>Wymagania wstępne

W tym samouczku są potrzebne:

* Informacje o koncie (Identyfikator konta, klucz konta, domena konta, Identyfikator subskrypcji). Jeśli nie masz konta, [Utwórz konto](../../../how-tos/create-an-account.md).
* Windows SDK 10.0.18362.0 [(Pobierz)](https://developer.microsoft.com/windows/downloads/windows-10-sdk).
* Najnowsza wersja programu Visual Studio 2019 [(Pobierz)](https://visualstudio.microsoft.com/vs/older-downloads/).
* [Visual Studio Tools dla rzeczywistości mieszanej](/windows/mixed-reality/install-the-tools). W szczególnych przypadkach następujące instalacje *obciążenia* są obowiązkowe:
  * **Programowanie aplikacji klasycznych w języku C++**
  * **Programowanie platforma uniwersalna systemu Windows (platformy UWP)**
* Szablony aplikacji rzeczywistości mieszanej systemu Windows dla programu Visual Studio [(Pobierz)](https://marketplace.visualstudio.com/items?itemName=WindowsMixedRealityteam.WindowsMixedRealityAppTemplatesVSIX).

## <a name="create-a-new-holographic-app-sample"></a>Tworzenie nowej przykładowej aplikacji Holographic

Pierwszym krokiem jest utworzenie przykładu giełdowego, który jest podstawą integracji zdalnego renderowania. Otwórz program Visual Studio i wybierz pozycję "Utwórz nowy projekt" i wyszukaj ciąg "Holographic DirectX 11 (aplikacja uniwersalna systemu Windows) (C++/WinRT)"

![Tworzenie nowego projektu](media/new-project-wizard.png)

Wpisz wybraną nazwę projektu, wybierz ścieżkę i wybierz przycisk "Utwórz".
W nowym projekcie Zmień konfigurację na **"Debug/arm64"**. Teraz powinno być możliwe skompilowanie i wdrożenie go na podłączonym urządzeniu HoloLens 2. Jeśli uruchomisz go na serwerze HoloLens, powinieneś zobaczyć obracający się moduł.

## <a name="add-remote-rendering-dependencies-through-nuget"></a>Dodawanie zależności renderowania zdalnego za poorednictwem narzędzia NuGet

Pierwszym krokiem dodawania funkcji renderowania zdalnego jest dodanie zależności po stronie klienta. Odpowiednie zależności są dostępne jako pakiet NuGet.
W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **"Zarządzaj pakietami NuGet..."** z menu kontekstowego.

W oknie dialogowym monitu Wyszukaj pakiet NuGet o nazwie **"Microsoft. Azure. RemoteRendering. cpp"**:

![Przeglądaj w poszukiwaniu pakietu NuGet](media/add-nuget.png)

i dodaj go do projektu, wybierając pakiet, a następnie naciskając przycisk "Zainstaluj".

Pakiet NuGet dodaje zależności renderowania zdalnego do projektu. W szczególności:
* Połącz z biblioteką klienta (RemoteRenderingClient. lib).
* Skonfiguruj zależności. dll.
* Ustaw poprawną ścieżkę do katalogu dołączania.

## <a name="project-preparation"></a>Przygotowanie projektu

Musimy wprowadzić niewielkie zmiany w istniejącym projekcie. Te zmiany są delikatne, ale bez konieczności renderowania zdalnego nie będzie działała.

### <a name="enable-multithread-protection-on-directx-device"></a>Włącz ochronę wielowątkowej na urządzeniu DirectX
Na `DirectX11` urządzeniu musi być włączona ochrona wielowątkowej. Aby to zmienić, Otwórz plik element deviceresources. cpp w folderze "Common" i Wstaw następujący kod na końcu funkcji `DeviceResources::CreateDeviceResources()` :

```cpp
// Enable multi thread protection as now multiple threads use the immediate context.
Microsoft::WRL::ComPtr<ID3D11Multithread> contextMultithread;
if (context.As(&contextMultithread) == S_OK)
{
    contextMultithread->SetMultithreadProtected(true);
}
```

### <a name="enable-network-capabilities-in-the-app-manifest"></a>Włączanie możliwości sieciowych w manifeście aplikacji
Możliwości sieci muszą być jawnie włączone dla wdrożonej aplikacji. Bez tej konfiguracji zapytania połączeń spowodują ostatecznie przekroczenie limitu czasu. Aby włączyć, kliknij dwukrotnie `package.appxmanifest` element w Eksploratorze rozwiązań. W następnym interfejsie użytkownika przejdź do karty **możliwości** i wybierz pozycję:
* Internet (serwer & klienta)
* Internet (klient)

![Możliwości sieci](media/appx-manifest-caps.png)


## <a name="integrate-remote-rendering"></a>Integracja renderowania zdalnego

Teraz, gdy projekt jest przygotowany, możemy zacząć od kodu. Dobrym punktem wejścia do aplikacji jest Klasa `HolographicAppMain` (plik HolographicAppMain. h/CPP), ponieważ ma ona wszystkie niezbędne punkty zaczepienia do inicjalizacji, cofnięcia inicjalizacji i renderowania.

### <a name="includes"></a>Zawiera

Zaczynamy od dodania niezbędnych dołączeń. Dodaj następujące elementy include do pliku HolographicAppMain. h:

```cpp
#include <AzureRemoteRendering.h>
```

... i te dodatkowe `include` dyrektywy do pliku HolographicAppMain. cpp:

```cpp
#include <AzureRemoteRendering.inl>
#include <RemoteRenderingExtensions.h>
#include <windows.perception.spatial.h>
```

W celu uproszczenia kodu zdefiniujemy następujący skrót przestrzeni nazw na początku pliku HolographicAppMain. h, po `include` dyrektywie:

```cpp
namespace RR = Microsoft::Azure::RemoteRendering;
```

Ten skrót jest przydatny, dlatego nie musimy pisać pełnej przestrzeni nazw wszędzie tam, gdzie nadal można rozpoznać struktury danych specyficzne dla ARR. Oczywiście możemy również użyć `using namespace...` dyrektywy.

### <a name="remote-rendering-initialization"></a>Inicjalizacja renderowania zdalnego
 
Musimy przechowywać kilka obiektów dla sesji itp. w okresie istnienia aplikacji. Okres istnienia pokrywa się z okresem istnienia `HolographicAppMain` obiektu aplikacji, więc dodajemy nasze obiekty jako elementy członkowskie do klasy `HolographicAppMain` . Następny krok polega na dodaniu następujących elementów członkowskich klasy w pliku HolographicAppMain. h:

```cpp
class HolographicAppMain
{
    ...
    // members:
    std::string m_sessionOverride;                // if we have a valid session ID, we specify it here. Otherwise a new one is created
    RR::ApiHandle<RR::RemoteRenderingClient> m_client;  // the client instance
    RR::ApiHandle<RR::RenderingSession> m_session;    // the current remote rendering session
    RR::ApiHandle<RR::RenderingConnection> m_api;       // the API instance, that is used to perform all the actions. This is just a shortcut to m_session->Connection()
    RR::ApiHandle<RR::GraphicsBindingWmrD3d11> m_graphicsBinding; // the graphics binding instance
}
```

Dobrym miejscem do wykonania rzeczywistej implementacji jest Konstruktor klasy `HolographicAppMain` . Musimy wykonać trzy typy inicjowania:
1. Jednorazowe inicjowanie systemu renderowania zdalnego
1. Tworzenie klienta (uwierzytelnianie)
1. Tworzenie sesji

Wszystkie te działania są przełączane sekwencyjnie w konstruktorze. Jednak w rzeczywistych przypadkach może być konieczne wykonanie tych czynności osobno.

Dodaj następujący kod na początku treści konstruktora w pliku HolographicAppMain. cpp:

```cpp
HolographicAppMain::HolographicAppMain(std::shared_ptr<DX::DeviceResources> const& deviceResources) :
    m_deviceResources(deviceResources)
{
    // 1. One time initialization
    {
        RR::RemoteRenderingInitialization clientInit;
        clientInit.ConnectionType = RR::ConnectionType::General;
        clientInit.GraphicsApi = RR::GraphicsApiType::WmrD3D11;
        clientInit.ToolId = "<sample name goes here>"; // <put your sample name here>
        clientInit.UnitsPerMeter = 1.0f;
        clientInit.Forward = RR::Axis::NegativeZ;
        clientInit.Right = RR::Axis::X;
        clientInit.Up = RR::Axis::Y;
        if (RR::StartupRemoteRendering(clientInit) != RR::Result::Success)
        {
            // something fundamental went wrong with the initialization
            throw std::exception("Failed to start remote rendering. Invalid client init data.");
        }
    }


    // 2. Create Client
    {
        // Users need to fill out the following with their account data and model
        RR::SessionConfiguration init;
        init.AccountId = "00000000-0000-0000-0000-000000000000";
        init.AccountKey = "<account key>";
        init.RemoteRenderingDomain = "westus2.mixedreality.azure.com"; // <change to the region that the rendering session should be created in>
        init.AccountDomain = "westus2.mixedreality.azure.com"; // <change to the region the account was created in>
        m_modelURI = "builtin://Engine";
        m_sessionOverride = ""; // If there is a valid session ID to re-use, put it here. Otherwise a new one is created
        m_client = RR::ApiHandle(RR::RemoteRenderingClient(init));
    }

    // 3. Open/create rendering session
    {
        auto SessionHandler = [&](RR::Status status, RR::ApiHandle<RR::CreateRenderingSessionResult> result)
        {
            if (status == RR::Status::OK)
            {
                auto ctx = result->GetContext();
                if (ctx.Result == RR::Result::Success)
                {
                    SetNewSession(result->GetSession());
                }
                else
                {
                    SetNewState(AppConnectionStatus::ConnectionFailed, ctx.ErrorMessage.c_str());
                }
            }
            else
            {
                SetNewState(AppConnectionStatus::ConnectionFailed, "failed");
            }
        };

        // If we had an old (valid) session that we can recycle, we call async function m_client->OpenRenderingSessionAsync
        if (!m_sessionOverride.empty())
        {
            m_client->OpenRenderingSessionAsync(m_sessionOverride, SessionHandler);
            SetNewState(AppConnectionStatus::CreatingSession, nullptr);
        }
        else
        {
            // create a new session
            RR::RenderingSessionCreationOptions init;
            init.MaxLeaseInMinutes = 10; // session is leased for 10 minutes
            init.Size = RR::RenderingSessionVmSize::Standard;
            m_client->CreateNewRenderingSessionAsync(init, SessionHandler);
            SetNewState(AppConnectionStatus::CreatingSession, nullptr);
        }
    }

    // Rest of constructor code:
    ...
}
```

Kod wywołuje funkcje członkowskie `SetNewSession` `SetNewState` , które zostaną zaimplementowane w następnym akapicie wraz z resztą kodu automatu Stanów.

Należy pamiętać, że poświadczenia są zakodowane w przykładzie i muszą zostać wypełnione w miejscu ([Identyfikator konta, klucz konta, domena konta](../../../how-tos/create-an-account.md#retrieve-the-account-information)i [domena zdalnego renderowania](../../../reference/regions.md)).

Przeprowadzamy deinicjalizację w sposób symetryczny i w odwrotnej kolejności na końcu treści destruktora:

```cpp
HolographicAppMain::~HolographicAppMain()
{
    // Existing destructor code:
    ...
    
    // Destroy session:
    if (m_session != nullptr)
    {
        m_session->Disconnect();
        m_session = nullptr;
    }

    // Destroy front end:
    m_client = nullptr;

    // One-time de-initialization:
    RR::ShutdownRemoteRendering();
}
```

## <a name="state-machine"></a>Automat Stanów

W przypadku renderowania zdalnego funkcja Key Functions do utworzenia sesji i załadowania modelu jest funkcjami asynchronicznymi. Aby to uwzględnić, potrzebujemy prostego automatu Stanów, który zasadniczo przechodzi automatycznie przez następujące stany:

*Inicjowanie — Tworzenie sesji > — > rozpoczęcia sesji > ładowanie modelu (z postępem)*

W związku z tym w następnym kroku dodamy do klasy transpozycję obsługi komputera stanu. Deklarujemy nasze własne Wyliczenie `AppConnectionStatus` dla różnych stanów, w których może znajdować się aplikacja. Jest on podobny do `RR::ConnectionStatus` , ale ma dodatkowy stan dla nieudanego połączenia.

Dodaj następujące elementy członkowskie i funkcje do deklaracji klasy:

```cpp
namespace HolographicApp
{
    // Our application's possible states:
    enum class AppConnectionStatus
    {
        Disconnected,

        CreatingSession,
        StartingSession,
        Connecting,
        Connected,

        // error state:
        ConnectionFailed,
    };

    class HolographicAppMain
    {
        ...
        // Member functions for state transition handling
        void OnConnectionStatusChanged(RR::ConnectionStatus status, RR::Result error);
        void SetNewState(AppConnectionStatus state, const char* statusMsg);
        void SetNewSession(RR::ApiHandle<RR::RenderingSession> newSession);
        void StartModelLoading();

        // Members for state handling:

        // Model loading:
        std::string m_modelURI;
        RR::ApiHandle<RR::LoadModelAsync> m_loadModelAsync;

        // Connection state machine:
        AppConnectionStatus m_currentStatus = AppConnectionStatus::Disconnected;
        std::string m_statusMsg;
        RR::Result m_connectionResult = RR::Result::Success;
        RR::Result m_modelLoadResult = RR::Result::Success;
        bool m_isConnected = false;
        bool m_sessionStarted = false;
        RR::ApiHandle<RR::SessionPropertiesAsync> m_sessionPropertiesAsync;
        bool m_modelLoadTriggered = false;
        float m_modelLoadingProgress = 0.f;
        bool m_modelLoadFinished = false;
        double m_timeAtLastRESTCall = 0;
        bool m_needsCoordinateSystemUpdate = true;
    }
```

Na stronie implementacja w pliku. cpp Dodaj następujące jednostki funkcji:

```cpp
void HolographicAppMain::StartModelLoading()
{
    m_modelLoadingProgress = 0.f;

    RR::LoadModelFromSasOptions options;
    options.ModelUri = m_modelURI.c_str();
    options.Parent = nullptr;

    // start the async model loading
    m_api->LoadModelFromSasAsync(options,
        // completed callback
        [this](RR::Status status, RR::ApiHandle<RR::LoadModelResult> result)
        {
            m_modelLoadResult = RR::StatusToResult(status);
            m_modelLoadFinished = true; // successful if m_modelLoadResult==RR::Result::Success
            char buffer[1024];
            sprintf_s(buffer, "Remote Rendering: Model loading completed. Result: %s\n", RR::ResultToString(m_modelLoadResult));
            OutputDebugStringA(buffer);
        },
        // progress update callback
            [this](float progress)
        {
            // progress callback
            m_modelLoadingProgress = progress;
            m_needsStatusUpdate = true;
        });
}



void HolographicAppMain::SetNewState(AppConnectionStatus state, const char* statusMsg)
{
    m_currentStatus = state;
    m_statusMsg = statusMsg ? statusMsg : "";

    // Some log for the VS output panel:
    const char* appStatus = nullptr;

    switch (state)
    {
        case AppConnectionStatus::Disconnected: appStatus = "Disconnected"; break;
        case AppConnectionStatus::CreatingSession: appStatus = "CreatingSession"; break;
        case AppConnectionStatus::StartingSession: appStatus = "StartingSession"; break;
        case AppConnectionStatus::Connecting: appStatus = "Connecting"; break;
        case AppConnectionStatus::Connected: appStatus = "Connected"; break;
        case AppConnectionStatus::ConnectionFailed: appStatus = "ConnectionFailed"; break;
    }

    char buffer[1024];
    sprintf_s(buffer, "Remote Rendering: New status: %s, result: %s\n", appStatus, m_statusMsg.c_str());
    OutputDebugStringA(buffer);
}

void HolographicAppMain::SetNewSession(RR::ApiHandle<RR::RenderingSession> newSession)
{
    SetNewState(AppConnectionStatus::StartingSession, nullptr);

    m_sessionStartingTime = m_timeAtLastRESTCall = m_timer.GetTotalSeconds();
    m_session = newSession;
    m_api = m_session->Connection();
    m_graphicsBinding = m_session->GetGraphicsBinding().as<RR::GraphicsBindingWmrD3d11>();
    m_session->ConnectionStatusChanged([this](auto status, auto error)
        {
            OnConnectionStatusChanged(status, error);
        });

};

void HolographicAppMain::OnConnectionStatusChanged(RR::ConnectionStatus status, RR::Result error)
{
    const char* asString = RR::ResultToString(error);
    m_connectionResult = error;

    switch (status)
    {
    case RR::ConnectionStatus::Connecting:
        SetNewState(AppConnectionStatus::Connecting, asString);
        break;
    case RR::ConnectionStatus::Connected:
        if (error == RR::Result::Success)
        {
            SetNewState(AppConnectionStatus::Connected, asString);
        }
        else
        {
            SetNewState(AppConnectionStatus::ConnectionFailed, asString);
        }
        m_modelLoadTriggered = m_modelLoadFinished = false;
        m_isConnected = error == RR::Result::Success;
        break;
    case RR::ConnectionStatus::Disconnected:
        if (error == RR::Result::Success)
        {
            SetNewState(AppConnectionStatus::Disconnected, asString);
        }
        else
        {
            SetNewState(AppConnectionStatus::ConnectionFailed, asString);
        }
        m_modelLoadTriggered = m_modelLoadFinished = false;
        m_isConnected = false;
        break;
    default:
        break;
    }
    
}
```

### <a name="per-frame-update"></a>Aktualizacja na ramkę

Konieczne jest zaktualizowanie klienta raz na cykl symulacji i wykonanie dodatkowych aktualizacji stanu. Funkcja `HolographicAppMain::Update` zapewnia dobry punkt zaczepienia dla aktualizacji dla poszczególnych ramek.

#### <a name="state-machine-update"></a>Aktualizacja automatu Stanów

Musimy sondować stan sesji i sprawdzić, czy przeszedł do `Ready` stanu. W przypadku pomyślnego nawiązania połączenia z modelem zostanie rozpoczęte ładowanie przez program `StartModelLoading` .

Dodaj następujący kod do treści funkcji `HolographicAppMain::Update` :

```cpp
// Updates the application state once per frame.
HolographicFrame HolographicAppMain::Update()
{
    if (m_session != nullptr)
    {
        // Tick the client to receive messages
        m_api->Update();

        if (!m_sessionStarted)
        {
            // Important: To avoid server-side throttling of the requests, we should call GetPropertiesAsync very infrequently:
            const double delayBetweenRESTCalls = 10.0;

            // query session status periodically until we reach 'session started'
            if (m_sessionPropertiesAsync == nullptr && m_timer.GetTotalSeconds() - m_timeAtLastRESTCall > delayBetweenRESTCalls)
            {
                m_timeAtLastRESTCall = m_timer.GetTotalSeconds();
                m_session->GetPropertiesAsync([this](RR::Status status, RR::ApiHandle<RR::RenderingSessionPropertiesResult> propertiesResult)
                    {
                        if (status == RR::Status::OK)
                        {
                            auto ctx = propertiesResult->GetContext();
                            if (ctx.Result == RR::Result::Success)
                            {
                                auto res = propertiesResult->GetSessionProperties();
                                switch (res.Status)
                                {
                                case RR::RenderingSessionStatus::Ready:
                                {
                                    // The following ConnectAsync is async, but we'll get notifications via OnConnectionStatusChanged
                                    m_sessionStarted = true;
                                    SetNewState(AppConnectionStatus::Connecting, nullptr);
                                    RR::RendererInitOptions init;
                                    init.IgnoreCertificateValidation = false;
                                    init.RenderMode = RR::ServiceRenderMode::Default;
                                    m_session->ConnectAsync(init, [](RR::Status, RR::ConnectionStatus) {});
                                }
                                break;
                                case RR::RenderingSessionStatus::Error:
                                    SetNewState(AppConnectionStatus::ConnectionFailed, "Session error");
                                    break;
                                case RR::RenderingSessionStatus::Stopped:
                                    SetNewState(AppConnectionStatus::ConnectionFailed, "Session stopped");
                                    break;
                                case RR::RenderingSessionStatus::Expired:
                                    SetNewState(AppConnectionStatus::ConnectionFailed, "Session expired");
                                    break;
                                }
                            }
                            else
                            {
                                SetNewState(AppConnectionStatus::ConnectionFailed, ctx.ErrorMessage.c_str());
                            }
                        }
                        else
                        {
                            SetNewState(AppConnectionStatus::ConnectionFailed, "Failed to retrieve session status");
                        }
                        m_sessionPropertiesQueryInProgress = false; // next try
                    });                }
            }
        }
        if (m_isConnected && !m_modelLoadTriggered)
        {
            m_modelLoadTriggered = true;
            StartModelLoading();
        }
    }

    if (m_needsCoordinateSystemUpdate && m_stationaryReferenceFrame && m_graphicsBinding)
    {
        // Set the coordinate system once. This must be called again whenever the coordinate system changes.
        winrt::com_ptr<ABI::Windows::Perception::Spatial::ISpatialCoordinateSystem> ptr{ m_stationaryReferenceFrame.CoordinateSystem().as<ABI::Windows::Perception::Spatial::ISpatialCoordinateSystem>() };
        m_graphicsBinding->UpdateUserCoordinateSystem(ptr.get());
        m_needsCoordinateSystemUpdate = false;
    }

    // Rest of the body:
    ...
}
```

#### <a name="coordinate-system-update"></a>Aktualizacja układu współrzędnych

Musimy wyrazić zgodę na użycie usługi renderowania w systemie współrzędnych. Aby uzyskać dostęp do układu współrzędnych, który ma być używany, potrzebujemy, `m_stationaryReferenceFrame` aby został utworzony na końcu funkcji `HolographicAppMain::OnHolographicDisplayIsAvailableChanged` .

Ten system współrzędnych zazwyczaj nie zmienia się, więc jest to jednorazowe inicjowanie. Należy ją ponownie wywołać, jeśli aplikacja zmieni układ współrzędnych.

Powyższy kod ustawia układ współrzędnych w ramach `Update` funkcji tak szybko, jak tylko firma Microsoft ma układ współrzędnych i połączonej sesji.

#### <a name="camera-update"></a>Aktualizacja aparatu

Musimy zaktualizować płaszczyzny przycinania kamer, aby kamera serwera była synchronizowana z lokalnym aparatem. Można to zrobić na bardzo końcu `Update` funkcji:

```cpp
    ...
    if (m_isConnected)
    {
        // Any near/far plane values of your choosing.
        constexpr float fNear = 0.1f;
        constexpr float fFar = 10.0f;
        for (HolographicCameraPose const& cameraPose : prediction.CameraPoses())
        {
            // Set near and far to the holographic camera as normal
            cameraPose.HolographicCamera().SetNearPlaneDistance(fNear);
            cameraPose.HolographicCamera().SetFarPlaneDistance(fFar);
        }

        // The API to inform the server always requires near < far. Depth buffer data will be converted locally to match what is set on the HolographicCamera.
        auto settings = m_api->GetCameraSettings();
        settings->SetNearAndFarPlane(std::min(fNear, fFar), std::max(fNear, fFar));
        settings->SetEnableDepth(true);
    }

    // The holographic frame will be used to get up-to-date view and projection matrices and
    // to present the swap chain.
    return holographicFrame;
}

```

### <a name="rendering"></a>Renderowanie

Ostatnim krokiem jest wywołanie renderowania zawartości zdalnej. Musimy to wywołać w dokładnej pozycji w potoku renderowania, po usunięciu elementu docelowego renderowania i ustawieniu okienka ekranu. Wstaw następujący fragment kodu do `UseHolographicCameraResources` blokady wewnątrz funkcji `HolographicAppMain::Render` :

```cpp
        ...
        // Existing clear function:
        context->ClearDepthStencilView(depthStencilView, D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);
        
        // ...

        // Existing check to test for valid camera:
        bool cameraActive = pCameraResources->AttachViewProjectionBuffer(m_deviceResources);


        // Inject remote rendering: as soon as we are connected, start blitting the remote frame.
        // We do the blitting after the Clear, and before cube rendering.
        if (m_isConnected && cameraActive)
        {
            m_graphicsBinding->BlitRemoteFrame();
        }

        ...
```

## <a name="run-the-sample"></a>Uruchamianie aplikacji przykładowej

Próbka powinna teraz znajdować się w stanie, w którym kompiluje i uruchamia.

Po poprawnym uruchomieniu przykładu jest on widoczny bezpośrednio od siebie, a po utworzeniu sesji i załadowaniu modelu jest renderowany model aparatu znajdujący się w bieżącym położeniu. Tworzenie sesji i ładowanie modelu mogą trwać do kilku minut. Bieżący stan jest zapisany tylko w panelu Wyjście programu Visual Studio. Dlatego zaleca się uruchomienie przykładu z poziomu programu Visual Studio.

> [!CAUTION]
> Klient rozłącza połączenie z serwerem, gdy funkcja Tick nie jest wywoływana przez kilka sekund. Dlatego wyzwalanie punktów przerwania może łatwo spowodować odłączenie aplikacji.

Aby wyświetlić informacje o odpowiednim stanie w panelu tekstu, zapoznaj się z wersją zainstalowaną w ramach tego samouczka w witrynie GitHub.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono wszystkie kroki niezbędne do dodania zdalnego renderowania do przykładowej **aplikacji Holographic** C++/DirectX11.
Aby przekonwertować własny model, zapoznaj się z następującym przewodnikiem Szybki Start:

> [!div class="nextstepaction"]
> [Szybki start: Konwertowanie modelu do renderowania](../../../quickstarts/convert-model.md)