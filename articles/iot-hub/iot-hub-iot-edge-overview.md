---
title: Panoramica di Azure IoT Edge | Microsoft Docs
description: Descrive i concetti principali dell'architettura di Azure IoT Edge, come gateway, moduli e broker.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="8a0e3-103">Concetti dell'architettura di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="8a0e3-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="8a0e3-104">Prima di esaminare il codice di esempio o di creare un gateway sul campo usando IoT Edge, è necessario conoscere i concetti principali che supportano l'architettura di IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="8a0e3-105">Moduli di IoT Edge</span><span class="sxs-lookup"><span data-stu-id="8a0e3-105">IoT Edge modules</span></span>

<span data-ttu-id="8a0e3-106">Per compilare un gateway con Azure IoT Edge, è necessario creare e assemblare i *moduli di IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="8a0e3-107">I moduli usano *messaggi* per scambiarsi dati tra loro.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="8a0e3-108">Un modulo riceve un messaggio, esegue un'azione su di esso, lo trasforma facoltativamente in un nuovo messaggio e quindi lo pubblica per l'elaborazione da parte di altri moduli.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="8a0e3-109">Alcuni moduli potrebbero produrre solo nuovi messaggi e non elaborare mai i messaggi in arrivo.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="8a0e3-110">Una catena di moduli crea una pipeline di elaborazione dei dati in cui ogni modulo esegue una trasformazione sui dati in un punto nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Catena di moduli nel gateway compilati con Azure IoT Edge][1]

<span data-ttu-id="8a0e3-112">IoT Edge contiene i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a0e3-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="8a0e3-113">Moduli già scritti che eseguono funzioni di gateway comuni.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="8a0e3-114">Le interfacce che uno sviluppatore può usare per scrivere i moduli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="8a0e3-115">L'infrastruttura necessaria per distribuire ed eseguire un set di moduli.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="8a0e3-116">L'SDK offre un livello di astrazione che consente di compilare gateway da eseguire in vari sistemi operativi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Livello di astrazione di Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="8a0e3-118">Messaggi</span><span class="sxs-lookup"><span data-stu-id="8a0e3-118">Messages</span></span>

<span data-ttu-id="8a0e3-119">Nonostante sia più semplice concettualizzare il funzionamento di un gateway come una trasmissione di messaggi tra moduli, ciò non lo riflette con precisione.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="8a0e3-120">I moduli di IoT Edge usano un broker per comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="8a0e3-121">I moduli pubblicano i messaggi nel broker tramite modelli di messaggistica, ad esempio bus o pubblicazione/sottoscrizione, e consentono al broker di instradare il messaggio ai moduli a esso connessi.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="8a0e3-122">Un modulo usa la funzione **Broker_Publish** per pubblicare un messaggio nel broker.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="8a0e3-123">Il broker recapita i messaggi a un modulo richiamando una funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="8a0e3-124">Un messaggio è costituito da un set di proprietà chiave/valore e contenuto passato come blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Ruolo del broker in Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="8a0e3-126">Routing e filtro dei messaggi</span><span class="sxs-lookup"><span data-stu-id="8a0e3-126">Message routing and filtering</span></span>

<span data-ttu-id="8a0e3-127">Per indirizzare i messaggi ai moduli di IoT Edge corretti, è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="8a0e3-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="8a0e3-128">È possibile passare un set di collegamenti al broker in modo che conosca l'origine e il sink di ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="8a0e3-129">Un modulo può filtrare le proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="8a0e3-130">Un modulo deve agire unicamente sui messaggi a esso destinati.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="8a0e3-131">I collegamenti e il filtro dei messaggi creano una pipeline dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="8a0e3-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a0e3-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a0e3-132">Next steps</span></span>

<span data-ttu-id="8a0e3-133">Per vedere l'applicazione di questi concetti in un esempio eseguibile, vedere [Esplorare l'architettura di Azure IoT Edge in Linux][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="8a0e3-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md