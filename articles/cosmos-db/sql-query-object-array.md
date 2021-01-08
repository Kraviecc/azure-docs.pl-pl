---
title: Praca z tablicami i obiektami w Azure Cosmos DB
description: Poznaj składnię SQL, aby utworzyć tablice i obiekty w Azure Cosmos DB. W tym artykule przedstawiono również przykłady wykonywania operacji na obiektach Array
author: timsander1
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: conceptual
ms.date: 01/07/2021
ms.author: tisande
ms.openlocfilehash: f959e4e230c1d9f89ad5141713b6a17a8cbb17a2
ms.sourcegitcommit: 42a4d0e8fa84609bec0f6c241abe1c20036b9575
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2021
ms.locfileid: "98018925"
---
# <a name="working-with-arrays-and-objects-in-azure-cosmos-db"></a>Praca z tablicami i obiektami w Azure Cosmos DB
[!INCLUDE[appliesto-sql-api](includes/appliesto-sql-api.md)]

Kluczową funkcją interfejsu API SQL Azure Cosmos DB jest tworzenie tablic i obiektów.

## <a name="arrays"></a>Tablice

Można skonstruować tablice, jak pokazano w następującym przykładzie:

```sql
SELECT [f.address.city, f.address.state] AS CityState
FROM Families f
```

Wyniki są następujące:

```json
[
  {
    "CityState": [
      "Seattle",
      "WA"
    ]
  },
  {
    "CityState": [
      "NY", 
      "NY"
    ]
  }
]
```

Możesz również użyć [wyrażenia Array](sql-query-subquery.md#array-expression) , aby utworzyć tablicę z wyników [podzapytania](sql-query-subquery.md) . To zapytanie pobiera wszystkie różne nazwy elementów podrzędnych w tablicy.

```sql
SELECT f.id, ARRAY(SELECT DISTINCT VALUE c.givenName FROM c IN f.children) as ChildNames
FROM f
```

Wyniki są następujące:

```json
[
    {
        "id": "AndersenFamily",
        "ChildNames": []
    },
    {
        "id": "WakefieldFamily",
        "ChildNames": [
            "Jesse",
            "Lisa"
        ]
    }
]
```

## <a name="iteration"></a><a id="Iteration"></a>Powtórz

Interfejs API SQL zapewnia obsługę iteracji w tablicach JSON przy użyciu [słowa kluczowego in](sql-query-keywords.md#in) w źródle from. W poniższym przykładzie:

```sql
SELECT *
FROM Families.children
```

Wyniki są następujące:

```json
[
  [
    {
      "firstName": "Henriette Thaulow",
      "gender": "female",
      "grade": 5,
      "pets": [{ "givenName": "Fluffy"}]
    }
  ], 
  [
    {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1
    }, 
    {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }
  ]
]
```

Następne zapytanie wykonuje iterację `children` w `Families` kontenerze. Tablica wyjściowa różni się od powyższego zapytania. Ten przykład dzieli `children` i spłaszcza wyniki do pojedynczej tablicy:  

```sql
SELECT *
FROM c IN Families.children
```

Wyniki są następujące:

```json
[
  {
      "firstName": "Henriette Thaulow",
      "gender": "female",
      "grade": 5,
      "pets": [{ "givenName": "Fluffy" }]
  },
  {
      "familyName": "Merriam",
      "givenName": "Jesse",
      "gender": "female",
      "grade": 1
  },
  {
      "familyName": "Miller",
      "givenName": "Lisa",
      "gender": "female",
      "grade": 8
  }
]
```

Można filtrować więcej według poszczególnych wpisów tablicy, jak pokazano w następującym przykładzie:

```sql
SELECT c.givenName
FROM c IN Families.children
WHERE c.grade = 8
```

Wyniki są następujące:

```json
[{
  "givenName": "Lisa"
}]
```

Można również agregować wynik iteracji tablicy. Na przykład następujące zapytanie liczy liczbę elementów podrzędnych między wszystkimi rodzinami:

```sql
SELECT COUNT(1) AS Count
FROM child IN Families.children
```

Wyniki są następujące:

```json
[
  {
    "Count": 3
  }
]
```

> [!NOTE]
> W przypadku użycia słowa kluczowego IN dla iteracji nie można filtrować ani projektować żadnych właściwości poza tablicą. Zamiast tego należy użyć [sprzężeń](sql-query-join.md).

## <a name="next-steps"></a>Następne kroki

- [Rozpoczęcie pracy](sql-query-getting-started.md)
- [Przykłady dla platformy .NET w usłudze Azure Cosmos DB](https://github.com/Azure/azure-cosmos-dotnet-v3)
- [Sprzężenia](sql-query-join.md)
