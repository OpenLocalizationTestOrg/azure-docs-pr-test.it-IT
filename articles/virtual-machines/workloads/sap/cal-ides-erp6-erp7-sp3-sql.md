---
title: aaaDeploy SAP IDE EHP7 SP3 per 6.0 ERP SAP in Azure | Documenti Microsoft
description: Distribuire SAP IDES EHP7 SP3 per SAP ERP 6.0 in Azure
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="b1a96-103">Distribuire SAP IDES EHP7 SP3 per SAP ERP 6.0 in Azure</span><span class="sxs-lookup"><span data-stu-id="b1a96-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="b1a96-104">Questo articolo viene descritto come toodeploy un SAP sistema IDE in esecuzione con SQL Server e del sistema operativo di Windows hello in Azure tramite hello libreria Appliance di Cloud SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="b1a96-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="b1a96-105">schermate di Hello illustrati hello dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b1a96-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="b1a96-106">toodeploy una soluzione diversa, attenersi alla stessa procedura hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="b1a96-107">toostart con hello CAL SAP, andare toohello [SAP Cloud accessorio libreria](https://cal.sap.com/) sito Web.</span><span class="sxs-lookup"><span data-stu-id="b1a96-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="b1a96-108">SAP anche dispone di un blog sui hello new [SAP Cloud accessorio libreria 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="b1a96-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="b1a96-109">Come di 29 maggio 2017, è possibile utilizzare modelli di distribuzione Azure Resource Manager hello inoltre distribuzione classica preferito meno toohello modello toodeploy hello CAL SAP.</span><span class="sxs-lookup"><span data-stu-id="b1a96-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="b1a96-110">È consigliabile utilizzare il nuovo modello di distribuzione di gestione delle risorse di hello e ignorare il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="b1a96-111">Se è già stato creato un account di SAP CAL che Usa modello classico hello, *toocreate è necessario un altro account di SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="b1a96-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="b1a96-112">Questo account deve tooexclusively distribuire in Azure utilizzando il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="b1a96-113">Dopo l'accesso toohello CAL SAP, prima pagina hello in genere ti toohello **soluzioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="b1a96-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="b1a96-114">soluzioni Hello offerte su hello CAL SAP sono costantemente, pertanto potrebbe essere tooscroll abbastanza soluzione hello toofind desiderata.</span><span class="sxs-lookup"><span data-stu-id="b1a96-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="b1a96-115">soluzioni basate su Windows IDE SAP Hello evidenziato che sono disponibile esclusivamente in Azure viene illustrato il processo di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="b1a96-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Soluzioni SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="b1a96-117">Creare un account in hello CAL SAP</span><span class="sxs-lookup"><span data-stu-id="b1a96-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="b1a96-118">toosign in toohello CAL SAP per hello prima volta, utilizzare S utente SAP o altre registrate con SAP dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b1a96-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="b1a96-119">Definire quindi un account di SAP CAL utilizzato da dispositivi di toodeploy hello CAL SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="b1a96-120">Nella definizione di account hello, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b1a96-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="b1a96-121">a.</span><span class="sxs-lookup"><span data-stu-id="b1a96-121">a.</span></span> <span data-ttu-id="b1a96-122">Selezionare il modello di distribuzione hello in Azure (classica o gestione delle risorse).</span><span class="sxs-lookup"><span data-stu-id="b1a96-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="b1a96-123">b.</span><span class="sxs-lookup"><span data-stu-id="b1a96-123">b.</span></span> <span data-ttu-id="b1a96-124">Immettere la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-124">Enter your Azure subscription.</span></span> <span data-ttu-id="b1a96-125">Un account di SAP CAL può essere assegnato solo sottoscrizione tooone.</span><span class="sxs-lookup"><span data-stu-id="b1a96-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="b1a96-126">Se è necessario più di una sottoscrizione, è necessario toocreate un altro account di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="b1a96-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="b1a96-127">c.</span><span class="sxs-lookup"><span data-stu-id="b1a96-127">c.</span></span> <span data-ttu-id="b1a96-128">Assegnare hello SAP CAL autorizzazione toodeploy alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="b1a96-129">passaggi successivi Hello mostrano come toocreate una licenza CAL SAP account per le distribuzioni di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b1a96-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="b1a96-130">Se hai già un account di SAP CAL che è il modello di distribuzione classica toohello collegato, si *necessario* toofollow questi toocreate passaggi un nuovo account di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="b1a96-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="b1a96-131">il nuovo account di SAP CAL Hello deve toodeploy nel modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="b1a96-132">una nuova licenza CAL di SAP toocreate account hello **account** pagina vengono visualizzate due opzioni per Azure:</span><span class="sxs-lookup"><span data-stu-id="b1a96-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="b1a96-133">a.</span><span class="sxs-lookup"><span data-stu-id="b1a96-133">a.</span></span> <span data-ttu-id="b1a96-134">**Microsoft Azure (versione classica)** è il modello di distribuzione classica hello e non è più preferito.</span><span class="sxs-lookup"><span data-stu-id="b1a96-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="b1a96-135">b.</span><span class="sxs-lookup"><span data-stu-id="b1a96-135">b.</span></span> <span data-ttu-id="b1a96-136">**Microsoft Azure** è il nuovo modello di distribuzione di gestione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Account SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="b1a96-138">Selezionare toodeploy nel modello di gestione risorse di hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Account SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="b1a96-140">Immettere hello Azure **ID sottoscrizione** che sono disponibili nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![ID sottoscrizione di SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="b1a96-142">tooauthorize hello CAL SAP toodeploy nella sottoscrizione di Azure hello è definito, fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="b1a96-143">Hello seguente pagina viene visualizzata nella scheda del browser hello:</span><span class="sxs-lookup"><span data-stu-id="b1a96-143">hello following page appears in hello browser tab:</span></span>

    ![Accesso ai servizi cloud di Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="b1a96-145">Se più di un utente è elencato, scegliere hello account Microsoft collegato toobe hello coadministrator di hello Azure sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="b1a96-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="b1a96-146">Hello seguente pagina viene visualizzata nella scheda del browser hello:</span><span class="sxs-lookup"><span data-stu-id="b1a96-146">hello following page appears in hello browser tab:</span></span>

    ![Conferma dei servizi cloud di Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="b1a96-148">Fare clic **Accept**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-148">Click **Accept**.</span></span> <span data-ttu-id="b1a96-149">Se viene concessa l'autorizzazione di hello, definizione di account di SAP CAL viene visualizzato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b1a96-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="b1a96-150">Dopo un breve periodo di tempo, un messaggio di conferma che il processo di autorizzazione hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="b1a96-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="b1a96-151">hello tooassign appena creati SAP CAL account tooyour utente, immettere il **ID utente** nella casella di testo a destra hello hello e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Associazione toouser account](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="b1a96-153">Fare clic su account utente di hello utilizzare toosign toohello CAL SAP, tooassociate **revisione**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="b1a96-154">associazione di hello toocreate tra l'utente e l'account di SAP CAL hello appena creato, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Associazione tooaccount dell'utente](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="b1a96-156">È stato creato un account SAP CAL in grado di:</span><span class="sxs-lookup"><span data-stu-id="b1a96-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="b1a96-157">Utilizzare il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b1a96-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="b1a96-158">Distribuire i sistemi SAP nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="b1a96-159">Prima di poter distribuire soluzioni SAP IDE hello basate su Windows e SQL Server, potrebbe essere necessario toosign per una sottoscrizione di SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="b1a96-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="b1a96-160">In caso contrario, la soluzione hello potrebbe essere visualizzato come **bloccato** nella pagina di panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="b1a96-161">Distribuire una soluzione</span><span class="sxs-lookup"><span data-stu-id="b1a96-161">Deploy a solution</span></span>
1. <span data-ttu-id="b1a96-162">Dopo aver impostato un account di SAP CAL, selezionare **hello soluzione SAP IDE su Windows e SQL Server** soluzione.</span><span class="sxs-lookup"><span data-stu-id="b1a96-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="b1a96-163">Fare clic su **Crea istanza**e verificare le condizioni di utilizzo e condizioni hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="b1a96-164">In hello **la modalità di base: Crea istanza** pagina, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b1a96-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="b1a96-165">a.</span><span class="sxs-lookup"><span data-stu-id="b1a96-165">a.</span></span> <span data-ttu-id="b1a96-166">Immettere un **nome** di istanza.</span><span class="sxs-lookup"><span data-stu-id="b1a96-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="b1a96-167">b.</span><span class="sxs-lookup"><span data-stu-id="b1a96-167">b.</span></span> <span data-ttu-id="b1a96-168">Selezionare un'**area** di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-168">Select an Azure **Region**.</span></span> <span data-ttu-id="b1a96-169">Potrebbe essere necessario un tooget sottoscrizione SAP CAL offerte più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="b1a96-170">c.</span><span class="sxs-lookup"><span data-stu-id="b1a96-170">c.</span></span>  <span data-ttu-id="b1a96-171">Immettere master hello **Password** per soluzione hello, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="b1a96-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![Modalità SAP CAL di base: creare un'istanza](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="b1a96-173">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-173">Click **Create**.</span></span> <span data-ttu-id="b1a96-174">Dopo alcuni minuti, a seconda delle dimensioni di hello e la complessità della soluzione hello (Buongiorno CAL SAP fornisce una stima), lo stato di hello viene visualizzato come attivo e pronto all'uso:</span><span class="sxs-lookup"><span data-stu-id="b1a96-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Istanze di SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="b1a96-176">gruppo di risorse toofind hello e tutti gli oggetti che sono stati creati da hello CAL SAP, visitare toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="b1a96-177">macchina virtuale Hello disponibili a partire dalla stessa istanza di nome specificato in hello SAP CAL hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Oggetti del gruppo di risorse](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="b1a96-179">Nel portale di SAP CAL hello, istanze toohello distribuito, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="b1a96-180">verrà visualizzata la finestra di Hello successiva finestra popup.</span><span class="sxs-lookup"><span data-stu-id="b1a96-180">hello following pop-up window appears:</span></span> 

    ![Connettersi toohello istanza](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="b1a96-182">Prima di poter utilizzare uno dei sistemi distribuito toohello tooconnect di hello opzioni, fare clic su **Guida introduttiva**.</span><span class="sxs-lookup"><span data-stu-id="b1a96-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="b1a96-183">i nomi di documentazione Hello hello utenti per ciascuno dei metodi di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="b1a96-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="b1a96-184">le password Hello per gli utenti vengono impostate toohello password master che è definito all'inizio di hello hello processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b1a96-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="b1a96-185">Nella documentazione di hello, sono elencati altri utenti più funzionalità e le relative password, che è possibile utilizzare toosign in toohello distribuita del sistema.</span><span class="sxs-lookup"><span data-stu-id="b1a96-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![Documentazione di benvenuto di SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="b1a96-187">In poche ore un sistema SAP IDES integro verrà distribuito in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="b1a96-188">Se è stata acquistata una sottoscrizione CAL SAP, SAP supporta distribuzioni tramite hello CAL SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a96-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="b1a96-189">coda di supporto Hello è BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="b1a96-189">hello support queue is BC-VCM-CAL.</span></span>

