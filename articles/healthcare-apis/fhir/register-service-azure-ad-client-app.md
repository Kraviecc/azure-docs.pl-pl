---
title: Rejestrowanie aplikacji usługi w usłudze Azure AD — Azure API for FHIR
description: Dowiedz się, jak zarejestrować aplikację klienta usługi w Azure Active Directory.
services: healthcare-apis
author: matjazl
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: conceptual
ms.date: 02/07/2019
ms.author: matjazl
ms.openlocfilehash: 6f7bf122b292ca144eac406957f19a13c7ba6662
ms.sourcegitcommit: 225e4b45844e845bc41d5c043587a61e6b6ce5ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2021
ms.locfileid: "103020065"
---
# <a name="register-a-service-client-application-in-azure-active-directory"></a>Rejestrowanie aplikacji klienckiej usługi w Azure Active Directory

W tym artykule dowiesz się, jak zarejestrować aplikację klienta usługi w Azure Active Directory. Rejestracje aplikacji klienckich są Azure Active Directory reprezentacje aplikacji, których można użyć do uwierzytelniania i uzyskiwania tokenów. Klient usługi jest przeznaczony do użycia przez aplikację w celu uzyskania tokenu dostępu bez interaktywnego uwierzytelniania użytkownika. Będzie on miał pewne uprawnienia do aplikacji i używa klucza tajnego aplikacji (hasła) podczas uzyskiwania tokenów dostępu.

Wykonaj następujące kroki, aby utworzyć nowego klienta usługi.

## <a name="app-registrations-in-azure-portal"></a>Rejestracje aplikacji w Azure Portal

1. W [Azure Portal](https://portal.azure.com)przejdź do **Azure Active Directory**.

2. Wybierz pozycję **Rejestracje aplikacji**.

    ![Azure Portal. Rejestracja nowej aplikacji.](media/how-to-aad/portal-aad-new-app-registration.png)

3. Wybierz pozycję **Nowa rejestracja**.

4. Nadaj klientowi usługi nazwę wyświetlaną. Aplikacje klienckie usługi zwykle nie używają adresu URL odpowiedzi.

    :::image type="content" source="media/service-client-app/service-client-registration.png" alt-text="Azure Portal. Rejestracja nowej aplikacji klienta usługi.":::

5. Wybierz pozycję **Zarejestruj**.

## <a name="api-permissions"></a>Uprawnienia aplikacji

Po zarejestrowaniu aplikacji należy wybrać uprawnienia interfejsu API, dla których ta aplikacja powinna mieć możliwość żądania w imieniu użytkowników:

1. Wybierz pozycję **uprawnienia interfejsu API**.
1. Wybierz pozycję **Dodaj uprawnienie**.

    Jeśli używasz interfejsu API platformy Azure dla usługi FHIR, dodasz uprawnienie do interfejsów API usługi Azure opieki IT, wyszukując **interfejsy API usługi Azure opieki zdrowotnej** w obszarze **interfejsy API używane przez moją organizację**. 

    Jeśli odwołujesz się do innej aplikacji zasobów, wybierz [rejestrację aplikacji interfejsu API FHIR](register-resource-azure-ad-client-app.md) utworzoną wcześniej w obszarze **Moje interfejsy API**.

    :::image type="content" source="media/service-client-app/service-client-org-api.png" alt-text="Klient poufny. Moje interfejsy API organizacji" lightbox="media/service-client-app/service-client-org-api-expanded.png":::

1. Wybierz zakresy (uprawnienia), które mogą być dostępne dla aplikacji poufnej w imieniu użytkownika:

    :::image type="content" source="media/service-client-app/service-client-add-permission.png" alt-text="Klient usługi. Delegowane uprawnienia":::

1. Udziel zgody aplikacji. Jeśli nie masz wymaganych uprawnień, skontaktuj się z administratorem Azure Active Directory:

    :::image type="content" source="media/service-client-app/service-client-grant-permission.png" alt-text="Klient usługi. Udziel zgody":::

## <a name="application-secret"></a>Klucz tajny aplikacji

Klient usługi wymaga klucza tajnego (hasła), aby uzyskać token.

1. Wybierz pozycję **certyfikaty & wpisy tajne**.
2. Wybierz pozycję **Nowy wpis tajny klienta**.

    ![Azure Portal. Klucz tajny klienta usługi](media/how-to-aad/portal-aad-register-new-app-registration-SERVICE-CLIENT-SECRET.png)

3. Podaj opis i czas trwania wpisu tajnego (1 rok, 2 lata lub nigdy).

4. Po wygenerowaniu wpisu tajnego zostanie on wyświetlony tylko raz w portalu. Zanotuj ją i przechowuj w bezpieczny sposób.

## <a name="next-steps"></a>Następne kroki

W tym artykule przedstawiono sposób rejestrowania aplikacji klienckiej usługi w Azure Active Directory. Następnie przetestuj dostęp do serwera FHIR za pomocą programu Poster.
 
>[!div class="nextstepaction"]
>[Dostęp do interfejsu API platformy Azure dla usługi FHIR za pomocą programu Poster](access-fhir-postman-tutorial.md)
