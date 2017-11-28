---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="4d4f1-101">Connettere il tooLog computer Linux Analitica</span><span class="sxs-lookup"><span data-stu-id="4d4f1-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="4d4f1-102">Log Analytics consente di raccogliere dati dai computer Linux e di agire in base a essi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="4d4f1-103">Aggiunta di dati raccolti da Linux tooOMS consente toomanage i sistemi Linux e le soluzioni contenitore come Docker, indipendentemente dalla posizione dei computer, praticamente ovunque.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="4d4f1-104">Origini dati possono risiedere nel data center locale come server fisici, computer virtuali in un servizio ospitato su cloud come Amazon Web Services (AWS) o Microsoft Azure, o anche hello portatile sulla propria scrivania.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="4d4f1-105">OMS raccoglie anche dati da computer Windows in modo analogo, quindi supporta un ambiente IT effettivamente ibrido.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="4d4f1-106">È possibile visualizzare e gestire i dati da tutte queste origini dati con Log Analytics in OMS con un singolo portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="4d4f1-107">Questo riduce la necessità di hello toomonitor con diversi sistemi, rende facile tooconsume ed è possibile esportare i dati desiderati toowhatever analitica soluzione o sistema aziendale già disponibile.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="4d4f1-108">Questo articolo è una Guida introduttiva che consente di raccogliere e gestire i dati per i computer Linux usando hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="4d4f1-109">Maggiori informazioni tecniche, ad esempio informazioni su configurazione del server proxy, informazioni sulle metriche di CollectD e origini dati JSON personalizzati sono disponibili nella [panoramica sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) e nella [documentazione completa sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="4d4f1-110">Attualmente, è possibile raccogliere hello seguenti tipi di dati da computer Linux:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="4d4f1-111">Metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-111">Performance metrics</span></span>
* <span data-ttu-id="4d4f1-112">Eventi SysLog</span><span class="sxs-lookup"><span data-stu-id="4d4f1-112">Syslog events</span></span>
* <span data-ttu-id="4d4f1-113">Avvisi da Nagios e Zabbix</span><span class="sxs-lookup"><span data-stu-id="4d4f1-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="4d4f1-114">Metriche delle prestazioni, inventario e log del contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="4d4f1-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="4d4f1-115">Versioni di Linux supportate</span><span class="sxs-lookup"><span data-stu-id="4d4f1-115">Supported Linux versions</span></span>
<span data-ttu-id="4d4f1-116">Le versioni x86 e x64 sono supportate ufficialmente su diverse distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="4d4f1-117">Tuttavia, hello agente OMS per Linux può essere eseguito anche in altre distribuzioni non elencate.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="4d4f1-118">Amazon Linux dalla 2012.09 alla 2015.09</span><span class="sxs-lookup"><span data-stu-id="4d4f1-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="4d4f1-119">CentOS Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="4d4f1-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="4d4f1-120">Oracle Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="4d4f1-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="4d4f1-121">Red Hat Enterprise Linux Server 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="4d4f1-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="4d4f1-122">Debian GNU/Linux 6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="4d4f1-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="4d4f1-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="4d4f1-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="4d4f1-124">SUSE Linux Enterprise Server 11 e 12</span><span class="sxs-lookup"><span data-stu-id="4d4f1-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="4d4f1-125">Agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-125">OMS Agent for Linux</span></span>
<span data-ttu-id="4d4f1-126">Hello agente Operations Management Suite per Linux è costituito da più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="4d4f1-127">versione file Hello contiene hello seguenti pacchetti, disponibili dal bundle della shell hello in esecuzione con `--extract`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="4d4f1-128">**Pacchetto**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-128">**Package**</span></span> | <span data-ttu-id="4d4f1-129">**Versione**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-129">**Version**</span></span> | <span data-ttu-id="4d4f1-130">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d4f1-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="4d4f1-131">omsagent</span></span> |<span data-ttu-id="4d4f1-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4d4f1-132">1.1.0</span></span> |<span data-ttu-id="4d4f1-133">Hello agente Operations Management Suite per Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="4d4f1-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="4d4f1-134">omsconfig</span></span> |<span data-ttu-id="4d4f1-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4d4f1-135">1.1.1</span></span> |<span data-ttu-id="4d4f1-136">Agente di configurazione per l'agente OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="4d4f1-137">omi</span><span class="sxs-lookup"><span data-stu-id="4d4f1-137">omi</span></span> |<span data-ttu-id="4d4f1-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="4d4f1-138">1.0.8.3</span></span> |<span data-ttu-id="4d4f1-139">Open Management Infrastructure (OMI): server CIM leggero</span><span class="sxs-lookup"><span data-stu-id="4d4f1-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="4d4f1-140">scx</span><span class="sxs-lookup"><span data-stu-id="4d4f1-140">scx</span></span> |<span data-ttu-id="4d4f1-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="4d4f1-141">1.6.2</span></span> |<span data-ttu-id="4d4f1-142">Provider OMI CIM per metriche delle prestazioni del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="4d4f1-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="4d4f1-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="4d4f1-143">apache-cimprov</span></span> |<span data-ttu-id="4d4f1-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4d4f1-144">1.0.0</span></span> |<span data-ttu-id="4d4f1-145">Monitoraggio delle prestazioni del server HTTP Apache per OMI.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="4d4f1-146">Installato solo se viene rilevato il server HTTP Apache.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="4d4f1-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="4d4f1-147">mysql-cimprov</span></span> |<span data-ttu-id="4d4f1-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4d4f1-148">1.0.0</span></span> |<span data-ttu-id="4d4f1-149">Monitoraggio delle prestazioni del server MySQL per OMI.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="4d4f1-150">Installato solo se viene rilevato il server MySQL/MariaDB.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="4d4f1-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="4d4f1-151">docker-cimprov</span></span> |<span data-ttu-id="4d4f1-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="4d4f1-152">0.1.0</span></span> |<span data-ttu-id="4d4f1-153">Provider Docker per OMI.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-153">Docker provider for OMI.</span></span> <span data-ttu-id="4d4f1-154">Installato solo se viene rilevato Docker.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="4d4f1-155">Elementi di installazione aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="4d4f1-155">Additional installation artifacts</span></span>
<span data-ttu-id="4d4f1-156">Dopo aver installato l'agente OMS hello per i pacchetti Linux, hello modifiche di configurazione aggiuntive a livello di sistema seguenti vengono applicate.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="4d4f1-157">Questi elementi vengono rimossi quando il pacchetto omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="4d4f1-158">Viene creato un utente senza privilegi denominato `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="4d4f1-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="4d4f1-159">Si tratta di hello account hello omsagent daemon eseguito come</span><span class="sxs-lookup"><span data-stu-id="4d4f1-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="4d4f1-160">Viene creato un file "include" sudoers in /etc/sudoers.d/omsagent. questo autorizza omsagent toorestart hello syslog e i daemon omsagent.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="4d4f1-161">Se le direttive "include" sudo non sono supportate nella versione di hello installata di sudo, queste voci verranno scritte troppo/ecc/file.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="4d4f1-162">configurazione di syslog Hello è tooforward modificato un subset dell'agente toohello eventi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="4d4f1-163">Per ulteriori informazioni, vedere hello **configurazione della raccolta dei dati** sezione riportata di seguito</span><span class="sxs-lookup"><span data-stu-id="4d4f1-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="4d4f1-164">Informazioni dettagliate sulla raccolta di dati Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-164">Linux data collection details</span></span>
<span data-ttu-id="4d4f1-165">Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="4d4f1-166">una sezione source</span><span class="sxs-lookup"><span data-stu-id="4d4f1-166">source</span></span> | <span data-ttu-id="4d4f1-167">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="4d4f1-167">Direct Agent</span></span> | <span data-ttu-id="4d4f1-168">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="4d4f1-168">SCOM agent</span></span> | <span data-ttu-id="4d4f1-169">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4d4f1-169">Azure Storage</span></span> | <span data-ttu-id="4d4f1-170">SCOM obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4d4f1-170">SCOM required?</span></span> | <span data-ttu-id="4d4f1-171">Dati dell'agente SCOM inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="4d4f1-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="4d4f1-172">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="4d4f1-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4d4f1-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="4d4f1-173">Zabbix</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="4d4f1-179">1 minuto</span><span class="sxs-lookup"><span data-stu-id="4d4f1-179">1 minute</span></span> |
| <span data-ttu-id="4d4f1-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="4d4f1-180">Nagios</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="4d4f1-186">All'arrivo</span><span class="sxs-lookup"><span data-stu-id="4d4f1-186">on arrival</span></span> |
| <span data-ttu-id="4d4f1-187">syslog</span><span class="sxs-lookup"><span data-stu-id="4d4f1-187">syslog</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="4d4f1-193">dall'Archiviazione di Azure: 10 minuti; dall'agente: all'arrivo</span><span class="sxs-lookup"><span data-stu-id="4d4f1-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="4d4f1-194">Contatori delle prestazioni di Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-194">Linux performance counters</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="4d4f1-200">Come pianificato, almeno 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="4d4f1-201">Rilevamento modifiche</span><span class="sxs-lookup"><span data-stu-id="4d4f1-201">change tracking</span></span> |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="4d4f1-207">Ogni ora</span><span class="sxs-lookup"><span data-stu-id="4d4f1-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="4d4f1-208">Requisiti del pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d4f1-208">Package Requirements</span></span>
| <span data-ttu-id="4d4f1-209">**Pacchetto obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-209">**Required package**</span></span> | <span data-ttu-id="4d4f1-210">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-210">**Description**</span></span> | <span data-ttu-id="4d4f1-211">**Versione minima**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d4f1-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="4d4f1-212">Glibc</span></span> |<span data-ttu-id="4d4f1-213">Libreria GNU C</span><span class="sxs-lookup"><span data-stu-id="4d4f1-213">GNU C library</span></span> |<span data-ttu-id="4d4f1-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="4d4f1-214">2.5-12</span></span> |
| <span data-ttu-id="4d4f1-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="4d4f1-215">Openssl</span></span> |<span data-ttu-id="4d4f1-216">Librerie OpenSSL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-216">OpenSSL libraries</span></span> |<span data-ttu-id="4d4f1-217">0.9.8e o 1.0</span><span class="sxs-lookup"><span data-stu-id="4d4f1-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="4d4f1-218">Curl</span><span class="sxs-lookup"><span data-stu-id="4d4f1-218">Curl</span></span> |<span data-ttu-id="4d4f1-219">Client Web cURL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-219">cURL web client</span></span> |<span data-ttu-id="4d4f1-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="4d4f1-220">7.15.5</span></span> |
| <span data-ttu-id="4d4f1-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="4d4f1-221">Python-ctypes</span></span> |<span data-ttu-id="4d4f1-222">Librerie di funzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-222">function libraries</span></span> |<span data-ttu-id="4d4f1-223">N/D</span><span class="sxs-lookup"><span data-stu-id="4d4f1-223">n/a</span></span> |
| <span data-ttu-id="4d4f1-224">PAM</span><span class="sxs-lookup"><span data-stu-id="4d4f1-224">PAM</span></span> |<span data-ttu-id="4d4f1-225">Moduli di autenticazione modulare</span><span class="sxs-lookup"><span data-stu-id="4d4f1-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="4d4f1-226">n/d</span><span class="sxs-lookup"><span data-stu-id="4d4f1-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="4d4f1-227">Rsyslog o syslog-ng sono necessari toocollect messaggi syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="4d4f1-228">il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="4d4f1-229">dati di syslog toocollect da questa versione di queste distribuzioni, hello rsyslog daemon deve essere installato e configurato tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="4d4f1-230">Installazione rapida</span><span class="sxs-lookup"><span data-stu-id="4d4f1-230">Quick install</span></span>
<span data-ttu-id="4d4f1-231">Eseguire i seguenti comandi toodownload hello omsagent hello, la convalida di checksum hello, quindi installare e agente hello onboard.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="4d4f1-232">I comandi sono per la versione a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-232">Commands are for 64-bit.</span></span> <span data-ttu-id="4d4f1-233">Hello ID area di lavoro e chiave primaria sono disponibili nel portale OMS hello in **impostazioni** su hello **Connected Sources** scheda.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![Dettagli dell'area di lavoro](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="4d4f1-235">Sono disponibili numerosi altri metodi di tooinstall hello agente e aggiornarlo.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="4d4f1-236">Altre informazioni su di essi in [hello tooinstall passaggi agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="4d4f1-237">È inoltre possibile visualizzare hello [Azure procedura dettagliata video](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="4d4f1-238">Scegliere il metodo di raccolta di dati Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="4d4f1-239">La modalità hello tipi di dati, che potrebbe ad esempio toocollect varia a seconda se si desidera portale di OMS hello toouse o se si desidera modificare i vari file di configurazione direttamente nei client Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="4d4f1-240">Se si sceglie portale hello toouse, configurazione hello viene inviato automaticamente tooall i client Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="4d4f1-241">Se servono configurazioni diverse per diversi client Linux, necessario file client tooedit singolarmente o utilizzare un'alternativa, come PowerShell DSC, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="4d4f1-242">È possibile specificare gli eventi syslog hello e contatori delle prestazioni che si desidera toocollect utilizzando file di configurazione nei computer Linux hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="4d4f1-243">*Se si sceglie la raccolta dei dati tooconfigure modificando i file di configurazione dell'agente, è necessario disabilitare la configurazione centralizzata di hello.*</span><span class="sxs-lookup"><span data-stu-id="4d4f1-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="4d4f1-244">Vengono fornite istruzioni sotto tooconfigure la raccolta dei dati dell'agente di hello i file di configurazione, nonché toodisable configurazione centrale per tutti gli agenti OMS per Linux o singoli computer.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="4d4f1-245">Disabilitare la gestione OMS per un singolo computer Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="4d4f1-246">Raccolta dei dati centralizzata per i dati di configurazione è disabilitata per un singolo computer Linux con hello script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="4d4f1-247">Ciò può risultare utile se un sottoinsieme di computer necessita di una configurazione specializzata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="4d4f1-248">toodisable configurazione centralizzata:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="4d4f1-249">toore-abilita la configurazione centralizzata:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="4d4f1-250">Contatori delle prestazioni di Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-250">Linux performance counters</span></span>
<span data-ttu-id="4d4f1-251">Contatori delle prestazioni di Linux sono contatori di prestazioni simili tooWindows, entrambi hanno un funzionamento analogo.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="4d4f1-252">È possibile utilizzare hello seguendo procedure tooadd e configurarli.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="4d4f1-253">Dopo che sono state aggiunte tooOMS, raccolta dei dati per loro ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="4d4f1-254">tooadd un contatore delle prestazioni di Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="4d4f1-255">gli agenti OMS per Linux tramite il portale di OMS hello tooconfigure, è possibile aggiungere i contatori delle prestazioni di Linux nella pagina Impostazioni hello, fare clic su **dati**.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="4d4f1-256">In hello **impostazioni** pagina **dati** , fare clic su **i contatori delle prestazioni di Linux** e quindi selezionare o digitare hello nome del contatore hello desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="4d4f1-257">![dati](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="4d4f1-258">Se non si conosce nome completo di hello del contatore di hello, è possibile iniziare a digitare un nome parziale e verrà visualizzato un elenco dei contatori disponibili.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="4d4f1-259">Quando si individua il contatore hello desidera tooadd, fare clic sul nome nell'elenco di hello hello e quindi fare clic su hello più hello tooadd icona contatore.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="4d4f1-260">Dopo aver aggiunto il contatore hello, viene visualizzato nell'elenco di hello dei contatori evidenziato con una barra colorata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="4d4f1-261">Per impostazione predefinita, hello **Apply below macchine toomy configurazione** opzione è selezionata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="4d4f1-262">Se si desidera toodisable l'invio di dati di configurazione, deselezionare la selezione di hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="4d4f1-263">Al termine la modifica dei contatori delle prestazioni, nella parte inferiore di hello della pagina hello fare clic su **salvare** toofinalize le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="4d4f1-264">le modifiche di configurazione Hello apportate vengono quindi inviate hello tooall gli agenti OMS per Linux registrati in OMS, in genere entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="4d4f1-265">Configurare i contatori delle prestazioni di Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="4d4f1-266">Per i contatori delle prestazioni di Windows è possibile scegliere un'istanza specifica per ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="4d4f1-267">Tuttavia, per i contatori delle prestazioni di Linux, qualsiasi istanza di un contatore prescelto si applica tooall i contatori figlio del contatore padre hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="4d4f1-268">Hello nella tabella seguente mostra le istanze comuni hello tooboth disponibili Linux e Windows contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="4d4f1-269">**Nome dell'istanza**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-269">**Instance name**</span></span> | <span data-ttu-id="4d4f1-270">**Significato**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="4d4f1-271">\_Totale</span><span class="sxs-lookup"><span data-stu-id="4d4f1-271">\_Total</span></span> |<span data-ttu-id="4d4f1-272">Totale di tutte le istanze di hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="4d4f1-273">Tutte le istanze</span><span class="sxs-lookup"><span data-stu-id="4d4f1-273">All instances</span></span> |
| <span data-ttu-id="4d4f1-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-274">(/&#124;/var)</span></span> |<span data-ttu-id="4d4f1-275">Corrisponde alle istanze denominate / oppure /var</span><span class="sxs-lookup"><span data-stu-id="4d4f1-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="4d4f1-276">Analogamente, hello intervallo di campionamento che si sceglie per un contatore padre si applica tooall i contatori figlio.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="4d4f1-277">In altre parole, tutti gli intervalli di campionamento contatore hello figlio e le istanze sono collegate tra loro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="4d4f1-278">Aggiungere e configurare le metriche delle prestazioni con Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="4d4f1-279">Toocollect le metriche delle prestazioni sono controllate dalla configurazione hello in/ecc/rifiutare/microsoft/omsagent/&lt;id area di lavoro&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="4d4f1-280">Vedere [metriche delle prestazioni disponibili](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) per le classi disponibili e le metriche per hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="4d4f1-281">Ogni oggetto, o categoria, delle prestazioni metriche toocollect deve essere definito nel file di configurazione hello come una singola `<source>` elemento.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="4d4f1-282">sintassi di Hello seguito è descritto hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="4d4f1-283">Hello parametri configurabili di questo elemento sono:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="4d4f1-284">**Oggetto\_nome**: nome dell'oggetto per la raccolta di hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="4d4f1-285">**Istanza\_regex**: un *espressione regolare* toocollect quali istanze di definizione.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="4d4f1-286">valore di Hello: `.*` specifica tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="4d4f1-287">le metriche del processore toocollect per solo hello \_istanza totale, è possibile specificare `_Total`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="4d4f1-288">per dati metrici sui processi toocollect hello solo le istanze crond o sshd, è possibile specificare: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="4d4f1-289">**Contatore\_nome\_regex**: un *espressione regolare* definizione toocollect quali contatori (per oggetto hello).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="4d4f1-290">specificare tutti i contatori per l'oggetto hello, toocollect: `.*`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="4d4f1-291">toocollect solo i contatori di spazio di swapping per l'oggetto memoria hello, è possibile specificare:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="4d4f1-292">**Intervallo:**: hello frequenza di raccolta contatori dell'oggetto cui hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="4d4f1-293">configurazione predefinita di Hello per le metriche delle prestazioni è:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="4d4f1-294">Abilitare i contatori delle prestazioni di MySQL usando comandi di Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="4d4f1-295">Se il MySQL Server o MariaDB Server viene rilevato nel computer di hello durante l'installazione del bundle omsagent hello, viene installata automaticamente un provider per il MySQL Server di monitoraggio delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="4d4f1-296">Questo provider si connette toohello locale MySQL/MariaDB server tooexpose le statistiche sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="4d4f1-297">È necessario tooconfigure le credenziali utente di MySQL in modo che hello provider possa accedere hello MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="4d4f1-298">toodefine un predefinito account utente per il server MySQL hello in localhost, usare hello esempio di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="4d4f1-299">file delle credenziali Hello deve essere leggibile per l'account omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="4d4f1-300">È consigliabile eseguire comandi di hello mycimprovauth come omsgent.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="4d4f1-301">In alternativa, è possibile specificare hello necessarie le credenziali di MySQL in un file, creando hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Per ulteriori informazioni sulla gestione delle credenziali di MySQL per il monitoraggio tramite file mysql-auth hello, vedere [le credenziali nel file di autenticazione hello il monitoraggio di MySQL gestire](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="4d4f1-302">Vedere [Database le autorizzazioni necessarie per i contatori delle prestazioni di MySQL](#database-permissions-required-for-mysql-performance-counters) per informazioni dettagliate sulle autorizzazioni per gli oggetti necessari per hello MySQL utente toocollect dati sulle prestazioni di MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="4d4f1-303">Abilitare i contatori delle prestazioni del server HTTP Apache usando comandi di Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="4d4f1-304">Se nel computer di hello viene rilevato Apache HTTP Server durante l'installazione del bundle omsagent hello, viene installata automaticamente un provider di Apache HTTP Server per il monitoraggio delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="4d4f1-305">Questo provider si basa su un "modulo" Apache che deve essere caricato in dati sulle prestazioni di ordine tooaccess Ciao Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="4d4f1-306">È possibile caricare il modulo di hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="4d4f1-307">toounload hello Apache modulo di monitoraggio, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="4d4f1-308">dati sulle prestazioni tooview con Log Analitica</span><span class="sxs-lookup"><span data-stu-id="4d4f1-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="4d4f1-309">Nel portale di Operations Management Suite hello, fare clic sul riquadro Log Search hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="4d4f1-310">Nella barra di ricerca hello, digitare `* (Type=Perf)` tooview tutti i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="4d4f1-311">Poiché OMS raccoglie anche i dati del contatore delle prestazioni di Windows, è necessario limitare ambito hello dati tooLinux specifici di ricerca.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="4d4f1-312">In tal caso, hello esempio permetterebbe di visualizzare le prestazioni dei dati specifico tooan server Linux di esempio denominato Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![Server di esempio visualizzato nei risultati della ricerca](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="4d4f1-314">Nei risultati di hello, è possibile fare clic su **metriche** contatori hello tooview che per la raccolta dei dati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="4d4f1-315">I dati in tempo reale vengono mostrati come grafici per ogni contatore.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-315">Real-time data is shown as graphs for each counter.</span></span>

![Metriche](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="4d4f1-317">syslog</span><span class="sxs-lookup"><span data-stu-id="4d4f1-317">Syslog</span></span>
<span data-ttu-id="4d4f1-318">Syslog è un protocollo analogo tooWindows i registri eventi di registrazione di eventi, ovvero entrambi funzionano in modo analogo, quando sono visualizzati in OMS.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="4d4f1-319">tooadd una nuova funzione syslog di Linux in OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="4d4f1-320">In hello **impostazioni** pagina **dati** , fare clic su **Syslog** e toohello a sinistra dell'icona di addizione hello, digitare hello nome della funzione syslog hello che si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="4d4f1-321">![Syslog per Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="4d4f1-322">Se non si conosce nome completo di hello della funzione di hello, è possibile iniziare a digitare un nome parziale e verrà visualizzato un elenco delle funzioni syslog disponibili.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="4d4f1-323">Quando si trova funzione syslog di hello desidera tooadd, fare clic sul nome nell'elenco di hello hello e quindi fare clic su hello più hello tooadd icona funzione syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="4d4f1-324">Dopo averla aggiunta, viene visualizzato nell'elenco di hello di funzione hello evidenziata con una barra colorata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="4d4f1-325">Successivamente, scegliere i livelli di gravità hello (categorie di informazioni funzione syslog) che si desidera toocollect.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="4d4f1-326">Nella parte inferiore di hello di hello pagina fare clic su **salvare** toofinalize le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="4d4f1-327">le modifiche di configurazione Hello apportate vengono quindi inviate hello tooall gli agenti OMS per Linux registrati in OMS, in genere entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="4d4f1-328">Configurare le funzionalità SysLog per Linux in Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="4d4f1-329">Gli eventi Syslog vengono inviati dal daemon syslog hello, ad esempio rsyslog o syslog-ng, porta locale tooa che l'agente di hello è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="4d4f1-330">Per impostazione predefinita, si tratta della porta 25224.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-330">By default, port 25224.</span></span> <span data-ttu-id="4d4f1-331">Quando viene installato l'agente di hello, viene applicata una configurazione predefinita di syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="4d4f1-332">disponibile in:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-332">This is found at:</span></span>

<span data-ttu-id="4d4f1-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="4d4f1-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="4d4f1-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="4d4f1-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="4d4f1-335">configurazione di syslog agente di Hello predefinita OMS carica gli eventi syslog da tutte le funzioni con un livello di gravità avviso o superiore.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="4d4f1-336">Se si modifica la configurazione di syslog hello, è necessario riavviare i daemon syslog hello hello modifiche tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="4d4f1-337">Hello configurazione predefinita di syslog per hello agente OMS per Linux per OMS è:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="4d4f1-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="4d4f1-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="4d4f1-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="4d4f1-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="4d4f1-340">tooview tutti gli eventi Syslog con Log Analitica</span><span class="sxs-lookup"><span data-stu-id="4d4f1-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="4d4f1-341">Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="4d4f1-342">In hello **Log Management** raggruppamento, scegliere una ricerca syslog predefinita e quindi selezionare uno toorun è.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="4d4f1-343">Questo esempio mostra tutti gli eventi SysLog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-343">This example shows all Syslog events.</span></span>

![Eventi SysLog visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="4d4f1-345">È ora possibile esaminare i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="4d4f1-346">Avvisi di Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-346">Linux alerts</span></span>
<span data-ttu-id="4d4f1-347">Se si usa Nagios o Zabbix toomanage che i computer Linux, quindi OMS può ricevere avvisi di hello generati da questi strumenti.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="4d4f1-348">Tuttavia, non sono attualmente presenti metodo tooconfigure in ingresso avviso dati tramite il portale di OMS hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="4d4f1-349">Al contrario, sarà necessario tooedit l'invio degli avvisi tooOMS una configurazione file toostart.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="4d4f1-350">Raccogliere avvisi da Nagios</span><span class="sxs-lookup"><span data-stu-id="4d4f1-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="4d4f1-351">toocollect gli avvisi da un server Nagios, è necessario hello toomake dopo le modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="4d4f1-352">Concedere all'utente di hello **omsagent** file di log Nagios toohello accesso in lettura (ad esempio /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="4d4f1-353">Supponendo che i file nagios.log hello è di proprietà di gruppo hello **nagios** , è possibile aggiungere l'utente hello **omsagent** toohello **nagios** gruppo.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="4d4f1-354">Modificare il file di confconfiguration hello (via/rifiutare/microsoft/omsagent / /&lt;id area di lavoro&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="4d4f1-355">Verificare che siano presenti e non come commento hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="4d4f1-356">Riavviare i daemon omsagent hello:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="4d4f1-357">Raccogliere avvisi da Zabbix</span><span class="sxs-lookup"><span data-stu-id="4d4f1-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="4d4f1-358">toocollect gli avvisi da un server Zabbix, la procedura è simile passaggi toothose precedenza per Nagios, ma sarà necessario toospecify un utente e password in *cancellare il testo*.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="4d4f1-359">Questo approccio non è ideale, ma verrà probabilmente modificato a breve.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="4d4f1-360">tooaddress questo problema, è consigliabile creare utente hello e concedere l'autorizzazione toomonitor solo.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="4d4f1-361">Una sezione di esempio del file di configurazione omsagent. conf hello (via/rifiutare/microsoft/omsagent / /&lt;id area di lavoro&gt;/conf/omsagent.conf) per Zabbix sarebbe simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="4d4f1-362">Visualizzare avvisi nella ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4d4f1-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="4d4f1-363">Dopo aver configurato il tooOMS di avvisi toosend computer Linux, è possibile utilizzare alcuni semplici ricerca query tooview hello gli avvisi del registro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="4d4f1-364">Hello esempio query di ricerca seguente restituisce tutti gli avvisi di hello registrato che sono stati generati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="4d4f1-365">Ad esempio, se si verifica un problema di problema nell'infrastruttura IT, quindi i risultati per hello query potrebbero indicare problemi hello potrebbero origine di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="4d4f1-366">Inoltre, è possibile isolare facilmente negli avvisi toohello da toohelp di sistema di origine "narrow" l'analisi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="4d4f1-367">Hello vantaggio è che non è necessariamente i sistemi di gestione di toogo toovarious dall'inizio di hello, purché gli avvisi vengono inviati tooOMS, è possibile avviare non esiste.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="4d4f1-368">tooview Nagios tutti gli avvisi con Log Analitica</span><span class="sxs-lookup"><span data-stu-id="4d4f1-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="4d4f1-369">Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="4d4f1-370">Nella barra di query hello, digitare hello seguenti query di ricerca</span><span class="sxs-lookup"><span data-stu-id="4d4f1-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Avvisi Nagios visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="4d4f1-372">Dopo aver visualizzato i risultati della ricerca hello, è possibile esaminare i dettagli aggiuntivi, ad esempio *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="4d4f1-373">tooview tutti gli avvisi Zabbix con Log Analitica</span><span class="sxs-lookup"><span data-stu-id="4d4f1-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="4d4f1-374">Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="4d4f1-375">Nella barra di query hello, digitare hello seguenti query di ricerca</span><span class="sxs-lookup"><span data-stu-id="4d4f1-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Avvisi Zabbix visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="4d4f1-377">Dopo aver visualizzato i risultati della ricerca hello, è possibile esaminare i dettagli aggiuntivi, ad esempio *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="4d4f1-378">Compatibilità con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4d4f1-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="4d4f1-379">Hello agente OMS per Linux condivide i file binari dell'agente con l'agente di System Center Operations Manager hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="4d4f1-380">L'installazione di hello agente OMS per Linux in un sistema attualmente gestito da Operations Manager aggiornamenti hello pacchetti OMI e SCX nella versione più recente di hello computer tooa.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="4d4f1-381">Hello agente OMS per Linux e System Center 2012 R2 sono compatibili.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="4d4f1-382">Tuttavia, **System Center 2012 SP1 e versioni precedenti sono attualmente non supportati o compatibili con hello agente OMS per Linux.**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="4d4f1-383">Se l'agente OMS per Linux hello è installato tooa computer che non è attualmente gestito da Operations Manager e in seguito si desidera computer hello toomanage con Operations Manager, è necessario modificare configurazione OMI hello prima di individuare computer hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="4d4f1-384">**Questo passaggio non è necessario se l'agente di Operations Manager hello viene installato prima di hello agente OMS per Linux.**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="4d4f1-385">tooenable hello agente OMS per Linux toocommunicate con Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4d4f1-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="4d4f1-386">Modificare hello file /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="4d4f1-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="4d4f1-387">Verificare che hello riga che inizia con **httpsport =** definisca hello porta 1270.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="4d4f1-388">ad esempio `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="4d4f1-389">Riavviare il server OMI hello:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="4d4f1-390">Autorizzazioni del database necessarie per i contatori delle prestazioni di MySQL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="4d4f1-391">toogrant autorizzazioni tooa utente monitoraggio di MySQL, hello utente che concede deve avere il privilegio 'GRANT option' hello nonché privilegio hello da concedere.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="4d4f1-392">Affinché l'utente di MySQL hello utente hello dati sulle prestazioni di tooreturn avrà bisogno di accesso toohello seguente query:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="4d4f1-393">Utente di MySQL toothese query hello richiede inoltre l'accesso SELECT toohello le tabelle predefinite seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="4d4f1-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="4d4f1-394">information_schema</span></span>
* <span data-ttu-id="4d4f1-395">mysql</span><span class="sxs-lookup"><span data-stu-id="4d4f1-395">mysql</span></span>

<span data-ttu-id="4d4f1-396">È possibile concedere questi privilegi eseguendo i comandi grant seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="4d4f1-397">Gestire le credenziali nel file di autenticazione hello il monitoraggio di MySQL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="4d4f1-398">Hello nelle sezioni seguenti gestire le credenziali di MySQL.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="4d4f1-399">Configurare il provider OMI MySQL hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="4d4f1-400">il provider OMI MySQL Hello richiede un utente di MySQL preconfigurato e installate le librerie client di MySQL in ordine tooquery hello prestazioni o informazioni sull'integrità dall'istanza di MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="4d4f1-401">File di autenticazione OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="4d4f1-402">Il provider OMI MySQL Usa un toodetermine di file di autenticazione quale istanza di MySQL hello indirizzo di binding e la porta è in attesa e quali credenziali toouse toogather metriche.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="4d4f1-403">Durante la hello installazione OMI MySQL provider analizzerà i file di configurazione my.cnf di MySQL (nei percorsi predefiniti) per indirizzo di binding e la porta e parzialmente hello set di file di autenticazione OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="4d4f1-404">toocomplete monitoraggio di un'istanza di server MySQL, aggiungere un file di autenticazione OMI MySQL pregenerato nella directory corretta di hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="4d4f1-405">Formato del file di autenticazione</span><span class="sxs-lookup"><span data-stu-id="4d4f1-405">Authentication file format</span></span>
<span data-ttu-id="4d4f1-406">Hello file autenticazione OMI MySQL è un file di testo che contiene informazioni su:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="4d4f1-407">Porta</span><span class="sxs-lookup"><span data-stu-id="4d4f1-407">Port</span></span>
* <span data-ttu-id="4d4f1-408">Bind-address</span><span class="sxs-lookup"><span data-stu-id="4d4f1-408">Bind-Address</span></span>
* <span data-ttu-id="4d4f1-409">Nome utente MySQL</span><span class="sxs-lookup"><span data-stu-id="4d4f1-409">MySQL username</span></span>
* <span data-ttu-id="4d4f1-410">Password con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="4d4f1-410">Base64 encoded password</span></span>

<span data-ttu-id="4d4f1-411">Hello file autenticazione OMI MySQL concede solo privilegi di lettura/scrittura toohello Linux utente che ha generato.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="4d4f1-412">Un file di autenticazione OMI MySQL predefinito contiene un'istanza predefinita e un numero di porta a seconda delle informazioni disponibili e analizzate dal file di configurazione di MySQL trovato hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="4d4f1-413">istanza predefinita di Hello è un toomake indica la gestione di più istanze di MySQL in un singolo host Linux e corrisponde hello istanza con la porta 0.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="4d4f1-414">Tutte le istanze aggiunte ereditano le proprietà impostate dall'istanza predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="4d4f1-415">Ad esempio, se viene aggiunto l'istanza di MySQL in ascolto sulla porta '3308', indirizzo di binding, username e password con codificata Base64 dell'istanza predefinita di hello verrà essere tootry utilizzato e monitorare hello istanza in ascolto sulla porta 3308.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="4d4f1-416">Se l'istanza hello sulla porta 3308 è associata tooanother indirizzo e utilizzi hello stesso nome utente di MySQL e una password solo hello respecification di hello è necessaria l'indirizzo di binding e hello altre proprietà verrà ereditata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="4d4f1-417">Esempi del file di autenticazione hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="4d4f1-418">Istanza predefinita e istanza con porta 3308:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="4d4f1-419">Istanza predefinita e istanza con porta 3308 e password con codifica Base 64 diversa:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="4d4f1-420">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-420">**Property**</span></span> | <span data-ttu-id="4d4f1-421">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4d4f1-422">Porta</span><span class="sxs-lookup"><span data-stu-id="4d4f1-422">Port</span></span> |<span data-ttu-id="4d4f1-423">Porta rappresenta hello di porta corrente hello MySQL istanza è in attesa.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="4d4f1-424">porta Hello 0 implica che proprietà hello seguenti vengono utilizzate per l'istanza predefinita.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="4d4f1-425">Bind-address</span><span class="sxs-lookup"><span data-stu-id="4d4f1-425">Bind-Address</span></span> |<span data-ttu-id="4d4f1-426">Indirizzo di binding Hello è hello corrente MySQL indirizzo di binding</span><span class="sxs-lookup"><span data-stu-id="4d4f1-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="4d4f1-427">username</span><span class="sxs-lookup"><span data-stu-id="4d4f1-427">username</span></span> |<span data-ttu-id="4d4f1-428">Questo nome utente hello dell'utente di MySQL hello a cui l'istanza di server MySQL hello toouse toomonitor.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="4d4f1-429">Password con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="4d4f1-429">Base64 encoded Password</span></span> |<span data-ttu-id="4d4f1-430">Si tratta hello password dell'utente di monitoraggio MySQL hello con codificata Base64.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="4d4f1-431">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="4d4f1-431">AutoUpdate</span></span> |<span data-ttu-id="4d4f1-432">Quando viene aggiornato il Provider OMI MySQL hello hello provider Ripeti analisi per le modifiche nel file my.cnf hello e sovrascrivere il file di autenticazione OMI MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="4d4f1-433">Impostare questo flag tootrue o false a seconda degli aggiornamenti necessari toohello OMI MySQL file di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="4d4f1-434">Percorso del file di autenticazione</span><span class="sxs-lookup"><span data-stu-id="4d4f1-434">Authentication file location</span></span>
<span data-ttu-id="4d4f1-435">Hello File autenticazione OMI MySQL dovrebbe essere si trova nella seguente posizione hello e nome "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="4d4f1-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="4d4f1-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="4d4f1-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="4d4f1-437">file Hello (e directory auth/omsagent) devono essere di proprietà utente omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="4d4f1-438">Log dell'agente</span><span class="sxs-lookup"><span data-stu-id="4d4f1-438">Agent logs</span></span>
<span data-ttu-id="4d4f1-439">log di Hello per hello agente OMS per Linux sono disponibili in:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="4d4f1-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="4d4f1-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="4d4f1-441">i registri di Hello per hello è agente OMS per Linux per il programma omsconfig (configurazione dell'agente) sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="4d4f1-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="4d4f1-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="4d4f1-443">Log per i componenti OMI e SCX hello (che forniscono dati di metrica di prestazioni) sono disponibili in:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="4d4f1-444">/var/opt/omi/log/ e /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="4d4f1-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="4d4f1-445">Risoluzione dei problemi di hello agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="4d4f1-446">Utilizzare hello seguente toodiagnose informazioni e risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="4d4f1-447">Se nessuna delle informazioni in questa sezione Risoluzione dei problemi di hello consente, consente inoltre hello seguenti risorse toohelp risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="4d4f1-448">I clienti con supporto tecnico Premier possono registrare un caso di supporto tramite [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="4d4f1-449">I clienti con contratti di supporto tecnico di Azure possono accedere casi di supporto in hello [portale di Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="4d4f1-450">Presentare un [problema GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="4d4f1-451">Forum di commenti e suggerimenti per idee e di un report sui bug toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="4d4f1-452">Percorsi log importanti</span><span class="sxs-lookup"><span data-stu-id="4d4f1-452">Important log locations</span></span>
| <span data-ttu-id="4d4f1-453">File</span><span class="sxs-lookup"><span data-stu-id="4d4f1-453">File</span></span> | <span data-ttu-id="4d4f1-454">Path</span><span class="sxs-lookup"><span data-stu-id="4d4f1-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="4d4f1-455">File di log dell'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="4d4f1-456">File di log di configurazione dell'agente OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="4d4f1-457">File di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="4d4f1-457">Important configuration files</span></span>
| <span data-ttu-id="4d4f1-458">Categoria</span><span class="sxs-lookup"><span data-stu-id="4d4f1-458">Catergory</span></span> | <span data-ttu-id="4d4f1-459">Percorso file</span><span class="sxs-lookup"><span data-stu-id="4d4f1-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="4d4f1-460">syslog</span><span class="sxs-lookup"><span data-stu-id="4d4f1-460">Syslog</span></span> |<span data-ttu-id="4d4f1-461">`/etc/syslog-ng/syslog-ng.conf` o `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="4d4f1-462">Output e agente generale Performance, Nagios, Zabbix e OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="4d4f1-463">Configurazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4d4f1-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="4d4f1-464">La modifica dei file di configurazione per i contatori delle prestazioni e Syslog vengono sovrascritti se è abilitata la configurazione del portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="4d4f1-465">È possibile disattivare la configurazione in hello portale di OMS (per tutti i nodi) o per singoli nodi eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="4d4f1-466">Abilitazione della registrazione di debug</span><span class="sxs-lookup"><span data-stu-id="4d4f1-466">Enable debug logging</span></span>
<span data-ttu-id="4d4f1-467">debug tooenable registrazione, è possibile utilizzare i plug-in output di hello OMS e un output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="4d4f1-468">Plug-in di output di OMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-468">OMS output plugin</span></span>
<span data-ttu-id="4d4f1-469">FluentD consente hello plug-in toospecify livelli di registrazione per i livelli di registrazione diversi per input e output.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="4d4f1-470">toospecify un livello di log diverso per l'output OMS, modificare la configurazione del agente generale hello in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="4d4f1-471">Nella parte inferiore di hello hello del file di configurazione, modificare hello `log_level` proprietà `info` troppo`debug`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="4d4f1-472">La registrazione di debug consente toosee in batch caricamenti toohello servizio OMS separandoli con un tipo, numero di elementi di dati e di tempo impiegato toosend.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="4d4f1-473">*Esempio di log abilitato per il debug:*</span><span class="sxs-lookup"><span data-stu-id="4d4f1-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="4d4f1-474">Output dettagliato</span><span class="sxs-lookup"><span data-stu-id="4d4f1-474">Verbose output</span></span>
<span data-ttu-id="4d4f1-475">Anziché utilizzare i plug-in output di hello OMS, si possono inoltre restituire gli elementi di dati direttamente troppo`stdout`, che è visibile in hello agente OMS per Linux file di log.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="4d4f1-476">Nel file di configurazione generale dell'agente OMS hello in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commento hello OMS plug-in di output aggiungendo un `#` davanti a ogni riga.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="4d4f1-477">Di seguito hello plug-in di output, rimuovere il commento hello nella seguente sezione rimuovendo hello hello `#` simbolo all'inizio di hello di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="4d4f1-478">I messaggi Syslog inoltrati non vengono visualizzati nel registro hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-479">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-479">Probable causes</span></span>
* <span data-ttu-id="4d4f1-480">Hello configurazione applicata toohello Linux server non consentono l'insieme di strutture di hello inviato e/o livelli di log</span><span class="sxs-lookup"><span data-stu-id="4d4f1-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="4d4f1-481">Syslog non è vengono inoltrati correttamente toohello Linux server</span><span class="sxs-lookup"><span data-stu-id="4d4f1-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="4d4f1-482">numero di Hello di messaggi inoltrati al secondo è troppo grande per la configurazione di base di hello agente OMS per Linux toohandle hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-483">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-483">Resolutions</span></span>
* <span data-ttu-id="4d4f1-484">Verificare che la configurazione nel portale di OMS hello hello per Syslog ha tutti i livelli di log corretto hello e le funzioni hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="4d4f1-485">**Portale OMS &gt; Impostazioni &gt; Dati &gt; Syslog**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="4d4f1-486">Verificare che syslog native messaggistica daemon (`rsyslog`, `syslog-ng`) è in grado di tooreceive messaggi hello inoltrato</span><span class="sxs-lookup"><span data-stu-id="4d4f1-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="4d4f1-487">Controllare le impostazioni del firewall su hello Syslog server tooensure che i messaggi non vengano bloccati</span><span class="sxs-lookup"><span data-stu-id="4d4f1-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="4d4f1-488">Simulare un tooOMS messaggio Syslog utilizzando hello `logger` comando - ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="4d4f1-489">Problemi di connessione tooOMS quando si utilizza un proxy</span><span class="sxs-lookup"><span data-stu-id="4d4f1-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-490">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-490">Probable causes</span></span>
* <span data-ttu-id="4d4f1-491">proxy Hello specificato quando l'installazione e configurazione agente hello è corretto</span><span class="sxs-lookup"><span data-stu-id="4d4f1-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="4d4f1-492">gli endpoint del servizio OMS Hello non sono whitelistested nel Data Center</span><span class="sxs-lookup"><span data-stu-id="4d4f1-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-493">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-493">Resolutions</span></span>
* <span data-ttu-id="4d4f1-494">Reinstallare hello agente OMS per Linux tramite comando con l'opzione hello seguente hello `-v` abilitato.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="4d4f1-495">In questo modo l'output dettagliato dell'agente di hello connessione tramite hello proxy toohello servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="4d4f1-496">Consultare la documentazione hello per proxy OMS [agente hello di configurazione per l'utilizzo con un server proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="4d4f1-497">Verificare che hello seguendo gli endpoint del servizio OMS sono inclusi</span><span class="sxs-lookup"><span data-stu-id="4d4f1-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="4d4f1-498">Risorsa agente</span><span class="sxs-lookup"><span data-stu-id="4d4f1-498">Agent Resource</span></span> | <span data-ttu-id="4d4f1-499">Porte</span><span class="sxs-lookup"><span data-stu-id="4d4f1-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="4d4f1-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="4d4f1-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="4d4f1-501">Porta 443</span><span class="sxs-lookup"><span data-stu-id="4d4f1-501">Port 443</span></span> |
| <span data-ttu-id="4d4f1-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="4d4f1-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="4d4f1-503">Porta 443</span><span class="sxs-lookup"><span data-stu-id="4d4f1-503">Port 443</span></span> |
| <span data-ttu-id="4d4f1-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="4d4f1-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="4d4f1-505">Porta 443</span><span class="sxs-lookup"><span data-stu-id="4d4f1-505">Port 443</span></span> |
| <span data-ttu-id="4d4f1-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="4d4f1-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="4d4f1-507">Porta 443</span><span class="sxs-lookup"><span data-stu-id="4d4f1-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="4d4f1-508">Viene visualizzato un messaggio di errore 403 durante il caricamento</span><span class="sxs-lookup"><span data-stu-id="4d4f1-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-509">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-509">Probable causes</span></span>
* <span data-ttu-id="4d4f1-510">hello data e ora non sono corrette nel Linux Server</span><span class="sxs-lookup"><span data-stu-id="4d4f1-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="4d4f1-511">Hello ID area di lavoro e la chiave dell'area di lavoro non sono corrette</span><span class="sxs-lookup"><span data-stu-id="4d4f1-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="4d4f1-512">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="4d4f1-512">Resolution</span></span>
* <span data-ttu-id="4d4f1-513">Verificare ora hello del server Linux con hello `date` comando.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="4d4f1-514">Se hello sono maggiori di dati o meno di 15 minuti da hello ora corrente, caricamento ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="4d4f1-515">toocorrect, aggiornare data hello e/o fuso orario del server Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="4d4f1-516">versione più recente di Hello di hello agente OMS per Linux che informa se l'errore di caricamento causa una differenza di tempo</span><span class="sxs-lookup"><span data-stu-id="4d4f1-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="4d4f1-517">Eseguire il re-caricamento tramite hello ID area di lavoro corretto e la chiave dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="4d4f1-518">Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="4d4f1-519">Viene visualizzato un errore 500 o errore 404 nel file di log hello dopo il caricamento</span><span class="sxs-lookup"><span data-stu-id="4d4f1-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="4d4f1-520">Si tratta di un problema noto che si verifica durante il primo caricamento hello dei dati di Linux in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="4d4f1-521">Questo non influisce sui dati inviati o su altri problemi.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="4d4f1-522">È possibile ignorare gli errori di hello quando inizialmente onboarding.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="4d4f1-523">Nagios dati non viene visualizzato nel portale di OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-524">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-524">Probable causes</span></span>
* <span data-ttu-id="4d4f1-525">Hello omsagent utente non dispone delle autorizzazioni tooread da file di log Nagios hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="4d4f1-526">sezioni di filtro e Hello Nagios origine sono ancora impostati come commenti file omsagent. conf hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-527">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-527">Resolutions</span></span>
* <span data-ttu-id="4d4f1-528">Aggiungere l'utente omsagent hello in ordine tooread dal file Nagios hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="4d4f1-529">Per maggiori informazioni, vedere [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Avvisi di Nagios).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="4d4f1-530">In hello agente OMS per il file di configurazione generale di Linux in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, assicurarsi che **entrambi** hello Nagios sezioni di origine e di filtro sono commenti rimossi, simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="4d4f1-531">I dati di Linux non viene visualizzato nel portale di OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-532">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-532">Probable causes</span></span>
* <span data-ttu-id="4d4f1-533">Errore del servizio di OMS toohello Onboarding</span><span class="sxs-lookup"><span data-stu-id="4d4f1-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="4d4f1-534">Connessione toohello servizio OMS è bloccato</span><span class="sxs-lookup"><span data-stu-id="4d4f1-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="4d4f1-535">Hello agente OMS per Linux dati viene eseguito il backup</span><span class="sxs-lookup"><span data-stu-id="4d4f1-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-536">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-536">Resolutions</span></span>
* <span data-ttu-id="4d4f1-537">Verificare che toohello onboarding servizio OMS ha avuto esito positivo, verificando che hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` esiste.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="4d4f1-538">Eseguire il re-caricamento tramite hello omsadmin.sh della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="4d4f1-539">Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="4d4f1-540">Se si utilizza un proxy, utilizzare hello proxy sulla risoluzione dei problemi passaggi precedente</span><span class="sxs-lookup"><span data-stu-id="4d4f1-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="4d4f1-541">In alcuni casi, quando l'agente OMS per Linux hello può comunicare con il servizio OMS, hello dati hello agente sono toohello backup buffer completo dimensioni pari a 50 MB.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="4d4f1-542">Riavviare hello agente OMS per Linux eseguendo hello `/opt/microsoft/omsagent/bin/service_control restart` comando.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="4d4f1-543">Il problema è risolto nell'agente versione 1.1.0-28 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="4d4f1-544">Configurazione del contatore delle prestazioni Syslog Linux non viene applicato nel portale OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-545">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-545">Probable causes</span></span>
* <span data-ttu-id="4d4f1-546">agente di configurazione Hello in hello agente OMS per Linux è recuperato dal portale OMS hello configurazione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="4d4f1-547">Hello impostazioni modificate nel portale di hello non sono state applicate</span><span class="sxs-lookup"><span data-stu-id="4d4f1-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-548">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-548">Resolutions</span></span>
<span data-ttu-id="4d4f1-549">`omsconfig`è l'agente di configurazione hello in hello agente OMS per Linux che recupera le modifiche di configurazione del portale di OMS ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="4d4f1-550">Questa configurazione viene quindi applicato toohello agente OMS per Linux i file di configurazione si trova in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="4d4f1-551">In alcuni casi, hello agente OMS per Linux agente di configurazione potrebbe non essere in grado di toocommunicate con il servizio di configurazione del portale hello risultante nella configurazione più recente non vengono applicati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="4d4f1-552">Verificare che hello `omsconfig` agente viene installato con l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="4d4f1-553">`dpkg --list omsconfig` oppure `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="4d4f1-554">Se non è installato, è possibile reinstallare hello versione hello agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="4d4f1-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="4d4f1-555">Verificare che hello `omsconfig` agente possa comunicare con il servizio OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="4d4f1-556">Eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="4d4f1-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="4d4f1-557">Hello comando precedente restituisce hello configurazione che l'agente recupera dal portale di hello, incluse le impostazioni di registro di sistema, i contatori delle prestazioni di Linux e i log personalizzati</span><span class="sxs-lookup"><span data-stu-id="4d4f1-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="4d4f1-558">Se il comando hello precedente non riesce, eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="4d4f1-559">Il comando forza hello omsconfig sono disponibili agenti toocommunicate con configurazione più recente di hello OMS servizio tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="4d4f1-560">Dati di log personalizzato Linux non viene visualizzato nel portale di OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="4d4f1-561">Possibili cause</span><span class="sxs-lookup"><span data-stu-id="4d4f1-561">Probable causes</span></span>
* <span data-ttu-id="4d4f1-562">Errore del servizio di caricamento tooOMS</span><span class="sxs-lookup"><span data-stu-id="4d4f1-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="4d4f1-563">Hello **hello applica seguente toomy configurazione server Linux** impostazione non è stata selezionata.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="4d4f1-564">non sono selezionato omsconfig sono disponibili log personalizzato hello più recente dal portale hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="4d4f1-565">Hello `omsagent` utilizzo è log personalizzato di hello tooaccess Impossibile a causa di problemi relativi alle autorizzazioni tooa o `omsagent` non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="4d4f1-566">In questo caso, si noterà hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="4d4f1-567">Si tratta di un problema noto con hello Race Condition che è stato risolto in hello agente OMS per Linux versione 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="4d4f1-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="4d4f1-568">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="4d4f1-568">Resolutions</span></span>
* <span data-ttu-id="4d4f1-569">Verificare di aver correttamente caricato, determinando se hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file esista.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="4d4f1-570">Se necessario, caricare nuovamente tramite riga di comando omsadmin.sh hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="4d4f1-571">Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="4d4f1-572">In hello portale di OMS, in **impostazioni** su hello **dati** scheda, verificare che hello **hello applica seguente toomy configurazione server Linux** impostazione è selezionata</span><span class="sxs-lookup"><span data-stu-id="4d4f1-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="4d4f1-573">![applicazione della configurazione](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="4d4f1-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="4d4f1-574">Verificare che hello `omsconfig` agente possa comunicare con il servizio OMS hello</span><span class="sxs-lookup"><span data-stu-id="4d4f1-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="4d4f1-575">Eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="4d4f1-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="4d4f1-576">Hello comando precedente restituisce hello configurazione che l'agente recupera dal hello portale, incluse le impostazioni di registro di sistema, i contatori delle prestazioni di Linux e i log personalizzati</span><span class="sxs-lookup"><span data-stu-id="4d4f1-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="4d4f1-577">Se il comando hello precedente non riesce, eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="4d4f1-578">Questo comando forza hello omsconfig sono disponibili agenti toocommunicate con il servizio OMS e recuperare la configurazione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="4d4f1-579">Anziché hello agente OMS per l'utente di Linux in esecuzione come utente con privilegi `root`, hello agente OMS per Linux viene eseguito come hello `omsagent` utente.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="4d4f1-580">Nella maggior parte dei casi, è necessario l'autorizzazione esplicita concessi all'utente di toohello in ordine tooread determinati file.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="4d4f1-581">autorizzazione toogrant troppo`omsagent` utente, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="4d4f1-582">Aggiungere hello `omsagent` gruppo specifico di utenti tooa con`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="4d4f1-583">File necessario concedere l'accesso in lettura universale toohello con`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="4d4f1-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="4d4f1-584">Si verifica un problema noto con hello Race Condition che è stato risolto in hello agente OMS per Linux versione 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="4d4f1-585">Dopo aver aggiornato toohello più recenti dell'agente, eseguire hello comando tooget hello più recente del plug-in output di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d4f1-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="4d4f1-586">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="4d4f1-586">Known limitations</span></span>
<span data-ttu-id="4d4f1-587">Esaminare hello seguenti sezioni toolearn sulle limitazioni attuali di hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="4d4f1-588">Diagnostica Azure</span><span class="sxs-lookup"><span data-stu-id="4d4f1-588">Azure Diagnostics</span></span>
<span data-ttu-id="4d4f1-589">Per le macchine virtuali Linux in esecuzione in Azure, ulteriori passaggi potrebbero essere necessario tooallow la raccolta dei dati da diagnostica di Azure e Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="4d4f1-590">**La versione 2.2** di hello estensione diagnostica per Linux è necessaria per la compatibilità con hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="4d4f1-591">Per ulteriori informazioni sull'installazione e configurazione di hello estensione diagnostica per Linux, vedere [utilizzare hello Azure CLI comando tooenable estensione diagnostica per Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="4d4f1-592">**Aggiornamento hello estensione di diagnostica per Linux da too2.2 2.0 di ASM CLI di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="4d4f1-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="4d4f1-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="4d4f1-594">Questi esempi di comando fanno riferimento a un file denominato PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="4d4f1-595">formato di Hello del file dovrebbe essere simile a hello seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="4d4f1-596">Sysklog non è supportato.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-596">Sysklog is not supported</span></span>
<span data-ttu-id="4d4f1-597">Rsyslog o syslog-ng sono necessari toocollect messaggi syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="4d4f1-598">il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="4d4f1-599">dati di syslog toocollect da questa versione di queste distribuzioni, hello rsyslog daemon deve essere installato e configurato tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="4d4f1-600">Per ulteriori informazioni sulla sostituzione di sysklog con rsyslog, vedere [installare il RPM rsyslog creato di recente hello](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="4d4f1-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d4f1-601">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d4f1-601">Next Steps</span></span>
* <span data-ttu-id="4d4f1-602">[Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="4d4f1-603">Acquisire familiarità con [log ricerche](log-analytics-log-searches.md) tooview dettagliate informazioni raccolte da soluzioni.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="4d4f1-604">Utilizzare [dashboard](log-analytics-dashboards.md) toosave e la visualizzazione ricerca personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4d4f1-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
