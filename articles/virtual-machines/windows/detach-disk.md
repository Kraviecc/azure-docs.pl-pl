---
title: Odłączanie dysku danych z maszyny wirtualnej z systemem Windows — Azure
description: Odłączanie dysku danych z maszyny wirtualnej na platformie Azure przy użyciu modelu wdrażania Menedżer zasobów.
author: cynthn
ms.service: virtual-machines-windows
ms.subservice: disks
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 01/26/2021
ms.author: cynthn
ms.openlocfilehash: 95f6ce2fefacd20102abe9bbe818f228139ca33d
ms.sourcegitcommit: 100390fefd8f1c48173c51b71650c8ca1b26f711
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898515"
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a>How to detach a data disk from a Windows virtual machine (Jak odłączyć dysk od maszyny wirtualnej systemu Windows)

Gdy już nie potrzebujesz dysku danych dołączonego do maszyny wirtualnej, możesz go łatwo odłączyć. Spowoduje to usunięcie dysku z maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.

> [!WARNING]
> Jeśli dysk zostanie odłączony, nie jest automatycznie usuwany. Jeśli subskrybujesz usługę Premium Storage, nadal będą naliczane opłaty za magazyn dla tego dysku. Aby uzyskać więcej informacji, zobacz [Cennik i rozliczenia w przypadku korzystania z Premium Storage](../disks-types.md#billing).

Jeśli chcesz użyć danych znajdujących się na tym dysku, możesz dołączyć go ponownie do tej samej lub innej maszyny wirtualnej.

 

## <a name="detach-a-data-disk-using-powershell"></a>Odłączanie dysku danych przy użyciu programu PowerShell

Możesz *gorąco* usuwanie dysku danych przy użyciu programu PowerShell, ale przed odłączeniem go od maszyny wirtualnej nie trzeba aktywnie używać dysku.

W tym przykładzie usuniemy **dysk o nazwie** **myVM** z maszyny wirtualnej z **grupy zasobów.** Najpierw należy usunąć dysk przy użyciu polecenia cmdlet [Remove-AzVMDataDisk](/powershell/module/az.compute/remove-azvmdatadisk) . Następnie należy zaktualizować stan maszyny wirtualnej za pomocą polecenia cmdlet [Update-AzVM](/powershell/module/az.compute/update-azvm) , aby ukończyć proces usuwania dysku z danymi.

```azurepowershell-interactive
$VirtualMachine = Get-AzVM `
   -ResourceGroupName "myResourceGroup" `
   -Name "myVM"
Remove-AzVMDataDisk `
   -VM $VirtualMachine `
   -Name "myDisk"
Update-AzVM `
   -ResourceGroupName "myResourceGroup" `
   -VM $VirtualMachine
```

Dysk pozostaje w magazynie, ale nie jest już dołączony do maszyny wirtualnej.

## <a name="detach-a-data-disk-using-the-portal"></a>Odłączanie dysku danych przy użyciu portalu

Można *gorąco* usuwanie dysku danych, ale nie należy aktywnie używać dysku przed odłączeniem go od maszyny wirtualnej.

1. W menu po lewej stronie wybierz pozycję **Virtual Machines**.
1. Wybierz maszynę wirtualną zawierającą dysk danych, który chcesz odłączyć.
1. W obszarze **Ustawienia** wybierz pozycję **Dyski**.
1. W okienku **dyski** z prawej strony dysku z danymi, które chcesz odłączyć, kliknij przycisk Usuń **X** .
1. Wybierz pozycję **Zapisz** w górnej części strony, aby zapisać zmiany.

Dysk pozostaje w magazynie, ale nie jest już dołączony do maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz ponownie użyć dysku z danymi, możesz [dołączyć go do innej maszyny wirtualnej](attach-managed-disk-portal.md).

Jeśli chcesz usunąć dysk, dzięki czemu nie będą już naliczane koszty magazynowania, zobacz [Znajdowanie i usuwanie niedołączonych dysków zarządzanych i niezarządzanych platformy Azure — Azure Portal](../disks-find-unattached-portal.md).