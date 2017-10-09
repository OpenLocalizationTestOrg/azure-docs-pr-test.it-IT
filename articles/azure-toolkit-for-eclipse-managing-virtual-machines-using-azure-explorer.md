---
title: macchine virtuali aaaManage tramite hello Azure Explorer per Eclipse | Documenti Microsoft
description: Informazioni su come toomanage macchine virtuali di Azure tramite hello Azure Explorer per Eclipse.
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="c72d0-103">Gestire le macchine virtuali tramite hello Azure Explorer per Eclipse</span><span class="sxs-lookup"><span data-stu-id="c72d0-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c72d0-104">Hello Esplora Azure, che fa parte di hello Azure Toolkit per Eclipse, fornisce agli sviluppatori Java una soluzione da usare per la gestione delle macchine virtuali nel proprio account da Azure all'interno di ambiente di sviluppo integrato (IDE) di hello Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c72d0-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c72d0-105">Creare una macchina virtuale in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c72d0-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="c72d0-106">una macchina virtuale utilizzando Esplora Azure hello toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c72d0-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="c72d0-107">Accedi tooyour account Azure tramite hello [accesso le istruzioni per hello Azure Toolkit per Eclipse].</span><span class="sxs-lookup"><span data-stu-id="c72d0-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="c72d0-108">In hello **Esplora Azure** visualizzare, espandere hello **Azure** nodo, fare doppio clic su **macchine virtuali**, quindi fare clic su **crea macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="c72d0-109">![Hello comando Crea macchina virtuale][CR01]</span><span class="sxs-lookup"><span data-stu-id="c72d0-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="c72d0-110">Hello **creare una nuova macchina virtuale** apre la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="c72d0-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c72d0-111">In hello **scegliere una sottoscrizione** finestra, selezionare la sottoscrizione e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Hello finestra scegliere una sottoscrizione][CR02]

