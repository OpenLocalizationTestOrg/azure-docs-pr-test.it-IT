---
title: Introduzione all'uso di R Server in HDInsight - Azure | Microsoft Docs
description: Informazioni sulla creazione di un cluster Apache Spark in HDInsight che include R Server e sull'invio di uno script R nel cluster.
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
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="f57f1-103">Introduzione all'uso di R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="f57f1-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="f57f1-104">HDInsight include un'opzione R Server da integrare nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="f57f1-105">Con questa opzione, gli script R possono usare Spark e MapReduce per eseguire i calcoli distribuiti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="f57f1-106">In questo documento si apprenderà come creare un R Server in un cluster HDInsight e come eseguire uno script R che illustra l'uso di Spark per i calcoli R distribuiti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f57f1-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f57f1-107">Prerequisites</span></span>

* <span data-ttu-id="f57f1-108">**Una sottoscrizione di Azure**: prima di iniziare questa esercitazione è necessario avere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f57f1-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="f57f1-109">Per altre informazioni, vedere il video su come [ottenere una versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f57f1-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="f57f1-110">**Un client Secure Shell (SSH)**: il client SSH viene usato per connettersi da remoto al cluster HDInsight ed eseguire i comandi direttamente nel cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="f57f1-111">Per altre informazioni, vedere l'articolo su come [usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="f57f1-112">**Chiavi SSH (facoltative)**: è possibile proteggere l'account SSH usato per connettersi al cluster mediante una password o una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="f57f1-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="f57f1-113">Usare una password è più semplice ed è possibile iniziare senza necessità di creare una coppia di chiavi pubblica/privata.</span><span class="sxs-lookup"><span data-stu-id="f57f1-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="f57f1-114">Tuttavia, usare una chiave è più sicuro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="f57f1-115">I passaggi in questo documento presuppongono che si stia usando una password.</span><span class="sxs-lookup"><span data-stu-id="f57f1-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="f57f1-116">Creazione automatizzata di cluster</span><span class="sxs-lookup"><span data-stu-id="f57f1-116">Automated cluster creation</span></span>

<span data-ttu-id="f57f1-117">È possibile automatizzare la creazione di cluster HDInsight R Server usando modelli di Azure Resource Manager, SDK e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f57f1-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="f57f1-118">Per creare un cluster R Server con un modello di Azure Resource Manager, vedere [Deploy an R-server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/) (Distribuire un cluster HDInsight R Server).</span><span class="sxs-lookup"><span data-stu-id="f57f1-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="f57f1-119">Per creare un cluster R Server con .NET SDK, vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="f57f1-120">Per distribuire R Server con PowerShell, vedere l'articolo sulla [creazione di un cluster R Server in HDInsight con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="f57f1-121">Creare il cluster con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f57f1-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="f57f1-122">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f57f1-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f57f1-123">Selezionare **Nuovo** -> **Intelligence e analisi** -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Immagine della creazione di un nuovo cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="f57f1-125">Nell'esperienza **Creazione rapida** inserire il nome del cluster nel campo **Nome cluster**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="f57f1-126">Se sono disponibili più sottoscrizioni di Azure, usare la voce **Sottoscrizione** per selezionare quella da usare.</span><span class="sxs-lookup"><span data-stu-id="f57f1-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![Selezione del nome del cluster e della sottoscrizione](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="f57f1-128">Selezionare **Tipo di cluster** per aprire il pannello **Configurazione cluster**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="f57f1-129">Nel pannello **Configurazione cluster** selezionare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f57f1-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="f57f1-130">**Tipo di cluster**: R Server</span><span class="sxs-lookup"><span data-stu-id="f57f1-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="f57f1-131">**Versione**: selezionare la versione di R Server da installare nel cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="f57f1-132">La versione attualmente disponibile è ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="f57f1-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="f57f1-133">Le note sulla versione per le versioni disponibili di R Server sono disponibili [qui](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="f57f1-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="f57f1-134">**R Studio community edition for R Server**: questo IDE basato su browser viene installato per impostazione predefinita sul nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="f57f1-135">Se si preferisce non installarlo, deselezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="f57f1-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="f57f1-136">Se si sceglie di installarlo, l'URL per l'accesso a RStudio Server è disponibile in un pannello delle applicazioni del portale per il cluster, dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="f57f1-137">Lasciare le altre opzioni impostate sui valori predefiniti e usare il pulsante **Seleziona** per salvare il tipo di cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![Schermata del pannello del tipo di cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="f57f1-139">Immettere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="f57f1-140">Specificare un **nome utente SSH**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="f57f1-141">SSH è usato per connettersi al cluster da remoto tramite un client **Secure Shell (SSH)**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="f57f1-142">È possibile specificare l'utente SSH in questa finestra di dialogo o dopo aver creato il cluster (nella scheda Configurazione per il cluster).</span><span class="sxs-lookup"><span data-stu-id="f57f1-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="f57f1-143">R Server è configurato in modo da prevedere il **nome utente SSH** "remoteuser".</span><span class="sxs-lookup"><span data-stu-id="f57f1-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="f57f1-144">**Se si usa un nome utente diverso, è necessario eseguire un passaggio aggiuntivo dopo la creazione del cluster.**</span><span class="sxs-lookup"><span data-stu-id="f57f1-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="f57f1-145">Lasciare selezionata la casella **Usa la stessa password dell'account di accesso del cluster** per usare la **PASSWORD** come tipo di autenticazione a meno che non si preferisca usare una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="f57f1-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="f57f1-146">Se si vuole accedere a R Server nel cluster tramite un client remoto, ad esempio RTVS, RStudio o un altro ambiente desktop IDE, è necessario usare una coppia di chiavi pubblica/privata.</span><span class="sxs-lookup"><span data-stu-id="f57f1-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="f57f1-147">Se si installa RStudio Server Community Edition, è necessario scegliere una password SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="f57f1-148">Per creare e usare una coppia di chiavi pubblica/privata, deselezionare **Usa la stessa password dell'account di accesso del cluster** e quindi selezionare **CHIAVE PUBBLICA** e procedere come segue.</span><span class="sxs-lookup"><span data-stu-id="f57f1-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="f57f1-149">Queste istruzioni presuppongono che Cygwin con ssh-keygen o equivalente sia già installato.</span><span class="sxs-lookup"><span data-stu-id="f57f1-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="f57f1-150">Dal prompt dei comandi sul computer portatile, generare una coppia di chiavi pubblica/privata:</span><span class="sxs-lookup"><span data-stu-id="f57f1-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="f57f1-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="f57f1-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="f57f1-152">Attenersi alla richiesta di un nome di un file di chiave e quindi immettere una passphrase per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f57f1-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="f57f1-153">La schermata dovrebbe essere simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f57f1-153">Your screen should look something like the following image:</span></span>

        ![Riga di comando SSH in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="f57f1-155">Questo comando crea un file di chiave privata e un file di chiave pubblica con il nome <nomefile-chiave-privata>.pub, ad esempio furiosa e furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="f57f1-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="f57f1-157">Specificare quindi il file di chiave pubblica (&#42;.pub) quando si assegnano le credenziali del cluster HDI e infine confermare il gruppo di risorse e l'area e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Pannello Credenziali](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="f57f1-159">Modificare le autorizzazioni per il file di chiave privata nel computer portatile:</span><span class="sxs-lookup"><span data-stu-id="f57f1-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="f57f1-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="f57f1-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="f57f1-161">Usare il file di chiave privata con SSH per l'accesso remoto:</span><span class="sxs-lookup"><span data-stu-id="f57f1-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="f57f1-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="f57f1-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="f57f1-163">o come parte della definizione del contesto di calcolo di Hadoop Spark per R Server nel client.</span><span class="sxs-lookup"><span data-stu-id="f57f1-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="f57f1-164">Vedere la sottosezione **Using Microsoft R Server as a Hadoop Client** (Uso di Microsoft R Server come client Hadoop) in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) (Creare un contesto di calcolo per Spark).</span><span class="sxs-lookup"><span data-stu-id="f57f1-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="f57f1-165">La creazione rapida esegue la transizione al pannello **Archiviazione** per selezionare le impostazioni dell'account di archiviazione da usare per il percorso principale del file system HDFS usato dal cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="f57f1-166">Selezionare un account di archiviazione di Azure nuovo o esistente oppure un account di archiviazione di Data Lake esistente.</span><span class="sxs-lookup"><span data-stu-id="f57f1-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="f57f1-167">Se si sceglie un account di archiviazione di Azure, è possibile selezionare un account di archiviazione esistente scegliendo **Selezionare un account di archiviazione** e quindi selezionando l'account desiderato.</span><span class="sxs-lookup"><span data-stu-id="f57f1-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="f57f1-168">Creare un nuovo account usando il collegamento **Nuovo** nella sezione **Selezionare un account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f57f1-169">Se si seleziona **Nuovo** è necessario immettere un nome per il nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="f57f1-170">Se il nome viene accettato, verrà visualizzato un segno di spunta verde.</span><span class="sxs-lookup"><span data-stu-id="f57f1-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="f57f1-171">Il **contenitore predefinito** viene impostato sul nome predefinito del cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="f57f1-172">Lasciare questa impostazione predefinita come valore.</span><span class="sxs-lookup"><span data-stu-id="f57f1-172">Leave this default as the value.</span></span>

      <span data-ttu-id="f57f1-173">Se è stata selezionata l'opzione per un nuovo account di archiviazione, viene visualizzato un prompt che consente di selezionare il **Percorso** per scegliere l'area in cui creare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![Pannello di origine dati](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="f57f1-175">La selezione del percorso per l'origine dati predefinita imposta anche il percorso del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="f57f1-176">L'origine dati del cluster e l'origine dati predefinita devono trovarsi nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="f57f1-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="f57f1-177">Se si vuole usare un Data Lake Store esistente, selezionare l'account di archiviazione ADLS da usare e aggiungere al cluster l'identità *ADD* del cluster per consentire l'accesso all'archivio.</span><span class="sxs-lookup"><span data-stu-id="f57f1-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="f57f1-178">Per altre informazioni su questo processo, vedere [Creare cluster HDInsight con Data Lake Store tramite il portale di Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="f57f1-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="f57f1-179">Usare il pulsante **Seleziona** per salvare la configurazione dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="f57f1-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="f57f1-180">Viene quindi visualizzato il pannello **Riepilogo** per convalidare tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f57f1-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="f57f1-181">Qui è possibile modificare le **dimensioni dei Cluster** per cambiare il numero di server del cluster e specificare qualsiasi **azione di script** da eseguire.</span><span class="sxs-lookup"><span data-stu-id="f57f1-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="f57f1-182">A meno che non si sia consapevoli di aver bisogno di un cluster di maggiori dimensioni, lasciare il numero di nodi di lavoro sul valore predefinito di `4`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="f57f1-183">All'interno del pannello viene visualizzato il costo stimato del cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![riepilogo cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="f57f1-185">Se necessario, è possibile ridimensionare il cluster in un secondo momento tramite il portale (**Cluster** -> **Impostazioni** -> **Ridimensiona cluster**) per aumentare o ridurre il numero di nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="f57f1-186">Questo ridimensionamento può essere utile per disattivare il cluster quando non è in uso o per aggiungere capacità allo scopo di soddisfare le esigenze di attività più estese.</span><span class="sxs-lookup"><span data-stu-id="f57f1-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="f57f1-187">Ecco alcuni fattori da tenere presente quando si modificano le dimensioni del cluster, dei nodi di dati e del nodo perimetrale:</span><span class="sxs-lookup"><span data-stu-id="f57f1-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="f57f1-188">Quando la quantità di dati è ingente, le prestazioni delle analisi R Server distribuite in Spark sono proporzionali al numero di nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="f57f1-189">Le prestazioni delle analisi Server R sono proporzionali alle dimensioni dei dati analizzati.</span><span class="sxs-lookup"><span data-stu-id="f57f1-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="f57f1-190">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f57f1-190">For example:</span></span>  

     * <span data-ttu-id="f57f1-191">Per quantità di dati di piccole e medie dimensioni, le prestazioni sono migliori se l'analisi avviene in un contesto di calcolo locale sul nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="f57f1-192">Per altre informazioni sugli scenari in cui i contesti di calcolo Spark e locale funzionano meglio, vedere Opzioni del contesto di calcolo per R Server su HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="f57f1-193">Se si accede al nodo perimetrale e si esegue lo script R, tutte le funzioni, ad eccezione delle funzioni ScaleR rx, vengono eseguite <strong>localmente</strong> sul nodo perimetrale,</span><span class="sxs-lookup"><span data-stu-id="f57f1-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="f57f1-194">in modo tale che la memoria e il numero di core del nodo perimetrale vengano ridimensionati secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="f57f1-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="f57f1-195">Lo stesso vale se si utilizza R Server su HDI come contesto di calcolo remoto dal computer portatile.</span><span class="sxs-lookup"><span data-stu-id="f57f1-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Pannello livelli dei prezzi di nodo](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="f57f1-197">Usare il pulsante **Seleziona** per salvare la configurazione dei piani tariffari del nodo.</span><span class="sxs-lookup"><span data-stu-id="f57f1-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="f57f1-198">È presente anche un collegamento **Scarica modello e parametri**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="f57f1-199">Fare clic su questo collegamento per visualizzare gli script utilizzabili per automatizzare la creazione di un cluster con la configurazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="f57f1-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="f57f1-200">Questi script sono anche disponibili dalla voce del portale di Azure per il cluster dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="f57f1-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f57f1-201">La creazione del cluster richiede tempo, in genere circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="f57f1-202">Usare il riquadro nella Schermata iniziale o la voce **Notifiche** nella parte sinistra della pagina per controllare il processo di creazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="f57f1-203">Connettersi a RStudio Server</span><span class="sxs-lookup"><span data-stu-id="f57f1-203">Connect to RStudio Server</span></span>

<span data-ttu-id="f57f1-204">Se si è scelto di includere RStudio Server Community Edition nell'installazione è possibile accedere a RStudio in due modi diversi.</span><span class="sxs-lookup"><span data-stu-id="f57f1-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="f57f1-205">Passare all'URL seguente (dove **CLUSTERNAME** è il nome del cluster creato):</span><span class="sxs-lookup"><span data-stu-id="f57f1-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="f57f1-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="f57f1-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="f57f1-207">Aprire la voce relativa al cluster nel portale di Azure e selezionare il collegamento rapido **Dashboard di R Server** e quindi **Dashboard di R Studio**:</span><span class="sxs-lookup"><span data-stu-id="f57f1-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![Accedere al dashboard di R Studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Accedere al dashboard di R Studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="f57f1-210">Indipendentemente dal metodo usato, al primo accesso è necessario eseguire l'autenticazione due volte.</span><span class="sxs-lookup"><span data-stu-id="f57f1-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="f57f1-211">Alla prima autenticazione, specificare l'*ID utente* e la *password amministratore del cluster*.</span><span class="sxs-lookup"><span data-stu-id="f57f1-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="f57f1-212">Alla seconda richiesta, specificare l'*ID utente* e la *password SSH*.</span><span class="sxs-lookup"><span data-stu-id="f57f1-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="f57f1-213">Per gli accessi successivi sono necessari solo l'*ID utente* e la *password SSH*.</span><span class="sxs-lookup"><span data-stu-id="f57f1-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="f57f1-214">Connettersi al nodo perimetrale di R Server</span><span class="sxs-lookup"><span data-stu-id="f57f1-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="f57f1-215">Connettersi al nodo perimetrale R Server del cluster HDInsight usando SSH con il comando:</span><span class="sxs-lookup"><span data-stu-id="f57f1-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="f57f1-216">È possibile trovare l'indirizzo `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` nel portale di Azure selezionando il cluster e quindi **Tutte le impostazioni** -> **App** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="f57f1-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="f57f1-217">Questa operazione consente di visualizzare le informazioni sull'endpoint SSH per il nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![Immagine dell'endpoint SSH per il nodo perimetrale](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="f57f1-219">Se è stata usata una password per proteggere l'account utente SSH, viene richiesto di specificarla.</span><span class="sxs-lookup"><span data-stu-id="f57f1-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="f57f1-220">Se è stata usata una chiave pubblica, può essere necessario usare il parametro `-i` per specificare la chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f57f1-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="f57f1-221">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f57f1-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="f57f1-222">Per altre informazioni, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f57f1-223">Una volta effettuata la connessione, viene visualizzato un prompt come quello che segue:</span><span class="sxs-lookup"><span data-stu-id="f57f1-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="f57f1-224">Abilitare più utenti simultanei</span><span class="sxs-lookup"><span data-stu-id="f57f1-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="f57f1-225">È possibile abilitare più utenti simultanei aggiungendo altri utenti per il nodo perimetrale in cui viene eseguita la versione Community di RStudio.</span><span class="sxs-lookup"><span data-stu-id="f57f1-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="f57f1-226">Quando si crea un cluster HDInsight, è necessario specificare due utenti: un utente HTTP e un utente SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Utenti simultanei 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="f57f1-228">**Nome utente dell'account di accesso del cluster**: utente HTTP per l'autenticazione tramite il gateway HDInsight usato per proteggere i cluster HDInsight creati.</span><span class="sxs-lookup"><span data-stu-id="f57f1-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="f57f1-229">Questo utente HTTP viene usato per accedere all'interfaccia utente di Ambari, all'interfaccia utente di YARN e ad altri componenti di interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="f57f1-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="f57f1-230">**Nome utente Secure Shell (SSH)**: utente SSH per accedere al cluster tramite Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="f57f1-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="f57f1-231">È un utente del sistema Linux per tutti i nodi head, di lavoro e perimetrali.</span><span class="sxs-lookup"><span data-stu-id="f57f1-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="f57f1-232">È così possibile usare Secure Shell per accedere a qualsiasi nodo di un cluster remoto.</span><span class="sxs-lookup"><span data-stu-id="f57f1-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="f57f1-233">La versione RStudio Server Community usata nel cluster di tipo Microsoft R Server in HDInsight accetta solo un nome utente e una password Linux come meccanismo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f57f1-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="f57f1-234">Non supporta il passaggio di token.</span><span class="sxs-lookup"><span data-stu-id="f57f1-234">It does not support passing tokens.</span></span> <span data-ttu-id="f57f1-235">Se si vuole usare RStudio per accedere a un nuovo cluster che si è creato, è necessario eseguire l'accesso due volte.</span><span class="sxs-lookup"><span data-stu-id="f57f1-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="f57f1-236">Accedere prima con le credenziali utente HTTP tramite il gateway HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f57f1-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![Utenti simultanei 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="f57f1-238">Usare quindi le credenziali utente SSH per accedere a RStudio:</span><span class="sxs-lookup"><span data-stu-id="f57f1-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![Utenti simultanei 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="f57f1-240">Attualmente, durante il provisioning di un cluster HDInsight è possibile creare un solo account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="f57f1-241">Per consentire a più utenti di accedere a cluster Microsoft R Server in HDInsight, è quindi necessario creare utenti aggiuntivi nel sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="f57f1-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="f57f1-242">Dato che RStudio Server Community è in esecuzione nel nodo perimetrale del cluster, si devono completare diversi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f57f1-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="f57f1-243">Usare l'utente SSH creato per accedere al nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="f57f1-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="f57f1-244">Aggiungere altri utenti Linux nel nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="f57f1-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="f57f1-245">Usare la versione Community di RStudio con l'utente creato</span><span class="sxs-lookup"><span data-stu-id="f57f1-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="f57f1-246">Passaggio 1: Usare l'utente SSH creato per accedere al nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="f57f1-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="f57f1-247">Scaricare qualsiasi strumento SSH (ad esempio, Putty) e usare l'utente SSH esistente per eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f57f1-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="f57f1-248">Seguire quindi le istruzioni riportate in [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md) per accedere al nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="f57f1-249">L'indirizzo del nodo perimetrale per R Server nel cluster HDInsight è: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="f57f1-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="f57f1-250">Passaggio 2: Aggiungere altri utenti Linux nel nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="f57f1-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="f57f1-251">Per aggiungere un utente al nodo perimetrale, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="f57f1-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="f57f1-252">Dovrebbero essere restituite le voci seguenti:</span><span class="sxs-lookup"><span data-stu-id="f57f1-252">You should see the following items returned:</span></span> 

![Utenti simultanei 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="f57f1-254">Quando viene richiesto di immettere la password Kerberos corrente, è sufficiente premere **INVIO** per ignorare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="f57f1-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="f57f1-255">L'opzione `-m` nel comando `useradd` indica che il sistema creerà una home directory per l'utente, obbligatoria per la versione Community di RStudio.</span><span class="sxs-lookup"><span data-stu-id="f57f1-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="f57f1-256">Passaggio 3: Usare la versione Community di RStudio con l'utente creato</span><span class="sxs-lookup"><span data-stu-id="f57f1-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="f57f1-257">Usare l'utente creato per accedere a RStudio:</span><span class="sxs-lookup"><span data-stu-id="f57f1-257">Use the user created to log in to RStudio:</span></span>

![Utenti simultanei 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="f57f1-259">Si noti che RStudio indica che si sta usando il nuovo utente (in questo caso, ad esempio, *sshuser6*) per l'accesso al cluster:</span><span class="sxs-lookup"><span data-stu-id="f57f1-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![Utenti simultanei 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="f57f1-261">Si può anche accedere simultaneamente da un'altra finestra del browser con le credenziali originali (per impostazione predefinita, *sshuser*).</span><span class="sxs-lookup"><span data-stu-id="f57f1-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="f57f1-262">È possibile inviare un processo usando funzioni ScaleR.</span><span class="sxs-lookup"><span data-stu-id="f57f1-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="f57f1-263">Di seguito è riportato un esempio dei comandi usati per eseguire un processo:</span><span class="sxs-lookup"><span data-stu-id="f57f1-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
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

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="f57f1-264">Si noti che i processi inviati sono associati a nomi utente diversi nell'interfaccia utente di YARN:</span><span class="sxs-lookup"><span data-stu-id="f57f1-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![Utenti simultanei 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="f57f1-266">Si noti anche gli utenti appena aggiunti non hanno privilegi a livello radice nel sistema Linux, ma hanno lo stesso accesso a tutti i file nella risorsa di archiviazione HDFS e WASB remota.</span><span class="sxs-lookup"><span data-stu-id="f57f1-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="f57f1-267">Usare la console di R</span><span class="sxs-lookup"><span data-stu-id="f57f1-267">Use the R console</span></span>

1. <span data-ttu-id="f57f1-268">Nella sessione SSH usare il comando seguente per avviare la console R:</span><span class="sxs-lookup"><span data-stu-id="f57f1-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="f57f1-269">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f57f1-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="f57f1-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span><span class="sxs-lookup"><span data-stu-id="f57f1-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="f57f1-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span><span class="sxs-lookup"><span data-stu-id="f57f1-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="f57f1-272">You are welcome to redistribute it under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="f57f1-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="f57f1-273">Type "license()" or "licence()" for distribution details.</span><span class="sxs-lookup"><span data-stu-id="f57f1-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="f57f1-274">Natural language support but running in an English locale</span><span class="sxs-lookup"><span data-stu-id="f57f1-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="f57f1-275">R is a collaborative project with many contributors.</span><span class="sxs-lookup"><span data-stu-id="f57f1-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="f57f1-276">Type "contributors()" for more information and "citation()" on how to cite R or R packages in publications.</span><span class="sxs-lookup"><span data-stu-id="f57f1-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="f57f1-277">Type "demo()" for some demos, "help()" for on-line help, or "help.start()" for an HTML browser interface to help.</span><span class="sxs-lookup"><span data-stu-id="f57f1-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="f57f1-278">Type "q()" to quit R.</span><span class="sxs-lookup"><span data-stu-id="f57f1-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="f57f1-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="f57f1-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="f57f1-280">Type "readme()" for release notes.</span><span class="sxs-lookup"><span data-stu-id="f57f1-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="f57f1-281">Dal prompt `>` è possibile immettere codice R.</span><span class="sxs-lookup"><span data-stu-id="f57f1-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="f57f1-282">R Server include pacchetti che consentono di interagire facilmente con Hadoop ed eseguire calcoli distribuiti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="f57f1-283">Ad esempio, usare il comando seguente per visualizzare la radice del file system predefinito per il cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f57f1-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="f57f1-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="f57f1-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="f57f1-285">È anche possibile usare l'indirizzamento in stile WASB.</span><span class="sxs-lookup"><span data-stu-id="f57f1-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="f57f1-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="f57f1-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="f57f1-287">Utilizzare R Server in HDI da un'istanza remota di Microsoft R Server o Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="f57f1-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="f57f1-288">È possibile configurare l'accesso al contesto di calcolo Hadoop Spark HDI da un'istanza remota di Microsoft R Server o Microsoft R Client in esecuzione in un computer desktop o portatile.</span><span class="sxs-lookup"><span data-stu-id="f57f1-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="f57f1-289">Vedere la sottosezione **Using Microsoft R Server as a Hadoop Client** (Uso di Microsoft R Server come client Hadoop) in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md) (Creare un contesto di calcolo per Spark).</span><span class="sxs-lookup"><span data-stu-id="f57f1-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="f57f1-290">A tale scopo, è necessario specificare le opzioni seguenti quando si definisce il contesto di calcolo RxSpark nel computer portatile: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="f57f1-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="f57f1-291">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f57f1-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="f57f1-292">Usare un contesto di calcolo</span><span class="sxs-lookup"><span data-stu-id="f57f1-292">Use a compute context</span></span>

<span data-ttu-id="f57f1-293">Un contesto di calcolo consente di controllare se il calcolo viene eseguito localmente sul nodo perimetrale o distribuito sui nodi del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="f57f1-294">Da RStudio Server o dalla console R (in una sessione SSH), usare il codice seguente per caricare dati di esempio nella risorsa di archiviazione predefinita per HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f57f1-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
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

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="f57f1-295">Successivamente, si creano alcune informazioni sui dati e si definiscono due origini dati in modo da poter lavorare con i dati.</span><span class="sxs-lookup"><span data-stu-id="f57f1-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="f57f1-296">Si prova poi a eseguire una regressione logistica sui dati usando il contesto di calcolo locale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="f57f1-297">L'output dovrebbe terminare con righe simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="f57f1-297">You should see output that ends with lines similar to the following:</span></span>

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

4. <span data-ttu-id="f57f1-298">Quindi, si prova a eseguire la stessa regressione logistica usando il contesto di Spark.</span><span class="sxs-lookup"><span data-stu-id="f57f1-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="f57f1-299">Il contesto di Spark distribuisce l'elaborazione su tutti i nodi del ruolo di lavoro del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="f57f1-300">È anche possibile usare MapReduce per distribuire il calcolo sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="f57f1-301">Per altre informazioni sul contesto di calcolo, vedere [Opzioni del contesto di calcolo per R Server su HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="f57f1-302">Distribuire il codice R su più nodi</span><span class="sxs-lookup"><span data-stu-id="f57f1-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="f57f1-303">Con R Server, è possibile prelevare facilmente il codice R esistente ed eseguirlo su più nodi del cluster tramite `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="f57f1-304">Questa funzione è utile in caso di sweep di parametri o simulazioni.</span><span class="sxs-lookup"><span data-stu-id="f57f1-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="f57f1-305">Il codice seguente è un esempio di come usare `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="f57f1-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="f57f1-306">Se si sta ancora usando il contesto Spark o MapReduce, questo comando restituisce il valore nodename per i nodi di lavoro in cui viene eseguito il codice `(Sys.info()["nodename"])`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="f57f1-307">In un cluster a quattro nodi, ad esempio, si può prevedere di ricevere un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f57f1-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="f57f1-308">Accesso ai dati in Hive e Parquet</span><span class="sxs-lookup"><span data-stu-id="f57f1-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="f57f1-309">Una funzionalità disponibile in R Server 9.1 consente l'accesso diretto ai dati in Hive e Parquet per l'uso da parte delle funzioni di ScaleR nel contesto di calcolo di Spark.</span><span class="sxs-lookup"><span data-stu-id="f57f1-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="f57f1-310">Queste funzionalità sono disponibili tramite nuove funzioni di origine dati ScaleR denominate RxHiveData e RxParquetData, che usano Spark SQL per caricare i dati direttamente in un frame di dati di Spark per l'analisi da parte di ScaleR.</span><span class="sxs-lookup"><span data-stu-id="f57f1-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="f57f1-311">Il codice seguente offre un esempio dell'uso delle nuove funzioni:</span><span class="sxs-lookup"><span data-stu-id="f57f1-311">The following code provides some sample code on use of the new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="f57f1-312">Per altre informazioni sull'uso di queste nuove funzioni, vedere la guida in linea di R Server tramite i comandi `?RxHivedata` e `?RxParquetData`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="f57f1-313">Installare pacchetti R aggiuntivi nel nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="f57f1-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="f57f1-314">Per installare pacchetti R aggiuntivi nel nodo perimetrale, è possibile usare `install.packages()` direttamente dall'interno della console R quando si è connessi al nodo perimetrale tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="f57f1-315">Tuttavia, se si desidera installare pacchetti R sui nodi di lavoro del cluster, è necessario usare un'azione di script.</span><span class="sxs-lookup"><span data-stu-id="f57f1-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="f57f1-316">Le azioni di script sono script Bash usati per apportare modifiche di configurazione al cluster HDInsight o per installare software aggiuntivo, ad esempio altri pacchetti R.</span><span class="sxs-lookup"><span data-stu-id="f57f1-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="f57f1-317">Per installare altri pacchetti tramite un'azione di script, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f57f1-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f57f1-318">Le azioni di script per installare altri pacchetti R sono possono essere usate solo dopo aver creato il cluster.</span><span class="sxs-lookup"><span data-stu-id="f57f1-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="f57f1-319">Non usare questa procedura durante la creazione del cluster poiché lo script si basa su R Server completamente installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="f57f1-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="f57f1-320">Nel [Portale di Azure](https://portal.azure.com)selezionare il proprio R Server sul cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f57f1-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="f57f1-321">Nel pannello **Impostazioni** selezionare **Azioni script** e quindi **Invia nuova** per inviare una nuova azione di script.</span><span class="sxs-lookup"><span data-stu-id="f57f1-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![Immagine del pannello Azioni script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="f57f1-323">Immettere le informazioni seguenti nel pannello **Invia azione script**:</span><span class="sxs-lookup"><span data-stu-id="f57f1-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="f57f1-324">**Nome**: nome descrittivo per identificare lo script</span><span class="sxs-lookup"><span data-stu-id="f57f1-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="f57f1-325">**URI script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="f57f1-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="f57f1-326">**Head**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="f57f1-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="f57f1-327">**Lavoro**: questa voce deve essere **selezionata**</span><span class="sxs-lookup"><span data-stu-id="f57f1-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="f57f1-328">**Nodi perimetrali**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="f57f1-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="f57f1-329">**Zookeeper**: questa voce deve essere **deselezionata**</span><span class="sxs-lookup"><span data-stu-id="f57f1-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="f57f1-330">**Parametri**: i pacchetti R da installare.</span><span class="sxs-lookup"><span data-stu-id="f57f1-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="f57f1-331">Ad esempio, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="f57f1-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="f57f1-332">**Salvare questa azione script in modo permanente...**: questa voce deve essere **selezionata**</span><span class="sxs-lookup"><span data-stu-id="f57f1-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="f57f1-333">Per impostazione predefinita, tutti i pacchetti R vengono installati da uno snapshot dell'archivio MRAN di Microsoft coerente con la versione di R Server che è stato installato.</span><span class="sxs-lookup"><span data-stu-id="f57f1-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="f57f1-334">L'installazione di versioni più recenti dei pacchetti espone al rischio di incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="f57f1-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="f57f1-335">Questo tipo di installazione è tuttavia possibile specificando `useCRAN` come primo elemento dell'elenco dei pacchetti, ad esempio `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="f57f1-336">Alcuni pacchetti R richiedono librerie di sistema di Linux aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f57f1-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="f57f1-337">Per praticità sono state preinstallate le dipendenze necessarie per i 100 pacchetti R più diffusi.</span><span class="sxs-lookup"><span data-stu-id="f57f1-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="f57f1-338">Tuttavia, se i pacchetti R installati richiedono altre librerie, è necessario scaricare lo script di base usato qui e continuare la procedura per installare le librerie di sistema.</span><span class="sxs-lookup"><span data-stu-id="f57f1-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="f57f1-339">È quindi necessario caricare lo script modificato in un contenitore BLOB pubblico su Archiviazione di Azure e usare lo script modificato per installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="f57f1-340">Per altre informazioni sullo sviluppo di azioni script, vedere l'articolo [Sviluppo di azioni script con HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f57f1-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Aggiunta di un'azione script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="f57f1-342">Selezionare **Crea** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="f57f1-342">Select **Create** to run the script.</span></span> <span data-ttu-id="f57f1-343">Una volta completato lo script, i pacchetti R sono disponibili su tutti i nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="f57f1-344">Uso della messa in funzione di Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="f57f1-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="f57f1-345">Dopo aver completato la modellazione dei dati, è possibile mettere in funzione il modello per generare previsioni.</span><span class="sxs-lookup"><span data-stu-id="f57f1-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="f57f1-346">Per configurare la messa in funzione di Microsoft R Server, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f57f1-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="f57f1-347">Innanzitutto, accedere tramite SSH al nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="f57f1-348">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="f57f1-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="f57f1-349">dopo aver usato SSH passare alla directory della versione corrispondente ed eseguire sudo sulla DLL di dotnet:</span><span class="sxs-lookup"><span data-stu-id="f57f1-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="f57f1-350">Per Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="f57f1-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="f57f1-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0 sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="f57f1-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="f57f1-352">Per Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="f57f1-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="f57f1-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="f57f1-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="f57f1-354">Per configurare la messa in funzione di Microsoft R Server con una configurazione di una casella, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="f57f1-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="f57f1-355">Selezionare "Configure R Server for Operationalization" (Configurare R Server per la messa in funzione)</span><span class="sxs-lookup"><span data-stu-id="f57f1-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="f57f1-356">Selezionare "A.</span><span class="sxs-lookup"><span data-stu-id="f57f1-356">Select “A.</span></span> <span data-ttu-id="f57f1-357">One-box (web + compute nodes)” (Una casella (Web + nodi di calcolo)"</span><span class="sxs-lookup"><span data-stu-id="f57f1-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="f57f1-358">Immettere una password per l'utente **admin**</span><span class="sxs-lookup"><span data-stu-id="f57f1-358">Enter a password for the **admin** user</span></span>

![Opzione per una casella](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="f57f1-360">Come passaggio facoltativo, è possibile eseguire controlli diagnostici eseguendo un test di diagnostica, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f57f1-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="f57f1-361">Selezionare "6.</span><span class="sxs-lookup"><span data-stu-id="f57f1-361">Select “6.</span></span> <span data-ttu-id="f57f1-362">Run diagnostic tests" (Esegui test diagnostici)</span><span class="sxs-lookup"><span data-stu-id="f57f1-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="f57f1-363">Selezionare "A.</span><span class="sxs-lookup"><span data-stu-id="f57f1-363">Select “A.</span></span> <span data-ttu-id="f57f1-364">Test configuration" (Configurazione test)</span><span class="sxs-lookup"><span data-stu-id="f57f1-364">Test configuration”</span></span>
3. <span data-ttu-id="f57f1-365">Immettere nome utente = "admin" e la password del passaggio di configurazione precedente</span><span class="sxs-lookup"><span data-stu-id="f57f1-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="f57f1-366">Conferma dell'integrità complessiva = pass</span><span class="sxs-lookup"><span data-stu-id="f57f1-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="f57f1-367">Uscire dall'utilità di amministrazione</span><span class="sxs-lookup"><span data-stu-id="f57f1-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="f57f1-368">Uscire da SSH</span><span class="sxs-lookup"><span data-stu-id="f57f1-368">Exit SSH</span></span>

![Diagnostica per la messa in funzione](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="f57f1-370">**Ritardi considerevoli quando si utilizza il servizio Web in Spark**</span><span class="sxs-lookup"><span data-stu-id="f57f1-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="f57f1-371">Se si riscontrano ritardi considerevoli quando si prova a utilizzare un servizio Web creato con le funzioni mrsdeploy in un contesto di calcolo di Spark, potrebbe essere necessario aggiungere alcune cartelle mancanti.</span><span class="sxs-lookup"><span data-stu-id="f57f1-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="f57f1-372">L'applicazione Spark appartiene a un utente chiamato "*rserve2*" quando viene richiamata da un servizio Web usando le funzioni mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="f57f1-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="f57f1-373">Per risolvere questo problema:</span><span class="sxs-lookup"><span data-stu-id="f57f1-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="f57f1-374">A questo punto la configurazione per la messa in funzione è completata.</span><span class="sxs-lookup"><span data-stu-id="f57f1-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="f57f1-375">È ora possibile usare il pacchetto "mrsdeploy" in RClient per connettersi alla messa in funzione sul nodo perimetrale e iniziare a usarne le funzionalità, ad esempio l'[esecuzione remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e i [servizi Web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="f57f1-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="f57f1-376">A seconda che il cluster sia configurato o meno su una rete virtuale, potrebbe essere necessario impostare il tunneling di inoltro alla porta tramite l'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="f57f1-377">Le sezioni seguenti illustrano come configurare questo tunnel.</span><span class="sxs-lookup"><span data-stu-id="f57f1-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="f57f1-378">Cluster RServer su rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f57f1-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="f57f1-379">Verificare che sia consentito il traffico attraverso la porta 12800 verso il nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="f57f1-380">In questo modo è possibile usare tale nodo per la connessione alla funzionalità di messa in funzione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="f57f1-381">Se `remoteLogin()` non può connettersi al nodo perimetrale ma è possibile accedere a tale nodo tramite SSH, è necessario verificare se la regola che consente il traffico sulla porta 12800 è stata impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="f57f1-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="f57f1-382">Se il problema persiste, può essere risolto configurando il tunneling di port forwarding tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="f57f1-383">Per istruzioni, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="f57f1-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="f57f1-384">Cluster RServer non impostato su rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f57f1-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="f57f1-385">Se il cluster non è configurato sulla rete virtuale o si riscontrano problemi relativi alla connettività tramite la rete virtuale, è possibile usare il tunneling di port forwarding SSH:</span><span class="sxs-lookup"><span data-stu-id="f57f1-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="f57f1-386">La configurazione è possibile anche in Putty.</span><span class="sxs-lookup"><span data-stu-id="f57f1-386">On Putty, you can set it up as well.</span></span>

![Connessione SSH con Putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="f57f1-388">Quando la sessione SSH è attiva, il traffico proveniente dalla porta 12800 del computer viene inoltrato alla porta 12800 del nodo perimetrale tramite la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="f57f1-389">Assicurarsi di usare `127.0.0.1:12800` nel metodo `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="f57f1-390">Viene così eseguito l'accesso alla messa in funzione del nodo perimetrale tramite port forwarding.</span><span class="sxs-lookup"><span data-stu-id="f57f1-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="f57f1-391">Procedura per ridimensionare i nodi di calcolo della messa in funzione di Microsoft R Server nei nodi del ruolo di lavoro di HDInsight</span><span class="sxs-lookup"><span data-stu-id="f57f1-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="f57f1-392">Rimuovere le autorizzazioni dei nodi del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="f57f1-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="f57f1-393">Attualmente Microsoft R Server non è gestito tramite Yarn.</span><span class="sxs-lookup"><span data-stu-id="f57f1-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="f57f1-394">Se è necessario rimuovere le autorizzazioni dei nodi del ruolo di lavoro, Yarn Resource Manager non funzionerà come previsto in quanto non sarà in grado di riconoscere le risorse impiegate dal server.</span><span class="sxs-lookup"><span data-stu-id="f57f1-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="f57f1-395">Per evitare questa situazione, è consigliabile rimuovere le autorizzazioni dei nodi del ruolo di lavoro prima di ridimensionare i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f57f1-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="f57f1-396">Passaggi per la rimozione delle autorizzazioni dei nodi del ruolo di lavoro:</span><span class="sxs-lookup"><span data-stu-id="f57f1-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="f57f1-397">Accedere alla console Ambari del cluster HDI e fare clic sulla scheda "Host"</span><span class="sxs-lookup"><span data-stu-id="f57f1-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="f57f1-398">Selezionare i nodi del ruolo di lavoro di cui rimuovere le autorizzazioni e fare clic su "Actions" (Azioni) > "Selected Hosts" (Host selezionati) > "Host" > e infine su "Turn ON Maintenance Mode" (Attiva modalità di manutenzione).</span><span class="sxs-lookup"><span data-stu-id="f57f1-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="f57f1-399">Ad esempio nell'immagine seguente i nodi selezionati per la rimozione delle autorizzazioni sono wn3 e wn4.</span><span class="sxs-lookup"><span data-stu-id="f57f1-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="f57f1-401">Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Decommission** (Rimuovi autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="f57f1-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="f57f1-402">Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Decommission** (Rimuovi autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="f57f1-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="f57f1-403">Selezionare **Actions** > **Selected Hosts** > **DataNodes** > fare clic su **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="f57f1-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="f57f1-404">Selezionare **Actions** > **Selected Hosts** > **NodeManagers** > fare clic su **Stop** (Arresta).</span><span class="sxs-lookup"><span data-stu-id="f57f1-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="f57f1-405">Selezionare **Actions** > **Selected Hosts** > **Hosts** > fare clic su **Stop All Components** (Arresta tutti i componenti).</span><span class="sxs-lookup"><span data-stu-id="f57f1-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="f57f1-406">Deselezionare i nodi del ruolo di lavoro e selezionare i nodi head.</span><span class="sxs-lookup"><span data-stu-id="f57f1-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="f57f1-407">Selezionare **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components** (Riavvia tutti i componenti).</span><span class="sxs-lookup"><span data-stu-id="f57f1-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="f57f1-408">Configurare i nodi di calcolo su ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione</span><span class="sxs-lookup"><span data-stu-id="f57f1-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="f57f1-409">Accedere tramite SSH a ogni nodo del ruolo di lavoro per il quale è stata rimossa l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="f57f1-410">Eseguire l'utilità di amministrazione con `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="f57f1-411">Immettere "1" per selezionare l'opzione "Configure R Server for Operationalization" (Configurare R Server per la messa in funzione).</span><span class="sxs-lookup"><span data-stu-id="f57f1-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="f57f1-412">Immettere "c" per selezionare l'opzione "C.</span><span class="sxs-lookup"><span data-stu-id="f57f1-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="f57f1-413">Compute node" (Nodo di calcolo).</span><span class="sxs-lookup"><span data-stu-id="f57f1-413">Compute node".</span></span> <span data-ttu-id="f57f1-414">Il nodo di calcolo viene configurato sul nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="f57f1-415">Uscire dall'utilità di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="f57f1-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="f57f1-416">Aggiungere i dettagli dei nodi di calcolo nel nodo Web</span><span class="sxs-lookup"><span data-stu-id="f57f1-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="f57f1-417">Dopo che tutti i nodi di lavoro per i quali è stata rimossa l'autorizzazione sono stati configurati per l'esecuzione del nodo di calcolo, tornare al nodo perimetrale e aggiungere gli indirizzi IP di tali nodi di lavoro nella configurazione del nodo Web Microsoft R Server:</span><span class="sxs-lookup"><span data-stu-id="f57f1-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="f57f1-418">Accedere tramite SSH al nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="f57f1-418">SSH into the edge node.</span></span>
* <span data-ttu-id="f57f1-419">Eseguire `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="f57f1-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="f57f1-420">Individuare la sezione dell'URI e aggiungere i dettagli relativi alla porta e all'IP del nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f57f1-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![Rimozione delle autorizzazioni dei nodi del ruolo di lavoro con la riga di comando](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="f57f1-422">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f57f1-422">Troubleshoot</span></span>

<span data-ttu-id="f57f1-423">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f57f1-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f57f1-424">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f57f1-424">Next steps</span></span>

<span data-ttu-id="f57f1-425">A questo punto dovrebbe essere chiaro come creare un nuovo cluster HDInsight che includa R Server, comprese le nozioni di base sull'uso della console di R da una sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="f57f1-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="f57f1-426">Gli argomenti seguenti illustrano altre modalità di gestione e uso di R Server in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f57f1-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="f57f1-427">Aggiungere RStudio Server a HDInsight (se non installato durante la creazione del cluster)</span><span class="sxs-lookup"><span data-stu-id="f57f1-427">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="f57f1-428">Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="f57f1-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="f57f1-429">Opzioni di Archiviazione di Azure per R Server su HDInsight</span><span class="sxs-lookup"><span data-stu-id="f57f1-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
