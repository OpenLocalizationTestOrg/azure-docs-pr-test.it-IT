---
title: aaaSet backup ibrida con HPC Pack del cluster in Azure | Documenti Microsoft
description: Informazioni su come Microsoft HPC Pack toouse e tooset Azure fino a un piccolo, ad alte prestazioni elaborazione (HPC) cluster ibrido
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="b020e-103">Configurare un cluster ibrido HPC (high performance computing) con Microsoft HPC Pack e nodi di calcolo di Azure su richiesta</span><span class="sxs-lookup"><span data-stu-id="b020e-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="b020e-104">Utilizzare Microsoft HPC Pack 2012 R2 e Azure tooset di una piccolo, ibrido elaborazione a elevate prestazioni cluster (HPC).</span><span class="sxs-lookup"><span data-stu-id="b020e-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="b020e-105">cluster Hello illustrati in questo articolo è costituito da un nodo head di HPC Pack locale e alcuni servizio cloud su richiesta in un Azure distribuire nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="b020e-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="b020e-106">È quindi possibile eseguire processi di calcolo nel cluster ibrido hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Cluster HPC ibrido][Overview] 

<span data-ttu-id="b020e-108">Questa esercitazione viene illustrato un approccio, talvolta definita cluster "burst toohello cloud," applicazioni complesse toorun di toouse scalabile su richiesta delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="b020e-109">Questa esercitazione non presuppone che si abbia esperienza nell'ambito dei cluster di calcolo o di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b020e-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="b020e-110">È previsto toohelp solo distribuire un cluster di calcolo ibrido rapidamente a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="b020e-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="b020e-111">Per considerazioni e passaggi toodeploy ibrida con HPC Pack del cluster su larga scala maggiore in un ambiente di produzione o toouse HPC Pack 2016, vedere hello [Guida dettagliata](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="b020e-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="b020e-112">Per altri scenari con HPC Pack, inclusa la distribuzione automatica di cluster nelle macchine virtuali di Azure, vedere [Opzioni per creare e gestire un cluster HPC in Azure con Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b020e-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b020e-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b020e-113">Prerequisites</span></span>
* <span data-ttu-id="b020e-114">**Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b020e-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="b020e-115">**Un computer locale che esegue Windows Server 2012 R2 o Windows Server 2012** -utilizzare questo computer come nodo head di hello del cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="b020e-116">Se Windows Server non è già in esecuzione, è possibile scaricare e installare una [versione di valutazione](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="b020e-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="b020e-117">computer Hello deve essere tooan aggiunti a un dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b020e-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="b020e-118">Per scopi di test, è possibile configurare i computer del nodo head hello come controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="b020e-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="b020e-119">tooadd hello ruolo server Servizi di dominio Active Directory e innalzare hello nodo head computer come controller di dominio, vedere la documentazione di hello per Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b020e-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="b020e-120">toosupport HPC Pack, hello del sistema operativo deve essere installato in una di queste lingue: inglese, giapponese o cinese (semplificato).</span><span class="sxs-lookup"><span data-stu-id="b020e-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="b020e-121">Verificare che siano installati gli aggiornamenti importanti.</span><span class="sxs-lookup"><span data-stu-id="b020e-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="b020e-122">**HPC Pack 2012 R2** - [scaricare](http://go.microsoft.com/fwlink/p/?linkid=328024) pacchetto di installazione hello hello ultima versione disponibile gratuitamente e copia hello file toohello computer nodo head.</span><span class="sxs-lookup"><span data-stu-id="b020e-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="b020e-123">Scegliere i file di installazione in hello stessa lingua di installazione di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b020e-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="b020e-124">Se si desidera toouse HPC Pack 2016 invece di HPC Pack 2012 R2, è necessaria una configurazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="b020e-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="b020e-125">Vedere hello [Guida dettagliata](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="b020e-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="b020e-126">**Account di dominio** -questo account deve essere configurato con le autorizzazioni di amministratore locale nel nodo head di hello tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b020e-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="b020e-127">**La connettività TCP sulla porta 443** da tooAzure nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="b020e-128">Installare HPC Pack nel nodo head hello</span><span class="sxs-lookup"><span data-stu-id="b020e-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="b020e-129">Installare prima Microsoft HPC Pack in un computer locale che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b020e-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="b020e-130">Il computer diventa nodo head di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="b020e-131">Accedere nel nodo head toohello utilizzando un account di dominio che dispone delle autorizzazioni di amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="b020e-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="b020e-132">Avviare Installazione guidata di HPC Pack hello, eseguire Setup.exe dal file di installazione di HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="b020e-133">In hello **il programma di installazione di HPC Pack 2012 R2** schermata, fare clic su **nuova installazione o aggiungere una nuova installazione esistente di funzionalità tooan**.</span><span class="sxs-lookup"><span data-stu-id="b020e-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![Installazione di HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="b020e-135">In hello **pagina Contratto di Microsoft Software utente**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="b020e-136">In hello **Selezione tipo di installazione** pagina, fare clic su **creare un nuovo cluster HPC creando un nodo head**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="b020e-137">Creazione guidata di Hello esegue diversi test pre-installazione.</span><span class="sxs-lookup"><span data-stu-id="b020e-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="b020e-138">Fare clic su **Avanti** su hello **regole di installazione** se tutti i test superati.</span><span class="sxs-lookup"><span data-stu-id="b020e-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="b020e-139">In caso contrario, esaminare le informazioni di hello fornite e apportare le modifiche necessarie nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="b020e-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="b020e-140">Quindi eseguire nuovamente i test di hello o se necessario inizio hello nuovamente Installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="b020e-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="b020e-141">In hello **configurazione DB HPC** assicurarsi **nodo Head** è selezionata per tutti i database HPC e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configurazione di database][install_hpc4]

8. <span data-ttu-id="b020e-143">Accettare le selezioni predefinite nelle pagine rimanenti di hello della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="b020e-144">In hello **installare i componenti richiesti** pagina, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="b020e-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Installa][install_hpc6]

9. <span data-ttu-id="b020e-146">Al termine dell'installazione di hello, deselezionare **avviare HPC Cluster Manager** e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b020e-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="b020e-147">HPC Cluster Manager viene avviato in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="b020e-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finish][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="b020e-149">Preparare hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="b020e-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="b020e-150">Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com) con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="b020e-151">Dopo aver completato questi passaggi, è possibile distribuire i nodi di Azure dal nodo head di hello in locale.</span><span class="sxs-lookup"><span data-stu-id="b020e-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="b020e-152">Prendere anche nota dell'ID sottoscrizione di Azure, che sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="b020e-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="b020e-153">Trovare l'ID di hello in **sottoscrizioni** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="b020e-154">Caricare il certificato di gestione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="b020e-154">Upload hello default management certificate</span></span>
<span data-ttu-id="b020e-155">HPC Pack consente di installare un certificato autofirmato nel nodo head hello, chiamato hello predefinito Microsoft HPC Azure Management certificato, che è possibile caricare un certificato di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="b020e-156">Questo certificato è stato specificato per il test e le distribuzioni di prova toosecure hello concatenate hello nodo head e Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="b020e-157">Dal computer del nodo head hello, accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b020e-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b020e-158">Fare clic su **Sottoscrizioni** > *nome_della_sottoscrizione*.</span><span class="sxs-lookup"><span data-stu-id="b020e-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="b020e-159">Fare clic su **Certificati di gestione** > **Carica**. 4.</span><span class="sxs-lookup"><span data-stu-id="b020e-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="b020e-160">Passare nel nodo head di hello per hello file c:\Programmi\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="b020e-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="b020e-161">Fare quindi clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="b020e-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="b020e-162">Hello **predefinito HPC Azure Management** certificato visualizzato nell'elenco di hello dei certificati di gestione.</span><span class="sxs-lookup"><span data-stu-id="b020e-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="b020e-163">Creazione di un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="b020e-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="b020e-164">Per prestazioni ottimali, creare account di archiviazione hello (in un passaggio successivo) e di servizio cloud hello in hello stessa area geografica.</span><span class="sxs-lookup"><span data-stu-id="b020e-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="b020e-165">Nel portale di hello, fare clic su **(classico) di servizi Cloud** > **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b020e-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="b020e-166">Digitare un nome DNS per il servizio di hello, scegliere un gruppo di risorse e un percorso e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="b020e-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="b020e-167">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b020e-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="b020e-168">Nel portale di hello, fare clic su **gli account di archiviazione (classico)** > **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b020e-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="b020e-169">Digitare un nome per l'account di hello e selezionare hello **classico** modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b020e-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="b020e-170">Scegliere un gruppo di risorse e mantenere i valori predefiniti per le altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="b020e-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="b020e-171">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b020e-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="b020e-172">Configurare un nodo head hello</span><span class="sxs-lookup"><span data-stu-id="b020e-172">Configure hello head node</span></span>
<span data-ttu-id="b020e-173">toouse toodeploy HPC Cluster Manager nodi di Azure e i processi toosubmit, eseguire innanzitutto alcuni passaggi di configurazione del cluster richiesto.</span><span class="sxs-lookup"><span data-stu-id="b020e-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="b020e-174">Nel nodo head hello, avviare Gestione Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="b020e-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="b020e-175">Se hello **Seleziona nodo Head** viene visualizzata la finestra di dialogo, fare clic su **Computer locale**.</span><span class="sxs-lookup"><span data-stu-id="b020e-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="b020e-176">Hello **elenco attività di distribuzione** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="b020e-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="b020e-177">In **Required deployment tasks** (Attività di distribuzione necessarie) fare clic su **Configure your network** (Configurare la rete).</span><span class="sxs-lookup"><span data-stu-id="b020e-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configurazione della rete][config_hpc2]

3. <span data-ttu-id="b020e-179">Nella configurazione guidata rete hello, selezionare **tutti i nodi solo in una rete aziendale** (topologia 5).</span><span class="sxs-lookup"><span data-stu-id="b020e-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="b020e-180">Questa configurazione di rete è hello più semplice per scopi dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="b020e-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topologia 5][config_hpc3]
   
4. <span data-ttu-id="b020e-182">Fare clic su **Avanti** i valori predefiniti di tooaccept nel hello restanti pagine della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="b020e-183">Quindi, nella hello **revisione** scheda, fare clic su **configura** configurazione di rete toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="b020e-184">In hello **elenco attività di distribuzione**, fare clic su **fornire le credenziali di installazione**.</span><span class="sxs-lookup"><span data-stu-id="b020e-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="b020e-185">In hello **credenziali per l'installazione** nella finestra di dialogo digitare hello le credenziali dell'account di dominio hello utilizzato tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b020e-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="b020e-186">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b020e-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="b020e-188">In hello **elenco attività di distribuzione**, fare clic su **configurare hello denominazione di nuovi nodi**.</span><span class="sxs-lookup"><span data-stu-id="b020e-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="b020e-189">In hello **specificare serie di denominazione nodo** finestra di dialogo casella, accettare il valore predefinito hello denominazione serie e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b020e-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="b020e-190">Completare questo passaggio, anche se hello nodi di Azure che è aggiungere in questa esercitazione vengono denominati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b020e-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Denominazione dei nodi][config_hpc8]
   
