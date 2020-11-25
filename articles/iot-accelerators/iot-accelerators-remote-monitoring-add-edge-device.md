---
title: Rozwiązanie do zdalnego monitorowania Dodawanie urządzenia brzegowego — Azure | Microsoft Docs
description: W tym artykule opisano sposób dodawania urządzenia IoT Edge do akceleratora rozwiązania do zdalnego monitorowania
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 10/09/2018
ms.topic: conceptual
ms.openlocfilehash: de060be7ace84ea309b71087a50fd572091bed43
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96004793"
---
# <a name="add-an-iot-edge-device-to-your-remote-monitoring-solution-accelerator"></a>Dodawanie urządzenia IoT Edge do akceleratora rozwiązania do monitorowania zdalnego

Aby dodać urządzenie [IoT Edge](../iot-edge/about-iot-edge.md) do akceleratora rozwiązania, wykonaj następujące dwa kroki:

1. Dodaj urządzenie brzegowe na stronie **Device Explorer** w interfejsie użytkownika sieci Web akceleratora rozwiązania do monitorowania zdalnego.
1. Zainstaluj środowisko uruchomieniowe IoT Edge na urządzeniu brzegowym.

## <a name="add-the-iot-edge-device"></a>Dodaj urządzenie IoT Edge

Aby dodać urządzenie usługi IoT Edge do akceleratora rozwiązania do monitorowania zdalnego, przejdź do strony **Device Explorer** w internetowym interfejsie użytkownika i kliknij pozycję **+ Nowe urządzenie**.

W panelu **nowe urządzenie** wybierz pozycję **IoT Edge urządzenie**. Dla innych właściwości możesz pozostawić ustawienia domyślne. Następnie kliknij pozycję **Zastosuj**:

![Dodawanie urządzenia usługi IoT Edge](media/iot-accelerators-remote-monitoring-add-edge-device/addedgedevice.png)

### <a name="alternative-ways-to-add-an-iot-edge-device"></a>Alternatywne sposoby dodawania urządzenia IoT Edge

Istnieje również możliwość zarejestrowania urządzenia IoT Edge bezpośrednio z wystąpieniem IoT Hub w akceleratorze rozwiązania. Musisz znać nazwę Centrum IoT w akceleratorze rozwiązania, zanim skorzystasz z następujących przewodników:

- [Zarejestruj nowe urządzenie Azure IoT Edge z poziomu Azure Portal](../iot-edge/how-to-register-device.md#register-in-the-azure-portal)
- [Rejestrowanie nowego urządzenia Azure IoT Edge przy użyciu interfejsu wiersza polecenia platformy Azure](../iot-edge/how-to-register-device.md#register-with-the-azure-cli)
- [Zarejestruj nowe urządzenie Azure IoT Edge z poziomu Visual Studio Code](../iot-edge/how-to-register-device.md#register-with-visual-studio-code)

Po zarejestrowaniu urządzenia bezpośrednio w usłudze IoT Hub w akceleratorze rozwiązania do monitorowania zdalnego jest on wyświetlany na stronie **Device Explorer** w interfejsie użytkownika sieci Web.

## <a name="install-the-iot-edge-runtime"></a>Instalowanie środowiska uruchomieniowego usługi IoT Edge

Aby można było wdrażać moduły na urządzeniu brzegowym, należy zainstalować środowisko uruchomieniowe IoT Edge na rzeczywistym urządzeniu. Poniższe przewodniki przedstawiają sposób instalowania środowiska uruchomieniowego na popularnych platformach urządzeń:

- [Zainstaluj środowisko uruchomieniowe Azure IoT Edge w systemie Linux (x64)](../iot-edge/how-to-install-iot-edge-linux.md)
- [Zainstaluj środowisko uruchomieniowe Azure IoT Edge w systemie Linux (ARM32v7/armhf)](../iot-edge/how-to-install-iot-edge-linux.md)
- [Instalowanie Azure IoT Edge środowiska uruchomieniowego w systemie Windows do użycia z kontenerami systemu Windows](../iot-edge/how-to-install-iot-edge-windows.md)
- [Zainstaluj środowisko uruchomieniowe Azure IoT Edge w systemie Windows do użycia z kontenerami systemu Linux](../iot-edge/how-to-install-iot-edge-windows-with-linux.md)
- [Zainstaluj środowisko uruchomieniowe IoT Edge w systemie Windows IoT Core](../iot-edge/how-to-install-iot-edge-windows.md)

## <a name="next-steps"></a>Następne kroki

Teraz, gdy przygotowano urządzenie IoT Edge, następnym krokiem jest wdrożenie modułów. Zobacz [Importowanie pakietu IoT Edge do akceleratora rozwiązania do monitorowania zdalnego](iot-accelerators-remote-monitoring-import-edge-package.md)