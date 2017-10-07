---
title: aaaGet avviato con Esplora risorse di archiviazione (anteprima) | Documenti Microsoft
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
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="31180-103">Guida introduttiva a Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="31180-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="31180-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="31180-104">Overview</span></span>
<span data-ttu-id="31180-105">Esplora archivi Azure (anteprima) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="31180-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="31180-106">In questo articolo viene illustrato hello diverse modalità di connessione tooand gestione degli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (anteprima)][15]

## <a name="prerequisites"></a><span data-ttu-id="31180-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31180-108">Prerequisites</span></span>
* [<span data-ttu-id="31180-109">Scaricare e installare Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="31180-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="31180-110">Connettersi al servizio o account di archiviazione tooa</span><span class="sxs-lookup"><span data-stu-id="31180-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="31180-111">Esplorazione dell'archiviazione (anteprima) fornisce diversi metodi tooconnect toostorage account.</span><span class="sxs-lookup"><span data-stu-id="31180-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="31180-112">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="31180-112">For example, you can:</span></span>
* <span data-ttu-id="31180-113">Collegare gli account toostorage associati alle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="31180-114">Connettersi toostorage account e servizi che vengono condivisi da altre sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="31180-115">Connettersi tooand gestire l'archiviazione locale tramite hello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="31180-116">Inoltre, è possibile usare gli account di archiviazione in Azure globale e nazionale:</span><span class="sxs-lookup"><span data-stu-id="31180-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="31180-117">[Connettersi tooan sottoscrizione di Azure](#connect-to-an-azure-subscription): gestire le risorse di archiviazione che appartengono tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="31180-118">[Utilizzare l'archiviazione locale per lo sviluppo](#work-with-local-development-storage): gestire l'archiviazione locale tramite hello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="31180-119">[Collega archiviazione tooexternal](#attach-or-detach-an-external-storage-account): gestire le risorse di archiviazione che appartengono tooanother sottoscrizione di Azure o che si trovano in national cloud di Azure con nome, chiave e gli endpoint dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="31180-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="31180-120">[Collegare un account di archiviazione tramite una firma di accesso condiviso](#attach-storage-account-using-sas): gestire le risorse di archiviazione che appartengono tooanother sottoscrizione di Azure tramite una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="31180-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="31180-121">[Collegare un servizio utilizzando una firma di accesso condiviso](#attach-service-using-sas): gestione di un servizio di archiviazione specifico (contenitore blob, coda o tabella) che appartiene tooanother sottoscrizione di Azure tramite una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="31180-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="31180-122">Connettersi tooan sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="31180-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="31180-123">Se non si ha un account Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="31180-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="31180-124">In Storage Explorer (anteprima), selezionare **Azure Account settings**(Impostazioni account Azure).</span><span class="sxs-lookup"><span data-stu-id="31180-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure Account settings][0]

2. <span data-ttu-id="31180-126">riquadro di sinistra Hello Visualizza tutti gli account di Microsoft hello a che è stato effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="31180-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="31180-127">tooconnect tooanother account, selezionare **aggiungere un account**, quindi seguire hello istruzioni toosign con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="31180-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="31180-128">Connessione toonational Azure (ad esempio Azure in Germania, Azure per enti pubblici e Cina di Azure tramite Accedi) non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="31180-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="31180-129">Vedere hello "collegamento o scollegamento di un account di archiviazione esterno" sezione per informazioni su come tooconnect toonational account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="31180-130">Dopo aver accedere correttamente con un account Microsoft, a sinistra hello riquadro viene popolato con hello le sottoscrizioni di Azure associate all'account.</span><span class="sxs-lookup"><span data-stu-id="31180-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="31180-131">Selezionare le sottoscrizioni di Azure che si desidera toowork con e quindi selezionare di hello **applica**.</span><span class="sxs-lookup"><span data-stu-id="31180-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="31180-132">(Selezione **tutte le sottoscrizioni** attiva o disattiva la selezione di tutti o nessuno dei hello elencate le sottoscrizioni di Azure.)</span><span class="sxs-lookup"><span data-stu-id="31180-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Selezionare le sottoscrizioni di Azure][3]  
    <span data-ttu-id="31180-134">riquadro di sinistra Hello consente di visualizzare gli account di archiviazione hello associati alle sottoscrizioni Azure hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="31180-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Sottoscrizioni di Azure selezionate][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="31180-136">La connessione di sottoscrizione di Azure Stack tooan</span><span class="sxs-lookup"><span data-stu-id="31180-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="31180-137">Per informazioni sulla sottoscrizione di Azure Stack tooan connessione, vedere [tooan connettere Esplora archivi sottoscrizione Azure Stack](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="31180-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="31180-138">Utilizzare la risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="31180-138">Work with local development storage</span></span>
<span data-ttu-id="31180-139">Con Esplora risorse di archiviazione (anteprima), è possibile utilizzare nel servizio di archiviazione locale tramite hello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="31180-140">Questo approccio consente di scrivere codice in base e i test di archiviazione senza dover necessariamente un account di archiviazione distribuito in Azure, perché l'account di archiviazione hello è emulata da hello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="31180-141">Hello emulatore di archiviazione di Azure è attualmente supportata solo per Windows.</span><span class="sxs-lookup"><span data-stu-id="31180-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="31180-142">Nel riquadro sinistro di hello di esplorazione dell'archiviazione (anteprima), espandere hello **(locale e connesse)** > **gli account di archiviazione** > **(sviluppo)** nodo.</span><span class="sxs-lookup"><span data-stu-id="31180-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nodo di sviluppo locale][21]

2. <span data-ttu-id="31180-144">Se non è stato ancora installato hello emulatore di archiviazione Azure, si toodo richiesta in questo caso, tramite una barra informazioni.</span><span class="sxs-lookup"><span data-stu-id="31180-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="31180-145">Se viene visualizzata la barra informazioni hello, selezionare **versione più recente di Download hello**e quindi installare l'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="31180-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Richiesta di download dell'Emulatore di archiviazione di Azure][22]

3. <span data-ttu-id="31180-147">Dopo l'installazione dell'emulatore hello, è possibile creare e lavorare con le tabelle, code e BLOB locali.</span><span class="sxs-lookup"><span data-stu-id="31180-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="31180-148">toolearn come tipo toowork con ogni account di archiviazione, vedere uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="31180-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="31180-149">Gestire le risorse dell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="31180-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="31180-150">Manage Azure file share storage resources (Gestire risorse di condivisione file di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="31180-151">Manage Azure queue storage resources (Gestire risorse di archiviazione code di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="31180-152">Manage Azure table storage resources (Gestire risorse di archiviazione tabelle di Azure): *presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="31180-153">Collegare o scollegare un account di archiviazione esterno</span><span class="sxs-lookup"><span data-stu-id="31180-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="31180-154">Con Esplora risorse di archiviazione (anteprima), è possibile collegare gli account di archiviazione tooexternal in modo che gli account di archiviazione possono essere condivisa con facilità.</span><span class="sxs-lookup"><span data-stu-id="31180-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="31180-155">Questa sezione viene illustrato come tooattach too(and detach from) gli account di archiviazione esterno.</span><span class="sxs-lookup"><span data-stu-id="31180-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="31180-156">Ottenere le credenziali dell'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="31180-156">Get hello storage account credentials</span></span>
<span data-ttu-id="31180-157">tooshare un account di archiviazione esterno, proprietario hello di tale account deve innanzitutto ottenere credenziali hello (nome dell'account e la chiave) per conto di hello e quindi condividere le informazioni che richiede account toothat (esterna) tooattach persona hello.</span><span class="sxs-lookup"><span data-stu-id="31180-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="31180-158">È possibile ottenere le credenziali dell'account di archiviazione hello tramite hello portale di Azure eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="31180-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="31180-159">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31180-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="31180-160">Selezionare **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="31180-160">Select **Browse**.</span></span>

3. <span data-ttu-id="31180-161">Selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="31180-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="31180-162">In hello **gli account di archiviazione** blade, account di archiviazione selezionare hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="31180-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="31180-163">In hello **impostazioni** pannello hello selezionato di account di archiviazione, selezionare **le chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="31180-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Opzione Chiavi di accesso][5]

6. <span data-ttu-id="31180-165">In hello **le chiavi di accesso** blade, hello copia **nome account di archiviazione** e **key1** valori da utilizzare quando ci si connette toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31180-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Chiavi di accesso][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="31180-167">Collegare l'account di archiviazione esterno tooan</span><span class="sxs-lookup"><span data-stu-id="31180-167">Attach tooan external storage account</span></span>
<span data-ttu-id="31180-168">account di archiviazione esterno tooan tooattach, è necessario nome e la chiave dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="31180-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="31180-169">sezione "Get hello archiviazione le credenziali dell'account" Hello viene illustrato come questi valori da tooobtain hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="31180-170">Tuttavia, nel portale di hello, viene chiamata chiave dell'account hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="31180-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="31180-171">Pertanto, in Esplora archivi (anteprima) richiede una chiave dell'account, è immettere hello **key1** valore.</span><span class="sxs-lookup"><span data-stu-id="31180-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="31180-172">In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="31180-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opzione di archiviazione tooAzure di connessione][23]

2. <span data-ttu-id="31180-174">In hello **connettersi tooAzure archiviazione** finestra di dialogo, specificare una chiave dell'account di hello (hello **key1** valore dal portale di Azure hello), quindi selezionare **successivo**.</span><span class="sxs-lookup"><span data-stu-id="31180-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31180-175">È possibile immettere una stringa di connessione di archiviazione hello da un account di archiviazione in Azure nazionali.</span><span class="sxs-lookup"><span data-stu-id="31180-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="31180-176">Gli account di archiviazione Germania tooAzure tooconnect, ad esempio, immettere la seguente connessione stringhe simili toohello:</span><span class="sxs-lookup"><span data-stu-id="31180-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="31180-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="31180-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="31180-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="31180-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="31180-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="31180-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="31180-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="31180-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="31180-181">È possibile ottenere la stringa di connessione hello da hello Azure portale in hello stesso modo come descritto in hello sezione "Ottenere le credenziali dell'account di archiviazione hello".</span><span class="sxs-lookup"><span data-stu-id="31180-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. <span data-ttu-id="31180-183">In hello **collega archiviazione esterna** della finestra di dialogo hello **nome Account** , immettere il nome di account di archiviazione hello, specificare le altre impostazioni desiderate e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31180-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Finestra di dialogo Associa archiviazione esterna][8]

4. <span data-ttu-id="31180-185">In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="31180-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="31180-186">Se si desidera toochange qualsiasi valore diverso, selezionare **nuovamente** e immettere nuovamente le impostazioni di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="31180-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="31180-187">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="31180-187">Select **Connect**.</span></span>

6. <span data-ttu-id="31180-188">Una volta stabilita la connessione, l'account di archiviazione esterno hello viene visualizzato con **(esterna)** aggiunto toohello nome account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31180-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Risultato della connessione di account di archiviazione esterno tooan][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="31180-190">Scollegarsi da un account di archiviazione esterno</span><span class="sxs-lookup"><span data-stu-id="31180-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="31180-191">Fare doppio clic su account di archiviazione esterno hello desidera toodetach e quindi selezionare **scollegamento**.</span><span class="sxs-lookup"><span data-stu-id="31180-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Opzione per scollegarsi da un account di archiviazione][10]

2. <span data-ttu-id="31180-193">Nel messaggio di conferma hello, selezionare **Sì** la disconnessione di hello tooconfirm dall'account di archiviazione esterna hello.</span><span class="sxs-lookup"><span data-stu-id="31180-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="31180-194">Collegare un account di archiviazione usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="31180-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="31180-195">Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) consente di concedere l'account di archiviazione di un accesso temporaneo tooa senza credenziali di sottoscrizione di Azure tooprovide salve di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="31180-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="31180-196">tooillustrate questo scenario, si ad esempio che utente a è un amministratore di una sottoscrizione di Azure ed è UserA tooallow UserB tooaccess uno spazio di archiviazione dell'account per un periodo limitato con determinate autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="31180-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="31180-197">UserA genera una firma di accesso condiviso (costituito dalla stringa di connessione hello per account di archiviazione hello) per un'ora specifica periodo e con le autorizzazioni di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="31180-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="31180-198">Condivisioni UserA hello SAS con hello persona (in questo esempio UserB) richiede l'account di archiviazione toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="31180-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="31180-199">UserB utilizza Esplora archivi (Preview) tooattach toohello account appartiene tooUserA utilizzando hello fornito SAS.</span><span class="sxs-lookup"><span data-stu-id="31180-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="31180-200">Ottenere una firma di accesso condiviso per conto di hello desiderato tooshare</span><span class="sxs-lookup"><span data-stu-id="31180-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="31180-201">In Esplora archivi (anteprima), fare doppio clic su account di archiviazione hello da condividere e quindi selezionare **ottenere firma di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="31180-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Menu di scelta rapida Get SAS (Ottieni firma di accesso condiviso)][13]

