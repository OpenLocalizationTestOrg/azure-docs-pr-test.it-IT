---
title: Personalizzare i cluster Hadoop per l'analisi scientifica dei dati per i team | Documentazione Microsoft
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="1a087-103">Personalizzare i cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati per i team</span><span class="sxs-lookup"><span data-stu-id="1a087-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="1a087-104">Questo articolo descrive come personalizzare un cluster Hadoop di HDInsight mediante l'installazione di Anaconda a 64 bit (Python 2.7) in ogni nodo quando viene eseguito il provisioning del cluster come servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a087-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="1a087-105">L'articolo illustra inoltre come accedere al nodo head per inviare i processi personalizzati al cluster.</span><span class="sxs-lookup"><span data-stu-id="1a087-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="1a087-106">Questa personalizzazione rende molti moduli Python comuni, che sono inclusi in Anaconda, facilmente disponibili per l'uso nelle funzioni definite dall'utente (UDF) progettate per elaborare i record di Hive nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1a087-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="1a087-107">Per le istruzioni sulle procedure impiegate in questo scenario, vedere [Come inviare query Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="1a087-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="1a087-108">Il menu seguente include collegamenti ad argomenti che descrivono come configurare i diversi ambienti di analisi scientifica dei dati usati dal [processo di analisi scientifica dei dati per i team](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a087-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="1a087-109"><a name="customize"></a>Personalizzare i cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a087-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="1a087-110">Per creare un cluster Hadoop di HDInsight personalizzato, accedere innanzitutto al [**portale di Azure classico**](https://manage.windowsazure.com/), fare clic su **Nuovo** nell'angolo inferiore sinistro e quindi selezionare SERVIZI DATI -> HDINSIGHT -> **CREAZIONE PERSONALIZZATA** per visualizzare la finestra **Dettagli cluster**.</span><span class="sxs-lookup"><span data-stu-id="1a087-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="1a087-112">Immettere il nome del cluster da creare nella pagina 1 della configurazione e accettare i valori predefiniti per gli altri campi.</span><span class="sxs-lookup"><span data-stu-id="1a087-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="1a087-113">Fare clic sulla freccia per passare alla pagina di configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="1a087-113">Click the arrow to go to the next configuration page.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="1a087-115">Nella pagina 2 della configurazione, immettere il numero di **NODI DEI DATI**, selezionare **RETE LOCALE/VIRTUALE**, quindi selezionare le dimensioni del **NODO HEAD** e del **NODO DATI**.</span><span class="sxs-lookup"><span data-stu-id="1a087-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="1a087-116">Fare clic sulla freccia per passare alla pagina di configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="1a087-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="1a087-117">La **RETE LOCALE/VIRTUALE** deve corrispondere all'area dell'account di archiviazione che verrà usato per il cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a087-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1a087-118">In caso contrario, nella quarta pagina della configurazione, l'account di archiviazione non verrà visualizzato nell'elenco a discesa **NOME ACCOUNT**.</span><span class="sxs-lookup"><span data-stu-id="1a087-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="1a087-120">Nella pagina di configurazione 3, fornire un nome utente e una password per il cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a087-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1a087-121">**Non** selezionare *Immettere metastore Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="1a087-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="1a087-122">Quindi, fare clic sulla freccia per passare alla pagina di configurazione successiva.</span><span class="sxs-lookup"><span data-stu-id="1a087-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="1a087-124">Nella pagina di configurazione 4, specificare il nome dell'account di archiviazione, il contenitore predefinito del cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a087-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1a087-125">Se si seleziona *Crea contenitore predefinito* dall'elenco a discesa **CONTENITORE PREDEFINITO**, verrà creato un contenitore con lo stesso nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="1a087-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="1a087-126">Fare clic sulla freccia per passare all'ultima pagina di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1a087-126">Click the arrow to go to the last configuration page.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="1a087-128">Nell'ultima pagina di configurazione **Azioni script**, fare clic sul pulsante **aggiungi script azione** e compilare i campi di testo con i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="1a087-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="1a087-129">**NOME**: qualsiasi stringa con il nome dell'azione script</span><span class="sxs-lookup"><span data-stu-id="1a087-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="1a087-130">**TIPO DI NODO**: selezionare **Tutti i nodi**</span><span class="sxs-lookup"><span data-stu-id="1a087-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="1a087-131">**URI SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="1a087-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="1a087-132">*publicscripts* è un contenitore pubblico nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1a087-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="1a087-133">*getgoing* viene usato per condividere file di script di PowerShell per facilitare agli utenti l'uso di Azure</span><span class="sxs-lookup"><span data-stu-id="1a087-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="1a087-134">**PARAMETRI**: lasciare vuoto</span><span class="sxs-lookup"><span data-stu-id="1a087-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="1a087-135">Infine, selezionare il segno di spunta per avviare la creazione del cluster Hadoop di HDInsight personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1a087-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="1a087-137"><a name="headnode"></a> Accedere al nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="1a087-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="1a087-138">È necessario abilitare l'accesso remoto al cluster Hadoop in Azure prima di poter accedere al nodo head del cluster Hadoop tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="1a087-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="1a087-139">Accedere al [**portale di Azure classico**](https://manage.windowsazure.com/), selezionare **HDInsight** a sinistra, selezionare il cluster Hadoop nell'elenco dei cluster, fare clic sulla scheda **CONFIGURAZIONE** e quindi fare clic sull'icona **ABILITA MODALITÀ REMOTA** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="1a087-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="1a087-141">Nella finestra **Configura desktop remoto** compilare i campi NOME UTENTE e PASSWORD e quindi selezionare la data di scadenza dell'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="1a087-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="1a087-142">Quindi fare clic sul segno di spunta per abilitare l'accesso remoto al nodo head del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a087-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="1a087-144">Il nome utente e la password per l'accesso remoto non sono il nome utente e la password usati per la creazione del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a087-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="1a087-145">Si tratta di un set separato di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a087-145">This is a separate set of credentials.</span></span> <span data-ttu-id="1a087-146">Inoltre, la data di scadenza dell'accesso remoto non deve superare i 7 giorni dalla data corrente.</span><span class="sxs-lookup"><span data-stu-id="1a087-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="1a087-147">Dopo aver abilitato l'accesso remoto, fare clic su **CONNETTI** nella parte inferiore della pagina per accedere in remoto al nodo head.</span><span class="sxs-lookup"><span data-stu-id="1a087-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="1a087-148">Si accede al nodo head del cluster Hadoop immettendo le credenziali per l'utente di accesso remoto specificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a087-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="1a087-150">I passaggi successivi del processo di analisi avanzata dei dati sono illustrati in [Processo di analisi scientifica dei dati per i team](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere lo spostamento dei dati in HDInsight e le successive procedure di elaborazione e campionamento in preparazione dell'apprendimento dei dati con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1a087-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="1a087-151">Vedere [Come inviare query Hive](machine-learning-data-science-move-hive-tables.md#submit) per istruzioni sull'accesso ai moduli di Python inclusi in Anaconda dal nodo head del cluster nelle funzioni definite dall'utente che consentono di elaborare i record di Hive archiviati nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1a087-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

