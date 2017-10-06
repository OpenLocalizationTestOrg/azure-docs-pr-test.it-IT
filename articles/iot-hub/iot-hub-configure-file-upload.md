---
title: caricamento del file hello tooconfigure portale Azure aaaUse | Documenti Microsoft
description: Come toouse hello Azure tooconfigure portale il file di IoT hub tooenable caricamenti da dispositivi connessi. Include informazioni sulla configurazione di account di archiviazione di Azure di destinazione hello.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Configurare il caricamento di file di IoT Hub mediante hello portale di Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Caricamento di file

hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub. Selezionare **caricamento del File** toodisplay un elenco di proprietà di caricamento di file per l'hub IoT hello che è stato modificato.

![Visualizza file IoT Hub caricare le impostazioni nel portale di hello][13]

**Contenitore di archiviazione**: utilizzare un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'IoT Hub di Azure tooselect portale hello. Se necessario, è possibile creare un account di archiviazione di Azure su hello **gli account di archiviazione** contenitore blob e blade in hello **contenitori** blade. IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.

![Visualizzare i contenitori di archiviazione per il caricamento di file nel portale di hello][14]

**Ricevere notifiche per i file caricati**: abilitare o disabilitare le notifiche di caricamento di file tramite attiva/disattiva hello.

**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub. Tooone ora l'impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.

**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere. Impostare tooone giorno per impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.

**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello. Too10 l'impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.

![Configurare il caricamento di file IoT Hub nel portale di hello][15]

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle funzionalità di caricamento file hello dell'IoT Hub, vedere [caricare i file da un dispositivo] [ lnk-upload] nella Guida per sviluppatori di IoT Hub hello.

Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:

* [Gestire in blocco i dispositivi IoT][lnk-bulk]
* [Metriche di Hub IoT][lnk-metrics]
* [Monitoraggio delle operazioni][lnk-monitor]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]
* [Soluzione IoT da hello la messa a terra sicura][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
