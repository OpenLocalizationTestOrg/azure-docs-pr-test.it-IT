---
title: dati aaaCollect da CollectD in OMS Log Analitica | Documenti Microsoft
description: "CollectD è un daemon Linux open source che, a intervalli regolari, raccoglie dati dalle applicazioni e informazioni a livello di sistema.  Questo articolo fornisce informazioni sulla raccolta di dati da CollectD in Log Analytics."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="f2634-104">Raccogliere dati da CollectD su agenti Linux in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2634-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="f2634-105">[CollectD](https://collectd.org/) è un daemon Linux open source che, a intervalli regolari, raccoglie metriche sulle prestazioni dalle applicazioni e informazioni a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="f2634-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="f2634-106">Applicazioni di esempio includono Nginx hello Java Virtual Machine (JVM) e il MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="f2634-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="f2634-107">Questo articolo fornisce informazioni sulla raccolta di dati sulle prestazioni da CollectD in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2634-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="f2634-108">Un elenco completo dei plug-in disponibili è contenuto nella [Tabella dei plug-in](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="f2634-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Panoramica di CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="f2634-110">Hello configurazione CollectD seguente è incluso in hello agente OMS per Linux tooroute CollectD dati toohello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="f2634-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="f2634-111">Inoltre, se si utilizza un versioni collectD prima 5.5 hello seguente configurazione invece di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="f2634-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="f2634-112">configurazione CollectD Hello Usa predefinito hello`write_http` plug-in toosend prestazioni dati di metrica sulla porta 26000 tooOMS agente per Linux.</span><span class="sxs-lookup"><span data-stu-id="f2634-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="f2634-113">Questa porta può essere configurato tooa personalizzato porta, se necessario.</span><span class="sxs-lookup"><span data-stu-id="f2634-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="f2634-114">Hello agente OMS per Linux inoltre in ascolto sulla porta 26000 per le metriche CollectD e quindi li converte tooOMS metriche di schema.</span><span class="sxs-lookup"><span data-stu-id="f2634-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="f2634-115">esempio Hello è hello agente OMS per Linux configurazione `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="f2634-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="f2634-116">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="f2634-116">Versions supported</span></span>
- <span data-ttu-id="f2634-117">Log Analytics supporta attualmente CollectD versione 4.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="f2634-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="f2634-118">Per la raccolta di metriche CollectD è necessario l'agente OMS per Linux v1.1.0-217 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f2634-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="f2634-119">Configurazione</span><span class="sxs-lookup"><span data-stu-id="f2634-119">Configuration</span></span>
<span data-ttu-id="f2634-120">di seguito Hello sono raccolta tooconfigure passaggi di base dei dati CollectD nel Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="f2634-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="f2634-121">Configurare CollectD toosend dati toohello agente OMS per Linux tramite plug-in write_http hello.</span><span class="sxs-lookup"><span data-stu-id="f2634-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="f2634-122">Configurare hello agente OMS per Linux toolisten per hello CollectD dati sulla porta appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="f2634-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="f2634-123">Riavviare CollectD e l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="f2634-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="f2634-124">Configurare CollectD tooforward dati</span><span class="sxs-lookup"><span data-stu-id="f2634-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="f2634-125">tooroute CollectD dati toohello agente OMS per Linux, `oms.conf` toobe esigenze aggiunta directory di configurazione del tooCollectD.</span><span class="sxs-lookup"><span data-stu-id="f2634-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="f2634-126">destinazione Hello di questo file dipende dalla distribuzione Linux hello del computer.</span><span class="sxs-lookup"><span data-stu-id="f2634-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="f2634-127">Se la directory di configurazione di CollectD si trova in /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="f2634-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="f2634-128">Se la directory di configurazione di CollectD si trova in /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="f2634-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="f2634-129">Per le versioni CollectD precedenti 5.5 è tag hello toomodify in `oms.conf` come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f2634-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="f2634-130">Copiare la directory di configurazione omsagent dell'area di lavoro collectd.conf toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="f2634-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="f2634-131">Riavviare CollectD e l'agente OMS per Linux con hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f2634-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="f2634-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="f2634-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="f2634-133">CollectD metriche tooLog conversione degli schemi Analitica</span><span class="sxs-lookup"><span data-stu-id="f2634-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="f2634-134">toomaintain un comune modello tra le metriche delle infrastrutture già raccolti dall'agente OMS per Linux e hello nuova metrica raccolte CollectD hello seguente mapping dello schema viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="f2634-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="f2634-135">Campo metrica CollectD</span><span class="sxs-lookup"><span data-stu-id="f2634-135">CollectD Metric field</span></span> | <span data-ttu-id="f2634-136">Campo Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2634-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="f2634-137">host</span><span class="sxs-lookup"><span data-stu-id="f2634-137">host</span></span> | <span data-ttu-id="f2634-138">Computer</span><span class="sxs-lookup"><span data-stu-id="f2634-138">Computer</span></span> |
| <span data-ttu-id="f2634-139">plugin</span><span class="sxs-lookup"><span data-stu-id="f2634-139">plugin</span></span> | <span data-ttu-id="f2634-140">Nessuno</span><span class="sxs-lookup"><span data-stu-id="f2634-140">None</span></span> |
| <span data-ttu-id="f2634-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="f2634-141">plugin_instance</span></span> | <span data-ttu-id="f2634-142">Nome dell'istanza</span><span class="sxs-lookup"><span data-stu-id="f2634-142">Instance Name</span></span><br><span data-ttu-id="f2634-143">Se **plugin_instance** è *null*, InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="f2634-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="f2634-144">type</span><span class="sxs-lookup"><span data-stu-id="f2634-144">type</span></span> | <span data-ttu-id="f2634-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="f2634-145">ObjectName</span></span> |
| <span data-ttu-id="f2634-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="f2634-146">type_instance</span></span> | <span data-ttu-id="f2634-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="f2634-147">CounterName</span></span><br><span data-ttu-id="f2634-148">Se **type_instance** è *null*, CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="f2634-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="f2634-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="f2634-149">dsnames[]</span></span> | <span data-ttu-id="f2634-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="f2634-150">CounterName</span></span> |
| <span data-ttu-id="f2634-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="f2634-151">dstypes</span></span> | <span data-ttu-id="f2634-152">Nessuno</span><span class="sxs-lookup"><span data-stu-id="f2634-152">None</span></span> |
| <span data-ttu-id="f2634-153">values[]</span><span class="sxs-lookup"><span data-stu-id="f2634-153">values[]</span></span> | <span data-ttu-id="f2634-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="f2634-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f2634-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2634-155">Next steps</span></span>
* <span data-ttu-id="f2634-156">Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="f2634-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="f2634-157">Utilizzare [campi personalizzati](log-analytics-custom-fields.md) tooparse dati da record syslog in singoli campi.</span><span class="sxs-lookup"><span data-stu-id="f2634-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