2. <span data-ttu-id="31180-203">In hello **firma di accesso condiviso** finestra di dialogo, specificare l'intervallo di tempo hello e le autorizzazioni desiderate per l'account di hello e quindi selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="31180-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="31180-204">![Finestra di dialogo Get SAS][14] (Ottieni firma di accesso condiviso)</span><span class="sxs-lookup"><span data-stu-id="31180-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="31180-205">Hello **firma di accesso condiviso** la finestra di dialogo viene visualizzata e viene visualizzato hello SAS.</span><span class="sxs-lookup"><span data-stu-id="31180-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="31180-206">Toohello Avanti **stringa di connessione**, selezionare **copia** toocopy è toohello Appunti, quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="31180-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="31180-207">Associare account toohello condiviso utilizzando hello SAS</span><span class="sxs-lookup"><span data-stu-id="31180-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="31180-208">In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="31180-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opzione di archiviazione tooAzure di connessione][23]

2. <span data-ttu-id="31180-210">In hello **connettersi tooAzure archiviazione** la finestra di dialogo, specificare la stringa di connessione hello e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31180-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. <span data-ttu-id="31180-212">In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="31180-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="31180-213">modifiche toomake, selezionare **nuovamente**, quindi immettere impostazioni hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="31180-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="31180-214">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="31180-214">Select **Connect**.</span></span>

