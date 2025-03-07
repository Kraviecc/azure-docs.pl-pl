---
title: 'Samouczek Azure Active Directory: integracja logowania jednokrotnego (SSO) z usługą Kendis — integracja z usługą Azure AD | Microsoft Docs'
description: Dowiedz się, jak skonfigurować Logowanie jednokrotne między Azure Active Directory Kendis i integracją z usługą Azure AD.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/04/2021
ms.author: jeedes
ms.openlocfilehash: 8409a4d897ea9b20528a5b30273819e6962774cb
ms.sourcegitcommit: 24a12d4692c4a4c97f6e31a5fbda971695c4cd68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2021
ms.locfileid: "102184495"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-kendis---azure-ad-integration"></a>Samouczek Azure Active Directory: integracja logowania jednokrotnego (SSO) z usługą Kendis — integracja z usługą Azure AD

W tym samouczku dowiesz się, jak zintegrować integrację usługi Kendis z usługą Azure AD z usługą Azure Active Directory (Azure AD). Po zintegrowaniu integracji usługi Kendis z usługą Azure AD z usługą Azure AD można:

* Kontrolka w usłudze Azure AD, która ma dostęp do integracji usługi Azure AD Kendis.
* Zezwól użytkownikom na automatyczne logowanie do integracji usługi Kendis z usługą Azure AD przy użyciu kont usługi Azure AD.
* Zarządzaj kontami w jednej centralnej lokalizacji — Azure Portal.

## <a name="prerequisites"></a>Wymagania wstępne

