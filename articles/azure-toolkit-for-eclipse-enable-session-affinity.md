---
title: "Abilitare l'affinità di sessione tramite il Toolkit di Azure per Eclipse"
description: "Informazioni su come abilitare l'affinità di sessione tramite il Toolkit di Azure per Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="bfa53-103">Abilitare l'affinità di sessione</span><span class="sxs-lookup"><span data-stu-id="bfa53-103">Enable Session Affinity</span></span>
<span data-ttu-id="bfa53-104">Nel Toolkit di Azure per Eclipse, è possibile abilitare l'affinità di sessione HTTP, o "sessioni permanenti", per i ruoli.</span><span class="sxs-lookup"><span data-stu-id="bfa53-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="bfa53-105">La figura seguente mostra la finestra di dialogo delle proprietà di **Bilanciamento del carico** utilizzata per abilitare la funzionalità di affinità di sessione:</span><span class="sxs-lookup"><span data-stu-id="bfa53-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="bfa53-106">Per abilitare l'affinità di sessione per il ruolo</span><span class="sxs-lookup"><span data-stu-id="bfa53-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="bfa53-107">Fare clic con il tasto destro del mouse sul ruolo in (Esplora progetti) di Eclipse, scegliere **Azure**, quindi fare clic su **Load Balancing** (Bilanciamento del carico).</span><span class="sxs-lookup"><span data-stu-id="bfa53-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="bfa53-108">Nella finestra di dialogo **Proprietà per il bilanciamento del carico del WorkerRole1** :</span><span class="sxs-lookup"><span data-stu-id="bfa53-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="bfa53-109">a.</span><span class="sxs-lookup"><span data-stu-id="bfa53-109">a.</span></span> <span data-ttu-id="bfa53-110">Controllare **Abilita l'affinità di sessione attiva HTTP (sessioni permanenti) per questo ruolo.**</span><span class="sxs-lookup"><span data-stu-id="bfa53-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="bfa53-111">b.</span><span class="sxs-lookup"><span data-stu-id="bfa53-111">b.</span></span> <span data-ttu-id="bfa53-112">Per gli **Input endpoint to use** (Endpoint di input da usare) selezionare un endpoint di input da usare, ad esempio, **http (public:80, private:8080)**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="bfa53-113">L'applicazione deve usare questo endpoint come l’endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfa53-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="bfa53-114">È possibile abilitare più endpoint per il ruolo, ma è possibile selezionare solo uno di essi per supportare le sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="bfa53-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="bfa53-115">c.</span><span class="sxs-lookup"><span data-stu-id="bfa53-115">c.</span></span> <span data-ttu-id="bfa53-116">Ricompilare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="bfa53-116">Rebuild your application.</span></span>

<span data-ttu-id="bfa53-117">Una volta abilitato, se si dispone di più di un'istanza del ruolo, le richieste HTTP provenienti da un determinato client continueranno ad essere gestite dalla stessa istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="bfa53-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="bfa53-118">Il Toolkit di Eclipse lo consente installando un modulo IIS speciale denominato Application Request Routing (ARR) in tutte le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="bfa53-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="bfa53-119">ARR reindirizza le richieste HTTP all'istanza del ruolo appropriato.</span><span class="sxs-lookup"><span data-stu-id="bfa53-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="bfa53-120">Il toolkit riconfigura automaticamente l'endpoint selezionato in modo che il traffico HTTP in ingresso viene instradato al software ARR.</span><span class="sxs-lookup"><span data-stu-id="bfa53-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="bfa53-121">Il toolkit crea anche un nuovo endpoint interno al quale server Java deve stare attenti per configurazione.</span><span class="sxs-lookup"><span data-stu-id="bfa53-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="bfa53-122">Si tratta dell'endpoint usato da ARR per reindirizzare il traffico HTTP all'istanza del ruolo appropriato.</span><span class="sxs-lookup"><span data-stu-id="bfa53-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="bfa53-123">In questo modo, ogni istanza del ruolo nella distribuzione multi-istanza funge da proxy inverso per tutte le altre istanze, abilitando le sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="bfa53-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="bfa53-124">Note sull'affinità di sessione</span><span class="sxs-lookup"><span data-stu-id="bfa53-124">Notes about session affinity</span></span>
* <span data-ttu-id="bfa53-125">L’affinità di sessione non funziona nell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="bfa53-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="bfa53-126">Le impostazioni possono essere applicate nell'emulatore di calcolo senza interferire con il processo di compilazione o con l’esecuzione dell'emulatore di calcolo, ma la funzionalità di per sé non funziona nell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="bfa53-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="bfa53-127">L’abilitazione dell’affinità di sessione comporterà un aumento della quantità di spazio nel disco preso dalla distribuzione in Azure, come software aggiuntivo verrà scaricato e installato nelle istanze del ruolo quando il servizio viene avviato nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa53-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="bfa53-128">Il tempo necessario per inizializzare ogni ruolo sarà maggiore.</span><span class="sxs-lookup"><span data-stu-id="bfa53-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="bfa53-129">Verrà aggiunto un endpoint interno, che fungerà da rerouter di traffico, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bfa53-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="bfa53-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bfa53-130">See Also</span></span>
<span data-ttu-id="bfa53-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bfa53-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="bfa53-132">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bfa53-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="bfa53-133">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bfa53-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="bfa53-134">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="bfa53-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
