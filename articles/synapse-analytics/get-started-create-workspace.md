---
title: 'Szybki Start: wprowadzenie — Tworzenie obszaru roboczego Synapse'
description: W tym samouczku dowiesz się, jak utworzyć obszar roboczy Synapse, dedykowaną pulę SQL i bezserwerową pulę Apache Spark.
services: synapse-analytics
author: saveenr
ms.author: saveenr
manager: julieMSFT
ms.reviewer: jrasnick
ms.service: synapse-analytics
ms.subservice: workspace
ms.topic: tutorial
ms.date: 12/31/2020
ms.openlocfilehash: 94d069a283249f2880743ba911c32bf3821d28c8
ms.sourcegitcommit: 24a12d4692c4a4c97f6e31a5fbda971695c4cd68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171487"
---
# <a name="creating-a-synapse-workspace"></a>Tworzenie obszaru roboczego Synapse

W tym samouczku dowiesz się, jak utworzyć obszar roboczy Synapse, dedykowaną pulę SQL i bezserwerową pulę Apache Spark. 

## <a name="prerequisites"></a>Wymagania wstępne

Aby wykonać kroki tego samouczka, musisz mieć dostęp do grupy zasobów, do której przypisano rolę **właściciela** . Utwórz obszar roboczy Synapse w tej grupie zasobów.

## <a name="create-a-synapse-workspace-in-the-azure-portal"></a>Utwórz obszar roboczy Synapse w Azure Portal

1. Otwórz [Azure Portal](https://portal.azure.com), na pasku wyszukiwania wprowadź **Synapse** bez naciśnięcia klawisza ENTER.
1. W wynikach wyszukiwania w obszarze **usługi** wybierz pozycję **Azure Synapse Analytics**.
1. Wybierz pozycję **Dodaj** , aby utworzyć obszar roboczy.
1. Karta **podstawy** , w obszarze **szczegóły projektu**, wypełnij następujące pola:
      1. **Subskrypcja** — wybierz dowolną subskrypcję.
      2. **Grupa zasobów** — Użyj dowolnej grupy zasobów.
      3. **Grupa zasobów** — pozostaw to pole puste.
1. Na karcie **podstawy** w obszarze **szczegóły obszaru roboczego** wypełnij następujące pola:
      1. **Nazwa obszaru roboczego** — wybierz dowolną globalnie unikatową nazwę. W tym samouczku użyjemy **obszaru roboczego**.
      1. **Region** — wybierz dowolny region.
      1. **Wybieranie Data Lake Storage Gen 2**
        1. Kliknij przycisk **z subskrypcji**.
        1. Według **nazwy konta**, kliknij przycisk **Utwórz nowe** i Nazwij nowe konto magazynu **contosolake** lub podobną, ponieważ ta nazwa musi być unikatowa.
        1. Według **nazwy systemu plików**, kliknij przycisk **Utwórz nowe** i nadaj nazwę **użytkownikom** IT. Spowoduje to utworzenie kontenera magazynu o nazwie **Użytkownicy**. Obszar roboczy będzie używał tego konta magazynu jako konta magazynu "podstawowe" do tabel platformy Spark i dzienników aplikacji platformy Spark.
        1. Zaznacz pole wyboru "Przypisz samodzielnie rolę współautor danych obiektów blob magazynu" na koncie Data Lake Storage Gen2. 
1. Wybierz pozycję **Przeglądanie + tworzenie** > **Utwórz**. Obszar roboczy jest gotowy w ciągu kilku minut.

> [!NOTE]
> Aby włączyć funkcje obszaru roboczego z istniejącej dedykowanej puli SQL (dawniej SQL DW), zapoznaj się z [tematem Włączanie obszaru roboczego dla dedykowanej puli SQL (dawniej SQL DW)](./sql-data-warehouse/workspace-connected-create.md).


## <a name="open-synapse-studio"></a>Otwórz Synapse Studio

Po utworzeniu obszaru roboczego usługi Azure Synapse dostępne są dwa sposoby otwierania programu Synapse Studio:

* Otwórz obszar roboczy Synapse w [Azure Portal](https://portal.azure.com)w sekcji **Omówienie** obszaru roboczego Synapse wybierz pozycję **Otwórz** w polu Otwórz Synapse Studio.
* Przejdź do `https://web.azuresynapse.net` obszaru roboczego i zaloguj się do niego.


## <a name="the-built-in-serverless-sql-pool"></a>Wbudowana Pula SQL bezserwerowa

Każdy obszar roboczy zawiera wstępnie zbudowaną pulę SQL bezserwerową o nazwie **wbudowane**. Nie można usunąć tej puli. Pule SQL bezserwerowe umożliwiają korzystanie z języka SQL bez konieczności rezerwowania pojemności z dedykowanymi pulami SQL. W przeciwieństwie do dedykowanych pul SQL, rozliczanie dla bezserwerowej puli SQL jest oparte na ilości danych przeskanowanych w celu uruchomienia zapytania, a nie liczby pojemności przydzielonej do puli.


## <a name="create-a-dedicated-sql-pool"></a>Tworzenie dedykowanej puli SQL

1. W programie Synapse Studio w okienku po lewej stronie wybierz pozycję **Zarządzaj**  >  **pulami SQL**.
1. Wybierz pozycję **Nowy**
1. W obszarze **Nazwa puli SQL** wybierz pozycję **SQLPOOL1**
1. Dla opcji **poziom wydajności** wybierz **DW100C**
1. Wybierz pozycję **Przeglądanie + tworzenie** > **Utwórz**. Dedykowana Pula SQL będzie gotowa w ciągu kilku minut. Dedykowana Pula SQL jest skojarzona z dedykowaną bazą danych puli SQL o nazwie **SQLPOOL1**.

Dedykowana Pula SQL zużywa zasoby do rozliczenia, o ile jest ona aktywna. Pulę można wstrzymać później, aby zmniejszyć koszty.

> [!NOTE] 
> Podczas tworzenia nowej dedykowanej puli SQL (dawniej SQL DW) w obszarze roboczym zostanie otwarta strona dedykowana obsługa administracyjna puli SQL. Inicjowanie obsługi administracyjnej odbywa się na logicznym serwerze SQL Server.


## <a name="create-a-serverless-apache-spark-pool"></a>Utwórz bezserwerową pulę Apache Spark

1. W programie Synapse Studio w okienku po lewej stronie wybierz pozycję **Zarządzaj**  >  **pulami Apache Spark**.
1. Wybierz pozycję **Nowy** 
1. W obszarze **Nazwa puli Apache Spark** wprowadź **Spark1**.
1. Dla **rozmiaru węzła** wprowadź **małe**.
1. Dla **liczby węzłów** ustaw wartość minimalną na 3 i wartość maksymalną na 3.
1. Wybierz pozycję **Przeglądanie + tworzenie** > **Utwórz**. Pula Apache Spark będzie gotowa w ciągu kilku sekund.

Pula platformy Spark informuje platformę Azure Synapse, ile zasobów platformy Spark ma używać. Płacisz tylko za wykorzystane zasoby. Gdy aktywne zaprzestanie korzystania z puli, zasoby są automatycznie przekroczenia limitu czasu i są odtwarzane.


## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Analizowanie przy użyciu dedykowanej puli SQL](get-started-analyze-sql-pool.md)
