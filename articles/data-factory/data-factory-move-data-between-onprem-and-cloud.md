---
title: Spostare dati con Gateway di gestione dati | Microsoft Docs
description: Configurare un gateway dati per spostare dati tra origini locali e il cloud. Usare Gateway di gestione dati in Azure Data Factory per spostare dati.
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
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="8fb7f-105">Spostare dati tra origini locali e il cloud con Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="8fb7f-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="8fb7f-106">Questo articolo offre una panoramica sull'integrazione tra archivi dati locali e archivi dati cloud con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="8fb7f-107">Si basa sull'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) e su altri articoli che illustrano i concetti di base relativi a Data Factory: [set di dati](data-factory-create-datasets.md) e [pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="8fb7f-108">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="8fb7f-108">Data Management Gateway</span></span>
<span data-ttu-id="8fb7f-109">È necessario installare il Gateway di gestione di dati sul computer locale per abilitare lo spostamento dei dati a/da un archivio dati locale.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="8fb7f-110">Il gateway può essere installato sullo stesso computer dell'archivio dati o su un computer diverso purché il gateway possa connettersi all'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fb7f-111">Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="8fb7f-112">Questa procedura dettagliata illustra come creare un'istanza di Data Factory con una pipeline che sposta i dati da un database di **SQL Server** locale a un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="8fb7f-113">Come parte della procedura dettagliata, viene installato e configurato il gateway di gestione dati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="8fb7f-114">Procedura dettagliata: Copiare i dati locali nel cloud</span><span class="sxs-lookup"><span data-stu-id="8fb7f-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="8fb7f-115">In questa procedura dettagliata si eseguiranno i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="8fb7f-116">Creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-116">Create a data factory.</span></span>
2. <span data-ttu-id="8fb7f-117">Creare un gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="8fb7f-118">Creare servizi collegati per gli archivi dati di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="8fb7f-119">Creare set di dati per rappresentare i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="8fb7f-120">Creare una pipeline con attività di copia per trasferire i dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="8fb7f-121">Prerequisiti per l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8fb7f-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="8fb7f-122">Prima di iniziare questa procedura dettagliata, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="8fb7f-123">**Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-123">**Azure subscription**.</span></span>  <span data-ttu-id="8fb7f-124">Se non è disponibile una sottoscrizione, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8fb7f-125">Per informazioni dettagliate, vedere l'articolo [Versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/) .</span><span class="sxs-lookup"><span data-stu-id="8fb7f-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="8fb7f-126">**Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-126">**Azure Storage Account**.</span></span> <span data-ttu-id="8fb7f-127">In questa esercitazione l'archiviazione BLOB viene usata come archivio dati di **destinazione/sink**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="8fb7f-128">Se non si ha un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) per informazioni su come crearne uno.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="8fb7f-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-129">**SQL Server**.</span></span> <span data-ttu-id="8fb7f-130">Usare un database di SQL Server locale come archivio dati di **origine** in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="8fb7f-131">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="8fb7f-131">Create data factory</span></span>
<span data-ttu-id="8fb7f-132">In questo passaggio si usa il portale di Azure per creare un'istanza di Azure Data Factory denominata **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="8fb7f-133">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fb7f-134">Fare clic su **+ Nuovo**, su **Intelligence e analisi** e quindi su **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nuovo->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="8fb7f-136">Nella pagina **Nuova data factory** immettere **ADFTutorialOnPremDF** come nome.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Aggiungi a schermata iniziale](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="8fb7f-138">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="8fb7f-139">Se viene visualizzato un errore simile a **Nome "ADFTutorialOnPremDF" per la data factory non disponibile**, cambiare il nome della data factory (ad esempio, nomeutenteADFTutorialOnPremDF) e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="8fb7f-140">Durante l'esecuzione dei passaggi rimanenti in questa esercitazione usare questo nome anziché ADFTutorialOnPremDF.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="8fb7f-141">Il nome della data factory può essere registrato in futuro come nome **DNS** e diventare quindi visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="8fb7f-142">Selezionare la **sottoscrizione di Azure** in cui creare la data factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="8fb7f-143">Selezionare un **gruppo di risorse** esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="8fb7f-144">Per l'esercitazione creare un gruppo di risorse denominato **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="8fb7f-145">Fare clic su **Crea** nella pagina **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8fb7f-146">Per creare istanze di data factory, è necessario essere membri del ruolo [Collaboratore Data factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) a livello di sottoscrizione/gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="8fb7f-147">Al termine della creazione viene visualizzata la pagina **Data Factory**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Home page di Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="8fb7f-149">Creare il gateway</span><span class="sxs-lookup"><span data-stu-id="8fb7f-149">Create gateway</span></span>
1. <span data-ttu-id="8fb7f-150">Nella pagina **Data Factory** fare clic sul riquadro **Creare e distribuire** per avviare l'**Editor** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Riquadro Creare e distribuire](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="8fb7f-152">Nell'editor di Data Factory fare clic su **... Altro** sulla barra degli strumenti e quindi fare clic su **Nuovo gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="8fb7f-153">In alternativa, è possibile fare clic con il pulsante destro del mouse su **Gateway dati** nella visualizzazione ad albero e fare clic su **Nuovo gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Nuovo gateway di dati nella barra degli strumenti](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="8fb7f-155">Nella pagina **Crea** immettere **adftutorialgateway** per il **nome** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Pagina per la creazione del gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="8fb7f-157">In questa procedura dettagliata si crea il gateway logico con un solo nodo, ossia un computer Windows locale.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="8fb7f-158">È possibile scalare orizzontalmente un gateway di gestione dati mediante l'associazione di più computer locali con il gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="8fb7f-159">È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="8fb7f-160">Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="8fb7f-161">Per informazioni dettagliate, vedere l'articolo [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) (Gateway di gestione dati - Disponibilità elevata e scalabilità (anteprima).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="8fb7f-162">Nella pagina **Configura** fare clic su **Installa direttamente nel computer**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="8fb7f-163">Con questa azione viene scaricato il pacchetto di installazione per il gateway, che viene installato, configurato e registrato nel computer.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="8fb7f-164">Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="8fb7f-165">Se si usa Chrome, accedere al [Chrome Web Store](https://chrome.google.com/webstore/), eseguire una ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni ClickOnce e installarla.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="8fb7f-166">Seguire la stessa procedura per Firefox (installazione di un componente aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="8fb7f-167">Fare clic sul pulsante **Apri menu** sulla barra degli strumenti (**tre righe orizzontali** nell'angolo superiore destro), fare clic su **Componenti aggiuntivi**, eseguire una ricerca con la parola chiave "ClickOnce", scegliere un'estensione ClickOnce e installarla.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Gateway - Pagina Configura](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="8fb7f-169">Si tratta del metodo più semplice (con un clic) per scaricare, installare, configurare e registrare il gateway in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="8fb7f-170">È possibile vedere l'applicazione **Gateway di gestione dati di Microsoft Configuration Manager** installata nel computer.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="8fb7f-171">È anche possibile trovare l'eseguibile **ConfigManager.exe** nella cartella: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="8fb7f-172">È anche possibile scaricare e installare manualmente il gateway usando i collegamenti nella pagina e registrarlo usando la chiave visualizzata nella casella di testo **NUOVA CHIAVE**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="8fb7f-173">Leggere l’articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per tutti i dettagli sul gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8fb7f-174">È necessario essere un amministratore nel computer locale per installare e configurare correttamente il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="8fb7f-175">È possibile aggiungere altri utenti al gruppo di Windows locale degli **utenti del gateway di gestione dati** .</span><span class="sxs-lookup"><span data-stu-id="8fb7f-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="8fb7f-176">I membri di questo gruppo possono usare lo strumento Gestione configurazione del gateway di gestione dati per configurare il gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="8fb7f-177">Attendere qualche minuto o finché non viene visualizzato il messaggio di notifica seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Installazione del gateway riuscita](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="8fb7f-179">Avviare l'applicazione **Gateway di gestione dati di Configuration Manager** nel computer.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="8fb7f-180">Nella finestra **Cerca** digitare **Gateway di gestione dati** per accedere a questa utilità.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="8fb7f-181">È anche possibile trovare l'eseguibile **ConfigManager.exe** nella cartella: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="8fb7f-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gestione configurazione di gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="8fb7f-183">Verificare che venga visualizzato il messaggio `adftutorialgateway is connected to the cloud service`.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="8fb7f-184">La barra di stato visualizza **Connesso al servizio cloud** insieme a un **segno di spunta verde**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="8fb7f-185">Nella scheda **Home** è anche possibile eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="8fb7f-186">**Registrare** un gateway con una chiave dal portale di Azure usando il pulsante Registra.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="8fb7f-187">**Interrompere** il servizio host del gateway di gestione dati in esecuzione nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="8fb7f-188">**Pianificare gli aggiornamenti** in modo che vengano installati in un preciso momento della giornata.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="8fb7f-189">Visualizzare la data dell'**ultimo aggiornamento** del gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="8fb7f-190">Specificare l'ora in cui è possibile installare un aggiornamento per il gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="8fb7f-191">Passare alla scheda **Impostazioni** . Il certificato specificato nella sezione **Certificato** viene usato per crittografare e decrittografare le credenziali per l'archivio dati locale specificato nel portale (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="8fb7f-192">Fare clic su **Modifica** per usare il proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="8fb7f-193">Per impostazione predefinita, il gateway usa il certificato generato automaticamente dal servizio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Configurazione certificati del gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="8fb7f-195">È anche possibile eseguire queste azioni nella scheda **Impostazioni**:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="8fb7f-196">Visualizzare o esportare il certificato usato dal gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="8fb7f-197">Modificare l'endpoint HTTPS usato dal gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="8fb7f-198">Impostare un proxy HTTP che verrà usato dal gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="8fb7f-199">(facoltativo) Passare alla scheda **Diagnostica**, selezionare l'opzione **Abilita la registrazione dettagliata** se si vuole abilitare la registrazione dettagliata che è possibile usare per risolvere i problemi del gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="8fb7f-200">Le informazioni sulla registrazione si trovano nel **Visualizzatore eventi**, nel nodo **Registri applicazioni e servizi** -> **Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Scheda Diagnostica](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="8fb7f-202">È inoltre possibile eseguire le azioni seguenti nella scheda **Diagnostica** :</span><span class="sxs-lookup"><span data-stu-id="8fb7f-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="8fb7f-203">Usare la sezione **Connessione di test** su un'origine dati locale con il gateway.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="8fb7f-204">Fare clic su **Visualizza registri** per vedere il registro del gateway di gestione dati in una finestra del Visualizzatore eventi.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="8fb7f-205">Fare clic su **Invia registri** per caricare un file zip dei registri degli ultimi sette giorni sul sito Microsoft al fine di facilitare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="8fb7f-206">Nella scheda **Diagnostica**, nella sezione **Test connessione** selezionare **SqlServer** come tipo di archivio dati, immettere il nome del server di database, il nome del database, specificare il tipo di autenticazione, immettere il nome utente e la password e fare clic su **Test** per verificare se il gateway può connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="8fb7f-207">Passare al Web browser e nel **portale di Azure** fare clic su **OK** nella pagina **Configura** e quindi nella pagina **Nuovo gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="8fb7f-208">Verrà visualizzato **adftutorialgateway** in **Gateway dati** nella visualizzazione albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="8fb7f-209">Se si fa clic, viene visualizzato l'oggetto JSON associato.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="8fb7f-210">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="8fb7f-210">Create linked services</span></span>
<span data-ttu-id="8fb7f-211">In questo passaggio vengono creati due servizi collegati: **AzureStorageLinkedService** e **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="8fb7f-212">Il servizio **SqlServerLinkedService** collega un database SQL Server locale, mentre il servizio collegato **AzureStorageLinkedService** collega un'archiviazione BLOB di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="8fb7f-213">Più avanti nella procedura dettagliata viene creata una pipeline che copia i dati dal database SQL Server locale all'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="8fb7f-214">Aggiungere un servizio collegato a un database di SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="8fb7f-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="8fb7f-215">Nell'**editor di Data Factory** fare clic su **Nuovo archivio dati** sulla barra degli strumenti e selezionare **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Nuovo servizio collegato di SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="8fb7f-217">Nell'**editor JSON** a destra seguire a questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="8fb7f-218">Per **gatewayName** specificare **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="8fb7f-219">In **connectionString** seguire a questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="8fb7f-220">Per **servername** immettere il nome del server che ospita il database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="8fb7f-221">Per **databasename** immettere il nome del database.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="8fb7f-222">Fare clic sul pulsante **Crittografa** sulla barra dei comandi</span><span class="sxs-lookup"><span data-stu-id="8fb7f-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="8fb7f-223">Viene visualizzata l'applicazione Gestione credenziali.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-223">You see the Credentials Manager application.</span></span>

         ![Applicazione Gestione credenziali](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="8fb7f-225">Nella finestra di dialogo **Impostazione credenziali** specificare il tipo di autenticazione, il nome utente e la password e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="8fb7f-226">Se la connessione viene stabilita correttamente, le credenziali crittografate vengono archiviate nel file JSON e la finestra di dialogo si chiude.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="8fb7f-227">Chiudere la scheda del browser vuota usata per avviare la finestra di dialogo se non viene chiusa automaticamente e tornare alla scheda con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="8fb7f-228">Nel computer gateway queste credenziali vengono **crittografate** con un certificato di proprietà del servizio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="8fb7f-229">Se invece si intende usare il certificato associato al gateway di gestione dati, vedere le informazioni su come [impostare le credenziali in modo sicuro](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="8fb7f-230">Fare clic su **Distribuisci** nella barra dei comandi per distribuire il servizio collegato di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="8fb7f-231">Verrà visualizzato il servizio collegato nella visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-231">You should see the linked service in the tree view.</span></span>

      ![Servizio collegato SQL Server nella visualizzazione albero](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="8fb7f-233">Aggiungere un servizio collegato per un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8fb7f-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="8fb7f-234">Nell'**editor di Data factory** fare clic su **Nuovo archivio dati** nella barra dei comandi e quindi su **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="8fb7f-235">Nel campo **Nome account**immettere il nome dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="8fb7f-236">Nel campo **Chiave account**immettere la chiave per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="8fb7f-237">Fare clic su **Distribuisci** per distribuire **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="8fb7f-238">Creare i set di dati</span><span class="sxs-lookup"><span data-stu-id="8fb7f-238">Create datasets</span></span>
<span data-ttu-id="8fb7f-239">In questo passaggio vengono creati i set di dati di input e di output che rappresentano i dati di input e di output per l'operazione di copia (database SQL Server locale => archiviazione BLOB di Azure).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="8fb7f-240">Prima di creare i set di dati, eseguire questa procedura (la procedura dettagliata segue l'elenco):</span><span class="sxs-lookup"><span data-stu-id="8fb7f-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="8fb7f-241">Creare una tabella denominata **emp** nel database SQL Server aggiunto come servizio collegato all'istanza di Data factory e inserire una coppia di voci di esempio nella tabella.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="8fb7f-242">Creare un contenitore BLOB denominato **adftutorial** nell'account di archiviazione BLOB di Azure aggiunto come servizio collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="8fb7f-243">Preparare SQL Server locale per l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8fb7f-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="8fb7f-244">Nel database specificato per il servizio collegato di SQL Server locale (**SqlServerLinkedService**) usare lo script SQL seguente per creare la tabella **emp** nel database.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

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
2. <span data-ttu-id="8fb7f-245">Inserire un esempio nella tabella:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="8fb7f-246">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="8fb7f-246">Create input dataset</span></span>

1. <span data-ttu-id="8fb7f-247">Nell'**editor di Data Factory** fare clic su **... Altro**, fare clic su **Nuovo set di dati** sulla barra dei comandi e quindi su **Tabella SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="8fb7f-248">Sostituire lo script JSON nel riquadro a destra con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-248">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="8fb7f-249">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-249">Note the following points:</span></span>

   * <span data-ttu-id="8fb7f-250">L'oggetto **type** è impostato su **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="8fb7f-251">L'oggetto **tableName** è impostato su **emp**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="8fb7f-252">**linkedServiceName** è impostato su **SqlServerLinkedService**. Questo servizio collegato è stato creato prima nel corso di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="8fb7f-253">Per un set di dati di input non generato da un'altra pipeline in Azure Data Factory, è necessario impostare **external** su **true**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="8fb7f-254">Indica che i dati di input sono generati al di fuori del servizio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="8fb7f-255">È possibile specificare i criteri di dati esterni necessari usando l'elemento **externalData** nella sezione **Policy**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="8fb7f-256">Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="8fb7f-257">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="8fb7f-258">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="8fb7f-258">Create output dataset</span></span>

1. <span data-ttu-id="8fb7f-259">Nell'**Editor di Data factory** fare clic su **Nuovo set di dati** sulla barra dei comandi e selezionare **Archiviazione BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="8fb7f-260">Sostituire lo script JSON nel riquadro a destra con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-260">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="8fb7f-261">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-261">Note the following points:</span></span>

   * <span data-ttu-id="8fb7f-262">L'oggetto **type** è impostato su **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="8fb7f-263">**linkedServiceName** è impostato su **AzureStorageLinkedService**. Questo servizio collegato è stato creato al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="8fb7f-264">**folderPath** è impostato su **adftutorial/outfromonpremdf** dove outfromonpremdf è la cartella nel contenitore adftutorial.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="8fb7f-265">Se non esiste ancora, creare il contenitore **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="8fb7f-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="8fb7f-266">L'oggetto **availability** è impostato su **hourly**. L'oggetto **frequency** è impostato su **hour** e l'oggetto **interval** è impostato su **1**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="8fb7f-267">Il servizio Data Factory genera una sezione di dati di output ogni ora nella tabella **emp** nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="8fb7f-268">Se non è stato specificato **fileName** per una **tabella di output**, i file generati in **folderPath** vengono denominati con il seguente formato: Data<Guid>.txt (ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="8fb7f-269">Per impostare **folderPath** e **fileName** dinamicamente in base all'ora **SliceStart**, usare la proprietà partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="8fb7f-270">Nell'esempio seguente folderPath usa Year, Month e Day dall'oggetto SliceStart (ora di inizio della sezione elaborata), mentre fileName usa Hour dall'oggetto SliceStart.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="8fb7f-271">Ad esempio, se una sezione viene generata per 2014-10-20T08:00:00, folderName è impostato su wikidatagateway/wikisampledataout/2014/10/20 e fileName è impostato su 08.csv.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

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

    <span data-ttu-id="8fb7f-272">Per informazioni dettagliate sulle proprietà JSON, vedere [Spostare dati da/verso l'archivio BLOB di Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="8fb7f-273">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il set di dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="8fb7f-274">Assicurarsi che entrambi i set di dati siano visibili nella visualizzazione albero.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="8fb7f-275">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="8fb7f-275">Create pipeline</span></span>
<span data-ttu-id="8fb7f-276">In questo passaggio viene creata una **pipeline** con un'**attività di copia** che usa **EmpOnPremSQLTable** come input e **OutputBlobTable** come output.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="8fb7f-277">Nell'editor di Data Factory fare clic su **... Altro** e quindi su **Nuova pipeline**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="8fb7f-278">Sostituire lo script JSON nel riquadro a destra con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
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
   > <span data-ttu-id="8fb7f-279">Sostituire il valore della proprietà **start** con il giorno corrente e il valore di **end** con il giorno successivo.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="8fb7f-280">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-280">Note the following points:</span></span>

   * <span data-ttu-id="8fb7f-281">Nella sezione delle attività esiste una sola attività con **type** impostato su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="8fb7f-282">**Input** for per l'attività è impostato su **EmpOnPremSQLTable** e **output** per l'attività è impostato su **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="8fb7f-283">Nella sezione **typeProperties** vengono specificati **SqlSource** come **tipo di origine** e archivio dati e **BlobSink ** è specificato come **tipo di sink**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="8fb7f-284">La query SQL `select * from emp` è specificata per la proprietà **sqlReaderQuery** di **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="8fb7f-285">Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8fb7f-286">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="8fb7f-287">Il valore di **end** è facoltativo, ma in questa esercitazione viene usato.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="8fb7f-288">Se non si specifica alcun valore per la proprietà **end**, il valore verrà calcolato come "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="8fb7f-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="8fb7f-289">Per eseguire la pipeline illimitatamente, specificare **9/9/9999** come valore per la proprietà **end**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="8fb7f-290">Si definisce la durata dell'elaborazione delle sezioni di dati in base alle proprietà di **disponibilità** definite per ogni set di dati di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="8fb7f-291">Nell'esempio sono visualizzate 24 sezioni di dati perché viene generata una sezione di dati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="8fb7f-292">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire la set di dati (la tabella è un set di dati rettangolare).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="8fb7f-293">Verificare che la pipeline venga visualizzata nella visualizzazione albero sotto il nodo **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="8fb7f-294">Ora fare clic su **X** due volte per chiudere la pagina e tornare alla pagina **Data Factory** per **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="8fb7f-295">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="8fb7f-295">**Congratulations!**</span></span> <span data-ttu-id="8fb7f-296">Una data factory di Azure, i servizi collegati, i set di dati e una pipeline sono stati creati correttamente e la pipeline è stata pianificata.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="8fb7f-297">Visualizzare la data factory in una vista diagramma</span><span class="sxs-lookup"><span data-stu-id="8fb7f-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="8fb7f-298">Nel **portale di Azure** fare clic sul riquadro **Diagramma** nella home page per l'istanza della data factory **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="8fb7f-299">:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-299">:</span></span>

    ![Collegamento al diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="8fb7f-301">Verrà visualizzato un diagramma simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="8fb7f-301">You should see the diagram similar to the following image:</span></span>

    ![Vista Diagramma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="8fb7f-303">È possibile eseguire lo zoom avanti, lo zoom indietro e lo zoom al 100%, adattare alla finestra, posizionare automaticamente pipeline e set di dati e visualizzare le informazioni sulla derivazione, evidenziando gli elementi upstream e downstream degli elementi selezionati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="8fb7f-304">È possibile fare doppio clic su un oggetto (set di dati di input/output o pipeline) per visualizzare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="8fb7f-305">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="8fb7f-305">Monitor pipeline</span></span>
<span data-ttu-id="8fb7f-306">In questo passaggio viene usato il portale di Azure per monitorare le attività in un'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="8fb7f-307">È anche possibile usare i cmdlet di PowerShell per monitorare i set di dati e le pipeline.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="8fb7f-308">Per altre informazioni sul monitoraggio, vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="8fb7f-309">Nel diagramma fare doppio clic su **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Sezioni EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="8fb7f-311">Si noti che tutte le sezioni di dati aggiornate hanno lo stato **Pronta** perché la durata della pipeline (dall'ora di inizio all'ora di fine) è nel passato,</span><span class="sxs-lookup"><span data-stu-id="8fb7f-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="8fb7f-312">ma anche perché i dati sono stati inseriti nel database di SQL Server dove sono rimasti.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="8fb7f-313">Verificare che non sia visualizzata alcuna sezione in **Sezioni con errori** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="8fb7f-314">Per visualizzare tutte le sezioni, fare clic su **Vedi altre** nella parte inferiore dell'elenco di sezioni.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="8fb7f-315">A questo punto, nella pagina **Set di dati** fare clic su **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Sezioni OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="8fb7f-317">Fare clic su una qualsiasi sezione dati dell'elenco per visualizzare la pagina **Sezione dati**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="8fb7f-318">Verranno visualizzate le esecuzioni di attività per la sezione.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-318">You see activity runs for the slice.</span></span> <span data-ttu-id="8fb7f-319">In genere viene visualizzata una sola esecuzione di attività.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-319">You see only one activity run usually.</span></span>  

    ![Pannello Sezione dati](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="8fb7f-321">Se lo stato della sezione non è **Pronto**, è possibile visualizzare le sezioni upstream che non sono pronte e bloccano l'esecuzione della sezione corrente nell'elenco **Sezioni upstream non pronte**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="8fb7f-322">Fare clic sull'**esecuzione attività** dall'elenco nella parte inferiore della pagina per visualizzare i **dettagli dell'esecuzione attività**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Pagina Dettagli esecuzione attività](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="8fb7f-324">Verranno visualizzate informazioni come la velocità effettiva, la durata e il gateway usato per trasferire i dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="8fb7f-325">Fare clic su **X** per chiudere tutte le pagine fino</span><span class="sxs-lookup"><span data-stu-id="8fb7f-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="8fb7f-326">a tornare alla home page di **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="8fb7f-327">(Facoltativo) Fare clic su **Pipeline** e su **ADFTutorialOnPremDF**, quindi eseguire il drill-through delle tabelle di input (**utilizzate**) o dei set di dati di output (**generati**).</span><span class="sxs-lookup"><span data-stu-id="8fb7f-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="8fb7f-328">Usare strumenti come [Microsoft Storage Explorer](http://storageexplorer.com/) per verificare che venga creato un BLOB/file ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Azure Storage Explorer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="8fb7f-330">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8fb7f-330">Next steps</span></span>
* <span data-ttu-id="8fb7f-331">Leggere l’articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per tutti i dettagli sul gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8fb7f-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="8fb7f-332">Per informazioni su come usare l'attività di copia per spostare i dati da un archivio dati di origine a un archivio dati sink, vedere l'articolo [Copiare dati dal BLOB di Azure in SQL Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="8fb7f-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
