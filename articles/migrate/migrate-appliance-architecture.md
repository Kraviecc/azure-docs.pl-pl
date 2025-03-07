---
title: Architektura urządzenia usługi Azure Migrate
description: Zawiera omówienie urządzenia Azure Migrate używanego w ocenie i migracji serwera.
author: vikram1988
ms.author: vibansa
ms.manager: abhemraj
ms.topic: conceptual
ms.date: 06/09/2020
ms.openlocfilehash: d695758849fd4f7e6f595820221f6b8606fe7cf1
ms.sourcegitcommit: 4b7a53cca4197db8166874831b9f93f716e38e30
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102096194"
---
# <a name="azure-migrate-appliance-architecture"></a>Architektura urządzenia usługi Azure Migrate

W tym artykule opisano architekturę i procesy urządzeń Azure Migrate. Urządzenie Azure Migrate jest lekkim urządzeniem wdrożonym lokalnie, aby odnajdywać maszyny wirtualne i serwery fizyczne do migracji na platformę Azure.

## <a name="deployment-scenarios"></a>Scenariusze wdrażania

Urządzenie Azure Migrate jest używane w następujących scenariuszach.

**Scenariusz** | **Narzędzie** | **Używane do** 
--- | --- | ---
**Odnajdywanie i ocenianie serwerów działających w środowisku VMware** | Azure Migrate: Ocena serwera | Odnajdź serwery działające w środowisku programu VMware<br/><br/> Wykonaj odnajdywanie zainstalowanych aplikacji, analizy zależności bez agenta i odnajdź SQL Server wystąpienia i bazy danych.<br/><br/> Zbieranie informacji o konfiguracji serwera i metadanych wydajności dla ocen.
**Migracja serwerów z systemem w środowisku VMware bez wykorzystania agentów** | Azure Migrate: Migracja serwera | Odnajdź serwery działające w środowisku programu VMware.<br/><br/> Replikowanie serwerów bez instalowania na nich agentów.
**Odnajdywanie i ocenianie serwerów działających w środowisku funkcji Hyper-V** | Azure Migrate: Ocena serwera | Odnajdź serwery działające w środowisku funkcji Hyper-V.<br/><br/> Zbieranie informacji o konfiguracji serwera i metadanych wydajności dla ocen.
**Odnajdywanie i ocenianie serwerów fizycznych lub zwirtualizowanych lokalnie** |  Azure Migrate: Ocena serwera |  Odnajdywanie serwerów fizycznych lub zwirtualizowanych lokalnie.<br/><br/> Zbieranie informacji o konfiguracji serwera i metadanych wydajności dla ocen.

## <a name="deployment-methods"></a>Metody wdrażania

Urządzenie można wdrożyć przy użyciu kilku metod:

- Urządzenie można wdrożyć przy użyciu szablonu dla serwerów działających w środowisku VMware lub funkcji Hyper-V ([szablon komórki jajowe dla oprogramowania VMware](how-to-set-up-appliance-vmware.md) lub [wirtualnego dysku twardego dla funkcji Hyper-v](how-to-set-up-appliance-hyper-v.md)).
- Jeśli nie chcesz używać szablonu, możesz wdrożyć urządzenie dla środowiska VMware lub funkcji Hyper-V przy użyciu [skryptu Instalatora programu PowerShell](deploy-appliance-script.md).
- W Azure Government należy wdrożyć urządzenie przy użyciu skryptu Instalatora programu PowerShell. W [tym miejscu](deploy-appliance-script-government.md)zapoznaj się z krokami wdrożenia.
- W przypadku serwerów fizycznych lub zwirtualizowanych lokalnie lub w innych chmurach urządzenie jest zawsze wdrażane przy użyciu skryptu Instalatora programu PowerShell. W [tym miejscu](how-to-set-up-appliance-physical.md)zapoznaj się z krokami wdrożenia.
- Linki do pobrania są dostępne w poniższych tabelach.

## <a name="appliance-services"></a>Usługi urządzeń

Urządzenie ma następujące usługi:

- **Menedżer konfiguracji urządzenia**: jest to aplikacja sieci Web, która może być skonfigurowana ze szczegółowymi informacjami na temat uruchamiania odnajdywania i oceny serwerów. 
- **Agent odnajdywania**: Agent zbiera metadane konfiguracji serwera, których można użyć do utworzenia jako oceny lokalne.
- **Agent oceny**: Agent zbiera metadane wydajności serwera, których można użyć do tworzenia ocen opartych na wydajności.
- **Usługa autoaktualizacji**: usługa utrzymuje wszystkie agenci uruchomione na urządzeniu. Jest ona automatycznie uruchamiana co 24 godziny.
- **Agent dra**: organizuje replikację serwera i koordynuje komunikację między replikowanymi serwerami i platformą Azure. Używane tylko w przypadku replikowania serwerów na platformę Azure przy użyciu migracji bez wykorzystania agentów.
- **Brama**: wysyła zreplikowane dane na platformę Azure. Używane tylko w przypadku replikowania serwerów na platformę Azure przy użyciu migracji bez wykorzystania agentów.
- **Agent odnajdywania i oceny SQL**: wysyła metadane konfiguracji i wydajności SQL Server wystąpień i baz danych na platformę Azure.

