---
title: Monitorare e gestire Azure HDInsight con l'interfaccia utente Web Ambari | Documentazione Microsoft
description: Informazioni sull'uso di Ambari per monitorare e gestire cluster HDInsight basati su Linux. Questo documento spiega come usare l'interfaccia utente Web di Ambari inclusa nei cluster HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="9631e-104">Gestire i cluster HDInsight mediante l'utilizzo dell'interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="9631e-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="9631e-105">Apache Ambari semplifica la gestione e il monitoraggio di un cluster Hadoop grazie a un'interfaccia utente Web facile da usare e alle API REST.</span><span class="sxs-lookup"><span data-stu-id="9631e-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="9631e-106">Ambari è incluso nei cluster HDInsight basati su Linux e viene usato per monitorare il cluster e modificare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="9631e-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="9631e-107">Questo documento spiega come usare l'interfaccia utente Web Ambari con un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="9631e-108"><a id="whatis"></a>Cos'è Ambari?</span><span class="sxs-lookup"><span data-stu-id="9631e-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="9631e-109">[Apache Ambari](http://ambari.apache.org) semplifica la gestione di Hadoop, fornendo un'interfaccia utente Web di facile utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9631e-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="9631e-110">È possibile usare Ambari per creare, gestire e monitorare cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9631e-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="9631e-111">Gli sviluppatori possono integrare queste funzionalità nelle applicazioni usando le [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="9631e-112">L'interfaccia utente Web Ambari è disponibile per impostazione predefinita con i cluster HDInsight che usano il sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="9631e-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9631e-113">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9631e-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9631e-114">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9631e-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="9631e-115">Connettività</span><span class="sxs-lookup"><span data-stu-id="9631e-115">Connectivity</span></span>

<span data-ttu-id="9631e-116">L'interfaccia utente Web Ambari è disponibile nel cluster HDInsight all'indirizzo HTTPS://CLUSTERNAME.azurehdidnsight.net, dove **CLUSTERNAME** è il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9631e-117">La connessione ad Ambari su HDInsight richiede HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9631e-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="9631e-118">Quando viene richiesta l'autenticazione, usare il nome e la password dell'account amministratore specificati quando è stato creato il cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="9631e-119">Tunnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="9631e-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="9631e-120">Mentre Ambari per il cluster è accessibile direttamente tramite Internet, alcuni collegamenti dall'interfaccia utente Web di Ambari (ad esempio JobTracker) non sono esposti in Internet.</span><span class="sxs-lookup"><span data-stu-id="9631e-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="9631e-121">Per accedere a questi servizi, è necessario creare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="9631e-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="9631e-122">Per altre informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="9631e-123">Interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="9631e-123">Ambari Web UI</span></span>

<span data-ttu-id="9631e-124">Quando ci si connette all'interfaccia utente Web di Ambari, è necessario eseguire l'autenticazione alla pagina.</span><span class="sxs-lookup"><span data-stu-id="9631e-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="9631e-125">Usare l'utente (valore predefinito Admin) e la password di amministrazione del cluster specificati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="9631e-126">Quando si apre la pagina, si noti la barra in alto,</span><span class="sxs-lookup"><span data-stu-id="9631e-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="9631e-127">che contiene le informazioni e i controlli seguenti:</span><span class="sxs-lookup"><span data-stu-id="9631e-127">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="9631e-129">**Logo di Ambari** : apre il dashboard, che può essere usato per monitorare il cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="9631e-130">**Numero di operazioni cluster** : visualizza il numero di operazioni in corso di Ambari.</span><span class="sxs-lookup"><span data-stu-id="9631e-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="9631e-131">Selezionando il nome del cluster o **# ops**, viene visualizzato un elenco delle operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="9631e-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="9631e-132">**# alerts**: visualizza eventuali messaggi di avviso o critici per il cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="9631e-133">**Dashboard** : visualizza il dashboard.</span><span class="sxs-lookup"><span data-stu-id="9631e-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="9631e-134">**Services** : informazioni e impostazioni di configurazione per i servizi del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="9631e-135">**Hosts** : informazioni e impostazioni di configurazione per i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="9631e-136">**Alerts** : log di informazioni, avvertenze e avvisi critici.</span><span class="sxs-lookup"><span data-stu-id="9631e-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="9631e-137">**Admin** - servizi/stack software che vengono installati nel cluster, informazioni sull'account di servizio e sicurezza Kerberos.</span><span class="sxs-lookup"><span data-stu-id="9631e-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="9631e-138">**Pulsante admin** : gestione di Ambari, impostazioni utente e disconnessione.</span><span class="sxs-lookup"><span data-stu-id="9631e-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="9631e-139">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="9631e-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="9631e-140">Avvisi</span><span class="sxs-lookup"><span data-stu-id="9631e-140">Alerts</span></span>

<span data-ttu-id="9631e-141">L'elenco seguente contiene gli stati di avviso comuni usati da Ambari:</span><span class="sxs-lookup"><span data-stu-id="9631e-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="9631e-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="9631e-142">**OK**</span></span>
* <span data-ttu-id="9631e-143">**Warning**</span><span class="sxs-lookup"><span data-stu-id="9631e-143">**Warning**</span></span>
* <span data-ttu-id="9631e-144">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="9631e-144">**CRITICAL**</span></span>
* <span data-ttu-id="9631e-145">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="9631e-145">**UNKNOWN**</span></span>

<span data-ttu-id="9631e-146">Gli avvisi con stato diverso da **OK** determinano la compilazione del campo **# alerts** (N. avvisi) nella parte superiore della pagina con il numero di avvisi.</span><span class="sxs-lookup"><span data-stu-id="9631e-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="9631e-147">Selezionando questa opzione vengono visualizzati gli avvisi e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="9631e-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="9631e-148">Gli avvisi sono organizzati in diversi gruppi predefiniti, che possono essere visualizzati dalla pagina **Alerts** .</span><span class="sxs-lookup"><span data-stu-id="9631e-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![pagina degli avvisi](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="9631e-150">È possibile gestire i gruppi scegliendo **Manage Alert Groups** (Gestisci gruppi di avvisi) dal menu **Actions** (Azioni).</span><span class="sxs-lookup"><span data-stu-id="9631e-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![finestra di dialogo Manage Alert Groups](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="9631e-152">È anche possibile gestire metodi di avviso e creare notifiche di avviso dal menu **Azioni**, selezionando __Manage Alert Notifications__ (Gestire notifiche di avviso).</span><span class="sxs-lookup"><span data-stu-id="9631e-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="9631e-153">Questa opzione consente di visualizzare le notifiche correnti</span><span class="sxs-lookup"><span data-stu-id="9631e-153">Any current notifications are displayed.</span></span> <span data-ttu-id="9631e-154">e di creare nuove notifiche.</span><span class="sxs-lookup"><span data-stu-id="9631e-154">You can also create notifications from here.</span></span> <span data-ttu-id="9631e-155">È possibile inviare notifiche tramite **EMAIL** o **SNMP** al verificarsi di specifiche combinazioni di avviso/gravità.</span><span class="sxs-lookup"><span data-stu-id="9631e-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="9631e-156">È possibile, ad esempio, inviare un messaggio e-mail quando uno degli avvisi del gruppo **YARN Default** (Impostazioni predefinite Yarn) viene impostato su **Critical** (Critico).</span><span class="sxs-lookup"><span data-stu-id="9631e-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![finestra di dialogo Create Alert](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="9631e-158">Selezionare infine __Manage Alert Settings__ (Gestire impostazioni di avviso) dal menu __Actions__ (Azioni) per stabilire il numero di volte in cui deve verificarsi un avviso prima che venga inviata una notifica.</span><span class="sxs-lookup"><span data-stu-id="9631e-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="9631e-159">Questa impostazione può essere usata per evitare notifiche relative ad errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="9631e-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="9631e-160">HDInsight</span><span class="sxs-lookup"><span data-stu-id="9631e-160">Cluster</span></span>

<span data-ttu-id="9631e-161">La scheda **Metrics** del dashboard contiene una serie di widget che consentono di monitorare lo stato del cluster in modo immediato.</span><span class="sxs-lookup"><span data-stu-id="9631e-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="9631e-162">Widget diversi, ad esempio **CPU Usage**, forniscono informazioni aggiuntive quando vengono selezionati.</span><span class="sxs-lookup"><span data-stu-id="9631e-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard con metriche](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="9631e-164">La scheda **Heatmaps** visualizza le metriche come mappe termiche colorate, dal verde al rosso.</span><span class="sxs-lookup"><span data-stu-id="9631e-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![dashboard con mappe termiche](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="9631e-166">Per altre informazioni sui nodi presenti nel cluster, selezionare **Host**.</span><span class="sxs-lookup"><span data-stu-id="9631e-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="9631e-167">Selezionare quindi il nodo desiderato.</span><span class="sxs-lookup"><span data-stu-id="9631e-167">Then select the specific node you are interested in.</span></span>

![dettagli dell'host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="9631e-169">Services</span><span class="sxs-lookup"><span data-stu-id="9631e-169">Services</span></span>

<span data-ttu-id="9631e-170">La barra laterale **Services** sul dashboard fornisce informazioni rapide sullo stato dei servizi in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="9631e-171">Vengono usate varie icone per indicare lo stato o le azioni da eseguire.</span><span class="sxs-lookup"><span data-stu-id="9631e-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="9631e-172">Un simbolo di riciclo giallo, ad esempio, indica che un servizio deve essere riciclato.</span><span class="sxs-lookup"><span data-stu-id="9631e-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![barra laterale dei servizi](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="9631e-174">I servizi visualizzati sono diversi per le diverse versioni e tipi di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="9631e-175">Quelli qui visualizzati possono differire da quelli visualizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="9631e-176">Selezionando un servizio vengono visualizzate informazioni più dettagliate su di esso.</span><span class="sxs-lookup"><span data-stu-id="9631e-176">Selecting a service displays more detailed information on the service.</span></span>

![informazioni di riepilogo sul servizio](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="9631e-178">Collegamenti rapidi</span><span class="sxs-lookup"><span data-stu-id="9631e-178">Quick links</span></span>

<span data-ttu-id="9631e-179">Alcuni servizi visualizzano un collegamento **Quick Links** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="9631e-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="9631e-180">Questi possono essere usati per accedere alle interfacce utente Web specifiche del servizio, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9631e-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="9631e-181">**Job History** : cronologia dei processi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9631e-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="9631e-182">**Resource Manager** : interfaccia utente di gestione risorse di YARN.</span><span class="sxs-lookup"><span data-stu-id="9631e-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="9631e-183">**NameNode** : interfaccia utente NameNode del file system distribuito Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="9631e-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="9631e-184">**Oozie Web UI** : interfaccia utente Oozie.</span><span class="sxs-lookup"><span data-stu-id="9631e-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="9631e-185">Selezionando uno di questi collegamenti, verrà aperta una nuova scheda nel browser che visualizzerà la pagina selezionata.</span><span class="sxs-lookup"><span data-stu-id="9631e-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="9631e-186">Se si seleziona la voce **Quick Links** (Collegamenti rapidi) per un servizio, è possibile che venga restituito un errore "server non disponibile".</span><span class="sxs-lookup"><span data-stu-id="9631e-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="9631e-187">Se si verifica questo errore, è necessario usare un tunnel SSH quando si seleziona la voce **Quick Links** (Collegamenti rapidi) per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="9631e-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="9631e-188">Per informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="9631e-189">gestione</span><span class="sxs-lookup"><span data-stu-id="9631e-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="9631e-190">Utenti, gruppi e autorizzazioni Ambari</span><span class="sxs-lookup"><span data-stu-id="9631e-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="9631e-191">L'uso di utenti, gruppi e autorizzazioni è supportato con un cluster HDInsight [aggiunto al dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="9631e-192">Per informazioni sull'uso dell'interfaccia utente di gestione di Ambari in un cluster aggiunto al dominio, vedere [Gestire cluster HDInsight aggiunti al dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="9631e-193">Non modificare la password del watchdog Ambari (hdinsightwatchdog) nel cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="9631e-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9631e-194">Se si modifica la password, non sarà più possibile usare azioni script o eseguire operazioni di ridimensionamento con il cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="9631e-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="9631e-195">Hosts</span></span>

<span data-ttu-id="9631e-196">La pagina **Hosts** elenca tutti gli host del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="9631e-197">Per gestire gli host, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="9631e-197">To manage hosts, follow these steps.</span></span>

![pagina Hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="9631e-199">Non usare le procedure per aggiungere, rimuovere o ripristinare un host con cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="9631e-200">Selezionare l'host che si vuole gestire.</span><span class="sxs-lookup"><span data-stu-id="9631e-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="9631e-201">Usare il menu **Actions** per selezionare l'azione da eseguire:</span><span class="sxs-lookup"><span data-stu-id="9631e-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="9631e-202">**Start all components** : avvia tutti i componenti nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="9631e-203">**Stop all components** : arresta tutti i componenti nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="9631e-204">**Restart all components** : arresta e avvia tutti i componenti nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="9631e-205">**Turn on maintenance mode** : elimina gli avvisi per l'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="9631e-206">Questa modalità deve essere abilitata se si eseguono azioni che generano avvisi,</span><span class="sxs-lookup"><span data-stu-id="9631e-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="9631e-207">come l'arresto e l'avvio di un servizio.</span><span class="sxs-lookup"><span data-stu-id="9631e-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="9631e-208">**Turn off maintenance mode** : ripristina la gestione normale degli avvisi dell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="9631e-209">**Stop** : arresta DataNode o NodeManagers nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="9631e-210">**Start** : avvia DataNode o NodeManagers nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="9631e-211">**Restart** : arresta e avvia DataNode o NodeManagers nell'host.</span><span class="sxs-lookup"><span data-stu-id="9631e-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="9631e-212">**Decommission** : rimuove un host dal cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9631e-213">Non usare questa azione nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="9631e-214">**Recommission** : aggiunge al cluster un host precedentemente rimosso.</span><span class="sxs-lookup"><span data-stu-id="9631e-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9631e-215">Non usare questa azione nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="9631e-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="9631e-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="9631e-217">Nella pagina **Dashboard** (Dashboard) o **Services** (Servizi) usare il pulsante **Actions** (Azioni) nella parte inferiore dell'elenco di servizi per arrestare e avviare tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="9631e-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="9631e-219">Anche se **Add Service** (Aggiungi servizio) è elencato in questo menu, non deve essere usato per aggiungere servizi al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9631e-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="9631e-220">È necessario aggiungere nuovi servizi.utilizzando un'azione di Script durante il provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="9631e-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="9631e-221">Per altre informazioni su come utilizzare le azioni di script, vedere [Personalizzare cluster HDInsight mediante l'azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="9631e-222">Il pulsante **Actions** consente di riavviare tutti i servizi, ma spesso si desidera avviare, arrestare o riavviare un servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="9631e-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="9631e-223">Seguire questa procedura per effettuare azioni per un singolo servizio:</span><span class="sxs-lookup"><span data-stu-id="9631e-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="9631e-224">Nella pagina **Dashboard** (Dashboard) o **Services** (Servizi) selezionare un servizio.</span><span class="sxs-lookup"><span data-stu-id="9631e-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="9631e-225">Nella parte superiore della scheda **Summary** (Riepilogo) fare clic sul pulsante **Service Actions** (Azioni servizio) e selezionare l'azione da intraprendere.</span><span class="sxs-lookup"><span data-stu-id="9631e-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="9631e-226">Il servizio viene riavviato in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="9631e-226">This restarts the service on all nodes.</span></span>

    ![azione del servizio](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="9631e-228">Se si riavviano alcuni servizi mentre il cluster è in esecuzione, è possibile che vengano generati avvisi.</span><span class="sxs-lookup"><span data-stu-id="9631e-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="9631e-229">Per evitare gli avvisi, è possibile usare il pulsante **Service Actions** (Azioni servizio) per abilitare **Maintenance mode** (Modalità manutenzione) per il servizio prima di eseguire il riavvio.</span><span class="sxs-lookup"><span data-stu-id="9631e-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="9631e-230">Dopo aver selezionato un'azione, il valore nel campo **# op** nella parte superiore della pagina aumenta per indicare che è in corso un'operazione in background.</span><span class="sxs-lookup"><span data-stu-id="9631e-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="9631e-231">Se configurato, viene visualizzato l'elenco delle operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="9631e-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9631e-232">Se è stata abilitata la **modalità di manutenzione** per il servizio, ricordarsi di disabilitarla usando il pulsante **Service Actions** (Azioni servizio) al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="9631e-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="9631e-233">Per configurare un servizio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9631e-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="9631e-234">Nella pagina **Dashboard** (Dashboard) o **Services** (Servizi) selezionare un servizio.</span><span class="sxs-lookup"><span data-stu-id="9631e-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="9631e-235">Selezionare la scheda **Configs** (Configurazioni).</span><span class="sxs-lookup"><span data-stu-id="9631e-235">Select the **Configs** tab.</span></span> <span data-ttu-id="9631e-236">Verrà visualizzata la configurazione corrente,</span><span class="sxs-lookup"><span data-stu-id="9631e-236">The current configuration is displayed.</span></span> <span data-ttu-id="9631e-237">insieme a un elenco delle configurazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="9631e-237">A list of previous configurations is also displayed.</span></span>

    ![configurazioni](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="9631e-239">Usare i campi visualizzati per modificare la configurazione, quindi selezionare **Save**.</span><span class="sxs-lookup"><span data-stu-id="9631e-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="9631e-240">In alternativa, selezionare una configurazione precedente, quindi **Make current** per ripristinare le impostazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="9631e-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="9631e-241">Viste di Ambari</span><span class="sxs-lookup"><span data-stu-id="9631e-241">Ambari views</span></span>

<span data-ttu-id="9631e-242">Le viste di Ambari consentono agli sviluppatori di collegare gli elementi dell'interfaccia utente all'interfaccia utente Web di Ambari usando il [framework delle viste di Ambari](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="9631e-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="9631e-243">HDInsight fornisce le viste seguenti i con tipi di cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="9631e-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="9631e-244">Gestore di code Yarn: il gestore delle code fornisce un'interfaccia utente semplice per la visualizzazione e la modifica di code YARN.</span><span class="sxs-lookup"><span data-stu-id="9631e-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="9631e-245">Viste di Hive: le viste di Hive consentono di eseguire query Hive direttamente dal Web browser.</span><span class="sxs-lookup"><span data-stu-id="9631e-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="9631e-246">È possibile salvare query, visualizzare i risultati, salvare i risultati nell'archiviazione cluster o scaricare i risultati nel sistema locale.</span><span class="sxs-lookup"><span data-stu-id="9631e-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="9631e-247">Per altre informazioni sull'uso delle viste di Hive, vedere l'argomento relativo all' [uso delle viste Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="9631e-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="9631e-248">Vista Tez: la vista Tez consente di comprendere meglio e ottimizzare i processi.</span><span class="sxs-lookup"><span data-stu-id="9631e-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="9631e-249">È possibile visualizzare informazioni sulle modalità di esecuzione dei processi Tez e sulle risorse usate.</span><span class="sxs-lookup"><span data-stu-id="9631e-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
