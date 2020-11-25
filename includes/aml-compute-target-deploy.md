---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: machine-learning
author: sdgilley
ms.service: machine-learning
ms.author: sgilley
manager: cgronlund
ms.custom: include file
ms.topic: include
ms.date: 11/02/2020
ms.openlocfilehash: 31d00222da540751a1f95120bea00535b099403d
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96027257"
---
Obiekt docelowy obliczeń używany do hostowania modelu będzie miał wpływ na koszt i dostępność wdrożonego punktu końcowego. Użyj tej tabeli, aby wybrać odpowiedni element docelowy obliczeń.

| Docelowy zasób obliczeniowy | Sposób użycia | Obsługa procesora GPU | Obsługa FPGA | Opis |
| ----- | ----- | ----- | ----- | ----- |
| [Lokalna &nbsp; Usługa sieci Web &nbsp;](../articles/machine-learning/how-to-deploy-local-container-notebook-vm.md) | Testowanie/debugowanie | &nbsp; | &nbsp; | Służy do ograniczonego testowania i rozwiązywania problemów. Przyspieszenie sprzętowe zależy od użycia bibliotek w systemie lokalnym.
| [Azure Kubernetes Service (AKS)](../articles/machine-learning/how-to-deploy-azure-kubernetes-service.md) | Wnioskowanie w czasie rzeczywistym |  [Tak](../articles/machine-learning/how-to-deploy-inferencing-gpus.md) (wdrożenie usługi sieci Web) | [Tak](../articles/machine-learning/how-to-deploy-fpga-web-service.md)   |Używany w przypadku wdrożeń produkcyjnych o dużej skali. Zapewnia krótki czas odpowiedzi i automatyczne skalowanie wdrożonej usługi. Skalowanie automatyczne klastra nie jest obsługiwane za pomocą zestawu SDK Azure Machine Learning. Aby zmienić węzły w klastrze AKS, użyj interfejsu użytkownika klastra AKS w Azure Portal. <br/><br/> Obsługiwane przez projektanta. |
| [Azure Container Instances](../articles/machine-learning/how-to-deploy-azure-container-instance.md) | Testowanie lub programowanie | &nbsp;  | &nbsp; | Używany w przypadku obciążeń opartych na PROCESORAch o niskiej skali, które wymagają mniej niż 48 GB pamięci RAM. <br/><br/> Obsługiwane przez projektanta. |
| [Klaster obliczeniowy usługi Azure Machine Learning](../articles/machine-learning/how-to-use-parallel-run-step.md) | &nbsp;Wnioskowanie partii | [Tak](../articles/machine-learning/how-to-use-parallel-run-step.md) (potok Machine Learning) | &nbsp;  | Uruchom ocenianie wsadowe w przypadku obliczeń bezserwerowych. Obsługuje maszyny wirtualne o normalnym i niskim priorytecie. |

> [!NOTE]
> Chociaż obiekty docelowe obliczeń, takie jak lokalne, Azure Machine Learning obliczeniowe i Azure Machine Learning, obsługują procesor GPU na potrzeby szkoleń i eksperymentowania, użycie procesora GPU do wnioskowania w przypadku _wdrożenia jako usługi sieci Web_ jest obsługiwane tylko w AKS.
>
> Użycie procesora GPU do wnioskowania, _gdy ocenianie z potokiem uczenia maszynowego_ jest obsługiwane tylko na Azure Machine Learning obliczeń.

> [!NOTE]
> * Wystąpienia kontenera są odpowiednie tylko w przypadku małych modeli o rozmiarze mniejszym niż 1 GB.
> * Używaj jednowęzłowych klastrów AKS na potrzeby tworzenia i testowania większych modeli.