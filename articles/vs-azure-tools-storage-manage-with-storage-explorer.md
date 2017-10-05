---
title: Guida introduttiva a Storage Explorer (anteprima) | Microsoft Docs
description: Gestire le risorsa di archiviazione di Azure con Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="53bb9-103">Guida introduttiva a Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="53bb9-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="53bb9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="53bb9-104">Overview</span></span>
<span data-ttu-id="53bb9-105">Azure Storage Explorer (anteprima) è un'app autonoma che consente di usare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="53bb9-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="53bb9-106">Questo articolo illustra diversi modi per connettersi agli account di archiviazione di Azure e per gestirli.</span><span class="sxs-lookup"><span data-stu-id="53bb9-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (anteprima)][15]

## <a name="prerequisites"></a><span data-ttu-id="53bb9-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="53bb9-108">Prerequisites</span></span>
* [<span data-ttu-id="53bb9-109">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="53bb9-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="53bb9-110">Connettersi a un account o a un servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="53bb9-110">Connect to a storage account or service</span></span>
<span data-ttu-id="53bb9-111">Storage Explorer (anteprima) offre numerosi modi per connettersi agli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="53bb9-112">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="53bb9-112">For example, you can:</span></span>
* <span data-ttu-id="53bb9-113">Connettersi agli account di archiviazione associati alle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="53bb9-114">Connettersi agli account e ai servizi di archiviazione condivisi da altre sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="53bb9-115">Connettersi alla risorsa di archiviazione locale e gestirla usando l'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="53bb9-116">Inoltre, è possibile usare gli account di archiviazione in Azure globale e nazionale:</span><span class="sxs-lookup"><span data-stu-id="53bb9-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="53bb9-117">[Connettersi a una sottoscrizione di Azure](#connect-to-an-azure-subscription): gestire le risorse di archiviazione appartenenti alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="53bb9-118">[Usare la risorsa di archiviazione locale](#work-with-local-development-storage): gestire la risorsa di archiviazione locale usando l'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="53bb9-119">[Collegarsi a una risorsa di archiviazione esterna](#attach-or-detach-an-external-storage-account): gestire le risorse di archiviazione appartenenti a un'altra sottoscrizione di Azure o ai cloud di Azure nazionale usando il nome, la chiave e gli endpoint dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="53bb9-120">[Collegare un account di archiviazione usando la firma di accesso condiviso](#attach-storage-account-using-sas): gestire le risorse di archiviazione appartenenti a un'altra sottoscrizione di Azure usando una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="53bb9-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="53bb9-121">[Collegare un servizio usando la firma di accesso condiviso](#attach-service-using-sas): gestire un servizio di archiviazione specifico (contenitore BLOB, coda o tabella) appartenente a un'altra sottoscrizione di Azure usando una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="53bb9-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="53bb9-122">Connettersi a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="53bb9-123">Se non si ha un account Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="53bb9-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="53bb9-124">In Storage Explorer (anteprima), selezionare **Azure Account settings**(Impostazioni account Azure).</span><span class="sxs-lookup"><span data-stu-id="53bb9-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure Account settings][0]

2. <span data-ttu-id="53bb9-126">Il riquadro sinistro visualizza tutti gli account Microsoft a cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="53bb9-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="53bb9-127">Per connettersi a un altro account, selezionare **Aggiungi un account** e seguire le istruzioni per accedere con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="53bb9-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="53bb9-128">La connessione ad Azure nazionale, ad esempio Azure Germania, Azure per enti pubblici e Azure Cina tramite accesso, non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="53bb9-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="53bb9-129">Vedere la sezione "Collegare o scollegare un account di archiviazione esterno" per la modalità di connessione agli account di archiviazione di Azure nazionale.</span><span class="sxs-lookup"><span data-stu-id="53bb9-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="53bb9-130">Dopo aver effettuato l'accesso con un account Microsoft, il riquadro sinistro viene popolato con le sottoscrizioni di Azure associate a tale account.</span><span class="sxs-lookup"><span data-stu-id="53bb9-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="53bb9-131">Selezionare le sottoscrizioni di Azure da usare e quindi selezionare **Applica**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="53bb9-132">Selezionando **Tutte le sottoscrizioni** , viene alternata la selezione di tutte o di nessuna delle sottoscrizioni di Azure elencate.</span><span class="sxs-lookup"><span data-stu-id="53bb9-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Selezionare le sottoscrizioni di Azure][3]  
    <span data-ttu-id="53bb9-134">Il riquadro sinistro mostra gli account di archiviazione associati alle sottoscrizioni di Azure selezionate.</span><span class="sxs-lookup"><span data-stu-id="53bb9-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Sottoscrizioni di Azure selezionate][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="53bb9-136">Connettersi a una sottoscrizione di Azure Stack</span><span class="sxs-lookup"><span data-stu-id="53bb9-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="53bb9-137">Per informazioni sulla connessione a una sottoscrizione di Azure Stack, vedere [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md) (Connettere Storage Explorer a una sottoscrizione di Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="53bb9-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="53bb9-138">Utilizzare la risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="53bb9-138">Work with local development storage</span></span>
<span data-ttu-id="53bb9-139">Storage Explorer (anteprima) consente di lavorare con la risorsa di archiviazione locale usando l'emulatore di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="53bb9-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="53bb9-140">che consente di scrivere codice per la risorsa di archiviazione e di testarla senza necessariamente avere un account di archiviazione distribuito in Azure, perché l'account di archiviazione viene emulato dall'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="53bb9-141">Emulatore di archiviazione di Azure è attualmente supportato solo per Windows.</span><span class="sxs-lookup"><span data-stu-id="53bb9-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="53bb9-142">Nel riquadro sinistro di Storage Explorer (anteprima) espandere il nodo **(Local and Attached) (Locale e collegato)** > **Storage Accounts (Account di archiviazione)** > **(Development) (Sviluppo)**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nodo di sviluppo locale][21]

2. <span data-ttu-id="53bb9-144">Se Emulatore di archiviazione di Azure non è ancora stato installato, verrà richiesto di farlo tramite una barra informazioni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="53bb9-145">Se la barra informazioni è visualizzata, selezionare **Scarica la versione più recente** e installare l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="53bb9-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Richiesta di download dell'Emulatore di archiviazione di Azure][22]

3. <span data-ttu-id="53bb9-147">Dopo aver installato l'emulatore è possibile creare e usare BLOB, code e tabelle locali.</span><span class="sxs-lookup"><span data-stu-id="53bb9-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="53bb9-148">Per informazioni su come usare i vari tipi di account di archiviazione, vedere uno degli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="53bb9-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="53bb9-149">Gestire le risorse dell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="53bb9-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="53bb9-150">Manage Azure file share storage resources (Gestire risorse di condivisione file di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="53bb9-151">Manage Azure queue storage resources (Gestire risorse di archiviazione code di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="53bb9-152">Manage Azure table storage resources (Gestire risorse di archiviazione tabelle di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="53bb9-153">Collegare o scollegare un account di archiviazione esterno</span><span class="sxs-lookup"><span data-stu-id="53bb9-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="53bb9-154">Storage Explorer (anteprima) consente di collegarsi agli account di archiviazione esterni per poter condividere facilmente gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="53bb9-155">Questa sezione illustra come collegarsi (e scollegarsi) agli account di archiviazione esterni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="53bb9-156">Ottenere le credenziali dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="53bb9-156">Get the storage account credentials</span></span>
<span data-ttu-id="53bb9-157">Per condividere un account di archiviazione esterno, il proprietario di tale account deve prima ottenere le credenziali, ovvero il nome e la chiave dell'account, e quindi condividere tali informazioni con la persona che vuole collegarsi a tale account esterno.</span><span class="sxs-lookup"><span data-stu-id="53bb9-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="53bb9-158">Per ottenere le credenziali dell'account di archiviazione nel portale di Azure, è possibile seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="53bb9-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="53bb9-159">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="53bb9-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="53bb9-160">Selezionare **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-160">Select **Browse**.</span></span>

3. <span data-ttu-id="53bb9-161">Selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="53bb9-162">Nel pannello **Account di archiviazione** selezionare l'account di archiviazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="53bb9-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="53bb9-163">Nel pannello **Impostazioni** per l'account di archiviazione selezionare **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Opzione Chiavi di accesso][5]

6. <span data-ttu-id="53bb9-165">Nel pannello **Chiavi di accesso** copiare i valori di **Nome account di archiviazione** e **key1** da usare quando ci si collega all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Chiavi di accesso][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="53bb9-167">Collegarsi a un account di archiviazione esterno</span><span class="sxs-lookup"><span data-stu-id="53bb9-167">Attach to an external storage account</span></span>
<span data-ttu-id="53bb9-168">Per il collegamento a un account di archiviazione esterno è necessario avere la chiave e il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="53bb9-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="53bb9-169">La sezione "Ottenere le credenziali dell'account di archiviazione" spiega come ottenere questi valori dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="53bb9-170">Nel portale, la chiave dell'account è tuttavia denominata **key1**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="53bb9-171">Quando Storage Explorer (anteprima) chiede la chiave dell'account, immettere quindi il valore di **key1**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="53bb9-172">In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="53bb9-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. <span data-ttu-id="53bb9-174">Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare la chiave dell'account, ovvero il valore di **key1** ottenuto dal portale di Azure, e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53bb9-175">È possibile immettere la stringa di connessione di archiviazione di un account di archiviazione in Azure nazionale.</span><span class="sxs-lookup"><span data-stu-id="53bb9-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="53bb9-176">Per connettersi ad esempio ad account di archiviazione di Azure Germania, immettere stringhe di connessione simile alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="53bb9-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="53bb9-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="53bb9-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="53bb9-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="53bb9-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="53bb9-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="53bb9-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="53bb9-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="53bb9-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="53bb9-181">È possibile ottenere la stringa di connessione dal portale di Azure come descritto nella sezione "Ottenere le credenziali dell'account di archiviazione".</span><span class="sxs-lookup"><span data-stu-id="53bb9-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. <span data-ttu-id="53bb9-183">Nella finestra di dialogo **Associa archiviazione esterna** immettere il nome dell'account di archiviazione nella casella **Nome account**, specificare eventuali altre impostazioni e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Finestra di dialogo Associa archiviazione esterna][8]

4. <span data-ttu-id="53bb9-185">Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="53bb9-186">Per apportare modifiche, selezionare **Indietro** e immettere nuovamente le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="53bb9-187">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-187">Select **Connect**.</span></span>

6. <span data-ttu-id="53bb9-188">Dopo la connessione, l'account di archiviazione esterno viene visualizzato con il testo **(Esterno)** aggiunto al nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Risultato della connessione a un account di archiviazione esterno][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="53bb9-190">Scollegarsi da un account di archiviazione esterno</span><span class="sxs-lookup"><span data-stu-id="53bb9-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="53bb9-191">Fare clic con il pulsante destro del mouse sull'account di archiviazione esterno che si vuole scollegare e quindi scegliere **Scollega**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Opzione per scollegarsi da un account di archiviazione][10]

