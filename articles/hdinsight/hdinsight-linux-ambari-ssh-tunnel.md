---
title: aaaUse SSH tunneling tooaccess Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse un toosecurely tunnel SSH individuare le risorse web ospitate sui nodi di HDInsight basati su Linux.
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
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="8417c-103">Usare SSH Tunneling tooaccess Ambari web dell'interfaccia utente, JobHistory, NameNode, Oozie e altre interfacce utente web</span><span class="sxs-lookup"><span data-stu-id="8417c-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="8417c-104">Cluster HDInsight basati su Linux forniscono l'interfaccia utente web tooAmbari accesso tramite Internet hello, ma alcune funzionalità di hello dell'interfaccia utente non sono.</span><span class="sxs-lookup"><span data-stu-id="8417c-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="8417c-105">Ad esempio, hello web dell'interfaccia utente per altri servizi che vengono rilevate tramite Ambari.</span><span class="sxs-lookup"><span data-stu-id="8417c-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="8417c-106">Per le funzionalità complete di hello Ambari web dell'interfaccia utente, è necessario utilizzare un'intestazione di cluster toohello tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="8417c-107">Perché usare un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="8417c-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="8417c-108">Molti dei menu hello in Ambari funzionano solo tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="8417c-109">Questi menu si basano su servizi e siti Web in esecuzione in altri tipi di nodi, ad esempio i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8417c-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="8417c-110">Spesso questi siti web non sono protetti, pertanto non è sicuro toodirectly espongono in hello internet.</span><span class="sxs-lookup"><span data-stu-id="8417c-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="8417c-111">Hello segue le interfacce utente Web richiede un tunnel SSH:</span><span class="sxs-lookup"><span data-stu-id="8417c-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="8417c-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="8417c-112">JobHistory</span></span>
* <span data-ttu-id="8417c-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="8417c-113">NameNode</span></span>
* <span data-ttu-id="8417c-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="8417c-114">Thread Stacks</span></span>
* <span data-ttu-id="8417c-115">Interfaccia utente Web di Oozie</span><span class="sxs-lookup"><span data-stu-id="8417c-115">Oozie web UI</span></span>
* <span data-ttu-id="8417c-116">HBase Master e l'interfaccia utente di Log</span><span class="sxs-lookup"><span data-stu-id="8417c-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="8417c-117">Se si utilizza toocustomize azioni Script del cluster, tutti i servizi o le utilità che si installa che espongono un'interfaccia utente web richiedono un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="8417c-118">Ad esempio, se si installa tonalità utilizzando un'azione di Script, è necessario utilizzare un SSH tunnel tooaccess hello tonalità interfaccia utente web.</span><span class="sxs-lookup"><span data-stu-id="8417c-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8417c-119">Se si dispone di accesso diretto tooHDInsight attraverso una rete virtuale, non è necessario toouse SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="8417c-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="8417c-120">Per un esempio di accedere direttamente alle HDInsight tramite una rete virtuale, vedere hello [rete locale di connettersi a HDInsight tooyour](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8417c-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="8417c-121">Che cos'è un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="8417c-121">What is an SSH tunnel</span></span>

<span data-ttu-id="8417c-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) instrada il traffico inviato tooa porta nella workstation locale.</span><span class="sxs-lookup"><span data-stu-id="8417c-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="8417c-123">Hello traffico viene indirizzato attraverso un SSH connessione tooyour HDInsight nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="8417c-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="8417c-124">richiesta di Hello viene risolto come se avesse origine nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="8417c-125">risposta Hello viene indirizzato attraverso la workstation di tooyour tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8417c-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8417c-126">Prerequisites</span></span>