5. <span data-ttu-id="31180-215">Dopo la connessione, viene visualizzato l'account di archiviazione di hello con **(SAS)** aggiunto toohello nome dell'account specificate.</span><span class="sxs-lookup"><span data-stu-id="31180-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Risultato dell'account collegato tooan tramite firma di accesso condiviso][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="31180-217">Collegare un servizio usando la firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="31180-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="31180-218">sezione "Collegare un account di archiviazione tramite una firma di accesso condiviso" Hello viene illustrato come un amministratore della sottoscrizione di Azure può concedere l'account di archiviazione di un accesso temporaneo tooa mediante la generazione e la condivisione di una firma di accesso condiviso per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="31180-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="31180-219">È allo stesso modo possibile generare una firma di accesso condiviso per un servizio specifico, ovvero contenitore BLOB, coda o tabella, in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31180-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="31180-220">Generare una firma di accesso condiviso per il servizio di hello che si desidera tooshare</span><span class="sxs-lookup"><span data-stu-id="31180-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="31180-221">In questo contesto, un servizio può essere un contenitore BLOB, una coda o una tabella.</span><span class="sxs-lookup"><span data-stu-id="31180-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="31180-222">toogenerate hello firma di accesso condiviso per un servizio elencato, vedere:</span><span class="sxs-lookup"><span data-stu-id="31180-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="31180-223">Ottenere hello firma di accesso condiviso per un contenitore blob</span><span class="sxs-lookup"><span data-stu-id="31180-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="31180-224">Ottenere hello firma di accesso condiviso per una condivisione file: *sarà presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="31180-225">Ottenere hello firma di accesso condiviso per una coda: *sarà presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="31180-226">Ottenere hello firma di accesso condiviso per una tabella: *sarà presto disponibile*</span><span class="sxs-lookup"><span data-stu-id="31180-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="31180-227">Collegare toohello condiviso account di servizio utilizzando hello SAS</span><span class="sxs-lookup"><span data-stu-id="31180-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="31180-228">In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="31180-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opzione di archiviazione tooAzure di connessione][23]