2. <span data-ttu-id="53bb9-193">Nella finestra di dialogo del messaggio di conferma, selezionare **Sì** per confermare che si vuole scollegare l'account di archiviazione esterno.</span><span class="sxs-lookup"><span data-stu-id="53bb9-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="53bb9-194">Collegare un account di archiviazione usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="53bb9-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="53bb9-195">Una [firma di accesso condiviso](storage/common/storage-dotnet-shared-access-signature-part-1.md) consente all'amministratore di una sottoscrizione di Azure di concedere temporaneamente l'accesso a un account di archiviazione senza dover fornire le credenziali della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="53bb9-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="53bb9-196">Per illustrare questo scenario, si supponga che l'utente A sia l'amministratore di una sottoscrizione di Azure e che voglia consentire all'utente B di accedere a un account di archiviazione per un periodo limitato con determinate autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="53bb9-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="53bb9-197">L'utente A genera una firma di accesso condiviso, costituita dalla stringa di connessione per l'account di archiviazione, per un periodo di tempo specifico e con le autorizzazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="53bb9-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="53bb9-198">L'utente A condivide la firma di accesso condiviso con la persona che vuole accedere all'account di archiviazione, ovvero l'utente B.</span><span class="sxs-lookup"><span data-stu-id="53bb9-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="53bb9-199">L'utente B usa Storage Explorer (anteprima) per collegarsi all'account appartenente all'utente A usando la firma di accesso condiviso fornita.</span><span class="sxs-lookup"><span data-stu-id="53bb9-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="53bb9-200">Ottenere una firma di accesso condiviso per l'account che si vuole condividere</span><span class="sxs-lookup"><span data-stu-id="53bb9-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="53bb9-201">In Storage Explorer (anteprima) fare clic con il pulsante destro del mouse sull'account di archiviazione che si vuole condividere e quindi scegliere **Get Shared Access Signature** (Ottieni firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="53bb9-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Menu di scelta rapida Get SAS (Ottieni firma di accesso condiviso)][13]

