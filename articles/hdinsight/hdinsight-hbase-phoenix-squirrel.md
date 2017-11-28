---
title: aaaUse Phoenix Apache ed esce con basati su Windows Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse Phoenix Apache in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="1abba-103">Usare Apache Phoenix e SQuirreL con i cluster HBase basati su Windows in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1abba-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="1abba-104">Informazioni su come toouse [Phoenix Apache](http://phoenix.apache.org/) in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1abba-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="1abba-105">Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="1abba-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="1abba-106">Per hello grammatica Phoenix, vedere [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="1abba-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="1abba-107">Per informazioni sulla versione Phoenix in HDInsight hello, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1abba-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="1abba-108">Hello passaggi sono disponibili solo in questo documento per i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1abba-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1abba-109">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="1abba-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1abba-110">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1abba-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1abba-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1abba-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1abba-112">Per informazioni sull'uso di Phoenix su HDInsight basato su Linux, vedere [Usare Apache Phoenix con cluster HBase basati su Linux in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1abba-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="1abba-113">Usare SQLLine</span><span class="sxs-lookup"><span data-stu-id="1abba-113">Use SQLLine</span></span>
<span data-ttu-id="1abba-114">[SQLLine](http://sqlline.sourceforge.net/) è un tooexecute di utilità della riga di comando SQL.</span><span class="sxs-lookup"><span data-stu-id="1abba-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1abba-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1abba-115">Prerequisites</span></span>
<span data-ttu-id="1abba-116">Prima di poter utilizzare SQLLine, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="1abba-117">**Un cluster HBase in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1abba-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="1abba-118">Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="1abba-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="1abba-119">**Connettere il cluster HBase toohello tramite protocollo desktop remoto hello**.</span><span class="sxs-lookup"><span data-stu-id="1abba-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="1abba-120">Per istruzioni, vedere [cluster di gestire Hadoop in HDInsight mediante hello portale di Azure classico][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="1abba-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="1abba-121">**toofind il nome host hello**</span><span class="sxs-lookup"><span data-stu-id="1abba-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="1abba-122">Aprire **della riga di comando Hadoop** da desktop hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="1abba-123">Eseguire hello suffisso DNS hello tooget di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1abba-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="1abba-124">Annotare il **suffisso DNS specifico della connessione**.</span><span class="sxs-lookup"><span data-stu-id="1abba-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="1abba-125">Ad esempio, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="1abba-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="1abba-126">Quando ci si connette cluster HBase tooan, sarà necessario tooone tooconnect di Zookeepers hello tramite FQDN.</span><span class="sxs-lookup"><span data-stu-id="1abba-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="1abba-127">Ogni cluster HDInsight ha tre Zookeeper:</span><span class="sxs-lookup"><span data-stu-id="1abba-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="1abba-128">*zookeeper0*, *zookeeper1* e *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="1abba-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="1abba-129">Hello FQDN sarà simile al seguente *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="1abba-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="1abba-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="1abba-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="1abba-131">Aprire **della riga di comando Hadoop** da desktop hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="1abba-132">Eseguire i seguenti comandi tooopen SQLLine hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight HBase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="1abba-134">comandi Hello utilizzati nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="1abba-135">Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="1abba-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="1abba-136">Usare SQuirreL</span><span class="sxs-lookup"><span data-stu-id="1abba-136">Use SQuirreL</span></span>
<span data-ttu-id="1abba-137">[Esce SQL Client](http://squirrel-sql.sourceforge.net/) è un programma Java con interfaccia grafico che consentono di struttura hello tooview di un database conforme a JDBC, esplorare i dati di hello in tabelle, eseguire comandi SQL e così via. Può essere utilizzato tooconnect tooApache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1abba-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="1abba-138">In questa sezione illustra come tooinstall e configurare esce il cluster workstation tooconnect tooan HBase in HDInsight tramite una VPN.</span><span class="sxs-lookup"><span data-stu-id="1abba-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1abba-139">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1abba-139">Prerequisites</span></span>
<span data-ttu-id="1abba-140">Prima di seguire le procedure di hello, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="1abba-141">Un cluster HBase distribuito tooan rete virtuale di Azure con una macchina virtuale DNS.</span><span class="sxs-lookup"><span data-stu-id="1abba-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="1abba-142">Per istruzioni, vedere [Creare cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="1abba-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="1abba-143">Ottiene il suffisso DNS specifico della connessione del cluster di hello HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="1abba-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="1abba-144">tooget RDP in cluster hello, esso, quindi eseguire IPConfig.</span><span class="sxs-lookup"><span data-stu-id="1abba-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="1abba-145">suffisso DNS Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="1abba-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="1abba-146">Scaricare e installare [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="1abba-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="1abba-147">Sarà necessario makecert da hello pacchetto toocreate il certificato.</span><span class="sxs-lookup"><span data-stu-id="1abba-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="1abba-148">Scaricare e installare [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="1abba-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="1abba-149">SQuirreL SQL Client versione 3.0 e versioni successive richiede la versione JRE 1.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1abba-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="1abba-150">Configurare un toohello di connessione VPN Point-to-Site rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1abba-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="1abba-151">La configurazione di una connessione VPN Point-To-Site prevede tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="1abba-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="1abba-152">Configurare una rete virtuale e un gateway di routing dinamico</span><span class="sxs-lookup"><span data-stu-id="1abba-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="1abba-153">Creare i certificati</span><span class="sxs-lookup"><span data-stu-id="1abba-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="1abba-154">Configurare il client VPN</span><span class="sxs-lookup"><span data-stu-id="1abba-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="1abba-155">Vedere [configurare tooan di connessione rete virtuale di Azure un VPN Point-to-Site](../vpn-gateway/vpn-gateway-point-to-site-create.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1abba-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="1abba-156">Configurare una rete virtuale e un gateway di routing dinamico</span><span class="sxs-lookup"><span data-stu-id="1abba-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="1abba-157">Garantire è stato effettuato il provisioning di un cluster HBase in una rete virtuale di Azure (vedere hello prerequisiti per questa sezione).</span><span class="sxs-lookup"><span data-stu-id="1abba-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="1abba-158">passaggio successivo Hello è tooconfigure una connessione point-to-site.</span><span class="sxs-lookup"><span data-stu-id="1abba-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="1abba-159">**connettività point-to-site di hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="1abba-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="1abba-160">Accedi toohello [portale di Azure classico][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1abba-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="1abba-161">A sinistra di hello, fare clic su **reti**.</span><span class="sxs-lookup"><span data-stu-id="1abba-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="1abba-162">Fare clic su rete virtuale di hello creato (vedere [provisioning HBase cluster nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="1abba-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="1abba-163">Fare clic su **configura** dall'alto hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="1abba-164">In hello **connettività point-to-site** selezionare **configurare la connettività point-to-site**.</span><span class="sxs-lookup"><span data-stu-id="1abba-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="1abba-165">Configurare **IP iniziale** e **CIDR** toospecify hello indirizzo IP da cui i client VPN riceveranno un indirizzo IP di indirizzi quando si è connessi.</span><span class="sxs-lookup"><span data-stu-id="1abba-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="1abba-166">intervallo di Hello non può sovrapporsi con uno qualsiasi dei hello intervalli presenti in locale di rete e hello connettono alla rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1abba-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="1abba-167">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="1abba-167">For example.</span></span> <span data-ttu-id="1abba-168">Se si seleziona 10.0.0.0/20 per la rete virtuale hello, è possibile selezionare 10.1.0.0/24 hello client dello spazio degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="1abba-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="1abba-169">Vedere hello [connettivitàPoint-To-Site] [ vnet-point-to-site-connectivity] pagina per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="1abba-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="1abba-170">Nella sezione di spazi indirizzi di rete virtuale hello, fare clic su **Aggiungi subnet gateway**.</span><span class="sxs-lookup"><span data-stu-id="1abba-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="1abba-171">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="1abba-172">Fare clic su **Sì** modifica hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1abba-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="1abba-173">Attendere che il sistema hello ha apportato hello modificare prima di continuare la procedura successiva toohello.</span><span class="sxs-lookup"><span data-stu-id="1abba-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="1abba-174">**toocreate un gateway con routing dinamico**</span><span class="sxs-lookup"><span data-stu-id="1abba-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="1abba-175">Dal portale di Azure classico hello, fare clic su **DASHBOARD** dall'alto hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="1abba-176">Fare clic su **crea GATEWAY** dal basso hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="1abba-177">Fare clic su **Sì** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1abba-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="1abba-178">Attendere fino a quando non è stato creato il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="1abba-179">Fare clic su **DASHBOARD** dall'alto hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="1abba-180">Verrà visualizzato un grafico visuale della rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Diagramma virtuale Point-to-Site della rete virtuale di Azure][img-vnet-diagram]

    <span data-ttu-id="1abba-182">diagramma di Hello Mostra le connessioni client 0.</span><span class="sxs-lookup"><span data-stu-id="1abba-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="1abba-183">Dopo aver apportato una rete virtuale toohello di connessione, il numero di hello sarà tooone aggiornato.</span><span class="sxs-lookup"><span data-stu-id="1abba-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="1abba-184">Creare i certificati</span><span class="sxs-lookup"><span data-stu-id="1abba-184">Create your certificates</span></span>
<span data-ttu-id="1abba-185">Un modo toocreate è un certificato x. 509 utilizzando hello strumento di creazione certificati (makecert.exe) fornita con [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1abba-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="1abba-186">**un certificato radice autofirmato toocreate**</span><span class="sxs-lookup"><span data-stu-id="1abba-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="1abba-187">Dalla workstation, aprire una finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1abba-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="1abba-188">Esplorazione delle cartelle di strumenti di Visual Studio toohello.</span><span class="sxs-lookup"><span data-stu-id="1abba-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="1abba-189">comando nel seguente esempio hello seguente Hello creare e installare un certificato radice nell'archivio certificati personali hello nella workstation e anche creare un file con estensione cer corrispondente che verrà caricato in un secondo momento toohello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="1abba-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="1abba-190">Cambiare directory toohello che si desidera hello toobe file con estensione cer trova, dove HBaseVnetVPNRootCertificate è il nome di hello che si desidera toouse certificato hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="1abba-191">Non chiudere hello il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1abba-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="1abba-192">Sarà necessario hello procedura descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="1abba-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1abba-193">Poiché è stato creato un certificato radice da cui verranno generati certificati client, è possibile desidera tooexport insieme alla relativa chiave privata e salvarlo tooa posizione sicura dove può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="1abba-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="1abba-194">**toocreate un certificato client**</span><span class="sxs-lookup"><span data-stu-id="1abba-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="1abba-195">Da hello stesso prompt dei comandi (e presenta toobe hello computer in cui è stato creato certificato radice hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="1abba-196">certificato client Hello deve essere generato dal certificato radice hello), esecuzione hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="1abba-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="1abba-197">HBaseVnetVPNRootCertificate è nome del certificato radice hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="1abba-198">Include un nome del certificato radice toomatch hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="1abba-199">Certificato radice hello sia certificato client hello vengono archiviati nell'archivio certificati personali nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1abba-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="1abba-200">Utilizzare tooverify Certmgr. msc.</span><span class="sxs-lookup"><span data-stu-id="1abba-200">Use certmgr.msc tooverify.</span></span>

    ![Certificato VPN Point-to-Site della rete virtuale di Azure][img-certificate]

    <span data-ttu-id="1abba-202">Un certificato client deve essere installato in ogni computer che si desidera rete virtuale di tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1abba-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="1abba-203">È consigliabile creare client univoci certificati per ogni computer che si desidera rete virtuale di tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1abba-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="1abba-204">i certificati client hello tooexport, utilizzare Certmgr. msc.</span><span class="sxs-lookup"><span data-stu-id="1abba-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="1abba-205">**tooupload hello radice certificato toohello portale classico di Azure**</span><span class="sxs-lookup"><span data-stu-id="1abba-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="1abba-206">Dal portale di Azure classico hello, fare clic su **rete** a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="1abba-207">Fare clic in cui viene distribuito il cluster HBase per la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="1abba-208">Fare clic su **certificati** dall'alto hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="1abba-209">Fare clic su **caricare** da hello basso e specificare i file del certificato radice hello creato nella procedura di hello prima dell'ultima.</span><span class="sxs-lookup"><span data-stu-id="1abba-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="1abba-210">Attendere che il certificato di hello ottenuto importato.</span><span class="sxs-lookup"><span data-stu-id="1abba-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="1abba-211">Fare clic su **DASHBOARD** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="1abba-212">diagramma virtuale Hello Mostra stato hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="1abba-213">Configurare il client VPN</span><span class="sxs-lookup"><span data-stu-id="1abba-213">Configure your VPN client</span></span>
<span data-ttu-id="1abba-214">**toodownload e installare il pacchetto VPN hello client**</span><span class="sxs-lookup"><span data-stu-id="1abba-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="1abba-215">Dalla pagina DASHBOARD hello della rete virtuale hello, nella sezione riepilogo rapido hello, fare clic su **Download hello pacchetto VPN Client a 64 bit** o **Download hello pacchetto VPN Client a 32 bit** in base il versione del sistema operativo della workstation.</span><span class="sxs-lookup"><span data-stu-id="1abba-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="1abba-216">Fare clic su **eseguire** pacchetto hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="1abba-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="1abba-217">Al prompt dei comandi sicurezza hello, fare clic su **informazioni**, quindi fare clic su **eseguire comunque**.</span><span class="sxs-lookup"><span data-stu-id="1abba-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="1abba-218">Fare clic due volte su **Sì** .</span><span class="sxs-lookup"><span data-stu-id="1abba-218">Click **Yes** twice.</span></span>

<span data-ttu-id="1abba-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="1abba-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="1abba-220">Sul desktop di hello della workstation, fare clic sull'icona di reti hello sulla barra delle applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="1abba-221">Verrà visualizzata una connessione VPN con il nome della propria rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1abba-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="1abba-222">Fare clic su nome della connessione VPN hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="1abba-223">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="1abba-223">Click **Connect**.</span></span>

<span data-ttu-id="1abba-224">**hello tootest risoluzione di nome di dominio e di connessione VPN**</span><span class="sxs-lookup"><span data-stu-id="1abba-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="1abba-225">Dalla workstation hello, aprire un prompt dei comandi e ping uno dei seguenti nomi di suffisso DNS del cluster HBase hello hello è myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="1abba-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="1abba-226">Installare e configurare SQuirreL sulla workstation</span><span class="sxs-lookup"><span data-stu-id="1abba-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="1abba-227">**tooinstall esce**</span><span class="sxs-lookup"><span data-stu-id="1abba-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="1abba-228">Scaricare file jar del client SQL esce hello da [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="1abba-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="1abba-229">File jar hello apertura ed esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1abba-229">Open/run hello jar file.</span></span> <span data-ttu-id="1abba-230">Richiede hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="1abba-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="1abba-231">Fare clic su **Next** due volte.</span><span class="sxs-lookup"><span data-stu-id="1abba-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="1abba-232">Specificare un percorso in cui occorre hello l'autorizzazione di scrittura e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1abba-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1abba-233">cartella di installazione predefinita di Hello è nella cartella c:\Programmi\Microsoft Files\squirrel-sql-3.6 hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="1abba-234">Nel percorso toothis toowrite ordine installer hello deve disporre dei privilegi di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="1abba-235">È possibile aprire un prompt dei comandi come amministratore, spostarsi nella cartella bin del tooJava ed eseguire quindi:</span><span class="sxs-lookup"><span data-stu-id="1abba-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="1abba-236">Java.exe-jar [percorso hello del file jar di hello esce]</span><span class="sxs-lookup"><span data-stu-id="1abba-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="1abba-237">Fare clic su **OK** tooconfirm creazione hello directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1abba-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="1abba-238">impostazione predefinita Hello è hello tooinstall Base pacchetti e Standard.</span><span class="sxs-lookup"><span data-stu-id="1abba-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="1abba-239">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1abba-239">Click **Next**.</span></span>
7. <span data-ttu-id="1abba-240">Fare clic su **Next** (Avanti) due volte e quindi su **Done** (Fine).</span><span class="sxs-lookup"><span data-stu-id="1abba-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="1abba-241">**driver di Phoenix hello tooinstall**</span><span class="sxs-lookup"><span data-stu-id="1abba-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="1abba-242">file jar di Hello phoenix driver si trova nel cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="1abba-243">percorso di Hello è simile toohello seguenti, in base alle versioni hello:</span><span class="sxs-lookup"><span data-stu-id="1abba-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="1abba-244">È necessario toocopy è tooyour workstation in hello [cartella di installazione esce] / percorso lib.</span><span class="sxs-lookup"><span data-stu-id="1abba-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="1abba-245">il modo più semplice Hello è tooRDP in cluster hello e quindi utilizzare file copia e Incolla (CTRL + C e CTRL + V) toocopy è tooyour workstation.</span><span class="sxs-lookup"><span data-stu-id="1abba-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="1abba-246">**tooadd un tooSQuirreL driver Phoenix**</span><span class="sxs-lookup"><span data-stu-id="1abba-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="1abba-247">Aprire SQuirreL SQL Client dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="1abba-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="1abba-248">Fare clic su hello **Driver** scheda hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="1abba-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="1abba-249">Da hello **driver** menu, fare clic su **nuovo Driver**.</span><span class="sxs-lookup"><span data-stu-id="1abba-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="1abba-250">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="1abba-250">Enter hello following information:</span></span>

   * <span data-ttu-id="1abba-251">**Name**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="1abba-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="1abba-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="1abba-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="1abba-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="1abba-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="1abba-254">Utente tutte le lettere minuscole nell'URL di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="1abba-255">È possibile usare il quorum zookeeper completo nel caso in cui uno di essi sia inattivo.</span><span class="sxs-lookup"><span data-stu-id="1abba-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="1abba-256">i nomi host Hello sono zookeeper0, zookeeper1 e zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="1abba-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. <span data-ttu-id="1abba-258">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1abba-258">Click **OK**.</span></span>

<span data-ttu-id="1abba-259">**un cluster HBase di alias toohello toocreate**</span><span class="sxs-lookup"><span data-stu-id="1abba-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="1abba-260">Esce, fare clic su hello **alias** scheda hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="1abba-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="1abba-261">Da hello **alias** menu, fare clic su **nuovo Alias**.</span><span class="sxs-lookup"><span data-stu-id="1abba-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="1abba-262">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="1abba-262">Enter hello following information:</span></span>

   * <span data-ttu-id="1abba-263">**Nome**: nome hello del cluster HBase hello o qualsiasi nome desiderato.</span><span class="sxs-lookup"><span data-stu-id="1abba-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="1abba-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="1abba-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="1abba-265">Nome del driver hello creato nella procedura precedente hello deve corrispondere.</span><span class="sxs-lookup"><span data-stu-id="1abba-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="1abba-266">**URL**: hello URL viene copiato dalla configurazione del driver.</span><span class="sxs-lookup"><span data-stu-id="1abba-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="1abba-267">Verificare che toouser lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="1abba-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="1abba-268">**Nome utente**: può essere qualsiasi testo.</span><span class="sxs-lookup"><span data-stu-id="1abba-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="1abba-269">Poiché si utilizza la connettività VPN in questo caso, il nome di utente hello non viene usato affatto.</span><span class="sxs-lookup"><span data-stu-id="1abba-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="1abba-270">**Password**: può essere qualsiasi testo.</span><span class="sxs-lookup"><span data-stu-id="1abba-270">**Password**: It can be any text.</span></span>

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. <span data-ttu-id="1abba-272">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="1abba-272">Click **Test**.</span></span>
5. <span data-ttu-id="1abba-273">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="1abba-273">Click **Connect**.</span></span> <span data-ttu-id="1abba-274">Quando la connessione di hello, esce aspetto:</span><span class="sxs-lookup"><span data-stu-id="1abba-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="1abba-276">**toorun un test**</span><span class="sxs-lookup"><span data-stu-id="1abba-276">**toorun a test**</span></span>

1. <span data-ttu-id="1abba-277">Fare clic su hello **SQL** scheda toohello destra Avanti **oggetti** scheda.</span><span class="sxs-lookup"><span data-stu-id="1abba-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="1abba-278">Copiare e incollare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1abba-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="1abba-279">Fare clic su pulsante di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="1abba-281">Passa indietro toohello **oggetti** scheda.</span><span class="sxs-lookup"><span data-stu-id="1abba-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="1abba-282">Espandere il nome di alias hello e quindi **tabella**.</span><span class="sxs-lookup"><span data-stu-id="1abba-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="1abba-283">Verrà visualizzata sotto la tabella nuova hello.</span><span class="sxs-lookup"><span data-stu-id="1abba-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1abba-284">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1abba-284">Next steps</span></span>
<span data-ttu-id="1abba-285">In questo articolo, si è appreso come toouse Phoenix Apache in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1abba-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="1abba-286">toolearn informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="1abba-286">toolearn more, see</span></span>

* <span data-ttu-id="1abba-287">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="1abba-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="1abba-288">[Eseguire il provisioning di cluster HBase in rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare con HBase direttamente.</span><span class="sxs-lookup"><span data-stu-id="1abba-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="1abba-289">[Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come la replica di HBase tooconfigure tra due Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="1abba-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="1abba-290">[Analizzare Twitter sentiment con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come toodo in tempo reale [analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei big data dall'utilizzo di HBase in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1abba-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
