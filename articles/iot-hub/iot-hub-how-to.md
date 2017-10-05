---
title: Utilizzo dell'hub IoT di Azure | Documentazione Microsoft
description: "In che modo gli sviluppatori usano le varie funzionalità di hub IoT?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="8ee5e-103">Procedure: Usare l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="8ee5e-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="8ee5e-104">Sono disponibili varie opzioni per apprendere come sviluppare per il servizio hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8ee5e-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="8ee5e-105">Leggere gli articoli concettuali che descrivono le funzionalità dell'hub IoT in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="8ee5e-106">Seguire una delle esercitazioni che illustrano le varie funzionalità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="8ee5e-107">Guida per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="8ee5e-107">Developer guide</span></span>

<span data-ttu-id="8ee5e-108">Gli sviluppatori possono leggere le linee guida teoriche e dettagliate relative all'hub IoT nella [Guida per gli sviluppatori][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="8ee5e-109">Questa guida include:</span><span class="sxs-lookup"><span data-stu-id="8ee5e-109">This guide includes:</span></span>

* <span data-ttu-id="8ee5e-110">Descrizioni dettagliate di tutte le funzionalità dell'hub IoT utili per imparare a usarle.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="8ee5e-111">Linee guida per la scelta quando sono disponibili più opzioni.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="8ee5e-112">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="8ee5e-112">Tutorials</span></span>

<span data-ttu-id="8ee5e-113">Se si preferisce apprendere le specifiche funzionalità di hub IoT tramite esercizi pratici, sono disponibili numerose esercitazioni tra cui scegliere.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="8ee5e-114">Molte esercitazioni sono disponibili anche in più linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="8ee5e-115">Le esercitazioni comprendono:</span><span class="sxs-lookup"><span data-stu-id="8ee5e-115">These tutorials include:</span></span>

- <span data-ttu-id="8ee5e-116">[Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route][lnk-routes-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="8ee5e-117">Questa esercitazione illustra come usare le regole di routing di hub IoT per inviare i messaggi da dispositivo a cloud con un semplice metodo basato sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="8ee5e-118">[Inviare messaggi da cloud a dispositivo con l'hub IoT][lnk-c2d-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="8ee5e-119">Questa esercitazione illustra come inviare messaggi dal cloud al dispositivo tramite l'hub IoT e ricevere messaggi dal cloud al dispositivo su un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="8ee5e-120">[Eseguire l'upload di file dai dispositivi al cloud con l'hub IoT][lnk-upload-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="8ee5e-121">Questa esercitazione illustra come usare le funzionalità di upload di file dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="8ee5e-122">[Introduzione ai dispositivi gemelli][lnk-twin-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="8ee5e-123">Questa esercitazione illustra i dispositivi gemelli, le proprietà segnalate, le proprietà desiderate e i tag.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="8ee5e-124">I dispositivi gemelli consentono di sincronizzare i valori dei dispositivi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="8ee5e-125">[Usare metodi diretti][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="8ee5e-126">Questa esercitazione illustra come usare metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="8ee5e-127">Aggiungere un gestore per un metodo diretto nel dispositivo simulato e richiamare il metodo diretto dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="8ee5e-128">[Introduzione alla gestione dei dispositivi][lnk-dm-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="8ee5e-129">Questa esercitazione illustra come usare le principali funzionalità di gestione dei dispositivi, ad esempio i dispositivi gemelli e i metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="8ee5e-130">Queste funzionalità consentono di riavviare in remoto il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="8ee5e-131">[Usare le proprietà desiderate per configurare i dispositivi][lnk-properties-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="8ee5e-132">Questa esercitazione illustra come usare le proprietà desiderate e segnalate del dispositivo gemello per configurare in remoto il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="8ee5e-133">[Usare i processi del dispositivo per avviare un aggiornamento del firmware del dispositivo][lnk-jobs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="8ee5e-134">Questa esercitazione illustra come usare le principali funzionalità di gestione dei dispositivi, ad esempio i dispositivi gemelli e i metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="8ee5e-135">Si impareranno a usare queste funzionalità per aggiornare in remoto il firmware del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="8ee5e-136">[Pianificare e trasmettere processi][lnk-schedule-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="8ee5e-137">Questa esercitazione illustra come usare le proprietà desiderate e i metodi diretti per interagire con più dispositivi a un orario pianificato.</span><span class="sxs-lookup"><span data-stu-id="8ee5e-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ee5e-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ee5e-138">Next steps</span></span>

<span data-ttu-id="8ee5e-139">Per altre informazioni sul servizio hub IoT, vedere la [Guida per gli sviluppatori][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="8ee5e-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md