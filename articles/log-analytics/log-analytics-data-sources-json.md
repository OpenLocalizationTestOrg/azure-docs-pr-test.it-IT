---
title: Raccolta di dati JSON personalizzati in Log Analytics di OMS | Microsoft Docs
description: "È possibile raccogliere origini dati JSON personalizzate in Log Analytics tramite l'agente OMS per Linux.  Queste origini dati personalizzate possono essere semplici script che restituiscono JSON, ad esempio curl, o uno degli oltre 300 plug-in di FluentD. Questo articolo descrive la configurazione necessaria per questa raccolta di dati."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="051dd-105">Raccolta di origini dati JSON personalizzate con l'agente OMS per Linux in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="051dd-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="051dd-106">È possibile raccogliere origini dati JSON personalizzate in Log Analytics tramite l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="051dd-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="051dd-107">Queste origini dati personalizzate possono essere semplici script che restituiscono JSON, ad esempio [curl](https://curl.haxx.se/), o uno degli oltre [300 plug-in di FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="051dd-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="051dd-108">Questo articolo descrive la configurazione necessaria per questa raccolta di dati.</span><span class="sxs-lookup"><span data-stu-id="051dd-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="051dd-109">Per i dati JSON personalizzati è necessario l'agente OMS per Linux v1.1.0-217+</span><span class="sxs-lookup"><span data-stu-id="051dd-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="051dd-110">Configurazione</span><span class="sxs-lookup"><span data-stu-id="051dd-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="051dd-111">Configurare il plug-in di input</span><span class="sxs-lookup"><span data-stu-id="051dd-111">Configure input plugin</span></span>

<span data-ttu-id="051dd-112">Per raccogliere dati JSON in Log Analytics, aggiungere `oms.api.` all'inizio di un tag FluentD in un plug-in di input.</span><span class="sxs-lookup"><span data-stu-id="051dd-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="051dd-113">Di seguito, ad esempio, è riportato un file di configurazione separato `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="051dd-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="051dd-114">Viene usato il plug-in FluentD `exec` per eseguire un comando curl ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="051dd-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="051dd-115">L'output di questo comando viene raccolto dal plug-in di output JSON.</span><span class="sxs-lookup"><span data-stu-id="051dd-115">The output from this command is collected by the JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="051dd-116">Per il file di configurazione aggiunto in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` sarà necessario modificare la proprietà con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="051dd-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="051dd-117">Configurare il plug-in di output</span><span class="sxs-lookup"><span data-stu-id="051dd-117">Configure output plugin</span></span> 
<span data-ttu-id="051dd-118">Aggiungere la configurazione del plug-in di output seguente alla configurazione principale presente in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o come un file di configurazione separato inserito in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="051dd-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="051dd-119">Riavviare l'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="051dd-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="051dd-120">Riavviare l'agente OMS per il servizio Linux con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="051dd-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="051dd-121">Output</span><span class="sxs-lookup"><span data-stu-id="051dd-121">Output</span></span>
<span data-ttu-id="051dd-122">I dati verranno raccolti in Log Analytics con un record di tipo `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="051dd-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="051dd-123">Il tag personalizzato `tag oms.api.tomcat` in Log Analytics, ad esempio, viene raccolto con un record di tipo `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="051dd-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="051dd-124">È possibile recuperare tutti i record di questo tipo con la ricerca log seguente.</span><span class="sxs-lookup"><span data-stu-id="051dd-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="051dd-125">Sono supportate anche origini dati JSON annidate, che tuttavia vengono indicizzate in base al campo padre.</span><span class="sxs-lookup"><span data-stu-id="051dd-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="051dd-126">I dati JSON seguenti, ad esempio, vengono restituiti da una ricerca di Log Analytics come `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="051dd-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="051dd-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="051dd-127">Next steps</span></span>
* <span data-ttu-id="051dd-128">Informazioni sulle [ricerche nei log](log-analytics-log-searches.md) per analizzare i dati raccolti dalle origini dati e dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="051dd-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 