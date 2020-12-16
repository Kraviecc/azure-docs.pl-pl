---
title: Dodawanie przepływu użytkownika samoobsługowego rejestrowania — Azure AD
description: Tworzenie przepływów użytkowników dla aplikacji, które są tworzone przez organizację. Następnie użytkownicy odwiedzający tę aplikację mogą uzyskać konto gościa przy użyciu opcji skonfigurowanych w przepływie użytkownika.
services: active-directory
ms.service: active-directory
ms.subservice: B2B
ms.topic: how-to
ms.date: 06/16/2020
ms.author: mimart
author: msmimart
manager: celestedg
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: f76f4a3e5fc87420c242c693e3c48a91244641e0
ms.sourcegitcommit: 77ab078e255034bd1a8db499eec6fe9b093a8e4f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97560037"
---
# <a name="add-a-self-service-sign-up-user-flow-to-an-app-preview"></a>Dodawanie przepływu użytkownika samoobsługowego rejestrowania do aplikacji (wersja zapoznawcza)
> [!NOTE]
> Rejestracja samoobsługowa jest publiczną funkcją w wersji zapoznawczej Azure Active Directory. Aby uzyskać więcej informacji na temat wersji zapoznawczych, zobacz [dodatkowe warunki użytkowania wersji](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)zapoznawczych Microsoft Azure.

Możesz tworzyć przepływy użytkowników dla aplikacji, które są tworzone przez organizację. Skojarzenie przepływu użytkownika z aplikacją pozwala na włączenie rejestracji w tej aplikacji. Możesz wybrać więcej niż jedną aplikację, która ma być skojarzona z przepływem użytkownika. Po skojarzeniu przepływu użytkownika z co najmniej jedną aplikacją użytkownicy, którzy odwiedzają tę aplikację, będą mogli zarejestrować się i uzyskać konto gościa przy użyciu opcji skonfigurowanych w przepływie użytkownika.

> [!NOTE]
> Przepływy użytkowników można kojarzyć z aplikacjami skompilowanymi przez organizację. Przepływów użytkowników nie można używać dla aplikacji firmy Microsoft, takich jak SharePoint i zespoły.

## <a name="before-you-begin"></a>Przed rozpoczęciem

### <a name="add-social-identity-providers-optional"></a>Dodaj dostawców tożsamości społecznościowych (opcjonalnie)

Usługa Azure AD jest domyślnym dostawcą tożsamości dla samoobsługowego rejestrowania się. Oznacza to, że użytkownicy mogą rejestrować się domyślnie przy użyciu konta usługi Azure AD. Dostawców tożsamości społecznościowych można również dołączać do tych przepływów rejestracji, aby obsługiwać konta Google i Facebook.

- [Dodawanie usługi Facebook do listy dostawców tożsamości społecznościowych](facebook-federation.md)
- [Dodaj firmę Google do listy dostawców tożsamości społecznościowych](google-federation.md)

> [!NOTE]
> W bieżącej wersji zapoznawczej, jeśli przepływ użytkownika samoobsługowego rejestrowania jest skojarzony z aplikacją i wysyłasz użytkownikowi zaproszenie do tej aplikacji, użytkownik nie będzie mógł skorzystać z konta usługi Gmail w celu zrealizowania zaproszenia. W ramach tego problemu użytkownik może przejść przez proces tworzenia konta samoobsługowego. Mogą oni lub korzystać z zaproszenia, uzyskując dostęp do innej aplikacji lub portalu Moje aplikacje pod adresem https://myapps.microsoft.com .

### <a name="define-custom-attributes-optional"></a>Zdefiniuj atrybuty niestandardowe (opcjonalnie)

Atrybuty użytkownika są wartościami zbieranymi od użytkownika podczas samoobsługowego rejestrowania się. Usługa Azure AD jest dostarczana z wbudowanym zestawem atrybutów, ale można utworzyć niestandardowe atrybuty do użycia w przepływie użytkownika. Można również odczytywać i zapisywać te atrybuty przy użyciu interfejsu API Microsoft Graph. Zobacz [Definiowanie atrybutów niestandardowych dla przepływów użytkowników](user-flow-add-custom-attributes.md).

## <a name="enable-self-service-sign-up-for-your-tenant"></a>Włączanie rejestracji samoobsługowej dla dzierżawy

Przed dodaniem przepływu użytkownika samoobsługowego rejestrowania do aplikacji należy włączyć tę funkcję dla dzierżawy. Po włączeniu kontrolki staną się dostępne w przepływie użytkownika, które umożliwiają skojarzenie przepływu użytkownika z aplikacją.