9. <span data-ttu-id="b020e-192">In hello **elenco attività di distribuzione**, fare clic su **creare un modello di nodo**.</span><span class="sxs-lookup"><span data-stu-id="b020e-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="b020e-193">Più avanti nell'esercitazione di hello, utilizzare cluster toohello di hello nodo modello tooadd nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="b020e-194">In Creazione guidata modello di nodo di hello, eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b020e-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="b020e-195">a.</span><span class="sxs-lookup"><span data-stu-id="b020e-195">a.</span></span> <span data-ttu-id="b020e-196">In hello **Scegli tipo di modello di nodo** pagina, fare clic su **il modello di nodo di Windows Azure**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Modello di nodo][config_hpc10]
    
    <span data-ttu-id="b020e-198">b.</span><span class="sxs-lookup"><span data-stu-id="b020e-198">b.</span></span> <span data-ttu-id="b020e-199">Fare clic su **Avanti** nome del modello predefinito di tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="b020e-200">c.</span><span class="sxs-lookup"><span data-stu-id="b020e-200">c.</span></span> <span data-ttu-id="b020e-201">In hello **forniscono informazioni sulla sottoscrizione** pagina, immettere l'ID sottoscrizione di Azure (disponibile nelle informazioni sull'account di Azure).</span><span class="sxs-lookup"><span data-stu-id="b020e-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="b020e-202">In **Certificato di gestione**cercare **Default Microsoft HPC Azure Management**.</span><span class="sxs-lookup"><span data-stu-id="b020e-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="b020e-203">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="b020e-203">Then click **Next**.</span></span>
    
    ![Modello di nodo][config_hpc12]
    
    <span data-ttu-id="b020e-205">d.</span><span class="sxs-lookup"><span data-stu-id="b020e-205">d.</span></span> <span data-ttu-id="b020e-206">In hello **forniscono informazioni sul servizio** pagina, servizio cloud selezionare hello e account di archiviazione hello creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b020e-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="b020e-207">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="b020e-207">Then click **Next**.</span></span>
    
    ![Modello di nodo][config_hpc13]
    
    <span data-ttu-id="b020e-209">e.</span><span class="sxs-lookup"><span data-stu-id="b020e-209">e.</span></span> <span data-ttu-id="b020e-210">Fare clic su **Avanti** i valori predefiniti di tooaccept nel hello restanti pagine della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="b020e-211">Quindi, nella hello **revisione** scheda, fare clic su **crea** modello di nodo toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b020e-212">Per impostazione predefinita, hello Azure nodo modello include le impostazioni per è toostart (provisioning) e i nodi di hello stop manualmente, utilizzando Gestione Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="b020e-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="b020e-213">È possibile configurare una pianificazione toostart e arrestare hello automaticamente i nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="b020e-214">Aggiungere nodi di Azure toohello cluster</span><span class="sxs-lookup"><span data-stu-id="b020e-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="b020e-215">Utilizzare cluster toohello di hello nodo modello tooadd nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="b020e-216">Aggiunta di cluster di hello nodi toohello archivia le informazioni di configurazione in modo che è possibile avviare (provisioning) usarle in qualsiasi momento nel servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="b020e-217">Dopo che le istanze di hello sono in esecuzione nel servizio cloud hello, ottiene addebitata solo la sottoscrizione per i nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="b020e-218">Seguire questi passaggi tooadd due piccole nodi.</span><span class="sxs-lookup"><span data-stu-id="b020e-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="b020e-219">In HPC Cluster Manager (Gestione cluster HPC) fare clic su **Node Management** (Gestione nodi), denominato **Resource Management** (Gestione risorse) nelle versioni correnti di HPC Pack, > **Add Node** (Aggiungi nodo).</span><span class="sxs-lookup"><span data-stu-id="b020e-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Actions][add_node1]

