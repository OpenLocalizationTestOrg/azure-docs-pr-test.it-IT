---
title: dati JSON personalizzato aaaCollecting in OMS Log Analitica | Documenti Microsoft
description: Origini di dati JSON personalizzati possono essere raccolti nel Log Analitica utilizzando hello agente OMS per Linux.  Queste origini dati personalizzate possono essere semplici script che restituiscono JSON, ad esempio curl, o uno degli oltre 300 plug-in di FluentD. Questo articolo descrive configurazione hello necessaria per questa raccolta di dati.
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="a5f55-105">Raccolta di origini di dati JSON personalizzate con hello agente OMS per Linux nel Log Analitica</span><span class="sxs-lookup"><span data-stu-id="a5f55-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="a5f55-106">Origini di dati JSON personalizzati possono essere raccolti nel Log Analitica utilizzando hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="a5f55-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="a5f55-107">Queste origini dati personalizzate possono essere semplici script che restituiscono JSON, ad esempio [curl](https://curl.haxx.se/), o uno degli oltre [300 plug-in di FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="a5f55-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="a5f55-108">Questo articolo descrive configurazione hello necessaria per questa raccolta di dati.</span><span class="sxs-lookup"><span data-stu-id="a5f55-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f55-109">Per i dati JSON personalizzati è necessario l'agente OMS per Linux v1.1.0-217+</span><span class="sxs-lookup"><span data-stu-id="a5f55-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="a5f55-110">Configurazione</span><span class="sxs-lookup"><span data-stu-id="a5f55-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="a5f55-111">Configurare il plug-in di input</span><span class="sxs-lookup"><span data-stu-id="a5f55-111">Configure input plugin</span></span>

<span data-ttu-id="a5f55-112">aggiungere i dati JSON toocollect nel Log Analitica, `oms.api.` toohello inizio di un tag FluentD in un plug-in di input.</span><span class="sxs-lookup"><span data-stu-id="a5f55-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="a5f55-113">Di seguito, ad esempio, è riportato un file di configurazione separato `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="a5f55-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="a5f55-114">Questo metodo utilizza plug-in di hello FluentD `exec` toorun un comando curl ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="a5f55-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="a5f55-115">output di Hello da questo comando viene raccolto dal plug-in output di hello JSON.</span><span class="sxs-lookup"><span data-stu-id="a5f55-115">hello output from this command is collected by hello JSON output plugin.</span></span>

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
<span data-ttu-id="a5f55-116">aggiunto in file di configurazione di Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` richiederà toohave della proprietà modificata con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a5f55-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="a5f55-117">Configurare il plug-in di output</span><span class="sxs-lookup"><span data-stu-id="a5f55-117">Configure output plugin</span></span> 
<span data-ttu-id="a5f55-118">Aggiungere hello output plug-in configurazione toohello configurazione principale in seguito `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o come un file di configurazione separato inserito`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="a5f55-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="a5f55-119">Riavviare l'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="a5f55-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="a5f55-120">Riavviare hello agente OMS per Linux servizio con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a5f55-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="a5f55-121">Output</span><span class="sxs-lookup"><span data-stu-id="a5f55-121">Output</span></span>
<span data-ttu-id="a5f55-122">verranno raccolti i dati di Hello in Log Analitica con un tipo di record `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="a5f55-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="a5f55-123">Ad esempio, hello tag personalizzato `tag oms.api.tomcat` nel Log Analitica con un tipo di record `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="a5f55-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="a5f55-124">È possibile recuperare tutti i record di questo tipo con hello ricerca nei log seguente.</span><span class="sxs-lookup"><span data-stu-id="a5f55-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="a5f55-125">Sono supportate anche origini dati JSON annidate, che tuttavia vengono indicizzate in base al campo padre.</span><span class="sxs-lookup"><span data-stu-id="a5f55-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="a5f55-126">Ad esempio, hello segue i dati JSON viene restituito da una ricerca Log Analitica come `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="a5f55-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="a5f55-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5f55-127">Next steps</span></span>
* <span data-ttu-id="a5f55-128">Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="a5f55-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 