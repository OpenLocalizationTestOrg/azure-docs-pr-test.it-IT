---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 2: strumenti di Azure (Windows) | Documenti Microsoft'
description: Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure) in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interfaccia della riga di comando di azure, servizio cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0a2e941119f9106add708591d52f32eb9ed08451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Ottenere gli strumenti di Azure (Windows 7 e versioni successive)
> [!div class="op_single_selector"]
> * [Windows 7 e versioni successive][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure). Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* Come tooinstall Python.
* Come tooinstall hello CLI di Azure.

## <a name="what-you-need"></a>Elementi necessari
* Un computer Windows con connessione Internet.
* Una sottoscrizione di Azure attiva. Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.

## <a name="install-python"></a>Installare Python
[Installare Python](https://www.python.org/downloads/) nel computer Windows. È possibile installare Python 2.7, 3.4 o 3.5. Questa esercitazione è basata su Python 2.7. Se è già stato installato Python, andare nella sezione successiva toohello e installare hello CLI di Azure.

È inoltre necessario percorso hello tooadd delle cartelle hello in python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente. Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Installare hello CLI di Azure
Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure. Si lavora direttamente da tooprovision la riga di comando e la gestione delle risorse.

hello tooinstall CLI di Azure, seguire questi passaggi:

1. Aprire una finestra del Prompt dei comandi come amministratore.
2. Eseguire hello seguenti comandi:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Verificare l'installazione di hello eseguendo hello comando seguente:

   ```cmd
   az iot -h
   ```

Viene visualizzato l'output seguente hello se installazione hello ha esito positivo.

![Output che indica l'esito positivo](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Riepilogo
È stato installato hello CLI di Azure. La prossima attività toocreate l'identità di Azure IoT hub e dispositivi tramite hello CLI di Azure.

## <a name="next-steps"></a>Passaggi successivi
[Creare l'hub IoT e registrare Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
