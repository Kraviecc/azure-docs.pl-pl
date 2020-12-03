---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: virtual-machines-linux
author: cynthn
ms.service: virtual-machines-linux
ms.topic: include
ms.date: 02/11/2019
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: 5bfe077a99a3e89efe5fe4257a646484fb3810da
ms.sourcegitcommit: 5b93010b69895f146b5afd637a42f17d780c165b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96536977"
---
## <a name="supported-distributions-and-drivers"></a>Obsługiwane dystrybucje i sterowniki

### <a name="nvidia-cuda-drivers"></a>Sterowniki NVIDIA CUDA

Sterowniki NVIDIA CUDA dla maszyn wirtualnych z serii NC, NCv2, Seria NCV3, ND i NDv2 (opcjonalne dla serii NV) są obsługiwane tylko w przypadku dystrybucji systemu Linux wymienionych w poniższej tabeli. Informacje o sterowniku CUDA są aktualne w momencie publikacji. Najnowsze sterowniki CUDA i obsługiwane systemy operacyjne można znaleźć w witrynie internetowej [firmy NVIDIA](https://developer.nvidia.com/cuda-zone) . Upewnij się, że instalujesz lub uaktualniasz do najnowszych sterowników CUDA dla dystrybucji. 

> [!TIP]
> Alternatywą dla ręcznej instalacji sterownika CUDA na maszynie wirtualnej z systemem Linux jest wdrożenie obrazu [Data Science Virtual Machine](../articles/machine-learning/data-science-virtual-machine/overview.md) platformy Azure. Wersje DSVM dla Ubuntu 16,04 LTS lub CentOS 7,4 wstępnie instalują sterowniki NVIDIA CUDA, bibliotekę sieciową CUDA głębokiej neuronowych oraz inne narzędzia.


### <a name="nvidia-grid-drivers"></a>Sterowniki sieci NVIDIA

Firma Microsoft redystrybuuje Instalatory sterowników NVIDIA GRID dla maszyn wirtualnych z serii NV i NVv3 używanych jako wirtualne stacje robocze lub aplikacje wirtualne. Zainstaluj tylko te sterowniki siatki na maszynach wirtualnych usługi Azure NV, tylko w systemach operacyjnych wymienionych w poniższej tabeli. Te sterowniki obejmują Licencjonowanie oprogramowania wirtualnej procesora GPU na platformie Azure. Nie trzeba konfigurować serwera licencji oprogramowania NVIDIA vGPU.

Sterowniki siatki rozpowszechniane przez platformę Azure nie działają na maszynach wirtualnych z serii nietrwałych, takich jak NC, NCv2, Seria NCV3, ND i NDv2.

|Dystrybucja|Sterownik|
| --- | -- |
|Ubuntu 18.04 LTS<br/><br/>Ubuntu 16.04 LTS<br/><br/>Red Hat Enterprise Linux 7,6 do 7,8, 8,0, 8,1<br/><br/>CentOS-based 7,6, 7,7, 8,0, 8 (1911)<br/><br/>SUSE Linux Enterprise Server 12 z dodatkiem SP2 | NVIDIA GRID 11,2, rozgałęzienie sterownika [R450](https://go.microsoft.com/fwlink/?linkid=874272)(. exe)|

Odwiedź witrynę [GitHub](https://github.com/Azure/azhpc-extensions/blob/master/NvidiaGPU/resources.json) , aby uzyskać pełną listę wszystkich poprzednich linków sterownika NVIDIA GRID.

> [!WARNING] 
> Instalacja oprogramowania innych firm na produktach systemu Red Hat może wpłynąć na warunki wsparcia systemu Red Hat. Zobacz [artykuł bazy wiedzy systemu Red Hat](https://access.redhat.com/articles/1067).
>
