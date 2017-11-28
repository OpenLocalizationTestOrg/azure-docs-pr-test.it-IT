---
title: aaaAdd archiviazione di Azure tramite i servizi connessi in Visual Studio | Documenti Microsoft
description: Aggiungere app tooyour di archiviazione di Azure tramite la finestra di dialogo di Visual Studio aggiungere servizi connessi hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="c9706-103">Aggiunta dell’archiviazione di Azure tramite Servizi connessi di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9706-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="c9706-104">Con Visual Studio, è possibile connettere uno qualsiasi dei seguenti tooAzure archiviazione utilizzando hello hello **aggiungere servizi connessi** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="c9706-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="c9706-105">Servizio cloud C#</span><span class="sxs-lookup"><span data-stu-id="c9706-105">C# cloud service</span></span>
- <span data-ttu-id="c9706-106">Servizio mobile back-end .NET</span><span class="sxs-lookup"><span data-stu-id="c9706-106">.NET backend mobile service</span></span>
- <span data-ttu-id="c9706-107">Sito Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c9706-107">ASP.NET website or service</span></span>
- <span data-ttu-id="c9706-108">Servizio ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c9706-108">ASP.NET Core service</span></span>
- <span data-ttu-id="c9706-109">Servizio Processo Web di Azure</span><span class="sxs-lookup"><span data-stu-id="c9706-109">Azure WebJob service</span></span> 

<span data-ttu-id="c9706-110">Hello funzionalità servizio connesso aggiunge tutti i riferimenti necessita hello e il progetto tooyour codice di connessione e modifica i file di configurazione in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="c9706-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="c9706-111">Dopo il completamento, hello **aggiungere servizi connessi** finestra di dialogo viene visualizzata automaticamente la documentazione che riporta in dettaglio hello passaggi necessari toostart utilizzo di archiviazione blob, code e tabelle.</span><span class="sxs-lookup"><span data-stu-id="c9706-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="c9706-112">La connessione di archiviazione tramite servizi connessi hello tooAzure finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="c9706-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="c9706-113">Aprire il progetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9706-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="c9706-114">In **Esplora soluzioni**, hello rapida **servizi connessi** nodo, quindi scegliere il menu di scelta rapida hello e selezionare **Aggiungi servizio connesso**.</span><span class="sxs-lookup"><span data-stu-id="c9706-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Aggiunta di un servizio connesso di Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="c9706-116">In hello **servizi connessi** selezionare **archiviazione Cloud con l'archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c9706-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Aggiungi Archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="c9706-118">In hello **di archiviazione di Azure** finestra di dialogo, selezionare un account di archiviazione esistente e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c9706-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="c9706-119">Se è necessario un account di archiviazione toocreate, andare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="c9706-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="c9706-120">In caso contrario, andare toostep 6.</span><span class="sxs-lookup"><span data-stu-id="c9706-120">Otherwise, skip toostep 6.</span></span>
    
    ![Aggiungere tooproject di account di archiviazione esistente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="c9706-122">toocreate un account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="c9706-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="c9706-123">Selezionare **creare un nuovo Account di archiviazione** nella parte inferiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c9706-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="c9706-124">Compilare hello **crea Account di archiviazione** finestra di dialogo e selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="c9706-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nuovo account di archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="c9706-126">Quando hello **di archiviazione di Azure** viene visualizzata una finestra di dialogo, il nuovo account di archiviazione hello viene visualizzato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="c9706-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="c9706-127">Selezionare il nuovo account di archiviazione hello nell'elenco di hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c9706-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="c9706-128">Hello archiviazione servizio connesso viene visualizzato sotto hello **riferimenti al servizio** nodo del progetto.</span><span class="sxs-lookup"><span data-stu-id="c9706-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="c9706-129">Come viene modificato il progetto</span><span class="sxs-lookup"><span data-stu-id="c9706-129">How your project is modified</span></span>
<span data-ttu-id="c9706-130">Quando si termina dialogo hello, Visual Studio aggiunge i riferimenti e modifica alcuni file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c9706-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="c9706-131">modifiche specifiche Hello dipendono dal tipo di progetto hello:</span><span class="sxs-lookup"><span data-stu-id="c9706-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="c9706-132">Progetti ASP.NET - [Risultati – Progetti ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126).</span><span class="sxs-lookup"><span data-stu-id="c9706-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="c9706-133">Progetti ASP.NET 5 - [Risultati – Progetti ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124).</span><span class="sxs-lookup"><span data-stu-id="c9706-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="c9706-134">Progetti del servizio cloud (ruoli Web e ruoli di lavoro) [Risultati - Progetti del servizio cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965).</span><span class="sxs-lookup"><span data-stu-id="c9706-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="c9706-135">Progetti di tipo processo Web - [Risultati - Progetti di tipo processo Web](visual-studio/vs-storage-webjobs-what-happened.md).</span><span class="sxs-lookup"><span data-stu-id="c9706-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9706-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9706-136">Next steps</span></span>
- [<span data-ttu-id="c9706-137">Forum MSDN: Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c9706-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- <span data-ttu-id="c9706-138">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="c9706-138">[Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
- [<span data-ttu-id="c9706-139">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c9706-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