2. <span data-ttu-id="b020e-221">In hello Aggiunta guidata nodi in hello **Selezione metodo di distribuzione** pagina, fare clic su **nodi di Azure aggiungere**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Aggiunta di un nodo di Azure][add_node1_1]

3. <span data-ttu-id="b020e-223">In hello **specificare nuovi nodi** pagina, il modello di nodo di Azure selezionare hello creato in precedenza (chiamato per impostazione predefinita **modello AzureNode predefinito**).</span><span class="sxs-lookup"><span data-stu-id="b020e-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="b020e-224">Specificare quindi **2** nodi di dimensioni **Small** e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="b020e-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Specifica dei nodi][add_node2]
   
4. <span data-ttu-id="b020e-226">In hello **completamento hello Aggiunta guidata nodi** pagina, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b020e-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="b020e-227">In Gestione cluster HPC saranno ora presenti due nodi di Azure denominati **AzureCN-0001** e **AzureCN-0002**.</span><span class="sxs-lookup"><span data-stu-id="b020e-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="b020e-228">Sono entrambi hello **non distribuiti** stato.</span><span class="sxs-lookup"><span data-stu-id="b020e-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Nodi aggiunti][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="b020e-230">Avviare hello nodi di Azure</span><span class="sxs-lookup"><span data-stu-id="b020e-230">Start hello Azure nodes</span></span>
<span data-ttu-id="b020e-231">Quando si desidera toouse hello le risorse cluster in Azure, utilizzare Gestione Cluster HPC toostart (provisioning) hello nodi di Azure e connetterle nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b020e-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="b020e-232">In Gestione Cluster HPC, fare clic su **nodo Gestione** (chiamato **la gestione delle risorse** nelle versioni correnti di HPC Pack), e selezionare hello nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="b020e-233">Fare clic su **Start** (Avvia) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b020e-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Avvio dei nodi][add_node4]
   
    <span data-ttu-id="b020e-235">nodi Hello transizione toohello **Provisioning** stato.</span><span class="sxs-lookup"><span data-stu-id="b020e-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="b020e-236">Provisioning hello tootrack log stato provisioning hello di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="b020e-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Provisioning dei nodi][add_node6]

