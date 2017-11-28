---
title: "Toolkit per IntelliJ - il Debug delle applicazioni in modalità remota in HDInsight Spark aaaAzure | Documenti Microsoft"
description: Informazioni su come utilizzare gli strumenti di HDInsight in Azure Toolkit per IntelliJ tooremotely debug applicazioni in esecuzione nel cluster HDInsight Spark tramite vpn.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="6c956-103">Utilizzare Azure Toolkit per le applicazioni di toodebug IntelliJ in modalità remota in HDInsight Spark tramite VPN</span><span class="sxs-lookup"><span data-stu-id="6c956-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="6c956-104">Si consiglia di hello modalità di debug di spark applicaltion in remoto tramite ssh.</span><span class="sxs-lookup"><span data-stu-id="6c956-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="6c956-105">Per istruzioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="6c956-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="6c956-106">In questo articolo vengono fornite istruzioni dettagliate su come toouse hello gli strumenti di HDInsight in Azure Toolkit per IntelliJ toosubmit un processo di Spark nel cluster HDInsight Spark e quindi eseguire il debug in modalità remota dal computer desktop.</span><span class="sxs-lookup"><span data-stu-id="6c956-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="6c956-107">toodo in tal caso, è necessario eseguire hello seguendo i passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="6c956-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="6c956-108">Creare una rete virtuale di Azure da sito a sito o da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="6c956-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="6c956-109">passaggi di Hello in questo documento presuppongono l'utilizzo di una rete da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="6c956-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="6c956-110">Creare un cluster Spark in HDInsight di Azure che fa parte di hello site-to-site rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c956-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="6c956-111">Verificare la connettività di hello tra nodo head cluster hello e desktop.</span><span class="sxs-lookup"><span data-stu-id="6c956-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="6c956-112">Creare un'applicazione Scala in IntelliJ IDEA e configurarla per il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="6c956-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="6c956-113">Esecuzione e il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c956-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6c956-114">Prerequisites</span></span>
* <span data-ttu-id="6c956-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c956-115">An Azure subscription.</span></span> <span data-ttu-id="6c956-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6c956-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6c956-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c956-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6c956-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6c956-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="6c956-119">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6c956-119">Oracle Java Development kit.</span></span> <span data-ttu-id="6c956-120">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="6c956-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="6c956-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6c956-121">IntelliJ IDEA.</span></span> <span data-ttu-id="6c956-122">In questo articolo viene usata la versione 2017.1.</span><span class="sxs-lookup"><span data-stu-id="6c956-122">This article uses version 2017.1.</span></span> <span data-ttu-id="6c956-123">Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="6c956-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="6c956-124">Strumenti HDInsight nel Toolkit di Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="6c956-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="6c956-125">Strumenti HDInsight per IntelliJ sono disponibili come parte di Azure Toolkit per IntelliJ hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="6c956-126">Per istruzioni su come tooinstall hello Azure Toolkit, vedere [installazione hello Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="6c956-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="6c956-127">Accedere alla propria sottoscrizione di Azure da IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6c956-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="6c956-128">Seguire le istruzioni di hello [qui](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="6c956-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="6c956-129">Durante l'esecuzione dell'applicazione di Spark Scala per il debug remoto in un computer Windows, è possibile ricevere un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) che si verifica a causa di tooa mancante WinUtils.exe in Windows.</span><span class="sxs-lookup"><span data-stu-id="6c956-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="6c956-130">toowork intorno a questo errore, è necessario [scaricare qui hello eseguibile](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa percorso **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="6c956-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="6c956-131">È quindi necessario aggiungere una variabile di ambiente **HADOOP_HOME** e impostare il valore di hello della variabile hello troppo**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="6c956-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="6c956-132">Passaggio 1: Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="6c956-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="6c956-133">Seguire le istruzioni di hello da hello seguito collegamenti toocreate una rete virtuale di Azure e quindi verificare la connettività di hello tra desktop hello e rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c956-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="6c956-134">Creare una rete virtuale con una connessione VPN da sito a sito tramite il portale di Azure e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c956-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="6c956-135">Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c956-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="6c956-136">Configurare una rete virtuale tooa connessione point-to-site tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c956-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="6c956-137">Passaggio 2: Creare un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6c956-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="6c956-138">Inoltre, è necessario creare un cluster Apache Spark in HDInsight di Azure che fa parte di hello rete virtuale di Azure che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6c956-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="6c956-139">Utilizzare le informazioni di hello disponibile all'indirizzo [basati su Linux creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="6c956-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="6c956-140">Come parte della configurazione facoltativa, selezionare hello rete virtuale di Azure creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="6c956-141">Passaggio 3: Verificare la connettività di hello tra nodo head cluster hello e desktop</span><span class="sxs-lookup"><span data-stu-id="6c956-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="6c956-142">Ottenere l'indirizzo IP hello del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="6c956-143">Aprire Ambari UI per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="6c956-144">Dal Pannello di hello cluster, fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="6c956-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="6c956-146">Hello Ambari UI, nell'angolo superiore destro di hello, fare clic su **host**.</span><span class="sxs-lookup"><span data-stu-id="6c956-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="6c956-148">Verrà visualizzato un elenco di nodi head, nodi del ruolo di lavoro e nodi zookeeper.</span><span class="sxs-lookup"><span data-stu-id="6c956-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="6c956-149">Hello headnodes hanno hello **hn*** prefisso.</span><span class="sxs-lookup"><span data-stu-id="6c956-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="6c956-150">Fare clic su nodo head prima hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-150">Click hello first headnode.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="6c956-152">Nella parte inferiore di hello della pagina hello che viene aperta, da hello **riepilogo** casella Indirizzo IP di hello copia del nodo head hello e il nome host hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="6c956-154">Includere l'indirizzo IP hello e il nome host di hello di hello nodo head toohello **host** file nel computer hello in cui si desidera toorun e debug in modalità remota i processi di Spark hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="6c956-155">Ciò consentirà toocommunicate con il nodo head hello utilizzando l'indirizzo IP hello nonché hostname hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="6c956-156">Aprire un blocco note con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="6c956-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="6c956-157">Scegliere dal menu file hello **aprire** e quindi passare toohello percorso del file host hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="6c956-158">In un computer Windows è `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="6c956-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="6c956-159">Aggiungere hello seguente toohello **host** file.</span><span class="sxs-lookup"><span data-stu-id="6c956-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="6c956-160">Dal computer hello che si è connessi toohello rete virtuale di Azure che viene utilizzato dal cluster HDInsight hello, verificare che è possibile effettuare il ping entrambi headnodes hello utilizzando l'indirizzo IP hello nonché hostname hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="6c956-161">SSH nel nodo head del cluster di hello utilizzando istruzioni hello in [cluster di HDInsight tooan Connetti tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6c956-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="6c956-162">Dal nodo head del cluster di hello, eseguire il ping hello di indirizzo IP del computer desktop hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="6c956-163">È necessario testare la connettività tooboth hello assegnati indirizzi IP computer toohello, uno per la connessione di rete hello e hello altri per hello rete virtuale di Azure che hello computer è connesso.</span><span class="sxs-lookup"><span data-stu-id="6c956-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="6c956-164">Ripetere i passaggi di hello per hello altri nodo head anche.</span><span class="sxs-lookup"><span data-stu-id="6c956-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="6c956-165">Passaggio 4: Creare un'applicazione di Scala Spark usando gli strumenti di HDInsight hello in Azure Toolkit per IntelliJ e configurarlo per il debug remoto</span><span class="sxs-lookup"><span data-stu-id="6c956-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="6c956-166">Avviare IntelliJ IDEA e creare un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="6c956-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="6c956-167">In hello dialogo Nuovo progetto, rendere hello opzioni seguenti e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="6c956-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Creazione di un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="6c956-169">Nel riquadro sinistro hello selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6c956-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="6c956-170">Nel riquadro destro hello selezionare **Spark in HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="6c956-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="6c956-171">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="6c956-171">Click **Next**.</span></span>
2. <span data-ttu-id="6c956-172">Nella finestra successiva hello forniscono hello seguenti dettagli di progetto e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="6c956-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="6c956-173">Specificare un nome per il progetto e il relativo percorso.</span><span class="sxs-lookup"><span data-stu-id="6c956-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="6c956-174">Per **Project SDK**, usare Java 1.8 per cluster Spark 2.x, Java 1.7 per cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="6c956-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="6c956-175">Per la **Versione di Spark**, la creazione guidata del progetto Scala integra la versione corretta per Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="6c956-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="6c956-176">Se la versione del cluster spark hello è 2.0 inferiore, scegliere nascita 1. x.</span><span class="sxs-lookup"><span data-stu-id="6c956-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="6c956-177">In caso contrario, selezionare Spark 2.x.</span><span class="sxs-lookup"><span data-stu-id="6c956-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="6c956-178">In questo esempio viene usata la versione Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="6c956-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="6c956-179">![Creare un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="6c956-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="6c956-180">progetto Spark Hello creerà automaticamente un elemento per l'utente.</span><span class="sxs-lookup"><span data-stu-id="6c956-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="6c956-181">elemento hello toosee, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="6c956-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="6c956-182">Da hello **File** menu, fare clic su **struttura del progetto**.</span><span class="sxs-lookup"><span data-stu-id="6c956-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="6c956-183">In hello **struttura del progetto** la finestra di dialogo, fare clic su **elementi** toosee hello predefinito l'elemento viene creato.</span><span class="sxs-lookup"><span data-stu-id="6c956-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="6c956-184">![Creare un file con estensione jar](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="6c956-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="6c956-185">È inoltre possibile creare la propria artefatto bly facendo clic su hello  **+**  icona, evidenziata nell'immagine di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="6c956-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="6c956-186">Aggiungere le librerie tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="6c956-186">Add libraries tooyour project.</span></span> <span data-ttu-id="6c956-187">tooadd una libreria, fare doppio clic su nome progetto hello nella struttura di progetto hello e quindi fare clic su **aprire le impostazioni del modulo**.</span><span class="sxs-lookup"><span data-stu-id="6c956-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="6c956-188">In hello **struttura del progetto** la finestra di dialogo, nel riquadro di sinistra hello, fare clic su **librerie**, fare clic sul simbolo hello (+) e quindi fare clic su **da Maven**.</span><span class="sxs-lookup"><span data-stu-id="6c956-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Aggiunta di una libreria](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="6c956-190">In hello **Download Library dal Repository di Maven** finestra di dialogo, cercare e aggiungere hello seguenti librerie.</span><span class="sxs-lookup"><span data-stu-id="6c956-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="6c956-191">Copia `yarn-site.xml` e `core-site.xml` da hello nodo head del cluster e aggiungerla toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="6c956-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="6c956-192">Utilizzare i seguenti comandi toocopy hello file hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="6c956-193">È possibile utilizzare [Cygwin](https://cygwin.com/install.html) seguente hello toorun `scp` comandi file hello toocopy headnodes cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="6c956-194">Poiché è stata già aggiunta hello cluster nodo head IP indirizzo e i nomi host fo hello file hosts sul desktop di hello, possiamo utilizzare hello **scp** comandi nel seguente modo hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="6c956-195">Aggiungere questi file di progetto tooyour copiandoli in hello **/src** cartella nella struttura del progetto, ad esempio `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="6c956-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="6c956-196">Hello aggiornamento `core-site.xml` hello toomake dopo le modifiche.</span><span class="sxs-lookup"><span data-stu-id="6c956-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="6c956-197">`core-site.xml`include l'account di archiviazione chiavi toohello crittografato hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="6c956-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="6c956-198">In hello `core-site.xml` che è stato aggiunto progetto toohello, chiave di crittografato hello sostituire con la chiave di archiviazione effettivo hello associata con l'account di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="6c956-199">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6c956-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="6c956-200">Rimuovere hello seguendo le voci dalla hello `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="6c956-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="6c956-201">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-201">Save hello file.</span></span>
7. <span data-ttu-id="6c956-202">Aggiungere classe di hello principale per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c956-202">Add hello Main class for your application.</span></span> <span data-ttu-id="6c956-203">Da hello **Esplora progetti**, fare doppio clic su **src**, punto troppo**New**, quindi fare clic su **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="6c956-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="6c956-205">In hello **Crea nuova classe Scala** finestra di dialogo immettere un nome, per **tipo** selezionare **oggetto**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c956-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="6c956-207">In hello `MyClusterAppMain.scala` file, incollare hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="6c956-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="6c956-208">Questo codice crea il contesto di Spark hello e avvia un `executeJob` metodo hello `SparkSample` oggetto.</span><span class="sxs-lookup"><span data-stu-id="6c956-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="6c956-209">Ripetere i passaggi 8 e 9 di sopra di un nuovo oggetto di Scala denominato tooadd `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="6c956-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="6c956-210">classe toothis aggiungere hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="6c956-210">toothis class add hello following code.</span></span> <span data-ttu-id="6c956-211">Questo codice legge i dati di hello da hello HVAC.csv (disponibile in tutti i cluster HDInsight Spark), recupera le righe hello solo con una cifra nella colonna settimo hello hello CSV e scrive l'output di hello troppo**/HVACOut** in predefinito hello contenitore di archiviazione per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="6c956-212">Ripetere i passaggi 8 e 9 di sopra di una nuova classe denominata tooadd `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="6c956-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="6c956-213">Questa classe implementa framework di test di Spark hello che viene utilizzato per il debug di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c956-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="6c956-214">Aggiungere i seguenti toohello codice hello `RemoteClusterDebugging` classe.</span><span class="sxs-lookup"><span data-stu-id="6c956-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="6c956-215">Alcuni aspetti importanti toonote qui:</span><span class="sxs-lookup"><span data-stu-id="6c956-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="6c956-216">Per `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, assicurarsi che sia disponibile nell'archiviazione cluster hello nel percorso specificato hello hello assembly Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="6c956-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="6c956-217">Per `setJars`, specificare il percorso di hello in cui verranno creati file jar di elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="6c956-218">In genere è `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="6c956-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="6c956-219">In hello `RemoteClusterDebugging` classe destro del mouse su hello `test` (parola chiave) e selezionare **Crea configurazione RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="6c956-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="6c956-221">Nella finestra di dialogo hello, specificare un nome per la configurazione di hello e selezionare hello **Test tipo** come **nome Test**.</span><span class="sxs-lookup"><span data-stu-id="6c956-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="6c956-222">Mantenere l'impostazione predefinita per tutti gli altri valori, fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c956-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="6c956-224">Verrà visualizzato un **remoto eseguire** configurazione elenco a discesa nella barra dei menu hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="6c956-226">Passaggio 5: Esecuzione di un'applicazione hello in modalità debug</span><span class="sxs-lookup"><span data-stu-id="6c956-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="6c956-227">Nel progetto IntelliJ IDEA, aprire `SparkSample.scala` e creare un rdd1 too'val successivo punto di interruzione '.</span><span class="sxs-lookup"><span data-stu-id="6c956-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="6c956-228">Nel menu a comparsa hello per la creazione di un punto di interruzione, selezionare **riga nella funzione executeJob**.</span><span class="sxs-lookup"><span data-stu-id="6c956-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Aggiunta di un punto di interruzione](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="6c956-230">Fare clic su hello **Debug eseguire** pulsante Avanti toohello **remoto eseguire** toostart elenco a discesa configurazione in esecuzione un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="6c956-232">Quando l'esecuzione del programma hello raggiunge il punto di interruzione hello, vedrai un **Debugger** scheda nel riquadro inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="6c956-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="6c956-234">Fare clic su hello (**+**) tooadd icona un'espressione di controllo come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="6c956-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="6c956-236">In questo caso, perché si è interrotta un'applicazione hello prima variabile hello `rdd1` è stato creato, utilizzando questa espressione di controllo è possibile vedere quali sono hello prime 5 righe nella variabile hello `rdd`.</span><span class="sxs-lookup"><span data-stu-id="6c956-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="6c956-237">Premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="6c956-237">Press **ENTER**.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="6c956-239">Ciò che viene visualizzato nell'immagine di hello sopra è in fase di esecuzione, è possibile eseguire una query terrabytes dei dati e di debug come l'avanzamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c956-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="6c956-240">Ad esempio, nell'output di hello illustrato nell'immagine di hello precedente, si noterà che hello prima riga dell'output di hello è un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="6c956-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="6c956-241">In base a ciò, è possibile modificare la riga di intestazione hello tooskip codice di applicazione se necessario.</span><span class="sxs-lookup"><span data-stu-id="6c956-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="6c956-242">È ora possibile fare clic su hello **programma Resume** tooproceed icona con l'applicazione di eseguire.</span><span class="sxs-lookup"><span data-stu-id="6c956-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="6c956-244">Se un'applicazione hello viene completata correttamente, verrà visualizzato un output simile hello seguente.</span><span class="sxs-lookup"><span data-stu-id="6c956-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Eseguire il programma di hello in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="6c956-246"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6c956-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="6c956-247">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="6c956-248">Demo</span><span class="sxs-lookup"><span data-stu-id="6c956-248">Demo</span></span>
* <span data-ttu-id="6c956-249">Creare il progetto Scala (video): [Creare applicazioni Spark in Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6c956-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="6c956-250">Eseguire il Debug remoto (Video): [utilizzare Azure Toolkit per le applicazioni in modalità remota nel HDInsight Cluster Spark toodebug IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6c956-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="6c956-251">Scenari</span><span class="sxs-lookup"><span data-stu-id="6c956-251">Scenarios</span></span>
* [<span data-ttu-id="6c956-252">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6c956-253">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="6c956-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6c956-254">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="6c956-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6c956-255">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="6c956-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6c956-256">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6c956-257">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="6c956-257">Create and run applications</span></span>
* [<span data-ttu-id="6c956-258">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="6c956-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6c956-259">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="6c956-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6c956-260">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="6c956-260">Tools and extensions</span></span>
* [<span data-ttu-id="6c956-261">Utilizzare gli strumenti di HDInsight in Azure Toolkit per IntelliJ toocreate e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="6c956-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6c956-262">Utilizzare Azure Toolkit per le applicazioni in modalità remota tramite SSH Spark toodebug IntelliJ</span><span class="sxs-lookup"><span data-stu-id="6c956-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="6c956-263">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="6c956-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="6c956-264">Utilizzare gli strumenti di HDInsight in Azure Toolkit per le applicazioni di Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="6c956-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="6c956-265">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="6c956-266">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6c956-267">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="6c956-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6c956-268">Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan</span><span class="sxs-lookup"><span data-stu-id="6c956-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6c956-269">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="6c956-269">Manage resources</span></span>
* [<span data-ttu-id="6c956-270">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="6c956-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6c956-271">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c956-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
