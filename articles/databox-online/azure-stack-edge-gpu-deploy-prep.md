---
title: Samouczek przygotowywania Azure Portal, środowiska centrum danych do wdrażania Azure Stack Edge — procesor GPU Microsoft Docs
description: Pierwszy samouczek dotyczący wdrażania Azure Stack brzegowej procesora GPU obejmuje przygotowywanie Azure Portal.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 10/21/2020
ms.author: alkohli
Customer intent: As an IT admin, I need to understand how to prepare the portal to deploy Azure Stack Edge Pro so I can use it to transfer data to Azure.
ms.openlocfilehash: cdfd012d5015e156439a1afa89e818bf82b64dc6
ms.sourcegitcommit: 6a350f39e2f04500ecb7235f5d88682eb4910ae8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96449325"
---
# <a name="tutorial-prepare-to-deploy-azure-stack-edge-pro-with-gpu"></a>Samouczek: przygotowanie do wdrożenia Azure Stack EDGE Pro z procesorem GPU 

Jest to pierwszy samouczek z serii samouczków wdrażania, które są wymagane do całkowitego wdrożenia Azure Stack EDGE Pro z procesorem GPU. W tym samouczku opisano sposób przygotowania Azure Portal w celu wdrożenia Azure Stackego zasobu brzegowego.

Do ukończenia procesu instalacji i konfiguracji niezbędne są uprawnienia administratora. Przygotowanie portalu zajmuje mniej niż 10 minut.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie nowego zasobu
> * Uzyskiwanie klucza aktywacji

### <a name="get-started"></a>Wprowadzenie

W przypadku wdrożenia programu Azure Stack EDGE Pro należy najpierw przygotować swoje środowisko. Gdy środowisko będzie gotowe, wykonaj wymagane kroki i w razie potrzeby opcjonalne kroki i procedury, aby całkowicie wdrożyć urządzenie. Instrukcje krok po kroku wskazują, kiedy należy wykonać każdy z tych wymaganych i opcjonalnych kroków.

