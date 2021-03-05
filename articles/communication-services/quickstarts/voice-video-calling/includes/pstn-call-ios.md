---
author: nikuklic
ms.service: azure-communication-services
ms.topic: include
ms.date: 9/11/2020
ms.author: nikuklic
ms.openlocfilehash: 80146b4da376f3a1d43bcecc89a4a335263ac5ad
ms.sourcegitcommit: dac05f662ac353c1c7c5294399fca2a99b4f89c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102193929"
---
[!INCLUDE [Emergency Calling Notice](../../../includes/emergency-calling-notice-include.md)]
## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure z aktywną subskrypcją. [Utwórz konto bezpłatnie](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 
- Wdrożony zasób usług komunikacyjnych. [Utwórz zasób usług komunikacyjnych](../../create-communication-resource.md).
- Numer telefonu uzyskany w zasobie usług komunikacyjnych. [jak uzyskać numer telefonu](../../telephony-sms/get-phone-number.md).
- A, `User Access Token` Aby włączyć klienta wywołania. Aby uzyskać więcej informacji na temat [uzyskiwania `User Access Token` ](../../access-tokens.md)
- Ukończ Przewodnik Szybki Start dotyczący [dodawania wywołania do aplikacji](../getting-started-with-calling.md)

### <a name="prerequisite-check"></a>Sprawdzanie wymagań wstępnych

- Aby wyświetlić numery telefonów skojarzone z zasobem usług komunikacyjnych, zaloguj się do [Azure Portal](https://portal.azure.com/), Znajdź zasób usługi komunikacyjnej i Otwórz kartę **numery telefonów** w okienku nawigacji po lewej stronie.
- Możesz skompilować i uruchomić swoją aplikację za pomocą usługi Azure Communications Services wywołującego bibliotekę kliencką dla systemu iOS:

## <a name="setting-up"></a>Konfigurowanie

## <a name="start-a-call-to-phone"></a>Rozpocznij wywołanie telefonu

Określ numer telefonu uzyskany w zasobie usług komunikacyjnych, który zostanie użyty do uruchomienia wywołania:
> [!WARNING]
> Należy zauważyć, że numery telefonów powinny być podane w standardowym formacie E. 164. (np.: + 12223334444)

Zmodyfikuj `startCall` procedurę obsługi zdarzeń, która będzie wykonywana po naciśnięciu przycisku *Rozpocznij połączenie* :

```swift
func startCall() {
    // Ask permissions
    AVAudioSession.sharedInstance().requestRecordPermission { (granted) in
        if granted {
            let startCallOptions = ACSStartCallOptions()
            startCallOptions!.alternateCallerID = PhoneNumber(phoneNumber: "+12223334444")
            self.call = self.callAgent!.startCall([PhoneNumber(phoneNumber: self.callee)], options: startCallOptions)
            self.callDelegate = CallDelegate(self)
            self.call!.delegate = self.callDelegate
        }
    }
}
```

## <a name="run-the-code"></a>Uruchamianie kodu

Możesz skompilować i uruchomić aplikację w symulatorze systemu iOS, wybierając opcję  >  **Uruchom** produkt lub używając skrótu klawiaturowego (&#8984;-R).

![Końcowy wygląd i działanie aplikacji szybkiego startu](../media/ios/quick-start-make-call.png)

Możesz nawiązać połączenie telefoniczne, podając numer telefonu w dodanym polu tekstowym, a następnie klikając przycisk **Rozpocznij połączenie** .
> [!WARNING]
> Należy zauważyć, że numery telefonów powinny być podane w standardowym formacie E. 164. (np.: + 12223334444)

> [!NOTE]
> Podczas pierwszego wywołania system wyświetli monit o uzyskanie dostępu do mikrofonu. W aplikacji produkcyjnej należy użyć `AVAudioSession` interfejsu API [Sprawdzanie stanu uprawnień](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources) i bezpiecznie aktualizować zachowanie aplikacji, gdy uprawnienie nie zostanie przyznane.