* <span data-ttu-id="8417c-127">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-127">An SSH client.</span></span> <span data-ttu-id="8417c-128">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8417c-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="8417c-129">Un browser web che può essere configurato un proxy SOCKS5 toouse.</span><span class="sxs-lookup"><span data-stu-id="8417c-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8417c-130">supporto dei proxy SOCKS Hello incorporato in Windows non supporta SOCKS5 e non funziona con i passaggi di hello in questo documento.</span><span class="sxs-lookup"><span data-stu-id="8417c-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="8417c-131">Hello browser seguenti si basano sulle impostazioni di proxy di Windows e operazioni non attualmente con passaggi hello in questo documento:</span><span class="sxs-lookup"><span data-stu-id="8417c-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="8417c-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="8417c-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="8417c-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="8417c-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="8417c-134">Google Chrome utilizza inoltre le impostazioni proxy di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="8417c-135">In questo caso, tuttavia, è possibile installare estensioni che supportano SOCKS5,</span><span class="sxs-lookup"><span data-stu-id="8417c-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="8417c-136">tra cui [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp) (opzione consigliata).</span><span class="sxs-lookup"><span data-stu-id="8417c-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="8417c-137"><a name="usessh"></a>Creare un tunnel comando SSH hello</span><span class="sxs-lookup"><span data-stu-id="8417c-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="8417c-138">Comando che segue hello utilizzare toocreate un tunnel SSH utilizzando hello `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="8417c-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="8417c-139">Sostituire **USERNAME** con un utente SSH per il cluster HDInsight e sostituire **CLUSTERNAME** con nome hello del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8417c-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="8417c-140">Questo comando crea una connessione che consenta di instradare i cluster di traffico toolocal porta 9876 toohello su SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="8417c-141">Hello opzioni sono:</span><span class="sxs-lookup"><span data-stu-id="8417c-141">hello options are:</span></span>

* <span data-ttu-id="8417c-142">**D 9876** -hello porta locale che instrada il traffico attraverso il tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="8417c-143">**C** : comprime tutti i dati, in quanto il traffico Web è costituito prevalentemente da testo.</span><span class="sxs-lookup"><span data-stu-id="8417c-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="8417c-144">**2** -force SSH tootry protocol versione 2 solo.</span><span class="sxs-lookup"><span data-stu-id="8417c-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="8417c-145">**q** : modalità non interattiva.</span><span class="sxs-lookup"><span data-stu-id="8417c-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="8417c-146">**T** : disabilita l'allocazione pseudo-tty perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="8417c-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="8417c-147">**n**: impedisce la lettura di STDIN perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="8417c-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="8417c-148">**N** : non esegue un comando remoto perché si tratta semplicemente dell'inoltro di una porta.</span><span class="sxs-lookup"><span data-stu-id="8417c-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="8417c-149">**f** -eseguito in background hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="8417c-150">Al termine del comando hello, il traffico inviato tooport 9876 nel computer locale hello è indirizzato toohello nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="8417c-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="8417c-151"><a name="useputty"></a>Creare un tunnel utilizzando PuTTY</span><span class="sxs-lookup"><span data-stu-id="8417c-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="8417c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) è un client SSH grafico per Windows.</span><span class="sxs-lookup"><span data-stu-id="8417c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="8417c-153">Utilizzare i seguenti passaggi toocreate un tunnel SSH tramite PuTTY hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="8417c-154">Aprire PuTTY e immettere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="8417c-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="8417c-155">Se non si ha familiarità con PuTTY, vedere hello [PuTTY documentazione (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="8417c-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="8417c-156">In hello **categoria** toohello sezione a sinistra della finestra di dialogo hello, espandere **connessione**, espandere **SSH**, quindi selezionare **tunnel**.</span><span class="sxs-lookup"><span data-stu-id="8417c-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="8417c-157">Fornire le seguenti informazioni su hello hello **opzioni che controllano SSH inoltro alla porta** form:</span><span class="sxs-lookup"><span data-stu-id="8417c-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="8417c-158">**Porta di origine** -hello porta sul client hello che si desidera tooforward.</span><span class="sxs-lookup"><span data-stu-id="8417c-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="8417c-159">Ad esempio, **9876**.</span><span class="sxs-lookup"><span data-stu-id="8417c-159">For example, **9876**.</span></span>

   * <span data-ttu-id="8417c-160">**Destinazione** -hello indirizzo SSH per cluster HDInsight basati su Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8417c-161">Ad esempio, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="8417c-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="8417c-162">**Dynamic** : consente il routing tramite proxy SOCKS dinamico.</span><span class="sxs-lookup"><span data-stu-id="8417c-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image of tunneling options](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="8417c-164">Fare clic su **Aggiungi** tooadd hello impostazioni e quindi fare clic su **aprire** tooopen una connessione SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="8417c-165">Quando richiesto, accedere toohello server.</span><span class="sxs-lookup"><span data-stu-id="8417c-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="8417c-166">Utilizzare tunnel hello dal browser</span><span class="sxs-lookup"><span data-stu-id="8417c-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8417c-167">Hello passaggi hello di utilizzare questa sezione del browser Mozilla FireFox, in quanto forniscono hello stesse impostazioni del proxy in tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="8417c-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="8417c-168">Altri browser moderni, ad esempio Google Chrome, potrebbe richiedere un'estensione, ad esempio toowork FoxyProxy con tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="8417c-169">Configurare hello browser toouse **localhost** e porta hello è utilizzato quando la creazione di tunnel hello come un **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="8417c-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="8417c-170">Ecco le impostazioni di Firefox hello aspetto.</span><span class="sxs-lookup"><span data-stu-id="8417c-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="8417c-171">Se si utilizza una porta diversa da quella 9876, modificare toohello porta hello che è utilizzato:</span><span class="sxs-lookup"><span data-stu-id="8417c-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![image of Firefox settings](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="8417c-173">Selezione **DNS remoto** risolve le richieste di sistema DNS (Domain Name) con i cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="8417c-174">Questa impostazione consente di risolvere DNS tramite hello del nodo head del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="8417c-175">Verificare il funzionamento di tale tunnel hello, visitare un sito, ad esempio [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="8417c-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="8417c-176">IP Hello restituito deve essere utilizzato da Data Center di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="8417c-177">Verificare con l’interfaccia utente web di Ambari</span><span class="sxs-lookup"><span data-stu-id="8417c-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="8417c-178">Dopo aver stabilito cluster hello, utilizzare hello tooverify passaggi che è possibile accedere servizio web, le interfacce utente da hello Ambari Web seguente:</span><span class="sxs-lookup"><span data-stu-id="8417c-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="8417c-179">Nel browser passare toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="8417c-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="8417c-180">Hello `headnodehost` indirizzo viene inviato su cluster di toohello tunnel hello e risolvere il nodo head toohello Ambari in esecuzione in.</span><span class="sxs-lookup"><span data-stu-id="8417c-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="8417c-181">Quando richiesto, immettere nome utente amministratore di hello (amministratore) e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="8417c-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="8417c-182">Può essere richiesto un secondo momento da hello Ambari web dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="8417c-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="8417c-183">In questo caso, immettere nuovamente le informazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8417c-184">Quando si utilizza hello http://headnodehost:8080 indirizzo tooconnect toohello cluster, ci si connette tramite il tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="8417c-185">Comunicazione sia protetta con tunnel SSH hello anziché HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8417c-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="8417c-186">tooconnect oltre hello internet tramite HTTPS, utilizzare https://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="8417c-187">Nell'elenco di hello sulla sinistra hello della pagina di hello hello dell'interfaccia utente Web Ambari, selezionare HDFS.</span><span class="sxs-lookup"><span data-stu-id="8417c-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Immagine con HDFS selezionata](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="8417c-189">Selezionare la visualizzazione di informazioni sul servizio HDFS hello **collegamenti rapidi**.</span><span class="sxs-lookup"><span data-stu-id="8417c-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="8417c-190">Viene visualizzato un elenco di nodi head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="8417c-191">Selezionare uno dei nodi head hello e quindi selezionare **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="8417c-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Immagine con menu collegamenti rapidi hello espanso](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="8417c-193">Quando si seleziona __Quick Links__ (Collegamenti rapidi), è possibile che venga visualizzato un indicatore di attesa.</span><span class="sxs-lookup"><span data-stu-id="8417c-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="8417c-194">Questa condizione può verificarsi se la connessione Internet è lenta.</span><span class="sxs-lookup"><span data-stu-id="8417c-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="8417c-195">Attendere un minuto o due per hello dati toobe ricevuto dal server hello, quindi ripetere l'operazione elenco hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="8417c-196">Alcune voci hello **collegamenti rapidi** menu può essere tagliato da hello destra dello schermo hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="8417c-197">In questo caso, espandere il menu di hello utilizzando il mouse e utilizzare hello freccia destra tooscroll chiave hello schermata toohello toosee destra hello resto del menu hello.</span><span class="sxs-lookup"><span data-stu-id="8417c-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="8417c-198">Viene visualizzato un toohello simile pagina seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="8417c-198">A page similar toohello following image is displayed:</span></span>

    ![Immagine di hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="8417c-200">Si noti hello URL della pagina. dovrebbe essere simile troppo**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="8417c-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="8417c-201">Questo URI utilizza hello interno completamente nome di dominio completo (FQDN) del nodo hello ed è accessibile solo quando si usa un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="8417c-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8417c-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8417c-202">Next steps</span></span>

<span data-ttu-id="8417c-203">Ora che si è appreso come toocreate e utilizzare un tunnel SSH, vedere hello documento per altri toouse modi Ambari seguenti:</span><span class="sxs-lookup"><span data-stu-id="8417c-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="8417c-204">Gestire i cluster HDInsight mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="8417c-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="8417c-205">Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8417c-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

