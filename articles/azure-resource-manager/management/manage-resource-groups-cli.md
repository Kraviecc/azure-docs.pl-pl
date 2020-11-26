---
title: Zarządzanie grupami zasobów — interfejs wiersza polecenia platformy Azure
description: Użyj interfejsu wiersza polecenia platformy Azure, aby zarządzać grupami zasobów za pomocą Azure Resource Manager. Pokazuje, jak tworzyć, wyświetlać i usuwać grupy zasobów.
author: mumian
ms.topic: conceptual
ms.date: 09/01/2020
ms.author: jgao
ms.custom: devx-track-azurecli
ms.openlocfilehash: 4a9a4ed4ebba7f6f2470bb9e7000a899ebc26323
ms.sourcegitcommit: d22a86a1329be8fd1913ce4d1bfbd2a125b2bcae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96185814"
---
# <a name="manage-azure-resource-manager-resource-groups-by-using-azure-cli"></a>Zarządzanie grupami zasobów Azure Resource Manager przy użyciu interfejsu wiersza polecenia platformy Azure

Dowiedz się, jak zarządzać grupami zasobów platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure z [Azure Resource Manager](overview.md) . Aby zarządzać zasobami platformy Azure, zobacz [Zarządzanie zasobami platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure](manage-resources-cli.md).

Inne artykuły dotyczące zarządzania grupami zasobów:

- [Zarządzanie grupami zasobów platformy Azure przy użyciu Azure Portal](manage-resources-portal.md)
- [Zarządzanie grupami zasobów platformy Azure przy użyciu Azure PowerShell](manage-resources-powershell.md)

## <a name="what-is-a-resource-group"></a>Co to jest Grupa zasobów

Grupa zasobów to kontener zawierający powiązane zasoby dla rozwiązania platformy Azure. Grupa zasobów może zawierać wszystkie zasoby dla rozwiązania lub tylko te zasoby, które mają być zarządzane jako grupa. Użytkownik decyduje o sposobie przydziału zasobów do grup zasobów pod kątem tego, co jest najbardziej odpowiednie dla danej organizacji. Ogólnie rzecz biorąc, Dodaj zasoby, które mają ten sam cykl życia do tej samej grupy zasobów, dzięki czemu możesz łatwo wdrażać, aktualizować i usuwać je jako grupę.

Grupa zasobów przechowuje metadane dotyczące zasobów. Z tego powodu określając lokalizację dla grupy zasobów, określasz miejsce, w którym przechowywane są metadane. W celu zapewnienia zgodności może być konieczne upewnienie się, że dane są przechowywane w konkretnym regionie.

Grupa zasobów przechowuje metadane dotyczące zasobów. W przypadku określania lokalizacji grupy zasobów należy określić miejsce przechowywania metadanych.

## <a name="create-resource-groups"></a>Tworzenie grup zasobów

Poniższe polecenie interfejsu wiersza polecenia tworzy grupę zasobów.

```azurecli-interactive
az group create --name demoResourceGroup --location westus
```

## <a name="list-resource-groups"></a>Wyświetl listę grup zasobów

Poniższy skrypt interfejsu wiersza polecenia zawiera listę grup zasobów w ramach subskrypcji.

```azurecli-interactive
az group list
```

Aby uzyskać jedną grupę zasobów:

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az group show --name $resourceGroupName
```

## <a name="delete-resource-groups"></a>Usuwanie grup zasobów

Następujący skrypt interfejsu wiersza polecenia usuwa grupę zasobów:

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az group delete --name $resourceGroupName
```

Aby uzyskać więcej informacji na temat sposobu, w jaki Azure Resource Manager kolejności usuwania zasobów, zobacz [Azure Resource Manager Usuwanie grupy zasobów](delete-resource-group.md).

## <a name="deploy-resources-to-an-existing-resource-group"></a>Wdrażanie zasobów w istniejącej grupie zasobów

