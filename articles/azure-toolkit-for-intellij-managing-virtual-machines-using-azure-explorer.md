---
title: Gestire le macchine virtuali con Azure Explorer per IntelliJ | Microsoft Docs
description: Informazioni su come gestire macchine virtuali di Azure con Azure Explorer per IntelliJ.
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="81541-103">Gestire macchine virtuali con Azure Explorer per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="81541-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="81541-104">Azure Explorer, che fa parte di Azure Toolkit for IntelliJ, offre agli sviluppatori Java una soluzione di facile uso per la gestione delle macchine virtuali con il proprio account Azure nell'ambiente di sviluppo integrato (IDE) di IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="81541-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="81541-105">Creare una macchina virtuale in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="81541-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="81541-106">Per creare una macchina virtuale con Azure Explorer, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="81541-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="81541-107">Accedere al proprio account Azure tramite la procedura descritta nell'articolo [Istruzioni di accesso per Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="81541-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="81541-108">Nella visualizzazione **Azure Explorer** espandere il nodo **Azure**, fare clic con il pulsante destro del mouse su **Macchine virtuali** e quindi fare clic su **Crea macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="81541-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="81541-109">![Comando Crea macchina virtuale][CR01]</span><span class="sxs-lookup"><span data-stu-id="81541-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="81541-110">Viene visualizzata la procedura guidata **Creare una nuova macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="81541-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="81541-111">Nella finestra **Scegliere una sottoscrizione** selezionare la sottoscrizione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="81541-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Finestra di dialogo Scegliere una sottoscrizione][CR02]

4. <span data-ttu-id="81541-113">Nella finestra **Selezionare un'immagine di macchina virtuale** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="81541-114">**Località**: specifica dove verrà creata la macchina virtuale, ad esempio *Stati Uniti occidentali*.</span><span class="sxs-lookup"><span data-stu-id="81541-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="81541-115">**Recommended Image** (Immagine consigliata): specifica che si sceglie un'immagine da un elenco abbreviato di immagini di uso comune.</span><span class="sxs-lookup"><span data-stu-id="81541-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="81541-116">**Immagine personalizzata**: specifica che si sceglie un'immagine personalizzata, fornendo le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="81541-117">**Autore**: specifica l'autore che ha creato l'immagine che verrà usata per creare la macchina virtuale, ad esempio *Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="81541-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="81541-118">**Offerta**: specifica la macchina virtuale offerta da usare dall'autore selezionato, ad esempio *JDK*.</span><span class="sxs-lookup"><span data-stu-id="81541-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="81541-119">**SKU**: specifica la SKU da usare nell'offerta selezionata, ad esempio *JDK_8*.</span><span class="sxs-lookup"><span data-stu-id="81541-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="81541-120">**Versione #**(N. versione): specifica la versione della SKU selezionata.</span><span class="sxs-lookup"><span data-stu-id="81541-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Finestra Selezionare un'immagine di macchina virtuale][CR03]

5. <span data-ttu-id="81541-122">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="81541-122">Click **Next**.</span></span> 

6. <span data-ttu-id="81541-123">Nella finestra **Impostazioni di base della macchina virtuale** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="81541-124">**Nome macchina virtuale**: specifica il nome della nuova macchina virtuale, che deve iniziare con una lettera e contenere solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="81541-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="81541-125">**Dimensioni**: specifica il numero di core e la quantità di memoria da allocare per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="81541-126">**Nome utente**: specifica l'account amministratore da creare per la gestione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="81541-127">**Password** e **Conferma**: specifica la password per l'account di amministratore.</span><span class="sxs-lookup"><span data-stu-id="81541-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Finestra Impostazioni di base della macchina virtuale][CR04]

7. <span data-ttu-id="81541-129">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="81541-129">Click **Next**.</span></span> 