2. <span data-ttu-id="53bb9-203">Nella finestra di dialogo **Shared Access Signature** (Firma di accesso condiviso) specificare il periodo di tempo e le autorizzazioni per l'account e quindi selezionare **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="53bb9-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="53bb9-204">![Finestra di dialogo Get SAS][14] (Ottieni firma di accesso condiviso)</span><span class="sxs-lookup"><span data-stu-id="53bb9-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="53bb9-205">La finestra di dialogo **Firma di accesso condiviso** visualizza la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="53bb9-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="53bb9-206">Selezionare **Copia** accanto a **Stringa di connessione** per copiare la stringa negli Appunti e quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="53bb9-207">Collegarsi all'account condiviso usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="53bb9-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="53bb9-208">In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="53bb9-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. <span data-ttu-id="53bb9-210">Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare la stringa di connessione e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. <span data-ttu-id="53bb9-212">Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="53bb9-213">Per apportare modifiche, selezionare **Indietro** e immettere le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="53bb9-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="53bb9-214">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-214">Select **Connect**.</span></span>

5. <span data-ttu-id="53bb9-215">Una volta collegato, l'account di archiviazione verrà visualizzato con il testo **(SAS)** (Firma di accesso condiviso) aggiunto al nome dell'account specificato.</span><span class="sxs-lookup"><span data-stu-id="53bb9-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![Risultato del collegamento a un account con firma di accesso condiviso][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="53bb9-217">Collegare un servizio usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="53bb9-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="53bb9-218">La sezione "Collegare un account di archiviazione usando la firma di accesso condiviso" illustra come l'amministratore di una sottoscrizione di Azure possa concedere l'accesso temporaneo a un account di archiviazione generando e condividendo una firma di accesso condiviso per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="53bb9-219">È allo stesso modo possibile generare una firma di accesso condiviso per un servizio specifico, ovvero contenitore BLOB, coda o tabella, in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53bb9-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="53bb9-220">Generare una firma di accesso condiviso per il servizio che si vuole condividere</span><span class="sxs-lookup"><span data-stu-id="53bb9-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="53bb9-221">In questo contesto, un servizio può essere un contenitore BLOB, una coda o una tabella.</span><span class="sxs-lookup"><span data-stu-id="53bb9-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="53bb9-222">Per generare la firma di accesso condiviso per un servizio elencato, vedere:</span><span class="sxs-lookup"><span data-stu-id="53bb9-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="53bb9-223">Ottenere la firma di accesso condiviso per un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="53bb9-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="53bb9-224">Get the SAS for a file share (Ottenere la firma di accesso condiviso per una condivisione file): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="53bb9-225">Get the SAS for a queue (Ottenere la firma di accesso condiviso per una coda): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="53bb9-226">Get the SAS for a table (Ottenere la firma di accesso condiviso per una tabella): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="53bb9-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="53bb9-227">Collegarsi al servizio account condiviso usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="53bb9-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="53bb9-228">In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="53bb9-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. <span data-ttu-id="53bb9-230">Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare l'URI della firma di accesso condiviso e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. <span data-ttu-id="53bb9-232">Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="53bb9-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="53bb9-233">Per apportare modifiche, selezionare **Indietro** e immettere le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="53bb9-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="53bb9-234">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="53bb9-234">Select **Connect**.</span></span>

