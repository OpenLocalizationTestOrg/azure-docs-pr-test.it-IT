---
title: un account di Batch nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come account toocreate un Batch di Azure in hello toorun portale Azure carichi di lavoro paralleli su larga scala nel cloud hello
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="f1839-103">Creare un account Batch con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1839-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1839-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1839-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="f1839-105">.NET per la gestione di Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="f1839-106">Informazioni su come l'account toocreate un Batch di Azure hello [portale di Azure][azure_portal], quindi scegliere Proprietà account hello che adattarlo allo scenario di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f1839-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="f1839-107">Informazioni in cui le proprietà dell'account importante toofind come chiavi di accesso e gli URL di account.</span><span class="sxs-lookup"><span data-stu-id="f1839-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="f1839-108">Per informazioni sugli account di Batch e scenari, vedere hello [panoramica delle funzioni](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="f1839-109">Creare un account Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-109">Create a Batch account</span></span>

<span data-ttu-id="f1839-110">Utilizzare hello portale toocreate un account Batch in uno dei due hello *modalità di allocazione del pool*: **Batch servizio** modalità o hello più recente **sottoscrizione utente** modalità, che richiede più configurazione.</span><span class="sxs-lookup"><span data-stu-id="f1839-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="f1839-111">Per informazioni su queste due modalità, vedere hello [panoramica delle funzioni](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="f1839-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="f1839-112">Per le funzionalità della modalità di sottoscrizione utente hello, vedere anche hello [post di blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="f1839-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="f1839-113">Modalità di servizio Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-113">Batch service mode</span></span>



1. <span data-ttu-id="f1839-114">Accedi toohello [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="f1839-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="f1839-115">Fare clic su **Nuovo** > **Calcolo** > **Servizio Batch**.</span><span class="sxs-lookup"><span data-stu-id="f1839-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch in hello Marketplace][marketplace_portal]
3. <span data-ttu-id="f1839-117">Hello **nuovo Account Batch** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="f1839-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="f1839-118">Vedere le descrizioni di hello di sotto di ciascun elemento del pannello.</span><span class="sxs-lookup"><span data-stu-id="f1839-118">See hello descriptions below of each blade element.</span></span>

    ![Creare un account Batch][account_portal]

    <span data-ttu-id="f1839-120">a.</span><span class="sxs-lookup"><span data-stu-id="f1839-120">a.</span></span> <span data-ttu-id="f1839-121">**Nome dell'account**: nome dell'account Batch hello scelto deve essere univoco all'interno di hello regione di Azure in cui viene creato l'account di hello (vedere **percorso** sotto).</span><span class="sxs-lookup"><span data-stu-id="f1839-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="f1839-122">nome dell'account Hello può contenere solo caratteri minuscoli o numeri e deve essere compresa tra 3 e 24 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f1839-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="f1839-123">b.</span><span class="sxs-lookup"><span data-stu-id="f1839-123">b.</span></span> <span data-ttu-id="f1839-124">**Sottoscrizione**: hello sottoscrizione in cui hello toocreate account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="f1839-125">Se è presente solo una sottoscrizione, è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f1839-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="f1839-126">c.</span><span class="sxs-lookup"><span data-stu-id="f1839-126">c.</span></span> <span data-ttu-id="f1839-127">**Modalità di allocazione pool**: selezionare **Batch service**.</span><span class="sxs-lookup"><span data-stu-id="f1839-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="f1839-128">c.</span><span class="sxs-lookup"><span data-stu-id="f1839-128">c.</span></span> <span data-ttu-id="f1839-129">**Gruppo di risorse**: selezionare un gruppo di risorse esistente per il nuovo account Batch. È possibile crearne facoltativamente uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="f1839-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="f1839-130">d.</span><span class="sxs-lookup"><span data-stu-id="f1839-130">d.</span></span> <span data-ttu-id="f1839-131">**Percorso**: hello Azure area in cui hello toocreate account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="f1839-132">Solo le aree di hello è supportate per la sottoscrizione e il gruppo di risorse vengono visualizzate come opzioni.</span><span class="sxs-lookup"><span data-stu-id="f1839-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="f1839-133">e.</span><span class="sxs-lookup"><span data-stu-id="f1839-133">e.</span></span> <span data-ttu-id="f1839-134">**Account di archiviazione** (facoltativo): account di Archiviazione di Azure per uso generico associato all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="f1839-135">Tale operazione è consigliata per la maggior parte degli account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="f1839-136">Per altri dettagli, vedere più avanti [Account di archiviazione di Azure collegato](#linked-azure-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="f1839-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="f1839-137">Fare clic su **crea** account hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1839-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="f1839-138">portale Hello indica la distribuzione è in corso.</span><span class="sxs-lookup"><span data-stu-id="f1839-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="f1839-139">Al termine, un viene visualizzata una notifica **Le distribuzioni sono riuscite** in **Notifiche**.</span><span class="sxs-lookup"><span data-stu-id="f1839-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="f1839-140">Modalità di sottoscrizione utente</span><span class="sxs-lookup"><span data-stu-id="f1839-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="f1839-141">Consente di Azure Batch tooaccess hello della sottoscrizione (operazione monouso)</span><span class="sxs-lookup"><span data-stu-id="f1839-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="f1839-142">Quando si crea il primo account Batch in modalità di sottoscrizione utente, eseguire la sottoscrizione con Batch hello tooregister i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f1839-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="f1839-143">(Se viene eseguita in precedenza questa operazione, ignorare toohello nella sezione successiva).</span><span class="sxs-lookup"><span data-stu-id="f1839-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="f1839-144">Accedi toohello [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="f1839-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="f1839-145">Fare clic su **più servizi** > **sottoscrizioni**, fare clic su sottoscrizione hello da toouse per hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="f1839-146">In hello **sottoscrizione** pannello, fare clic su **Access control (IAM)** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f1839-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Controllo di accesso alla sottoscrizione][subscription_access]

4. <span data-ttu-id="f1839-148">In hello **aggiungere autorizzazioni** blade, seleziona hello **collaboratore** ruolo, cercare hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="f1839-149">Fino a individuare hello API di ricerca per ognuna di queste stringhe:</span><span class="sxs-lookup"><span data-stu-id="f1839-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="f1839-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="f1839-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="f1839-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="f1839-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="f1839-152">I tenant di Azure AD più recenti potrebbero usare questo nome.</span><span class="sxs-lookup"><span data-stu-id="f1839-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="f1839-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** ID hello per hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="f1839-154">Dopo aver individuato hello API Batch, selezionarlo e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f1839-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Aggiungere le autorizzazioni di Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="f1839-156">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="f1839-156">Create a key vault</span></span>
<span data-ttu-id="f1839-157">In modalità di sottoscrizione utente, è necessario un insieme di credenziali chiave di Azure che appartiene toothe stesso gruppo di risorse hello Batch account toobe creato.</span><span class="sxs-lookup"><span data-stu-id="f1839-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="f1839-158">Verificare che il gruppo di risorse hello è in un'area in cui è Batch [disponibile](https://azure.microsoft.com/regions/services/) e che supporta la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f1839-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="f1839-159">In hello [portale di Azure][azure_portal], fare clic su **New** > **sicurezza + identità** > **insieme di credenziali chiave** .</span><span class="sxs-lookup"><span data-stu-id="f1839-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="f1839-160">In hello **Crea insieme di credenziali chiave** pannello, immettere un nome per l'insieme di credenziali chiave hello e creare un gruppo di risorse nell'area di hello desiderato per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="f1839-161">Lasciare le impostazioni di valori predefiniti rimanenti hello, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f1839-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="f1839-162">Creare un account Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-162">Create a Batch account</span></span>

1. <span data-ttu-id="f1839-163">In hello [portale di Azure][azure_portal], fare clic su **New** > **calcolo** > **servizio Batch**.</span><span class="sxs-lookup"><span data-stu-id="f1839-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch in hello Marketplace][marketplace_portal]
3. <span data-ttu-id="f1839-165">Hello **nuovo Account Batch** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="f1839-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="f1839-166">Vedere le descrizioni di hello di sotto di ciascun elemento del pannello.</span><span class="sxs-lookup"><span data-stu-id="f1839-166">See hello descriptions below of each blade element.</span></span>

    ![Creare un account Batch][account_portal_byos]

    <span data-ttu-id="f1839-168">a.</span><span class="sxs-lookup"><span data-stu-id="f1839-168">a.</span></span> <span data-ttu-id="f1839-169">**Nome dell'account**: nome dell'account Batch hello scelto deve essere univoco all'interno di hello regione di Azure in cui viene creato l'account di hello (vedere **percorso** sotto).</span><span class="sxs-lookup"><span data-stu-id="f1839-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="f1839-170">nome dell'account Hello può contenere solo caratteri minuscoli o numeri e deve essere compresa tra 3 e 24 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f1839-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="f1839-171">b.</span><span class="sxs-lookup"><span data-stu-id="f1839-171">b.</span></span> <span data-ttu-id="f1839-172">**Sottoscrizione**: se si dispone di più di una sottoscrizione, selezionare una sottoscrizione hello registrati con hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="f1839-173">c.</span><span class="sxs-lookup"><span data-stu-id="f1839-173">c.</span></span> <span data-ttu-id="f1839-174">**Modalità di allocazione pool**: selezionare **Sottoscrizione utente**.</span><span class="sxs-lookup"><span data-stu-id="f1839-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="f1839-175">d.</span><span class="sxs-lookup"><span data-stu-id="f1839-175">d.</span></span> <span data-ttu-id="f1839-176">**Insieme di credenziali chiave**: hello selezionare insieme di credenziali chiave creata per l'account Batch nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f1839-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="f1839-177">In modo facoltativo creare un nuovo insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="f1839-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="f1839-178">Dopo aver selezionato l'insieme di credenziali hello, selezionare hello casella di controllo toogrant Azure Batch accesso toohello chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f1839-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="f1839-179">c.</span><span class="sxs-lookup"><span data-stu-id="f1839-179">c.</span></span> <span data-ttu-id="f1839-180">**Gruppo di risorse**: gruppo di risorse selezionare hello in cui viene creato l'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="f1839-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="f1839-181">d.</span><span class="sxs-lookup"><span data-stu-id="f1839-181">d.</span></span> <span data-ttu-id="f1839-182">**Percorso**: hello Azure area in cui è stato creato hello chiave dell'insieme di credenziali per l'account Batch hello.</span><span class="sxs-lookup"><span data-stu-id="f1839-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="f1839-183">e.</span><span class="sxs-lookup"><span data-stu-id="f1839-183">e.</span></span> <span data-ttu-id="f1839-184">**Account di archiviazione** (facoltativo): account di Archiviazione di Azure per uso generico associato all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="f1839-185">Tale operazione è consigliata per la maggior parte degli account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="f1839-186">Per altri dettagli, vedere più avanti [Account di archiviazione di Azure collegato](#linked-azure-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="f1839-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="f1839-187">Fare clic su **crea** account hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1839-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="f1839-188">portale Hello indica la distribuzione è in corso.</span><span class="sxs-lookup"><span data-stu-id="f1839-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="f1839-189">Al termine, un viene visualizzata una notifica **Le distribuzioni sono riuscite** in **Notifiche**.</span><span class="sxs-lookup"><span data-stu-id="f1839-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="f1839-190">Visualizzare le proprietà dell'account Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-190">View Batch account properties</span></span>
<span data-ttu-id="f1839-191">Una volta hello account è stato creato, è possibile aprire hello **pannello account Batch** tooaccess le impostazioni e proprietà.</span><span class="sxs-lookup"><span data-stu-id="f1839-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="f1839-192">È possibile accedere a tutte le impostazioni dell'account e le proprietà tramite i menu a sinistra del Pannello di account Batch hello hello.</span><span class="sxs-lookup"><span data-stu-id="f1839-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Pannello Account Batch nel portale di Azure][account_blade]

* <span data-ttu-id="f1839-194">**URL dell'account batch**: quando si sviluppa un'applicazione con hello [API Batch](batch-apis-tools.md#azure-accounts-for-batch-development), è necessario un tooaccess URL di account delle risorse di Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="f1839-195">Un URL dell'account Batch è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="f1839-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL dell'account Batch nel portale][account_url]

* <span data-ttu-id="f1839-197">**Le chiavi di accesso** (modalità servizio Batch): tooauthenticate accesso tooyour account Batch dall'applicazione, è necessario una chiave di accesso di account.</span><span class="sxs-lookup"><span data-stu-id="f1839-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="f1839-198">Questa impostazione non è disponibile in modalità di sottoscrizione utente, in cui si usa l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1839-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="f1839-199">tooview o rigenerare le chiavi di accesso dell'account Batch, immettere `keys` nel menu a sinistra di hello **ricerca** nel Pannello di account Batch hello e quindi selezionare **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="f1839-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Chiavi dell'account Batch nel portale di Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="f1839-201">Account di archiviazione di Azure collegato</span><span class="sxs-lookup"><span data-stu-id="f1839-201">Linked Azure Storage account</span></span>

<span data-ttu-id="f1839-202">Facoltativamente, è possibile collegare un utilizzo generale tooyour di account di archiviazione di Azure account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="f1839-203">Hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch utilizza l'archiviazione Blob di Azure, come hello [Batch File convenzioni .NET](batch-task-output.md) libreria.</span><span class="sxs-lookup"><span data-stu-id="f1839-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="f1839-204">Queste funzionalità opzionali facilitano la distribuzione delle applicazioni che eseguono le attività Batch hello e rendere persistenti i dati di hello che producono.</span><span class="sxs-lookup"><span data-stu-id="f1839-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="f1839-205">È consigliabile creare un nuovo account di archiviazione da usare esclusivamente con l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Creazione di un account di archiviazione per utilizzo generico][storage_account]

> [!NOTE]
> <span data-ttu-id="f1839-207">Azure Batch supporta attualmente solo hello Storage account tipi generici.</span><span class="sxs-lookup"><span data-stu-id="f1839-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="f1839-208">Questo tipo di account è descritto nel passaggio 5, [Creare un account di archiviazione] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="f1839-209">Prestare attenzione quando si rigenerano le chiavi di accesso hello di un account di archiviazione collegato.</span><span class="sxs-lookup"><span data-stu-id="f1839-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="f1839-210">Rigenera solo una chiave di account di archiviazione e fare clic su **sincronizzazione delle chiavi** su hello collegato blade di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f1839-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="f1839-211">Attendere cinque minuti tooallow hello chiavi toopropagate toohello nodi di calcolo nei pool, quindi rigenerare e sincronizzare hello altre chiavi, se necessario.</span><span class="sxs-lookup"><span data-stu-id="f1839-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="f1839-212">Se si rigenera entrambe le chiavi in hello stesso tempo, i nodi di calcolo non saranno in grado di toosynchronize ognuna delle due chiavi e account di accesso toohello archiviazione andranno perse.</span><span class="sxs-lookup"><span data-stu-id="f1839-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="f1839-213">![Rigenerazione delle chiavi degli account di archiviazione][4]</span><span class="sxs-lookup"><span data-stu-id="f1839-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="f1839-214">Quote e limiti del servizio Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-214">Batch service quotas and limits</span></span>
<span data-ttu-id="f1839-215">Essere consapevoli che come con la sottoscrizione di Azure e altri Azure dei servizi, alcuni [quote e limiti](batch-quota-limit.md) applicare tooBatch account.</span><span class="sxs-lookup"><span data-stu-id="f1839-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="f1839-216">Le quote correnti per un account Batch vengono visualizzate nel portale di hello nell'account hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="f1839-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Quote dell'account Batch nel portale di Azure][quotas]



<span data-ttu-id="f1839-218">Inoltre, molte di queste quote possono essere aumentate semplicemente con una richiesta di supporto prodotto gratuito inviata nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f1839-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="f1839-219">Vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per ulteriori informazioni sulla richiesta di quota aumenta.</span><span class="sxs-lookup"><span data-stu-id="f1839-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="f1839-220">Altre opzioni di gestione dell'account Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-220">Other Batch account management options</span></span>
<span data-ttu-id="f1839-221">Inoltre toousing hello portale di Azure, è anche possibile creare e gestire gli account Batch con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="f1839-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="f1839-222">Cmdlet di PowerShell per Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="f1839-223">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f1839-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="f1839-224">.NET per la gestione di Batch</span><span class="sxs-lookup"><span data-stu-id="f1839-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="f1839-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1839-225">Next steps</span></span>
* <span data-ttu-id="f1839-226">Vedere hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md) toolearn ulteriori informazioni sulle funzionalità e concetti relativi al servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="f1839-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="f1839-227">articolo Hello illustra risorse Batch primarie hello come pool, nodi di calcolo, i processi e attività e viene fornita una panoramica di hello funzionalità del servizio che consentono l'esecuzione del carico di lavoro di calcolo su larga scala.</span><span class="sxs-lookup"><span data-stu-id="f1839-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="f1839-228">Nozioni di base hello dello sviluppo di un'applicazione abilitata per Batch utilizzando hello [libreria client .NET per Batch](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f1839-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="f1839-229">Questi articoli introduttivi consentono di eseguire un'applicazione funzionante che utilizza hello Batch servizio tooexecute un carico di lavoro in più nodi di calcolo e include l'utilizzo di archiviazione di Azure per il recupero e la gestione temporanea di file del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f1839-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Rigenerazione delle chiavi degli account di archiviazione"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
