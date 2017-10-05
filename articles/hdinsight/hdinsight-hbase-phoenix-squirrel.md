---
title: Usare Apache Phoenix e SQuirreL con Azure HDInsight basato su Windows | Documentazione Microsoft
description: Informazioni su come usare Apache Phoenix in HDInsight e su come installare e configurare SQuirreL sulla workstation per la connessione a un cluster HBase in HDInsight.
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
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="0ee29-103">Usare Apache Phoenix e SQuirreL con i cluster HBase basati su Windows in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ee29-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="0ee29-104">Informazioni su come usare [Apache Phoenix](http://phoenix.apache.org/) in HDInsight e su come installare e configurare SQuirrel sulla workstation per la connessione a un cluster HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee29-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="0ee29-105">Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="0ee29-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="0ee29-106">Per la grammatica Phoenix, vedere [Grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="0ee29-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="0ee29-107">Per informazioni sulla versione di Phoenix in HDInsight, vedere l'articolo relativo alle [novità delle versioni cluster di Hadoop incluse in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0ee29-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="0ee29-108">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="0ee29-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="0ee29-109">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="0ee29-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="0ee29-110">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="0ee29-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0ee29-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0ee29-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="0ee29-112">Per informazioni sull'uso di Phoenix su HDInsight basato su Linux, vedere [Usare Apache Phoenix con cluster HBase basati su Linux in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0ee29-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="0ee29-113">Usare SQLLine</span><span class="sxs-lookup"><span data-stu-id="0ee29-113">Use SQLLine</span></span>
<span data-ttu-id="0ee29-114">[SQLLine](http://sqlline.sourceforge.net/) è un'utilità della riga di comando per eseguire SQL.</span><span class="sxs-lookup"><span data-stu-id="0ee29-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0ee29-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0ee29-115">Prerequisites</span></span>
<span data-ttu-id="0ee29-116">Per usare SQLLine sono necessari:</span><span class="sxs-lookup"><span data-stu-id="0ee29-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="0ee29-117">**Un cluster HBase in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="0ee29-118">Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="0ee29-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="0ee29-119">**Connessione al cluster HBase tramite il file RDP (Remote Desktop Protocol)**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="0ee29-120">Per istruzioni, vedere l'articolo su come [gestire cluster Hadoop in HDInsight con il portale di Azure classico][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="0ee29-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="0ee29-121">**Per individuare il nome host**</span><span class="sxs-lookup"><span data-stu-id="0ee29-121">**To find out the host name**</span></span>

1. <span data-ttu-id="0ee29-122">Aprire la **riga di comando di Hadoop** dal desktop.</span><span class="sxs-lookup"><span data-stu-id="0ee29-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="0ee29-123">Eseguire il comando seguente per richiamare il suffisso DNS:</span><span class="sxs-lookup"><span data-stu-id="0ee29-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="0ee29-124">Annotare il **suffisso DNS specifico della connessione**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="0ee29-125">Ad esempio, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="0ee29-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="0ee29-126">Quando ci si connette a un cluster HBase, sarà necessario connettersi a uno dei Zookeeper usando il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="0ee29-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="0ee29-127">Ogni cluster HDInsight ha tre Zookeeper:</span><span class="sxs-lookup"><span data-stu-id="0ee29-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="0ee29-128">*zookeeper0*, *zookeeper1* e *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="0ee29-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="0ee29-129">Il nome di dominio completo sarà simile a *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="0ee29-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="0ee29-130">**Per usare SQLLine**</span><span class="sxs-lookup"><span data-stu-id="0ee29-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="0ee29-131">Aprire la **riga di comando di Hadoop** dal desktop.</span><span class="sxs-lookup"><span data-stu-id="0ee29-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="0ee29-132">Eseguire i comandi seguenti per aprire SQLLine:</span><span class="sxs-lookup"><span data-stu-id="0ee29-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight HBase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="0ee29-134">I comandi usati nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="0ee29-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="0ee29-135">Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="0ee29-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="0ee29-136">Usare SQuirreL</span><span class="sxs-lookup"><span data-stu-id="0ee29-136">Use SQuirreL</span></span>
<span data-ttu-id="0ee29-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) è un programma Java grafico che consente di visualizzare la struttura di un database conforme a JDBC, esplorare i dati nelle tabelle, eseguire comandi SQL e così via. Può essere usato per connettersi a Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee29-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="0ee29-138">Questa sezione illustra come installare e configurare SQuirreL sulla workstation per la connessione a un cluster HBase in HDInsight tramite VPN.</span><span class="sxs-lookup"><span data-stu-id="0ee29-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0ee29-139">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0ee29-139">Prerequisites</span></span>
<span data-ttu-id="0ee29-140">Prima di iniziare le procedure sono necessari:</span><span class="sxs-lookup"><span data-stu-id="0ee29-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="0ee29-141">Un cluster HBase distribuito in una rete virtuale di Azure con una macchina virtuale DNS.</span><span class="sxs-lookup"><span data-stu-id="0ee29-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="0ee29-142">Per istruzioni, vedere [Creare cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="0ee29-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="0ee29-143">Ottenere il suffisso DNS specifico della connessione per il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ee29-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="0ee29-144">Per ottenerlo, effettuare una connessione RDP al cluster e quindi eseguire IPConfig.</span><span class="sxs-lookup"><span data-stu-id="0ee29-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="0ee29-145">Il suffisso DNS è simile a:</span><span class="sxs-lookup"><span data-stu-id="0ee29-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="0ee29-146">Scaricare e installare [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="0ee29-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="0ee29-147">Sarà necessario eseguire lo strumento MakeCert dal pacchetto per creare il certificato.</span><span class="sxs-lookup"><span data-stu-id="0ee29-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="0ee29-148">Scaricare e installare [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="0ee29-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="0ee29-149">SQuirreL SQL Client versione 3.0 e versioni successive richiede la versione JRE 1.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="0ee29-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="0ee29-150">Configurare una connessione VPN Point-to-Site alla rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0ee29-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="0ee29-151">La configurazione di una connessione VPN Point-To-Site prevede tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="0ee29-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="0ee29-152">Configurare una rete virtuale e un gateway di routing dinamico</span><span class="sxs-lookup"><span data-stu-id="0ee29-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="0ee29-153">Creare i certificati</span><span class="sxs-lookup"><span data-stu-id="0ee29-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="0ee29-154">Configurare il client VPN</span><span class="sxs-lookup"><span data-stu-id="0ee29-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="0ee29-155">Per altre informazioni, vedere [Configurare una connessione VPN Point-to-Site alla rete virtuale di Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) .</span><span class="sxs-lookup"><span data-stu-id="0ee29-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="0ee29-156">Configurare una rete virtuale e un gateway di routing dinamico</span><span class="sxs-lookup"><span data-stu-id="0ee29-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="0ee29-157">Assicurarsi di aver eseguito il provisioning di un cluster HBase in una rete virtuale di Azure (vedere i prerequisiti per questa sezione).</span><span class="sxs-lookup"><span data-stu-id="0ee29-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="0ee29-158">Il passaggio successivo consiste nel configurare una connessione Point-to-Site.</span><span class="sxs-lookup"><span data-stu-id="0ee29-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="0ee29-159">**Per configurare la connettività Point-to-Site**</span><span class="sxs-lookup"><span data-stu-id="0ee29-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="0ee29-160">Accedere al [portale di Azure classico][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0ee29-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="0ee29-161">A sinistra, fare clic su **RETI**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="0ee29-162">Fare clic sulla rete virtuale creata (vedere l'articolo relativo al [provisioning di cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="0ee29-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="0ee29-163">Fare clic su **CONFIGURA** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="0ee29-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="0ee29-164">Nella sezione **Connettività Point-to-Site** selezionare **Configura connettività Point-to-Site**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="0ee29-165">Configurare **IP iniziale** e **CIDR** per specificare l'intervallo indirizzi IP dal quale i client VPN riceveranno un indirizzo IP durante la connessione.</span><span class="sxs-lookup"><span data-stu-id="0ee29-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="0ee29-166">L'intervallo non può sovrapporsi con nessuno degli intervalli all'interno della rete locale e la rete virtuale di Azure alla quale si effettuerà la connessione.</span><span class="sxs-lookup"><span data-stu-id="0ee29-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="0ee29-167">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="0ee29-167">For example.</span></span> <span data-ttu-id="0ee29-168">se si seleziona 10.0.0.0/20 per la rete virtuale è possibile selezionare 10.1.0.0/24 per lo spazio degli indirizzi dei client.</span><span class="sxs-lookup"><span data-stu-id="0ee29-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="0ee29-169">Per altre informazioni, vedere la pagina relativa alla [connettività Point-To-Site][vnet-point-to-site-connectivity].</span><span class="sxs-lookup"><span data-stu-id="0ee29-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="0ee29-170">Nella sezione relativa agli spazi di indirizzi della rete virtuale, fare clic su **Aggiungi subnet gateway**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="0ee29-171">Fare clic su **SALVA** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="0ee29-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="0ee29-172">Fare clic **SÌ** per confermare la modifica.</span><span class="sxs-lookup"><span data-stu-id="0ee29-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="0ee29-173">Attendere che il sistema abbia terminato di apportare la modifica prima di passare alla procedura successiva.</span><span class="sxs-lookup"><span data-stu-id="0ee29-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="0ee29-174">**Per creare un gateway di routing dinamico**</span><span class="sxs-lookup"><span data-stu-id="0ee29-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="0ee29-175">Dal portale di Azure classico, fare clic su **DASHBOARD** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="0ee29-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="0ee29-176">Fare clic su **CREA GATEWAY** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="0ee29-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="0ee29-177">Fare clic su **SÌ** per confermare.</span><span class="sxs-lookup"><span data-stu-id="0ee29-177">Click **YES** to confirm.</span></span> <span data-ttu-id="0ee29-178">Attendere la creazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="0ee29-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="0ee29-179">Fare clic su **DASHBOARD** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="0ee29-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="0ee29-180">Verrà visualizzato un grafico visuale della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="0ee29-180">You will see a visual diagram of the virtual network:</span></span>

    ![Diagramma virtuale Point-to-Site della rete virtuale di Azure][img-vnet-diagram]

    <span data-ttu-id="0ee29-182">Il diagramma mostra 0 connessioni client.</span><span class="sxs-lookup"><span data-stu-id="0ee29-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="0ee29-183">Dopo aver eseguito una connessione alla rete virtuale, il numero verrà aggiornato a uno.</span><span class="sxs-lookup"><span data-stu-id="0ee29-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="0ee29-184">Creare i certificati</span><span class="sxs-lookup"><span data-stu-id="0ee29-184">Create your certificates</span></span>
<span data-ttu-id="0ee29-185">Un modo per creare un certificato X.509 consiste nell'usare lo strumento di creazione certificati (makecert.exe) fornito con [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ee29-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="0ee29-186">**Per creare un certificato radice autofirmato**</span><span class="sxs-lookup"><span data-stu-id="0ee29-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="0ee29-187">Dalla workstation, aprire una finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0ee29-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="0ee29-188">Passare alla cartella Strumenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ee29-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="0ee29-189">Il comando nell'esempio seguente consente di creare e installare un certificato radice nell'archivio certificati personale nella workstation e creare anche un file corrispondente con estensione cer da caricare in seguito nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0ee29-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="0ee29-190">Passare alla directory in cui si vuole inserire il file con estensione cer, dove HBaseVnetVPNRootCertificate è il nome che si vuole usare per il certificato.</span><span class="sxs-lookup"><span data-stu-id="0ee29-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="0ee29-191">Non chiudere il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0ee29-191">Don't close the command prompt.</span></span>  <span data-ttu-id="0ee29-192">Sarà necessario nella procedura successiva.</span><span class="sxs-lookup"><span data-stu-id="0ee29-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ee29-193">Poiché è stato creato un certificato radice da cui verranno generati i certificati client, è possibile esportarlo, insieme alla relativa chiave privata e salvarlo in una posizione sicura dove può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="0ee29-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="0ee29-194">**Per creare un certificato client**</span><span class="sxs-lookup"><span data-stu-id="0ee29-194">**To create a client certificate**</span></span>

* <span data-ttu-id="0ee29-195">Dallo stesso prompt dei comandi (deve essere sullo stesso computer in cui è stato creato il certificato radice.</span><span class="sxs-lookup"><span data-stu-id="0ee29-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="0ee29-196">Il certificato client deve essere generato dal certificato principale), eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0ee29-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="0ee29-197">HBaseVnetVPNRootCertificate è il nome del certificato radice.</span><span class="sxs-lookup"><span data-stu-id="0ee29-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="0ee29-198">Deve corrispondere al nome del certificato radice.</span><span class="sxs-lookup"><span data-stu-id="0ee29-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="0ee29-199">Il certificato radice e il certificato client vengono archiviati nell'archivio certificati personali del computer.</span><span class="sxs-lookup"><span data-stu-id="0ee29-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="0ee29-200">Usare certmgr.msc per verificare.</span><span class="sxs-lookup"><span data-stu-id="0ee29-200">Use certmgr.msc to verify.</span></span>

    ![Certificato VPN Point-to-Site della rete virtuale di Azure][img-certificate]

    <span data-ttu-id="0ee29-202">Un certificato client deve essere installato in ogni computer che si connette alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ee29-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="0ee29-203">Si consiglia di creare client univoci certificati per ogni computer che si desidera connettersi alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ee29-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="0ee29-204">Per esportare i certificati client, usare certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="0ee29-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="0ee29-205">**Per caricare il certificato radice nel portale di Azure classico**</span><span class="sxs-lookup"><span data-stu-id="0ee29-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="0ee29-206">Dal portale di Azure classico, fare clic su **RETE** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0ee29-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="0ee29-207">Fare clic sulla rete virtuale in cui è stato distribuito il cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ee29-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="0ee29-208">Fare clic su **CERTIFICATI** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="0ee29-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="0ee29-209">Fare clic **CARICA** dalla parte inferiore e specificare il file del certificato radice creato nella penultima procedura.</span><span class="sxs-lookup"><span data-stu-id="0ee29-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="0ee29-210">Attendere che il certificato sia stato importato.</span><span class="sxs-lookup"><span data-stu-id="0ee29-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="0ee29-211">Fare clic su **DASHBOARD** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="0ee29-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="0ee29-212">Lo stato viene mostrato nel diagramma virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ee29-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="0ee29-213">Configurare il client VPN</span><span class="sxs-lookup"><span data-stu-id="0ee29-213">Configure your VPN client</span></span>
<span data-ttu-id="0ee29-214">**Per scaricare e installare il pacchetto VPN del client**</span><span class="sxs-lookup"><span data-stu-id="0ee29-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="0ee29-215">Nella sezione di riepilogo rapido della pagina DASHBOARD della rete virtuale fare clic su **Scarica pacchetto VPN client a 64 bit** o su **Scarica pacchetto VPN client a 32 bit** in base alla versione del sistema operativo della workstation.</span><span class="sxs-lookup"><span data-stu-id="0ee29-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="0ee29-216">Fare clic su **Esegui** per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0ee29-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="0ee29-217">Quando viene visualizzato l'avviso di sicurezza, fare clic su **Altre informazioni** e quindi su **Esegui comunque**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="0ee29-218">Fare clic due volte su **Sì** .</span><span class="sxs-lookup"><span data-stu-id="0ee29-218">Click **Yes** twice.</span></span>

<span data-ttu-id="0ee29-219">**Per connettersi alla rete VPN**</span><span class="sxs-lookup"><span data-stu-id="0ee29-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="0ee29-220">Sul desktop della workstation, fare clic sull'icona Reti sulla barra delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0ee29-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="0ee29-221">Verrà visualizzata una connessione VPN con il nome della propria rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ee29-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="0ee29-222">Fare clic sul nome della connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="0ee29-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="0ee29-223">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-223">Click **Connect**.</span></span>

<span data-ttu-id="0ee29-224">**Per testare la risoluzione del nome dominio e la connessione VPN**</span><span class="sxs-lookup"><span data-stu-id="0ee29-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="0ee29-225">Dalla workstation, aprire un prompt dei comandi ed eseguire il ping di uno dei seguenti nomi dato che il suffisso DNS del cluster HBase è myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="0ee29-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="0ee29-226">Installare e configurare SQuirreL sulla workstation</span><span class="sxs-lookup"><span data-stu-id="0ee29-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="0ee29-227">**Per installare SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="0ee29-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="0ee29-228">Scaricare il file jar di SQL SQuirreL Client da [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="0ee29-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="0ee29-229">Aprire/eseguire il file jar.</span><span class="sxs-lookup"><span data-stu-id="0ee29-229">Open/run the jar file.</span></span> <span data-ttu-id="0ee29-230">È richiesto [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="0ee29-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="0ee29-231">Fare clic su **Next** due volte.</span><span class="sxs-lookup"><span data-stu-id="0ee29-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="0ee29-232">Specificare un percorso per cui si dispone dell'autorizzazione di scrittura e fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0ee29-233">La cartella di installazione predefinita è nella cartella c:\Programmi\Microsoft Files\squirrel-sql-3.6.</span><span class="sxs-lookup"><span data-stu-id="0ee29-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="0ee29-234">Per scrivere in questo percorso, al programma di installazione devono essere concessi i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="0ee29-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="0ee29-235">È possibile aprire un prompt dei comandi come amministratore, passare alla cartella bin di Java e quindi eseguire:</span><span class="sxs-lookup"><span data-stu-id="0ee29-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="0ee29-236">java.exe -jar [percorso del file JAR SQuirreL]</span><span class="sxs-lookup"><span data-stu-id="0ee29-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="0ee29-237">Fare clic su **OK** per confermare la creazione della directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0ee29-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="0ee29-238">L'impostazione predefinita consiste nell'installare i pacchetti Base e Standard.</span><span class="sxs-lookup"><span data-stu-id="0ee29-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="0ee29-239">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-239">Click **Next**.</span></span>
7. <span data-ttu-id="0ee29-240">Fare clic su **Next** (Avanti) due volte e quindi su **Done** (Fine).</span><span class="sxs-lookup"><span data-stu-id="0ee29-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="0ee29-241">**Per installare il driver Phoenix**</span><span class="sxs-lookup"><span data-stu-id="0ee29-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="0ee29-242">Il file jar del driver Phoenix si trova nel cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ee29-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="0ee29-243">Il percorso è simile al seguente in base alle versioni:</span><span class="sxs-lookup"><span data-stu-id="0ee29-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="0ee29-244">È necessario copiarlo nella workstation nel percorso [cartella di installazione SQuirreL]/lib.</span><span class="sxs-lookup"><span data-stu-id="0ee29-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="0ee29-245">Il modo più semplice consiste nell'effettuare una connessione RDP al cluster e quindi copiare e incollare il file (CTRL + C e CTRL + V) nella workstation.</span><span class="sxs-lookup"><span data-stu-id="0ee29-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="0ee29-246">**Per aggiungere un driver di Phoenix a SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="0ee29-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="0ee29-247">Aprire SQuirreL SQL Client dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="0ee29-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="0ee29-248">Fare clic sulla scheda **Driver** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0ee29-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="0ee29-249">Scegliere **New Driver** (Nuovo driver) dal menu **Driver**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="0ee29-250">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="0ee29-250">Enter the following information:</span></span>

   * <span data-ttu-id="0ee29-251">**Name**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="0ee29-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="0ee29-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="0ee29-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="0ee29-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="0ee29-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="0ee29-254">Usare solo lettere minuscole nell'URL di esempio.</span><span class="sxs-lookup"><span data-stu-id="0ee29-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="0ee29-255">È possibile usare il quorum zookeeper completo nel caso in cui uno di essi sia inattivo.</span><span class="sxs-lookup"><span data-stu-id="0ee29-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="0ee29-256">I nomi host sono zookeeper0, zookeeper1 e zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="0ee29-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. <span data-ttu-id="0ee29-258">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-258">Click **OK**.</span></span>

<span data-ttu-id="0ee29-259">**Per creare un alias per il cluster HBase**</span><span class="sxs-lookup"><span data-stu-id="0ee29-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="0ee29-260">Da SQuirreL, fare clic sulla scheda **Alias** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0ee29-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="0ee29-261">Scegliere **New Alias** (Nuovo alias) dal menu **Aliases** (Alias).</span><span class="sxs-lookup"><span data-stu-id="0ee29-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="0ee29-262">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="0ee29-262">Enter the following information:</span></span>

   * <span data-ttu-id="0ee29-263">**Name**: il nome del cluster HBase o qualsiasi altro nome.</span><span class="sxs-lookup"><span data-stu-id="0ee29-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="0ee29-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="0ee29-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="0ee29-265">Deve corrispondere al nome del driver creato nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="0ee29-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="0ee29-266">**URL**: l'URL viene copiato dalla configurazione del driver.</span><span class="sxs-lookup"><span data-stu-id="0ee29-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="0ee29-267">Assicurarsi di usare solo lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="0ee29-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="0ee29-268">**Nome utente**: può essere qualsiasi testo.</span><span class="sxs-lookup"><span data-stu-id="0ee29-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="0ee29-269">Poiché qui viene usata la connettività VPN, il nome utente non viene utilizzato affatto.</span><span class="sxs-lookup"><span data-stu-id="0ee29-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="0ee29-270">**Password**: può essere qualsiasi testo.</span><span class="sxs-lookup"><span data-stu-id="0ee29-270">**Password**: It can be any text.</span></span>

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. <span data-ttu-id="0ee29-272">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-272">Click **Test**.</span></span>
5. <span data-ttu-id="0ee29-273">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-273">Click **Connect**.</span></span> <span data-ttu-id="0ee29-274">Quando viene effettuata la connessione, SQuirreL ha l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="0ee29-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="0ee29-276">**Per eseguire un test**</span><span class="sxs-lookup"><span data-stu-id="0ee29-276">**To run a test**</span></span>

1. <span data-ttu-id="0ee29-277">Fare clic sulla scheda **SQL** accanto alla scheda **Objects** (Oggetti).</span><span class="sxs-lookup"><span data-stu-id="0ee29-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="0ee29-278">Copiare e incollare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0ee29-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="0ee29-279">Fare clic sul pulsante di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0ee29-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="0ee29-281">Tornare alla scheda **Objects** .</span><span class="sxs-lookup"><span data-stu-id="0ee29-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="0ee29-282">Espandere il nome alias, quindi espandere **TABLE**.</span><span class="sxs-lookup"><span data-stu-id="0ee29-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="0ee29-283">La nuova tabella verrà elencata nell'area sottostante.</span><span class="sxs-lookup"><span data-stu-id="0ee29-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ee29-284">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ee29-284">Next steps</span></span>
<span data-ttu-id="0ee29-285">In questo articolo si è appreso come usare Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee29-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="0ee29-286">Per altre informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="0ee29-286">To learn more, see</span></span>

* <span data-ttu-id="0ee29-287">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="0ee29-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="0ee29-288">[Effettuare il provisioning di cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione con la rete virtuale, i cluster HBase possono essere distribuiti nella stessa rete virtuale delle applicazioni in modo che queste ultime possano comunicare direttamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="0ee29-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="0ee29-289">[Configurare la replica HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come configurare la replica HBase in due data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee29-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="0ee29-290">[Analizzare il sentiment di Twitter con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come eseguire l'[analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei Big Data usando HBase in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ee29-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