4. <span data-ttu-id="c72d0-113">In hello **selezionare un'immagine di macchina virtuale** finestra immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c72d0-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="c72d0-114">**Località**: specifica dove verrà creata la macchina virtuale, ad esempio *Stati Uniti occidentali*.</span><span class="sxs-lookup"><span data-stu-id="c72d0-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="c72d0-115">**Server di pubblicazione**: specifica i server di pubblicazione di hello immagine hello userai toocreate la macchina virtuale è stata creata (ad esempio, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c72d0-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="c72d0-116">**Offrono**: specifica macchina virtuale hello offerta toouse dal server di pubblicazione selezionato hello (ad esempio, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c72d0-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="c72d0-117">**SKU**: hello stockkeeping prodotto (SKU) toouse dall'offerta selezionata hello specifica (ad esempio, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c72d0-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="c72d0-118">**Versione #**: specifica la versione di hello selezionato toouse SKU.</span><span class="sxs-lookup"><span data-stu-id="c72d0-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Hello selezionare una finestra dell'immagine di macchina virtuale][CR03]

5. <span data-ttu-id="c72d0-120">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-120">Click **Next**.</span></span>

6. <span data-ttu-id="c72d0-121">In hello **le impostazioni di base di macchina virtuale** finestra immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c72d0-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="c72d0-122">**Nome della macchina virtuale**: Specifica il nome di hello per la nuova macchina virtuale, che deve iniziare con una lettera e contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="c72d0-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c72d0-123">**Dimensioni**: Specifica il numero di hello di core e memoria tooallocate per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="c72d0-124">**Nome utente**: hello amministratore account toocreate per la gestione della macchina virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="c72d0-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="c72d0-125">**Password** e **conferma**: specifica hello password per l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="c72d0-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![finestra Impostazioni di base di macchina virtuale Hello][CR04]

7. <span data-ttu-id="c72d0-127">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-127">Click **Next**.</span></span>

8. <span data-ttu-id="c72d0-128">In hello **Crea nuovo Account di archiviazione** finestra immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c72d0-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="c72d0-129">**Gruppo di risorse**: Specifica il gruppo di risorse hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="c72d0-130">Selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="c72d0-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="c72d0-131">**Creare nuovi**: Specifica che si desidera toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c72d0-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c72d0-132">**Usa esistente**: Specifica che si desidera tooselect un gruppo di risorse che è già associato a un account Azure.</span><span class="sxs-lookup"><span data-stu-id="c72d0-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![finestra di dialogo Crea nuovo Account di archiviazione Hello][CR05]

   * <span data-ttu-id="c72d0-134">**Account di archiviazione**: hello storage account toouse per archiviare la macchina virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="c72d0-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="c72d0-135">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="c72d0-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="c72d0-136">**Rete virtuale** e **Subnet**: specifica la rete virtuale hello e subnet che si connetterà la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c72d0-137">È possibile usare una subnet e una rete esistente oppure creare una rete e una subnet nuove.</span><span class="sxs-lookup"><span data-stu-id="c72d0-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c72d0-138">Se si seleziona **Crea nuovo**, viene visualizzata la finestra di dialogo seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c72d0-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![finestra di dialogo Crea nuova rete virtuale Hello][CR06]

9. <span data-ttu-id="c72d0-140">In hello **risorse associata** finestra immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c72d0-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="c72d0-141">**Indirizzo IP pubblico**: specifica un indirizzo IP con connessione esterna per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c72d0-142">È possibile scegliere un nuovo indirizzo IP toocreate o, se la macchina virtuale non avrà un indirizzo IP pubblico, è possibile selezionare **(nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="c72d0-143">**Gruppo di sicurezza di rete**: specifica un firewall di rete facoltativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c72d0-144">È possibile selezionare un firewall esistente oppure, se la macchina virtuale non usa un firewall di rete, è possibile selezionare **(Nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="c72d0-145">**Set di disponibilità**: specifica un set di disponibilità facoltativo a cui può appartenere la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c72d0-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c72d0-146">È possibile selezionare un set di disponibilità esistente o creare un nuovo set di disponibilità o se la macchina virtuale non apparterrà tooan set di disponibilità, è possibile selezionare **(nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![finestra di risorse associati Hello][CR07]

9. <span data-ttu-id="c72d0-148">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-148">Click **Finish**.</span></span>  
  <span data-ttu-id="c72d0-149">La nuova macchina virtuale viene visualizzata nella finestra degli strumenti di Esplora Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c72d0-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nuova macchina virtuale][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c72d0-151">Riavvio di una macchina virtuale in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c72d0-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="c72d0-152">una macchina virtuale utilizzando hello Esplora Azure in Eclipse, toorestart hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c72d0-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c72d0-153">In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![comando di riavvio Hello macchina virtuale][RE01]

2. <span data-ttu-id="c72d0-155">Nella finestra di conferma hello, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-155">In hello confirmation window, click **Yes**.</span></span>

   ![finestra di conferma riavvio Hello][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c72d0-157">Arrestare una macchina virtuale in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c72d0-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="c72d0-158">tooshut verso il basso di una macchina virtuale in esecuzione utilizzando hello Esplora Azure in Eclipse, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c72d0-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c72d0-159">In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **arresto**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![comando di arresto di macchina virtuale Hello][SH01]

2. <span data-ttu-id="c72d0-161">Nella finestra di conferma hello, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-161">In hello confirmation window, click **Yes**.</span></span>

   ![finestra di conferma di Hello arresto di macchina virtuale][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c72d0-163">Eliminare una macchina virtuale in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c72d0-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="c72d0-164">una macchina virtuale utilizzando hello Esplora Azure in Eclipse, toodelete hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c72d0-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c72d0-165">In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![comando di eliminazione Hello macchina virtuale][DE01]

2. <span data-ttu-id="c72d0-167">Nella finestra di conferma hello, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c72d0-167">In hello confirmation window, click **Yes**.</span></span>

   ![finestra di conferma l'eliminazione di macchina virtuale Hello][DE02]

## <a name="next-steps"></a><span data-ttu-id="c72d0-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c72d0-169">Next steps</span></span>
<span data-ttu-id="c72d0-170">Per ulteriori informazioni sulle dimensioni di macchina virtuale di Azure e sui prezzi, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="c72d0-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="c72d0-171">Dimensioni delle macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="c72d0-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c72d0-172">[Dimensioni per le macchine virtuali Windows in Azure]</span><span class="sxs-lookup"><span data-stu-id="c72d0-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c72d0-173">[Dimensioni delle macchine virtuali Linux in Azure]</span><span class="sxs-lookup"><span data-stu-id="c72d0-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c72d0-174">Prezzi delle macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="c72d0-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c72d0-175">[Prezzi delle macchine virtuali in Windows]</span><span class="sxs-lookup"><span data-stu-id="c72d0-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c72d0-176">[Prezzi delle macchine virtuali in Linux]</span><span class="sxs-lookup"><span data-stu-id="c72d0-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c72d0-177">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="c72d0-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="c72d0-178">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c72d0-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c72d0-179">[Novità di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c72d0-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c72d0-180">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c72d0-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c72d0-181">[accesso le istruzioni per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c72d0-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c72d0-182">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c72d0-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c72d0-183">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c72d0-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c72d0-184">[Novità di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c72d0-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c72d0-185">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c72d0-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c72d0-186">[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c72d0-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c72d0-187">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c72d0-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c72d0-188">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c72d0-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Dimensioni per le macchine virtuali Windows in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Dimensioni delle macchine virtuali Linux in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prezzi delle macchine virtuali in Windows]: /pricing/details/virtual-machines/windows/
[Prezzi delle macchine virtuali in Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