3. <span data-ttu-id="b020e-238">Dopo alcuni minuti, hello nodi di Azure completare il provisioning e sono in hello **Offline** stato.</span><span class="sxs-lookup"><span data-stu-id="b020e-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="b020e-239">In questo stato, le istanze del ruolo hello sono in esecuzione ma non ancora accettano i processi cluster.</span><span class="sxs-lookup"><span data-stu-id="b020e-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="b020e-240">tooconfirm che hello istanze del ruolo sono in esecuzione, hello portale di Azure, fare clic su **servizi Cloud (classico)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="b020e-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="b020e-241">Dovrebbe essere due **HpcWorkerRole** istanze (nodi) in esecuzione nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="b020e-242">HPC Pack distribuisce automaticamente anche due **HpcProxy** istanze comunicazione toohandle (dimensione media) tra Azure e hello del nodo head.</span><span class="sxs-lookup"><span data-stu-id="b020e-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Esecuzione delle istanze][view_instances1]

5. <span data-ttu-id="b020e-244">toorun online i nodi di Azure di hello toobring cluster processi, hello selezionare nodi, pulsante destro del mouse e quindi fare clic su **in linea**.</span><span class="sxs-lookup"><span data-stu-id="b020e-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nodi offline][add_node7]
   
    <span data-ttu-id="b020e-246">Gestione Cluster HPC indica che i nodi di hello in hello **Online** stato.</span><span class="sxs-lookup"><span data-stu-id="b020e-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="b020e-247">Eseguire un comando cluster hello</span><span class="sxs-lookup"><span data-stu-id="b020e-247">Run a command across hello cluster</span></span>
