---
title: aaaOverview del bordo IoT di Azure | Documenti Microsoft
description: Viene descritto hello architetturale concetti chiave di Azure IoT Edge come gateway, i moduli e istanze di Service Broker.
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="a449e-103">Concetti dell'architettura di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a449e-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="a449e-104">Prima di esaminare qualsiasi codice di esempio o creare proprio gateway di campo tramite IoT Edge, è necessario comprendere i concetti chiave hello che supportano l'architettura di hello del bordo IoT.</span><span class="sxs-lookup"><span data-stu-id="a449e-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="a449e-105">Moduli di IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a449e-105">IoT Edge modules</span></span>

<span data-ttu-id="a449e-106">Per compilare un gateway con Azure IoT Edge, è necessario creare e assemblare i *moduli di IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="a449e-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="a449e-107">Utilizzano i moduli *messaggi* tooexchange dati tra loro.</span><span class="sxs-lookup"><span data-stu-id="a449e-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="a449e-108">Un modulo riceve un messaggio, esegue un'azione su di esso, facoltativamente, li trasforma in un nuovo messaggio e pubblica quindi per tooprocess altri moduli.</span><span class="sxs-lookup"><span data-stu-id="a449e-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="a449e-109">Alcuni moduli potrebbero produrre solo nuovi messaggi e non elaborare mai i messaggi in arrivo.</span><span class="sxs-lookup"><span data-stu-id="a449e-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="a449e-110">Una catena di moduli crea una pipeline di elaborazione dei dati con ogni modulo eseguendo una trasformazione sui dati hello in un determinato punto nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="a449e-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Catena di moduli nel gateway compilati con Azure IoT Edge][1]

<span data-ttu-id="a449e-112">Bordo IoT contiene hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="a449e-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="a449e-113">Moduli già scritti che eseguono funzioni di gateway comuni.</span><span class="sxs-lookup"><span data-stu-id="a449e-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="a449e-114">interfacce Hello un sviluppatore possono utilizzare moduli personalizzati toowrite.</span><span class="sxs-lookup"><span data-stu-id="a449e-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="a449e-115">Hello infrastruttura necessarie toodeploy ed eseguire un set di moduli.</span><span class="sxs-lookup"><span data-stu-id="a449e-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="a449e-116">Hello SDK fornisce un livello di astrazione che consente di toobuild gateway toorun in vari sistemi operativi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="a449e-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Livello di astrazione di Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="a449e-118">Messaggi</span><span class="sxs-lookup"><span data-stu-id="a449e-118">Messages</span></span>

<span data-ttu-id="a449e-119">Sebbene pensa moduli passando tooeach altri messaggi è un modo pratico di tooconceptualize funzionamento di un gateway, non in modo accurato riflette cosa accade.</span><span class="sxs-lookup"><span data-stu-id="a449e-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="a449e-120">I moduli di IoT Edge utilizzano un toocommunicate broker tra loro.</span><span class="sxs-lookup"><span data-stu-id="a449e-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="a449e-121">I moduli pubblicano broker toohello messaggi (tramite modelli di messaggistica, ad esempio, bus o di pubblicazione/sottoscrizione) e quindi consentono hello broker route hello messaggio toohello moduli connesso tooit.</span><span class="sxs-lookup"><span data-stu-id="a449e-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="a449e-122">Un modulo Usa hello **Broker_Publish** funzione toopublish un broker toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="a449e-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="a449e-123">broker di Hello recapita modulo tooa messaggi richiamando una funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="a449e-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="a449e-124">Un messaggio è costituito da un set di proprietà chiave/valore e contenuto passato come blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="a449e-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![ruolo Hello di Service Broker in Azure IoT Edge hello][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="a449e-126">Routing e filtro dei messaggi</span><span class="sxs-lookup"><span data-stu-id="a449e-126">Message routing and filtering</span></span>

<span data-ttu-id="a449e-127">Esistono due modi toodirect messaggi toohello corretto IoT bordo i moduli:</span><span class="sxs-lookup"><span data-stu-id="a449e-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="a449e-128">È possibile passare un set di collegamenti possono essere passati broker toohello in modo da Service broker hello hello origine e sink per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="a449e-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="a449e-129">Un modulo è possibile filtrare per proprietà hello del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="a449e-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="a449e-130">Un modulo deve agire solo su un messaggio se il messaggio hello destinato.</span><span class="sxs-lookup"><span data-stu-id="a449e-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="a449e-131">I collegamenti e il filtro dei messaggi creano una pipeline dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="a449e-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a449e-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a449e-132">Next steps</span></span>

<span data-ttu-id="a449e-133">toosee questi concetti applicati in un esempio è possibile eseguire, vedere [architettura esplorare Azure IoT Edge][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="a449e-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md