5. <span data-ttu-id="53bb9-235">Una volta collegato, il nuovo servizio collegato verrà visualizzato nel nodo **(Service SAS)** (Firma di accesso condiviso servizio).</span><span class="sxs-lookup"><span data-stu-id="53bb9-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Risultato della connessione a un servizio condiviso usando una firma di accesso condiviso][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="53bb9-237">Cercare gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="53bb9-237">Search for storage accounts</span></span>
<span data-ttu-id="53bb9-238">Se l'elenco di account di archiviazione è lungo, è possibile trovare rapidamente un determinato account di archiviazione usando la casella di ricerca nella parte superiore del riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="53bb9-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="53bb9-239">Mentre si digita nella casella di ricerca, il riquadro sinistro mostra gli account di archiviazione che corrispondono al valore di ricerca immesso fino a quel momento.</span><span class="sxs-lookup"><span data-stu-id="53bb9-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="53bb9-240">La ricerca di tutti gli account di archiviazione il cui nome contiene **tarcher** è ad esempio illustrata nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="53bb9-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Ricerca dell'account di archiviazione][11]

## <a name="next-steps"></a><span data-ttu-id="53bb9-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53bb9-242">Next steps</span></span>
* [<span data-ttu-id="53bb9-243">Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="53bb9-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
