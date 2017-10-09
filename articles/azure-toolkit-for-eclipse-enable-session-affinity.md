---
title: "utilizzo di affinità di sessione aaaEnable hello Azure Toolkit per Eclipse"
description: "Informazioni su come l'affinità di sessione tooenable utilizzando hello Azure Toolkit per Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="02421-103">Abilitare l'affinità di sessione</span><span class="sxs-lookup"><span data-stu-id="02421-103">Enable Session Affinity</span></span>
<span data-ttu-id="02421-104">All'interno di hello Azure Toolkit per Eclipse, è possibile abilitare l'affinità di sessione HTTP, o "sessioni permanenti", per i ruoli.</span><span class="sxs-lookup"><span data-stu-id="02421-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="02421-105">Hello immagine seguente viene illustrato hello **il bilanciamento del carico** funzionalità affinità di sessione di proprietà finestra di dialogo utilizzata tooenable hello:</span><span class="sxs-lookup"><span data-stu-id="02421-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="02421-106">tooenable l'affinità di sessione per il ruolo</span><span class="sxs-lookup"><span data-stu-id="02421-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="02421-107">Fare doppio clic su ruolo hello in Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **il bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="02421-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="02421-108">In hello **proprietà per il bilanciamento del carico WorkerRole1** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="02421-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="02421-109">a.</span><span class="sxs-lookup"><span data-stu-id="02421-109">a.</span></span> <span data-ttu-id="02421-110">Controllare **Abilita l'affinità di sessione attiva HTTP (sessioni permanenti) per questo ruolo.**</span><span class="sxs-lookup"><span data-stu-id="02421-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="02421-111">b.</span><span class="sxs-lookup"><span data-stu-id="02421-111">b.</span></span> <span data-ttu-id="02421-112">Per **toouse endpoint di Input**, selezionare toouse un endpoint di input, ad esempio, **http (public: 80, private: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="02421-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="02421-113">L'applicazione deve usare questo endpoint come l’endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="02421-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="02421-114">È possibile abilitare più endpoint per il ruolo, ma è possibile selezionare solo uno di essi toosupport sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="02421-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="02421-115">c.</span><span class="sxs-lookup"><span data-stu-id="02421-115">c.</span></span> <span data-ttu-id="02421-116">Ricompilare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="02421-116">Rebuild your application.</span></span>

<span data-ttu-id="02421-117">Una volta abilitato, se si dispone di più istanze di ruolo, le richieste HTTP provenienti da un client specifico continuerà gestita da hello stessa istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="02421-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="02421-118">Hello Eclipse Toolkit lo consente installando un modulo IIS speciale denominato Application Request Routing (ARR) in ognuna delle istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="02421-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="02421-119">ARR reindirizza l'istanza del ruolo appropriata toohello le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="02421-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="02421-120">Hello toolkit riconfigura automaticamente l'endpoint hello selezionata in modo che il traffico HTTP in ingresso hello è primo toohello indirizzato ARR software.</span><span class="sxs-lookup"><span data-stu-id="02421-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="02421-121">Hello toolkit crea anche un nuovo endpoint interno che toolisten configurato per il server Java.</span><span class="sxs-lookup"><span data-stu-id="02421-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="02421-122">Ovvero endpoint hello utilizzato dall'istanza di ruolo appropriato di ARR tooreroute hello HTTP traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="02421-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="02421-123">In questo modo, ogni istanza del ruolo nella distribuzione multi-istanza funge da proxy inverso per tutti hello altri casi, l'abilitazione di sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="02421-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="02421-124">Note sull'affinità di sessione</span><span class="sxs-lookup"><span data-stu-id="02421-124">Notes about session affinity</span></span>
* <span data-ttu-id="02421-125">Affinità di sessione non funziona nell'emulatore di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="02421-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="02421-126">Hello impostazioni possono essere applicate nell'emulatore di calcolo hello senza interferire con il processo di compilazione o dell'esecuzione dell'emulatore di calcolo, ma non funziona nell'emulatore di calcolo hello funzionalità hello stessa.</span><span class="sxs-lookup"><span data-stu-id="02421-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="02421-127">Abilitazione di affinità di sessione comporterà un aumento della quantità di hello di spazio su disco occupato dalla distribuzione in Azure, come verrà scaricato e installato nelle istanze del ruolo quando il servizio viene avviato nel cloud di Azure hello software aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="02421-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="02421-128">Hello ora tooinitialize ogni ruolo richiederà più tempo.</span><span class="sxs-lookup"><span data-stu-id="02421-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="02421-129">Verrà aggiunto un endpoint interno, toofunction come rerouter un traffico, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="02421-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="02421-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="02421-130">See Also</span></span>
<span data-ttu-id="02421-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02421-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="02421-132">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02421-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="02421-133">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02421-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="02421-134">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="02421-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
