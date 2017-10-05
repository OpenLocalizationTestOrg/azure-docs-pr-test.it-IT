---
title: Distribuire SAP S/4 HANA o BW/4 HANA in una macchina virtuale di Azure | Microsoft Docs
description: Distribuire SAP S/4HANA o BW/4HANA in una macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="e5a94-103">Distribuire SAP S/4HANA o BW/4HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="e5a94-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="e5a94-104">Questo articolo descrive come distribuire S/4HANA in Azure tramite SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="e5a94-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="e5a94-105">Per distribuire altre soluzioni basate su SAP HANA, ad esempio BW/4HANA, seguire la stessa procedura.</span><span class="sxs-lookup"><span data-stu-id="e5a94-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="e5a94-106">Per altre informazioni su SAP CAL, visitare il sito Web [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="e5a94-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="e5a94-107">Esiste anche un blog di SAP su [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="e5a94-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="e5a94-108">A partire dal 29 maggio 2017, per distribuire SAP CAL è possibile usare il modello di distribuzione Azure Resource Manager, oltre al modello di distribuzione classica, non preferito.</span><span class="sxs-lookup"><span data-stu-id="e5a94-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="e5a94-109">È consigliabile usare il nuovo modello di distribuzione Resource Manager, ignorando il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e5a94-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="e5a94-110">Procedura dettagliata per distribuire la soluzione</span><span class="sxs-lookup"><span data-stu-id="e5a94-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="e5a94-111">La sequenza di screenshot che segue illustra come distribuire S/4HANA in Azure tramite SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="e5a94-112">Per altre soluzioni, ad esempio BW/4HANA, il processo è lo stesso.</span><span class="sxs-lookup"><span data-stu-id="e5a94-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="e5a94-113">La pagina **Solutions** (Soluzioni) illustra alcune delle soluzioni SAP CAL basate su HANA disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="e5a94-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** è nella riga centrale:</span><span class="sxs-lookup"><span data-stu-id="e5a94-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![Soluzioni SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="e5a94-116">Creare un account in SAP CAL</span><span class="sxs-lookup"><span data-stu-id="e5a94-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="e5a94-117">Per accedere a SAP CAL per la prima volta, usare un account SAP S-User o un altro account utente registrato con SAP.</span><span class="sxs-lookup"><span data-stu-id="e5a94-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="e5a94-118">Definire quindi un account SAP CAL da usare per distribuire appliance in Azure con SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="e5a94-119">Nella definizione dell'account è necessario:</span><span class="sxs-lookup"><span data-stu-id="e5a94-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="e5a94-120">a.</span><span class="sxs-lookup"><span data-stu-id="e5a94-120">a.</span></span> <span data-ttu-id="e5a94-121">Selezionare il modello di distribuzione in Azure (Resource Manager o classica).</span><span class="sxs-lookup"><span data-stu-id="e5a94-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="e5a94-122">b.</span><span class="sxs-lookup"><span data-stu-id="e5a94-122">b.</span></span> <span data-ttu-id="e5a94-123">Immettere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-123">Enter your Azure subscription.</span></span> <span data-ttu-id="e5a94-124">Un account SAP CAL può essere assegnato a una sola sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e5a94-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="e5a94-125">Se sono necessarie più sottoscrizioni, è necessario creare più account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="e5a94-126">c.</span><span class="sxs-lookup"><span data-stu-id="e5a94-126">c.</span></span> <span data-ttu-id="e5a94-127">Concedere a SAP CAL l'autorizzazione alla distribuzione all'interno della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="e5a94-128">I passaggi successivi illustrano come creare un account SAP CAL per le distribuzioni Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5a94-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="e5a94-129">Se è già disponibile un account SAP CAL collegato al modello di distribuzione classica, per creare un nuovo account SAP CAL è *necessario* seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e5a94-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="e5a94-130">Il nuovo account SAP CAL deve eseguire la distribuzione nel modello Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5a94-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="e5a94-131">Creare un nuovo account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="e5a94-132">La pagina **Accounts** (Account) presenta tre scelte per Azure:</span><span class="sxs-lookup"><span data-stu-id="e5a94-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="e5a94-133">a.</span><span class="sxs-lookup"><span data-stu-id="e5a94-133">a.</span></span> <span data-ttu-id="e5a94-134">**Microsoft Azure (classic)** (Microsoft Azure (classica)), il modello di distribuzione classica, non rappresenta più il modello di distribuzione preferito.</span><span class="sxs-lookup"><span data-stu-id="e5a94-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="e5a94-135">b.</span><span class="sxs-lookup"><span data-stu-id="e5a94-135">b.</span></span> <span data-ttu-id="e5a94-136">**Microsoft Azure** corrisponde al nuovo modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5a94-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="e5a94-137">c.</span><span class="sxs-lookup"><span data-stu-id="e5a94-137">c.</span></span> <span data-ttu-id="e5a94-138">**Windows Azure operated by 21Vianet** (Windows Azure gestito da 21Vianet) è un'opzione disponibile in Cina che usa il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e5a94-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="e5a94-139">Per distribuire il modello Resource Manager, selezionare **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e5a94-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Dettagli dell'account SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="e5a94-141">Immettere l'**ID sottoscrizione** di Azure, reperibile nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![Account SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="e5a94-143">Per autorizzare SAP CAL alla distribuzione nella sottoscrizione di Azure definita, fare clic su **Authorize** (Autorizza).</span><span class="sxs-lookup"><span data-stu-id="e5a94-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="e5a94-144">Nella scheda del browser viene visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="e5a94-144">The following page appears in the browser tab:</span></span>

   ![Accesso ai servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="e5a94-146">Se sono elencati più utenti, scegliere l'account Microsoft collegato come coamministratore della sottoscrizione di Azure selezionata.</span><span class="sxs-lookup"><span data-stu-id="e5a94-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="e5a94-147">Nella scheda del browser viene visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="e5a94-147">The following page appears in the browser tab:</span></span>

   ![Conferma dei servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="e5a94-149">Fare clic **Accept**.</span><span class="sxs-lookup"><span data-stu-id="e5a94-149">Click **Accept**.</span></span> <span data-ttu-id="e5a94-150">Se l'autorizzazione ha esito positivo, viene visualizzata nuovamente la definizione dell'account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="e5a94-151">Dopo un breve periodo, viene visualizzato un messaggio di conferma del completamento del processo di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e5a94-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="e5a94-152">Per assegnare a un utente l'account SAP CAL appena creato, immettere l'**ID utente** nella casella di testo a destra e fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="e5a94-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![Associazione tra account e utente](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="e5a94-154">Per associare l'account all'utente usato per accedere a SAP CAL, fare clic su **Review** (Verifica).</span><span class="sxs-lookup"><span data-stu-id="e5a94-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="e5a94-155">Per creare l'associazione tra l'utente e l'account SAP CAL appena creato, fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="e5a94-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![Associazione tra utente e account SAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="e5a94-157">È stato creato un account SAP CAL in grado di:</span><span class="sxs-lookup"><span data-stu-id="e5a94-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="e5a94-158">Usare il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5a94-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="e5a94-159">Distribuire i sistemi SAP nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="e5a94-160">È ora possibile iniziare a distribuire S/4HANA nella sottoscrizione utente in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="e5a94-161">Prima di continuare, determinare se sono disponibili quote core di Azure per macchine virtuali di serie H di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="e5a94-162">Attualmente, per distribuire alcune soluzioni basate su SAP HANA, SAP CAL usa macchine virtuali di serie H di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="e5a94-163">È possibile tuttavia che la sottoscrizione di Azure in uso non abbia quote core per la serie H.</span><span class="sxs-lookup"><span data-stu-id="e5a94-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="e5a94-164">In questo caso, è necessario contattare il supporto tecnico di Azure per ottenere una quota di almeno 16 serie H.</span><span class="sxs-lookup"><span data-stu-id="e5a94-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="e5a94-165">Quando si distribuisce una soluzione in Azure con SAP CAL, può accadere che sia possibile scegliere una sola area di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="e5a94-166">Per eseguire la distribuzione in aree di Azure diverse da quella suggerita da SAP CAL, è necessario acquistare una sottoscrizione CAL da SAP.</span><span class="sxs-lookup"><span data-stu-id="e5a94-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="e5a94-167">Potrebbe anche essere necessario aprire un messaggio con SAP per farsi abilitare l'account CAL per il recapito in aree di Azure diverse da quelle suggerite inizialmente.</span><span class="sxs-lookup"><span data-stu-id="e5a94-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="e5a94-168">Distribuire una soluzione</span><span class="sxs-lookup"><span data-stu-id="e5a94-168">Deploy a solution</span></span>

<span data-ttu-id="e5a94-169">Verrà ora distribuita una soluzione dalla pagina **Solutions** (Soluzioni) di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="e5a94-170">Con SAP CAL sono disponibili due sequenze di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="e5a94-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="e5a94-171">Una sequenza di base, che usa una sola pagina per definire il sistema da distribuire</span><span class="sxs-lookup"><span data-stu-id="e5a94-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="e5a94-172">Una sequenza avanzata, che offre opzioni specifiche per le dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e5a94-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="e5a94-173">In questo articolo verrà illustrato il percorso di distribuzione di base.</span><span class="sxs-lookup"><span data-stu-id="e5a94-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="e5a94-174">Nella pagina **Account Details** (Dettagli account) è necessario:</span><span class="sxs-lookup"><span data-stu-id="e5a94-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="e5a94-175">a.</span><span class="sxs-lookup"><span data-stu-id="e5a94-175">a.</span></span> <span data-ttu-id="e5a94-176">Selezionare un account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-176">Select an SAP CAL account.</span></span> <span data-ttu-id="e5a94-177">Usare un account associato alla distribuzione con il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5a94-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="e5a94-178">b.</span><span class="sxs-lookup"><span data-stu-id="e5a94-178">b.</span></span> <span data-ttu-id="e5a94-179">Immettere un **nome** di istanza.</span><span class="sxs-lookup"><span data-stu-id="e5a94-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="e5a94-180">c.</span><span class="sxs-lookup"><span data-stu-id="e5a94-180">c.</span></span> <span data-ttu-id="e5a94-181">Selezionare un'**area** di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-181">Select an Azure **Region**.</span></span> <span data-ttu-id="e5a94-182">SAP CAL suggerisce un'area.</span><span class="sxs-lookup"><span data-stu-id="e5a94-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="e5a94-183">Se è necessaria un'altra area di Azure e non si ha una sottoscrizione SAP CAL, è necessario ordinare una sottoscrizione CAL a SAP.</span><span class="sxs-lookup"><span data-stu-id="e5a94-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="e5a94-184">d.</span><span class="sxs-lookup"><span data-stu-id="e5a94-184">d.</span></span> <span data-ttu-id="e5a94-185">Immettere una **password** master di otto o nove caratteri per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="e5a94-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="e5a94-186">La password viene usata per gli amministratori dei diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="e5a94-186">The password is used for the administrators of the different components.</span></span>

   ![Modalità SAP CAL di base: creare un'istanza](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="e5a94-188">Fare clic su **Create** (Crea). Nella finestra di messaggio visualizzata fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5a94-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![Dimensioni delle macchine virtuali supportate da SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="e5a94-190">Nella finestra di dialogo **Private Key** (Chiave privata) fare clic su **Store** (Archivia) per archiviare la chiave privata in SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="e5a94-191">Per usare la password di protezione per la chiave privata, fare clic su **Download** (Scarica).</span><span class="sxs-lookup"><span data-stu-id="e5a94-191">To use password protection for the private key, click **Download**.</span></span> 

   ![Chiave privata SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="e5a94-193">Leggere il messaggio in **Warning** (Avviso) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5a94-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Avviso di SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="e5a94-195">Verrà ora eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e5a94-195">Now the deployment takes place.</span></span> <span data-ttu-id="e5a94-196">Dopo alcuni minuti, a seconda della dimensione e della complessità della soluzione, di cui SAP CAL fornisce una stima, la soluzione viene visualizzata come attiva e pronta all'uso.</span><span class="sxs-lookup"><span data-stu-id="e5a94-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="e5a94-197">Per individuare le macchine virtuali raccolte con le altre risorse associate in un unico gruppo di risorse, passare al Portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e5a94-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![Oggetti SAP CAL distribuiti nel nuovo portale](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="e5a94-199">Nel portale SAP CAL lo stato è visualizzato come **Active** (Attivo).</span><span class="sxs-lookup"><span data-stu-id="e5a94-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="e5a94-200">Per connettersi alla soluzione, fare clic su **Connect** (Connetti).</span><span class="sxs-lookup"><span data-stu-id="e5a94-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="e5a94-201">All'interno di questa soluzione sono distribuite opzioni diverse per la connessione a componenti diversi.</span><span class="sxs-lookup"><span data-stu-id="e5a94-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![Istanze di SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="e5a94-203">Prima che sia possibile usare una delle opzioni per la connessione ai sistemi distribuiti, è necessario fare clic su **Getting Started Guide** (Guida introduttiva).</span><span class="sxs-lookup"><span data-stu-id="e5a94-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![Finestra Connect to the Instance (Connettersi all'istanza)](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="e5a94-205">La documentazione cita gli utenti per ognuno dei metodi di connettività.</span><span class="sxs-lookup"><span data-stu-id="e5a94-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="e5a94-206">Le password per questi utenti corrispondono alla password master definita all'inizio del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e5a94-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="e5a94-207">Nella documentazione sono elencati altri utenti funzionali con le relative password. È possibile usare questi utenti per accedere al sistema distribuito.</span><span class="sxs-lookup"><span data-stu-id="e5a94-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="e5a94-208">Se ad esempio si usa la GUI SAP preinstallata nel computer Desktop remoto Windows, il sistema S/4 può avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e5a94-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![SM50 nella GUI SAP preinstallata](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="e5a94-210">Se invece si usa DBA Cockpit, l'istanza può avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e5a94-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![SM50 nella GUI SAP DBA Cockpit](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="e5a94-212">In poche ore un'appliance SAP S/4 integra verrà distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a94-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="e5a94-213">Se è stata acquistata una sottoscrizione SAP CAL, SAP offre il supporto completo alle distribuzioni in Azure tramite SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="e5a94-214">La coda di supporto è BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="e5a94-214">The support queue is BC-VCM-CAL.</span></span>







