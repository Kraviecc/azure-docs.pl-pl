---
title: Co to jest usługa Azure Synapse Analytics?
description: Omówienie usługi Azure Synapse Analytics
services: synapse-analytics
author: saveenr
ms.service: synapse-analytics
ms.topic: overview
ms.subservice: overview
ms.date: 10/28/2020
ms.author: saveenr
ms.reviewer: jrasnick
ms.openlocfilehash: 37768b994d4b61ee728e04352f027a6f5a478341
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102031620"
---
# <a name="what-is-azure-synapse-analytics"></a>Co to jest usługa Azure Synapse Analytics?

Analiza przedsiębiorstwa musi być wydajna na bardzo dużą skalę w przypadku dowolnego rodzaju danych, zarówno nieprzetworzony, rafinowany, jak i wysoce nadzorowany. Zwykle jest to konieczne, aby przedsiębiorstwa współpracowały z dużą ilością danych i technologiami magazynowania danych w złożonych potokach danych, które działają między danymi w magazynach relacyjnych i jeziorach danych. Te rodzaje rozwiązań są trudne do skompilowania, utrzymania i zabezpieczenia. Opóźnienia w zakresie złożoności zapewniające zapotrzebowanie na przedsiębiorstwa.

**Azure Synapse** to zintegrowana usługa analityczna, która przyspiesza czas w celu wglądu w dane między magazynami danych i systemami danych Big Data. Usługa Azure Synapse umożliwia łączenie najlepszych technologii **SQL** używanych w magazynach danych w przedsiębiorstwie, technologii **Spark** używanych w przypadku danych Big Data, **potoków** do integracji danych i ETL/ELT oraz głębokiej integracji z innymi usługami platformy Azure, takimi jak **Power BI**, **CosmosDB** i **Azure**.

## <a name="key-features--benefits"></a>Najważniejsze funkcje & korzyści

### <a name="industry-leading-sql"></a>Wiodące w branży SQL

* **Synapse SQL** to rozproszony system zapytań dla języka T-SQL, który umożliwia tworzenie i obsługę magazynów danych oraz scenariuszy wirtualizacji danych oraz rozszerza język t-SQL na potrzeby przesyłania strumieniowego i scenariuszy uczenia maszynowego.
* Program Synapse SQL oferuje **bezserwerowe** i **dedykowane** modele zasobów, oferując opcje zużycia i rozliczeń w celu dopasowania do Twoich potrzeb. Aby zapewnić przewidywalność wydajności i kosztów, utwórz dedykowane pule SQL, umożliwiające zarezerwowanie mocy obliczeniowej dla danych przechowywanych w tabelach SQL. W przypadku obciążeń nieplanowanych lub na rozerwanie należy użyć punktu końcowego SQL Always dostępnego serwera.
* Korzystanie z wbudowanych funkcji **przesyłania strumieniowego** w celu wywożenia danych ze źródeł danych w chmurze w tabelach SQL
* Integrowanie AI z programem SQL przy użyciu modeli **uczenia maszynowego** do oceny danych za pomocą [funkcji przewidywania T-SQL](/sql/t-sql/queries/predict-transact-sql?view=azure-sqldw-latest&preserve-view=true)

### <a name="industry-standard-apache-spark"></a>Apache Spark standardowa

**Apache Spark dla systemu Azure Synapse** głęboko i bezproblemowo integruje Apache Spark — najpopularniejszy aparat danych Big Data, który służy do przygotowywania danych, inżynierii danych, ETL i uczenia maszynowego.

* Modele ML z algorytmami SparkML i integracją usługi Azure dla Apache Spark 2,4 z wbudowaną obsługą systemu Linux Foundation w systemie.
* Uproszczony model zasobów, który uwalnia użytkownika od konieczności zarządzania klastrami.
* Szybka konfiguracja platformy Spark i agresywne Skalowanie automatyczne.
* Wbudowana obsługa programu .NET for Spark umożliwiająca ponowne użycie doświadczenia w języku C# i istniejącego kodu platformy .NET w aplikacji platformy Spark.

### <a name="interop-of-sql-and-apache-spark-on-your-data-lake"></a>Międzyoperacyjność SQL i Apache Spark na Data Lake

Usługa Azure Synapse usuwa tradycyjne bariery technologiczne między programami SQL i Spark. Możesz bezproblemowo mieszać i dopasowywać w zależności od potrzeb i wiedzy fachowej.

* Udostępniony system metadanych zgodny z platformą Hive umożliwia używanie tabel zdefiniowanych dla plików w usłudze Data Lake do bezproblemowego wykorzystania przez platformę Spark lub Hive.
* SQL i Spark mogą bezpośrednio eksplorować i analizować pliki Parquet, CSV, TSV i JSON przechowywane w usłudze Data Lake.
* Szybkie skalowalne obciążenie i zwalnianie danych przechodzących między bazami danych SQL i Spark

### <a name="built-in-data-integration-via-pipelines"></a>Wbudowana integracja danych za pośrednictwem potoków

Usługa Azure Synapse jest wbudowana przy użyciu tego samego aparatu integracji danych i środowisk Azure Data Factory, co pozwala na tworzenie rozbudowanych potoków ETL w skali, bez opuszczania usługi Azure Synapse Analytics.

* Pozyskiwanie danych ze źródeł danych 90 +
* Code-Free ETL z działaniami przepływu danych
* Organizowanie notesów, zadań platformy Spark, procedur składowanych, skryptów SQL i innych

### <a name="unified-management-monitoring-and-security"></a>Ujednolicone zarządzanie, monitorowanie i zabezpieczenia

Usługa Azure Synapse umożliwia przedsiębiorstwom zarządzanie zasobami analitycznymi, monitorowanie użycia i działania oraz Wymuszanie zabezpieczeń.

* Przypisywanie użytkowników do roli w celu uproszczenia dostępu do zasobów analitycznych
* Szczegółowa kontrola dostępu do danych i kodu
* Pojedynczy pulpit nawigacyjny do monitorowania zasobów, użycia i użytkowników w ramach programu SQL i platformy Spark

### <a name="unified-experience"></a>Ujednolicone środowisko

**Synapse Studio** to środowisko użytkownika, które wiąże wszystko ze sobą w przypadku inżynierów danych. Umożliwia im to każde zadanie potrzebne do utworzenia kompletnego rozwiązania do analizy.

* Kluczowe dane engingeer zadania w jednym miejscu: pozyskiwanie, eksplorowanie, przygotowywanie, organizowanie, wizualizowanie
* Wiodąca w branży produktywność pisania kodu SQL lub Spark: Tworzenie, debugowanie i Optymalizacja wydajności
* Integracja z procesem ciągłej integracji/ciągłego wdrażania

## <a name="engage-with-the-synapse-engineering-team"></a>Zaangażuj się z zespołem inżynierów Synapse

- [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-synapse): zadawaj pytania dotyczące programowania.
- [Microsoft Q&stronie pytania](/answers/topics/azure-synapse-analytics.html): zadawaj pytania techniczne.

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie do usługi Azure Synapse Analytics](get-started.md)
* [Tworzenie obszaru roboczego](quickstart-create-workspace.md)
* [Korzystanie z bezserwerowej puli SQL](quickstart-sql-on-demand.md)
