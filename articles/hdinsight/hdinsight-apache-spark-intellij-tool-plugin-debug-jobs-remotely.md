---
title: "Azure Toolkit for IntelliJ: debug delle applicazioni in modalità remota su HDInsight Spark | Microsoft Docs"
description: Informazioni su come usare gli Strumenti HDInsight nel Toolkit di Azure per IntelliJ per il debug remoto di applicazioni in esecuzione nei cluster HDInsight Spark tramite VPN.
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="5f71d-103">Usare Azure Toolkit per IntelliJ per il debug remoto delle applicazioni su HDInsight Spark tramite VPN</span><span class="sxs-lookup"><span data-stu-id="5f71d-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="5f71d-104">È consigliabile usare la modalità di debug dell'applicazione Spark da remoto tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="5f71d-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="5f71d-105">Per istruzioni vedere [Eseguire il debug remoto delle applicazioni Spark su un cluster HDInsight con Azure Toolkit per IntelliJ tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="5f71d-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="5f71d-106">Questo articolo offre indicazioni dettagliate su come usare gli strumenti HDInsight nel Toolkit di Azure per IntelliJ per inviare un processo Spark nel cluster HDInsight Spark e quindi eseguirne il debug remoto dal computer desktop.</span><span class="sxs-lookup"><span data-stu-id="5f71d-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="5f71d-107">A tale scopo, è necessario seguire questa procedura generale:</span><span class="sxs-lookup"><span data-stu-id="5f71d-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="5f71d-108">Creare una rete virtuale di Azure da sito a sito o da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="5f71d-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="5f71d-109">Le procedure descritte in questo documento presuppongono che si usi una rete da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="5f71d-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="5f71d-110">Creare un cluster Spark in Azure HDInsight incluso nella rete virtuale da sito a sito di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f71d-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="5f71d-111">Verificare la connettività tra il nodo head del cluster e il PC desktop.</span><span class="sxs-lookup"><span data-stu-id="5f71d-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="5f71d-112">Creare un'applicazione Scala in IntelliJ IDEA e configurarla per il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="5f71d-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="5f71d-113">Eseguire l'applicazione ed effettuarne il debug.</span><span class="sxs-lookup"><span data-stu-id="5f71d-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f71d-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f71d-114">Prerequisites</span></span>
* <span data-ttu-id="5f71d-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f71d-115">An Azure subscription.</span></span> <span data-ttu-id="5f71d-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5f71d-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5f71d-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f71d-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5f71d-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5f71d-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="5f71d-119">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="5f71d-119">Oracle Java Development kit.</span></span> <span data-ttu-id="5f71d-120">Per installarlo, fare clic [qui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="5f71d-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="5f71d-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5f71d-121">IntelliJ IDEA.</span></span> <span data-ttu-id="5f71d-122">In questo articolo viene usata la versione 2017.1.</span><span class="sxs-lookup"><span data-stu-id="5f71d-122">This article uses version 2017.1.</span></span> <span data-ttu-id="5f71d-123">Per installarlo, fare clic [qui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="5f71d-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="5f71d-124">Strumenti HDInsight nel Toolkit di Azure per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5f71d-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5f71d-125">Gli strumenti HDInsight per IntelliJ sono disponibili come parte di Azure Toolkit per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5f71d-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5f71d-126">Per istruzioni su come installare Azure Toolkit, vedere [Installazione di Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="5f71d-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="5f71d-127">Accedere alla propria sottoscrizione di Azure da IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5f71d-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="5f71d-128">Seguire le istruzioni riportate [qui](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="5f71d-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="5f71d-129">Quando si esegue l'applicazione Spark in Scala per il debug remoto in un computer Windows, potrebbe essere restituita un'eccezione, come illustrato in [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) , causata da un file WinUtils.exe mancante in Windows.</span><span class="sxs-lookup"><span data-stu-id="5f71d-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="5f71d-130">Per risolvere questo errore, è necessario [scaricare il file eseguibile da qui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) in un percorso come **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="5f71d-131">È quindi necessario aggiungere una variabile di ambiente **HADOOP_HOME** e impostare il valore della variabile su **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="5f71d-132">Passaggio 1: Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5f71d-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="5f71d-133">Seguire le istruzioni riportate nei collegamenti seguenti per creare una rete virtuale di Azure e quindi verificare la connettività tra il PC desktop e la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f71d-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="5f71d-134">Creare una rete virtuale con una connessione VPN da sito a sito tramite il portale di Azure e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f71d-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="5f71d-135">Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f71d-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="5f71d-136">Configurare una connessione da punto a sito a una rete virtuale con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f71d-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="5f71d-137">Passaggio 2: Creare un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5f71d-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="5f71d-138">È consigliabile creare anche un cluster Apache Spark in Azure HDInsight incluso nella rete virtuale di Azure creata.</span><span class="sxs-lookup"><span data-stu-id="5f71d-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="5f71d-139">Usare le informazioni disponibili in [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5f71d-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5f71d-140">Nell'ambito della configurazione facoltativa, selezionare la rete virtuale di Azure creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="5f71d-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="5f71d-141">Passaggio 3: Verificare la connettività tra il nodo head del cluster e il PC desktop</span><span class="sxs-lookup"><span data-stu-id="5f71d-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="5f71d-142">Ottenere l'indirizzo IP del nodo head.</span><span class="sxs-lookup"><span data-stu-id="5f71d-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="5f71d-143">Aprire l'interfaccia utente di Ambari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="5f71d-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="5f71d-144">Dal pannello del cluster fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-144">From the cluster blade, click **Dashboard**.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="5f71d-146">Nell'angolo superiore destro dell'interfaccia utente di Ambari fare clic su **Hosts**(Host).</span><span class="sxs-lookup"><span data-stu-id="5f71d-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="5f71d-148">Verrà visualizzato un elenco di nodi head, nodi del ruolo di lavoro e nodi zookeeper.</span><span class="sxs-lookup"><span data-stu-id="5f71d-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="5f71d-149">I nodi head hanno il prefisso **hn***.</span><span class="sxs-lookup"><span data-stu-id="5f71d-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="5f71d-150">Fare clic sul primo nodo head.</span><span class="sxs-lookup"><span data-stu-id="5f71d-150">Click the first headnode.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="5f71d-152">Nella parte inferiore della pagina visualizzata copiare l'indirizzo IP del nodo head e il nome host dalla casella **Summary** (Riepilogo).</span><span class="sxs-lookup"><span data-stu-id="5f71d-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![Individuazione dell'indirizzo IP del nodo head](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="5f71d-154">Includere l'indirizzo IP e il nome host del nodo head nel file **hosts** nel computer in cui si vuole eseguire i processi Spark ed effettuarne il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="5f71d-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="5f71d-155">Sarà così possibile comunicare con il nodo head usando sia l'indirizzo IP che il nome host.</span><span class="sxs-lookup"><span data-stu-id="5f71d-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="5f71d-156">Aprire un blocco note con autorizzazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="5f71d-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="5f71d-157">Scegliere **Apri** dal menu File e quindi passare al percorso del file hosts.</span><span class="sxs-lookup"><span data-stu-id="5f71d-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="5f71d-158">In un computer Windows è `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="5f71d-159">Aggiungere quanto riportato di seguito al file **hosts** .</span><span class="sxs-lookup"><span data-stu-id="5f71d-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="5f71d-160">Nel computer che è stato connesso alla rete virtuale di Azure usata dal cluster HDInsight verificare che sia possibile effettuare il ping di entrambi i nodi head usando sia l'indirizzo IP che il nome host.</span><span class="sxs-lookup"><span data-stu-id="5f71d-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="5f71d-161">Connettersi con SSH al nodo head del cluster seguendo le istruzioni riportate in [Connettersi a un cluster HDInsight basato su Linux](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5f71d-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="5f71d-162">Dal nodo head del cluster effettuare il ping dell'indirizzo IP del computer desktop.</span><span class="sxs-lookup"><span data-stu-id="5f71d-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="5f71d-163">È consigliabile testare la connettività per entrambi gli indirizzi IP assegnati al computer, uno per la connessione di rete e l'altro per la rete virtuale di Azure a cui il computer è connesso.</span><span class="sxs-lookup"><span data-stu-id="5f71d-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="5f71d-164">Ripetere questi passaggi anche per l'altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="5f71d-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="5f71d-165">Passaggio 4: Creare un'applicazione Spark in Scala usando gli strumenti HDInsight nel Toolkit di Azure per IntelliJ e configurarla per il debug remoto</span><span class="sxs-lookup"><span data-stu-id="5f71d-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="5f71d-166">Avviare IntelliJ IDEA e creare un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="5f71d-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="5f71d-167">Nella finestra di dialogo del nuovo progetto selezionare le opzioni seguenti e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="5f71d-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Creazione di un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="5f71d-169">Selezionare **HDInsight** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="5f71d-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="5f71d-170">Selezionare **Spark on HDInsight (Scala)**(Spark in HDInsight - Scala) nel riquadro destro.</span><span class="sxs-lookup"><span data-stu-id="5f71d-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="5f71d-171">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-171">Click **Next**.</span></span>
2. <span data-ttu-id="5f71d-172">Nella finestra successiva inserire i dettagli di progetto seguenti e quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="5f71d-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="5f71d-173">Specificare un nome per il progetto e il relativo percorso.</span><span class="sxs-lookup"><span data-stu-id="5f71d-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="5f71d-174">Per **Project SDK**, usare Java 1.8 per cluster Spark 2.x, Java 1.7 per cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="5f71d-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="5f71d-175">Per la **Versione di Spark**, la creazione guidata del progetto Scala integra la versione corretta per Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="5f71d-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="5f71d-176">Se la versione del cluster Spark è inferiore a 2.0, scegliere Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="5f71d-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="5f71d-177">In caso contrario, selezionare Spark 2.x.</span><span class="sxs-lookup"><span data-stu-id="5f71d-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="5f71d-178">In questo esempio viene usata la versione Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="5f71d-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="5f71d-179">![Creare un'applicazione Spark in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="5f71d-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="5f71d-180">Il progetto Spark creerà automaticamente un elemento.</span><span class="sxs-lookup"><span data-stu-id="5f71d-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="5f71d-181">Per visualizzare l'elemento, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="5f71d-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="5f71d-182">Scegliere **Project Structure** (Struttura progetto) dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="5f71d-183">Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Artifacts** (Elementi) per visualizzare l'elemento predefinito creato.</span><span class="sxs-lookup"><span data-stu-id="5f71d-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="5f71d-184">![Creare un file con estensione jar](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="5f71d-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="5f71d-185">È anche possibile creare un elemento personalizzato facendo clic sull'icona **+** evidenziata nell'immagine precedente.</span><span class="sxs-lookup"><span data-stu-id="5f71d-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="5f71d-186">Aggiungere librerie al progetto.</span><span class="sxs-lookup"><span data-stu-id="5f71d-186">Add libraries to your project.</span></span> <span data-ttu-id="5f71d-187">Per aggiungere una libreria, fare clic con il pulsante destro del mouse sul nome del progetto nell'albero del progetto e quindi scegliere **Open Module Settings**(Apri impostazioni modulo).</span><span class="sxs-lookup"><span data-stu-id="5f71d-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="5f71d-188">Nella finestra di dialogo **Project Structure** (Struttura progetto) fare clic su **Libraries** (Librerie) nel riquadro sinistro, quindi sul simbolo (+) e infine su **From Maven** (Da Maven).</span><span class="sxs-lookup"><span data-stu-id="5f71d-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![Aggiunta di una libreria](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="5f71d-190">Nella finestra di dialogo **Download Library from Maven Repository** (Scarica libreria da repository Maven) cercare e aggiungere le librerie seguenti.</span><span class="sxs-lookup"><span data-stu-id="5f71d-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="5f71d-191">Copiare `yarn-site.xml` e `core-site.xml` dal nodo head del cluster e aggiungerli al progetto.</span><span class="sxs-lookup"><span data-stu-id="5f71d-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="5f71d-192">Per copiare i file, usare i comandi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5f71d-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="5f71d-193">Per copiare i file dai nodi head del cluster è possibile usare [Cygwin](https://cygwin.com/install.html) per eseguire i comandi `scp` seguenti.</span><span class="sxs-lookup"><span data-stu-id="5f71d-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="5f71d-194">Poiché gli indirizzi IP e i nomi host dei nodi head del cluster sono già stati aggiunti al file hosts nel PC desktop, si possono usare i comandi **scp** nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="5f71d-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="5f71d-195">Aggiungere questi file al progetto copiandoli nella cartella **/src** dell'albero del progetto, ad esempio `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="5f71d-196">Aggiornare `core-site.xml` per apportare le modifiche seguenti.</span><span class="sxs-lookup"><span data-stu-id="5f71d-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="5f71d-197">`core-site.xml` include la chiave crittografata per l'account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="5f71d-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="5f71d-198">Nel file `core-site.xml` aggiunto al progetto, sostituire la chiave crittografata con la chiave di archiviazione effettiva associata all'account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="5f71d-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="5f71d-199">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5f71d-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="5f71d-200">Rimuovere le voci seguenti da `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="5f71d-201">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="5f71d-201">Save the file.</span></span>
7. <span data-ttu-id="5f71d-202">Aggiungere la classe principale per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f71d-202">Add the Main class for your application.</span></span> <span data-ttu-id="5f71d-203">In **Project Explorer** (Esplora progetti) fare clic con il pulsante destro del mouse su **src**, scegliere **New** (Nuovo) e quindi fare clic su **Scala class** (Classe Scala).</span><span class="sxs-lookup"><span data-stu-id="5f71d-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="5f71d-205">Nella finestra di dialogo **Create New Scala Class** (Crea nuova classe Scala) immettere un nome, selezionare **Object** (Oggetto) per il campo **Kind** (Tipologia) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Aggiunta di un codice sorgente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="5f71d-207">Incollare il codice seguente nel file `MyClusterAppMain.scala` .</span><span class="sxs-lookup"><span data-stu-id="5f71d-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="5f71d-208">Questo codice crea il contesto Spark e avvia un metodo `executeJob` dall'oggetto `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="5f71d-209">Ripetere i precedenti passaggi 8 e 9 per aggiungere un nuovo oggetto Scala denominato `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="5f71d-210">Aggiungere il codice seguente a questa classe.</span><span class="sxs-lookup"><span data-stu-id="5f71d-210">To this class add the following code.</span></span> <span data-ttu-id="5f71d-211">Questo codice legge i dati dal file HVAC.csv, disponibile in tutti i cluster HDInsight Spark, recupera le righe con una sola cifra nella settima colonna del file CSV e scrive l'output in **/HVACOut** nel contenitore di archiviazione predefinito per il cluster.</span><span class="sxs-lookup"><span data-stu-id="5f71d-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="5f71d-212">Ripetere i precedenti passaggi 8 e 9 per aggiungere una nuova classe denominata `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="5f71d-213">Questa classe implementa il framework di test Spark usato per il debug delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5f71d-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="5f71d-214">Aggiungere il codice seguente alla classe `RemoteClusterDebugging` .</span><span class="sxs-lookup"><span data-stu-id="5f71d-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="5f71d-215">Alcuni aspetti importanti da notare:</span><span class="sxs-lookup"><span data-stu-id="5f71d-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="5f71d-216">Per `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, verificare che il file JAR dell'assembly Spark sia disponibile nell'archiviazione cluster al percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="5f71d-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="5f71d-217">Per `setJars`, specificare il percorso in cui verrà creato il file JAR dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="5f71d-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="5f71d-218">In genere è `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="5f71d-219">Nella classe `RemoteClusterDebugging` fare clic con il pulsante destro del mouse sulla parola chiave `test` e scegliere **Create RemoteClusterDebugging Configuration** (Crea configurazione RemoteClusterDebugging).</span><span class="sxs-lookup"><span data-stu-id="5f71d-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="5f71d-221">Nella finestra di dialogo specificare un nome per la configurazione e selezionare **Test name** (Nome test) come **Test kind** (Tipologia test).</span><span class="sxs-lookup"><span data-stu-id="5f71d-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="5f71d-222">Mantenere l'impostazione predefinita per tutti gli altri valori, fare clic su **Apply** (Applica) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="5f71d-224">Nella barra dei menu verrà ora visualizzato un menu a discesa della configurazione **Remote Run** (Esecuzione remota).</span><span class="sxs-lookup"><span data-stu-id="5f71d-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![Creazione della configurazione remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="5f71d-226">Passaggio 5: Eseguire l'applicazione in modalità di debug</span><span class="sxs-lookup"><span data-stu-id="5f71d-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="5f71d-227">Nel progetto IntelliJ IDEA aprire `SparkSample.scala` e creare un punto di interruzione accanto a "val rdd1".</span><span class="sxs-lookup"><span data-stu-id="5f71d-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="5f71d-228">Nel menu a comparsa per la creazione di un punto di interruzione selezionare **line in function executeJob**(riga in funzione executeJob).</span><span class="sxs-lookup"><span data-stu-id="5f71d-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Aggiunta di un punto di interruzione](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="5f71d-230">Fare clic sul pulsante **Debug Run** (Esecuzione debug) accanto al menu a discesa della configurazione **Remote Run** (Esecuzione remota) per avviare l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f71d-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="5f71d-232">Quando l'esecuzione del programma raggiunge il punto di interruzione, nel riquadro inferiore verrà visualizzata una scheda **Debugger** .</span><span class="sxs-lookup"><span data-stu-id="5f71d-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="5f71d-234">Fare clic sull'icona (**+**) per aggiungere un'espressione di controllo come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="5f71d-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="5f71d-236">Poiché l'applicazione è stata interrotta prima della creazione della variabile `rdd1`, usando questa espressione di controllo si possono visualizzare le prime 5 righe nella variabile `rdd`.</span><span class="sxs-lookup"><span data-stu-id="5f71d-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="5f71d-237">Premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="5f71d-237">Press **ENTER**.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="5f71d-239">L'immagine precedente illustra che in fase di esecuzione è possibile eseguire query su terabyte di dati e il debug dell'avanzamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f71d-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="5f71d-240">Nell'output illustrato nell'immagine precedente, ad esempio, si può osservare che la prima riga dell'output è un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="5f71d-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="5f71d-241">Sulla base di questo, è possibile modificare il codice dell'applicazione per ignorare la riga di intestazione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5f71d-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="5f71d-242">È ora possibile fare clic sull'icona **Resume Program** (Riprendi programma) per continuare l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f71d-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="5f71d-244">Se l'applicazione viene completata, verrà visualizzato un output simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="5f71d-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![Esecuzione del programma in modalità di debug](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="5f71d-246"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5f71d-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5f71d-247">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="5f71d-248">Demo</span><span class="sxs-lookup"><span data-stu-id="5f71d-248">Demo</span></span>
* <span data-ttu-id="5f71d-249">Creare il progetto Scala (video): [Creare applicazioni Spark in Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5f71d-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="5f71d-250">Debug remoto (video): [Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark nel cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5f71d-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="5f71d-251">Scenari</span><span class="sxs-lookup"><span data-stu-id="5f71d-251">Scenarios</span></span>
* [<span data-ttu-id="5f71d-252">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5f71d-253">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="5f71d-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5f71d-254">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="5f71d-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5f71d-255">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="5f71d-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="5f71d-256">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5f71d-257">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="5f71d-257">Create and run applications</span></span>
* [<span data-ttu-id="5f71d-258">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="5f71d-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5f71d-259">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="5f71d-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5f71d-260">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="5f71d-260">Tools and extensions</span></span>
* [<span data-ttu-id="5f71d-261">Usare gli strumenti HDInsight nel Toolkit di Azure per IntelliJ per creare e inviare applicazioni Spark in Scala</span><span class="sxs-lookup"><span data-stu-id="5f71d-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5f71d-262">Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite SSH</span><span class="sxs-lookup"><span data-stu-id="5f71d-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="5f71d-263">Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="5f71d-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="5f71d-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications (Usare gli strumenti HDInsight nel Toolkit di Azure per Eclipse per creare applicazioni Spark)</span><span class="sxs-lookup"><span data-stu-id="5f71d-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="5f71d-265">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5f71d-266">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5f71d-267">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="5f71d-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5f71d-268">Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5f71d-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5f71d-269">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="5f71d-269">Manage resources</span></span>
* [<span data-ttu-id="5f71d-270">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5f71d-271">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f71d-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