> [!Note]
> Ostatnie 3 usługi są dostępne tylko na urządzeniu używanym do odnajdywania i oceny serwerów działających w środowisku programu VMware.<br/> Odnajdywanie i Ocena SQL Server wystąpień i baz danych działających w środowisku VMware jest teraz w wersji zapoznawczej. Aby wypróbować tę funkcję, użyj [**tego linku**](https://aka.ms/AzureMigrate/SQL) , aby utworzyć projekt w regionie **Australia Wschodnia** . Jeśli masz już projekt w Australii wschodniej i chcesz wypróbować tę funkcję, upewnij się, że zostały spełnione [**wymagania wstępne**](how-to-discover-sql-existing-project.md) w portalu.


## <a name="discovery-and-collection-process"></a>Proces odnajdywania i kolekcjonowania

:::image type="content" source="./media/migrate-appliance-architecture/architecture1.png" alt-text="Architektura urządzenia":::

Urządzenie komunikuje się ze źródłami odnajdywania przy użyciu następującego procesu.

**Proces** | **Urządzenie VMware** | **Urządzenie funkcji Hyper-V** | **Urządzenie fizyczne**
---|---|---|---
**Rozpocznij odnajdowanie** | Urządzenie domyślnie komunikuje się z serwerem vCenter Server na porcie TCP 443. Jeśli serwer vCenter nasłuchuje na innym porcie, można go skonfigurować w Menedżerze konfiguracji urządzenia. | Urządzenie komunikuje się z hostami funkcji Hyper-V na porcie WinRM 5985 (HTTP). | Urządzenie komunikuje się z serwerami z systemem Windows za pośrednictwem portu WinRM 5985 (HTTP) z serwerami z systemem Linux za pośrednictwem portu 22 (TCP).
**Zbieranie metadanych dotyczących konfiguracji i wydajności** | Urządzenie zbiera metadane serwerów działających na vCenter Server przy użyciu interfejsów API vSphere przez połączenie się z portem 443 (port domyślny) lub dowolnego innego portu, vCenter Server nasłuchuje. | Urządzenie zbiera metadane serwerów uruchomionych na hostach funkcji Hyper-V przy użyciu sesji model wspólnych informacji (CIM) z hostami na porcie 5985.| Urządzenie zbiera metadane z serwerów z systemem Windows przy użyciu sesji model wspólnych informacji (CIM) z serwerami na porcie 5985 i z serwerów z systemem Linux przy użyciu łączności SSH na porcie 22.
**Wyślij dane odnajdywania** | Urządzenie wysyła zebrane dane do Azure Migrate: Ocena serwera i Azure Migrate: Migracja serwera przez Port SSL 443.<br/><br/> Urządzenie może nawiązać połączenie z platformą Azure za pośrednictwem Internetu lub za pośrednictwem ExpressRoute (wymaga komunikacji równorzędnej firmy Microsoft). | Urządzenie wysyła zebrane dane do Azure Migrate: Ocena serwera przez Port SSL 443.<br/><br/> Urządzenie może nawiązać połączenie z platformą Azure za pośrednictwem Internetu lub za pośrednictwem ExpressRoute (wymaga komunikacji równorzędnej firmy Microsoft).| Urządzenie wysyła zebrane dane do Azure Migrate: Ocena serwera przez Port SSL 443.<br/><br/> Urządzenie może nawiązać połączenie z platformą Azure za pośrednictwem Internetu lub za pośrednictwem ExpressRoute (wymaga komunikacji równorzędnej firmy Microsoft).
**Częstotliwość zbierania danych** | Metadane konfiguracji są zbierane i wysyłane co 30 minut. <br/><br/> Metadane wydajności są zbierane co 20 sekund i są agregowane w celu wysyłania punktów danych do platformy Azure co 10 minut. <br/><br/> Dane spisu oprogramowania są wysyłane do platformy Azure co 12 godzin. <br/><br/> Dane zależności bez agenta są zbierane co 5 minut, agregowane na urządzeniu i wysyłane do platformy Azure co 6 godzin. <br/><br/> Dane konfiguracji SQL Server są aktualizowane co 24 godziny, a dane wydajności są przechwytywane co 30 sekund.| Metadane konfiguracji są zbierane i wysyłane co 30 minut. <br/><br/> Metadane wydajności są zbierane co 30 sekund i są agregowane w celu wysyłania punktów danych do platformy Azure co 10 minut.|  Metadane konfiguracji są zbierane i wysyłane co 30 minut. <br/><br/> Metadane wydajności są zbierane co 5 minut i są agregowane w celu wysyłania punktów danych do platformy Azure co 10 minut.
**Ocenianie i migrowanie** | Możesz tworzyć oceny z metadanych zebranych przez urządzenie przy użyciu Azure Migrate: narzędzia do oceny serwera.<br/><br/>Ponadto można również rozpocząć Migrowanie serwerów z systemem w środowisku VMware przy użyciu Azure Migrate: Narzędzia migracji serwera do organizowania replikacji serwera bez agentów.| Możesz tworzyć oceny z metadanych zebranych przez urządzenie przy użyciu Azure Migrate: narzędzia do oceny serwera. | Możesz tworzyć oceny z metadanych zebranych przez urządzenie przy użyciu Azure Migrate: narzędzia do oceny serwera.

## <a name="next-steps"></a>Następne kroki

[Zapoznaj](migrate-appliance.md) się z matrycą obsługi urządzeń.