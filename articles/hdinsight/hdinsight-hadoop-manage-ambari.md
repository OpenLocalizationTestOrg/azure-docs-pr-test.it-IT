---
title: aaaMonitor e la gestione di Azure HDInsight con Ambari Web UI | Documenti Microsoft
description: "Informazioni su come toouse Ambari toomonitor e gestire cluster HDInsight basati su Linux. Nel presente documento, si apprenderà come cluster di hello toouse dell'interfaccia utente Web Ambari incluso in HDInsight."
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
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="17aa8-104">Gestire cluster HDInsight con Ambari Web UI hello</span><span class="sxs-lookup"><span data-stu-id="17aa8-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="17aa8-105">Ambari Apache semplifica la gestione hello e monitoraggio di un cluster Hadoop fornendo un web toouse semplice interfaccia utente e REST API.</span><span class="sxs-lookup"><span data-stu-id="17aa8-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="17aa8-106">Ambari è incluso nei cluster HDInsight basati su Linux ed è utilizzato toomonitor hello cluster e apportare modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="17aa8-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="17aa8-107">In questo documento viene illustrato come toouse hello dell'interfaccia utente Web Ambari con un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17aa8-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="17aa8-108"><a id="whatis"></a>Cos'è Ambari?</span><span class="sxs-lookup"><span data-stu-id="17aa8-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="17aa8-109">[Apache Ambari](http://ambari.apache.org) semplifica la gestione di Hadoop, fornendo un'interfaccia utente Web di facile utilizzo.</span><span class="sxs-lookup"><span data-stu-id="17aa8-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="17aa8-110">È possibile usare Ambari per creare, gestire e monitorare cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="17aa8-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="17aa8-111">Gli sviluppatori possono integrare queste funzionalità nelle proprie applicazioni utilizzando hello [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="17aa8-112">interfaccia utente Web Ambari Hello viene fornito per impostazione predefinita con i cluster HDInsight che utilizzano il sistema operativo Linux di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17aa8-113">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="17aa8-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="17aa8-114">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="17aa8-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="17aa8-115">Connettività</span><span class="sxs-lookup"><span data-stu-id="17aa8-115">Connectivity</span></span>

<span data-ttu-id="17aa8-116">interfaccia utente Web Ambari Hello è disponibile nel cluster HDInsight in HTTPS://CLUSTERNAME.azurehdidnsight.net, in cui **CLUSTERNAME** hello nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17aa8-117">Connessione tooAmbari in HDInsight richiede HTTPS.</span><span class="sxs-lookup"><span data-stu-id="17aa8-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="17aa8-118">Quando richiesto per l'autenticazione, utilizzare nome dell'account admin hello e la password forniti quando è stato creato il cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="17aa8-119">Tunnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="17aa8-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="17aa8-120">Mentre Ambari per il cluster è accessibile direttamente su Internet hello, alcuni collegamenti da hello dell'interfaccia utente Web Ambari (ad esempio toohello JobTracker) non sono esposte in hello internet.</span><span class="sxs-lookup"><span data-stu-id="17aa8-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="17aa8-121">tooaccess questi servizi, è necessario creare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="17aa8-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="17aa8-122">Per altre informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="17aa8-123">Interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="17aa8-123">Ambari Web UI</span></span>

<span data-ttu-id="17aa8-124">Durante la connessione dell'interfaccia utente Web Ambari toohello, verrà richiesta tooauthenticate toohello pagina.</span><span class="sxs-lookup"><span data-stu-id="17aa8-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="17aa8-125">Utilizzare l'utente di amministrazione cluster hello (impostazione predefinita Admin) e la password utilizzati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="17aa8-126">Quando si apre la pagina hello, si noti la barra hello nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="17aa8-127">Questa barra contiene seguente hello informazioni e i controlli:</span><span class="sxs-lookup"><span data-stu-id="17aa8-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="17aa8-129">**Logo Ambari** -apre hello dashboard in cui può essere utilizzato toomonitor hello cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="17aa8-130">**Cluster ops # nome** -Visualizza il numero di hello di operazioni Ambari in corso.</span><span class="sxs-lookup"><span data-stu-id="17aa8-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="17aa8-131">Se si seleziona il nome del cluster hello o **ops #** Visualizza un elenco di operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="17aa8-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="17aa8-132">**gli avvisi #** -consente di visualizzare gli avvisi o gli avvisi critici, se presente, per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="17aa8-133">**Dashboard** -dashboard hello Visualizza.</span><span class="sxs-lookup"><span data-stu-id="17aa8-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="17aa8-134">**Servizi** -informazioni e impostazioni di configurazione per i servizi cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="17aa8-135">**Host** -informazioni e impostazioni di configurazione per i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="17aa8-136">**Alerts** : log di informazioni, avvertenze e avvisi critici.</span><span class="sxs-lookup"><span data-stu-id="17aa8-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="17aa8-137">**Amministrazione** -stack di Software e servizi installate nel cluster hello, informazioni sull'account di servizio e di sicurezza Kerberos.</span><span class="sxs-lookup"><span data-stu-id="17aa8-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="17aa8-138">**Pulsante admin** : gestione di Ambari, impostazioni utente e disconnessione.</span><span class="sxs-lookup"><span data-stu-id="17aa8-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="17aa8-139">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="17aa8-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="17aa8-140">Avvisi</span><span class="sxs-lookup"><span data-stu-id="17aa8-140">Alerts</span></span>

<span data-ttu-id="17aa8-141">Hello elenco seguente contiene hello comuni avviso utilizzato da Ambari:</span><span class="sxs-lookup"><span data-stu-id="17aa8-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="17aa8-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="17aa8-142">**OK**</span></span>
* <span data-ttu-id="17aa8-143">**Warning**</span><span class="sxs-lookup"><span data-stu-id="17aa8-143">**Warning**</span></span>
* <span data-ttu-id="17aa8-144">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="17aa8-144">**CRITICAL**</span></span>
* <span data-ttu-id="17aa8-145">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="17aa8-145">**UNKNOWN**</span></span>

<span data-ttu-id="17aa8-146">Avvisi di diverso da **OK** causare hello **avvisi #** voce nella parte superiore di hello totale hello pagina toodisplay hello degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="17aa8-147">Selezionando questa voce consente di visualizzare gli avvisi di hello e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="17aa8-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="17aa8-148">Gli avvisi sono organizzati in diversi gruppi predefiniti, che possono essere visualizzati da hello **avvisi** pagina.</span><span class="sxs-lookup"><span data-stu-id="17aa8-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![pagina degli avvisi](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="17aa8-150">È possibile gestire i gruppi di hello utilizzando hello **azioni** menu e selezionando **Gestisci gruppi avviso**.</span><span class="sxs-lookup"><span data-stu-id="17aa8-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![finestra di dialogo Manage Alert Groups](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="17aa8-152">È anche possibile gestire metodi avvisi e creare le notifiche di avviso da hello **azioni** menu selezionando __gestire le notifiche di avviso__.</span><span class="sxs-lookup"><span data-stu-id="17aa8-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="17aa8-153">Questa opzione consente di visualizzare le notifiche correnti</span><span class="sxs-lookup"><span data-stu-id="17aa8-153">Any current notifications are displayed.</span></span> <span data-ttu-id="17aa8-154">e di creare nuove notifiche.</span><span class="sxs-lookup"><span data-stu-id="17aa8-154">You can also create notifications from here.</span></span> <span data-ttu-id="17aa8-155">È possibile inviare notifiche tramite **EMAIL** o **SNMP** al verificarsi di specifiche combinazioni di avviso/gravità.</span><span class="sxs-lookup"><span data-stu-id="17aa8-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="17aa8-156">Ad esempio, è possibile inviare un messaggio di posta elettronica quando uno degli avvisi di hello in hello **YARN predefinito** gruppo troppo**critico**.</span><span class="sxs-lookup"><span data-stu-id="17aa8-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![finestra di dialogo Create Alert](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="17aa8-158">Infine, la selezione __Gestione impostazioni di avviso__ da hello __azioni__ menu consente numero hello tooset deve occorrenze di un avviso prima che venga inviata una notifica.</span><span class="sxs-lookup"><span data-stu-id="17aa8-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="17aa8-159">Questa impostazione può essere utilizzato tooprevent notifiche per errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="17aa8-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="17aa8-160">HDInsight</span><span class="sxs-lookup"><span data-stu-id="17aa8-160">Cluster</span></span>

<span data-ttu-id="17aa8-161">Hello **metriche** scheda dashboard hello contiene una serie di widget che rendono lo stato di hello toomonitor semplice del cluster a colpo d'occhio.</span><span class="sxs-lookup"><span data-stu-id="17aa8-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="17aa8-162">Widget diversi, ad esempio **CPU Usage**, forniscono informazioni aggiuntive quando vengono selezionati.</span><span class="sxs-lookup"><span data-stu-id="17aa8-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard con metriche](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="17aa8-164">Hello **Heatmaps** scheda Visualizza le metriche come heatmaps colorato, passando da toored verde.</span><span class="sxs-lookup"><span data-stu-id="17aa8-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![dashboard con mappe termiche](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="17aa8-166">Per ulteriori informazioni sui nodi hello all'interno di cluster hello, selezionare **host**.</span><span class="sxs-lookup"><span data-stu-id="17aa8-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="17aa8-167">Selezionare quindi nodo specifico di hello che si è interessati.</span><span class="sxs-lookup"><span data-stu-id="17aa8-167">Then select hello specific node you are interested in.</span></span>

![dettagli dell'host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="17aa8-169">Services</span><span class="sxs-lookup"><span data-stu-id="17aa8-169">Services</span></span>

<span data-ttu-id="17aa8-170">Hello **servizi** barra laterale dashboard hello offre una visione rapida stato hello dei servizi di hello in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="17aa8-171">Icone diverse sono stato tooindicate utilizzato o azioni da intraprendere.</span><span class="sxs-lookup"><span data-stu-id="17aa8-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="17aa8-172">Ad esempio, viene visualizzato un simbolo di riciclo giallo se un servizio deve toobe riciclato.</span><span class="sxs-lookup"><span data-stu-id="17aa8-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![barra laterale dei servizi](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="17aa8-174">servizi di Hello visualizzati diversi tra versioni e i tipi di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17aa8-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="17aa8-175">servizi Hello visualizzati qui potrebbero essere diversi da servizi di hello visualizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="17aa8-176">Selezione di un servizio consente di visualizzare informazioni più dettagliate sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-176">Selecting a service displays more detailed information on hello service.</span></span>

![informazioni di riepilogo sul servizio](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="17aa8-178">Collegamenti rapidi</span><span class="sxs-lookup"><span data-stu-id="17aa8-178">Quick links</span></span>

<span data-ttu-id="17aa8-179">Alcuni servizi di visualizzare un **collegamenti rapidi** collegamento nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="17aa8-180">Può trattarsi di web specifico del servizio utilizzato tooaccess le interfacce utente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17aa8-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="17aa8-181">**Job History** : cronologia dei processi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="17aa8-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="17aa8-182">**Resource Manager** : interfaccia utente di gestione risorse di YARN.</span><span class="sxs-lookup"><span data-stu-id="17aa8-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="17aa8-183">**NameNode** : interfaccia utente NameNode del file system distribuito Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="17aa8-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="17aa8-184">**Oozie Web UI** : interfaccia utente Oozie.</span><span class="sxs-lookup"><span data-stu-id="17aa8-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="17aa8-185">Selezionare uno dei seguenti collegamenti per aprire una nuova scheda nel browser, che consente di visualizzare la pagina selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="17aa8-186">Se si seleziona hello **collegamenti rapidi** voce per un servizio può restituire un errore "server non trovato".</span><span class="sxs-lookup"><span data-stu-id="17aa8-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="17aa8-187">Se si verifica questo errore, è necessario utilizzare un tunnel SSH quando si utilizza hello **collegamenti rapidi** voce per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="17aa8-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="17aa8-188">Per informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="17aa8-189">gestione</span><span class="sxs-lookup"><span data-stu-id="17aa8-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="17aa8-190">Utenti, gruppi e autorizzazioni Ambari</span><span class="sxs-lookup"><span data-stu-id="17aa8-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="17aa8-191">L'uso di utenti, gruppi e autorizzazioni è supportato con un cluster HDInsight [aggiunto al dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="17aa8-192">Per informazioni sull'utilizzo dell'interfaccia utente Gestione Ambari hello in un cluster di dominio, vedere [la gestione dei cluster HDInsight dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="17aa8-193">Non modificare la password di hello di watchdog di hello Ambari (hdinsightwatchdog) il cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="17aa8-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="17aa8-194">La modifica di interruzioni di password hello hello azioni script toouse di capacità o eseguire le operazioni di ridimensionamento con il cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="17aa8-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="17aa8-195">Hosts</span></span>

<span data-ttu-id="17aa8-196">Hello **host** pagina vengono elencati tutti gli host cluster hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="17aa8-197">gli host toomanage, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-197">toomanage hosts, follow these steps.</span></span>

![pagina Hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="17aa8-199">Non usare le procedure per aggiungere, rimuovere o ripristinare un host con cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17aa8-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="17aa8-200">Selezionare un host di hello che si desidera toomanage.</span><span class="sxs-lookup"><span data-stu-id="17aa8-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="17aa8-201">Hello utilizzare **azioni** azione hello tooselect di menu che si desidera tooperform:</span><span class="sxs-lookup"><span data-stu-id="17aa8-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="17aa8-202">**Avviare tutti i componenti** -avviare tutti i componenti nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="17aa8-203">**Arrestare tutti i componenti** -Arresta tutti i componenti su host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="17aa8-204">**Riavviare tutti i componenti** : arrestare e avviare tutti i componenti nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="17aa8-205">**Attivare la modalità di manutenzione** -Elimina gli avvisi per host hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="17aa8-206">Questa modalità deve essere abilitata se si eseguono azioni che generano avvisi,</span><span class="sxs-lookup"><span data-stu-id="17aa8-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="17aa8-207">come l'arresto e l'avvio di un servizio.</span><span class="sxs-lookup"><span data-stu-id="17aa8-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="17aa8-208">**Disattivare la modalità di manutenzione** -restituisce hello avvisi toonormal host.</span><span class="sxs-lookup"><span data-stu-id="17aa8-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="17aa8-209">**Arrestare** -DataNode si arresta o NodeManagers nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="17aa8-210">**Avviare** -avvia DataNode o NodeManagers nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="17aa8-211">**Riavviare** -arresta e avvia DataNode o NodeManagers nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="17aa8-212">**Rimuovere le autorizzazioni** -rimuove un host dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="17aa8-213">Non usare questa azione nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17aa8-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="17aa8-214">**Recommission** -aggiunge un cluster di toohello host eliminato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="17aa8-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="17aa8-215">Non usare questa azione nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17aa8-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="17aa8-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="17aa8-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="17aa8-217">Da hello **Dashboard** o **servizi** pagina, utilizzare hello **azioni** pulsante nella parte inferiore di hello dell'elenco di hello di servizi toostop e avviare tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="17aa8-219">Mentre **Aggiungi servizio** è elencato in questo menu, non può essere cluster HDInsight toohello di tooadd utilizzati servizi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="17aa8-220">È necessario aggiungere nuovi servizi.utilizzando un'azione di Script durante il provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="17aa8-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="17aa8-221">Per altre informazioni su come utilizzare le azioni di script, vedere [Personalizzare cluster HDInsight mediante l'azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="17aa8-222">Durante la hello **azioni** pulsante possibile riavviare tutti i servizi, spesso si desidera toostart, arrestare o riavviare un servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="17aa8-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="17aa8-223">Utilizzare hello seguenti passaggi viene tooperform azioni in un singolo servizio:</span><span class="sxs-lookup"><span data-stu-id="17aa8-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="17aa8-224">Da hello **Dashboard** o **servizi** pagina, selezionare un servizio.</span><span class="sxs-lookup"><span data-stu-id="17aa8-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="17aa8-225">Dall'alto hello di hello **riepilogo** scheda, utilizzare hello **azioni servizio** pulsante e selezionare hello azione tootake.</span><span class="sxs-lookup"><span data-stu-id="17aa8-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="17aa8-226">Verrà riavviato il servizio di hello in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-226">This restarts hello service on all nodes.</span></span>

    ![azione del servizio](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="17aa8-228">Il riavvio di alcuni servizi durante l'esecuzione di cluster hello potrebbe generare avvisi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="17aa8-229">tooavoid degli avvisi, è possibile utilizzare hello **azioni servizio** pulsante tooenable **modalità manutenzione** per servizio hello prima di eseguire il riavvio di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="17aa8-230">Dopo aver selezionata un'azione, hello **op #** voce nella parte superiore di hello di hello pagina incrementi tooshow in corso un'operazione in background.</span><span class="sxs-lookup"><span data-stu-id="17aa8-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="17aa8-231">Se configurato toodisplay, viene visualizzato l'elenco di hello delle operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="17aa8-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17aa8-232">Se è stata abilitata **modalità manutenzione** per il servizio di hello, ricordare toodisable usando hello **azioni servizio** pulsante una volta completata l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="17aa8-233">tooconfigure un servizio, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="17aa8-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="17aa8-234">Da hello **Dashboard** o **servizi** pagina, selezionare un servizio.</span><span class="sxs-lookup"><span data-stu-id="17aa8-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="17aa8-235">Seleziona hello **configurazioni** configurazione corrente di hello scheda viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="17aa8-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="17aa8-236">insieme a un elenco delle configurazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="17aa8-236">A list of previous configurations is also displayed.</span></span>

    ![configurazioni](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="17aa8-238">Utilizzare la configurazione hello campi visualizzati toomodify hello e quindi selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="17aa8-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="17aa8-239">Oppure selezionare una configurazione precedente e quindi selezionare **impostare come corrente** tooroll nuovamente le impostazioni precedenti toohello.</span><span class="sxs-lookup"><span data-stu-id="17aa8-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="17aa8-240">Viste di Ambari</span><span class="sxs-lookup"><span data-stu-id="17aa8-240">Ambari views</span></span>

<span data-ttu-id="17aa8-241">Ambari viste consentono agli sviluppatori elementi dell'interfaccia utente tooplug in hello dell'interfaccia utente Web Ambari utilizzando hello [Ambari viste Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="17aa8-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="17aa8-242">HDInsight fornisce hello seguenti viste con tipi di cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="17aa8-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="17aa8-243">Gestore delle code yarn: gestore delle code hello fornisce un'interfaccia utente semplice per la visualizzazione e modifica di YARN code.</span><span class="sxs-lookup"><span data-stu-id="17aa8-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="17aa8-244">Visualizzazione di hive: hello vista Hive consente query Hive toorun direttamente dal browser web.</span><span class="sxs-lookup"><span data-stu-id="17aa8-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="17aa8-245">Si può salvare le query, visualizzare i risultati, salvare i risultati di archiviazione cluster toohello o scaricare risultati tooyour locale sistema.</span><span class="sxs-lookup"><span data-stu-id="17aa8-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="17aa8-246">Per altre informazioni sull'uso delle viste di Hive, vedere l'argomento relativo all' [uso delle viste Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="17aa8-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="17aa8-247">Tez: hello Tez visualizzazione consente di toobetter comprendere e ottimizzare i processi.</span><span class="sxs-lookup"><span data-stu-id="17aa8-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="17aa8-248">È possibile visualizzare informazioni sulle modalità di esecuzione dei processi Tez e sulle risorse usate.</span><span class="sxs-lookup"><span data-stu-id="17aa8-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
