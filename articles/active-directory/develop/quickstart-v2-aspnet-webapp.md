---
title: 'Szybki Start: Dodawanie logowania z firmą Microsoft do aplikacji sieci Web ASP.NET | Azure'
titleSuffix: Microsoft identity platform
description: W tym przewodniku szybki start dowiesz się, jak zaimplementować logowanie firmy Microsoft w aplikacji sieci Web ASP.NET za pomocą usługi OpenID Connect Connect.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 09/25/2020
ms.author: jmprieur
ms.custom: devx-track-csharp, aaddev, identityplatformtop40, scenarios:getting-started, languages:ASP.NET, contperf-fy21q1
ms.openlocfilehash: 420415cc3bc2228a104ccf054098543bf04847b0
ms.sourcegitcommit: 2dd0932ba9925b6d8e3be34822cc389cade21b0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2021
ms.locfileid: "99225769"
---
# <a name="quickstart-add-microsoft-identity-platform-sign-in-to-an-aspnet-web-app"></a>Szybki Start: Dodawanie logowania do platformy tożsamości firmy Microsoft do aplikacji sieci Web ASP.NET

W tym przewodniku szybki start pobierasz i uruchamiasz przykładowy kod, który pokazuje, jak aplikacja sieci Web ASP.NET może zalogować użytkowników z dowolnej organizacji Azure Active Directory (Azure AD). 

