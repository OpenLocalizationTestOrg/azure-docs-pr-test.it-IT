---
title: Raccogliere dati da CollectD in Log Analytics di OMS | Microsoft Docs
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="2739f-104">Raccogliere dati da CollectD su agenti Linux in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2739f-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="2739f-105">[CollectD](https://collectd.org/) è un daemon Linux open source che, a intervalli regolari, raccoglie metriche sulle prestazioni dalle applicazioni e informazioni a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="2739f-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="2739f-106">Applicazioni di esempio includono Java Virtual Machine (JVM), MySQL Server e Nginx.</span><span class="sxs-lookup"><span data-stu-id="2739f-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="2739f-107">Questo articolo fornisce informazioni sulla raccolta di dati sulle prestazioni da CollectD in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2739f-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="2739f-108">Un elenco completo dei plug-in disponibili è contenuto nella [Tabella dei plug-in](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="2739f-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Panoramica di CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="2739f-110">Nell'agente OMS per Linux è inclusa la configurazione di CollectD seguente per indirizzare dati CollectD all'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="2739f-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="2739f-111">Se si usa una versione di CollectD precedente a 5.5, adottare invece la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="2739f-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="2739f-112">La configurazione di CollectD usa il plug-in predefinito `write_http` per inviare dati delle metriche sulle prestazioni all'agente OMS per Linux tramite la porta 26000.</span><span class="sxs-lookup"><span data-stu-id="2739f-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="2739f-113">Se necessario, questa porta può essere configurata su una porta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2739f-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="2739f-114">L'agente OMS per Linux resta in ascolto delle metriche di CollectD sulla porta 26000 e le converte anche in metriche per lo schema OMS.</span><span class="sxs-lookup"><span data-stu-id="2739f-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="2739f-115">Di seguito è illustrata la configurazione dell'agente OMS per Linux `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="2739f-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="2739f-116">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="2739f-116">Versions supported</span></span>
- <span data-ttu-id="2739f-117">Log Analytics supporta attualmente CollectD versione 4.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2739f-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="2739f-118">Per la raccolta di metriche CollectD è necessario l'agente OMS per Linux v1.1.0-217 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2739f-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="2739f-119">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2739f-119">Configuration</span></span>
<span data-ttu-id="2739f-120">Di seguito è riportata la procedura di base per configurare la raccolta di dati CollectD in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2739f-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="2739f-121">Configurare CollectD per l'invio di dati all'agente OMS per Linux con il plug-in write_http.</span><span class="sxs-lookup"><span data-stu-id="2739f-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="2739f-122">Configurare l'agente OMS per Linux restare in ascolto dei dati di CollectD sulla porta appropriata.</span><span class="sxs-lookup"><span data-stu-id="2739f-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="2739f-123">Riavviare CollectD e l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="2739f-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="2739f-124">Configurare CollectD per l'inoltro di dati</span><span class="sxs-lookup"><span data-stu-id="2739f-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="2739f-125">Per indirizzare dati di CollectD all'agente OMS per Linux, è necessario che `oms.conf` sia stato aggiunto alla directory di configurazione di CollectD.</span><span class="sxs-lookup"><span data-stu-id="2739f-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="2739f-126">La destinazione di questo file dipende dalla distribuzione di Linux presente sul computer.</span><span class="sxs-lookup"><span data-stu-id="2739f-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="2739f-127">Se la directory di configurazione di CollectD si trova in /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="2739f-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="2739f-128">Se la directory di configurazione di CollectD si trova in /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="2739f-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="2739f-129">Per versioni di CollectD antecedenti a 5.5, è necessario modificare i tag in `oms.conf`, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2739f-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="2739f-130">Copiare collectd.conf nella directory di configurazione di omsagent dell'area di lavoro desiderata.</span><span class="sxs-lookup"><span data-stu-id="2739f-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="2739f-131">Riavviare CollectD e l'agente OMS per Linux con i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2739f-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="2739f-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="2739f-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="2739f-133">Conversione dello schema di metriche di CollectD nello schema di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2739f-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="2739f-134">Per mantenere un modello comune tra le metriche dell'infrastruttura già raccolte dall'agente OMS per Linux e le nuove metriche raccolte da CollectD, viene usato lo schema di mapping seguente:</span><span class="sxs-lookup"><span data-stu-id="2739f-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="2739f-135">Campo metrica CollectD</span><span class="sxs-lookup"><span data-stu-id="2739f-135">CollectD Metric field</span></span> | <span data-ttu-id="2739f-136">Campo Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2739f-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="2739f-137">host</span><span class="sxs-lookup"><span data-stu-id="2739f-137">host</span></span> | <span data-ttu-id="2739f-138">Computer</span><span class="sxs-lookup"><span data-stu-id="2739f-138">Computer</span></span> |
| <span data-ttu-id="2739f-139">plugin</span><span class="sxs-lookup"><span data-stu-id="2739f-139">plugin</span></span> | <span data-ttu-id="2739f-140">Nessuno</span><span class="sxs-lookup"><span data-stu-id="2739f-140">None</span></span> |
| <span data-ttu-id="2739f-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="2739f-141">plugin_instance</span></span> | <span data-ttu-id="2739f-142">Nome dell'istanza</span><span class="sxs-lookup"><span data-stu-id="2739f-142">Instance Name</span></span><br><span data-ttu-id="2739f-143">Se **plugin_instance** è *null*, InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="2739f-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="2739f-144">type</span><span class="sxs-lookup"><span data-stu-id="2739f-144">type</span></span> | <span data-ttu-id="2739f-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="2739f-145">ObjectName</span></span> |
| <span data-ttu-id="2739f-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="2739f-146">type_instance</span></span> | <span data-ttu-id="2739f-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="2739f-147">CounterName</span></span><br><span data-ttu-id="2739f-148">Se **type_instance** è *null*, CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="2739f-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="2739f-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="2739f-149">dsnames[]</span></span> | <span data-ttu-id="2739f-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="2739f-150">CounterName</span></span> |
| <span data-ttu-id="2739f-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="2739f-151">dstypes</span></span> | <span data-ttu-id="2739f-152">Nessuno</span><span class="sxs-lookup"><span data-stu-id="2739f-152">None</span></span> |
| <span data-ttu-id="2739f-153">values[]</span><span class="sxs-lookup"><span data-stu-id="2739f-153">values[]</span></span> | <span data-ttu-id="2739f-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="2739f-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2739f-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2739f-155">Next steps</span></span>
* <span data-ttu-id="2739f-156">Informazioni sulle [ricerche nei log](log-analytics-log-searches.md) per analizzare i dati raccolti dalle origini dati e dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="2739f-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="2739f-157">Usare [campi personalizzati](log-analytics-custom-fields.md) per analizzare i dati dei record Syslog nei singoli campi.</span><span class="sxs-lookup"><span data-stu-id="2739f-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

