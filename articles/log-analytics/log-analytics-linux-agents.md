---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="9aab7-101">Connettere computer Linux a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="9aab7-102">Log Analytics consente di raccogliere dati dai computer Linux e di agire in base a essi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="9aab7-103">L'aggiunta di dati raccolti da Linux a OMS consente di gestire sistemi Linux e soluzioni contenitore come Docker indipendentemente dalla posizione in cui si trovano i computer, ovvero quasi ovunque.</span><span class="sxs-lookup"><span data-stu-id="9aab7-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="9aab7-104">Le origini dati possono trovarsi nel data center locale come server fisici, in computer virtuali in un servizio ospitato sul cloud come Amazon Web Services (AWS) o Microsoft Azure o anche sul computer portatile sulla scrivania.</span><span class="sxs-lookup"><span data-stu-id="9aab7-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="9aab7-105">OMS raccoglie anche dati da computer Windows in modo analogo, quindi supporta un ambiente IT effettivamente ibrido.</span><span class="sxs-lookup"><span data-stu-id="9aab7-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="9aab7-106">È possibile visualizzare e gestire i dati da tutte queste origini dati con Log Analytics in OMS con un singolo portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="9aab7-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="9aab7-107">Ciò consente di ridurre la necessità di monitorarle usando molti sistemi diversi, ne semplifica l'utilizzo e consente di esportare qualsiasi tipo di dati in qualsiasi soluzione di analisi business o in qualsiasi sistema già disponibile.</span><span class="sxs-lookup"><span data-stu-id="9aab7-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="9aab7-108">Questo articolo è una breve guida introduttiva che illustra come raccogliere e gestire i dati per i computer Linux usando l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="9aab7-109">Maggiori informazioni tecniche, ad esempio informazioni su configurazione del server proxy, informazioni sulle metriche di CollectD e origini dati JSON personalizzati sono disponibili nella [panoramica sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) e nella [documentazione completa sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="9aab7-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="9aab7-110">È attualmente possibile raccogliere i tipi di dati seguenti da computer Linux:</span><span class="sxs-lookup"><span data-stu-id="9aab7-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="9aab7-111">Metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-111">Performance metrics</span></span>
* <span data-ttu-id="9aab7-112">Eventi SysLog</span><span class="sxs-lookup"><span data-stu-id="9aab7-112">Syslog events</span></span>
* <span data-ttu-id="9aab7-113">Avvisi da Nagios e Zabbix</span><span class="sxs-lookup"><span data-stu-id="9aab7-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="9aab7-114">Metriche delle prestazioni, inventario e log del contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="9aab7-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="9aab7-115">Versioni di Linux supportate</span><span class="sxs-lookup"><span data-stu-id="9aab7-115">Supported Linux versions</span></span>
<span data-ttu-id="9aab7-116">Le versioni x86 e x64 sono supportate ufficialmente su diverse distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="9aab7-117">È tuttavia possibile che l'agente OMS per Linux sia eseguito in altre distribuzioni non elencate.</span><span class="sxs-lookup"><span data-stu-id="9aab7-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="9aab7-118">Amazon Linux dalla 2012.09 alla 2015.09</span><span class="sxs-lookup"><span data-stu-id="9aab7-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="9aab7-119">CentOS Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="9aab7-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="9aab7-120">Oracle Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="9aab7-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="9aab7-121">Red Hat Enterprise Linux Server 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="9aab7-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="9aab7-122">Debian GNU/Linux 6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="9aab7-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="9aab7-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="9aab7-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="9aab7-124">SUSE Linux Enterprise Server 11 e 12</span><span class="sxs-lookup"><span data-stu-id="9aab7-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="9aab7-125">Agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-125">OMS Agent for Linux</span></span>
<span data-ttu-id="9aab7-126">Operations Management Suite Agent per Linux è costituito da più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="9aab7-127">Il file della versione rilasciata contiene i pacchetti seguenti, disponibili mediante l'esecuzione dell'aggregazione della shell con `--extract`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="9aab7-128">**Pacchetto**</span><span class="sxs-lookup"><span data-stu-id="9aab7-128">**Package**</span></span> | <span data-ttu-id="9aab7-129">**Versione**</span><span class="sxs-lookup"><span data-stu-id="9aab7-129">**Version**</span></span> | <span data-ttu-id="9aab7-130">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9aab7-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9aab7-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="9aab7-131">omsagent</span></span> |<span data-ttu-id="9aab7-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9aab7-132">1.1.0</span></span> |<span data-ttu-id="9aab7-133">Agente Operations Management Suite per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="9aab7-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="9aab7-134">omsconfig</span></span> |<span data-ttu-id="9aab7-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9aab7-135">1.1.1</span></span> |<span data-ttu-id="9aab7-136">Agente di configurazione per l'agente OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="9aab7-137">omi</span><span class="sxs-lookup"><span data-stu-id="9aab7-137">omi</span></span> |<span data-ttu-id="9aab7-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="9aab7-138">1.0.8.3</span></span> |<span data-ttu-id="9aab7-139">Open Management Infrastructure (OMI): server CIM leggero</span><span class="sxs-lookup"><span data-stu-id="9aab7-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="9aab7-140">scx</span><span class="sxs-lookup"><span data-stu-id="9aab7-140">scx</span></span> |<span data-ttu-id="9aab7-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="9aab7-141">1.6.2</span></span> |<span data-ttu-id="9aab7-142">Provider OMI CIM per metriche delle prestazioni del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="9aab7-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="9aab7-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="9aab7-143">apache-cimprov</span></span> |<span data-ttu-id="9aab7-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9aab7-144">1.0.0</span></span> |<span data-ttu-id="9aab7-145">Monitoraggio delle prestazioni del server HTTP Apache per OMI.</span><span class="sxs-lookup"><span data-stu-id="9aab7-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9aab7-146">Installato solo se viene rilevato il server HTTP Apache.</span><span class="sxs-lookup"><span data-stu-id="9aab7-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="9aab7-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="9aab7-147">mysql-cimprov</span></span> |<span data-ttu-id="9aab7-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9aab7-148">1.0.0</span></span> |<span data-ttu-id="9aab7-149">Monitoraggio delle prestazioni del server MySQL per OMI.</span><span class="sxs-lookup"><span data-stu-id="9aab7-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9aab7-150">Installato solo se viene rilevato il server MySQL/MariaDB.</span><span class="sxs-lookup"><span data-stu-id="9aab7-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="9aab7-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="9aab7-151">docker-cimprov</span></span> |<span data-ttu-id="9aab7-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="9aab7-152">0.1.0</span></span> |<span data-ttu-id="9aab7-153">Provider Docker per OMI.</span><span class="sxs-lookup"><span data-stu-id="9aab7-153">Docker provider for OMI.</span></span> <span data-ttu-id="9aab7-154">Installato solo se viene rilevato Docker.</span><span class="sxs-lookup"><span data-stu-id="9aab7-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="9aab7-155">Elementi di installazione aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="9aab7-155">Additional installation artifacts</span></span>
<span data-ttu-id="9aab7-156">Dopo l'installazione dei pacchetti dell'agente OMS per Linux, vengono applicate le modifiche di configurazione aggiuntive seguenti a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="9aab7-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="9aab7-157">Questi elementi vengono rimossi quando viene disinstallato il pacchetto omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="9aab7-158">Viene creato un utente senza privilegi denominato `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="9aab7-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="9aab7-159">Si tratta dell'account usato per l'esecuzione del daemon omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="9aab7-160">Viene creato un file "include" sudoers nel percorso /etc/sudoers.d/omsagent. Questo file autorizza omsagent a riavviare i daemon SysLog e omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="9aab7-161">Se le direttive "include" sudo non sono supportate nella versione di sudo installata, queste voci verranno scritte in /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="9aab7-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="9aab7-162">La configurazione di SysLog viene modificata in modo da inoltrare un sottoinsieme di eventi all'agente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="9aab7-163">Per altre informazioni, vedere la sezione **Configurazione della raccolta di dati** più avanti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="9aab7-164">Informazioni dettagliate sulla raccolta di dati Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-164">Linux data collection details</span></span>
<span data-ttu-id="9aab7-165">La tabella seguente mostra i metodi di raccolta di dati e altre informazioni dettagliate sul modo in cui vengono raccolti i dati.</span><span class="sxs-lookup"><span data-stu-id="9aab7-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="9aab7-166">una sezione source</span><span class="sxs-lookup"><span data-stu-id="9aab7-166">source</span></span> | <span data-ttu-id="9aab7-167">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="9aab7-167">Direct Agent</span></span> | <span data-ttu-id="9aab7-168">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="9aab7-168">SCOM agent</span></span> | <span data-ttu-id="9aab7-169">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9aab7-169">Azure Storage</span></span> | <span data-ttu-id="9aab7-170">SCOM obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="9aab7-170">SCOM required?</span></span> | <span data-ttu-id="9aab7-171">Dati dell'agente SCOM inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="9aab7-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="9aab7-172">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="9aab7-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9aab7-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="9aab7-173">Zabbix</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9aab7-179">1 minuto</span><span class="sxs-lookup"><span data-stu-id="9aab7-179">1 minute</span></span> |
| <span data-ttu-id="9aab7-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="9aab7-180">Nagios</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9aab7-186">All'arrivo</span><span class="sxs-lookup"><span data-stu-id="9aab7-186">on arrival</span></span> |
| <span data-ttu-id="9aab7-187">syslog</span><span class="sxs-lookup"><span data-stu-id="9aab7-187">syslog</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9aab7-193">dall'Archiviazione di Azure: 10 minuti; dall'agente: all'arrivo</span><span class="sxs-lookup"><span data-stu-id="9aab7-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="9aab7-194">Contatori delle prestazioni di Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-194">Linux performance counters</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9aab7-200">Come pianificato, almeno 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="9aab7-201">Rilevamento modifiche</span><span class="sxs-lookup"><span data-stu-id="9aab7-201">change tracking</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9aab7-207">Ogni ora</span><span class="sxs-lookup"><span data-stu-id="9aab7-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="9aab7-208">Requisiti del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9aab7-208">Package Requirements</span></span>
| <span data-ttu-id="9aab7-209">**Pacchetto obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="9aab7-209">**Required package**</span></span> | <span data-ttu-id="9aab7-210">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9aab7-210">**Description**</span></span> | <span data-ttu-id="9aab7-211">**Versione minima**</span><span class="sxs-lookup"><span data-stu-id="9aab7-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9aab7-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="9aab7-212">Glibc</span></span> |<span data-ttu-id="9aab7-213">Libreria GNU C</span><span class="sxs-lookup"><span data-stu-id="9aab7-213">GNU C library</span></span> |<span data-ttu-id="9aab7-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="9aab7-214">2.5-12</span></span> |
| <span data-ttu-id="9aab7-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="9aab7-215">Openssl</span></span> |<span data-ttu-id="9aab7-216">Librerie OpenSSL</span><span class="sxs-lookup"><span data-stu-id="9aab7-216">OpenSSL libraries</span></span> |<span data-ttu-id="9aab7-217">0.9.8e o 1.0</span><span class="sxs-lookup"><span data-stu-id="9aab7-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="9aab7-218">Curl</span><span class="sxs-lookup"><span data-stu-id="9aab7-218">Curl</span></span> |<span data-ttu-id="9aab7-219">Client Web cURL</span><span class="sxs-lookup"><span data-stu-id="9aab7-219">cURL web client</span></span> |<span data-ttu-id="9aab7-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="9aab7-220">7.15.5</span></span> |
| <span data-ttu-id="9aab7-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="9aab7-221">Python-ctypes</span></span> |<span data-ttu-id="9aab7-222">Librerie di funzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-222">function libraries</span></span> |<span data-ttu-id="9aab7-223">N/D</span><span class="sxs-lookup"><span data-stu-id="9aab7-223">n/a</span></span> |
| <span data-ttu-id="9aab7-224">PAM</span><span class="sxs-lookup"><span data-stu-id="9aab7-224">PAM</span></span> |<span data-ttu-id="9aab7-225">Moduli di autenticazione modulare</span><span class="sxs-lookup"><span data-stu-id="9aab7-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="9aab7-226">N/D</span><span class="sxs-lookup"><span data-stu-id="9aab7-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="9aab7-227">Per raccogliere i messaggi SysLog, è necessario rsyslog o syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="9aab7-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="9aab7-228">Il daemon SysLog predefinito nella versione 5 di Red Hat Enterprise Linux, CentOS e nella versione Oracle Linux (sysklog) non è supportato per la raccolta di eventi SysLog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9aab7-229">Per raccogliere i dati di SysLog da questa versione delle distribuzioni, è necessario installare e configurare il daemon rsyslog in modo da sostituire sysklog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="9aab7-230">Installazione rapida</span><span class="sxs-lookup"><span data-stu-id="9aab7-230">Quick install</span></span>
<span data-ttu-id="9aab7-231">Eseguire i comandi seguenti per scaricare omsagent, convalidare il checksum, quindi installare e caricare l'agente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="9aab7-232">I comandi sono per la versione a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9aab7-232">Commands are for 64-bit.</span></span> <span data-ttu-id="9aab7-233">I valori per l'ID area di lavoro e la chiave primaria sono disponibili in **Impostazioni** nella scheda **Origini connesse** del portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![Dettagli dell'area di lavoro](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="9aab7-235">È possibile installare e aggiornare l'agente in molti altri modi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="9aab7-236">Per altre informazioni, vedere i [Passaggi per installare l'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="9aab7-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="9aab7-237">È inoltre possibile visualizzare il [video con la procedura dettagliata di Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="9aab7-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="9aab7-238">Scegliere il metodo di raccolta di dati Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="9aab7-239">La modalità di selezione dei tipi di dati da raccogliere dipende dal fatto che si scelga di usare il portale OMS o di modificare diversi file di configurazione direttamente nei client Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="9aab7-240">Se si sceglie di usare il portale, la configurazione viene inviata automaticamente a tutti i client Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="9aab7-241">Se sono necessarie configurazioni diverse per diversi client Linux, occorrerà modificare i singoli file client oppure usare un'alternativa come PowerShell DSC, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="9aab7-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="9aab7-242">È possibile specificare gli eventi SysLog e i contatori delle prestazioni da raccogliere usando file di configurazione nei computer Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="9aab7-243">*Se si sceglie di configurare la raccolta di dati modificando i file di configurazione dell'agente, è necessario disabilitare la configurazione centralizzata.*</span><span class="sxs-lookup"><span data-stu-id="9aab7-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="9aab7-244">Di seguito sono disponibili istruzioni per la configurazione della raccolta di dati nei file di configurazione dell'agente, oltre alle istruzioni per la disabilitazione della configurazione centrale per tutti gli agenti OMS per Linux o per singoli computer.</span><span class="sxs-lookup"><span data-stu-id="9aab7-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="9aab7-245">Disabilitare la gestione OMS per un singolo computer Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="9aab7-246">La raccolta di dati centralizzata per i dati di configurazione viene disabilitata per un singolo computer Linux mediante lo script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="9aab7-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="9aab7-247">Ciò può risultare utile se un sottoinsieme di computer necessita di una configurazione specializzata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="9aab7-248">Per disabilitare la configurazione centralizzata:</span><span class="sxs-lookup"><span data-stu-id="9aab7-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="9aab7-249">Per abilitare di nuovo la configurazione centralizzata:</span><span class="sxs-lookup"><span data-stu-id="9aab7-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="9aab7-250">Contatori delle prestazioni di Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-250">Linux performance counters</span></span>
<span data-ttu-id="9aab7-251">I contatori delle prestazioni di Linux sono simili ai contatori delle prestazioni di Windows e hanno un funzionamento analogo.</span><span class="sxs-lookup"><span data-stu-id="9aab7-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="9aab7-252">È possibile usare le procedure seguenti per aggiungerli e configurarli.</span><span class="sxs-lookup"><span data-stu-id="9aab7-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="9aab7-253">Dopo l'aggiunta a OMS, i dati vengono raccolti per questi contatori ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="9aab7-254">Per aggiungere un contatore delle prestazioni di Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="9aab7-255">Per configurare gli agenti OMS per Linux usando il portale OMS, è possibile aggiungere contatori delle prestazioni di Linux nella pagina Impostazioni facendo clic su **Dati**.</span><span class="sxs-lookup"><span data-stu-id="9aab7-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="9aab7-256">Alla pagina **Impostazioni** di **Dati** fare clic su **Contatori delle prestazioni di Linux** e quindi selezionare o digitare il nome del contatore da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="9aab7-257">![dati](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="9aab7-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="9aab7-258">Se non si conosce il nome completo del contatore, è possibile iniziare a immettere un nome parziale. Verrà visualizzato un elenco di contatori disponibili.</span><span class="sxs-lookup"><span data-stu-id="9aab7-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="9aab7-259">Quando si trova il contatore da aggiungere, fare clic sul nome nell'elenco, quindi fare clic sull'icona del segno più per aggiungere il contatore.</span><span class="sxs-lookup"><span data-stu-id="9aab7-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="9aab7-260">Dopo l'aggiunta, il contatore viene visualizzato nell'elenco di contatori, evidenziato con una barra colorata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="9aab7-261">Per impostazione predefinita, l'opzione **Applica la configurazione seguente alle macchine virtuali** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="9aab7-262">Se si vuole disabilitare l'invio dei dati di configurazione, deselezionare l'opzione.</span><span class="sxs-lookup"><span data-stu-id="9aab7-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="9aab7-263">Al termine della modifica dei contatori delle prestazioni, nella parte inferiore della pagina fare clic su **Salva** per finalizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9aab7-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="9aab7-264">Le modifiche apportate alla configurazione vengono inviate a tutti gli agenti OMS per Linux registrati con OMS, in genere entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="9aab7-265">Configurare i contatori delle prestazioni di Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="9aab7-266">Per i contatori delle prestazioni di Windows è possibile scegliere un'istanza specifica per ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="9aab7-267">Per i contatori delle prestazioni di Linux, tuttavia, qualsiasi istanza di un contatore scelta viene applicata a tutti i contatori figlio del contatore padre.</span><span class="sxs-lookup"><span data-stu-id="9aab7-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="9aab7-268">La tabella seguente illustra le istanze comuni disponibili ai contatori delle prestazioni di Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="9aab7-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="9aab7-269">**Nome dell'istanza**</span><span class="sxs-lookup"><span data-stu-id="9aab7-269">**Instance name**</span></span> | <span data-ttu-id="9aab7-270">**Significato**</span><span class="sxs-lookup"><span data-stu-id="9aab7-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9aab7-271">\_Totale</span><span class="sxs-lookup"><span data-stu-id="9aab7-271">\_Total</span></span> |<span data-ttu-id="9aab7-272">Totale di tutte le istanze</span><span class="sxs-lookup"><span data-stu-id="9aab7-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="9aab7-273">Tutte le istanze</span><span class="sxs-lookup"><span data-stu-id="9aab7-273">All instances</span></span> |
| <span data-ttu-id="9aab7-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="9aab7-274">(/&#124;/var)</span></span> |<span data-ttu-id="9aab7-275">Corrisponde alle istanze denominate / oppure /var</span><span class="sxs-lookup"><span data-stu-id="9aab7-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="9aab7-276">Analogamente, l'intervallo di campionamento scelto per un contatore padre viene applicato a tutti i rispettivi contatori figlio.</span><span class="sxs-lookup"><span data-stu-id="9aab7-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="9aab7-277">In altri termini, gli intervalli di campionamento e le istanze di tutti i contatori figlio sono collegati tra loro.</span><span class="sxs-lookup"><span data-stu-id="9aab7-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="9aab7-278">Aggiungere e configurare le metriche delle prestazioni con Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="9aab7-279">Le metriche delle prestazioni sono controllate dalla configurazione in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="9aab7-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="9aab7-280">Per informazioni sulle classi e sulle metriche disponibili per l'agente OMS per Linux, vedere la pagina relativa alle [Metriche delle prestazioni disponibili](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) .</span><span class="sxs-lookup"><span data-stu-id="9aab7-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="9aab7-281">Ogni oggetto o categoria delle metriche delle prestazioni da raccogliere deve essere definito nel file di configurazione come singolo elemento `<source>` .</span><span class="sxs-lookup"><span data-stu-id="9aab7-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="9aab7-282">La sintassi segue il modello seguente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="9aab7-283">Ecco i parametri configurabili di questo elemento:</span><span class="sxs-lookup"><span data-stu-id="9aab7-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="9aab7-284">**Object\_name**: il nome dell'oggetto per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="9aab7-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="9aab7-285">**Instance\_regex**: un'*espressione regolare* che definisce le istanze da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="9aab7-286">Il valore `.*` specifica tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="9aab7-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="9aab7-287">Per raccogliere le metriche del processore solo per l'istanza \_Total, è possibile specificare `_Total`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="9aab7-288">Per raccogliere le metriche del processore solo per le istanze crond o sshd, è possibile specificare `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="9aab7-289">**Counter\_name\_regex**: un'*espressione regolare* che definisce i contatori per l'oggetto da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="9aab7-290">Per raccogliere tutti i contatori per l'oggetto, specificare `.*`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="9aab7-291">Per raccogliere solo i contatori dello spazio di swapping per l'oggetto Memory, è possibile specificare `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="9aab7-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="9aab7-292">**Interval:**: frequenza con cui vengono raccolti i contatori dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9aab7-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="9aab7-293">Ecco la configurazione predefinita per le metriche delle prestazioni:</span><span class="sxs-lookup"><span data-stu-id="9aab7-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="9aab7-294">Abilitare i contatori delle prestazioni di MySQL usando comandi di Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="9aab7-295">Se viene rilevato un server MySQL o MariaDB nel computer in cui è installata l'aggregazione omsagent, viene installato automaticamente un provider di monitoraggio delle prestazioni per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="9aab7-296">Questo provider si connette al server MySQL/MariaDB locale per esporre le statistiche relative alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="9aab7-297">È necessario configurare le credenziali dell'utente di MySQL, in modo che il provider possa accedere al server MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="9aab7-298">Per definire un account utente predefinito per il server MySQL su localhost, usare il comando di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="9aab7-299">Il file delle credenziali deve essere leggibile dall'account omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="9aab7-300">È consigliabile eseguire il comando mycimprovauth come omsgent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="9aab7-301">In alternativa, è possibile specificare le credenziali di MySQL necessarie in un file, creando il file /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="9aab7-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="9aab7-302">Per altre informazioni sulla gestione delle credenziali di MySQL per il monitoraggio mediante il file mysql-auth, vedere [Gestire le credenziali per il monitoraggio di MySQL nel file di autenticazione](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="9aab7-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="9aab7-303">Per informazioni dettagliate sulle autorizzazioni oggetto richieste dall'utente di MySQL per raccogliere i dati sulle prestazioni del server MySQL, vedere [Autorizzazioni del database necessarie per i contatori delle prestazioni di MySQL](#database-permissions-required-for-mysql-performance-counters) .</span><span class="sxs-lookup"><span data-stu-id="9aab7-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="9aab7-304">Abilitare i contatori delle prestazioni del server HTTP Apache usando comandi di Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="9aab7-305">Se viene rilevato un server HTTP Apache nel computer in cui è installata l'aggregazione omsagent, viene installato automaticamente un provider di monitoraggio delle prestazioni per il server HTTP Apache.</span><span class="sxs-lookup"><span data-stu-id="9aab7-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="9aab7-306">Questo provider si basa su un "modulo" Apache che deve essere caricato nel server HTTP Apache in modo da accedere ai dati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="9aab7-307">È possibile caricare il modulo con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="9aab7-308">Per scaricare il modulo di monitoraggio Apache, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="9aab7-309">Per visualizzare i dati sulle prestazioni con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="9aab7-310">Nel portale di Operations Management Suite fare clic sul riquadro Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="9aab7-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="9aab7-311">Nella barra di ricerca digitare `* (Type=Perf)` per visualizzare tutti i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="9aab7-312">Poiché OMS raccoglie anche i dati dei contatori delle prestazioni di Windows, è necessario limitare l'ambito della ricerca a dati specifici di Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="9aab7-313">L'esempio seguente consente quindi di visualizzare i dati sulle prestazioni specifici per un server Linux di esempio denominato Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="9aab7-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![Server di esempio visualizzato nei risultati della ricerca](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="9aab7-315">Nei risultati è possibile fare clic su **Metriche** per visualizzare i contatori per cui sono stati raccolti i dati.</span><span class="sxs-lookup"><span data-stu-id="9aab7-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="9aab7-316">I dati in tempo reale vengono mostrati come grafici per ogni contatore.</span><span class="sxs-lookup"><span data-stu-id="9aab7-316">Real-time data is shown as graphs for each counter.</span></span>

![Metriche](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="9aab7-318">syslog</span><span class="sxs-lookup"><span data-stu-id="9aab7-318">Syslog</span></span>
<span data-ttu-id="9aab7-319">SysLog è un protocollo di registrazione di eventi analogo ai registri eventi di Windows. Il funzionamento di entrambi è simile in caso di visualizzazione in OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="9aab7-320">Per aggiungere una nuova funzionalità SysLog per Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="9aab7-321">Alla pagina **Impostazioni** di **Dati** fare clic su **Syslog** e quindi, a sinistra dell'icona con il segno più, digitare il nome della funzionalità Syslog da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="9aab7-322">![Syslog per Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="9aab7-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="9aab7-323">Se non si conosce il nome completo della funzionalità, è possibile iniziare a immettere un nome parziale. Verrà visualizzato un elenco di funzionalità SysLog disponibili.</span><span class="sxs-lookup"><span data-stu-id="9aab7-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="9aab7-324">Quando si trova la funzionalità SysLog da aggiungere, fare clic sul nome nell'elenco, quindi fare clic sull'icona del segno più per aggiungere la funzionalità SysLog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="9aab7-325">Dopo l'aggiunta, la funzionalità viene visualizzata nell'elenco, evidenziata con una barra colorata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="9aab7-326">Scegliere quindi il livello di gravità, ovvero le categorie di informazioni sulle funzionalità SysLog, da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="9aab7-327">Nella parte inferiore della pagina fare clic su **Salva** per finalizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9aab7-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="9aab7-328">Le modifiche apportate alla configurazione vengono inviate a tutti gli agenti OMS per Linux registrati con OMS, in genere entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="9aab7-329">Configurare le funzionalità SysLog per Linux in Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="9aab7-330">Gli eventi SysLog vengono inviati dal daemon SysLog, ad esempio rsyslog o syslog-ng, a una porta locale su cui è in ascolto l'agente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="9aab7-331">Per impostazione predefinita, si tratta della porta 25224.</span><span class="sxs-lookup"><span data-stu-id="9aab7-331">By default, port 25224.</span></span> <span data-ttu-id="9aab7-332">Quando l'agente viene installato, viene applicata una configurazione di SysLog predefinita,</span><span class="sxs-lookup"><span data-stu-id="9aab7-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="9aab7-333">disponibile in:</span><span class="sxs-lookup"><span data-stu-id="9aab7-333">This is found at:</span></span>

<span data-ttu-id="9aab7-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="9aab7-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="9aab7-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="9aab7-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="9aab7-336">La configurazione di SysLog per l'agente OMS carica eventi SysLog da tutte le funzionalità con gravità pari a un avviso o superiore.</span><span class="sxs-lookup"><span data-stu-id="9aab7-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="9aab7-337">Se si modifica la configurazione di SysLog, è necessario riavviare il daemon SysLog per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9aab7-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="9aab7-338">Ecco la configurazione predefinita di SysLog per l'agente OMS per Linux per OMS:</span><span class="sxs-lookup"><span data-stu-id="9aab7-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="9aab7-339">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="9aab7-339">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="9aab7-340">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="9aab7-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="9aab7-341">Per visualizzare tutti gli eventi SysLog con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="9aab7-342">Nel portale di Operations Management Suite fare clic sul riquadro **Ricerca log** .</span><span class="sxs-lookup"><span data-stu-id="9aab7-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9aab7-343">Nel gruppo **Gestione log** scegliere una ricerca SysLog predefinita e quindi selezionare un'opzione per eseguirla.</span><span class="sxs-lookup"><span data-stu-id="9aab7-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="9aab7-344">Questo esempio mostra tutti gli eventi SysLog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-344">This example shows all Syslog events.</span></span>

![Eventi SysLog visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="9aab7-346">È ora possibile esaminare i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="9aab7-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="9aab7-347">Avvisi di Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-347">Linux alerts</span></span>
<span data-ttu-id="9aab7-348">Se si usa Nagios o Zabbix per gestire i computer Linux, OMS può ricevere gli avvisi generati da questi strumenti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="9aab7-349">Non è tuttavia disponibile attualmente alcun metodo per configurare i dati sugli avvisi in ingresso usando il portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="9aab7-350">Sarà invece necessario modificare un file di configurazione per iniziare a inviare avvisi a OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="9aab7-351">Raccogliere avvisi da Nagios</span><span class="sxs-lookup"><span data-stu-id="9aab7-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="9aab7-352">Per raccogliere avvisi da un server Nagios, è necessario apportare le modifiche seguenti alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="9aab7-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="9aab7-353">Concedere all'utente **omsagent** l'accesso in lettura al file di log Nagios, ad esempio /var/log/nagios/nagios.log.</span><span class="sxs-lookup"><span data-stu-id="9aab7-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="9aab7-354">Supponendo che il file nagios.log sia di proprietà del gruppo **nagios**, è possibile aggiungere l'utente **omsagent** al gruppo **nagios**.</span><span class="sxs-lookup"><span data-stu-id="9aab7-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="9aab7-355">Modificare il file omsagent.confconfiguration (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="9aab7-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="9aab7-356">Assicurarsi che le voci seguenti siano presenti e non impostate come commento:</span><span class="sxs-lookup"><span data-stu-id="9aab7-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="9aab7-357">Riavviare il daemon omsagent:</span><span class="sxs-lookup"><span data-stu-id="9aab7-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="9aab7-358">Raccogliere avvisi da Zabbix</span><span class="sxs-lookup"><span data-stu-id="9aab7-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="9aab7-359">Per raccogliere avvisi da un server Zabbix, sarà necessario eseguire una procedura analoga a quella precedente per Nagios, ma occorrerà specificare un utente e una password in *testo non crittografato*.</span><span class="sxs-lookup"><span data-stu-id="9aab7-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="9aab7-360">Questo approccio non è ideale, ma verrà probabilmente modificato a breve.</span><span class="sxs-lookup"><span data-stu-id="9aab7-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="9aab7-361">Per risolvere questo problema, è consigliabile creare l'utente e assegnare all'utente solo le autorizzazioni per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="9aab7-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="9aab7-362">Una sezione di esempio del file di configurazione omsagent.conf (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) per Zabbix dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="9aab7-363">Visualizzare avvisi nella ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="9aab7-364">Dopo avere configurato i computer Linux per l'invio di avvisi a OMS, è possibile usare alcune semplici query di ricerca nel log per visualizzare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="9aab7-365">L'esempio di query di ricerca seguente restituisce tutti gli avvisi registrati che sono stati generati.</span><span class="sxs-lookup"><span data-stu-id="9aab7-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="9aab7-366">Ad esempio, se si verifica qualche problema nell'infrastruttura IT, i risultati per l'esempio di query seguente potrebbero indicare l'origine del problema.</span><span class="sxs-lookup"><span data-stu-id="9aab7-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="9aab7-367">Sarà anche possibile esaminare nel dettaglio gli avvisi in base al sistema di origine, per perfezionare la ricerca.</span><span class="sxs-lookup"><span data-stu-id="9aab7-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="9aab7-368">Non sarà quindi necessario passare a diversi sistemi di gestione fin dall'inizio. Se gli avvisi vengono inviati a OMS, sarà possibile iniziare da tale sistema.</span><span class="sxs-lookup"><span data-stu-id="9aab7-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="9aab7-369">Per visualizzare tutti gli avvisi di Nagios con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="9aab7-370">Nel portale di Operations Management Suite fare clic sul riquadro **Ricerca log** .</span><span class="sxs-lookup"><span data-stu-id="9aab7-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9aab7-371">Nella barra per le query immettere la query di ricerca seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Avvisi Nagios visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="9aab7-373">Dopo avere visualizzato i risultati della ricerca, è possibile analizzare altri dettagli, ad esempio *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="9aab7-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="9aab7-374">Per visualizzare tutti gli avvisi di Zabbix con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9aab7-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="9aab7-375">Nel portale di Operations Management Suite fare clic sul riquadro **Ricerca log** .</span><span class="sxs-lookup"><span data-stu-id="9aab7-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9aab7-376">Nella barra per le query immettere la query di ricerca seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Avvisi Zabbix visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="9aab7-378">Dopo avere visualizzato i risultati della ricerca, è possibile analizzare altri dettagli, ad esempio *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="9aab7-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="9aab7-379">Compatibilità con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9aab7-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="9aab7-380">L'agente OMS per Linux condivide file binari dell'agente con l'agente System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="9aab7-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="9aab7-381">Se si installa l'agente OMS per Linux in un sistema attualmente gestito da Operations Manager, i pacchetti OMI e SCX nel computer vengono aggiornati a una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="9aab7-382">L'agente OMS per Linux e System Center 2012 R2 sono compatibili,</span><span class="sxs-lookup"><span data-stu-id="9aab7-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="9aab7-383">ma **System Center 2012 SP1 e le versioni precedenti non sono attualmente compatibili o supportati con l'agente OMS per Linux.**</span><span class="sxs-lookup"><span data-stu-id="9aab7-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="9aab7-384">Se l'agente OMS per Linux viene installato in un computer attualmente non gestito da Operations Manager e successivamente si vuole gestire il computer con Operations Manager, è necessario modificare la configurazione OMI prima di individuare il computer.</span><span class="sxs-lookup"><span data-stu-id="9aab7-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="9aab7-385">**Questo passaggio non è necessario se l'agente Operations Manager viene installato prima dell'agente OMS per Linux.**</span><span class="sxs-lookup"><span data-stu-id="9aab7-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="9aab7-386">Per consentire all'agente OMS per Linux di comunicare con Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9aab7-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="9aab7-387">Modificare il file /etc/opt/omi/conf/omiserver.conf.</span><span class="sxs-lookup"><span data-stu-id="9aab7-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="9aab7-388">Assicurarsi che la riga che inizia con **httpsport=** definisca la porta 1270,</span><span class="sxs-lookup"><span data-stu-id="9aab7-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="9aab7-389">ad esempio `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="9aab7-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="9aab7-390">Riavviare il server OMI:</span><span class="sxs-lookup"><span data-stu-id="9aab7-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="9aab7-391">Autorizzazioni del database necessarie per i contatori delle prestazioni di MySQL</span><span class="sxs-lookup"><span data-stu-id="9aab7-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="9aab7-392">Per concedere autorizzazioni a un utente di monitoraggio di MySQL, l'utente che le concede deve avere il privilegio 'GRANT option', oltre al privilegio da concedere.</span><span class="sxs-lookup"><span data-stu-id="9aab7-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="9aab7-393">Perché l'utente di MySQL possa restituire i dati sulle prestazioni, è necessario che l'utente possa accedere alle query seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="9aab7-394">Oltre a queste query, l'utente di MySQL deve avere accesso di tipo SELECT alle tabelle predefinite seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="9aab7-395">information_schema</span><span class="sxs-lookup"><span data-stu-id="9aab7-395">information_schema</span></span>
* <span data-ttu-id="9aab7-396">mysql</span><span class="sxs-lookup"><span data-stu-id="9aab7-396">mysql</span></span>

<span data-ttu-id="9aab7-397">Questi privilegi possono essere concessi mediante l'esecuzione dei comandi grant seguenti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="9aab7-398">Gestire le credenziali per il monitoraggio di MySQL nel file di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9aab7-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="9aab7-399">Le sezioni seguenti illustrano come gestire le credenziali di MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="9aab7-400">Configurare il provider OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="9aab7-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="9aab7-401">Il provider OMI MySQL richiede un utente di MySQL preconfigurato e librerie client MySQL installate, in modo da eseguire query sulle prestazioni/informazioni sull'integrità dall'istanza di MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="9aab7-402">File di autenticazione OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="9aab7-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="9aab7-403">Il provider OMI MySQL usa un file di autenticazione per determinare il valore bind-address e la porta su cui è in ascolto l'istanza di MySQL e infine le credenziali da usare per raccogliere metriche.</span><span class="sxs-lookup"><span data-stu-id="9aab7-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="9aab7-404">Durante l'installazione, il provider OMI MySQL analizzerà i file di configurazione my.cnf di MySQL (percorsi predefiniti) alla ricerca del valore bind-address e della porta e imposterà in modo parziale il file di configurazione OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="9aab7-405">Per completare il monitoraggio di un'istanza del server MySQL, aggiungere un file di autenticazione OMI MySQL pregenerato alla directory corretta.</span><span class="sxs-lookup"><span data-stu-id="9aab7-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="9aab7-406">Formato del file di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9aab7-406">Authentication file format</span></span>
<span data-ttu-id="9aab7-407">Il file di autenticazione OMI MySQL è un file di testo che contiene informazioni sugli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="9aab7-408">Port</span><span class="sxs-lookup"><span data-stu-id="9aab7-408">Port</span></span>
* <span data-ttu-id="9aab7-409">Bind-address</span><span class="sxs-lookup"><span data-stu-id="9aab7-409">Bind-Address</span></span>
* <span data-ttu-id="9aab7-410">Nome utente MySQL</span><span class="sxs-lookup"><span data-stu-id="9aab7-410">MySQL username</span></span>
* <span data-ttu-id="9aab7-411">Password con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="9aab7-411">Base64 encoded password</span></span>

<span data-ttu-id="9aab7-412">Il file di autenticazione OMI MySQL concede privilegi solo per la lettura/scrittura per l'utente Linux che lo ha generato.</span><span class="sxs-lookup"><span data-stu-id="9aab7-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="9aab7-413">Un file di autenticazione OMI MySQL predefinito contiene un'istanza predefinita e un numero di porta, in base alle informazioni disponibili e analizzate nel file di configurazione MySQL trovato.</span><span class="sxs-lookup"><span data-stu-id="9aab7-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="9aab7-414">L'istanza predefinita semplifica la gestione di più istanze di MySQL in un host Linux e viene indicata dall'istanza con porta 0.</span><span class="sxs-lookup"><span data-stu-id="9aab7-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="9aab7-415">Tutte le istanze aggiunte erediteranno le proprietà impostate dall'istanza predefinita.</span><span class="sxs-lookup"><span data-stu-id="9aab7-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="9aab7-416">Ad esempio, se viene aggiunta l'istanza di MySQL in ascolto sulla porta "3308", il valore bind-address, il nome utente e la password con codifica Base64 dell'istanza predefinita verranno usati per provare a monitorare l'istanza in ascolto sulla porta 3308.</span><span class="sxs-lookup"><span data-stu-id="9aab7-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="9aab7-417">Se l'istanza sulla porta 3308 è associata a un altro indirizzo e usa la stessa coppia nome utente e password di MySQL, sarà necessario specificare di nuovo solo il valore bind-address e le altre proprietà verranno ereditate.</span><span class="sxs-lookup"><span data-stu-id="9aab7-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="9aab7-418">Gli esempi del file di autenticazione hanno un aspetto analogo ai seguenti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="9aab7-419">Istanza predefinita e istanza con porta 3308:</span><span class="sxs-lookup"><span data-stu-id="9aab7-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="9aab7-420">Istanza predefinita e istanza con porta 3308 e password con codifica Base 64 diversa:</span><span class="sxs-lookup"><span data-stu-id="9aab7-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="9aab7-421">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="9aab7-421">**Property**</span></span> | <span data-ttu-id="9aab7-422">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9aab7-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9aab7-423">Port</span><span class="sxs-lookup"><span data-stu-id="9aab7-423">Port</span></span> |<span data-ttu-id="9aab7-424">Port rappresenta la porta corrente su cui è in ascolto l'istanza di MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="9aab7-425">La porta 0 indica che le proprietà seguenti vengono usate per l'istanza predefinita.</span><span class="sxs-lookup"><span data-stu-id="9aab7-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="9aab7-426">Bind-address</span><span class="sxs-lookup"><span data-stu-id="9aab7-426">Bind-Address</span></span> |<span data-ttu-id="9aab7-427">Bind-address corrisponde al valore bind-address corrente di MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="9aab7-428">username</span><span class="sxs-lookup"><span data-stu-id="9aab7-428">username</span></span> |<span data-ttu-id="9aab7-429">Nome utente dell'utente di MySQL da usare per monitorare l'istanza del server MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="9aab7-430">Password con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="9aab7-430">Base64 encoded Password</span></span> |<span data-ttu-id="9aab7-431">Password dell'utente di monitoraggio di MySQL con codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="9aab7-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="9aab7-432">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="9aab7-432">AutoUpdate</span></span> |<span data-ttu-id="9aab7-433">Quando il provider OMI MySQL viene aggiornato, ripeterà l'analisi alla ricerca di modifiche nel file my.cnf e sovrascriverà il file di autenticazione OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="9aab7-434">Impostare questo flag su true o false, in base agli aggiornamenti necessari per il file di autenticazione OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="9aab7-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="9aab7-435">Percorso del file di autenticazione</span><span class="sxs-lookup"><span data-stu-id="9aab7-435">Authentication file location</span></span>
<span data-ttu-id="9aab7-436">Il file di autenticazione OMI MySQL deve trovarsi nel percorso seguente e deve essere denominato "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="9aab7-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="9aab7-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="9aab7-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="9aab7-438">Il file e la directory auth/omsagent devono essere di proprietà dell'utente omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="9aab7-439">Log dell'agente</span><span class="sxs-lookup"><span data-stu-id="9aab7-439">Agent logs</span></span>
<span data-ttu-id="9aab7-440">I log per l'agente OMS per Linux sono disponibili nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="9aab7-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="9aab7-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="9aab7-442">I log per l'agente OMS per Linux per il programma omsconfig (configurazione dell'agente) sono disponibili nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="9aab7-443">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="9aab7-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="9aab7-444">I log per i componenti OMI e SCX, che forniscono i dati sulle metriche sulle prestazioni, sono disponibili nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="9aab7-445">/var/opt/omi/log/ e /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="9aab7-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="9aab7-446">Risoluzione dei problemi dell'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="9aab7-447">Usare le seguenti informazioni per diagnosticare e risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="9aab7-448">Se nessuna delle informazioni sulla risoluzione dei problemi presenti in questa sezione è utile, è possibile usare anche le risorse seguenti per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="9aab7-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="9aab7-449">I clienti con supporto tecnico Premier possono registrare un caso di supporto tramite [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="9aab7-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="9aab7-450">I clienti con contratti di supporto tecnico di Azure possono registrare casi di supporto nel [portale di Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="9aab7-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="9aab7-451">Presentare un [problema GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="9aab7-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="9aab7-452">Per trovare idee e creare un report dei bug, consultare il forum di commenti e suggerimenti [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="9aab7-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="9aab7-453">Percorsi log importanti</span><span class="sxs-lookup"><span data-stu-id="9aab7-453">Important log locations</span></span>
| <span data-ttu-id="9aab7-454">File</span><span class="sxs-lookup"><span data-stu-id="9aab7-454">File</span></span> | <span data-ttu-id="9aab7-455">Path</span><span class="sxs-lookup"><span data-stu-id="9aab7-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="9aab7-456">File di log dell'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="9aab7-457">File di log di configurazione dell'agente OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="9aab7-458">File di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="9aab7-458">Important configuration files</span></span>
| <span data-ttu-id="9aab7-459">Categoria</span><span class="sxs-lookup"><span data-stu-id="9aab7-459">Catergory</span></span> | <span data-ttu-id="9aab7-460">Percorso file</span><span class="sxs-lookup"><span data-stu-id="9aab7-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="9aab7-461">syslog</span><span class="sxs-lookup"><span data-stu-id="9aab7-461">Syslog</span></span> |<span data-ttu-id="9aab7-462">`/etc/syslog-ng/syslog-ng.conf` o `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="9aab7-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="9aab7-463">Output e agente generale Performance, Nagios, Zabbix e OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="9aab7-464">Configurazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9aab7-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="9aab7-465">La modifica dei file di configurazione per i contatori delle prestazioni e Syslog vengono sovrascritti se è abilitata la configurazione del portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="9aab7-466">È possibile disabilitare la configurazione nel portale di OMS (per tutti i nodi) o per i singoli nodi eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="9aab7-467">Abilitazione della registrazione di debug</span><span class="sxs-lookup"><span data-stu-id="9aab7-467">Enable debug logging</span></span>
<span data-ttu-id="9aab7-468">Per abilitare la registrazione di debug, è possibile usare il plug-in di output di OMS e l'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="9aab7-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="9aab7-469">Plug-in di output di OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-469">OMS output plugin</span></span>
<span data-ttu-id="9aab7-470">FluentD consente al plug-in di specificare i livelli di registrazione per diversi livelli di log per input e output.</span><span class="sxs-lookup"><span data-stu-id="9aab7-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="9aab7-471">Per specificare un livello di log diverso per l'output di OMS, modificare la configurazione dell'agente generale nel file `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="9aab7-472">Nella parte inferiore del file di configurazione, modificare la proprietà `log_level` da `info` a `debug`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="9aab7-473">La registrazione di debug consente di visualizzare i caricamenti in batch nel servizio OMS separati in base a tipo, numero di elementi di dati e tempo impiegato per l'invio.</span><span class="sxs-lookup"><span data-stu-id="9aab7-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="9aab7-474">*Esempio di log abilitato per il debug:*</span><span class="sxs-lookup"><span data-stu-id="9aab7-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="9aab7-475">Output dettagliato</span><span class="sxs-lookup"><span data-stu-id="9aab7-475">Verbose output</span></span>
<span data-ttu-id="9aab7-476">Anziché usare il plug-in output di OMS, è anche possibile inviare elementi di dati direttamente a `stdout`, che è visibile nel file di log dell'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="9aab7-477">Nel file di configurazione dell'agente generale OMS in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, impostare come commento il plug-in di output di OMS aggiungendo `#` davanti a ogni riga.</span><span class="sxs-lookup"><span data-stu-id="9aab7-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="9aab7-478">Sotto l'output di plug-in, rimuovere il commento nella sezione seguente eliminando il simbolo `#` all'inizio di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="9aab7-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="9aab7-479">I messaggi Syslog inoltrati non vengono visualizzati nel log</span><span class="sxs-lookup"><span data-stu-id="9aab7-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-480">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-480">Probable causes</span></span>
* <span data-ttu-id="9aab7-481">La configurazione applicata al server Linux non consente la raccolta delle strutture e/o dei livelli di log inviati</span><span class="sxs-lookup"><span data-stu-id="9aab7-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="9aab7-482">Syslog non viene inoltrato correttamente al server Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="9aab7-483">Il numero di messaggi inoltrati al secondo è troppo elevato, di conseguenza la configurazione di base dell'agente OMS per Linux non può gestirli</span><span class="sxs-lookup"><span data-stu-id="9aab7-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-484">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-484">Resolutions</span></span>
* <span data-ttu-id="9aab7-485">Verificare che la configurazione nel portale OMS per Syslog disponga di tutte le strutture e dei livelli di log corretti</span><span class="sxs-lookup"><span data-stu-id="9aab7-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="9aab7-486">**Portale OMS > Impostazioni > Dati > Syslog**</span><span class="sxs-lookup"><span data-stu-id="9aab7-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="9aab7-487">Verificare che i daemon di messaggistica Syslog nativi (`rsyslog`, `syslog-ng`) siano in grado di ricevere i messaggi inoltrati</span><span class="sxs-lookup"><span data-stu-id="9aab7-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="9aab7-488">Controllare le impostazioni del firewall sul server Syslog per verificare che i messaggi non vengano bloccati</span><span class="sxs-lookup"><span data-stu-id="9aab7-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="9aab7-489">Simulare un messaggio Syslog per OMS usando il comando `logger`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9aab7-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="9aab7-490">Problemi di connessione a OMS quando si usa un proxy</span><span class="sxs-lookup"><span data-stu-id="9aab7-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-491">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-491">Probable causes</span></span>
* <span data-ttu-id="9aab7-492">Il proxy specificato durante l'installazione e la configurazione dell'agente non è corretto</span><span class="sxs-lookup"><span data-stu-id="9aab7-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="9aab7-493">Gli endpoint del servizio OMS non sono presenti nell'elenco elementi consentiti del data center</span><span class="sxs-lookup"><span data-stu-id="9aab7-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-494">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-494">Resolutions</span></span>
* <span data-ttu-id="9aab7-495">Reinstallare l'agente OMS per Linux usando il comando seguente con l'opzione `-v` abilitata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="9aab7-496">In questo modo l'output dettagliato dell'agente si connette tramite proxy al servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="9aab7-497">Consultare la documentazione relativa al proxy OMS in [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server) (Configurazione dell'agente per l'uso con un server proxy HTTP)</span><span class="sxs-lookup"><span data-stu-id="9aab7-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="9aab7-498">Verificare che i seguenti endpoint del servizio OMS siano inclusi nell'elenco elementi consentiti</span><span class="sxs-lookup"><span data-stu-id="9aab7-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="9aab7-499">Risorsa agente</span><span class="sxs-lookup"><span data-stu-id="9aab7-499">Agent Resource</span></span> | <span data-ttu-id="9aab7-500">Porte</span><span class="sxs-lookup"><span data-stu-id="9aab7-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="9aab7-501">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9aab7-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="9aab7-502">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9aab7-502">Port 443</span></span> |
| <span data-ttu-id="9aab7-503">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9aab7-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="9aab7-504">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9aab7-504">Port 443</span></span> |
| <span data-ttu-id="9aab7-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="9aab7-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="9aab7-506">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9aab7-506">Port 443</span></span> |
| <span data-ttu-id="9aab7-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9aab7-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="9aab7-508">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9aab7-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="9aab7-509">Viene visualizzato un messaggio di errore 403 durante il caricamento</span><span class="sxs-lookup"><span data-stu-id="9aab7-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-510">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-510">Probable causes</span></span>
* <span data-ttu-id="9aab7-511">Data e ora non sono corrette nel server Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="9aab7-512">L'ID e la chiave dell'area di lavoro usati non sono corretti</span><span class="sxs-lookup"><span data-stu-id="9aab7-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="9aab7-513">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="9aab7-513">Resolution</span></span>
* <span data-ttu-id="9aab7-514">Verificare l'ora sul server Linux con il comando `date`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="9aab7-515">Se nei dati si verifica una differenza di 15 minuti per eccesso o per difetto rispetto all'ora corrente, il caricamento ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9aab7-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="9aab7-516">Per risolvere il problema, aggiornare la data e/o il fuso orario del server Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="9aab7-517">La versione più recente dell'agente OMS per Linux informa se una differenza di orario provoca un errore di caricamento</span><span class="sxs-lookup"><span data-stu-id="9aab7-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="9aab7-518">Ripetere il caricamento usando l'ID e la chiave dell'area di lavoro corretti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="9aab7-519">Per maggiori informazioni, vedere [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Caricamento usando la riga di comando).</span><span class="sxs-lookup"><span data-stu-id="9aab7-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="9aab7-520">Nel file di log viene visualizzato un errore 500 o 404 dopo il caricamento</span><span class="sxs-lookup"><span data-stu-id="9aab7-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="9aab7-521">Si tratta di un problema noto che si verifica durante il primo caricamento dei dati di Linux in un'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="9aab7-522">Questo non influisce sui dati inviati o su altri problemi.</span><span class="sxs-lookup"><span data-stu-id="9aab7-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="9aab7-523">È possibile ignorare gli errori durante il caricamento iniziale.</span><span class="sxs-lookup"><span data-stu-id="9aab7-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="9aab7-524">I dati di Nagios non vengono visualizzati nel portale di OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-525">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-525">Probable causes</span></span>
* <span data-ttu-id="9aab7-526">L'utente omsagent non dispone delle autorizzazioni per leggere dai file di log di Nagios</span><span class="sxs-lookup"><span data-stu-id="9aab7-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="9aab7-527">Le sezioni di origine e filtro di Nagios continuano a essere commentate nel file omsagent.conf</span><span class="sxs-lookup"><span data-stu-id="9aab7-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-528">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-528">Resolutions</span></span>
* <span data-ttu-id="9aab7-529">Per leggere dal file di Nagios, aggiungere l'utente omsagent.</span><span class="sxs-lookup"><span data-stu-id="9aab7-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="9aab7-530">Per maggiori informazioni, vedere [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Avvisi di Nagios).</span><span class="sxs-lookup"><span data-stu-id="9aab7-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="9aab7-531">Nel file di configurazione generale dell'agente OMS per Linux in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` assicurarsi che **entrambe** le sezioni (di origine e filtro) di Nagios contengano i commenti rimossi, in modo analogo all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="9aab7-532">I dati di Linux non vengono visualizzati nel portale di OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-533">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-533">Probable causes</span></span>
* <span data-ttu-id="9aab7-534">Il caricamento nel servizio OMS ha avuto esito negativo</span><span class="sxs-lookup"><span data-stu-id="9aab7-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="9aab7-535">La connessione al servizio OMS è bloccata</span><span class="sxs-lookup"><span data-stu-id="9aab7-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="9aab7-536">Viene eseguito il backup dei dati dell'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-537">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-537">Resolutions</span></span>
* <span data-ttu-id="9aab7-538">Controllare che il caricamento sul servizio OMS abbia avuto esito positivo verificando che `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` esista.</span><span class="sxs-lookup"><span data-stu-id="9aab7-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="9aab7-539">Ripetere il caricamento usando la riga di comando omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="9aab7-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="9aab7-540">Per maggiori informazioni, vedere [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Caricamento usando la riga di comando).</span><span class="sxs-lookup"><span data-stu-id="9aab7-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="9aab7-541">Se si usa un proxy, seguire i passaggi per la risoluzione dei problemi del proxy riportati sopra</span><span class="sxs-lookup"><span data-stu-id="9aab7-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="9aab7-542">In alcuni casi, quando l'agente OMS per Linux non può comunicare con il servizio OMS, viene eseguito il backup dei dati dell'agente alle dimensioni intere del buffer, cioè 50 MB.</span><span class="sxs-lookup"><span data-stu-id="9aab7-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="9aab7-543">Riavviare l'agente OMS per Linux eseguendo il comando `/opt/microsoft/omsagent/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="9aab7-544">Il problema è risolto nell'agente versione 1.1.0-28 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9aab7-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="9aab7-545">La configurazione del contatore delle prestazioni Syslog per Linux non viene applicata nel portale di OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-546">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-546">Probable causes</span></span>
* <span data-ttu-id="9aab7-547">L'agente di configurazione nell'agente OMS per Linux non ha recuperato la configurazione più recente dal portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="9aab7-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="9aab7-548">Le impostazioni modificate nel portale non sono state applicate</span><span class="sxs-lookup"><span data-stu-id="9aab7-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-549">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-549">Resolutions</span></span>
<span data-ttu-id="9aab7-550">`omsconfig` è l'agente di configurazione nell'agente OMS per Linux che recupera le modifiche alla configurazione del portale di OMS ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="9aab7-551">Questa configurazione viene quindi applicata ai file di configurazione dell'agente OMS per Linux disponibile su `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="9aab7-552">In alcuni casi, l'agente di configurazione OMS per Linux potrebbe non essere in grado di comunicare con il servizio di configurazione del portale, di conseguenza la configurazione più recente non viene applicata.</span><span class="sxs-lookup"><span data-stu-id="9aab7-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="9aab7-553">Verificare che l'agente `omsconfig` sia installato con le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="9aab7-554">`dpkg --list omsconfig` oppure `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="9aab7-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="9aab7-555">Se non è installato, reinstallare la versione più recente dell'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="9aab7-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="9aab7-556">Verificare che l'agente `omsconfig` possa comunicare con il servizio OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="9aab7-557">Eseguire il comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`</span><span class="sxs-lookup"><span data-stu-id="9aab7-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="9aab7-558">Il comando precedente restituisce la configurazione che l'agente recupera dal portale, incluse le impostazioni di Syslog, i contatori delle prestazioni di Linux e i log personalizzati</span><span class="sxs-lookup"><span data-stu-id="9aab7-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="9aab7-559">Se il comando precedente ha esito negativo, eseguire il comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="9aab7-560">Questo comando forza l'agente omsconfig a comunicare con il servizio OMS per recuperare la configurazione più recente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="9aab7-561">I dati personalizzati di Linux non vengono visualizzati nel portale di OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9aab7-562">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="9aab7-562">Probable causes</span></span>
* <span data-ttu-id="9aab7-563">Il caricamento nel servizio OMS ha avuto esito negativo</span><span class="sxs-lookup"><span data-stu-id="9aab7-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="9aab7-564">L'impostazione **Applica la configurazione seguente ai server Linux** non è stata selezionata</span><span class="sxs-lookup"><span data-stu-id="9aab7-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="9aab7-565">omsconfig non ha selezionato il log personalizzato più recente dal portale</span><span class="sxs-lookup"><span data-stu-id="9aab7-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="9aab7-566">L'uso di `omsagent` non consente di accedere al log personalizzato a causa di un problema con le autorizzazioni oppure non è stato possibile trovare `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="9aab7-567">In questo caso, viene visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="9aab7-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="9aab7-568">Si tratta di un problema noto con la race condition che è stato risolto nell'agente OMS per Linux versione 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="9aab7-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9aab7-569">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9aab7-569">Resolutions</span></span>
* <span data-ttu-id="9aab7-570">Verificare che il caricamento sia stato eseguito correttamente determinando se il file `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` esiste.</span><span class="sxs-lookup"><span data-stu-id="9aab7-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="9aab7-571">Se necessario, ripetere il caricamento usando la riga di comando omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="9aab7-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="9aab7-572">Per maggiori informazioni, vedere [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Caricamento usando la riga di comando).</span><span class="sxs-lookup"><span data-stu-id="9aab7-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="9aab7-573">In **Impostazioni** nella scheda **Dati** del portale di OMS verificare che sia selezionata l'impostazione **Applica la configurazione seguente ai server Linux**</span><span class="sxs-lookup"><span data-stu-id="9aab7-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="9aab7-574">![applicazione della configurazione](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="9aab7-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="9aab7-575">Verificare che l'agente `omsconfig` possa comunicare con il servizio OMS</span><span class="sxs-lookup"><span data-stu-id="9aab7-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="9aab7-576">Eseguire il comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`</span><span class="sxs-lookup"><span data-stu-id="9aab7-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="9aab7-577">Il comando precedente restituisce la configurazione che l'agente recupera dal portale, incluse le impostazioni di Syslog, i contatori delle prestazioni di Linux e i log personalizzati</span><span class="sxs-lookup"><span data-stu-id="9aab7-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="9aab7-578">Se il comando precedente ha esito negativo, eseguire il comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="9aab7-579">Questo comando forza l'agente omsconfig a comunicare con il servizio OMS e a recuperare la configurazione più recente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="9aab7-580">Invece di eseguire l'utente dell'agente OMS per Linux come utente privilegiato `root`, viene eseguito l'agente OMS per Linux come utente `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="9aab7-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="9aab7-581">Nella maggior parte dei casi, è necessario che all'utente venga concessa l'autorizzazione esplicita per leggere alcuni file.</span><span class="sxs-lookup"><span data-stu-id="9aab7-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="9aab7-582">Per concedere l'autorizzazione all'utente `omsagent`, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9aab7-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="9aab7-583">Aggiungere l'utente `omsagent` a un gruppo specifico con `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="9aab7-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="9aab7-584">Concedere l'accesso universale in lettura al file richiesto con `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="9aab7-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="9aab7-585">È presente un problema noto con la race condition che è stato risolto nell'agente OMS per Linux versione 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="9aab7-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="9aab7-586">Dopo l'aggiornamento all'agente più recente, eseguire il comando seguente per ottenere la versione più recente del plug-in di output:</span><span class="sxs-lookup"><span data-stu-id="9aab7-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="9aab7-587">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="9aab7-587">Known limitations</span></span>
<span data-ttu-id="9aab7-588">Per informazioni sulle limitazioni correnti per l'agente OMS per Linux, vedere le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9aab7-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="9aab7-589">Diagnostica Azure</span><span class="sxs-lookup"><span data-stu-id="9aab7-589">Azure Diagnostics</span></span>
<span data-ttu-id="9aab7-590">Per le macchine virtuali Linux in esecuzione in Azure potrebbero essere necessari passaggi aggiuntivi per consentire la raccolta di dati da parte di Diagnostica di Azure e Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9aab7-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="9aab7-591">**versione 2.2** dell'estensione di diagnostica per Linux è necessaria per la compatibilità con l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="9aab7-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="9aab7-592">Per altre informazioni sull'installazione e sulla configurazione dell'estensione di diagnostica per Linux, vedere [Usare l'interfaccia della riga di comando di Azure per abilitare l'estensione di diagnostica per Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="9aab7-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="9aab7-593">**Aggiornamento dell'estensione di diagnostica per Linux dalla versione 2.0 alla versione 2.2 di ASM dell'interfaccia della riga di comando di Azure:**</span><span class="sxs-lookup"><span data-stu-id="9aab7-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="9aab7-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="9aab7-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="9aab7-595">Questi esempi di comando fanno riferimento a un file denominato PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="9aab7-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="9aab7-596">Il formato del file deve essere analogo all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="9aab7-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="9aab7-597">Sysklog non è supportato.</span><span class="sxs-lookup"><span data-stu-id="9aab7-597">Sysklog is not supported</span></span>
<span data-ttu-id="9aab7-598">Per raccogliere i messaggi SysLog, è necessario rsyslog o syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="9aab7-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="9aab7-599">Il daemon SysLog predefinito nella versione 5 di Red Hat Enterprise Linux, CentOS e nella versione Oracle Linux (sysklog) non è supportato per la raccolta di eventi SysLog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9aab7-600">Per raccogliere i dati di SysLog da questa versione delle distribuzioni, è necessario installare e configurare il daemon rsyslog in modo da sostituire sysklog.</span><span class="sxs-lookup"><span data-stu-id="9aab7-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="9aab7-601">Per altre informazioni sulla sostituzione di sysklog con rsyslog, vedere la pagina relativa all' [installazione di RPM rsyslog appena compilato](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="9aab7-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aab7-602">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9aab7-602">Next Steps</span></span>
* <span data-ttu-id="9aab7-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) (Aggiungere soluzioni di Log Analytics dalla raccolta soluzioni) per aggiungere funzionalità e raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="9aab7-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="9aab7-604">Acquisire familiarità con le [ricerche nei log](log-analytics-log-searches.md) per visualizzare le informazioni dettagliate raccolte dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9aab7-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="9aab7-605">Usare i [dashboard](log-analytics-dashboards.md) per salvare e visualizzare le ricerche personalizzate.</span><span class="sxs-lookup"><span data-stu-id="9aab7-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
