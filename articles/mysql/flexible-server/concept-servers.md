---
title: Pojęcia dotyczące serwera — Azure Database for MySQL elastyczny serwer
description: W tym temacie przedstawiono zagadnienia i wskazówki dotyczące pracy z Azure Database for MySQL elastycznym serwerze
author: mksuni
ms.author: sumuth
ms.service: mysql
ms.topic: conceptual
ms.date: 09/21/2020
ms.openlocfilehash: b664dd406a1ab90b4ea5e85005a69935f345c609
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102034663"
---
# <a name="server-concepts-in-azure-database-for-mysql-flexible-server-preview"></a>Pojęcia dotyczące serwerów w Azure Database for MySQL elastycznym serwerze (wersja zapoznawcza)

> [!IMPORTANT] 
> Serwer elastyczny Azure Database for MySQL jest obecnie w publicznej wersji zapoznawczej.

W tym artykule przedstawiono zagadnienia i wytyczne dotyczące pracy z serwerami elastycznymi Azure Database for MySQL.

## <a name="what-is-an-azure-database-for-mysql-flexible-server"></a>Co to jest Azure Database for MySQL elastyczny serwer?

Azure Database for MySQL elastyczny serwer to w pełni zarządzana usługa bazy danych, w której działa wersja społeczności MySQL. Ogólnie rzecz biorąc, usługa została zaprojektowana pod kątem zapewniania elastyczności i dostosowywania konfiguracji na podstawie wymagań użytkownika. Jest to ta sama konstrukcja serwera MySQL, która może być znana na świecie lokalnym. W odróżnieniu od tego, elastyczny serwer jest zarządzany, umożliwia korzystanie z wydajności systemu, lepszej zarządzania serwerem i kontroli oraz udostępnia dostęp i funkcje na poziomie serwera.

Serwer elastyczny Azure Database for MySQL:

- Jest tworzony w ramach subskrypcji platformy Azure.
- Jest zasobem nadrzędnym dla baz danych.
- Zezwala na korzystanie z konfiguracji MySQL przez parametry serwera (łącze do pojęć dotyczących parametrów serwera).
- Wykonuje automatyczne kopie zapasowe i obsługuje przywracanie do punktu w czasie.
- Udostępnia przestrzeń nazw dla baz danych.
- Jest kontenerem z semantyką silnego okresu istnienia — usuwa serwer i usuwa zawarte bazy danych.
- Kolokacja zasobów w regionie.
- Obsługa harmonogramu konserwacji serwera dla klienta
- Możliwość wdrażania elastycznych serwerów w strefie nadmiarowej konfiguracji w celu zwiększenia wysokiej dostępności
- Zapewnia integrację sieci wirtualnej na potrzeby dostępu do serwera bazy danych
- Zapewnia sposób oszczędzania kosztów, zatrzymując serwer elastyczny, gdy nie jest używany
- Zapewnia zakres zasad zarządzania, które mają zastosowanie do swoich baz danych: logowania, zapory, użytkowników, ról, konfiguracji itp.
- Obsługuje wersje główne programu MySQL 5,7 i MySQL 8,0. Aby uzyskać więcej informacji, zobacz [obsługiwane wersje aparatów Azure Database for MySQL](./../concepts-supported-versions.md).

Na serwerze elastycznym Azure Database for MySQL można utworzyć jedną lub wiele baz danych. Możesz wybrać opcję tworzenia pojedynczej bazy danych na serwerze w celu używania wszystkich zasobów lub tworzenia wielu baz danych w celu udostępniania zasobów. Cennik jest uporządkowany według serwera w oparciu o konfigurację warstwy obliczeniowej, rdzeni wirtualnych i magazynu (GB). Aby uzyskać więcej informacji, zobacz artykuł [Obliczanie i magazynowanie](./concepts-compute-storage.md).

## <a name="stopstart-an-azure-database-for-mysql-flexible-server"></a>Zatrzymaj/Uruchom Azure Database for MySQL elastyczny serwer

Azure Database for MySQL elastyczny serwer umożliwia **zatrzymanie** serwera, gdy nie jest używany, i **uruchomienie** serwera podczas wznawiania działania. Ma to na celu zaoszczędzenie kosztów na serwerach bazy danych i płatność tylko za zasób, gdy jest używany. Jest to jeszcze ważniejsze w przypadku obciążeń deweloperskich i testowych, a w przypadku korzystania z serwera tylko dla części dnia. Po zatrzymaniu serwera wszystkie aktywne połączenia zostaną usunięte. Później, jeśli chcesz przywrócić serwer do trybu online, możesz użyć [Azure Portal](how-to-stop-start-server-portal.md) lub interfejsu wiersza polecenia.

Gdy serwer jest w stanie **zatrzymania** , obliczenia serwera nie są naliczane. Magazyn jest jednak nadal rozliczany jako magazyn serwera, aby zapewnić dostępność plików danych po ponownym uruchomieniu serwera.

> [!IMPORTANT]
> **Zatrzymanie** serwera pozostanie w tym stanie w ciągu następnych 7 dni w rozciągnięciu. Jeśli nie **uruchomisz** go ręcznie w tym czasie, serwer zostanie automatycznie uruchomiony po upływie 7 dni. Jeśli nie używasz serwera, możesz go **zatrzymać** ponownie.

Gdy serwer czasu zostanie zatrzymany, na serwerze nie można wykonać żadnych operacji zarządzania. Aby zmienić ustawienia konfiguracji na serwerze, należy [uruchomić serwer](how-to-stop-start-server-portal.md). Zapoznaj się z [ograniczeniami Zatrzymaj/Rozpocznij](./concepts-limitations.md#stopstart-operation).

## <a name="how-do-i-manage-a-server"></a>Jak mogę zarządzać serwerem?

Można zarządzać Azure Database for MySQL elastycznym serwerze przy użyciu [Azure Portal](./quickstart-create-server-portal.md) lub [interfejsu wiersza polecenia platformy Azure](./quickstart-create-server-cli.md).

## <a name="next-steps"></a>Następne kroki

-   Dowiedz się więcej o [tworzeniu serwera](./quickstart-create-server-portal.md)
-   Informacje o [monitorowaniu i alertach](./how-to-alert-on-metric.md)

