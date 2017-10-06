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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="12253-104">Configurare il caricamento di file di IoT Hub mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="12253-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="12253-105">Caricamento di file</span><span class="sxs-lookup"><span data-stu-id="12253-105">File upload</span></span>

<span data-ttu-id="12253-106">hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub.</span><span class="sxs-lookup"><span data-stu-id="12253-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="12253-107">Selezionare **caricamento del File** toodisplay un elenco di proprietà di caricamento di file per l'hub IoT hello che è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="12253-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Visualizza file IoT Hub caricare le impostazioni nel portale di hello][13]

<span data-ttu-id="12253-109">**Contenitore di archiviazione**: utilizzare un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'IoT Hub di Azure tooselect portale hello.</span><span class="sxs-lookup"><span data-stu-id="12253-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="12253-110">Se necessario, è possibile creare un account di archiviazione di Azure su hello **gli account di archiviazione** contenitore blob e blade in hello **contenitori** blade.</span><span class="sxs-lookup"><span data-stu-id="12253-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="12253-111">IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="12253-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Visualizzare i contenitori di archiviazione per il caricamento di file nel portale di hello][14]

<span data-ttu-id="12253-113">**Ricevere notifiche per i file caricati**: abilitare o disabilitare le notifiche di caricamento di file tramite attiva/disattiva hello.</span><span class="sxs-lookup"><span data-stu-id="12253-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="12253-114">**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12253-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="12253-115">Tooone ora l'impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.</span><span class="sxs-lookup"><span data-stu-id="12253-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="12253-116">**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere.</span><span class="sxs-lookup"><span data-stu-id="12253-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="12253-117">Impostare tooone giorno per impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.</span><span class="sxs-lookup"><span data-stu-id="12253-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="12253-118">**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="12253-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="12253-119">Too10 l'impostazione predefinita, ma possono essere valori tooother personalizzato con dispositivo di scorrimento hello.</span><span class="sxs-lookup"><span data-stu-id="12253-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Configurare il caricamento di file IoT Hub nel portale di hello][15]

## <a name="next-steps"></a><span data-ttu-id="12253-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12253-121">Next steps</span></span>

<span data-ttu-id="12253-122">Per ulteriori informazioni sulle funzionalità di caricamento file hello dell'IoT Hub, vedere [caricare i file da un dispositivo] [ lnk-upload] nella Guida per sviluppatori di IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="12253-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="12253-123">Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12253-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="12253-124">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="12253-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="12253-125">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="12253-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="12253-126">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="12253-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="12253-127">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="12253-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="12253-128">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="12253-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="12253-129">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="12253-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="12253-130">[Soluzione IoT da hello la messa a terra sicura][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="12253-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
