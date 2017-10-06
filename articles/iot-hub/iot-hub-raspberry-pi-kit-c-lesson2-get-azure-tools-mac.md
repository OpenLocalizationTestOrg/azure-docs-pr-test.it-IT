---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 2: strumenti di Azure (macOS) | Documenti Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, interfaccia della riga di comando di azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Ottenere gli strumenti di Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 e versioni successive](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Installare hello Azure interfaccia della riga di comando (CLI di Azure). Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* Come tooinstall CLI di Azure.
* Come tooadd un sottogruppo di IoT di hello CLI di Azure.

## <a name="what-you-need"></a>Elementi necessari
* Un Mac con connessione Internet.
* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.

## <a name="install-python"></a>Installare Python
Sebbene macOS include Python 2.7 predefinito hello, è consigliabile installare Python tramite Homebrew. Vedere [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (Installazione di Python in macOS).

Installare Python e pip eseguendo hello comando seguente:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Installare hello CLI di Azure
Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure. Si lavora direttamente da tooprovision la riga di comando e la gestione delle risorse. 

tooinstall hello CLI di Azure più recenti, seguire questi passaggi:

1. Eseguire i seguenti comandi in una finestra terminale hello. Potrebbe richiedere cinque minuti tooinstall hello CLI di Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Verificare l'installazione di hello eseguendo hello comando seguente:

   ```bash
   az iot -h
   ```

Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Riepilogo
È stato installato hello CLI di Azure. L'attività successiva è toocreate l'identità di hub e dispositivi Azure IoT utilizzando hello CLI di Azure.

## <a name="next-steps"></a>Passaggi successivi
[Creare l'hub IoT e registrare Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