Zobacz [, jak działa Przykładowa](#how-the-sample-works) ilustracja.
> [!div renderon="docs"]
> ## <a name="prerequisites"></a>Wymagania wstępne
>
> * Konto platformy Azure z aktywną subskrypcją. [Utwórz konto bezpłatnie](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
> * [Visual Studio 2019](https://visualstudio.microsoft.com/vs/)
> * [.NET Framework 4.7.2 +](https://dotnet.microsoft.com/download/visual-studio-sdks)
>
> ## <a name="register-and-download-your-quickstart-app"></a>Rejestrowanie i pobieranie aplikacji Szybki start
> Istnieją dwie opcje uruchamiania aplikacji Szybki start:
> * [Ekspresowe] [Opcja 1. Zarejestrowanie i automatyczne skonfigurowanie aplikacji, a następnie pobranie przykładowego kodu](#option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample)
> * [Ręczne] [Opcja 2. Zarejestrowanie i ręczne skonfigurowanie aplikacji oraz przykładowego kodu](#option-2-register-and-manually-configure-your-application-and-code-sample)
>
> ### <a name="option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>Opcja 1. Zarejestrowanie i automatyczne skonfigurowanie aplikacji, a następnie pobranie przykładowego kodu
>
> 1. Przejdź do środowiska szybkiego startu w <a href="https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/AspNetWebAppQuickstartPage/sourceType/docs" target="_blank">Azure Portal rejestracje aplikacji <span class="docon docon-navigate-external x-hidden-focus"></span> </a> .
> 1. Wprowadź nazwę aplikacji i wybierz pozycję **Zarejestruj**.
> 1. Postępuj zgodnie z instrukcjami, aby jednym kliknięciem pobrać i automatycznie skonfigurować nową aplikację.
>
> ### <a name="option-2-register-and-manually-configure-your-application-and-code-sample"></a>Opcja 2. Zarejestrowanie i ręczne skonfigurowanie aplikacji oraz przykładowego kodu
>
> #### <a name="step-1-register-your-application"></a>Krok 1. Rejestrowanie aplikacji
> Aby ręcznie zarejestrować aplikację i dodać informacje na temat rejestracji aplikacji do rozwiązania, wykonaj następujące czynności:
>
> 1. Zaloguj się do <a href="https://portal.azure.com/" target="_blank">Azure Portal <span class="docon docon-navigate-external x-hidden-focus"></span> </a>.
> 1. Jeśli masz dostęp do wielu dzierżawców, Użyj filtru **katalogów i subskrypcji** :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false"::: w górnym menu, aby wybrać dzierżawcę, w którym chcesz zarejestrować aplikację.
> 1. Wyszukaj i wybierz pozycję **Azure Active Directory**.
> 1. W obszarze **Zarządzaj** wybierz pozycję **rejestracje aplikacji**  >  **Nowa rejestracja**.
> 1. Wprowadź **nazwę** aplikacji, na przykład `ASPNET-Quickstart` . Użytkownicy Twojej aplikacji mogą zobaczyć tę nazwę i można ją później zmienić.
> 1. Dodaj `https://localhost:44368/` w obszarze **URI przekierowania** i wybierz pozycję **zarejestruj**.
> 1. W obszarze **Zarządzaj** wybierz pozycję **uwierzytelnianie**.
> 1. W sekcji **niejawne przyznanie i przepływy hybrydowe** wybierz pozycję **identyfikatory tokenów**.
> 1. Wybierz pozycję **Zapisz**.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-1-configure-your-application-in-azure-portal"></a>Krok 1. Konfigurowanie aplikacji w witrynie Azure Portal
> Ten przykładowy kod w tym przewodniku Szybki Start wymaga **identyfikatora URI przekierowania** o wartości `https://localhost:44368/` .

> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [Wprowadź tę zmianę automatycznie]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![Already configured](media/quickstart-v2-aspnet-webapp/green-check.png) (Już skonfigurowano) Twoja aplikacja została skonfigurowana za pomocą tego atrybutu

#### <a name="step-2-download-your-project"></a>Krok 2. Pobieranie projektu

> [!div renderon="docs"]
> [Pobierz rozwiązanie Visual Studio 2019](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip)

> [!div renderon="portal" class="sxs-lookup"]
> Uruchom projekt przy użyciu programu Visual Studio 2019.
> [!div renderon="portal" id="autoupdate" class="sxs-lookup nextstepaction"]
> [Pobierz przykład kodu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip)

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-3-your-app-is-configured-and-ready-to-run"></a>Krok 3. Twoja aplikacja jest skonfigurowana i gotowa do uruchomienia
> Twój projekt został skonfigurowany z wartościami właściwości aplikacji.

> [!div renderon="docs"]
> #### <a name="step-3-run-your-visual-studio-project"></a>Krok 3. uruchamianie projektu programu Visual Studio

1. Wyodrębnij plik zip do folderu lokalnego bliższego folderowi głównemu, na przykład **C:\Azure-Samples**
1. Otwórz rozwiązanie w programie Visual Studio (AppModelv2-WebApp-OpenIDConnect-DotNet.sln)
1. W zależności od wersji programu Visual Studio, może być konieczne kliknięcie prawym przyciskiem myszy projektu `AppModelv2-WebApp-OpenIDConnect-DotNet` i **przywrócenie pakietów NuGet**
1. Otwórz konsolę Menedżera pakietów (widok-> innej konsoli Menedżera pakietów systemu Windows — >) i uruchom `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`

> [!div renderon="docs"]
> 5. Przeprowadź edycję pliku **Web.config** i zastąp parametry `ClientId` oraz `Tenant` następującymi:
>    ```xml
>    <add key="ClientId" value="Enter_the_Application_Id_here" />
>    <add key="Tenant" value="Enter_the_Tenant_Info_Here" />
>    ```
>    Gdzie:
> - `Enter_the_Application_Id_here` jest identyfikatorem dla zarejestrowanej aplikacji.
> - `Enter_the_Tenant_Info_Here` jest jedną z poniższych opcji:
>   - Jeśli aplikacja obsługuje **tylko moją organizację**, Zastąp tę wartość **identyfikatorem dzierżawy** lub **nazwą dzierżawy** (na przykład contoso.onmicrosoft.com).
>   - Jeśli aplikacja obsługuje tryb **Konta w dowolnym katalogu organizacyjnym**, zastąp tę wartość za pomocą wartości `organizations`
>   - Jeśli aplikacja obsługuje tryb **Wszyscy użytkownicy kont Microsoft**, zastąp tę wartość za pomocą wartości `common`
>
> > [!TIP]
> > - Aby znaleźć wartości *Identyfikator aplikacji*, *Identyfikator katalogu (dzierżawy)* i *Obsługiwane typy kont*, przejdź do strony **Przegląd**
> > - Upewnij się, że wartość `redirectUri` w **Web.config** odpowiada **identyfikatorowi URI przekierowania** zdefiniowanego dla rejestracji aplikacji w usłudze Azure AD (jeśli nie, przejdź do menu **uwierzytelniania** dla rejestracji aplikacji i zaktualizuj **Identyfikator URI przekierowania** , aby dopasować)

> [!div class="sxs-lookup" renderon="portal"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

## <a name="more-information"></a>Więcej informacji

Ta sekcja zawiera omówienie kodu wymaganego do logowania użytkowników. Ten przegląd może być przydatny do zrozumienia sposobu działania kodu, głównych argumentów oraz, jeśli chcesz dodać logowanie do istniejącej aplikacji ASP.NET.

### <a name="how-the-sample-works"></a>Jak działa przykład
![Pokazuje sposób działania przykładowej aplikacji wygenerowanej przez ten przewodnik Szybki Start](media/quickstart-v2-aspnet-webapp/aspnetwebapp-intro.svg)

### <a name="owin-middleware-nuget-packages"></a>Pakiety NuGet oprogramowania pośredniczącego OWIN

Potok uwierzytelniania można skonfigurować przy użyciu uwierzytelniania na podstawie plików cookie, korzystając z protokołu OpenID Connect na platformie ASP.NET wraz z pakietami oprogramowania pośredniczącego OWIN. Te pakiety można zainstalować, uruchamiając następujące polecenia w **konsoli menedżera pakietów** programu Visual Studio:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

### <a name="owin-startup-class"></a>Klasa początkowa OWIN

Oprogramowanie pośredniczące OWIN używa *klasy uruchamiania* , która jest uruchamiana podczas inicjowania procesu hostingu. W tym przewodniku szybki start plik *Startup.cs* znajduje się w folderze głównym. W poniższym kodzie przedstawiono parametr użyty w tym przewodniku Szybki start:

```csharp
public void Configuration(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());
    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            // Sets the ClientId, authority, RedirectUri as obtained from web.config
            ClientId = clientId,
            Authority = authority,
            RedirectUri = redirectUri,
            // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
            PostLogoutRedirectUri = redirectUri,
            Scope = OpenIdConnectScope.OpenIdProfile,
            // ResponseType is set to request the id_token - which contains basic information about the signed-in user
            ResponseType = OpenIdConnectResponseType.IdToken,
            // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
            // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
            // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter
            TokenValidationParameters = new TokenValidationParameters()
            {
                ValidateIssuer = false // Simplification (see note below)
            },
            // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
            Notifications = new OpenIdConnectAuthenticationNotifications
            {
                AuthenticationFailed = OnAuthenticationFailed
            }
        }
    );
}
```

> |Lokalizacja  | Opis |
> |---------|---------|
> | `ClientId`     | Identyfikator aplikacji z aplikacji zarejestrowanej w witrynie Azure Portal |
> | `Authority`    | Punkt końcowy usługi STS na potrzeby uwierzytelnienia użytkownika. Zazwyczaj jest to adres `https://login.microsoftonline.com/{tenant}/v2.0` dla chmury publicznej, gdzie parametr {tenant} jest nazwą dzierżawy, identyfikatorem dzierżawy lub ma wartość *common* na potrzeby odwołania do wspólnego punktu końcowego (używany dla aplikacji z wieloma dzierżawami) |
> | `RedirectUri`  | Adres URL, pod który użytkownicy są wysyłani po uwierzytelnieniu na platformie tożsamości firmy Microsoft |
> | `PostLogoutRedirectUri`     | Adres URL, do którego przekierowywani są użytkownicy po wylogowaniu |
> | `Scope`     | Lista zażądanych zakresów oddzielonych spacjami |
> | `ResponseType`     | Żądanie, którego odpowiedź z procesu uwierzytelniania zawiera identyfikator tokenu |
> | `TokenValidationParameters`     | Lista parametrów na potrzeby weryfikacji tokenu. W tym przypadku parametr `ValidateIssuer` ustawiono na wartość `false`, aby wskazać, że może akceptować logowania z dowolnych kont osobistych i służbowych |
> | `Notifications`     | Lista obiektów delegowanych, które mogą być wykonywane w ramach różnych komunikatów *OpenIdConnect* |


> [!NOTE]
> Ustawienie to `ValidateIssuer = false` uproszczenie dla tego przewodnika Szybki Start. W rzeczywistych aplikacjach należy sprawdzić poprawność wystawcy.
> Zapoznaj się z przykładami, aby dowiedzieć się, jak to zrobić.

### <a name="initiate-an-authentication-challenge"></a>Inicjowanie żądania uwierzytelnienia

Możesz wymusić logowanie użytkownika, wysyłając żądanie uwierzytelnienia w kontrolerze:

```csharp
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}
```

> [!TIP]
> Wysłanie żądania uwierzytelnienia przy użyciu powyższej metody jest opcjonalne i jest zwykle używane, gdy chcesz, aby widok był dostępny zarówno dla uwierzytelnionych, jak i nieuwierzytelnionych użytkowników. Innym rozwiązaniem jest ochrona kontrolerów przy użyciu metody opisanej w następnej sekcji.

### <a name="protect-a-controller-or-a-controllers-method"></a>Ochrona kontrolera lub metody kontrolera

Kontroler lub akcje kontrolera można chronić za pomocą atrybutu `[Authorize]`. Ten atrybut ogranicza dostęp do kontrolera lub akcji, zezwalając na dostęp do akcji w kontrolerze tylko uwierzytelnionym użytkownikom, co oznacza, że żądanie uwierzytelnienia zostanie wysłane automatycznie, gdy *nieuwierzytelniony* użytkownik podejmie próbę uzyskania dostępu do jednej z akcji lub kontrolera oznaczonego za pomocą atrybutu `[Authorize]`.

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>Następne kroki

Wypróbuj samouczek platformy ASP.NET, aby uzyskać instrukcje krok po kroku dotyczące tworzenia aplikacji i nowych funkcji, w tym pełne objaśnienie informacji zawartych w tym przewodniku Szybki start.

> [!div class="nextstepaction"]
> [Dodawanie logowania do aplikacji sieci Web ASP.NET](tutorial-v2-asp-webapp.md)