Aby rozpocząć, potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz subskrypcji, możesz uzyskać [bezpłatne konto](https://azure.microsoft.com/free/).
* Kendis — subskrypcja z włączonym logowaniem jednokrotnym (SSO) w usłudze Azure AD.

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i testujesz Logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Kendis — integracja z usługą Azure AD obsługuje usługę **SP i dostawcy tożsamości** zainicjowano Logowanie jednokrotne
* Kendis — integracja z usługą Azure AD obsługuje funkcję aprowizacji użytkowników **just in Time**


## <a name="adding-kendis---azure-ad-integration-from-the-gallery"></a>Dodawanie Kendis — integracja z usługą Azure AD z galerii

Aby skonfigurować integrację Kendis z integracją usługi Azure AD z usługą Azure AD, musisz dodać integrację Kendis-Azure AD z galerii do listy zarządzanych aplikacji SaaS.

1. Zaloguj się do Azure Portal przy użyciu konta służbowego lub konto Microsoft prywatnego.
1. W okienku nawigacji po lewej stronie wybierz usługę **Azure Active Directory** .
1. Przejdź do **aplikacji przedsiębiorstwa** , a następnie wybierz pozycję **wszystkie aplikacje**.
1. Aby dodać nową aplikację, wybierz pozycję **Nowa aplikacja**.
1. W sekcji **Dodaj z galerii** wpisz **Kendis — integracja z usługą Azure AD** w polu wyszukiwania.
1. Wybierz pozycję **Kendis — integracja z usługą Azure AD** z panelu wyników, a następnie Dodaj aplikację. Poczekaj kilka sekund, gdy aplikacja zostanie dodana do dzierżawy.


## <a name="configure-and-test-azure-ad-sso-for-kendis---azure-ad-integration"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD dla Kendis — integracja z usługą Azure AD

Skonfiguruj i przetestuj Logowanie jednokrotne w usłudze Azure AD za pomocą usługi Kendis — integracja z usługą Azure AD przy użyciu użytkownika testowego o nazwie **B. Simon**. Aby logowanie jednokrotne działało, należy ustanowić relację linku między użytkownikiem usługi Azure AD i powiązanym użytkownikiem w usłudze Kendis — integracja z usługą Azure AD.

Aby skonfigurować i przetestować Logowanie jednokrotne usługi Azure AD za pomocą usługi Kendis — integracja z usługą Azure AD, wykonaj następujące czynności:

1. **[Skonfiguruj Logowanie jednokrotne usługi Azure AD](#configure-azure-ad-sso)** , aby umożliwić użytkownikom korzystanie z tej funkcji.
    1. **[Utwórz użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować Logowanie jednokrotne w usłudze Azure AD za pomocą usługi B. Simon.
    1. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić usłudze B. Simon korzystanie z logowania jednokrotnego w usłudze Azure AD.
1. **[Konfigurowanie Kendis-Azure rejestracji jednokrotnej integracji usługi AD](#configure-kendis-azure-ad-integration-sso)** w celu skonfigurowania ustawień logowania jednokrotnego na stronie aplikacji.
    1. **[Utwórz Kendis-Azure użytkownika testowego integracji usługi AD](#create-kendis-azure-ad-integration-test-user)** , aby uzyskać odpowiednik elementu B. Simon w usłudze Kendis — integracja z usługą Azure AD, która jest połączona z reprezentacją użytkownika w usłudze Azure AD.
1. **[Przetestuj Logowanie jednokrotne](#test-sso)** — aby sprawdzić, czy konfiguracja działa.

## <a name="configure-azure-ad-sso"></a>Konfigurowanie rejestracji jednokrotnej w usłudze Azure AD

Wykonaj następujące kroki, aby włączyć logowanie jednokrotne usługi Azure AD w Azure Portal.

1. W Azure Portal na stronie integracja aplikacji **Azure AD Integration Kendis** Znajdź sekcję **Zarządzanie** i wybierz pozycję **Logowanie jednokrotne**.
1. Na stronie **Wybierz metodę logowania jednokrotnego** wybierz pozycję **SAML**.
1. Na stronie **Konfigurowanie logowania jednokrotnego przy użyciu języka SAML** kliknij ikonę ołówka dla **podstawowej konfiguracji SAML** , aby edytować ustawienia.

   ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

1. Jeśli chcesz skonfigurować aplikację w trybie inicjalizacji **dostawcy tożsamości** , w sekcji **Podstawowa konfiguracja SAML** wprowadź wartości dla następujących pól:

    a. W polu tekstowym **Identyfikator** wpisz adres URL, używając następującego wzorca: `https://<SUBDOMAIN>.kendis.io`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://<SUBDOMAIN>.kendis.io/login/saml`

1. Kliknij pozycję **Ustaw dodatkowe adresy URL** i wykonaj następujące kroki, jeśli chcesz skonfigurować aplikację w trybie inicjowania programu **SP** :

    W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<SUBDOMAIN>.kendis.io/login`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Należy je zastąpić rzeczywistymi wartościami identyfikatora, adresu URL odpowiedzi i adresu URL logowania. Contact [Kendis — zespół obsługi klienta integracji usługi Azure AD](mailto:support@kendis.io) , aby uzyskać te wartości. Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

1. Na stronie **Konfigurowanie logowania jednokrotnego przy użyciu języka SAML** w sekcji **certyfikat podpisywania SAML** Znajdź **certyfikat (base64)** i wybierz pozycję **Pobierz** , aby pobrać certyfikat i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/certificatebase64.png)

1. W sekcji **Konfigurowanie usługi Kendis — integracja z usługą Azure AD** skopiuj odpowiednie adresy URL na podstawie wymagania.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji utworzysz użytkownika testowego w Azure Portal o nazwie B. Simon.

1. W lewym okienku w Azure Portal wybierz pozycję **Azure Active Directory**, wybierz pozycję **Użytkownicy**, a następnie wybierz pozycję **Wszyscy użytkownicy**.
1. Wybierz pozycję **nowy użytkownik** w górnej części ekranu.
1. We właściwościach **użytkownika** wykonaj następujące kroki:
   1. W polu **Nazwa** wprowadź wartość `B.Simon`.  
   1. W polu **Nazwa użytkownika** wprowadź wartość username@companydomain.extension . Na przykład `B.Simon@contoso.com`.
   1. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu **Hasło**.
   1. Kliknij pozycję **Utwórz**.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji włączysz usługę B. Simon, aby korzystać z logowania jednokrotnego na platformie Azure, przyznając dostęp do integracji usługi Kendis z usługą Azure AD.

1. W Azure Portal wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz pozycję **wszystkie aplikacje**.
1. Na liście Aplikacje wybierz pozycję **Kendis — integracja z usługą Azure AD**.
1. Na stronie Przegląd aplikacji Znajdź sekcję **Zarządzanie** i wybierz pozycję **Użytkownicy i grupy**.
1. Wybierz pozycję **Dodaj użytkownika**, a następnie w oknie dialogowym **Dodawanie przypisania** wybierz pozycję **Użytkownicy i grupy** .
1. W oknie dialogowym **Użytkownicy i grupy** wybierz pozycję **B. Simon** z listy Użytkownicy, a następnie kliknij przycisk **Wybierz** w dolnej części ekranu.
1. Jeśli oczekujesz, że rola ma być przypisana do użytkowników, możesz wybrać ją z listy rozwijanej **Wybierz rolę** . Jeśli nie skonfigurowano roli dla tej aplikacji, zostanie wyświetlona wybrana rola "domyślny dostęp".
1. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz** .

## <a name="configure-kendis-azure-ad-integration-sso"></a>Konfigurowanie Kendis-Azure rejestracji jednokrotnej integracji z usługą AD

1. Aby zautomatyzować konfigurację w ramach integracji usługi Kendis z usługą Azure AD, musisz zainstalować **Moje aplikacje bezpieczne logowanie do przeglądarki** , klikając pozycję **Zainstaluj rozszerzenie**.

    ![Rozszerzenie moje aplikacje](common/install-myappssecure-extension.png)

2. Po dodaniu rozszerzenia do przeglądarki, kliknij pozycję **Konfiguracja Kendis — integracja z usługą Azure AD** spowoduje przekierowanie do aplikacji Kendis-Azure AD Integration. Z tego miejsca podaj poświadczenia administratora, aby zalogować się do usługi Kendis — integracja z usługą Azure AD. Rozszerzenie przeglądarki automatycznie skonfiguruje aplikację i automatyzuje kroki 3-5.

    ![Konfiguracja konfiguracji](common/setup-sso.png)

3. Jeśli chcesz ręcznie skonfigurować integrację usługi Kendis — Azure AD, w innym oknie przeglądarki sieci Web Zaloguj się do witryny firmy Kendis — integracja z usługą Azure AD jako administrator.

4. Przejdź do **ustawień > konfiguracjami protokołu SAML**.

    ![ustawienia konfiguracji protokołu SAML](./media/kendis-scaling-agile-platform-tutorial/settings.png)

5. Kliknij przycisk **Edytuj** w dolnej części strony i wykonaj następujące czynności.

    ![Konfiguracje SAML](./media/kendis-scaling-agile-platform-tutorial/saml-configuration-settings.png)

    a. Kopiuj wartość **adresu URL wywołania zwrotnego** , wklej tę wartość w polu tekstowym **adres URL odpowiedzi** w sekcji podstawowa konfiguracja SAML w Azure Portal.

    b. W polu tekstowym adres URL logowania jednokrotnego **dostawcy tożsamości** wklej wartość **adresu URL logowania** , która została skopiowana z Azure Portal.

    c.  W polu tekstowym **wystawca dostawcy tożsamości** wklej wartość **identyfikatora usługi Azure AD (identyfikator jednostki)** skopiowaną z Azure Portal.

    d. Otwórz pobrany **certyfikat (base64)** z Azure Portal do Notatnika i wklej zawartość do pola tekstowego **certyfikatu X. 509** .

    e. Z listy opcji **Wybierz pozycję Grupa domyślna** . 

    f. Kliknij pozycję **Zapisz**.

### <a name="create-kendis-azure-ad-integration-test-user"></a>Utwórz użytkownika testowego integracji usługi AD Kendis-Azure

W tej sekcji użytkownik o nazwie Britta Simon jest tworzony w usłudze Kendis — integracji z usługą Azure AD. Kendis — integracja z usługą Azure AD obsługuje funkcję aprowizacji użytkowników just-in-Time, która jest domyślnie włączona. W tej sekcji nie musisz niczego robić. Jeśli użytkownik nie istnieje jeszcze w usłudze Kendis — integracja z usługą Azure AD, po uwierzytelnieniu zostanie utworzony nowy.

## <a name="test-sso"></a>Testuj Logowanie jednokrotne

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu następujących opcji. 

#### <a name="sp-initiated"></a>Zainicjowano SP:

* Kliknij pozycję **Testuj tę aplikację** w Azure Portal. Spowoduje to przekierowanie na adres URL logowania do usługi Azure AD Kendis, w którym można zainicjować przepływ logowania.  

* Przejdź do Kendis — adres URL logowania do usługi Azure AD Integration bezpośrednio i zainicjuj tam przepływ logowania.

#### <a name="idp-initiated"></a>DOSTAWCY tożsamości zainicjowane:

* Kliknij pozycję **Testuj tę aplikację** w Azure Portal i należy automatycznie zalogować się do integracji usługi Kendis — Azure AD, dla której skonfigurowano Logowanie jednokrotne 

Możesz również użyć aplikacji Microsoft my Apps, aby przetestować aplikację w dowolnym trybie. Po kliknięciu kafelka integracja Kendis-Azure AD w obszarze Moje aplikacje, jeśli zostanie on skonfigurowany w trybie SP, nastąpi przekierowanie do strony logowania do aplikacji w celu zainicjowania przepływu logowania i skonfigurowania w trybie dostawcy tożsamości, należy automatycznie zalogować się do integracji z usługą Azure AD, dla której skonfigurowano Logowanie jednokrotne. Aby uzyskać więcej informacji o moich aplikacjach, zobacz [wprowadzenie do aplikacji Moje aplikacje](../user-help/my-apps-portal-end-user-access.md).


## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu integracji usługi Azure AD Kendis można wymusić kontrolę sesji, co chroni eksfiltracji i niefiltrowanie danych poufnych organizacji w czasie rzeczywistym. Kontrolka sesji rozciąga się od dostępu warunkowego. [Dowiedz się, jak wymuszać kontrolę sesji za pomocą Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).