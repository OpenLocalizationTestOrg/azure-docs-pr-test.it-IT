---
title: gli account di archiviazione aaaManage utilizzando hello Azure Explorer per Eclipse | Documenti Microsoft
description: Informazioni su come toomanage account di archiviazione di Azure tramite hello Azure Explorer per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="65035-103">Gestire gli account di archiviazione tramite hello Azure Explorer per Eclipse</span><span class="sxs-lookup"><span data-stu-id="65035-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="65035-104">Hello Esplora Azure, che fa parte di hello Azure Toolkit per Eclipse, fornisce agli sviluppatori di Java con una soluzione da usare per la gestione degli account di archiviazione nel proprio account da Azure all'interno di ambiente di sviluppo integrato (IDE) di hello Eclipse.</span><span class="sxs-lookup"><span data-stu-id="65035-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="65035-105">Creazione di un account di archiviazione in Eclipse</span><span class="sxs-lookup"><span data-stu-id="65035-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="65035-106">un account di archiviazione tramite Esplora Azure hello toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="65035-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="65035-107">Accedi tooyour account Azure tramite hello [accesso le istruzioni per hello Azure Toolkit per Eclipse].</span><span class="sxs-lookup"><span data-stu-id="65035-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="65035-108">In hello **Esplora Azure** visualizzare, espandere hello **Azure** nodo, fare doppio clic su **gli account di archiviazione**, quindi fare clic su **crea Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="65035-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando Crea account di archiviazione][CS01]

3. <span data-ttu-id="65035-110">In hello **crea Account di archiviazione** finestra di dialogo specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="65035-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Finestra di dialogo Crea un nuovo account di archiviazione][CS02]

   * <span data-ttu-id="65035-112">**Nome**: Specifica il nome di hello hello nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65035-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="65035-113">**Sottoscrizione**: specifica sottoscrizione di Azure che si vuole toouse per il nuovo account di archiviazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="65035-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="65035-114">**Gruppo di risorse**: Specifica il gruppo di risorse hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="65035-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="65035-115">Selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="65035-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="65035-116">**Crea nuovo**: Specifica che si desidera toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="65035-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="65035-117">**Usa esistente**: specifica che sarà possibile scegliere in un elenco i gruppi di risorse associate all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="65035-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="65035-118">**Area**: Specifica il percorso di hello in cui verranno creati account di archiviazione (ad esempio, "Stati Uniti occidentali").</span><span class="sxs-lookup"><span data-stu-id="65035-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="65035-119">**Tipo di conto**: Specifica il tipo di hello di toocreate di account di archiviazione (ad esempio, "archiviazione Blob").</span><span class="sxs-lookup"><span data-stu-id="65035-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="65035-120">Per altre informazioni, vedere [Informazioni sugli account di archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="65035-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="65035-121">**Prestazioni**: specifica l'account di archiviazione offerta toouse dal server di pubblicazione selezionato hello (ad esempio, "Premium").</span><span class="sxs-lookup"><span data-stu-id="65035-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="65035-122">Per altre informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="65035-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="65035-123">**Replica**: specifica la replica di hello hello account di archiviazione (ad esempio, "con ridondanza della zona").</span><span class="sxs-lookup"><span data-stu-id="65035-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="65035-124">Per altre informazioni, vedere [Replica di Archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="65035-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="65035-125">Dopo aver specificato tutti hello opzioni precedenti, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="65035-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="65035-126">Creazione di un contenitore di archiviazione in Eclipse</span><span class="sxs-lookup"><span data-stu-id="65035-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="65035-127">un contenitore di archiviazione tramite Esplora Azure hello toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="65035-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="65035-128">In hello **Esplora Azure** visualizzare, fare doppio clic su account di archiviazione hello in cui si desidera toocreate un contenitore e quindi fare clic su **crea contenitore blob**.</span><span class="sxs-lookup"><span data-stu-id="65035-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Comando Crea contenitore BLOB][CC01]

