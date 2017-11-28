---
title: aaaCustomize Hadoop cluster per processo di analisi scientifica dei dati di Team hello | Documenti Microsoft
description: "Moduli di Python più diffusi resi disponibili nei cluster personalizzati Hadoop di Azure HDInsight."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="9c5e6-103">Personalizzare i cluster di Azure HDInsight Hadoop per hello processo di analisi scientifica dei dati di Team</span><span class="sxs-lookup"><span data-stu-id="9c5e6-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="9c5e6-104">In questo articolo viene descritto come toocustomize un HDInsight Hadoop cluster tramite l'installazione a 64 bit Anaconda (Python 2.7) in ogni nodo quando viene eseguito il provisioning di cluster hello come un servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="9c5e6-105">Viene inoltre illustrato come tooaccess hello cluster toohello di nodo head toosubmit processi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="9c5e6-106">Questa personalizzazione rende molti moduli Python più diffusi, inclusi in Anaconda, funzioni definite (UDF) che sono facilmente disponibili per l'utilizzo in utente progettato tooprocess record Hive nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="9c5e6-107">Per istruzioni sulle procedure hello utilizzate in questo scenario, vedere [come query Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="9c5e6-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="9c5e6-108">i menu seguenti Hello collega tootopics che descrivono come tooset backup hello diversi ambienti di analisi scientifica dei dati utilizzata dal hello [Team Data Science processo (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c5e6-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="9c5e6-109"><a name="customize"></a>Personalizzare i cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c5e6-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="9c5e6-110">avviare toocreate un cluster HDInsight Hadoop personalizzato, effettuando l'accesso troppo[**portale di Azure classico**](https://manage.windowsazure.com/), fare clic su **New** nell'angolo inferiore, hello a sinistra e quindi selezionare i servizi dati -> HDINSIGHT -> **creazione personalizzata** toobring backup hello **i dettagli del Cluster** finestra.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="9c5e6-112">Immettere il nome di hello di hello cluster toobe creato nella pagina configurazione 1 e accettare i valori predefiniti per hello altri campi.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="9c5e6-113">Fare clic su hello freccia toogo toohello pagina Configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="9c5e6-115">Nella pagina configurazione 2, immettere il numero di hello di **nodi dati**selezionare hello **area/rete virtuale**e selezionare le dimensioni di hello di hello **nodo HEAD** e hello **Nodo dati**.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="9c5e6-116">Fare clic su hello freccia toogo toohello pagina Configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="9c5e6-117">Hello **area/rete virtuale** ha toobe hello stesso come area hello hello dell'account di archiviazione che verrà utilizzato per il cluster HDInsight Hadoop hello toobe.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9c5e6-118">In caso contrario, nella pagina di configurazione quarto hello, account di archiviazione hello non apparirà nell'elenco a discesa hello di **nome ACCOUNT**.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="9c5e6-120">Nella pagina Configurazione 3, fornire un nome utente e una password per hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9c5e6-121">**Non** hello seleziona *hello immettere Metastore Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="9c5e6-122">Quindi, fare clic su hello freccia toogo toohello pagina Configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="9c5e6-124">Nella pagina configurazione 4, specificare il nome di account di archiviazione hello, il contenitore predefinito hello di hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9c5e6-125">Se si seleziona *crea contenitore predefinito* in hello **contenitore predefinito** elenco a discesa, un contenitore con hello stesso nome, verrà creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="9c5e6-126">Fare clic su hello freccia toogo toohello ultima pagina di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="9c5e6-128">In hello finale **azioni Script** pagina di configurazione, fare clic su **aggiungere script azione** pulsante e compilare i campi di testo hello con i seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="9c5e6-129">**NOME** -qualsiasi stringa come nome hello di questa azione di script</span><span class="sxs-lookup"><span data-stu-id="9c5e6-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="9c5e6-130">**TIPO DI NODO**: selezionare **Tutti i nodi**</span><span class="sxs-lookup"><span data-stu-id="9c5e6-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="9c5e6-131">**URI SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="9c5e6-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="9c5e6-132">*publicscripts* è un contenitore pubblico nell'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="9c5e6-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="9c5e6-133">*getgoing* utilizziamo tooshare PowerShell script file toofacilitate il lavoro degli utenti in Azure</span><span class="sxs-lookup"><span data-stu-id="9c5e6-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="9c5e6-134">**PARAMETRI**: lasciare vuoto</span><span class="sxs-lookup"><span data-stu-id="9c5e6-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="9c5e6-135">Infine, fare clic su hello segno di spunta toostart hello la creazione di cluster HDInsight Hadoop hello personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="9c5e6-137"><a name="headnode"></a>Accedere hello nodo Head del Hadoop Cluster</span><span class="sxs-lookup"><span data-stu-id="9c5e6-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="9c5e6-138">Prima di poter accedere nodo head di hello del cluster Hadoop hello tramite RDP, è necessario abilitare cluster Hadoop toohello di accesso remoto in Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="9c5e6-139">Accedi toohello [ **portale di Azure classico**](https://manage.windowsazure.com/)selezionare **HDInsight** hello sinistra, selezionare il cluster Hadoop hello elenco di cluster, fare clic su hello  **CONFIGURAZIONE** scheda e quindi fare clic su hello **ABILITA modalità remota** icona hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="9c5e6-141">In hello **configurare Desktop remoto** finestra immettere hello nome utente e i campi PASSWORD e selezionare la data di scadenza hello per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="9c5e6-142">Quindi fare clic su hello segno di spunta tooenable hello accesso remoto toohello nodo head del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="9c5e6-144">nome utente Hello e una password per l'accesso remoto hello non sono il nome di utente hello e la password utilizzati durante la creazione di un cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="9c5e6-145">Si tratta di un set separato di credenziali.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-145">This is a separate set of credentials.</span></span> <span data-ttu-id="9c5e6-146">Data di scadenza hello di accesso remoto hello è inoltre toobe entro 7 giorni da hello data corrente.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="9c5e6-147">Dopo aver abilitato l'accesso remoto, fare clic su **CONNETTI** nella parte inferiore di hello di hello pagina tooremote nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="9c5e6-148">Toohello nodo head del cluster Hadoop hello si accede tramite l'immissione di credenziali hello per utente di accesso remoto hello specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="9c5e6-150">Hello passaggi successivi hello avanzate processo analitica vengono eseguito il mapping in hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere passaggi spostare i dati in HDInsight, quindi l'elaborazione e di esempio, in preparazione per l'apprendimento dai dati hello con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="9c5e6-151">Vedere [come query Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) per istruzioni su come tooaccess hello moduli Python inclusi in Anaconda dal nodo head di hello del cluster di hello nelle funzioni definite dall'utente (UDF) che vengono utilizzati tooprocess Hive record archiviati cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9c5e6-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

