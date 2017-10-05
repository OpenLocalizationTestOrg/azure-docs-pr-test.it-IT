---
title: Usare il tunneling SSH per accedere ad Azure HDInsight | Microsoft Docs
description: Informazioni su come utilizzare un tunnel SSH per esplorare in modo sicuro le risorse web ospitate sui nodi HDInsight basati su Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="a44ea-103">Usare il tunneling SSH per accedere all'interfaccia utente Web di Ambari, JobHistory, NameNode, Oozie e altre interfacce utente Web</span><span class="sxs-lookup"><span data-stu-id="a44ea-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="a44ea-104">I cluster HDInsight basati su Linux forniscono l’accesso all’interfaccia web di Ambari su internet, ma alcune funzionalità dell’interfaccia utente non ci sono.</span><span class="sxs-lookup"><span data-stu-id="a44ea-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="a44ea-105">Ad esempio, l'interfaccia utente web per altri servizi che vengono rilevati tramite Ambari.</span><span class="sxs-lookup"><span data-stu-id="a44ea-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="a44ea-106">Per la funzionalità completa dell'interfaccia utente web di Ambari, è necessario utilizzare un tunnel SSH all’head del cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="a44ea-107">Perché usare un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="a44ea-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="a44ea-108">Diversi menu di Ambari funzionano solo con un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="a44ea-109">Questi menu si basano su servizi e siti Web in esecuzione in altri tipi di nodi, ad esempio i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a44ea-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="a44ea-110">Spesso questi siti web non sono protetti, pertanto non è opportuno esporli direttamente su internet.</span><span class="sxs-lookup"><span data-stu-id="a44ea-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="a44ea-111">Le interfacce utente Web seguenti richiedono un tunnel SSH:</span><span class="sxs-lookup"><span data-stu-id="a44ea-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="a44ea-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="a44ea-112">JobHistory</span></span>
* <span data-ttu-id="a44ea-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="a44ea-113">NameNode</span></span>
* <span data-ttu-id="a44ea-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="a44ea-114">Thread Stacks</span></span>
* <span data-ttu-id="a44ea-115">Interfaccia utente Web di Oozie</span><span class="sxs-lookup"><span data-stu-id="a44ea-115">Oozie web UI</span></span>
* <span data-ttu-id="a44ea-116">HBase Master e l'interfaccia utente di Log</span><span class="sxs-lookup"><span data-stu-id="a44ea-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="a44ea-117">Se si usano azioni script per personalizzare il cluster, tutti i servizi o le utilità installate che espongono un'interfaccia utente Web richiedono un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="a44ea-118">Ad esempio, se si installa Hue utilizzando un'azione di Script, è necessario utilizzare un tunnel SSH per accedere all'interfaccia utente web di Hue.</span><span class="sxs-lookup"><span data-stu-id="a44ea-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a44ea-119">Se si ha accesso diretto a HDInsight tramite una rete virtuale, non è necessario usare tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="a44ea-120">Per un esempio di accesso diretto a HDInsight tramite una rete virtuale, vedere il documento [Connettere HDInsight alla rete locale](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="a44ea-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="a44ea-121">Che cos'è un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="a44ea-121">What is an SSH tunnel</span></span>

<span data-ttu-id="a44ea-122">Il [tunneling Secure Shell (SSH)](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) instrada il traffico inviato a una porta nella workstation locale.</span><span class="sxs-lookup"><span data-stu-id="a44ea-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="a44ea-123">Il traffico viene instradato tramite una connessione SSH al nodo head del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a44ea-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="a44ea-124">La richiesta viene risolta come se fosse stata originata nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="a44ea-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="a44ea-125">La risposta viene instradata attraverso il tunnel alla workstation in uso.</span><span class="sxs-lookup"><span data-stu-id="a44ea-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a44ea-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a44ea-126">Prerequisites</span></span>

* <span data-ttu-id="a44ea-127">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-127">An SSH client.</span></span> <span data-ttu-id="a44ea-128">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a44ea-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="a44ea-129">Un Web browser che può essere configurato per l'uso di un proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="a44ea-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="a44ea-130">Il supporto per il proxy SOCKS integrato in Windows non include il supporto per SOCKS5 e non può quindi essere usato per la procedura descritta in questo documento.</span><span class="sxs-lookup"><span data-stu-id="a44ea-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="a44ea-131">I browser seguenti si basano sulle impostazioni proxy di Windows e non possono essere usati per la procedura illustrata in questo documento:</span><span class="sxs-lookup"><span data-stu-id="a44ea-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="a44ea-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="a44ea-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="a44ea-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a44ea-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="a44ea-134">Anche Google Chrome si basa sulle impostazioni proxy di Windows.</span><span class="sxs-lookup"><span data-stu-id="a44ea-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="a44ea-135">In questo caso, tuttavia, è possibile installare estensioni che supportano SOCKS5,</span><span class="sxs-lookup"><span data-stu-id="a44ea-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="a44ea-136">tra cui [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp) (opzione consigliata).</span><span class="sxs-lookup"><span data-stu-id="a44ea-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="a44ea-137"><a name="usessh"></a>Creare un tunnel con il comando SSH</span><span class="sxs-lookup"><span data-stu-id="a44ea-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="a44ea-138">Utilizzare il comando seguente per creare un SSH tunnel utilizzando il comando `ssh` .</span><span class="sxs-lookup"><span data-stu-id="a44ea-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="a44ea-139">Sostituire **USERNAME** con un utente SSH per il cluster HDInsight e **CLUSTERNAME** con il nome del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a44ea-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="a44ea-140">Questo comando crea una connessione che instrada il traffico alla porta locale 9876 al cluster su SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="a44ea-141">Le opzioni sono:</span><span class="sxs-lookup"><span data-stu-id="a44ea-141">The options are:</span></span>

* <span data-ttu-id="a44ea-142">**D 9876**: la porta locale che instrada il traffico attraverso il tunnel.</span><span class="sxs-lookup"><span data-stu-id="a44ea-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="a44ea-143">**C** : comprime tutti i dati, in quanto il traffico Web è costituito prevalentemente da testo.</span><span class="sxs-lookup"><span data-stu-id="a44ea-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="a44ea-144">**2** : forza SSH a tentare solo il protocollo versione 2.</span><span class="sxs-lookup"><span data-stu-id="a44ea-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="a44ea-145">**q** : modalità non interattiva.</span><span class="sxs-lookup"><span data-stu-id="a44ea-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="a44ea-146">**T** : disabilita l'allocazione pseudo-tty perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="a44ea-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="a44ea-147">**n**: impedisce la lettura di STDIN perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="a44ea-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="a44ea-148">**N** : non esegue un comando remoto perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="a44ea-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="a44ea-149">**f** : effettua l'esecuzione in background.</span><span class="sxs-lookup"><span data-stu-id="a44ea-149">**f** - Run in the background.</span></span>

<span data-ttu-id="a44ea-150">Al termine del comando, il traffico inviato alla porta 9876 nel computer locale viene instradato al nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="a44ea-151"><a name="useputty"></a>Creare un tunnel utilizzando PuTTY</span><span class="sxs-lookup"><span data-stu-id="a44ea-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="a44ea-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) è un client SSH grafico per Windows.</span><span class="sxs-lookup"><span data-stu-id="a44ea-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="a44ea-153">Usare la procedura seguente per creare un tunnel SSH con PuTTY:</span><span class="sxs-lookup"><span data-stu-id="a44ea-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="a44ea-154">Aprire PuTTY e immettere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="a44ea-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="a44ea-155">Se non si ha familiarità con PuTTY, vedere la [documentazione di PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="a44ea-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="a44ea-156">Nella sezione **Category** sul lato sinistro della finestra di dialogo espandere **Connection**, **SSH** e infine selezionare **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="a44ea-157">Fornire le seguenti informazioni nel modulo **Options controlling SSH port forwarding** :</span><span class="sxs-lookup"><span data-stu-id="a44ea-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="a44ea-158">**Source port** : la porta del client che si desidera inoltrare.</span><span class="sxs-lookup"><span data-stu-id="a44ea-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="a44ea-159">Ad esempio, **9876**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-159">For example, **9876**.</span></span>

   * <span data-ttu-id="a44ea-160">**Destination** : l'indirizzo SSH del cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="a44ea-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a44ea-161">Ad esempio, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="a44ea-162">**Dynamic** : consente il routing tramite proxy SOCKS dinamico.</span><span class="sxs-lookup"><span data-stu-id="a44ea-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image of tunneling options](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="a44ea-164">Fare clic su **Add** per aggiungere le impostazioni, quindi su **Open** per aprire una connessione SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="a44ea-165">Quando richiesto, accedere al server.</span><span class="sxs-lookup"><span data-stu-id="a44ea-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="a44ea-166">Usare il tunnel dal browser</span><span class="sxs-lookup"><span data-stu-id="a44ea-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a44ea-167">Nella procedura illustrata in questa sezione viene usato il browser Mozilla FireFox, poiché prevede le stesse impostazioni proxy per tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="a44ea-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="a44ea-168">È possibile che altri browser moderni, tra cui Google Chrome, richiedano un'estensione come FoxyProxy per poter interagire con il tunnel.</span><span class="sxs-lookup"><span data-stu-id="a44ea-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="a44ea-169">Configurare il browser in modo che usi **localhost** e la porta usata al momento della creazione del tunnel come proxy **SOCKS v5**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="a44ea-170">Ecco visualizzate le impostazioni di Firefox.</span><span class="sxs-lookup"><span data-stu-id="a44ea-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="a44ea-171">Se si usa una porta diversa da quella 9876, cambiare la porta con quella usata:</span><span class="sxs-lookup"><span data-stu-id="a44ea-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![image of Firefox settings](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="a44ea-173">Se si seleziona **Remote DNS**, le richieste DNS (Domain Name System) vengono risolte usando il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a44ea-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="a44ea-174">Questa impostazione risolve DNS usando il nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="a44ea-175">Per verificare il funzionamento del tunnel, visitare un sito, ad esempio [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="a44ea-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="a44ea-176">L'indirizzo IP restituito deve essere uno usato dal data center di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a44ea-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="a44ea-177">Verificare con l’interfaccia utente web di Ambari</span><span class="sxs-lookup"><span data-stu-id="a44ea-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="a44ea-178">Una volta stabilito il cluster, utilizzare la procedura seguente per verificare che sia possibile accedere all’interfaccia utente del servizio dal web Ambari:</span><span class="sxs-lookup"><span data-stu-id="a44ea-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="a44ea-179">Nel browser passare a http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="a44ea-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="a44ea-180">L'indirizzo `headnodehost` viene inviato al cluster tramite il tunnel e quindi risolto nel nodo head in cui è in esecuzione Ambari.</span><span class="sxs-lookup"><span data-stu-id="a44ea-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="a44ea-181">Quando richiesto, immettere il nome dell'account amministratore (admin) e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="a44ea-182">Può essere richiesto una seconda volta dall'interfaccia utente web di Ambari.</span><span class="sxs-lookup"><span data-stu-id="a44ea-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="a44ea-183">In tal caso, è necessario immettere nuovamente le informazioni.</span><span class="sxs-lookup"><span data-stu-id="a44ea-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a44ea-184">Quando si usa l'indirizzo http://headnodehost:8080 per connettersi al cluster, la connessione viene stabilita tramite il tunnel.</span><span class="sxs-lookup"><span data-stu-id="a44ea-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="a44ea-185">La comunicazione viene protetta usando il tunnel SSH invece di HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a44ea-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="a44ea-186">Per connettersi a Internet tramite HTTPS, usare https://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** è il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="a44ea-187">Dall'interfaccia utente Web di Ambari, selezionare HDFS dall'elenco a sinistra della pagina.</span><span class="sxs-lookup"><span data-stu-id="a44ea-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Immagine con HDFS selezionata](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="a44ea-189">Quando le informazioni del servizio HDFS vengono visualizzate, selezionare **Collegamenti rapidi**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="a44ea-190">Verrà visualizzato un elenco di nodi head del cluster.</span><span class="sxs-lookup"><span data-stu-id="a44ea-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="a44ea-191">Selezionare uno dei nodi head e quindi selezionare l' **interfaccia utente di NameNode**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Immagine con il menu di collegamenti rapidi espanso](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="a44ea-193">Quando si seleziona __Quick Links__ (Collegamenti rapidi), è possibile che venga visualizzato un indicatore di attesa.</span><span class="sxs-lookup"><span data-stu-id="a44ea-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="a44ea-194">Questa condizione può verificarsi se la connessione Internet è lenta.</span><span class="sxs-lookup"><span data-stu-id="a44ea-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="a44ea-195">Attendere un minuto o due perché i dati vengano ricevuti dal server, poi riprovare con l'elenco.</span><span class="sxs-lookup"><span data-stu-id="a44ea-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="a44ea-196">Alcune voci del menu **Quick Links** (Collegamenti rapidi) potrebbero risultare troncate sul lato destro della schermata.</span><span class="sxs-lookup"><span data-stu-id="a44ea-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="a44ea-197">In tal caso, espandere il menu con il mouse e usare il tasto freccia destra per scorrere la schermata verso destra e visualizzare il resto del menu.</span><span class="sxs-lookup"><span data-stu-id="a44ea-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="a44ea-198">Viene visualizzata una pagina simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="a44ea-198">A page similar to the following image is displayed:</span></span>

    ![Immagine dell'interfaccia utente di NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="a44ea-200">Si noti l'URL della pagina, che dovrebbe essere simile a **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="a44ea-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="a44ea-201">Questo URI usa il nome di dominio interno completo (FQDN) del nodo ed è accessibile solo quando si usa un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="a44ea-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a44ea-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a44ea-202">Next steps</span></span>

<span data-ttu-id="a44ea-203">Dopo avere appreso come creare e usare un tunnel SSH, vedere il documento seguente per conoscere gli altri modi di usare Ambari:</span><span class="sxs-lookup"><span data-stu-id="a44ea-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="a44ea-204">Gestire i cluster HDInsight mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="a44ea-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="a44ea-205">Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a44ea-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