2. <span data-ttu-id="65035-130">In hello **crea contenitore blob** la finestra di dialogo, specificare nome hello per il contenitore e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="65035-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="65035-131">Per altre informazioni sulla denominazione dei contenitori di archiviazione, vedere l'articolo relativo alla [denominazione e riferimento a contenitori, BLOB e metadati].</span><span class="sxs-lookup"><span data-stu-id="65035-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Finestra di dialogo Crea contenitore BLOB][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="65035-133">Eliminazione di un contenitore di archiviazione in Eclipse</span><span class="sxs-lookup"><span data-stu-id="65035-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="65035-134">un contenitore di archiviazione tramite Esplora Azure hello toodelete hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="65035-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="65035-135">In hello **Esplora Azure** consente di visualizzare, fare doppio clic su contenitore di archiviazione hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="65035-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Comando Elimina contenitore di archiviazione][DC01]

2. <span data-ttu-id="65035-137">Nella finestra di conferma hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="65035-137">In hello confirmation window, click **OK**.</span></span>

   ![Finestra di conferma dell'eliminazione del contenitore di archiviazione][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="65035-139">Eliminazione di un account di archiviazione in Eclipse</span><span class="sxs-lookup"><span data-stu-id="65035-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="65035-140">un account di archiviazione tramite Esplora Azure hello toodelete hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="65035-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="65035-141">In hello **Esplora Azure** consente di visualizzare, fare doppio clic su account di archiviazione hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="65035-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Comando Elimina account di archiviazione][DS01]

2. <span data-ttu-id="65035-143">Nella finestra di conferma hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="65035-143">In hello confirmation window, click **OK**.</span></span>

   ![Finestra di conferma dell'eliminazione dell'account di archiviazione][DS02]

## <a name="next-steps"></a><span data-ttu-id="65035-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65035-145">Next steps</span></span>
<span data-ttu-id="65035-146">Per ulteriori informazioni sugli account di archiviazione di Azure, le dimensioni e sui prezzi, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="65035-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="65035-147">[Introduzione tooMicrosoft di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="65035-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="65035-148">[Informazioni sugli account di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="65035-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="65035-149">Dimensioni degli account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65035-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="65035-150">[Sizes for Windows storage accounts in Azure] (Dimensioni degli account di archiviazione Windows in Azure)</span><span class="sxs-lookup"><span data-stu-id="65035-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="65035-151">[Sizes for Linux storage accounts in Azure] (Dimensioni degli account di archiviazione Linux in Azure)</span><span class="sxs-lookup"><span data-stu-id="65035-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="65035-152">Prezzi per gli account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65035-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="65035-153">[Prezzi per gli account di archiviazione Windows]</span><span class="sxs-lookup"><span data-stu-id="65035-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="65035-154">[Prezzi per gli account di archiviazione Linux]</span><span class="sxs-lookup"><span data-stu-id="65035-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="65035-155">Per ulteriori informazioni su Azure Toolkit per IDE Java, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="65035-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="65035-156">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65035-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65035-157">[Novità di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65035-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65035-158">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65035-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65035-159">[accesso le istruzioni per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65035-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="65035-160">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="65035-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="65035-161">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65035-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65035-162">[Novità di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65035-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65035-163">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65035-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65035-164">[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65035-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="65035-165">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="65035-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="65035-166">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="65035-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[accesso le istruzioni per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/

[Introduzione tooMicrosoft di archiviazione di Azure]: /azure/storage/storage-introduction
[Informazioni sugli account di archiviazione di Azure]: /azure/storage/storage-create-storage-account
[Replica di Archiviazione di Azure]: /azure/storage/storage-redundancy
[Obiettivi di scalabilità e prestazioni per Archiviazione di Azure]: /azure/storage/storage-scalability-targets
[denominazione e riferimento a contenitori, BLOB e metadati]: http://go.microsoft.com/fwlink/?LinkId=255555

[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes (Dimensioni degli account di archiviazione Windows in Azure)
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes (Dimensioni degli account di archiviazione Linux in Azure)
[Prezzi per gli account di archiviazione Windows]: /pricing/details/virtual-machines/windows/
[Prezzi per gli account di archiviazione Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
