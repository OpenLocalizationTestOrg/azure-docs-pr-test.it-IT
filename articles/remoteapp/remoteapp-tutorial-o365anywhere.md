---
title: aaaGet hello stessa esperienza di Office 365 su qualsiasi dispositivo con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooshare qualsiasi app di Office 365 con gli utenti con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="e0e1a-103">Get hello stessa esperienza di Office 365 su qualsiasi dispositivo con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e0e1a-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e0e1a-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e0e1a-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e0e1a-106">In questo articolo illustra come toodeploy Office 365 su qualsiasi dispositivo nell'azienda.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="e0e1a-107">Gli utenti possono usare hello stesse funzionalità e di esperienza dell'interfaccia utente in Windows, Android e Apple.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="e0e1a-108">A questo scopo, si userà Azure RemoteApp mediante l’hosting di Office 365 in macchine virtuali scalabili di Azure a cui gli utenti possono connettersi.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="e0e1a-109">Questo set di macchine virtuali è detto "raccolta nel cloud".</span><span class="sxs-lookup"><span data-stu-id="e0e1a-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="e0e1a-110">Creare una raccolta nel cloud</span><span class="sxs-lookup"><span data-stu-id="e0e1a-110">Create a cloud collection</span></span>
<span data-ttu-id="e0e1a-111">Dopo aver creato un account Azure, passare troppo**RemoteApp** facendo clic sul collegamento hello hello lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="e0e1a-112">![Con Azure RemoteApp nel portale di Azure hello](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="e0e1a-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="e0e1a-113">Procedere quindi alla **nuova** nella parte inferiore di hello e "Creazione rapida" una raccolta.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="e0e1a-114">Specificare un nome area hello, sottoscrizione hello, piano hello e immagine hello "Proffesional Office 2013" fornito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="e0e1a-115">![Finestra di dialogo Crea](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="e0e1a-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="e0e1a-116">Al termine processo di creazione di hello modulo hello raccolta deve iniziare.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="e0e1a-117">Questa operazione potrebbe richiedere ore tooan o meno.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-117">This may take up tooan hour or so.</span></span>

![Waiting](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="e0e1a-119">Al termine il processo di hello, sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="e0e1a-120">Se si fa clic su **Pubblicazione** , si noterà che la maggior parte delle applicazioni di Office è già stata pubblicata.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="e0e1a-121">![Raccolta creata](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="e0e1a-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![App pubblicate](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="e0e1a-123">A questo punto è anche possibile aggiungere più utenti che hanno accesso toothis raccolta facendo **accesso utente**.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="e0e1a-124">![Configurare l'accesso utente](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="e0e1a-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="e0e1a-125">Ora si proverà timeout connessione tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="e0e1a-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="e0e1a-126">Connettersi tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="e0e1a-126">Connect tooOffice 365</span></span>
<span data-ttu-id="e0e1a-127">Si sarà head su troppo[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scorrere verso il basso e fare clic su **scaricare i client** client di Azure RemoteApp hello tooinstall sul dispositivo hello ci si trova.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="e0e1a-128">Hello schermate riportate di seguito sono per Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="e0e1a-129">Una volta avviata un'applicazione hello chiesto toosign con l'account Microsoft (precedentemente denominato "Live ID"), utilizzare hello corrisponde a quello dell'account di Azure per il momento.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="e0e1a-130">Dopo avere eseguito l'accesso dovrebbe essere visualizzata una notifica relativa a nuovi inviti. Fare clic sulla notifica per visualizzare un elenco come il seguente.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="e0e1a-131">Accettare l'invito hello corrispondente della posta elettronica del proprietario di account di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Nuovo invito](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="e0e1a-133">Ecco come appare la schermata quando sono presenti nuovi inviti.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-133">What it looks like when there are new invitations.</span></span>

![Accettare un'applicazione](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="e0e1a-135">Dopo avere accettato l'invito hello dovrebbe tutte le app di Office hello nel client di Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Elenco di app](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="e0e1a-137">Quando si sceglie uno di tali applicazioni, hello devono iniziare in hello macchina virtuale di Azure e dovrebbe essere tutto a posto.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="e0e1a-138">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="e0e1a-138">Enjoy!</span></span>

![Avvio](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