<span data-ttu-id="b020e-248">installazione di hello toocheck, utilizzare hello HPC Pack **clusrun** comando toorun un comando o l'applicazione in uno o più nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="b020e-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="b020e-249">Un esempio semplice, utilizzare **clusrun** configurazione IP di hello tooget di hello nodi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b020e-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="b020e-250">Nel nodo head hello, aprire un prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b020e-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="b020e-251">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b020e-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="b020e-252">Se richiesto, immettere la password dell'amministratore del cluster.</span><span class="sxs-lookup"><span data-stu-id="b020e-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="b020e-253">Dovrebbe essere simile toohello seguenti di output del comando.</span><span class="sxs-lookup"><span data-stu-id="b020e-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="b020e-255">Esecuzione di un processo di test</span><span class="sxs-lookup"><span data-stu-id="b020e-255">Run a test job</span></span>
<span data-ttu-id="b020e-256">Inviare un processo di test in esecuzione su cluster ibrido hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="b020e-257">Questo esempio è un processo parametrico di organizzazione semplice, ovvero un tipo di calcolo intrinsecamente parallelo.</span><span class="sxs-lookup"><span data-stu-id="b020e-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="b020e-258">Questo esempio viene eseguito sottoattività aggiungere tooitself un integer con hello **set /a** comando.</span><span class="sxs-lookup"><span data-stu-id="b020e-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="b020e-259">Tutti i nodi nel cluster hello hello contribuiscono toofinishing hello sottoattività per numeri interi da 1 too100.</span><span class="sxs-lookup"><span data-stu-id="b020e-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="b020e-260">In HPC Cluster Manager (Gestione cluster HPC) fare clic su **Job Management** (Gestione processi) > **New Parametric Sweep Job** (Nuovo processo parametrico di organizzazione).</span><span class="sxs-lookup"><span data-stu-id="b020e-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nuovo processo][test_job1]