2. <span data-ttu-id="31180-230">In hello **connettersi tooAzure archiviazione** nella finestra di dialogo specificare hello URI SAS e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="31180-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. <span data-ttu-id="31180-232">In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="31180-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="31180-233">modifiche toomake, selezionare **nuovamente**, quindi immettere impostazioni hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="31180-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="31180-234">Selezionare **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="31180-234">Select **Connect**.</span></span>

5. <span data-ttu-id="31180-235">Dopo la connessione, hello servizio appena collegato viene visualizzato in hello **(servizio SAS)** nodo.</span><span class="sxs-lookup"><span data-stu-id="31180-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Risultato dell'associazione servizio tooa condivisa tramite una firma di accesso condiviso][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="31180-237">Cercare gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="31180-237">Search for storage accounts</span></span>
<span data-ttu-id="31180-238">Se si dispone di un lungo elenco di account di archiviazione, toolocate un modo rapido un determinato account di archiviazione è casella di ricerca toouse hello nella parte superiore di hello del riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="31180-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="31180-239">Mentre si digita nella casella di ricerca hello, hello riquadro a sinistra consente di visualizzare hello account di archiviazione corrispondono hello valore di ricerca che immesso toothat un punto.</span><span class="sxs-lookup"><span data-stu-id="31180-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="31180-240">Ad esempio, una ricerca per gli account di archiviazione il cui nome contiene **tarcher** è illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="31180-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Ricerca dell'account di archiviazione][11]

## <a name="next-steps"></a><span data-ttu-id="31180-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31180-242">Next steps</span></span>
* [<span data-ttu-id="31180-243">Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="31180-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
