---
title: Usare il portale di Azure per configurare il caricamento dei file | Microsoft Docs
description: Come usare il portale di Azure per configurare l'hub IoT per abilitare i caricamenti di file da dispositivi connessi. Include informazioni sulla configurazione dell'account di archiviazione di Azure di destinazione.
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
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="5d937-104">Configurare i caricamenti dei file nell'hub IoT con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5d937-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="5d937-105">Caricamento di file</span><span class="sxs-lookup"><span data-stu-id="5d937-105">File upload</span></span>

<span data-ttu-id="5d937-106">Per usare la [funzionalità di caricamento di file nell'hub IoT][lnk-upload], è prima di tutto necessario associare un account di archiviazione di Azure all'hub.</span><span class="sxs-lookup"><span data-stu-id="5d937-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="5d937-107">Selezionare **Caricamento del file** per visualizzare un elenco di proprietà di caricamento del file per l'hub IoT da modificare.</span><span class="sxs-lookup"><span data-stu-id="5d937-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Visualizzare le impostazioni di caricamento di file dell'hub IoT nel portale][13]

<span data-ttu-id="5d937-109">**Contenitore di archiviazione**: usare il portale di Azure per selezionare il contenitore BLOB in un account di archiviazione di Azure nella sottoscrizione corrente da associare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d937-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="5d937-110">Se necessario, è possibile creare un account di archiviazione di Azure nel pannello **Account di archiviazione** e un nuovo contenitore BLOB nel pannello **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="5d937-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="5d937-111">L'hub IoT genera automaticamente URI di firma di accesso condiviso con autorizzazioni di scrittura per questo contenitore BLOB che possono essere usati dai dispositivi durante il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="5d937-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Visualizzare i contenitori di archiviazione per il caricamento di file nel portale][14]

<span data-ttu-id="5d937-113">**Receive notifications for uploaded files**(Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file mediante l'apposita opzione.</span><span class="sxs-lookup"><span data-stu-id="5d937-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="5d937-114">**SAS TTL**(TTL di firma di accesso condiviso): questa impostazione indica la durata degli URI di firma di accesso condiviso restituiti dal dispositivo tramite l’hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d937-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="5d937-115">Per impostazione predefinita è impostato su un'ora, ma può essere personalizzato con altri valori tramite il dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="5d937-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="5d937-116">**File notification settings default TTL**(TTL predefinito per le impostazioni di notifica dei file): durata di una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="5d937-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="5d937-117">Per impostazione predefinita è impostato su un giorno, ma può essere personalizzato con altri valori tramite il dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="5d937-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="5d937-118">**File notification maximum delivery count**(Numero massimo di recapiti per le notifiche dei file): numero di tentativi che verranno eseguiti dall'hub IoT per distribuire una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="5d937-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="5d937-119">Per impostazione predefinita è impostato su 10, ma può essere personalizzato con altri valori tramite il dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="5d937-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Configurare il caricamento di file dell'hub IoT nel portale][15]

## <a name="next-steps"></a><span data-ttu-id="5d937-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d937-121">Next steps</span></span>

<span data-ttu-id="5d937-122">Per altre informazioni sulle funzionalità di caricamento dei file dell'hub IoT, vedere [Caricare file da un dispositivo][lnk-upload] nella Guida per gli sviluppatori dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d937-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="5d937-123">Per ulteriori informazioni sulla gestione dell'hub IoT di Azure, consultare questi collegamenti:</span><span class="sxs-lookup"><span data-stu-id="5d937-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5d937-124">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="5d937-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="5d937-125">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5d937-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5d937-126">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5d937-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5d937-127">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="5d937-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5d937-128">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5d937-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5d937-129">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5d937-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="5d937-130">[Proteggere la soluzione IoT sin dall'inizio][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5d937-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
