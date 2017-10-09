---
title: dati aaaMove - Gateway di gestione dati | Documenti Microsoft
description: Impostare un data gateway toomove di dati tra sedi locali e hello cloud. Usare Gateway di gestione dati in Azure Data Factory toomove i dati.
keywords: gateway dati, integrazione di dati, spostare dati, credenziali del gateway
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="3b91d-105">Spostare dati tra origini locali e cloud hello con Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="3b91d-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="3b91d-106">Questo articolo offre una panoramica sull'integrazione tra archivi dati locali e archivi dati cloud con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3b91d-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="3b91d-107">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo e altri articoli concetti principali di data factory: [set di dati](data-factory-create-datasets.md) e [pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3b91d-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="3b91d-108">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="3b91d-108">Data Management Gateway</span></span>
<span data-ttu-id="3b91d-109">È necessario installare il Gateway di gestione di dati nel tooenable macchina locale lo spostamento dei dati da e verso un archivio dati locale.</span><span class="sxs-lookup"><span data-stu-id="3b91d-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="3b91d-110">Hello gateway può essere installato su hello che stesso computer come archivio dati hello o in un computer diverso, purché il gateway di hello possa connettersi toohello archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b91d-111">Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="3b91d-112">Hello seguente procedura dettagliata illustra come una data factory con una pipeline che sposta i dati da una locale toocreate **SQL Server** database archivio blob di Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="3b91d-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="3b91d-113">Come parte della procedura dettagliata di hello, installare e configurare hello Gateway di gestione dati nel computer.</span><span class="sxs-lookup"><span data-stu-id="3b91d-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="3b91d-114">Procedura dettagliata: copiare toocloud dati locale</span><span class="sxs-lookup"><span data-stu-id="3b91d-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="3b91d-115">In questa procedura dettagliata hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="3b91d-116">Creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="3b91d-116">Create a data factory.</span></span>
2. <span data-ttu-id="3b91d-117">Creare un gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="3b91d-118">Creare servizi collegati per gli archivi dati di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="3b91d-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="3b91d-119">Creare set di dati toorepresent input e output dei dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="3b91d-120">Creare una pipeline con un copia attività toomove hello dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="3b91d-121">Prerequisiti per l'esercitazione hello</span><span class="sxs-lookup"><span data-stu-id="3b91d-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="3b91d-122">Prima di iniziare questa procedura dettagliata, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="3b91d-123">**Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-123">**Azure subscription**.</span></span>  <span data-ttu-id="3b91d-124">Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="3b91d-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3b91d-125">Vedere hello [versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="3b91d-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="3b91d-126">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-126">**Azure Storage Account**.</span></span> <span data-ttu-id="3b91d-127">Usare l'archiviazione di blob hello come un **destinazione/sink** archivio dati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3b91d-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="3b91d-128">Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="3b91d-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="3b91d-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-129">**SQL Server**.</span></span> <span data-ttu-id="3b91d-130">Usare un database di SQL Server locale come archivio dati di **origine** in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3b91d-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="3b91d-131">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="3b91d-131">Create data factory</span></span>
<span data-ttu-id="3b91d-132">In questo passaggio, si usa hello Azure toocreate portale un'istanza di Azure Data Factory denominato **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="3b91d-133">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b91d-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b91d-134">Fare clic su **+ Nuovo**, su **Intelligence e analisi** e quindi su **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nuovo->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="3b91d-136">In hello **nuova data factory** pagina, immettere **ADFTutorialOnPremDF** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="3b91d-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Aggiungere tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="3b91d-138">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="3b91d-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="3b91d-139">Se viene visualizzato l'errore hello: **"ADFTutorialOnPremDF" nome della Data factory non è disponibile**, modificare il nome di hello di hello data factory (ad esempio, yournameADFTutorialOnPremDF) e provare a creare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="3b91d-140">Durante l'esecuzione dei passaggi rimanenti in questa esercitazione usare questo nome anziché ADFTutorialOnPremDF.</span><span class="sxs-lookup"><span data-stu-id="3b91d-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="3b91d-141">nome Hello della hello data factory può essere registrato come un **DNS** nome nel futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="3b91d-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="3b91d-142">Seleziona hello **sottoscrizione di Azure** in cui si desidera hello data factory toobe creato.</span><span class="sxs-lookup"><span data-stu-id="3b91d-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="3b91d-143">Selezionare un **gruppo di risorse** esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="3b91d-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="3b91d-144">Per l'esercitazione hello, creare un gruppo di risorse denominato: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="3b91d-145">Fare clic su **crea** su hello **nuova data factory** pagina.</span><span class="sxs-lookup"><span data-stu-id="3b91d-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3b91d-146">le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="3b91d-147">Una volta completata la creazione, vedrai hello **Data Factory** pagina come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="3b91d-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Home page di Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="3b91d-149">Creare il gateway</span><span class="sxs-lookup"><span data-stu-id="3b91d-149">Create gateway</span></span>
1. <span data-ttu-id="3b91d-150">In hello **Data Factory** pagina, fare clic su **autore e distribuire** riquadro toolaunch hello **Editor** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Riquadro Creare e distribuire](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="3b91d-152">Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori** hello barra degli strumenti e quindi fare clic su **nuovo gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="3b91d-153">In alternativa, è possibile fare doppio clic **gateway dati** in hello visualizzazione struttura ad albero, quindi fare clic su **nuovo gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Nuovo gateway di dati nella barra degli strumenti](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="3b91d-155">In hello **crea** pagina, immettere **adftutorialgateway** per hello **nome**, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Pagina per la creazione del gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="3b91d-157">In questa procedura dettagliata, si crea gateway logico hello con un solo nodo (computer di Windows locale).</span><span class="sxs-lookup"><span data-stu-id="3b91d-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="3b91d-158">È possibile scalare orizzontalmente un gateway di gestione di dati mediante l'associazione di più computer locali con gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="3b91d-159">È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="3b91d-160">Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="3b91d-161">Per informazioni dettagliate, vedere l'articolo [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) (Gateway di gestione dati - Disponibilità elevata e scalabilità (anteprima).</span><span class="sxs-lookup"><span data-stu-id="3b91d-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="3b91d-162">In hello **configura** pagina, fare clic su **installare direttamente in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="3b91d-163">Questa azione Scarica il pacchetto di installazione hello per gateway hello, installa, configura e registra gateway hello computer hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="3b91d-164">Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="3b91d-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="3b91d-165">Se si utilizza Chrome, andare toohello [archivio web Chrome](https://chrome.google.com/webstore/), eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="3b91d-166">Hello stesso per Firefox (Installa componente aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="3b91d-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="3b91d-167">Fare clic su **Apri Menu** sulla barra degli strumenti hello (**tre linee orizzontali** nell'angolo superiore destro hello), fare clic su **componenti aggiuntivi**, eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle hello Estensioni di ClickOnce e installarlo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Gateway - Pagina Configura](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="3b91d-169">In questo modo è più semplice toodownload modo (un solo clic) hello, installare, configurare e registrare il gateway di hello in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="3b91d-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="3b91d-170">È possibile visualizzare hello **Gestione configurazione di Microsoft Data Management Gateway** applicazione è installata nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3b91d-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="3b91d-171">È anche possibile trovare hello eseguibile **ConfigManager.exe** nella cartella hello: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="3b91d-172">È anche possibile scaricare e installare il gateway manualmente utilizzando i collegamenti di hello in questa pagina e registrarlo con chiave hello indicata nella hello **nuova chiave** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="3b91d-173">Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per tutti i dettagli sul gateway hello di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b91d-174">È necessario essere un amministratore hello tooinstall di computer locale e configurare correttamente hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="3b91d-175">È possibile aggiungere altri utenti toohello **Data Management Gateway Users** gruppo locale di Windows.</span><span class="sxs-lookup"><span data-stu-id="3b91d-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="3b91d-176">membri di Hello di questo gruppo possono usare gateway di hello gestione di configurazione di Gateway di gestione dati strumento tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="3b91d-177">Attendere un paio di minuti o attendere fino a visualizzare hello seguente messaggio di notifica:</span><span class="sxs-lookup"><span data-stu-id="3b91d-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Installazione del gateway riuscita](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="3b91d-179">Avviare l'applicazione **Gateway di gestione dati di Configuration Manager** nel computer.</span><span class="sxs-lookup"><span data-stu-id="3b91d-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="3b91d-180">In hello **ricerca** finestra **Gateway di gestione dati** tooaccess questo utilità.</span><span class="sxs-lookup"><span data-stu-id="3b91d-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="3b91d-181">È anche possibile trovare hello eseguibile **ConfigManager.exe** nella cartella hello: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="3b91d-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gestione configurazione di gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="3b91d-183">Verificare che venga visualizzato il messaggio `adftutorialgateway is connected toohello cloud service`.</span><span class="sxs-lookup"><span data-stu-id="3b91d-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="3b91d-184">Consente di visualizzare hello nella parte inferiore della barra di stato Hello **toohello cloud servizio connesso** insieme a un **segno di spunta verde**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="3b91d-185">In hello **Home** scheda, è inoltre possibile eseguire hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="3b91d-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="3b91d-186">**Registrare** un gateway con una chiave dal portale di Azure usando il pulsante Registro hello hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="3b91d-187">**Arrestare** hello Gateway Host servizio di gestione dati in esecuzione nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="3b91d-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="3b91d-188">**Pianificare gli aggiornamenti** toobe installato in un momento specifico del giorno hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="3b91d-189">Verificare quando è stato gateway hello **ultimo aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="3b91d-190">Specificare l'ora in cui è possibile installare un gateway toohello di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3b91d-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="3b91d-191">Passare toohello **impostazioni** scheda hello certificato hello **certificato** sezione è costituita dalle credenziali tooencrypt/decrittografia utilizzati per l'archivio di dati locale hello specificato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="3b91d-192">(facoltativo) Fare clic su **modifica** toouse il proprio certificato invece.</span><span class="sxs-lookup"><span data-stu-id="3b91d-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="3b91d-193">Per impostazione predefinita, il gateway hello utilizza certificato hello è generato automaticamente da hello servizio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3b91d-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Configurazione certificati del gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="3b91d-195">È inoltre possibile eseguire hello le azioni seguenti sulla hello **impostazioni** scheda:</span><span class="sxs-lookup"><span data-stu-id="3b91d-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="3b91d-196">Consente di visualizzare o esportare il certificato di hello usato dal gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="3b91d-197">Modificare l'endpoint HTTPS hello usati dal gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="3b91d-198">Impostare un toobe proxy HTTP utilizzato dal gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="3b91d-199">(facoltativo) Passare toohello **diagnostica** scheda, controllare hello **abilitare la registrazione dettagliata** opzione se si desidera la registrazione che è possibile utilizzare tootroubleshoot eventuali problemi con il gateway hello dettagliata tooenable.</span><span class="sxs-lookup"><span data-stu-id="3b91d-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="3b91d-200">Hello informazioni di registrazione possono trovarsi **Visualizzatore eventi** in **registri applicazioni e servizi** -> **Gateway di gestione dati** nodo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Scheda Diagnostica](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="3b91d-202">È inoltre possibile eseguire dopo le azioni in hello hello **diagnostica** scheda:</span><span class="sxs-lookup"><span data-stu-id="3b91d-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="3b91d-203">Utilizzare **Test connessione** origine dati locale tooan sezione usando hello gateway.</span><span class="sxs-lookup"><span data-stu-id="3b91d-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="3b91d-204">Fare clic su **Visualizza log** toosee hello Gateway di gestione dati di log in una finestra del Visualizzatore eventi.</span><span class="sxs-lookup"><span data-stu-id="3b91d-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="3b91d-205">Fare clic su **inviare i log** tooupload un file zip con log di ultimi sette giorni tooMicrosoft toofacilitate risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3b91d-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="3b91d-206">In hello **diagnostica** scheda hello **Test connessione** selezionare **SqlServer** per tipo hello hello dati archivio, immettere il nome di hello hello del server di database, nome del Hello database, specificare il tipo di autenticazione, immettere nome utente e password e fare clic su **Test** tootest se gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="3b91d-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="3b91d-207">Browser web toohello di commutatore e in hello **portale di Azure**, fare clic su **OK** su hello **configura** pagina e quindi su hello **nuovo gateway dati** pagina.</span><span class="sxs-lookup"><span data-stu-id="3b91d-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="3b91d-208">Dovrebbe essere **adftutorialgateway** in **gateway dati** nella visualizzazione ad albero di hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="3b91d-209">Se è selezionata, verrà visualizzato hello associata JSON.</span><span class="sxs-lookup"><span data-stu-id="3b91d-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="3b91d-210">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="3b91d-210">Create linked services</span></span>
<span data-ttu-id="3b91d-211">In questo passaggio vengono creati due servizi collegati: **AzureStorageLinkedService** e **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="3b91d-212">Hello **SqlServerLinkedService** collega un database di SQL Server locale e hello **AzureStorageLinkedService** servizio collegato collega una data factory di toohello archivio blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b91d-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="3b91d-213">Una pipeline viene creata più avanti in questa procedura dettagliata che copia i dati dal database SQL Server on-premise di hello toohello archivio di blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b91d-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="3b91d-214">Aggiungere un database di SQL Server on-premise tooan servizio collegato</span><span class="sxs-lookup"><span data-stu-id="3b91d-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="3b91d-215">In hello **Editor delle Data Factory**, fare clic su **nuovo archivio dati** sulla barra degli strumenti hello e selezionare **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Nuovo servizio collegato di SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="3b91d-217">In hello **editor JSON** su hello destra, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="3b91d-218">Per hello **gatewayName**, specificare **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="3b91d-219">In hello **connectionString**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="3b91d-220">Per **servername**, immettere il nome di hello del server di hello che ospita il database di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="3b91d-221">Per **databasename**, immettere il nome di hello del database di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="3b91d-222">Fare clic su **Encrypt** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="3b91d-223">Viene visualizzata l'applicazione di gestione credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-223">You see hello Credentials Manager application.</span></span>

         ![Applicazione Gestione credenziali](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="3b91d-225">In hello **impostazione delle credenziali** la finestra di dialogo, specificare il tipo di autenticazione, nome utente e password e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="3b91d-226">Se la connessione hello ha esito positivo, crittografato hello credenziali vengono archiviate in hello JSON e chiude la finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="3b91d-227">Chiudere scheda del browser vuota hello avviata la finestra di dialogo hello se non viene chiuso automaticamente e tornare scheda toohello con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b91d-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="3b91d-228">Nel computer gateway hello, queste credenziali sono **crittografati** proprietario di servizio utilizzando un certificato che hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3b91d-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="3b91d-229">Se si desidera certificato hello toouse viene invece associato hello Gateway di gestione dati, vedere [impostare in modo sicuro le credenziali](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="3b91d-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="3b91d-230">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello servizio collegato SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b91d-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="3b91d-231">Verrà visualizzato il servizio collegato hello nella visualizzazione ad albero di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-231">You should see hello linked service in hello tree view.</span></span>

      ![Servizio collegato SQL Server nella visualizzazione ad albero hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="3b91d-233">Aggiungere un servizio collegato per un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3b91d-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="3b91d-234">In hello **Editor delle Data Factory**, fare clic su **nuovo archivio dati** hello barra dei comandi e fare clic su **archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="3b91d-235">Immettere nome hello dell'account di archiviazione di Azure per hello **nome Account**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="3b91d-236">Immettere la chiave hello per l'account di archiviazione di Azure per hello **chiave dell'Account**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="3b91d-237">Fare clic su **Distribuisci** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="3b91d-238">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="3b91d-238">Create datasets</span></span>
<span data-ttu-id="3b91d-239">In questo passaggio, creare input e output di set di dati che rappresentano i dati di input e outpui per l'operazione di copia hello (database di SQL Server in locale = > archiviazione blob di Azure).</span><span class="sxs-lookup"><span data-stu-id="3b91d-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="3b91d-240">Prima di creare set di dati, hello (procedura dettagliata seguente elenco hello) come segue:</span><span class="sxs-lookup"><span data-stu-id="3b91d-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="3b91d-241">Creare una tabella denominata **emp** in Database di SQL Server è stato aggiunto come una data factory di servizio collegato toohello hello e inserire un paio di voci di esempio nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="3b91d-242">Creare un contenitore blob denominato **adftutorial** in hello Azure blob account di archiviazione è stato aggiunto come una data factory toohello servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="3b91d-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="3b91d-243">Preparare il Server SQL locale hello esercitazione</span><span class="sxs-lookup"><span data-stu-id="3b91d-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="3b91d-244">Nel database di hello specificata per hello on-premise SQL Server il servizio collegato (**SqlServerLinkedService**), utilizzare hello hello toocreate di script SQL seguente **emp** tabella nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="3b91d-245">Inserire un punto qualsiasi nella tabella di hello:</span><span class="sxs-lookup"><span data-stu-id="3b91d-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="3b91d-246">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="3b91d-246">Create input dataset</span></span>

1. <span data-ttu-id="3b91d-247">In hello **Editor delle Data Factory**, fare clic su **... Ulteriori**, fare clic su **nuovo set di dati** hello barra dei comandi e fare clic su **tabella di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="3b91d-248">Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="3b91d-248">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="3b91d-249">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-249">Note hello following points:</span></span>

   * <span data-ttu-id="3b91d-250">**tipo** è troppo**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="3b91d-251">**tableName** è troppo**emp**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="3b91d-252">**linkedServiceName** è troppo**SqlServerLinkedService** (è stato creato questo servizio collegato in precedenza in questa procedura dettagliata.).</span><span class="sxs-lookup"><span data-stu-id="3b91d-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="3b91d-253">Per un set di dati input che non viene generato da un'altra pipeline nella Data Factory di Azure, è necessario impostare **esterno** troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="3b91d-254">Indica i dati di input hello sono prodotto toohello esterno, il servizio Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b91d-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="3b91d-255">È possibile specificare i criteri di dati esterni tramite hello **externalData** elemento hello **criteri** sezione.</span><span class="sxs-lookup"><span data-stu-id="3b91d-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="3b91d-256">Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="3b91d-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="3b91d-257">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="3b91d-258">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="3b91d-258">Create output dataset</span></span>

1. <span data-ttu-id="3b91d-259">In hello **Editor delle Data Factory**, fare clic su **nuovo set di dati** hello barra dei comandi e fare clic su **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="3b91d-260">Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="3b91d-260">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="3b91d-261">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-261">Note hello following points:</span></span>

   * <span data-ttu-id="3b91d-262">**tipo** è troppo**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="3b91d-263">**linkedServiceName** è troppo**AzureStorageLinkedService** (nel passaggio 2 è stato creato questo servizio collegato).</span><span class="sxs-lookup"><span data-stu-id="3b91d-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="3b91d-264">**folderPath** è troppo**adftutorial/outfromonpremdf** dove outfromonpremdf è la cartella hello nel contenitore adftutorial hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="3b91d-265">Creare hello **adftutorial** contenitore se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="3b91d-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="3b91d-266">Hello **disponibilità** è troppo**oraria** (**frequenza** impostare troppo**ora** e **intervallo** impostare troppo **1**).</span><span class="sxs-lookup"><span data-stu-id="3b91d-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="3b91d-267">servizio Data Factory Hello genera una sezione di dati di output ogni ora in hello **emp** tabella nel Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="3b91d-268">Se non si specifica un **fileName** per un **tabella di output**, i file generato hello in hello **folderPath** indicati nel seguente formato hello: dati.<Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="3b91d-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="3b91d-269">tooset **folderPath** e **fileName** in modo dinamico in base a hello **SliceStart** tempo, utilizzare proprietà partitionedBy hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="3b91d-270">Nell'esempio seguente di hello, folderPath Usa anno, mese e giorno da hello SliceStart (ora di inizio della sezione hello in fase di elaborazione) e nome file utilizza ora da hello SliceStart.</span><span class="sxs-lookup"><span data-stu-id="3b91d-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="3b91d-271">Ad esempio, se viene viene prodotta una sezione per 2014-10-20T08:00:00, folderName hello è impostato toowikidatagateway/wikisampledataout/2014/10/20 e hello fileName è impostato too08.csv.</span><span class="sxs-lookup"><span data-stu-id="3b91d-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="3b91d-272">Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso l'archivio BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="3b91d-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="3b91d-273">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="3b91d-274">Assicurarsi di visualizzare i set di dati sia hello nella visualizzazione ad albero di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="3b91d-275">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="3b91d-275">Create pipeline</span></span>
<span data-ttu-id="3b91d-276">In questo passaggio viene creata una **pipeline** con un'**attività di copia** che usa **EmpOnPremSQLTable** come input e **OutputBlobTable** come output.</span><span class="sxs-lookup"><span data-stu-id="3b91d-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="3b91d-277">Nell'editor di Data Factory fare clic su **... Altro** e quindi su **Nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="3b91d-278">Sostituire hello JSON nel riquadro di destra hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="3b91d-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="3b91d-279">Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="3b91d-280">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="3b91d-280">Note hello following points:</span></span>

   * <span data-ttu-id="3b91d-281">Nella sezione attività hello è solo l'attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="3b91d-282">**Input** per attività hello è troppo**EmpOnPremSQLTable** e **output** per attività hello è troppo**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="3b91d-283">In hello **typeProperties** sezione **SqlSource** è specificato come hello **tipo di origine** e * * BlobSink * * è specificato come hello **tipodisink**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="3b91d-284">Query SQL `select * from emp` specificato per hello **sqlReaderQuery** proprietà di **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="3b91d-285">Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="3b91d-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="3b91d-286">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="3b91d-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="3b91d-287">Hello **fine** è facoltativo, ma viene usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3b91d-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="3b91d-288">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**".</span><span class="sxs-lookup"><span data-stu-id="3b91d-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="3b91d-289">specificare in modo indefinito, pipeline hello toorun **9/9/9999** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="3b91d-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="3b91d-290">Si sta definendo il periodo di tempo in cui hello vengono elaborate le sezioni di dati in base a hello hello **disponibilità** proprietà che sono state definite per ogni set di dati di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3b91d-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="3b91d-291">Nell'esempio hello, esistono 24 sezioni di dati come ogni sezione di dati viene prodotta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3b91d-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="3b91d-292">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello dataset (la tabella è un set di dati rettangolare).</span><span class="sxs-lookup"><span data-stu-id="3b91d-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="3b91d-293">Confermare che pipeline hello viene visualizzato nella visualizzazione struttura ad albero di hello in **pipeline** nodo.</span><span class="sxs-lookup"><span data-stu-id="3b91d-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="3b91d-294">A questo punto, fare clic su **X** due volte tooclose hello pagina tooget indietro toohello **Data Factory** pagina per hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="3b91d-295">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="3b91d-295">**Congratulations!**</span></span> <span data-ttu-id="3b91d-296">Creazione completata una data factory di Azure, servizi collegati, i set di dati e una pipeline e pipeline hello pianificato.</span><span class="sxs-lookup"><span data-stu-id="3b91d-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="3b91d-297">Data factory di visualizzazione hello in una vista diagramma</span><span class="sxs-lookup"><span data-stu-id="3b91d-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="3b91d-298">In hello **portale di Azure**, fare clic su **diagramma** riquadro hello home page di hello **ADFTutorialOnPremDF** factory di dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="3b91d-299">:</span><span class="sxs-lookup"><span data-stu-id="3b91d-299">:</span></span>

    ![Collegamento al diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="3b91d-301">Dovrebbe essere simile toohello diagramma hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="3b91d-301">You should see hello diagram similar toohello following image:</span></span>

    ![Vista Diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="3b91d-303">È possibile eseguire lo zoom avanti, eseguire lo zoom indietro, zoom too100%, toofit zoom, automaticamente le pipeline di posizione e i set di dati e visualizzare le informazioni di derivazione (evidenzia gli elementi a monte e a valle degli elementi selezionati).</span><span class="sxs-lookup"><span data-stu-id="3b91d-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="3b91d-304">È possibile fare doppio clic su una proprietà toosee dell'oggetto (set di dati di input/output o pipeline) per tale.</span><span class="sxs-lookup"><span data-stu-id="3b91d-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="3b91d-305">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="3b91d-305">Monitor pipeline</span></span>
<span data-ttu-id="3b91d-306">In questo passaggio, utilizzare hello Azure toomonitor portale cosa accade in un data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b91d-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="3b91d-307">È anche possibile utilizzare le pipeline e set di dati toomonitor cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b91d-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="3b91d-308">Per altre informazioni sul monitoraggio, vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3b91d-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="3b91d-309">Nel diagramma hello, fare doppio clic su **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Sezioni EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="3b91d-311">Si noti che tutti i dati di hello seziona backup sono **pronto** stato perché la durata della pipeline hello (ora di inizio ora tooend) si trova in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="3b91d-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="3b91d-312">È inoltre perché è stato inserito dati hello nel database di SQL Server hello e è presente tutto il tempo hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="3b91d-313">Verificare che non sono presenti sezioni visualizzati in hello **sezioni problema** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="3b91d-314">Fare clic su tutte le sezioni, hello tooview **vedere più** nella parte inferiore di hello dell'elenco di hello di sezioni.</span><span class="sxs-lookup"><span data-stu-id="3b91d-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="3b91d-315">A questo punto, In hello **set di dati** pagina, fare clic su **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Sezioni OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="3b91d-317">Fare clic su qualsiasi sezione di dati dall'elenco hello e dovrebbe essere hello **sezione dati** pagina.</span><span class="sxs-lookup"><span data-stu-id="3b91d-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="3b91d-318">Viene visualizzato l'attività viene eseguita per sezione hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="3b91d-319">In genere viene visualizzata una sola esecuzione di attività.</span><span class="sxs-lookup"><span data-stu-id="3b91d-319">You see only one activity run usually.</span></span>  

    ![Pannello Sezione dati](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="3b91d-321">Se la sezione hello non hello **pronto** stato, è possibile vedere le sezioni upstream hello che non sono pronti e bloccano l'intervallo corrente di hello l'esecuzione in hello **sezioni Upstream non pronte** elenco.</span><span class="sxs-lookup"><span data-stu-id="3b91d-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="3b91d-322">Fare clic su hello **esecuzione dell'attività** dall'elenco hello hello inferiore toosee **Dettagli esecuzione attività**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Pagina Dettagli esecuzione attività](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="3b91d-324">Ad esempio la velocità effettiva, la durata e gateway hello utilizzati dati hello tootransfer, si vedrà informazioni.</span><span class="sxs-lookup"><span data-stu-id="3b91d-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="3b91d-325">Fare clic su **X** tooclose tutti hello pagine fino a</span><span class="sxs-lookup"><span data-stu-id="3b91d-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="3b91d-326">tornare home page di toohello per hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="3b91d-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="3b91d-327">(Facoltativo) Fare clic su **Pipeline** e su **ADFTutorialOnPremDF**, quindi eseguire il drill-through delle tabelle di input (**utilizzate**) o dei set di dati di output (**generati**).</span><span class="sxs-lookup"><span data-stu-id="3b91d-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="3b91d-328">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) tooverify che viene creato un blob o file per ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3b91d-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Azure Storage Explorer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="3b91d-330">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b91d-330">Next steps</span></span>
* <span data-ttu-id="3b91d-331">Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per tutti i dettagli sul Gateway di gestione dati hello di hello.</span><span class="sxs-lookup"><span data-stu-id="3b91d-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="3b91d-332">Vedere [copiare i dati da Blob di Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn su come dati di toomove toouse attività di copia da un'origine archiviano tooa sink dati.</span><span class="sxs-lookup"><span data-stu-id="3b91d-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
