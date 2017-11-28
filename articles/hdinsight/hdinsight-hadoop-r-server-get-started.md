---
title: aaaGet avviato con il Server di R in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toocreate un Apache nascita nel cluster HDInsight che include i Server di R e inviare uno script R in cluster hello.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="8b21a-103">Introduzione all'uso di R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b21a-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="8b21a-104">HDInsight include un toobe opzione R Server integrato nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b21a-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="8b21a-105">Questa opzione consente agli script R toouse Spark e MapReduce toorun distribuiti i calcoli.</span><span class="sxs-lookup"><span data-stu-id="8b21a-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="8b21a-106">In questo documento, viene illustrato come un Server di R in cluster HDInsight e quindi Esegui una R script che illustra l'uso di Spark per toocreate distribuiti calcoli R.</span><span class="sxs-lookup"><span data-stu-id="8b21a-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8b21a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b21a-107">Prerequisites</span></span>

* <span data-ttu-id="8b21a-108">**Una sottoscrizione di Azure**: prima di iniziare questa esercitazione è necessario avere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b21a-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="8b21a-109">Articolo passare toohello [versione di valutazione gratuita di Microsoft Azure ottenere](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8b21a-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="8b21a-110">**Un client Secure Shell (SSH)**: viene usato un SSH client tooremotely cluster HDInsight toohello connettersi ed eseguire comandi direttamente nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="8b21a-111">Per altre informazioni, vedere l'articolo su come [usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="8b21a-112">**Le chiavi SSH (facoltative)**: È possibile proteggere hello SSH account utilizzato tooconnect toohello cluster tramite una password o una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="8b21a-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="8b21a-113">Utilizzando una password è più semplice e consente di tooget avviato senza toocreate una coppia di chiavi pubblica/privata.</span><span class="sxs-lookup"><span data-stu-id="8b21a-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="8b21a-114">Tuttavia, usare una chiave è più sicuro.</span><span class="sxs-lookup"><span data-stu-id="8b21a-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="8b21a-115">passaggi di Hello in questo documento si presuppongono che si sta utilizzando una password.</span><span class="sxs-lookup"><span data-stu-id="8b21a-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="8b21a-116">Creazione automatizzata di cluster</span><span class="sxs-lookup"><span data-stu-id="8b21a-116">Automated cluster creation</span></span>

<span data-ttu-id="8b21a-117">È possibile automatizzare la creazione di hello di HDInsight R Servers tramite Gestione risorse di Azure modelli, hello SDK e anche PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b21a-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="8b21a-118">toocreate un Server di R usando un modello di gestione delle risorse di Azure, vedere [distribuire un cluster di HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="8b21a-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="8b21a-119">toocreate un Server di R usando hello .NET SDK, vedere [creare cluster basati su Linux in HDInsight mediante hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8b21a-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="8b21a-120">R Server toodeploy tramite powershell, vedere l'articolo hello in [creazione di un Server di R in HDInsight con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="8b21a-121">Creare il cluster di hello utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b21a-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="8b21a-122">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b21a-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8b21a-123">Selezionare **Nuovo** -> **Intelligence e analisi** -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Immagine della creazione di un nuovo cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="8b21a-125">In hello **creazione rapida** esperienza, immettere un nome per il cluster hello in hello **nome Cluster** campo.</span><span class="sxs-lookup"><span data-stu-id="8b21a-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="8b21a-126">Se si dispone di più sottoscrizioni di Azure, utilizzare hello **sottoscrizione** voce tooselect hello uno desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="8b21a-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Selezione del nome del cluster e della sottoscrizione](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="8b21a-128">Selezionare **Cluster tipo** tooopen hello **configurazione Cluster** blade.</span><span class="sxs-lookup"><span data-stu-id="8b21a-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="8b21a-129">In hello **configurazione Cluster** pannello hello seleziona le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="8b21a-130">**Tipo di cluster**: R Server</span><span class="sxs-lookup"><span data-stu-id="8b21a-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="8b21a-131">**Versione**: versione di hello selezionare tooinstall R Server nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="8b21a-132">versione di Hello attualmente disponibile è ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="8b21a-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="8b21a-133">Sono disponibili note sulla versione per le versioni disponibili di hello del Server di R [qui](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="8b21a-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="8b21a-134">**Edizione community R Studio per R Server**: questo IDE basate su browser viene installato per impostazione predefinita nel nodo edge hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="8b21a-135">Se si preferisce toonot è installato, quindi deselezionare la casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="8b21a-136">Se si sceglie toohave è installato, hello URL per l'accesso a hello accesso RStudio Server si trova in un pannello dell'applicazione del portale per il cluster dopo averla creata.</span><span class="sxs-lookup"><span data-stu-id="8b21a-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="8b21a-137">Lasciare le altre opzioni hello i valori predefiniti di hello e utilizzare hello **selezionare** toosave hello cluster tipo di pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b21a-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Schermata del pannello del tipo di cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="8b21a-139">Immettere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="8b21a-140">Specificare un **nome utente SSH**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="8b21a-141">SSH è usato tooremotely connettersi toohello cluster utilizzando un **Secure Shell (SSH)** client.</span><span class="sxs-lookup"><span data-stu-id="8b21a-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="8b21a-142">È possibile specificare utente SSH hello in questa finestra di dialogo oppure dopo la creazione del cluster hello (nella scheda Configurazione di hello per cluster hello).</span><span class="sxs-lookup"><span data-stu-id="8b21a-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="8b21a-143">R Server è configurato tooexpect un **nome utente SSH** di "remoteuser".</span><span class="sxs-lookup"><span data-stu-id="8b21a-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="8b21a-144">**Se si utilizza un nome utente diverso, è necessario eseguire un passaggio aggiuntivo dopo la creazione di cluster hello.**</span><span class="sxs-lookup"><span data-stu-id="8b21a-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="8b21a-145">La casella di hello lasciare per **usare stessa password account di accesso cluster** toouse **PASSWORD** come hello l'autenticazione di tipo a meno che non si preferisce l'utilizzo di una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="8b21a-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="8b21a-146">È necessario tooaccess una coppia di chiavi pubblica/privata R Server nel cluster hello tramite un client come, ad esempio, RTVS, RStudio o altri IDE desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="8b21a-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="8b21a-147">Se si installa hello edizione community RStudio Server, è necessario toochoose una password SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="8b21a-148">toocreate e utilizzare una coppia di chiavi pubblica/privata, deselezionare **usare stessa password account di accesso cluster** e quindi selezionare **chiave pubblica** e procedere come segue.</span><span class="sxs-lookup"><span data-stu-id="8b21a-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="8b21a-149">Queste istruzioni presuppongono che Cygwin con ssh-keygen o equivalente sia già installato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="8b21a-150">Generare una coppia di chiavi pubblica/privata dal prompt dei comandi di hello in un computer portatile:</span><span class="sxs-lookup"><span data-stu-id="8b21a-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="8b21a-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="8b21a-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="8b21a-152">Seguire hello prompt tooname un file di chiave, quindi immettere una passphrase per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8b21a-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="8b21a-153">La schermata dovrebbe essere simile al seguente hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="8b21a-153">Your screen should look something like hello following image:</span></span>

        ![Riga di comando SSH in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="8b21a-155">Questo comando crea un file di chiave privata e un file di chiave pubblica in hello < privato-key-filename > nome pub, ad esempio furiosa e furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="8b21a-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="8b21a-157">Specificare quindi il file di chiave pubblica hello (&#42;. pub) quando l'assegnazione HDI le credenziali del cluster e infine verificare il gruppo di risorse, area e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Pannello Credenziali](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="8b21a-159">Modificare le autorizzazioni per file di chiave privata hello in un computer portatile:</span><span class="sxs-lookup"><span data-stu-id="8b21a-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="8b21a-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="8b21a-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="8b21a-161">Utilizzare il file di chiave privata di hello con SSH per l'accesso remoto:</span><span class="sxs-lookup"><span data-stu-id="8b21a-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="8b21a-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="8b21a-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="8b21a-163">In alternativa, come definizione di hello parte di Spark il Hadoop contesto di calcolo per il Server di R nel client hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="8b21a-164">Vedere hello **utilizzando Microsoft R Server come Hadoop Client** sottosezione [creare un contesto di calcolo per Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="8b21a-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="8b21a-165">Creazione rapida di Hello si esegue la transizione toohello **archiviazione** account archiviazione hello tooselect pannello impostazioni toobe hello al percorso principale di hello HDFS file system utilizzato dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="8b21a-166">Selezionare un account di archiviazione di Azure nuovo o esistente oppure un account di archiviazione di Data Lake esistente.</span><span class="sxs-lookup"><span data-stu-id="8b21a-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="8b21a-167">Se si seleziona un account di archiviazione di Azure, è selezionato un account di archiviazione esistente scegliendo **selezionare un account di archiviazione** e quindi selezionando conto hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="8b21a-168">Creare un nuovo account tramite hello **Crea nuovo** collegamento hello **selezionare un account di archiviazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8b21a-169">Se si seleziona **New** è necessario immettere un nome per il nuovo account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="8b21a-170">Se il nome di hello è accettato, viene visualizzato un segno di spunta verde.</span><span class="sxs-lookup"><span data-stu-id="8b21a-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="8b21a-171">Hello **contenitore predefinito** nome toohello impostazioni predefinite del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="8b21a-172">Lasciare l'impostazione predefinita come valore di hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="8b21a-173">Se una nuova opzione di account di archiviazione è stata selezionata un prompt dei comandi tooselect **percorso** è specificato tooselect toocreate quale area hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Pannello di origine dati](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="8b21a-175">Selezionando il percorso di hello per l'origine dei dati predefinita hello imposta anche percorso hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="8b21a-176">Hello predefinito e cluster di origine dati deve essere in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="8b21a-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="8b21a-177">Se si desidera toouse un archivio Data Lake esistente, quindi selezionare hello toouse account di archiviazione ADLS e aggiungere il cluster hello *Aggiungi* archivio identità di tooyour cluster tooallow accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="8b21a-178">Per altre informazioni su questo processo, vedere [Creare cluster HDInsight con Data Lake Store tramite il portale di Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="8b21a-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="8b21a-179">Hello utilizzare **selezionare** configurazione dell'origine dati hello toosave pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b21a-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="8b21a-180">Hello **riepilogo** pannello visualizza quindi toovalidate tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="8b21a-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="8b21a-181">Qui è possibile modificare il **dimensioni del Cluster** toomodify hello numero di server nel cluster e specificare le **Script azioni** desiderato toorun.</span><span class="sxs-lookup"><span data-stu-id="8b21a-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="8b21a-182">A meno che non si conosce la necessità di un cluster di dimensioni maggiore, lasciare il numero di hello di nodi di lavoro predefinito hello `4`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="8b21a-183">Hello stimato costo del cluster hello viene visualizzato all'interno di blade hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![riepilogo cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="8b21a-185">Se necessario, è possibile ridimensionare il cluster in un secondo momento tramite hello portale (**Cluster** -> **impostazioni** -> **scala Cluster**) tooincrease o ridurre il numero di hello di nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b21a-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="8b21a-186">Il ridimensionamento può essere utile per minimo verso il basso cluster hello quando non è in uso o per l'aggiunta di dimensionamento hello toomeet attività più grandi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="8b21a-187">Tookeep alcuni fattori presente quando il cluster, nodi dati hello e nodo di hello del bordo di ridimensionamento sono:</span><span class="sxs-lookup"><span data-stu-id="8b21a-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="8b21a-188">prestazioni Hello di analisi di R Server distribuite in Spark sono proporzionale toohello numero di nodi di lavoro se dati hello sono grandi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="8b21a-189">prestazioni Hello di analisi di R Server sono lineare nella dimensione di hello dei dati da analizzare.</span><span class="sxs-lookup"><span data-stu-id="8b21a-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="8b21a-190">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8b21a-190">For example:</span></span>  

     * <span data-ttu-id="8b21a-191">Per i dati di piccole toomodest, delle prestazioni sono consigliabile quando analizzato in un contesto di calcolo locale nel nodo edge hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="8b21a-192">Per altre informazioni sugli scenari di hello in cui hello locale e Spark contesti di calcolo funzionano meglio, vedere le opzioni di contesto di calcolo per il Server di R in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b21a-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="8b21a-193">Se si accedere nodo edge toohello ed esegue lo script R, quindi vengono eseguiti tutti ma hello rx-funzioni ScaleR <strong>localmente</strong> nel nodo edge hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="8b21a-194">Pertanto hello memoria e numero di core del nodo perimetrale hello deve essere ridimensionata di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="8b21a-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="8b21a-195">Hello che ciò vale anche se si utilizza Server R come contesto di calcolo remoto HDI dal portatile.</span><span class="sxs-lookup"><span data-stu-id="8b21a-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Pannello livelli dei prezzi di nodo](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="8b21a-197">Hello utilizzare **selezionare** nodo hello del pulsante toosave dei prezzi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="8b21a-198">È presente anche un collegamento **Scarica modello e parametri**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="8b21a-199">Fare clic su questo script toodisplay collegamento che possono essere utilizzati tooautomate hello creazione di un cluster con configurazione selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="8b21a-200">Questi script sono disponibili da hello voce portale Azure per il cluster anche dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8b21a-201">Comporta un tempo per hello cluster toobe creato, in genere circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="8b21a-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="8b21a-202">Utilizzare il riquadro hello su hello schermata iniziale oppure hello **notifiche** voce hello a sinistra della hello pagina toocheck nel processo di creazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="8b21a-203">Connettersi tooRStudio Server</span><span class="sxs-lookup"><span data-stu-id="8b21a-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="8b21a-204">Se si è scelto tooinclude edizione community RStudio Server dell'installazione, è possibile accedere accesso RStudio hello tramite due metodi diversi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="8b21a-205">Passare toohello URL seguente (dove **CLUSTERNAME** hello nome del cluster di hello creato):</span><span class="sxs-lookup"><span data-stu-id="8b21a-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="8b21a-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="8b21a-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="8b21a-207">Aprire la voce hello per il cluster in hello portale di Azure seleziona hello **R Server dashboard** collegamento rapido e quindi selezionando hello **R Studio Dashboard**:</span><span class="sxs-lookup"><span data-stu-id="8b21a-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Dashboard di accesso hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Dashboard di accesso hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="8b21a-210">Indipendentemente dal metodo hello utilizzato, hello primo tentativo di accesso è necessario tooauthenticate due volte.</span><span class="sxs-lookup"><span data-stu-id="8b21a-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="8b21a-211">Fornire l'autenticazione prima di hello, hello *ID utente di amministrazione del cluster* e *password*.</span><span class="sxs-lookup"><span data-stu-id="8b21a-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="8b21a-212">Al prompt dei comandi secondo hello fornire hello *SSH userid* e *password*.</span><span class="sxs-lookup"><span data-stu-id="8b21a-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="8b21a-213">Log successivi aggiuntivi richiedono solo hello *password SSH* e *userid*.</span><span class="sxs-lookup"><span data-stu-id="8b21a-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="8b21a-214">Connettere toohello R Server edge nodo</span><span class="sxs-lookup"><span data-stu-id="8b21a-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="8b21a-215">Connettersi tooR nodo del lato Server del cluster HDInsight hello tramite SSH con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="8b21a-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="8b21a-216">È possibile trovare hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` indirizzo nel portale di Azure selezionando il cluster, quindi hello **tutte le impostazioni** -> **app** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="8b21a-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="8b21a-217">Consente di visualizzare informazioni sull'Endpoint SSH per il nodo di edge hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Immagine di hello SSH Endpoint per il nodo di edge hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="8b21a-219">Se si utilizza un toosecure password account utente SSH, si è tooenter richiesto è.</span><span class="sxs-lookup"><span data-stu-id="8b21a-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="8b21a-220">Se si utilizza una chiave pubblica, è possibile hello toouse `-i` toospecify parametro hello chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8b21a-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="8b21a-221">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8b21a-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8b21a-222">Per ulteriori informazioni, vedere [connettersi tooHDInsight (Hadoop) tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="8b21a-223">Una volta connessi, verrà visualizzato un prompt dei comandi seguenti toohello simile:</span><span class="sxs-lookup"><span data-stu-id="8b21a-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="8b21a-224">Abilitare più utenti simultanei</span><span class="sxs-lookup"><span data-stu-id="8b21a-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="8b21a-225">L'aggiunta di più utenti per il nodo di edge hello in cui hello community RStudio viene eseguita la versione, è possibile abilitare più utenti simultanei.</span><span class="sxs-lookup"><span data-stu-id="8b21a-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="8b21a-226">Quando si crea un cluster HDInsight, è necessario specificare due utenti: un utente HTTP e un utente SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Utenti simultanei 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="8b21a-228">**Nome utente account di accesso del cluster**: un utente HTTP per l'autenticazione tramite gateway HDInsight hello che viene utilizzato tooprotect hello HDInsight cluster creato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="8b21a-229">Questo utente HTTP è utilizzato tooaccess hello Ambari UI, interfaccia utente di YARN, nonché altri componenti dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="8b21a-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="8b21a-230">**Nome utente della Shell (SSH) protetta**: un cluster di hello tooaccess utente SSH tramite shell protetta.</span><span class="sxs-lookup"><span data-stu-id="8b21a-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="8b21a-231">Questo utente è un utente nel sistema Linux per tutti i nodi head hello, nodi di lavoro e i nodi periferici hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="8b21a-232">È possibile utilizzare shell protetta tooaccess uno qualsiasi dei nodi hello in un cluster remoto.</span><span class="sxs-lookup"><span data-stu-id="8b21a-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="8b21a-233">versione di R Studio Server Community Hello utilizzata in hello Microsoft R Server nel cluster di HDInsight tipo accetta solo nome utente di Linux e la password come un meccanismo di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b21a-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="8b21a-234">Non supporta il passaggio di token.</span><span class="sxs-lookup"><span data-stu-id="8b21a-234">It does not support passing tokens.</span></span> <span data-ttu-id="8b21a-235">Pertanto, se è stato creato un nuovo cluster e si desidera toouse R Studio tooaccess, è necessario toolog in due volte.</span><span class="sxs-lookup"><span data-stu-id="8b21a-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="8b21a-236">Primo accesso con le credenziali utente hello HTTP tramite hello HDInsight Gateway:</span><span class="sxs-lookup"><span data-stu-id="8b21a-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Utenti simultanei 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="8b21a-238">Utilizzare quindi hello SSH utente credenziali toolog in tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="8b21a-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Utenti simultanei 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="8b21a-240">Attualmente, durante il provisioning di un cluster HDInsight è possibile creare un solo account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="8b21a-241">In modo tooenable cluster più utenti tooaccess Microsoft R Server in HDInsight, è necessario toocreate altri utenti nel sistema Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="8b21a-242">Poiché RStudio Server Community è in esecuzione sul nodo del bordo del cluster di hello, vi sono alcuni passaggi di seguito:</span><span class="sxs-lookup"><span data-stu-id="8b21a-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="8b21a-243">Utilizzare hello creato SSH utente toolog nel nodo di edge toohello</span><span class="sxs-lookup"><span data-stu-id="8b21a-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="8b21a-244">Aggiungere altri utenti Linux nel nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="8b21a-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="8b21a-245">Utilizzare la versione RStudio Community con utente hello creato</span><span class="sxs-lookup"><span data-stu-id="8b21a-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="8b21a-246">Passaggio 1: Utilizzare hello creato SSH utente toolog nel nodo di edge toohello</span><span class="sxs-lookup"><span data-stu-id="8b21a-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="8b21a-247">Scaricare uno strumento SSH (ad esempio Putty) e utilizzare hello esistente SSH utente toolog in.</span><span class="sxs-lookup"><span data-stu-id="8b21a-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="8b21a-248">Segui hello istruzioni fornite in [connettersi tooHDInsight (Hadoop) tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello nodo del bordo.</span><span class="sxs-lookup"><span data-stu-id="8b21a-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="8b21a-249">indirizzo del nodo perimetrale Hello per R Server nel cluster HDInsight è: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="8b21a-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="8b21a-250">Passaggio 2: Aggiungere altri utenti Linux nel nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="8b21a-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="8b21a-251">tooadd un nodo di edge toohello utente, eseguire i comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="8b21a-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="8b21a-252">È necessario visualizzare hello elementi restituiti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-252">You should see hello following items returned:</span></span> 

![Utenti simultanei 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="8b21a-254">Quando viene richiesto di "password Kerberos corrente:", è sufficiente premere **invio** tooignore è.</span><span class="sxs-lookup"><span data-stu-id="8b21a-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="8b21a-255">Hello `-m` opzione `useradd` comando indica che il sistema hello creerà una home directory utente hello, che è obbligatorio per la versione RStudio Community.</span><span class="sxs-lookup"><span data-stu-id="8b21a-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="8b21a-256">Passaggio 3: Versione usare RStudio Community con utente hello creato</span><span class="sxs-lookup"><span data-stu-id="8b21a-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="8b21a-257">Utilizzare hello creati dall'utente toolog tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="8b21a-257">Use hello user created toolog in tooRStudio:</span></span>

![Utenti simultanei 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="8b21a-259">Si noti che RStudio indica che si sta utilizzando un nuovo utente hello (qui, ad esempio, *sshuser6*) toolog cluster hello:</span><span class="sxs-lookup"><span data-stu-id="8b21a-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Utenti simultanei 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="8b21a-261">È anche possibile accedere con credenziali originale hello (per impostazione predefinita è *sshuser*) contemporaneamente da un'altra finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="8b21a-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="8b21a-262">È possibile inviare un processo usando funzioni ScaleR.</span><span class="sxs-lookup"><span data-stu-id="8b21a-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="8b21a-263">Ecco un esempio di hello comandi utilizzati toorun un processo:</span><span class="sxs-lookup"><span data-stu-id="8b21a-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="8b21a-264">Si noti che i processi di hello inviati in diversi nomi utente nell'interfaccia utente di YARN:</span><span class="sxs-lookup"><span data-stu-id="8b21a-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Utenti simultanei 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="8b21a-266">Si noti inoltre che hello appena aggiunti utenti non dispongono di privilegi radice nel sistema di Linux, ma hanno hello stesso di accedere ai file di hello tooall hello HDFS e WASB archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="8b21a-267">Usare la console di hello R</span><span class="sxs-lookup"><span data-stu-id="8b21a-267">Use hello R console</span></span>

1. <span data-ttu-id="8b21a-268">Dalla sessione SSH hello, utilizzare hello console hello R toostart dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="8b21a-269">Verrà visualizzato il seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="8b21a-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="8b21a-270">R versione 3.2.2 (2015-08-14): "Incendio" Copyright (C) 2015 hello R Foundation per la piattaforma di elaborazione statistica: x86_64-pc-linux-gnu (64 bit)</span><span class="sxs-lookup"><span data-stu-id="8b21a-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="8b21a-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span><span class="sxs-lookup"><span data-stu-id="8b21a-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="8b21a-272">Si è tooredistribute iniziale in determinate condizioni.</span><span class="sxs-lookup"><span data-stu-id="8b21a-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="8b21a-273">Type "license()" or "licence()" for distribution details.</span><span class="sxs-lookup"><span data-stu-id="8b21a-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="8b21a-274">Natural language support but running in an English locale</span><span class="sxs-lookup"><span data-stu-id="8b21a-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="8b21a-275">R is a collaborative project with many contributors.</span><span class="sxs-lookup"><span data-stu-id="8b21a-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="8b21a-276">Digitare 'contributors()' per ulteriori informazioni e 'citation()' in modalità toocite R o R pacchetti nelle pubblicazioni.</span><span class="sxs-lookup"><span data-stu-id="8b21a-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="8b21a-277">Digitare 'demo ()' per alcuni demo, 'help()' per la Guida in linea o 'help.start()' per un toohelp di interfaccia browser HTML.</span><span class="sxs-lookup"><span data-stu-id="8b21a-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="8b21a-278">Digitare 'OcxQmail' tooquit R.</span><span class="sxs-lookup"><span data-stu-id="8b21a-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="8b21a-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="8b21a-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="8b21a-280">Type "readme()" for release notes.</span><span class="sxs-lookup"><span data-stu-id="8b21a-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="8b21a-281">Da hello `>` prompt dei comandi, è possibile immettere il codice R.</span><span class="sxs-lookup"><span data-stu-id="8b21a-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="8b21a-282">Server R include i pacchetti che consentono di tooeasily interagire con Hadoop ed eseguire calcoli distribuiti.</span><span class="sxs-lookup"><span data-stu-id="8b21a-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="8b21a-283">Ad esempio, utilizzare hello comando tooview hello radice hello predefiniti del file system per il cluster HDInsight hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="8b21a-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="8b21a-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="8b21a-285">È inoltre possibile utilizzare hello WASB stile addressing.</span><span class="sxs-lookup"><span data-stu-id="8b21a-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="8b21a-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="8b21a-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="8b21a-287">Utilizzare R Server in HDI da un'istanza remota di Microsoft R Server o Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="8b21a-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="8b21a-288">È possibile tooset il contesto di calcolo Hadoop Spark HDI toohello accesso da un'istanza remota di Microsoft R Server o Microsoft R Client in esecuzione in un computer desktop o portatile.</span><span class="sxs-lookup"><span data-stu-id="8b21a-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="8b21a-289">Vedere **utilizzando Microsoft R Server come Hadoop Client** sottosezione hello [creazione di un contesto di calcolo per Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="8b21a-290">toodo in tal caso, è necessario hello toospecify le opzioni seguenti quando si definisce il contesto di calcolo di hello RxSpark in un computer portatile: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="8b21a-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="8b21a-291">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8b21a-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="8b21a-292">Usare un contesto di calcolo</span><span class="sxs-lookup"><span data-stu-id="8b21a-292">Use a compute context</span></span>

<span data-ttu-id="8b21a-293">Un contesto di calcolo consente toocontrol se calcolo viene eseguito localmente sul nodo del bordo hello o distribuito tra i nodi nel cluster HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="8b21a-294">Dalla console di hello R (in una sessione SSH) o il RStudio Server, utilizzare hello segue i dati di esempio di codice tooload nell'account di archiviazione predefinito hello per HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8b21a-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="8b21a-295">Successivamente, si creare alcune informazioni di dati e definire due origini dati in modo che è possibile utilizzare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="8b21a-296">Eseguire una regressione logistica sui dati hello utilizzando il contesto di calcolo locale hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="8b21a-297">È necessario visualizzare l'output che termina con toohello simile di righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="8b21a-298">Successivamente, eseguire la regressione logistica stesso utilizzando il contesto di Spark hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="8b21a-299">contesto di Spark Hello distribuisce l'elaborazione di tutti i nodi di lavoro di hello in cluster di HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="8b21a-300">È anche possibile utilizzare MapReduce toodistribute calcolo tra nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="8b21a-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="8b21a-301">Per altre informazioni sul contesto di calcolo, vedere [Opzioni del contesto di calcolo per R Server su HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="8b21a-302">Distribuire i nodi toomultiple codice R</span><span class="sxs-lookup"><span data-stu-id="8b21a-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="8b21a-303">Con R Server, è possibile eseguire codice R esistente facilmente ed eseguito in più nodi nel cluster hello utilizzando `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="8b21a-304">Questa funzione è utile in caso di sweep di parametri o simulazioni.</span><span class="sxs-lookup"><span data-stu-id="8b21a-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="8b21a-305">il codice seguente Hello è riportato un esempio di come toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="8b21a-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="8b21a-306">Se si utilizza ancora hello Spark o contesto MapReduce, questo comando restituisce il valore di nodename hello per nodi di lavoro hello tale codice hello `(Sys.info()["nodename"])` viene eseguito in.</span><span class="sxs-lookup"><span data-stu-id="8b21a-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="8b21a-307">Ad esempio, in un cluster a quattro nodi, si prevede di tooreceive output simili toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="8b21a-308">Accesso ai dati in Hive e Parquet</span><span class="sxs-lookup"><span data-stu-id="8b21a-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="8b21a-309">Una funzionalità disponibile in R Server 9.1 consente l'accesso diretto toodata Hive e Parquet per l'utilizzo per le funzioni ScaleR nel contesto di calcolo di hello Spark.</span><span class="sxs-lookup"><span data-stu-id="8b21a-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="8b21a-310">Queste funzionalità sono disponibili tramite i nuovi dati origine le funzioni ScaleR chiamate RxHiveData e RxParquetData che funzionano tramite l'utilizzo di dati di Spark SQL tooload direttamente in un frame di dati di Spark per l'analisi da ScaleR.</span><span class="sxs-lookup"><span data-stu-id="8b21a-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="8b21a-311">Hello di codice seguente fornisce un codice di esempio sull'utilizzo di nuove funzioni hello:</span><span class="sxs-lookup"><span data-stu-id="8b21a-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="8b21a-312">Per altre informazioni sull'utilizzo di queste nuove funzioni, vedere la Guida online hello in R Server tramite l'utilizzo di hello `?RxHivedata` e `?RxParquetData` comandi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="8b21a-313">Installare pacchetti R aggiuntivi nel nodo del bordo hello</span><span class="sxs-lookup"><span data-stu-id="8b21a-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="8b21a-314">Se si desidera tooinstall pacchetti R aggiuntivi nel nodo di hello edge, è possibile utilizzare `install.packages()` direttamente dall'interno hello console R quando connesso toohello bordo nodo tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="8b21a-315">Tuttavia, se è necessario pacchetti R tooinstall in nodi di lavoro di hello di hello cluster, è necessario utilizzare un'azione di Script.</span><span class="sxs-lookup"><span data-stu-id="8b21a-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="8b21a-316">Le azioni script sono gli script Bash toomake utilizzato configurazione modifiche toohello HDInsight cluster o tooinstall software aggiuntivo, ad esempio pacchetti R aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="8b21a-317">tooinstall pacchetti aggiuntivi con un'azione di Script, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b21a-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b21a-318">Utilizzo di pacchetti R aggiuntivi di azioni Script tooinstall sono utilizzabili solo dopo aver creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="8b21a-319">Non utilizzare questa procedura durante la creazione del cluster come script hello si basa su R Server viene completamente installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="8b21a-320">Da hello [portale di Azure](https://portal.azure.com), selezionare il Server di R nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b21a-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="8b21a-321">Da hello **impostazioni** pannello seleziona **azioni Script** e quindi **inviare nuovi** toosubmit una nuova azione di Script.</span><span class="sxs-lookup"><span data-stu-id="8b21a-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Immagine del pannello Azioni script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="8b21a-323">Da hello **inviare l'azione script** pannello fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="8b21a-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="8b21a-324">**Nome**: un semplice nome tooidentify questo script</span><span class="sxs-lookup"><span data-stu-id="8b21a-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="8b21a-325">**URI script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="8b21a-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="8b21a-326">**Head**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="8b21a-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="8b21a-327">**Lavoro**: questa voce deve essere **selezionata**</span><span class="sxs-lookup"><span data-stu-id="8b21a-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="8b21a-328">**Nodi perimetrali**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="8b21a-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="8b21a-329">**Zookeeper**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="8b21a-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="8b21a-330">**I parametri**: hello R pacchetti toobe installato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="8b21a-331">Ad esempio, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="8b21a-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="8b21a-332">**Salvare questa azione script in modo permanente...**: questa voce deve essere **selezionata**</span><span class="sxs-lookup"><span data-stu-id="8b21a-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="8b21a-333">Per impostazione predefinita, tutti i pacchetti R installati da uno snapshot del repository MRAN Microsoft hello coerente con la versione di hello del Server di R che è stato installato.</span><span class="sxs-lookup"><span data-stu-id="8b21a-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="8b21a-334">Se si desidera tooinstall le versioni più recenti dei pacchetti, vi è rischio di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="8b21a-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="8b21a-335">Tuttavia questo tipo di installazione è possibile specificando `useCRAN` come hello elencare primo elemento del pacchetto di hello, ad esempio `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="8b21a-336">Alcuni pacchetti R richiedono librerie di sistema di Linux aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="8b21a-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="8b21a-337">Per praticità, è stato preinstallato dipendenze hello necessarie hello primi 100 pacchetti R più diffusi.</span><span class="sxs-lookup"><span data-stu-id="8b21a-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="8b21a-338">Tuttavia, se si installa i pacchetti R di hello richiedono librerie oltre a questi quindi è necessario scaricare script di base hello utilizzato in questo argomento e aggiungere passaggi tooinstall hello sistema librerie.</span><span class="sxs-lookup"><span data-stu-id="8b21a-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="8b21a-339">È necessario quindi pubblica tooa script hello modificato di caricamento blob contenitore nell'archiviazione di Azure e utilizzare i pacchetti hello modificato script tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="8b21a-340">Per altre informazioni sullo sviluppo di azioni script, vedere l'articolo [Sviluppo di azioni script con HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8b21a-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Aggiunta di un'azione script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="8b21a-342">Selezionare **crea** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8b21a-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="8b21a-343">Al termine dell'esecuzione dello script hello, i pacchetti hello R sono disponibili in tutti i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8b21a-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="8b21a-344">Uso della messa in funzione di Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="8b21a-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="8b21a-345">Una volta completata la modellazione dei dati, è possibile rendere operative le stime di toomake modello hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="8b21a-346">tooconfigure per rendere operativo Microsoft R Server, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b21a-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="8b21a-347">Prima di tutto, ssh nel nodo di hello del bordo.</span><span class="sxs-lookup"><span data-stu-id="8b21a-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="8b21a-348">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="8b21a-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8b21a-349">Dopo l'utilizzo di ssh, cambiare directory per la versione appropriata di hello e sudo hello dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="8b21a-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="8b21a-350">Per Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="8b21a-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="8b21a-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0 sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="8b21a-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="8b21a-352">Per Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="8b21a-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="8b21a-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="8b21a-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="8b21a-354">rendere operativo Microsoft R Server tooconfigure con una configurazione di una casella hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b21a-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="8b21a-355">Selezionare "Configure R Server for Operationalization" (Configurare R Server per la messa in funzione)</span><span class="sxs-lookup"><span data-stu-id="8b21a-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="8b21a-356">Selezionare "A.</span><span class="sxs-lookup"><span data-stu-id="8b21a-356">Select “A.</span></span> <span data-ttu-id="8b21a-357">One-box (web + compute nodes)” (Una casella (Web + nodi di calcolo)"</span><span class="sxs-lookup"><span data-stu-id="8b21a-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="8b21a-358">Immettere una password per hello **admin** utente</span><span class="sxs-lookup"><span data-stu-id="8b21a-358">Enter a password for hello **admin** user</span></span>

![Opzione per una casella](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="8b21a-360">Come passaggio facoltativo, è possibile eseguire controlli diagnostici eseguendo un test di diagnostica, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8b21a-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="8b21a-361">Selezionare "6.</span><span class="sxs-lookup"><span data-stu-id="8b21a-361">Select “6.</span></span> <span data-ttu-id="8b21a-362">Run diagnostic tests" (Esegui test diagnostici)</span><span class="sxs-lookup"><span data-stu-id="8b21a-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="8b21a-363">Selezionare "A.</span><span class="sxs-lookup"><span data-stu-id="8b21a-363">Select “A.</span></span> <span data-ttu-id="8b21a-364">Test configuration" (Configurazione test)</span><span class="sxs-lookup"><span data-stu-id="8b21a-364">Test configuration”</span></span>
3. <span data-ttu-id="8b21a-365">Immettere nome utente = "admin" e la password del passaggio di configurazione precedente</span><span class="sxs-lookup"><span data-stu-id="8b21a-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="8b21a-366">Conferma dell'integrità complessiva = pass</span><span class="sxs-lookup"><span data-stu-id="8b21a-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="8b21a-367">Utilità di amministrazione di hello uscita</span><span class="sxs-lookup"><span data-stu-id="8b21a-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="8b21a-368">Uscire da SSH</span><span class="sxs-lookup"><span data-stu-id="8b21a-368">Exit SSH</span></span>

![Diagnostica per la messa in funzione](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="8b21a-370">**Ritardi considerevoli quando si utilizza il servizio Web in Spark**</span><span class="sxs-lookup"><span data-stu-id="8b21a-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="8b21a-371">Se si verificano ritardi quando si tenta di tooconsume un servizio web creato con mrsdeploy funzioni in un contesto di calcolo Spark, potrebbe essere necessario tooadd alcune cartelle mancanti.</span><span class="sxs-lookup"><span data-stu-id="8b21a-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="8b21a-372">applicazione di Spark Hello appartiene tooa utente denominato '*rserve2*' ogni volta che viene chiamato da un servizio web utilizzando le funzioni mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="8b21a-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="8b21a-373">toowork questo problema:</span><span class="sxs-lookup"><span data-stu-id="8b21a-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="8b21a-374">In questa fase, configurazione hello per rendere operativo è stata completata.</span><span class="sxs-lookup"><span data-stu-id="8b21a-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="8b21a-375">È ora possibile usare hello 'mrsdeploy' pacchetto sul toohello di tooconnect RClient rendere operativo il nel nodo del bordo e iniziare a usare le funzionalità come [esecuzione remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e [servizi web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="8b21a-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="8b21a-376">A seconda se il cluster è installato in una rete virtuale o non, potrebbe essere necessario tooset backup Porta avanti tunneling tramite account di accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="8b21a-377">Hello sezioni seguenti illustrano come tooset backup questo tunnel.</span><span class="sxs-lookup"><span data-stu-id="8b21a-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="8b21a-378">Cluster RServer su rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8b21a-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="8b21a-379">Assicurarsi che consentire il traffico attraverso il nodo 12800 toohello bordo porta.</span><span class="sxs-lookup"><span data-stu-id="8b21a-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="8b21a-380">In questo modo, è possibile utilizzare funzionalità di hello edge nodi tooconnect toohello rendere operativo.</span><span class="sxs-lookup"><span data-stu-id="8b21a-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="8b21a-381">Se hello `remoteLogin()` non è possibile connettere toohello bordo nodo, ma è possibile nodo del bordo di toohello SSH, quindi è necessario tooverify se traffico sulla porta 12800 tooallow regole di hello è stato impostato correttamente o meno.</span><span class="sxs-lookup"><span data-stu-id="8b21a-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="8b21a-382">Se si continua, il problema di hello tooface, è possibile aggirare il mediante l'impostazione di porta Avanti tunneling tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="8b21a-383">Per istruzioni, vedere hello seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="8b21a-384">Cluster RServer non impostato su rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8b21a-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="8b21a-385">Se il cluster non è configurato sulla rete virtuale o si riscontrano problemi relativi alla connettività tramite la rete virtuale, è possibile usare il tunneling di port forwarding SSH:</span><span class="sxs-lookup"><span data-stu-id="8b21a-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8b21a-386">La configurazione è possibile anche in Putty.</span><span class="sxs-lookup"><span data-stu-id="8b21a-386">On Putty, you can set it up as well.</span></span>

![Connessione SSH con Putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="8b21a-388">Una volta la sessione SSH è attiva, il traffico di hello dalla porta del computer 12800 verrà inoltrato porta del nodo perimetrale toohello 12800 tramite una sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="8b21a-389">Assicurarsi di usare `127.0.0.1:12800` nel metodo `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="8b21a-390">Questo accesso rendere operativo il del nodo perimetrale toohello tramite inoltro alla porta.</span><span class="sxs-lookup"><span data-stu-id="8b21a-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="8b21a-391">Come nodi in HDInsight i nodi di lavoro di calcolo tooscale rendere operativo il Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="8b21a-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="8b21a-392">Rimuovere le autorizzazioni ai nodi di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="8b21a-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="8b21a-393">Attualmente Microsoft R Server non è gestito tramite Yarn.</span><span class="sxs-lookup"><span data-stu-id="8b21a-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="8b21a-394">Se i nodi di lavoro hello non vengono rimossi, hello Gestione risorse di Yarn non funzionerà come previsto perché non sarà compatibile con risorse hello utilizzata dal server hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="8b21a-395">In ordine tooavoid questa situazione, si consiglia di rimozione di nodi di lavoro hello prima la scalabilità orizzontale nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="8b21a-396">Nodi di lavoro toodecommissioning passaggi:</span><span class="sxs-lookup"><span data-stu-id="8b21a-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="8b21a-397">Accedere alla console Ambari tooHDI del cluster e fare clic sulla scheda "host"</span><span class="sxs-lookup"><span data-stu-id="8b21a-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="8b21a-398">Selezionare i nodi di lavoro (toobe messo fuori servizio), fare clic sul menu "azioni" > "Selezionato gli host" > "Hosts" > fare clic su "Attivare la modalità di manutenzione ON".</span><span class="sxs-lookup"><span data-stu-id="8b21a-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="8b21a-399">Ad esempio, nella seguente immagine hello è stato selezionato toodecommission wn3 e wn4.</span><span class="sxs-lookup"><span data-stu-id="8b21a-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="8b21a-401">Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Decommission** (Rimuovi autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="8b21a-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="8b21a-402">Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Decommission** (Rimuovi autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="8b21a-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="8b21a-403">Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="8b21a-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="8b21a-404">Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="8b21a-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="8b21a-405">Selezionare **Actions** > **Selected Hosts** > **Hosts** > fare clic su **Stop All Components** (Arresta tutti i componenti).</span><span class="sxs-lookup"><span data-stu-id="8b21a-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="8b21a-406">Deselezionare i nodi di lavoro hello e selezionare i nodi head hello</span><span class="sxs-lookup"><span data-stu-id="8b21a-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="8b21a-407">Selezionare **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components** (Riavvia tutti i componenti).</span><span class="sxs-lookup"><span data-stu-id="8b21a-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="8b21a-408">Configurare i nodi di calcolo su ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione</span><span class="sxs-lookup"><span data-stu-id="8b21a-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="8b21a-409">Accedere tramite SSH a ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="8b21a-410">Eseguire l'utilità di amministrazione con `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="8b21a-411">Immettere "1" l'opzione tooselect "Configurare R Server per rendere operativo il".</span><span class="sxs-lookup"><span data-stu-id="8b21a-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="8b21a-412">Immettere l'opzione tooselect "c" "c.</span><span class="sxs-lookup"><span data-stu-id="8b21a-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="8b21a-413">Compute node" (Nodo di calcolo).</span><span class="sxs-lookup"><span data-stu-id="8b21a-413">Compute node".</span></span> <span data-ttu-id="8b21a-414">Consente di configurare il nodo di calcolo hello nel nodo lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="8b21a-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="8b21a-415">Hello uscita utilità di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="8b21a-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="8b21a-416">Aggiungere i dettagli dei nodi di calcolo nel nodo Web</span><span class="sxs-lookup"><span data-stu-id="8b21a-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="8b21a-417">Dopo aver configurati tutti i nodi di lavoro rimossi toorun nodo di calcolo, tornare nel nodo edge hello e aggiungere gli indirizzi IP dei nodi di lavoro rimossi in configurazione del nodo di hello Microsoft R Server web:</span><span class="sxs-lookup"><span data-stu-id="8b21a-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="8b21a-418">SSH nel nodo di hello del bordo.</span><span class="sxs-lookup"><span data-stu-id="8b21a-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="8b21a-419">Eseguire `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="8b21a-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="8b21a-420">Cercare la sezione "URI" hello e aggiungere l'indirizzo IP del nodo di lavoro e dettagli della porta.</span><span class="sxs-lookup"><span data-stu-id="8b21a-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro con la riga di comando](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="8b21a-422">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="8b21a-422">Troubleshoot</span></span>

<span data-ttu-id="8b21a-423">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="8b21a-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8b21a-424">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b21a-424">Next steps</span></span>

<span data-ttu-id="8b21a-425">A questo punto è necessario comprendere come un nuovo cluster HDInsight che include hello R Server hello concetti di base e dell'utilizzo toocreate hello console R da una sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="8b21a-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="8b21a-426">Hello seguenti argomenti vengono illustrati altri modi di gestione e utilizzo del Server di R in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8b21a-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="8b21a-427">Aggiungere RStudio Server tooHDInsight (se non è installato durante la creazione del cluster)</span><span class="sxs-lookup"><span data-stu-id="8b21a-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="8b21a-428">Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="8b21a-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="8b21a-429">Opzioni di Archiviazione di Azure per R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b21a-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