| Krok | Opis |
| --- | --- |
| **Przygotowanie** |Te kroki należy wykonać w celu przygotowania do nadchodzącego wdrożenia. |
| **[Lista kontrolna konfiguracji wdrożenia](#deployment-configuration-checklist)** |Ta lista kontrolna umożliwia zbieranie i rejestrowanie informacji przed wdrożeniem i w jego trakcie. |
| **[Wymagania wstępne dotyczące wdrażania](#prerequisites)** |Służą do sprawdzania, czy środowisko jest gotowe do przeprowadzenia wdrożenia. |
|  | |
|**Samouczki dotyczące wdrażania** |Te samouczki są wymagane do wdrożenia urządzenia z usługą Azure Stack Edge w środowisku produkcyjnym. |
|**[1. Przygotuj Azure Portal dla Azure Stack brzeg Pro](azure-stack-edge-gpu-deploy-prep.md)** |Utwórz i skonfiguruj zasób Azure Stack Edge przed zainstalowaniem urządzenia fizycznego z krawędzią okna Azure Stack. |
|**[2. Zainstaluj Azure Stack EDGE Pro](azure-stack-edge-gpu-deploy-install.md)**|Rozpakuj, stojak i podłącz kable do urządzenia fizycznego w Azure Stack EDGE Pro.  |
|**[3. Nawiązywanie połączenia z usługą Azure Stack EDGE Pro](azure-stack-edge-gpu-deploy-connect.md)** |Po zainstalowaniu urządzenia Połącz się z lokalnym interfejsem użytkownika sieci Web urządzenia.  |
|**[4. Skonfiguruj ustawienia sieci dla Azure Stack EDGE Pro](azure-stack-edge-gpu-deploy-configure-network-compute-web-proxy.md)** |Skonfiguruj sieć, w tym ustawienia sieci Web i internetowego serwera proxy dla Twojego urządzenia.   |
|**[5. Skonfiguruj ustawienia urządzenia dla programu Azure Stack EDGE Pro](azure-stack-edge-gpu-deploy-set-up-device-update-time.md)** |Przypisz nazwę urządzenia i domenę DNS, skonfiguruj serwer aktualizacji i godzinę urządzenia. |
|**[6. Skonfiguruj ustawienia zabezpieczeń dla Azure Stack EDGE Pro](azure-stack-edge-gpu-deploy-configure-certificates.md)** |Skonfiguruj certyfikaty dla urządzenia. Użyj certyfikatów wygenerowanych przez urządzenia lub Przenieś własne certyfikaty.   |
|**[7. Aktywuj Azure Stack Edge w wersji Pro](azure-stack-edge-gpu-deploy-activate.md)** |Aktywuj urządzenie przy użyciu klucza aktywacji z usługi. Urządzenie jest gotowe do skonfigurowania udziałów SMB lub NFS lub łączenia się za pośrednictwem interfejsu REST. |
|**[8. Konfigurowanie obliczeń](azure-stack-edge-gpu-deploy-configure-compute.md)** |Skonfiguruj rolę obliczeń na urządzeniu. Spowoduje to również utworzenie klastra Kubernetes. |
|**[9a. Transferowanie danych za pomocą udziałów brzegowych](azure-stack-edge-j-series-deploy-add-shares.md)** |Dodaj udziały i nawiąż z nimi połączenie za pomocą protokołu SMB lub NFS. |
|**[9b. Transferowanie danych za pomocą kont magazynu Edge](azure-stack-edge-j-series-deploy-add-storage-accounts.md)** |Dodawanie kont magazynu i nawiązywanie połączenia z usługą BLOB Storage za pośrednictwem interfejsów API REST. |


Teraz możesz zacząć zbierać informacje dotyczące konfiguracji oprogramowania dla urządzenia z usługą Azure Stack EDGE Pro.

## <a name="deployment-configuration-checklist"></a>Lista kontrolna dotycząca konfiguracji wdrożenia

Przed wdrożeniem urządzenia należy zebrać informacje w celu skonfigurowania oprogramowania na urządzeniu Azure Stack Edge. Wcześniejsze przygotowanie niektórych z tych informacji pomaga usprawnić proces wdrażania urządzenia w środowisku. [Lista kontrolna konfiguracji wdrożenia programu Azure Stack Edge](azure-stack-edge-gpu-deploy-checklist.md) w programie umożliwia zanotowanie szczegółów konfiguracji podczas wdrażania urządzenia.


## <a name="prerequisites"></a>Wymagania wstępne

Poniżej przedstawiono wymagania wstępne dotyczące konfiguracji dla zasobu usługi Azure Stack Edge, urządzenia brzegowego Azure Stack Edge i sieci centrum danych.

### <a name="for-the-azure-stack-edge-resource"></a>Dla zasobu brzegowego Azure Stack

Przed rozpoczęciem upewnij się, że:

- Subskrypcja Microsoft Azure jest włączona dla zasobu Azure Stack Edge. Upewnij się, że użyto obsługiwanej subskrypcji, takiej jak [Microsoft Umowa Enterprise (EA)](https://azure.microsoft.com/overview/sales-number/), [dostawca rozwiązań w chmurze (CSP)](/partner-center/azure-plan-lp)lub [dostęp sponsorowany Microsoft Azure](https://azure.microsoft.com/offers/ms-azr-0036p/). Subskrypcje z płatnością zgodnie z rzeczywistym użyciem nie są obsługiwane. Aby zidentyfikować typ posiadanej subskrypcji platformy Azure, zobacz artykuł [co to jest oferta platformy Azure?](../cost-management-billing/manage/switch-azure-offer.md#what-is-an-azure-offer)
- Masz uprawnienia właściciela lub współautora na poziomie grupy zasobów dla Azure Stack EDGE Pro/Data Box Gateway, IoT Hub i zasobów usługi Azure Storage.

    - Aby utworzyć dowolny zasób Azure Stack Edge/Data Box Gateway, należy mieć uprawnienia jako współautora (lub wyższe) w zakresie na poziomie grupy zasobów. 
    - Należy również upewnić się, że `Microsoft.DataBoxEdge` `MicrosoftKeyVault` dostawcy zasobów i są zarejestrowani. Aby utworzyć dowolny zasób IoT Hub, `Microsoft.Devices` należy zarejestrować dostawcę. 
        - Aby zarejestrować dostawcę zasobów, w Azure Portal przejdź do **strony głównej > subskrypcji > dostawców zasobów > subskrypcji**. 
        - Wyszukaj określonego dostawcę zasobów, na przykład, `Microsoft.DataBoxEdge` i zarejestruj dostawcę zasobów. 
    - Aby utworzyć zasób konta magazynu, należy ponownie uzyskać wartość współautor lub wyższy dostęp do zakresu na poziomie grupy zasobów. Usługa Azure Storage jest domyślnie zarejestrowanym dostawcą zasobów.
- Masz uprawnienia administratora lub użytkownika do Azure Active Directory interfejs API programu Graph do generowania klucza aktywacji lub operacji poświadczeń, takich jak tworzenie udziałów, które korzystają z konta magazynu. Aby uzyskać więcej informacji, zobacz [Azure Active Directory interfejs API programu Graph](/previous-versions/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes#default-access-for-administrators-users-and-guest-users-).


### <a name="for-the-azure-stack-edge-pro-device"></a>Dla urządzenia Azure Stack EDGE Pro

Przed wdrożeniem urządzenia fizycznego upewnij się, że są spełnione następujące warunki:

- Zawarto przegląd informacji o bezpieczeństwie uwzględnionych w pakiecie dostawy.
- Dostępne jest gniazdo o rozmiarze 1U w standardowym 19 "stojaku w centrum danych na potrzeby instalowania urządzenia.
- Masz dostęp do płaskiej, stabilnej i poziomej powierzchni roboczej, gdzie można bezpiecznie umieścić urządzenie.
- Miejsce, w którym chcesz skonfigurować urządzenie, ma standardowe zasilanie prądem przemiennym z niezależnego źródła lub jednostkę dystrybucji zasilania na stojaku (PDU, rack power distribution unit) z zasilaczem UPS.
- Masz dostęp do urządzenia fizycznego.


### <a name="for-the-datacenter-network"></a>Sieć centrum danych

Przed rozpoczęciem upewnij się, że:

- Sieć w centrum danych jest konfigurowana zgodnie z wymaganiami dotyczącymi sieci dla urządzenia z Azure Stack Edge. Aby uzyskać więcej informacji, zobacz [Azure Stack Edge — wymagania systemowe](azure-stack-edge-system-requirements.md).

- W normalnych warunkach operacyjnych Azure Stack EDGE Pro masz:

    - Co najmniej 10 MB/s, aby upewnić się, że urządzenie pozostaje zaktualizowane.
    - Co najmniej 20 MB/s dedykowane i pobiera przepustowość do przesyłania plików.

## <a name="create-a-new-resource"></a>Tworzenie nowego zasobu

Jeśli masz istniejący zasób Azure Stack Edge do zarządzania urządzeniem fizycznym, Pomiń ten krok i przejdź do pozycji [Pobierz klucz aktywacji](#get-the-activation-key).

Aby utworzyć zasób Azure Stack Edge, wykonaj następujące czynności w Azure Portal.

1. Użyj poświadczeń Microsoft Azure, aby zalogować się do Azure Portal pod tym adresem URL: [https://portal.azure.com](https://portal.azure.com) .

2. W okienku po lewej stronie wybierz pozycję **+ Utwórz zasób**. Wyszukaj i wybierz pozycję **Azure Stack Edge/Data Box Gateway**. Wybierz pozycję **Utwórz**. 

3. Wybierz subskrypcję, która ma być używana na potrzeby urządzenia z Azure Stack EDGE Pro. Wybierz kraj, w którym chcesz wysłać to urządzenie fizyczne. Wybierz pozycję **Pokaż urządzenia**.

    ![Utwórz zasób 1](media/azure-stack-edge-gpu-deploy-prep/create-resource-1.png)

4. Wybierz pozycję typ urządzenia. W obszarze **Azure Stack EDGE Pro** wybierz pozycję **Azure Stack EDGE Pro z procesorem GPU** , a następnie wybierz **pozycję Wybierz**. Jeśli widzisz jakiekolwiek problemy lub nie można wybrać typu urządzenia, przejdź do obszaru [Rozwiązywanie problemów z kolejnością](azure-stack-edge-troubleshoot-ordering.md).

    ![Tworzenie zasobu 3](media/azure-stack-edge-gpu-deploy-prep/create-resource-3.png)

5. W zależności od potrzeb firmy można wybrać pozycję Azure Stack EDGE Pro z 1 lub 2 graficznymi jednostkami przetwarzania (GPU) firmy NVIDIA. 

    ![Tworzenie zasobu 4](media/azure-stack-edge-gpu-deploy-prep/create-resource-4.png)

6. Na karcie **podstawowe** wprowadź lub wybierz poniższe **szczegóły projektu**.
    
    |Ustawienie  |Wartość  |
    |---------|---------|
    |Subskrypcja    |Jest to wypełniane automatycznie w oparciu o wcześniejszy wybór. Subskrypcja jest połączona z kontem rozliczeniowym. |
    |Grupa zasobów  |Wybierz istniejącą grupę lub utwórz nową.<br>Dowiedz się więcej o [grupach zasobów platformy Azure](../azure-resource-manager/management/overview.md).     |

7. Wprowadź lub wybierz następujące **szczegóły wystąpienia**.

    |Ustawienie  |Wartość  |
    |---------|---------|
    |Nazwa   | Przyjazna nazwa identyfikująca zasób.<br>Nazwa może zawierać od 2 do 50 znaków, w tym litery, cyfry i łączniki.<br> Nazwa rozpoczyna się i kończy literą lub cyfrą.        |
    |Region (Region)     |Aby uzyskać listę wszystkich regionów, w których jest dostępny zasób Azure Stack Edge, zobacz [dostępność produktów platformy Azure według regionów](https://azure.microsoft.com/global-infrastructure/services/?products=databox&regions=all). W przypadku korzystania z Azure Government wszystkie regiony rządowe są dostępne, jak pokazano w [regionach świadczenia usługi Azure](https://azure.microsoft.com/global-infrastructure/regions/).<br> Wybierz lokalizację najbliżej regionu geograficznego, w którym chcesz wdrożyć urządzenie.|

    ![Tworzenie zasobu 5](media/azure-stack-edge-gpu-deploy-prep/create-resource-5.png)

8. Wybierz pozycję **Dalej: adres wysyłkowy**.

    - Jeśli masz już urządzenie, zaznacz pole kombi dla **urządzenia z Azure Stack EDGE Pro**.

        ![Tworzenie zasobu 6](media/azure-stack-edge-gpu-deploy-prep/create-resource-6.png)

    - Jeśli jest to nowe urządzenie, które ma być uporządkowane, wprowadź nazwę kontaktu, firmę, adres, który ma zostać wysłany do urządzenia, i informacje kontaktowe.

        ![Tworzenie zasobu 7](media/azure-stack-edge-gpu-deploy-prep/create-resource-7.png)

9. Wybierz pozycję **Dalej: Tagi**. Opcjonalnie możesz podać znaczniki kategoryzacji zasobów i skonsolidować rozliczenia. Wybierz pozycję **Dalej: Przeglądanie i tworzenie**.

10. Na karcie **Recenzja + tworzenie** Przejrzyj **szczegóły cennika**, **warunki użytkowania** i szczegóły dotyczące zasobu. Zaznacz pole kombi dla **zrecenzowanych warunków zachowania poufności informacji**.

    ![Tworzenie zasobu 8](media/azure-stack-edge-gpu-deploy-prep/create-resource-8.png) 

    Użytkownik otrzymuje również powiadomienie, że podczas tworzenia zasobu jest włączony tożsamość usługi zarządzanej (MSI), który umożliwia uwierzytelnianie w usługach w chmurze. Ta tożsamość istnieje pod warunkiem, że istnieje zasób.

11. Wybierz pozycję **Utwórz**.

Tworzenie zasobu trwa kilka minut. Tworzony jest również plik MSI, który umożliwia Azure Stack urządzeniu brzegowego komunikowanie się z dostawcą zasobów na platformie Azure.

Po pomyślnym utworzeniu i wdrożeniu zasobu zostanie wyświetlone powiadomienie. Wybierz pozycję **Przejdź do zasobu**.

![Przejdź do zasobu Azure Stack EDGE Pro](media/azure-stack-edge-gpu-deploy-prep/azure-stack-edge-resource-1.png)

Po złożeniu zamówienia firma Microsoft przegląda zamówienie i dotrze do Ciebie (za pośrednictwem poczty e-mail), podając szczegóły dotyczące wysyłki.

<!--![Notification for review of the Azure Stack Edge Pro order](media/azure-stack-edge-gpu-deploy-prep/azure-stack-edge-resource-2.png)-->

> [!NOTE]
>Jeśli chcesz utworzyć wiele zamówień w tym samym czasie lub sklonować istniejące zamówienie, możesz użyć [skryptów w przykładach platformy Azure](https://github.com/Azure-Samples/azure-stack-edge-order). Aby uzyskać więcej informacji, zobacz plik Readme.

W przypadku wystąpienia problemów występujących w procesie zamówienia zobacz [Rozwiązywanie problemów z kolejnością](azure-stack-edge-troubleshoot-ordering.md).

## <a name="get-the-activation-key"></a>Uzyskiwanie klucza aktywacji

Po rozpoczęciu i uruchomieniu Azure Stack brzegowej należy uzyskać klucz aktywacji. Ten klucz służy do uaktywniania i łączenia urządzenia Azure Stack EDGE Pro z zasobem. Ten klucz można uzyskać już teraz za pośrednictwem witryny Azure Portal.

1. Wybierz utworzony zasób. Wybierz pozycję **Przegląd** , a następnie wybierz pozycję **Konfiguracja urządzenia**.

    ![Wybierz konfigurację urządzenia](media/azure-stack-edge-gpu-deploy-prep/azure-stack-edge-resource-2.png)

2. Na kafelku **Aktywuj** podaj nazwę Azure Key Vault lub zaakceptuj nazwę domyślną. Nazwa magazynu kluczy może mieć długość od 3 do 24 znaków. 

    Magazyn kluczy jest tworzony dla każdego zasobu usługi Azure Stack Edge, który został aktywowany z urządzeniem. Magazyn kluczy pozwala przechowywać klucze tajne i uzyskiwać do nich dostęp, na przykład klucz integralności kanału (CIK) dla usługi jest przechowywany w magazynie kluczy. 

    Po określeniu nazwy magazynu kluczy wybierz pozycję **Generuj klucz** , aby utworzyć klucz aktywacji. 

    ![Pobieranie klucza aktywacji](media/azure-stack-edge-gpu-deploy-prep/azure-stack-edge-resource-3.png)

    Poczekaj kilka minut, aż zostanie utworzony magazyn kluczy i klucz aktywacji. Wybierz ikonę kopiowania, aby skopiować klucz i zapisać go do użytku w przyszłości.


> [!IMPORTANT]
> - Klucz aktywacji wygasa po trzech dniach od jego wygenerowania.
> - Jeśli klucz wygaśnie, wygeneruj nowy klucz. Starszy klucz nie jest prawidłowy.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono informacje dotyczące Azure Stack krawędzi programu Edge dla pakietu Pro, takich jak:

> [!div class="checklist"]
> * Tworzenie nowego zasobu
> * Uzyskiwanie klucza aktywacji

Przejdź do następnego samouczka, aby dowiedzieć się, jak zainstalować program Azure Stack EDGE Pro.

> [!div class="nextstepaction"]
> [Zainstaluj Azure Stack EDGE Pro](./azure-stack-edge-gpu-deploy-install.md)