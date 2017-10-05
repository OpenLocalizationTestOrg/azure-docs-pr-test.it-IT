---
title: Aggiungere spazio di archiviazione di Azure mediante Servizi connessi in Visual Studio | Documentazione Microsoft
description: Aggiungere archiviazione di Azure all'applicazione usando la finestra di dialogo Aggiungi servizi connessi di Visual Studio
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
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="2b041-103">Aggiunta dell’archiviazione di Azure tramite Servizi connessi di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b041-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="2b041-104">Con Visual Studio è possibile connettere uno dei servizi seguenti ad Archiviazione di Azure tramite la finestra di dialogo **Add Connected Services** (Aggiungi servizi connessi):</span><span class="sxs-lookup"><span data-stu-id="2b041-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="2b041-105">Servizio cloud C#</span><span class="sxs-lookup"><span data-stu-id="2b041-105">C# cloud service</span></span>
- <span data-ttu-id="2b041-106">Servizio mobile back-end .NET</span><span class="sxs-lookup"><span data-stu-id="2b041-106">.NET backend mobile service</span></span>
- <span data-ttu-id="2b041-107">Sito Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2b041-107">ASP.NET website or service</span></span>
- <span data-ttu-id="2b041-108">Servizio ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2b041-108">ASP.NET Core service</span></span>
- <span data-ttu-id="2b041-109">Servizio Processo Web di Azure</span><span class="sxs-lookup"><span data-stu-id="2b041-109">Azure WebJob service</span></span> 

<span data-ttu-id="2b041-110">La funzionalità servizio connesso aggiunge al progetto tutti i riferimenti richiesti e il codice di connessione e modifica i file di configurazione in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="2b041-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="2b041-111">Dopo il completamento, la finestra di dialogo **Add Connected Services** (Aggiungi servizi connessi) visualizza automaticamente la documentazione che illustra in dettaglio i passaggi necessari per iniziare a lavorare con l'archiviazione BLOB, le code e le tabelle.</span><span class="sxs-lookup"><span data-stu-id="2b041-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="2b041-112">Connettersi ad archiviazione di Azure usando la finestra di dialogo Servizi connessi</span><span class="sxs-lookup"><span data-stu-id="2b041-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="2b041-113">Aprire il progetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b041-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="2b041-114">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Servizi connessi** e scegliere **Add Connected Services** (Aggiungi servizi connessi) dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="2b041-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Aggiunta di un servizio connesso di Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="2b041-116">Nella pagina **Servizi connessi** selezionare **Archiviazione cloud con Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b041-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Aggiungi Archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="2b041-118">Nella finestra di dialogo **Archiviazione di Azure** selezionare un account di archiviazione esistente, quindi **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2b041-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="2b041-119">Se è necessario creare un account di archiviazione, andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="2b041-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="2b041-120">In caso contrario, andare direttamente al passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="2b041-120">Otherwise, skip to step 6.</span></span>
    
    ![Aggiungere un account di archiviazione esistente al progetto l'elenco](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="2b041-122">Per creare un account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="2b041-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="2b041-123">Nella parte inferiore della finestra di dialogo fare clic su **Crea un nuovo account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="2b041-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="2b041-124">Compilare la finestra di dialogo **Crea account di archiviazione** e selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2b041-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nuovo account di archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="2b041-126">Quando viene visualizzata la finestra di dialogo **Archiviazione di Azure**, la nuova risorsa di archiviazione viene visualizzata nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2b041-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="2b041-127">Selezionare la nuova risorsa di archiviazione nell'elenco e quindi **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2b041-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="2b041-128">Il servizio connesso di archiviazione viene visualizzato sotto il nodo **Riferimenti servizio** del progetto.</span><span class="sxs-lookup"><span data-stu-id="2b041-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="2b041-129">Come viene modificato il progetto</span><span class="sxs-lookup"><span data-stu-id="2b041-129">How your project is modified</span></span>
<span data-ttu-id="2b041-130">Una volta terminata la finestra di dialogo, Visual Studio aggiunge riferimenti e modifica di alcuni file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2b041-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="2b041-131">Le modifiche specifiche dipendono dal tipo di progetto.</span><span class="sxs-lookup"><span data-stu-id="2b041-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="2b041-132">Progetti ASP.NET - [Risultati – Progetti ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126).</span><span class="sxs-lookup"><span data-stu-id="2b041-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="2b041-133">Progetti ASP.NET 5 - [Risultati – Progetti ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124).</span><span class="sxs-lookup"><span data-stu-id="2b041-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="2b041-134">Progetti del servizio cloud (ruoli Web e ruoli di lavoro) [Risultati - Progetti del servizio cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965).</span><span class="sxs-lookup"><span data-stu-id="2b041-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="2b041-135">Progetti di tipo processo Web - [Risultati - Progetti di tipo processo Web](visual-studio/vs-storage-webjobs-what-happened.md).</span><span class="sxs-lookup"><span data-stu-id="2b041-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b041-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b041-136">Next steps</span></span>
- [<span data-ttu-id="2b041-137">Forum MSDN: Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2b041-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- <span data-ttu-id="2b041-138">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="2b041-138">[Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
- [<span data-ttu-id="2b041-139">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2b041-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
