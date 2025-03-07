---
title: 'Szybki Start: Tworzenie publicznego modułu równoważenia obciążenia — Azure Portal'
titleSuffix: Azure Load Balancer
description: Ten przewodnik Szybki Start przedstawia sposób tworzenia modułu równoważenia obciążenia przy użyciu Azure Portal.
services: load-balancer
documentationcenter: na
author: asudbring
manager: KumudD
Customer intent: I want to create a load balancer so that I can load balance internet traffic to VMs.
ms.service: load-balancer
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2021
ms.author: allensu
ms.custom: mvc
ms.openlocfilehash: 634f09c7862f6e3e2f147094503f5a574476ef91
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102034391"
---
# <a name="quickstart-create-a-public-load-balancer-to-load-balance-vms-using-the-azure-portal"></a>Szybki Start: Tworzenie publicznego modułu równoważenia obciążenia w celu równoważenia obciążenia maszyn wirtualnych przy użyciu Azure Portal

Rozpocznij pracę z Azure Load Balancer przy użyciu Azure Portal, aby utworzyć publiczny moduł równoważenia obciążenia i trzy maszyny wirtualne.

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure z aktywną subskrypcją. [Utwórz konto bezpłatnie](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="sign-in-to-azure"></a>Logowanie do platformy Azure

Zaloguj się do witryny Azure Portal pod adresem [https://portal.azure.com](https://portal.azure.com).

---

# <a name="standard-sku"></a>[**Standardowy SKU**](#tab/option-1-create-load-balancer-standard)

>[!NOTE]
>Moduł równoważenia obciążenia w warstwie Standardowa jest zalecany w przypadku obciążeń produkcyjnych.  Aby uzyskać więcej informacji o jednostkach SKU, zobacz **[Azure Load Balancer SKU](skus.md)**.

:::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/resources-diagram.png" alt-text="Zasoby usługi równoważenia obciążenia w warstwie Standardowa utworzone w ramach szybkiego startu." border="false":::

*Ilustracja: zasoby utworzone w ramach szybkiego startu.*

W tej sekcji utworzysz moduł równoważenia obciążenia, który równoważy obciążenie maszyn wirtualnych. 

Podczas tworzenia publicznego modułu równoważenia obciążenia tworzony jest nowy publiczny adres IP skonfigurowany jako fronton (domyślnie **LoadBalancerFrontend** ) dla usługi równoważenia obciążenia.

1. Wybierz pozycję **Utwórz zasób**. 
2. W polu wyszukiwania wprowadź **moduł równoważenia obciążenia**. Wybierz pozycję **moduł równoważenia obciążenia** w wynikach wyszukiwania.
3. Na stronie **moduł równoważenia obciążenia** wybierz pozycję **Utwórz**.
4. Na stronie **Tworzenie modułu równoważenia obciążenia** wprowadź lub wybierz następujące informacje: 

    | Ustawienie                 | Wartość                                              |
    | ---                     | ---                                                |
    | Subskrypcja               | Wybierz subskrypcję.    |    
    | Grupa zasobów         | W polu tekstowym wybierz pozycję **Utwórz nową** i wprowadź **CreatePubLBQS-RG** .|
    | Nazwa                   | Wprowadź **myLoadBalancer**                                   |
    | Region (Region)         | Wybierz **(Europa) Europa Zachodnia**.                                        |
    | Typ          | Wybierz pozycję **Publiczna**.                                        |
    | SKU           | Pozostaw wartość domyślną **Standardowa**. |
    | Warstwa          | Pozostaw domyślne ustawienie **regionalne**. |
    | Publiczny adres IP | Wybierz pozycję **Utwórz nowy**. Jeśli masz istniejący publiczny adres IP, którego chcesz użyć, wybierz pozycję **Użyj istniejącej**. |
    | Nazwa publicznego adresu IP | Wpisz **myPublicIP** w polu tekstowym.|
    | Strefa dostępności | Wybierz opcję **strefa nadmiarowa** , aby utworzyć odporny moduł równoważenia obciążenia. Aby utworzyć strefowy moduł równoważenia obciążenia, wybierz określoną strefę z 1, 2 lub 3 |
    | Dodaj publiczny adres IPv6 | Wybierz pozycję **Nie**. </br> Aby uzyskać więcej informacji na temat adresów IPv6 i modułu równoważenia obciążenia, zobacz [co to jest protokół IPv6 dla platformy Azure Virtual Network?](../virtual-network/ipv6-overview.md)  |
    | Preferencja routingu | Pozostaw wartość domyślną **sieci Microsoft**. </br> Aby uzyskać więcej informacji o preferencjach routingu, zobacz [co to jest preferencja routingu (wersja zapoznawcza)?](../virtual-network/routing-preference-overview.md). |

5. Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **Przegląd + Utwórz**.

6. Na karcie **Recenzja i tworzenie** wybierz pozycję **Utwórz**.   
    
    :::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/create-standard-load-balancer.png" alt-text="Tworzenie modułu równoważenia obciążenia w warstwie Standardowa" border="true":::
 
## <a name="create-load-balancer-resources"></a>Tworzenie zasobów modułu równoważenia obciążenia

W tej sekcji skonfigurujesz:

* Ustawienia usługi równoważenia obciążenia dla puli adresów zaplecza.
* Sonda kondycji.
* Reguła modułu równoważenia obciążenia.

### <a name="create-a-backend-pool"></a>Tworzenie puli zaplecza

Pula adresów zaplecza zawiera adresy IP wirtualnych (kart sieciowych) podłączonych do modułu równoważenia obciążenia. 

Utwórz pulę adresów zaplecza **myBackendPool** , aby uwzględnić maszyny wirtualne na potrzeby ruchu internetowego związanego z równoważeniem obciążenia.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **Pule zaplecza**, a następnie wybierz pozycję **Dodaj**.

3. Na stronie **Dodawanie puli zaplecza** wpisz nazwę **myBackendPool**, jako nazwę puli zaplecza, a następnie wybierz pozycję **Dodaj**.

### <a name="create-a-health-probe"></a>Tworzenie sondy kondycji

Moduł równoważenia obciążenia monitoruje stan aplikacji przy użyciu sondy kondycji. 

Sonda kondycji dodaje lub usuwa maszyny wirtualne z modułu równoważenia obciążenia na podstawie odpowiedzi na testy kondycji. 

Utwórz sondę kondycji o nazwie **myHealthProbe**, aby monitorować kondycję maszyn wirtualnych.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **sondy kondycji**, a następnie wybierz pozycję **Dodaj**.
    
    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myHealthProbe**. |
    | Protokół | Wybierz pozycję **http**. |
    | Port | Wprowadź **80**.|
    | Interwał | Wprowadź **15** dla liczby **interwałów** (w sekundach) między kolejnymi próbami sondowania. |
    | Próg złej kondycji | Wybierz **2** dla liczby **progów złej kondycji** lub kolejnych niepowodzeń sondy, które muszą wystąpić, zanim maszyna wirtualna zostanie uznana za złą.|
    | | |

3. Pozostaw pozostałe wartości domyślne i wybierz **przycisk OK**.

### <a name="create-a-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia

Reguła modułu równoważenia obciążenia służy do definiowania sposobu dystrybucji ruchu do maszyn wirtualnych. Należy zdefiniować konfigurację adresu IP frontonu dla ruchu przychodzącego i pulę adresów IP zaplecza do odbierania ruchu. Port źródłowy i docelowy są zdefiniowane w regule. 

W tej sekcji utworzysz regułę modułu równoważenia obciążenia:

* O nazwie **myHTTPRule**.
* Na frontonie o nazwie **LoadBalancerFrontEnd**.
* Nasłuchiwanie na **porcie 80**.
* Kieruje ruch o zrównoważonym obciążeniu do zaplecza o nazwie **myBackendPool** na **porcie 80**.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **reguły równoważenia obciążenia**, a następnie wybierz pozycję **Dodaj**.

3. Użyj tych wartości, aby skonfigurować regułę równoważenia obciążenia:
    
    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myHTTPRule**. |
    | Wersja protokołu IP | Wybierz **protokół IPv4** |
    | Adres IP frontonu | Wybierz **LoadBalancerFrontEnd** |
    | Protokół | Wybierz pozycję **TCP**. |
    | Port | Wprowadź **80**.|
    | Port zaplecza | Wprowadź **80**. |
    | Pula zaplecza | Wybierz pozycję **myBackendPool**.|
    | Sonda kondycji | Wybierz pozycję **myHealthProbe**. |
    | Limit czasu bezczynności (minuty) | Przesuń suwak do **15** minut. |
    | Resetowanie protokołu TCP | Wybierz pozycję **Włączone**. |
    | Translacja adresów sieciowych dla ruchu wychodzącego (Resources) | Wybierz **(zalecane) Użyj reguł ruchu wychodzącego, aby zapewnić członkom puli zaplecza dostęp do Internetu.** |

4. Pozostaw pozostałe wartości domyślne, a następnie wybierz przycisk **OK**.

## <a name="create-backend-servers"></a>Tworzenie serwerów zaplecza

W tej sekcji omówiono następujące zagadnienia:

* Utwórz sieć wirtualną.
* Utwórz trzy maszyny wirtualne dla puli zaplecza modułu równoważenia obciążenia.
* Zainstaluj usługi IIS na maszynach wirtualnych w celu przetestowania modułu równoważenia obciążenia.

## <a name="create-the-virtual-network"></a>Tworzenie sieci wirtualnej

W tej sekcji utworzysz sieć wirtualną i podsieć.

1. W lewym górnym rogu ekranu wybierz pozycję **Utwórz zasób > Sieć > Sieć wirtualna** lub wyszukaj frazę **Sieć wirtualna** w polu wyszukiwania.

2. W obszarze **Utwórz sieć wirtualną** wprowadź lub wybierz te informacje na karcie **podstawowe** :

    | **Ustawienie**          | **Wartość**                                                           |
    |------------------|-----------------------------------------------------------------|
    | **Szczegóły projektu**  |                                                                 |
    | Subskrypcja     | Wybierz subskrypcję platformy Azure                                  |
    | Grupa zasobów   | Wybierz pozycję **CreatePubLBQS — RG** |
    | **Szczegóły wystąpienia** |                                                                 |
    | Nazwa             | Wprowadź **myVNet**                                    |
    | Region (Region)           | Wybierz **Europa Zachodnia** |

3. Wybierz kartę **adresy IP** lub wybierz przycisk **Dalej: adresy IP** w dolnej części strony.

4. Na karcie **adresy IP** wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Przestrzeń adresowa IPv4 | Wprowadź **10.1.0.0/16** |

5. W obszarze **Nazwa podsieci** wybierz pozycję **domyślny** wyraz.

6. W obszarze **Edytuj podsieć** wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Nazwa podsieci | Wprowadź **myBackendSubnet** |
    | Zakres adresów podsieci | Wprowadź **10.1.0.0/24** |

7. Wybierz pozycję **Zapisz**.

8. Wybierz kartę **zabezpieczenia** .

9. W obszarze **BastionHost** wybierz pozycję **enable (Włącz**). Wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Nazwa bastionu | Wprowadź **myBastionHost** |
    | Przestrzeń adresowa AzureBastionSubnet | Wprowadź **10.1.1.0/24** |
    | Publiczny adres IP | Wybierz pozycję **Utwórz nowy**. </br> W obszarze **Nazwa** wprowadź **myBastionIP**. </br> Wybierz przycisk **OK**. |


8. Wybierz kartę **Recenzja + tworzenie** lub wybierz przycisk **Recenzja + tworzenie** .

9. Wybierz przycisk **Utwórz**.

### <a name="create-virtual-machines"></a>Tworzenie maszyn wirtualnych

W tej sekcji utworzysz trzy maszyny wirtualne (**myVM1**, **myVM2** i **myVM3**) w trzech różnych strefach (**Strefa 1**, **strefa 2** i **strefa 3**). 

Te maszyny wirtualne są dodawane do puli zaplecza modułu równoważenia obciążenia, który został utworzony wcześniej.

1. W lewym górnym rogu portalu wybierz pozycję **Utwórz zasób**  >  **obliczeniowy**  >  **maszyny wirtualnej**. 
   
2. W obszarze **Utwórz maszynę wirtualną** wpisz lub wybierz wartości z karty **podstawowe** :

    | Ustawienie | Wartość                                          |
    |-----------------------|----------------------------------|
    | **Szczegóły projektu** |  |
    | Subskrypcja | Wybierz subskrypcję platformy Azure |
    | Grupa zasobów | Wybierz pozycję **CreatePubLBQS — RG** |
    | **Szczegóły wystąpienia** |  |
    | Nazwa maszyny wirtualnej | Wprowadź **myVM1** |
    | Region (Region) | Wybierz **Europa Zachodnia** |
    | Opcje dostępności | Wybierz **strefy dostępności** |
    | Strefa dostępności | Wybierz **1** |
    | Image (Obraz) | Wybierz pozycję **Windows Server 2019 Datacenter** |
    | Wystąpienie usługi Azure Spot | Wybierz pozycję **nie** |
    | Rozmiar | Wybierz rozmiar maszyny wirtualnej lub ustaw ustawienie domyślne |
    | **Konto administratora** |  |
    | Nazwa użytkownika | Wprowadź nazwę użytkownika |
    | Hasło | Wprowadź hasło |
    | Potwierdź hasło | Ponownie wprowadź hasło |
    | **Reguły portów ruchu przychodzącego** |  |
    | Publiczne porty wejściowe | Nie zaznaczaj **niczego** |

3. Wybierz kartę **Sieć** lub wybierz pozycję **Dalej: Dyski**, a następnie pozycję **Dalej: Sieć**.
  
4. Na karcie Sieć wybierz lub wprowadź:

    | Ustawienie | Wartość |
    |-|-|
    | **Interfejs sieciowy** |  |
    | Sieć wirtualna | **myVNet** |
    | Podsieć | **myBackendSubnet** |
    | Publiczny adres IP | Wybierz pozycję **Brak**. |
    | Grupa zabezpieczeń sieci karty sieciowej | Wybierz pozycję **Zaawansowane**|
    | Konfigurowanie sieciowej grupy zabezpieczeń | Wybierz pozycję **Utwórz nowy**. </br> W **grupie Tworzenie zabezpieczeń sieci** wprowadź **MyNSG** w polu **Nazwa**. </br> W obszarze **reguły ruchu przychodzącego** wybierz pozycję **+ Dodaj regułę ruchu przychodzącego**. </br> W obszarze  **zakresy portów docelowych** wprowadź **80**. </br> W obszarze **priorytet** wprowadź **100**. </br> W polu **Nazwa** wprowadź **myHTTPRule** </br> Wybierz pozycję **Dodaj**. </br> Wybierz przycisk **OK**. |
    | **Równoważenie obciążenia**  |
    | Umieścić tę maszynę wirtualną za istniejącym rozwiązaniem równoważenia obciążenia? | Wybierz pozycję **Tak** |
    | **Ustawienia równoważenia obciążenia** |
    | Opcje równoważenia obciążenia | Wybieranie **usługi Azure Load Balancing** |
    | Wybierz moduł równoważenia obciążenia | Wybierz **myLoadBalancer**  |
    | Wybierz pulę zaplecza | Wybierz **myBackendPool** |

5. Wybierz kartę **Zarządzanie** lub wybierz pozycję **Dalej** > **Zarządzanie**.

6. Na karcie **Zarządzanie** wybierz lub wprowadź:
    
    | Ustawienie | Wartość |
    |-|-|
    | **Monitorowanie** |  |
    | Diagnostyka rozruchu | Wybierz pozycję **wyłączone** |
   
7. Wybierz pozycję **Przejrzyj i utwórz**. 
  
8. Przejrzyj ustawienia, a następnie wybierz pozycję **Utwórz**.

9. Wykonaj kroki od 1 do 8, aby utworzyć dwie dodatkowe maszyny wirtualne z następującymi wartościami, a wszystkie inne ustawienia takie same jak **myVM1**:

    | Ustawienie | MW 2| MASZYNA WIRTUALNA 3|
    | ------- | ----- |---|
    | Nazwa |  **myVM2** |**myVM3**|
    | Strefa dostępności | **2** |**3**|
    | Sieciowa grupa zabezpieczeń | Wybierz istniejący **myNSG**| Wybierz istniejący **myNSG**|

## <a name="create-outbound-rule-configuration"></a>Utwórz konfigurację reguły ruchu wychodzącego
Reguły ruchu wychodzącego modułu równoważenia obciążenia Skonfiguruj wychodzące pliki zasad sieciowych dla maszyn wirtualnych w puli zaplecza. 

Aby uzyskać więcej informacji na temat połączeń wychodzących, zobacz [połączenia wychodzące na platformie Azure](load-balancer-outbound-connections.md).

### <a name="create-outbound-rule"></a>Utwórz regułę ruchu wychodzącego

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **reguły ruchu wychodzącego**, a następnie wybierz pozycję **Dodaj**.

3. Użyj tych wartości, aby skonfigurować reguły ruchu wychodzącego:

    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myOutboundRule**. |
    | Adres IP frontonu | Wybierz pozycję **Utwórz nowy**. </br> W polu **Nazwa** wprowadź **LoadBalancerFrontEndOutbound**. </br> Wybierz **adres IP** lub **prefiks IP**. </br> Wybierz pozycję **Utwórz nowy** w obszarze **publiczny adres IP** lub **publiczny prefiks adresu IP**. </br> W obszarze Nazwa wprowadź  **myPublicIPOutbound** lub **myPublicIPPrefixOutbound**. </br> Wybierz pozycję **Dodaj**.|
    | Limit czasu bezczynności (minuty) | Przesuń suwak do **15 minut**.|
    | Resetowanie protokołu TCP | Wybierz pozycję **Włączone**.|
    | Pula zaplecza | Wybierz pozycję **Utwórz nowy**. </br> Wprowadź **myBackendPoolOutbound** w polu **Nazwa**. </br> Wybierz pozycję **Dodaj**. |
    | Alokacja portu — alokacja portu > | Wybierz pozycję **ręcznie wybierz liczbę portów wychodzących** |
    | Porty wychodzące — > wybór | Wybierz **porty na wystąpienie** |
    | Porty wychodzące — porty > na wystąpienie | Wprowadź **10000**. |

4. Wybierz pozycję **Dodaj**.

### <a name="add-virtual-machines-to-outbound-pool"></a>Dodawanie maszyn wirtualnych do puli wychodzącej

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **Pule zaplecza**.

3. Wybierz pozycję **myBackendPoolOutbound**.

4. W obszarze **Sieć wirtualna** wybierz pozycję **myVNet**.

5. W obszarze **maszyny wirtualne** wybierz pozycję **+ Dodaj**.

6. Zaznacz pola wyboru obok pozycji **myVM1**, **myVM2** i **myVM3**. 

7. Wybierz pozycję **Dodaj**.

8. Wybierz pozycję **Zapisz**.

# <a name="basic-sku"></a>[**Podstawowy SKU**](#tab/option-1-create-load-balancer-basic)

>[!NOTE]
>Moduł równoważenia obciążenia w warstwie Standardowa jest zalecany w przypadku obciążeń produkcyjnych.  Aby uzyskać więcej informacji o jednostkach SKU, zobacz **[Azure Load Balancer SKU](skus.md)**.

:::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/resources-diagram-basic.png" alt-text="Zasoby podstawowego modułu równoważenia obciążenia utworzone w ramach szybkiego startu." border="false":::

*Ilustracja: zasoby utworzone w ramach szybkiego startu.*

W tej sekcji utworzysz moduł równoważenia obciążenia, który równoważy obciążenie maszyn wirtualnych. 

Podczas tworzenia publicznego modułu równoważenia obciążenia tworzony jest nowy publiczny adres IP skonfigurowany jako fronton (domyślnie **LoadBalancerFrontend** ) dla usługi równoważenia obciążenia.

1. Wybierz pozycję **Utwórz zasób**. 
2. W polu wyszukiwania wprowadź **moduł równoważenia obciążenia**. Wybierz pozycję **moduł równoważenia obciążenia** w wynikach wyszukiwania.
3. Na stronie **moduł równoważenia obciążenia** wybierz pozycję **Utwórz**.
4. Na stronie **Tworzenie modułu równoważenia obciążenia** wprowadź lub wybierz następujące informacje: 

    | Ustawienie                 | Wartość                                              |
    | ---                     | ---                                                |
    | Subskrypcja               | Wybierz subskrypcję.    |    
    | Grupa zasobów         | W polu tekstowym wybierz pozycję **Utwórz nową** i wpisz **CreatePubLBQS-RG** .|
    | Nazwa                   | Wprowadź **myLoadBalancer**                                   |
    | Region (Region)         | Wybierz pozycję **Europa Zachodnia**.                                        |
    | Typ          | Wybierz pozycję **Publiczna**.                                        |
    | SKU           | Wybierz pozycję **podstawowa** |
    | Publiczny adres IP | Wybierz pozycję **Utwórz nowy**. Jeśli masz istniejący publiczny adres IP, którego chcesz użyć, wybierz pozycję **Użyj istniejącej**. |
    | Nazwa publicznego adresu IP | Wpisz **myPublicIP** w polu tekstowym.|
    | Przypisanie | Wybierz **dynamiczny** |
    | Dodaj publiczny adres IPv6 | Wybierz pozycję **Nie**. </br> Aby uzyskać więcej informacji na temat adresów IPv6 i modułu równoważenia obciążenia, zobacz [co to jest protokół IPv6 dla platformy Azure Virtual Network?](../virtual-network/ipv6-overview.md)  |

5. Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **Przegląd + Utwórz**.

6. Na karcie **Recenzja i tworzenie** wybierz pozycję **Utwórz**.   

    :::image type="content" source="./media/quickstart-load-balancer-standard-public-portal/create-basic-load-balancer.png" alt-text="Tworzenie podstawowego modułu równoważenia obciążenia" border="true":::

## <a name="create-load-balancer-resources"></a>Tworzenie zasobów modułu równoważenia obciążenia

W tej sekcji skonfigurujesz:

* Utwórz sieć wirtualną.
* Ustawienia usługi równoważenia obciążenia dla puli adresów zaplecza.
* Sonda kondycji.
* Reguła modułu równoważenia obciążenia.

## <a name="create-the-virtual-network"></a>Tworzenie sieci wirtualnej

W tej sekcji utworzysz sieć wirtualną i podsieć.

1. W lewym górnym rogu ekranu wybierz pozycję **Utwórz zasób > Sieć > Sieć wirtualna** lub wyszukaj frazę **Sieć wirtualna** w polu wyszukiwania.

2. W obszarze **Utwórz sieć wirtualną** wprowadź lub wybierz te informacje na karcie **podstawowe** :

    | **Ustawienie**          | **Wartość**                                                           |
    |------------------|-----------------------------------------------------------------|
    | **Szczegóły projektu**  |                                                                 |
    | Subskrypcja     | Wybierz subskrypcję platformy Azure                                  |
    | Grupa zasobów   | Wybierz pozycję **CreatePubLBQS — RG** |
    | **Szczegóły wystąpienia** |                                                                 |
    | Nazwa             | Wprowadź **myVNet**                                    |
    | Region (Region)           | Wybierz **Europa Zachodnia** |

3. Wybierz kartę **adresy IP** lub wybierz przycisk **Dalej: adresy IP** w dolnej części strony.

4. Na karcie **adresy IP** wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Przestrzeń adresowa IPv4 | Wprowadź **10.1.0.0/16** |

5. W obszarze **Nazwa podsieci** wybierz pozycję **domyślny** wyraz.

6. W obszarze **Edytuj podsieć** wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Nazwa podsieci | Wprowadź **myBackendSubnet** |
    | Zakres adresów podsieci | Wprowadź **10.1.0.0/24** |

7. Wybierz pozycję **Zapisz**.

8. Wybierz kartę **zabezpieczenia** .

9. W obszarze **BastionHost** wybierz pozycję **enable (Włącz**). Wprowadź następujące informacje:

    | Ustawienie            | Wartość                      |
    |--------------------|----------------------------|
    | Nazwa bastionu | Wprowadź **myBastionHost** |
    | Przestrzeń adresowa AzureBastionSubnet | Wprowadź **10.1.1.0/24** |
    | Publiczny adres IP | Wybierz pozycję **Utwórz nowy**. </br> W obszarze **Nazwa** wprowadź **myBastionIP**. </br> Wybierz przycisk **OK**. |


8. Wybierz kartę **Recenzja + tworzenie** lub wybierz przycisk **Recenzja + tworzenie** .

9. Wybierz przycisk **Utwórz**.
### <a name="create-a-backend-pool"></a>Tworzenie puli zaplecza

Pula adresów zaplecza zawiera adresy IP wirtualnych (kart sieciowych) podłączonych do modułu równoważenia obciążenia. 

Utwórz pulę adresów zaplecza **myBackendPool** , aby uwzględnić maszyny wirtualne na potrzeby ruchu internetowego związanego z równoważeniem obciążenia.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **Pule zaplecza**, a następnie wybierz pozycję **Dodaj**.

3. Na stronie **Dodawanie puli zaplecza** wprowadź lub wybierz:
    
    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myBackendPool**. |
    | Sieć wirtualna | Wybierz pozycję **myVNet**. |
    | Skojarzone z | Wybierz **maszyny wirtualne** |

### <a name="create-a-health-probe"></a>Tworzenie sondy kondycji

Moduł równoważenia obciążenia monitoruje stan aplikacji przy użyciu sondy kondycji. 

Sonda kondycji dodaje lub usuwa maszyny wirtualne z modułu równoważenia obciążenia na podstawie odpowiedzi na testy kondycji. 

Utwórz sondę kondycji o nazwie **myHealthProbe**, aby monitorować kondycję maszyn wirtualnych.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **sondy kondycji**, a następnie wybierz pozycję **Dodaj**.
    
    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myHealthProbe**. |
    | Protokół | Wybierz pozycję **http**. |
    | Port | Wprowadź **80**.|
    | Ścieżka | Wejść **/** |
    | Interwał | Wprowadź **15** dla liczby **interwałów** (w sekundach) między kolejnymi próbami sondowania. |
    | Próg złej kondycji | Wybierz **2** dla liczby **progów złej kondycji** lub kolejnych niepowodzeń sondy, które muszą wystąpić, zanim maszyna wirtualna zostanie uznana za złą.|

3. Wybierz przycisk **OK**.

### <a name="create-a-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia

Reguła modułu równoważenia obciążenia służy do definiowania sposobu dystrybucji ruchu do maszyn wirtualnych. Należy zdefiniować konfigurację adresu IP frontonu dla ruchu przychodzącego i pulę adresów IP zaplecza do odbierania ruchu. Port źródłowy i docelowy są zdefiniowane w regule. 

W tej sekcji utworzysz regułę modułu równoważenia obciążenia:

* O nazwie **myHTTPRule**.
* Na frontonie o nazwie **LoadBalancerFrontEnd**.
* Nasłuchiwanie na **porcie 80**.
* Kieruje ruch o zrównoważonym obciążeniu do zaplecza o nazwie **myBackendPool** na **porcie 80**.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **reguły równoważenia obciążenia**, a następnie wybierz pozycję **Dodaj**.

3. Użyj tych wartości, aby skonfigurować regułę równoważenia obciążenia:
    
    | Ustawienie | Wartość |
    | ------- | ----- |
    | Nazwa | Wprowadź **myHTTPRule**. |
    | Wersja protokołu IP | Wybierz **protokół IPv4** |
    | Adres IP frontonu | Wybierz **LoadBalancerFrontEnd** |
    | Protokół | Wybierz pozycję **TCP**. |
    | Port | Wprowadź **80**.|
    | Port zaplecza | Wprowadź **80**. |
    | Pula zaplecza | Wybierz pozycję **myBackendPool**.|
    | Sonda kondycji | Wybierz pozycję **myHealthProbe**. |
    | Limit czasu bezczynności (minuty) | Przesuń suwak do **15** minut. |
 
4. Pozostaw pozostałe wartości domyślne, a następnie wybierz przycisk **OK**.

## <a name="create-backend-servers"></a>Tworzenie serwerów zaplecza

W tej sekcji omówiono następujące zagadnienia:

* Utwórz trzy maszyny wirtualne dla puli zaplecza modułu równoważenia obciążenia.
* Utwórz zestaw dostępności dla maszyn wirtualnych.
* Zainstaluj usługi IIS na maszynach wirtualnych w celu przetestowania modułu równoważenia obciążenia.

### <a name="create-virtual-machines"></a>Tworzenie maszyn wirtualnych

W tej sekcji utworzysz trzy maszyny wirtualne (**myVM1**, **myVM2** i **myVM3**) z podstawowym publicznym adresem IP.  

Trzy maszyny wirtualne zostaną dodane do zestawu dostępności o nazwie **myAvailabilitySet**.

Te maszyny wirtualne są dodawane do puli zaplecza modułu równoważenia obciążenia, który został utworzony wcześniej.

1. W lewym górnym rogu portalu wybierz pozycję **Utwórz zasób**  >  **obliczeniowy**  >  **maszyny wirtualnej**. 
   
2. W obszarze **Utwórz maszynę wirtualną** wpisz lub wybierz wartości z karty **podstawowe** :

    | Ustawienie | Wartość                                          |
    |-----------------------|----------------------------------|
    | **Szczegóły projektu** |  |
    | Subskrypcja | Wybierz subskrypcję platformy Azure |
    | Grupa zasobów | Wybierz pozycję **CreatePubLBQS — RG** |
    | **Szczegóły wystąpienia** |  |
    | Nazwa maszyny wirtualnej | Wprowadź **myVM1** |
    | Region (Region) | Wybierz **Europa Zachodnia** |
    | Opcje dostępności | Wybierz pozycję **Zestaw dostępności** |
    | Zestaw dostępności | Wybierz pozycję **Utwórz nowy**. </br> Wprowadź **myAvailabilitySet** w polu **Nazwa**. </br> Wybierz przycisk **OK**. |
    | Image (Obraz) | **Windows Server 2019 Datacenter** |
    | Wystąpienie usługi Azure Spot | Wybierz pozycję **nie** |
    | Rozmiar | Wybierz rozmiar maszyny wirtualnej lub ustaw ustawienie domyślne |
    | **Konto administratora** |  |
    | Nazwa użytkownika | Wprowadź nazwę użytkownika |
    | Hasło | Wprowadź hasło |
    | Potwierdź hasło | Ponownie wprowadź hasło |

3. Wybierz kartę **Sieć** lub wybierz pozycję **Dalej: Dyski**, a następnie pozycję **Dalej: Sieć**.
  
4. Na karcie Sieć wybierz lub wprowadź:

    | Ustawienie | Wartość |
    |-|-|
    | **Interfejs sieciowy** |  |
    | Sieć wirtualna | Wybierz **myVNet** |
    | Podsieć | Wybierz **myBackendSubnet** |
    | Publiczny adres IP | Nie zaznaczaj **niczego** |
    | Grupa zabezpieczeń sieci karty sieciowej | Wybierz pozycję **Zaawansowane**|
    | Konfigurowanie sieciowej grupy zabezpieczeń | Wybierz pozycję **Utwórz nowy**. </br> W **grupie Tworzenie zabezpieczeń sieci** wprowadź **MyNSG** w polu **Nazwa**. </br> W obszarze **reguły ruchu przychodzącego** wybierz pozycję **+ Dodaj regułę ruchu przychodzącego**. </br> W obszarze  **zakresy portów docelowych** wprowadź **80**. </br> W obszarze **priorytet** wprowadź **100**. </br> W polu **Nazwa** wprowadź **myHTTPRule** </br> Wybierz pozycję **Dodaj**. </br> Wybierz przycisk **OK**. |
    | **Równoważenie obciążenia**  |
    | Umieścić tę maszynę wirtualną za istniejącym rozwiązaniem równoważenia obciążenia? | Wybierz pozycję **nie** |
 
5. Wybierz kartę **Zarządzanie** lub wybierz pozycję **Dalej** > **Zarządzanie**.

6. Na karcie **Zarządzanie** wybierz lub wprowadź:
    
    | Ustawienie | Wartość |
    |---|---|
    | **Monitorowanie** | |
    | Diagnostyka rozruchu | Wybierz pozycję **wyłączone** |

7. Wybierz pozycję **Przejrzyj i utwórz**. 
  
8. Przejrzyj ustawienia, a następnie wybierz pozycję **Utwórz**.

9. Wykonaj kroki od 1 do 8, aby utworzyć dwie dodatkowe maszyny wirtualne z następującymi wartościami, a wszystkie inne ustawienia takie same jak **myVM1**:

    | Ustawienie | MW 2| MASZYNA WIRTUALNA 3|
    | ------- | ----- |---|
    | Nazwa |  **myVM2** |**myVM3**|
    | Zestaw dostępności| Wybierz **myAvailabilitySet** | Wybierz **myAvailabilitySet**|
    | Sieciowa grupa zabezpieczeń | Wybierz istniejący **myNSG**| Wybierz istniejący **myNSG**|

### <a name="add-virtual-machines-to-the-backend-pool"></a>Dodawanie maszyn wirtualnych do puli zaplecza

Maszyny wirtualne utworzone w poprzednich krokach należy dodać do puli zaplecza **myLoadBalancer**.

1. W menu po lewej stronie wybierz pozycję Wszystkie **usługi** , wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myLoadBalancer** z listy zasoby.

2. W obszarze **Ustawienia** wybierz pozycję **Pule zaplecza**, a następnie wybierz pozycję **myBackendPool**.

3. Wybierz **maszyny wirtualne** **powiązane** z.

4. W sekcji **maszyny wirtualne** wybierz pozycję **+ Dodaj**.

5. Zaznacz pola obok pozycji **myVM1**, **myVM2** i **myVM3**.

6. Wybierz pozycję **Dodaj**.

7. Wybierz pozycję **Zapisz**.

---

## <a name="install-iis"></a>Instalowanie usług IIS

1. Wybierz pozycję **wszystkie usługi** w menu po lewej stronie, wybierz pozycję **wszystkie zasoby**, a następnie na liście zasobów wybierz pozycję **myVM1** , która znajduje się w grupie zasobów **CreatePubLBQS-RG** .

2. Na stronie **Przegląd** wybierz opcję **Połącz**, a następnie **bastionu**.

4. Wprowadź nazwę użytkownika i hasło wprowadzone podczas tworzenia maszyny wirtualnej.

5. Wybierz pozycję **Połącz**.

6. Na pulpicie serwera przejdź do **narzędzi administracyjnych systemu Windows**  >  **programu Windows PowerShell**.

7. W oknie programu PowerShell uruchom następujące polecenia, aby:

    * Zainstaluj serwer IIS
    * Usuń domyślny plik iisstart.htm
    * Dodaj nowy plik iisstart.htm, który wyświetla nazwę maszyny wirtualnej:

   ```powershell
    
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add a new htm file that displays server name
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
   ```
8. Zamknij sesję bastionu z **myVM1**.

9. Powtórz kroki od 1 do 6, aby zainstalować usługi IIS i zaktualizowany plik iisstart.htm na maszynach **myVM2** i **myVM3**.

## <a name="test-the-load-balancer"></a>Testowanie modułu równoważenia obciążenia

1. Znajdź publiczny adres IP dla usługi Load Balancer na ekranie **Przegląd**. Wybierz pozycję **wszystkie usługi** w menu po lewej stronie, wybierz pozycję **wszystkie zasoby**, a następnie wybierz pozycję **myPublicIP**.

2. Skopiuj publiczny adres IP, a następnie wklej go na pasku adresu przeglądarki. W przeglądarce jest wyświetlana domyślna strona internetowego serwera usług IIS.

   ![Internetowy serwer usług IIS](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

Aby zobaczyć, jak moduł równoważenia obciążenia dystrybuuje ruch między wszystkimi trzema maszynami wirtualnymi, można dostosować domyślną stronę każdego z serwerów sieci Web usług IIS na maszynie wirtualnej, a następnie wymusić odświeżenie przeglądarki sieci Web na komputerze klienckim.

## <a name="clean-up-resources"></a>Czyszczenie zasobów

Gdy grupa zasobów, moduł równoważenia obciążenia i wszystkie pokrewne zasoby nie będą już potrzebne, usuń je. W tym celu wybierz grupę zasobów **CreatePubLBQS-RG** , która zawiera zasoby, a następnie wybierz pozycję **Usuń**.

## <a name="next-steps"></a>Następne kroki

W ramach tego przewodnika Szybki start wykonasz następujące czynności:

* Utworzono Load Balancer platformy Azure w warstwie Standardowa lub podstawowa
* Dołączono 3 maszyny wirtualne do modułu równoważenia obciążenia.
* Skonfigurowano regułę ruchu modułu równoważenia obciążenia, sondę kondycji, a następnie przetestowano moduł równoważenia obciążenia. 

Aby dowiedzieć się więcej na temat Azure Load Balancer, przejdź do:
> [!div class="nextstepaction"]
> [Co to jest usługa Azure Load Balancer?](load-balancer-overview.md)