Zobacz [wdrażanie zasobów w istniejącej grupie zasobów](manage-resources-cli.md#deploy-resources-to-an-existing-resource-group).

## <a name="deploy-a-resource-group-and-resources"></a>Wdrażanie grupy zasobów i zasobów

Można utworzyć grupę zasobów i wdrożyć zasoby w grupie przy użyciu szablonu Menedżer zasobów. Aby uzyskać więcej informacji, zobacz [Tworzenie grupy zasobów i wdrażanie zasobów](../templates/deploy-to-subscription.md#resource-groups).

## <a name="redeploy-when-deployment-fails"></a>Wdróż ponownie w przypadku niepowodzenia wdrożenia

Ta funkcja jest również znana jako *Rollback w przypadku błędu*. Aby uzyskać więcej informacji, zobacz [ponowne wdrażanie w przypadku niepowodzenia wdrożenia](../templates/rollback-on-error.md).

## <a name="move-to-another-resource-group-or-subscription"></a>Przenieś do innej grupy zasobów lub subskrypcji

Zasoby w grupie można przenieść do innej grupy zasobów. Aby uzyskać więcej informacji, zobacz [przenoszenie zasobów](manage-resources-cli.md#move-resources).

## <a name="lock-resource-groups"></a>Zablokuj grupy zasobów

Blokowanie uniemożliwia innym użytkownikom w organizacji przypadkowe usuwanie lub modyfikowanie krytycznych zasobów, takich jak subskrypcja platformy Azure, Grupa zasobów lub zasób. 

Poniższy skrypt blokuje grupę zasobów, aby nie można było usunąć grupy zasobów.

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az lock create --name LockGroup --lock-type CanNotDelete --resource-group $resourceGroupName  
```

Następujący skrypt pobiera wszystkie blokady dla grupy zasobów:

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az lock list --resource-group $resourceGroupName  
```

Następujący skrypt usuwa blokadę:

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the lock name:" &&
read lockName &&
az lock delete --name $lockName --resource-group $resourceGroupName
```

Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).

## <a name="tag-resource-groups"></a>Dodawanie tagów do grup zasobów

Możesz zastosować znaczniki do grup zasobów i zasobów, aby logicznie organizować zasoby. Aby uzyskać więcej informacji, zobacz [Używanie tagów do organizowania zasobów platformy Azure](tag-resources.md#azure-cli).

## <a name="export-resource-groups-to-templates"></a>Eksportowanie grup zasobów do szablonów

Po pomyślnym skonfigurowaniu grupy zasobów warto wyświetlić szablon Menedżer zasobów dla grupy zasobów. Eksportowanie szablonu oferuje dwie korzyści:

- Automatyzuj przyszłe wdrożenia rozwiązania, ponieważ szablon zawiera całą kompletną infrastrukturę.
- Poznaj składnię szablonu, przeglądając JavaScript Object Notation (JSON), który reprezentuje Twoje rozwiązanie.

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az group export --name $resourceGroupName  
```

Skrypt wyświetla szablon w konsoli programu.  Skopiuj kod JSON i Zapisz go jako plik.

Funkcja eksportowania szablonu nie obsługuje eksportowania zasobów Azure Data Factory. Aby dowiedzieć się, jak wyeksportować zasoby Data Factory, zobacz [kopiowanie lub klonowanie fabryki danych w Azure Data Factory](../../data-factory/copy-clone-data-factory.md).

Aby wyeksportować zasoby utworzone za pomocą klasycznego modelu wdrażania, należy [je zmigrować do modelu wdrażania Menedżer zasobów](../../virtual-machines/migration-classic-resource-manager-overview.md).

Aby uzyskać więcej informacji, zobacz [Eksportowanie jednego i wielu zasobów do szablonu w Azure Portal](../templates/export-template-portal.md).

## <a name="manage-access-to-resource-groups"></a>Zarządzanie dostępem do grup zasobów

[Kontrola dostępu oparta na rolach (Azure RBAC)](../../role-based-access-control/overview.md) umożliwia zarządzanie dostępem do zasobów na platformie Azure. Aby uzyskać więcej informacji, zobacz [Dodawanie lub usuwanie przypisań ról platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure](../../role-based-access-control/role-assignments-cli.md).

## <a name="next-steps"></a>Następne kroki

- Aby dowiedzieć się Azure Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](overview.md).
- Aby poznać składnię szablonu Menedżer zasobów, zobacz [Opis struktury i składni Azure Resource Manager szablonów](../templates/template-syntax.md).
- Aby dowiedzieć się, jak opracowywać szablony, zobacz [Samouczki krok po kroku](../index.yml).
- Aby wyświetlić Azure Resource Manager Schematy szablonów, zobacz [Dokumentacja szablonu](/azure/templates/).