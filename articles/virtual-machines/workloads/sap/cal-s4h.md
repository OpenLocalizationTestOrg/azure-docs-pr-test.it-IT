---
title: aaaDeploy S/4HANA SAP o BW/4HANA in una macchina virtuale di Azure | Documenti Microsoft
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
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="78ba5-103">Distribuire SAP S/4HANA o BW/4HANA in Azure</span><span class="sxs-lookup"><span data-stu-id="78ba5-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="78ba5-104">In questo articolo viene descritto come toodeploy S/4HANA in Azure utilizzando hello libreria Appliance di Cloud SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="78ba5-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="78ba5-105">toodeploy altre soluzioni basate su SAP HANA, ad esempio BW/4HANA, seguono hello stessi passaggi.</span><span class="sxs-lookup"><span data-stu-id="78ba5-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="78ba5-106">Per ulteriori informazioni su hello CAL SAP, visitare toohello [SAP Cloud accessorio libreria](https://cal.sap.com/) sito Web.</span><span class="sxs-lookup"><span data-stu-id="78ba5-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="78ba5-107">SAP include anche un blog sui hello [SAP Cloud accessorio libreria 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="78ba5-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="78ba5-108">Come di 29 maggio 2017, è possibile utilizzare modelli di distribuzione Azure Resource Manager hello inoltre distribuzione classica preferito meno toohello modello toodeploy hello CAL SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="78ba5-109">È consigliabile utilizzare il nuovo modello di distribuzione di gestione delle risorse di hello e ignorare il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="78ba5-110">Soluzione di hello toodeploy passaggi della procedura guidata</span><span class="sxs-lookup"><span data-stu-id="78ba5-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="78ba5-111">Hello sequenza degli screenshot seguente mostra come toodeploy S/4HANA in Azure utilizzando hello CAL SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="78ba5-112">il processo di Hello funziona hello allo stesso modo di altre soluzioni, ad esempio BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="78ba5-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="78ba5-113">Hello **soluzioni** pagina vengono illustrati alcuni dei hello soluzioni basate su SAP HANA CAL disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="78ba5-114">**SAP S/4HANA 1610 FPS01, Fully-Activated accessorio** nella riga centrale hello:</span><span class="sxs-lookup"><span data-stu-id="78ba5-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Soluzioni SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="78ba5-116">Creare un account in hello CAL SAP</span><span class="sxs-lookup"><span data-stu-id="78ba5-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="78ba5-117">toosign in toohello CAL SAP per hello prima volta, utilizzare S utente SAP o altre registrate con SAP dall'utente.</span><span class="sxs-lookup"><span data-stu-id="78ba5-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="78ba5-118">Definire quindi un account di SAP CAL utilizzato da dispositivi di toodeploy hello CAL SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="78ba5-119">Nella definizione di account hello, è necessario:</span><span class="sxs-lookup"><span data-stu-id="78ba5-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="78ba5-120">a.</span><span class="sxs-lookup"><span data-stu-id="78ba5-120">a.</span></span> <span data-ttu-id="78ba5-121">Selezionare il modello di distribuzione hello in Azure (classica o gestione delle risorse).</span><span class="sxs-lookup"><span data-stu-id="78ba5-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="78ba5-122">b.</span><span class="sxs-lookup"><span data-stu-id="78ba5-122">b.</span></span> <span data-ttu-id="78ba5-123">Immettere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-123">Enter your Azure subscription.</span></span> <span data-ttu-id="78ba5-124">Un account di SAP CAL può essere assegnato solo sottoscrizione tooone.</span><span class="sxs-lookup"><span data-stu-id="78ba5-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="78ba5-125">Se è necessario più di una sottoscrizione, è necessario toocreate un altro account di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="78ba5-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="78ba5-126">c.</span><span class="sxs-lookup"><span data-stu-id="78ba5-126">c.</span></span> <span data-ttu-id="78ba5-127">Assegnare hello SAP CAL autorizzazione toodeploy alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="78ba5-128">passaggi successivi Hello mostrano come toocreate una licenza CAL SAP account per le distribuzioni di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="78ba5-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="78ba5-129">Se hai già un account di SAP CAL che è il modello di distribuzione classica toohello collegato, si *necessario* toofollow questi toocreate passaggi un nuovo account di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="78ba5-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="78ba5-130">il nuovo account di SAP CAL Hello deve toodeploy nel modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="78ba5-131">Creare un nuovo account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="78ba5-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="78ba5-132">Hello **account** pagina sono disponibili tre opzioni Azure:</span><span class="sxs-lookup"><span data-stu-id="78ba5-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="78ba5-133">a.</span><span class="sxs-lookup"><span data-stu-id="78ba5-133">a.</span></span> <span data-ttu-id="78ba5-134">**Microsoft Azure (versione classica)** è il modello di distribuzione classica hello e non è più preferito.</span><span class="sxs-lookup"><span data-stu-id="78ba5-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="78ba5-135">b.</span><span class="sxs-lookup"><span data-stu-id="78ba5-135">b.</span></span> <span data-ttu-id="78ba5-136">**Microsoft Azure** è il nuovo modello di distribuzione di gestione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="78ba5-137">c.</span><span class="sxs-lookup"><span data-stu-id="78ba5-137">c.</span></span> <span data-ttu-id="78ba5-138">**Windows Azure gestito da 21Vianet** è un'opzione in Cina che utilizza il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="78ba5-139">Selezionare toodeploy nel modello di gestione risorse di hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Dettagli dell'account SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="78ba5-141">Immettere hello Azure **ID sottoscrizione** che sono disponibili nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Account SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="78ba5-143">tooauthorize hello CAL SAP toodeploy nella sottoscrizione di Azure hello è definito, fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="78ba5-144">Hello seguente pagina viene visualizzata nella scheda del browser hello:</span><span class="sxs-lookup"><span data-stu-id="78ba5-144">hello following page appears in hello browser tab:</span></span>

   ![Accesso ai servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="78ba5-146">Se più di un utente è elencato, scegliere hello account Microsoft collegato toobe hello coadministrator di hello Azure sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="78ba5-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="78ba5-147">Hello seguente pagina viene visualizzata nella scheda del browser hello:</span><span class="sxs-lookup"><span data-stu-id="78ba5-147">hello following page appears in hello browser tab:</span></span>

   ![Conferma dei servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="78ba5-149">Fare clic **Accept**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-149">Click **Accept**.</span></span> <span data-ttu-id="78ba5-150">Se viene concessa l'autorizzazione di hello, definizione di account di SAP CAL viene visualizzato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="78ba5-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="78ba5-151">Dopo un breve periodo di tempo, un messaggio di conferma che il processo di autorizzazione hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="78ba5-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="78ba5-152">hello tooassign appena creati SAP CAL account tooyour utente, immettere il **ID utente** nella casella di testo a destra hello hello e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Associazione toouser account](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="78ba5-154">Fare clic su account utente di hello utilizzare toosign toohello CAL SAP, tooassociate **revisione**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="78ba5-155">associazione di hello toocreate tra l'utente e l'account di SAP CAL hello appena creato, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Associazione dell'account utente tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="78ba5-157">È stato creato un account SAP CAL in grado di:</span><span class="sxs-lookup"><span data-stu-id="78ba5-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="78ba5-158">Utilizzare il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="78ba5-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="78ba5-159">Distribuire i sistemi SAP nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="78ba5-160">È ora possibile avviare toodeploy S/4HANA alla sottoscrizione di utente in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="78ba5-161">Prima di continuare, determinare se sono disponibili quote core di Azure per macchine virtuali di serie H di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="78ba5-162">In un momento hello, hello SAP CAL utilizza toodeploy H serie macchine virtuali di Azure alcune delle soluzioni basate su SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="78ba5-163">È possibile tuttavia che la sottoscrizione di Azure in uso non abbia quote core per la serie H.</span><span class="sxs-lookup"><span data-stu-id="78ba5-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="78ba5-164">In questo caso, potrebbe essere necessario toocontact supporto tecnico di Azure tooget una quota di almeno 16 core H serie.</span><span class="sxs-lookup"><span data-stu-id="78ba5-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="78ba5-165">Quando si distribuisce una soluzione hello CAL SAP in Azure, si noterà che è possibile scegliere una sola area di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="78ba5-166">toodeploy in aree di Azure diverso da hello uno suggeriti da hello CAL SAP, è necessario toopurchase una sottoscrizione CAL da SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="78ba5-167">Inoltre potrebbe essere necessario un messaggio con SAP toohave tooopen il toodeliver account abilitato CAL in aree di Azure diverso da quelli suggeriti inizialmente hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="78ba5-168">Distribuire una soluzione</span><span class="sxs-lookup"><span data-stu-id="78ba5-168">Deploy a solution</span></span>

<span data-ttu-id="78ba5-169">Consente di distribuire una soluzione da hello **soluzioni** pagina di hello CAL SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="78ba5-170">Hello CAL SAP dispone di due sequenze toodeploy:</span><span class="sxs-lookup"><span data-stu-id="78ba5-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="78ba5-171">Una sequenza di base che usa uno toobe di sistema di hello toodefine, pagina distribuito</span><span class="sxs-lookup"><span data-stu-id="78ba5-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="78ba5-172">Una sequenza avanzata, che offre opzioni specifiche per le dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="78ba5-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="78ba5-173">Viene descritto come hello qui toodeployment di percorso di base.</span><span class="sxs-lookup"><span data-stu-id="78ba5-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="78ba5-174">In hello **dettagli Account** pagina, è necessario:</span><span class="sxs-lookup"><span data-stu-id="78ba5-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="78ba5-175">a.</span><span class="sxs-lookup"><span data-stu-id="78ba5-175">a.</span></span> <span data-ttu-id="78ba5-176">Selezionare un account SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="78ba5-176">Select an SAP CAL account.</span></span> <span data-ttu-id="78ba5-177">(Utilizzare un account che sia associato toodeploy con modello di distribuzione di gestione risorse di hello).</span><span class="sxs-lookup"><span data-stu-id="78ba5-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="78ba5-178">b.</span><span class="sxs-lookup"><span data-stu-id="78ba5-178">b.</span></span> <span data-ttu-id="78ba5-179">Immettere un **nome** di istanza.</span><span class="sxs-lookup"><span data-stu-id="78ba5-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="78ba5-180">c.</span><span class="sxs-lookup"><span data-stu-id="78ba5-180">c.</span></span> <span data-ttu-id="78ba5-181">Selezionare un'**area** di Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-181">Select an Azure **Region**.</span></span> <span data-ttu-id="78ba5-182">Hello SAP CAL suggerisce una regione.</span><span class="sxs-lookup"><span data-stu-id="78ba5-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="78ba5-183">Se occorre un'altra area di Azure e non si dispone di una sottoscrizione CAL SAP, è necessario tooorder una licenza CAL sottoscrizione con SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="78ba5-184">d.</span><span class="sxs-lookup"><span data-stu-id="78ba5-184">d.</span></span> <span data-ttu-id="78ba5-185">Immettere un master **Password** per soluzione hello di otto o nove caratteri.</span><span class="sxs-lookup"><span data-stu-id="78ba5-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="78ba5-186">Hello password viene utilizzata per gli amministratori di hello dei diversi componenti hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Modalità SAP CAL di base: creare un'istanza](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="78ba5-188">Fare clic su **crea**, nella finestra di messaggio hello che viene visualizzato, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![Dimensioni delle macchine virtuali supportate da SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="78ba5-190">In hello **chiave privata** la finestra di dialogo, fare clic su **archivio** toostore hello chiave privata hello CAL SAP.</span><span class="sxs-lookup"><span data-stu-id="78ba5-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="78ba5-191">Fare clic su toouse password di protezione per la chiave privata di hello **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Chiave privata SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="78ba5-193">Hello lettura CAL SAP **avviso** messaggio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Avviso di SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="78ba5-195">Distribuzione di hello viene ora eseguita.</span><span class="sxs-lookup"><span data-stu-id="78ba5-195">Now hello deployment takes place.</span></span> <span data-ttu-id="78ba5-196">Dopo alcuni minuti, a seconda delle dimensioni di hello e la complessità della soluzione hello (Buongiorno CAL SAP fornisce una stima), lo stato di hello è visualizzato come attivo e pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="78ba5-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="78ba5-197">macchine virtuali di hello toofind raccolte con hello altre risorse associate in un gruppo di risorse, visitare il portale di Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="78ba5-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Oggetti CAL SAP distribuiti nel nuovo portale di hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="78ba5-199">Nel portale di SAP CAL hello, viene visualizzato lo stato di hello come **Active**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="78ba5-200">soluzione toohello tooconnect, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="78ba5-201">Diverse opzioni tooconnect toohello diversi componenti vengono distribuiti all'interno di questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="78ba5-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Istanze di SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="78ba5-203">Prima di poter utilizzare uno dei sistemi distribuito toohello tooconnect di hello opzioni, fare clic su **Guida introduttiva**.</span><span class="sxs-lookup"><span data-stu-id="78ba5-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Connettersi toohello istanza](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="78ba5-205">i nomi di documentazione Hello hello utenti per ciascuno dei metodi di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="78ba5-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="78ba5-206">le password Hello per gli utenti vengono impostate toohello password master che è definito all'inizio di hello hello processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="78ba5-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="78ba5-207">Nella documentazione di hello, sono elencati altri utenti più funzionalità e le relative password, che è possibile utilizzare toosign in toohello distribuita del sistema.</span><span class="sxs-lookup"><span data-stu-id="78ba5-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="78ba5-208">Ad esempio, se si utilizza hello SAPGUI sia preinstallato nel computer Desktop remoto di Windows hello, hello sistema S/4 potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="78ba5-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 in hello preinstallato SAPGUI](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="78ba5-210">O se si utilizza hello DBACockpit, istanza hello potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="78ba5-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 in hello DBACockpit SAPGUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="78ba5-212">In poche ore un'appliance SAP S/4 integra verrà distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="78ba5-213">Se è stata acquistata una sottoscrizione CAL SAP, SAP supporta distribuzioni tramite hello CAL SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ba5-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="78ba5-214">coda di supporto Hello è BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="78ba5-214">hello support queue is BC-VCM-CAL.</span></span>







