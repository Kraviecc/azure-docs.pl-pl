---
title: Tworzenie maszyny wirtualnej na podstawie uogólnionego obrazu przy użyciu interfejsu wiersza polecenia platformy Azure
description: Utwórz maszynę wirtualną na podstawie uogólnionej wersji obrazu przy użyciu interfejsu wiersza polecenia platformy Azure.
author: cynthn
ms.service: virtual-machines
ms.subservice: imaging
ms.topic: how-to
ms.workload: infrastructure
ms.date: 05/04/2020
ms.author: cynthn
ms.custom: devx-track-azurecli
ms.openlocfilehash: ec589848625e1114dedd8c58b41f7ecbc991f311
ms.sourcegitcommit: aaa65bd769eb2e234e42cfb07d7d459a2cc273ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/27/2021
ms.locfileid: "98881978"
---
# <a name="create-a-vm-from-a-generalized-image-version-using-the-cli"></a>Tworzenie maszyny wirtualnej na podstawie uogólnionej wersji obrazu przy użyciu interfejsu wiersza polecenia

Utwórz maszynę wirtualną na podstawie [uogólnionej wersji obrazu](./shared-image-galleries.md#generalized-and-specialized-images) przechowywanej w galerii obrazów udostępnionych. Jeśli chcesz utworzyć maszynę wirtualną przy użyciu wyspecjalizowanego obrazu, zobacz [Tworzenie maszyny wirtualnej na podstawie wyspecjalizowanego obrazu](vm-specialized-image-version-powershell.md). 


## <a name="get-the-image-id"></a>Pobieranie identyfikatora obrazu

Wyświetl listę definicji obrazów w galerii za pomocą polecenia [AZ SIG Image-Definition list](/cli/azure/sig/image-definition#az-sig-image-definition-list) , aby wyświetlić nazwę i identyfikator definicji.

```azurecli-interactive 
resourceGroup=myGalleryRG
gallery=myGallery
az sig image-definition list --resource-group $resourceGroup --gallery-name $gallery --query "[].[name, id]" --output tsv
```

## <a name="create-the-vm"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę wirtualną przy użyciu polecenia [az vm create](/cli/azure/vm#az-vm-create). Aby użyć najnowszej wersji obrazu, ustaw `--image` na identyfikator definicji obrazu. 

W tym przykładzie Zastąp nazwy zasobów zgodnie z wymaganiami. 

```azurecli-interactive 
imgDef="/subscriptions/<subscription ID where the gallery is located>/resourceGroups/myGalleryRG/providers/Microsoft.Compute/galleries/myGallery/images/myImageDefinition"
vmResourceGroup=myResourceGroup
location=eastus
vmName=myVM
adminUsername=azureuser


az group create --name $vmResourceGroup --location $location

az vm create\
   --resource-group $vmResourceGroup \
   --name $vmName \
   --image $imgDef \
   --admin-username $adminUsername \
   --generate-ssh-keys
```

Można również użyć określonej wersji, używając identyfikatora wersji obrazu dla `--image` parametru. Na przykład, aby użyć *1.0.0* wersji obrazu typu: `--image "/subscriptions/<subscription ID where the gallery is located>/resourceGroups/myGalleryRG/providers/Microsoft.Compute/galleries/myGallery/images/myImageDefinition/versions/1.0.0"` .

## <a name="next-steps"></a>Następne kroki

[Usługa Azure Image Builder (wersja zapoznawcza)](./image-builder-overview.md) ułatwia automatyzację tworzenia wersji obrazu. można nawet użyć jej do aktualizacji i [tworzenia nowej wersji obrazu z istniejącej wersji obrazu](./linux/image-builder-gallery-update-image-version.md).