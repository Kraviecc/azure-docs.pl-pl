---
title: Obsługa 32-bitowych systemów operacyjnych na maszynach wirtualnych platformy Azure | Microsoft Docs
description: Informacje o systemach operacyjnych obsługiwanych w usłudze Azure Virtual Machines
services: virtual-machines-windows, azure-resource-manager
documentationcenter: ''
author: v-miegge
manager: dcscontentpm
editor: ''
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.topic: troubleshooting
ms.date: 09/18/2019
ms.author: v-miegge
ms.openlocfilehash: 81b7efdd6bca0471719c11d130be95405f4d54e1
ms.sourcegitcommit: f5b8410738bee1381407786fcb9d3d3ab838d813
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/14/2021
ms.locfileid: "98210192"
---
# <a name="support-for-32-bit-operating-systems-in-azure-virtual-machines"></a>Obsługa 32-bitowych systemów operacyjnych na maszynach wirtualnych platformy Azure

Microsoft Azure teraz umożliwia użytkownikom korzystanie z 32-bitowych systemów operacyjnych Windows na platformie Azure. Obsługiwane są tylko wyspecjalizowane dyski VHD, a uogólnione obrazy nie będą działały na platformie Azure. Ponieważ niektóre z tych systemów operacyjnych osiągnęły już swoją umowę dotyczącą korzystania z usługi Life, firma Microsoft może nie oferować dodatkowej pomocy technicznej. Pomoc techniczna nie jest również oferowana dla systemów operacyjnych opartych na systemie Linux lub Berkeley Software Distribution (BSD), które działają na Microsoft Azure maszynę wirtualną.

> [!NOTE]
> Platforma Azure ma ograniczenie przestrzeni adresów pamięci narzucone na maszynach wirtualnych z 32-bitowymi systemami operacyjnymi, w których można udostępnić maszynę wirtualną tylko 1 GB pamięci (*szczególnie w jednostkach SKU klienta, takich jak Win7 lub Win10*), a pozostała część pamięci dla maszyny wirtualnej będzie wyświetlana jako zarezerwowana w ramach maszyny wirtualnej gościa. Jest to znany problem i obecnie nie mamy EZT, aby rozwiązać problem. Zalecamy przechodzenie do 64-bitowych wersji systemu operacyjnego.
> 

## <a name="more-information"></a>Więcej informacji

Aby uzyskać więcej informacji na temat systemów operacyjnych obsługiwanych w usłudze Azure Virtual Machines, przejdź do następujących artykułów z bazy wiedzy Microsoft Knowledge Base:

* [Pomoc techniczna dotycząca oprogramowania serwerowego firmy Microsoft dla maszyn wirtualnych platformy Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)
* [Obsługa systemu Linux i technologii open source na platformie Azure](https://support.microsoft.com/help/2941892/support-for-linux-and-open-source-technology-in-azure)

## <a name="references"></a>Odwołania

* [Dowiedz się więcej o bezpłatnych rozszerzonych aktualizacjach zabezpieczeń dla systemu Windows Server 2008/R2 na platformie Azure](https://www.microsoft.com/cloud-platform/windows-server-2008)
* [Dowiedz się więcej o obsłudze systemu Windows Server 2008 z dodatkiem SP2 32-bitowym wyspecjalizowanym obrazom na platformie Azure](/windows-server/get-started/uploading-specialized-ws08-image-to-azure)
* [Dowiedz się więcej o obsłudze migracji obrazów systemu Windows Server 2008 na platformie Azure przy użyciu Azure Site Recovery](../../site-recovery/migrate-tutorial-windows-server-2008.md)
* [Dowiedz się więcej o obsługiwanych systemach operacyjnych rozszerzenia platformy Azure](https://support.microsoft.com/help/4078134/azure-extension-supported-operating-systems)
* [Dowiedz się więcej o uruchamianiu systemu Windows Server 2003 na Microsoft Azure](https://support.microsoft.com/help/3206074/running-windows-server-2003-on-microsoft-azure)

## <a name="next-steps"></a>Następne kroki

Jeśli potrzebujesz więcej pomocy w dowolnym punkcie tego artykułu, skontaktuj się z ekspertami platformy Azure na [forach MSDN i Stack Overflow](https://azure.microsoft.com/support/forums/).

Alternatywnie możesz zaplikować zdarzenie pomocy technicznej platformy Azure. Przejdź do [witryny pomocy technicznej systemu Azure](https://azure.microsoft.com/support/options/) i wybierz pozycję **Uzyskaj pomoc techniczną**.