1. Zaloguj się do [Azure Portal](https://portal.azure.com) jako administrator usługi Azure AD.
2. W obszarze **usługi platformy Azure** wybierz pozycję **Azure Active Directory**.
3. Wybierz pozycję **Ustawienia użytkownika**, a następnie w obszarze **użytkownicy zewnętrzni** wybierz pozycję **Zarządzaj ustawieniami współpracy zewnętrznej**.
4. Ustaw opcję Włącz logowanie samoobsługowe dla **gościa za pomocą funkcji przepływy użytkownika (wersja zapoznawcza)** Przełącz na **wartość tak**.

   ![Włącz rejestrację samoobsługową gościa](media/self-service-sign-up-user-flow/enable-self-service-sign-up.png)
5. Wybierz pozycję **Zapisz**.
## <a name="create-the-user-flow-for-self-service-sign-up"></a>Tworzenie przepływu użytkownika na potrzeby rejestracji samoobsługowej

Następnie utworzysz przepływ użytkownika na potrzeby rejestracji samoobsługowej i dodasz go do aplikacji.

1. Zaloguj się do [Azure Portal](https://portal.azure.com) jako administrator usługi Azure AD.
2. W obszarze **usługi platformy Azure** wybierz pozycję **Azure Active Directory**.
3. W menu po lewej stronie wybierz pozycję **tożsamości zewnętrzne**.
4. Wybierz pozycję **przepływy użytkownika (wersja zapoznawcza)**, a następnie wybierz pozycję **Nowy przepływ użytkownika**.

   ![Dodaj nowy przycisk przepływu użytkownika](media/self-service-sign-up-user-flow/new-user-flow.png)

5. Na stronie **Tworzenie** wprowadź **nazwę** przepływu użytkownika. Należy pamiętać, że nazwa jest automatycznie prefiksem **B2X_1_**.
6. Na liście **dostawcy tożsamości** wybierz co najmniej jednego dostawcę tożsamości, którego użytkownicy zewnętrzni mogą używać do logowania się do aplikacji. **Konto Azure Active Directory** jest domyślnie zaznaczone. (Zobacz [przed rozpoczęciem](#before-you-begin) wcześniejszego działania w tym artykule, aby dowiedzieć się, jak dodać dostawców tożsamości).
7. W obszarze **atrybuty użytkownika** wybierz atrybuty, które mają być zbierane od użytkownika. Aby uzyskać dodatkowe atrybuty, wybierz pozycję **Pokaż więcej**. Na przykład wybierz pozycję **Pokaż więcej**, a następnie wybierz atrybuty i oświadczenia dla **kraju/regionu**, **Nazwa wyświetlana** i **Kod pocztowy**. Wybierz przycisk **OK**.

   ![Tworzenie nowej strony przepływu użytkownika](media/self-service-sign-up-user-flow/create-user-flow.png)

8. Wybierz pozycję **Utwórz**.
9. Nowy przepływ użytkownika zostanie wyświetlony na liście **przepływy użytkownika (wersja zapoznawcza)** . W razie potrzeby Odśwież stronę.

## <a name="select-the-layout-of-the-attribute-collection-form"></a>Wybierz układ formularza kolekcji atrybutów

Możesz wybrać kolejność, w jakiej atrybuty są wyświetlane na stronie rejestracji. 

1. W witrynie [Azure Portal](https://portal.azure.com) wybierz pozycję **Azure Active Directory**.
2. Wybierz pozycję **tożsamości zewnętrzne**, wybierz pozycję **przepływy użytkownika (wersja zapoznawcza)**.
3. Wybierz z listy przepływ użytkownika do samoobsługowego rejestrowania.
4. W obszarze **Dostosowywanie** wybierz pozycję **układy stron**.
5. Zostaną wyświetlone atrybuty wybrane do zebrania. Aby zmienić kolejność wyświetlania, wybierz atrybut, a następnie wybierz pozycję Przenieś w **górę**, **Przenieś w dół**, **Przenieś w górę** lub **Przenieś w** dół.
6. Wybierz pozycję **Zapisz**.

## <a name="add-applications-to-the-self-service-sign-up-user-flow"></a>Dodawanie aplikacji do przepływu użytkownika samoobsługowego rejestrowania

Teraz można kojarzyć aplikacje z przepływem użytkownika.

1. Zaloguj się do [Azure Portal](https://portal.azure.com) jako administrator usługi Azure AD.
2. W obszarze **usługi platformy Azure** wybierz pozycję **Azure Active Directory**.
3. W menu po lewej stronie wybierz pozycję **tożsamości zewnętrzne**.
4. W obszarze **rejestracja samoobsługowa** wybierz pozycję **przepływy użytkownika (wersja zapoznawcza)**.
5. Wybierz z listy przepływ użytkownika do samoobsługowego rejestrowania.
6. W menu po lewej stronie w obszarze **Użyj** wybierz pozycję **aplikacje**.
7. Wybierz pozycję **Dodaj aplikację**.

   ![Przypisywanie aplikacji do przepływu użytkownika](media/self-service-sign-up-user-flow/assign-app-to-user-flow.png)

8. Wybierz aplikację z listy. Lub użyj pola wyszukiwania, aby znaleźć aplikację, a następnie wybierz ją.
9. Kliknij pozycję **Wybierz**.

## <a name="next-steps"></a>Następne kroki

- [Dodaj firmę Google do listy dostawców tożsamości społecznościowych](google-federation.md)
- [Dodawanie usługi Facebook do listy dostawców tożsamości społecznościowych](facebook-federation.md)
- [Używanie łączników interfejsu API do dostosowywania i zwiększania przepływów użytkownika za pośrednictwem interfejsów API sieci Web](api-connectors-overview.md)
- [Dodawanie niestandardowego przepływu pracy zatwierdzenia do przepływu użytkownika](self-service-sign-up-add-approvals.md)