8. <span data-ttu-id="81541-130">Nella finestra **Risorse associate** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="81541-131">**Gruppo di risorse**: specifica il gruppo di risorse per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="81541-132">Selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-132">Select one of the following options:</span></span>
      * <span data-ttu-id="81541-133">**Crea nuovo**: specifica che si intende creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="81541-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="81541-134">**Usa esistente**: specifica che si vuole scegliere in un elenco i gruppi di risorse associati all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="81541-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Finestra Risorse associate][CR07]

   * <span data-ttu-id="81541-136">**Account di archiviazione**: specifica l'account di archiviazione da usare per archiviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="81541-137">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="81541-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="81541-138">Se si sceglie **Crea nuovo**, verrà visualizzata la finestra di dialogo seguente:</span><span class="sxs-lookup"><span data-stu-id="81541-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Finestra di dialogo Crea account di archiviazione][CR05]

   * <span data-ttu-id="81541-140">**Rete virtuale** e **Subnet**: specifica la rete virtuale e la subnet a cui si connetterà la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="81541-141">È possibile usare una subnet e una rete esistente oppure creare una rete e una subnet nuove.</span><span class="sxs-lookup"><span data-stu-id="81541-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="81541-142">Se si seleziona **Crea nuovo**, verrà visualizzata la finestra di dialogo seguente:</span><span class="sxs-lookup"><span data-stu-id="81541-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Finestra di dialogo Crea rete virtuale][CR06]

   * <span data-ttu-id="81541-144">**Indirizzo IP pubblico**: specifica un indirizzo IP con connessione esterna per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="81541-145">È possibile scegliere di creare un nuovo indirizzo IP o, se la macchina virtuale non avrà un indirizzo IP pubblico, è possibile selezionare **(Nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="81541-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="81541-146">**Gruppo di sicurezza di rete**: specifica un firewall di rete facoltativo per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="81541-147">È possibile selezionare un firewall esistente oppure, se la macchina virtuale non usa un firewall di rete, è possibile selezionare **(Nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="81541-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="81541-148">**Set di disponibilità**: specifica un set di disponibilità facoltativo a cui può appartenere la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81541-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="81541-149">È possibile selezionare un set di disponibilità esistente, creare un nuovo set di disponibilità o, se la macchina virtuale non apparterrà a un set di disponibilità, selezionare **(Nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="81541-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="81541-150">Fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="81541-150">Click **Finish**.</span></span>  
    <span data-ttu-id="81541-151">La nuova macchina virtuale viene visualizzata nella finestra dello strumento Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="81541-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nuova macchina virtuale nella visualizzazione Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="81541-153">Riavviare una macchina virtuale in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="81541-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="81541-154">Per riavviare una macchina virtuale con Azure Explorer in IntelliJ, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="81541-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="81541-155">Nella visualizzazione **Azure Explorer** fare clic con il pulsante destro del mouse sulla macchina virtuale e quindi selezionare **Riavvia**.</span><span class="sxs-lookup"><span data-stu-id="81541-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Comando di riavvio della macchina virtuale][RE01]

2. <span data-ttu-id="81541-157">Nella finestra di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="81541-157">In the confirmation window, click **Yes**.</span></span> 

   ![Finestra di conferma del riavvio della macchina virtuale][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="81541-159">Arrestare una macchina virtuale in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="81541-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="81541-160">Per arrestare una macchina virtuale in esecuzione con Azure Explorer in IntelliJ, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="81541-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="81541-161">Nella visualizzazione **Azure Explorer** fare clic con il pulsante destro del mouse sulla macchina virtuale e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="81541-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Comando di arresto della macchina virtuale][SH01]

2. <span data-ttu-id="81541-163">Nella finestra di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="81541-163">In the confirmation window, click **Yes**.</span></span> 

   ![Finestra di conferma dell'arresto della macchina virtuale][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="81541-165">Eliminare una macchina virtuale in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="81541-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="81541-166">Per eliminare una macchina virtuale con Azure Explorer in IntelliJ, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="81541-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="81541-167">Nella visualizzazione **Azure Explorer** fare clic con il pulsante destro del mouse sulla macchina virtuale e quindi selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="81541-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Comando di eliminazione della macchina virtuale][DE01]

2. <span data-ttu-id="81541-169">Nella finestra di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="81541-169">In the confirmation window, click **Yes**.</span></span> 

   ![Finestra di conferma dell'eliminazione della macchina virtuale][DE02]

## <a name="next-steps"></a><span data-ttu-id="81541-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81541-171">Next steps</span></span>
<span data-ttu-id="81541-172">Per altre informazioni sulle dimensioni e sui prezzi delle macchine virtuali in Azure, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="81541-173">Dimensioni delle macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="81541-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="81541-174">[Dimensioni per le macchine virtuali Windows in Azure]</span><span class="sxs-lookup"><span data-stu-id="81541-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="81541-175">[Dimensioni delle macchine virtuali Linux in Azure]</span><span class="sxs-lookup"><span data-stu-id="81541-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="81541-176">Prezzi delle macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="81541-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="81541-177">[Prezzi delle macchine virtuali in Windows]</span><span class="sxs-lookup"><span data-stu-id="81541-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="81541-178">[Prezzi delle macchine virtuali in Linux]</span><span class="sxs-lookup"><span data-stu-id="81541-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="81541-179">Per altre informazioni sui Toolkit di Azure per gli IDE di Java, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="81541-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="81541-180">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="81541-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="81541-181">[Novità di Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="81541-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="81541-182">[Installare il Toolkit di Azure per Eclipse.]</span><span class="sxs-lookup"><span data-stu-id="81541-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="81541-183">[Istruzioni di accesso per Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="81541-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="81541-184">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="81541-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="81541-185">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="81541-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="81541-186">[Novità di Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="81541-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="81541-187">[Installazione del Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="81541-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="81541-188">[Istruzioni di accesso per Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="81541-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="81541-189">[Creare un'app Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="81541-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="81541-190">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="81541-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="81541-191">[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="81541-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="81541-192">[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="81541-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="81541-193">[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="81541-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="81541-194">[Creare un'app Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="81541-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="81541-195">[Installare il Toolkit di Azure per Eclipse.]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="81541-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="81541-196">[Installazione del Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="81541-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="81541-197">[Istruzioni di accesso per Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="81541-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="81541-198">[Istruzioni di accesso per Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="81541-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="81541-199">[Novità di Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="81541-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="81541-200">[Novità di Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="81541-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="81541-201">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="81541-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="81541-202">[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="81541-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="81541-203">[Dimensioni per le macchine virtuali Windows in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="81541-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="81541-204">[Dimensioni delle macchine virtuali Linux in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="81541-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="81541-205">[Prezzi delle macchine virtuali in Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="81541-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="81541-206">[Prezzi delle macchine virtuali in Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="81541-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