2. <span data-ttu-id="b020e-262">In hello **nuovo processo di Sweep parametrico** della finestra di dialogo **riga di comando**, tipo `set /a *+*` (sovrascrivendo hello riga di comando predefinito visualizzato).</span><span class="sxs-lookup"><span data-stu-id="b020e-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="b020e-263">Lasciare i valori predefiniti per hello rimanenti impostazioni e quindi fare clic su **Invia** processo hello toosubmit.</span><span class="sxs-lookup"><span data-stu-id="b020e-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Sweep parametrico][param_sweep1]

3. <span data-ttu-id="b020e-265">Termine del processo di hello, fare doppio clic su hello **attività durante lo Sweep My** processo.</span><span class="sxs-lookup"><span data-stu-id="b020e-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="b020e-266">Fare clic su **Visualizza attività**, quindi fare clic su un output di hello calcolato tooview sottoattività di tale sottoattività.</span><span class="sxs-lookup"><span data-stu-id="b020e-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Risultati delle attività][view_job361]

5. <span data-ttu-id="b020e-268">Fare clic su quale nodo eseguita calcolo hello tale sottoattività, toosee **allocata nodi**.</span><span class="sxs-lookup"><span data-stu-id="b020e-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="b020e-269">(il nome del nodo nel proprio cluster potrebbe essere diverso).</span><span class="sxs-lookup"><span data-stu-id="b020e-269">(Your cluster might show a different node name.)</span></span>
   
    ![Risultati delle attività][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="b020e-271">Arrestare hello nodi di Azure</span><span class="sxs-lookup"><span data-stu-id="b020e-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="b020e-272">Dopo aver tentato cluster hello, arrestare la account tooyour hello nodi di Azure tooavoid costi non necessari.</span><span class="sxs-lookup"><span data-stu-id="b020e-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="b020e-273">Questo passaggio Arresta servizio cloud hello e rimuove le istanze del ruolo Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="b020e-274">In HPC Cluster Manager (Gestione cluster HPC) selezionare entrambi i nodi di Azure in **Node Management** (Gestione Nodi), denominato **Resource Management** (Gestione risorse) in versioni precedenti di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b020e-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="b020e-275">Fare quindi clic su **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="b020e-275">Then, click **Stop**.</span></span>
   
    ![Interruzione dei nodi][stop_node1]

2. <span data-ttu-id="b020e-277">In hello **nodi di Azure Arresta** la finestra di dialogo, fare clic su **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="b020e-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="b020e-278">nodi Hello transizione toohello **arresto** stato.</span><span class="sxs-lookup"><span data-stu-id="b020e-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="b020e-279">Dopo alcuni minuti, HPC Cluster Manager mostra che sono nodi hello **non distribuiti**.</span><span class="sxs-lookup"><span data-stu-id="b020e-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Nodi non distribuiti][stop_node4]

4. <span data-ttu-id="b020e-281">tooconfirm le istanze del ruolo hello non è più in esecuzione in Azure, in hello Azure fare clic su portale, **(classico) di servizi Cloud** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="b020e-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="b020e-282">Nessuna istanza viene distribuita nell'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="b020e-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="b020e-283">Esercitazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b020e-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b020e-284">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b020e-284">Next steps</span></span>
* <span data-ttu-id="b020e-285">Esplorare la documentazione di hello per [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="b020e-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="b020e-286">vedere tooset di una distribuzione di cluster HPC Pack su larga scala maggiore, ibrida [potenziamento tooAzure istanze del ruolo di lavoro con Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="b020e-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="b020e-287">Per altri modi toocreate un cluster HPC Pack in Azure, incluse utilizzando i modelli di gestione risorse di Azure, vedere [opzioni cluster HPC con Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b020e-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
