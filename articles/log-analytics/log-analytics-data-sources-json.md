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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Raccolta di origini di dati JSON personalizzate con hello agente OMS per Linux nel Log Analitica
Origini di dati JSON personalizzati possono essere raccolti nel Log Analitica utilizzando hello agente OMS per Linux.  Queste origini dati personalizzate possono essere semplici script che restituiscono JSON, ad esempio [curl](https://curl.haxx.se/), o uno degli oltre [300 plug-in di FluentD](http://www.fluentd.org/plugins/all). Questo articolo descrive configurazione hello necessaria per questa raccolta di dati.

> [!NOTE]
> Per i dati JSON personalizzati è necessario l'agente OMS per Linux v1.1.0-217+

## <a name="configuration"></a>Configurazione

### <a name="configure-input-plugin"></a>Configurare il plug-in di input

aggiungere i dati JSON toocollect nel Log Analitica, `oms.api.` toohello inizio di un tag FluentD in un plug-in di input.

Di seguito, ad esempio, è riportato un file di configurazione separato `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Questo metodo utilizza plug-in di hello FluentD `exec` toorun un comando curl ogni 30 secondi.  output di Hello da questo comando viene raccolto dal plug-in output di hello JSON.

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
aggiunto in file di configurazione di Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` richiederà toohave della proprietà modificata con hello comando seguente.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configurare il plug-in di output 
Aggiungere hello output plug-in configurazione toohello configurazione principale in seguito `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o come un file di configurazione separato inserito`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Riavviare l'agente OMS per Linux
Riavviare hello agente OMS per Linux servizio con hello comando seguente.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Output
verranno raccolti i dati di Hello in Log Analitica con un tipo di record `<FLUENTD_TAG>_CL`.

Ad esempio, hello tag personalizzato `tag oms.api.tomcat` nel Log Analitica con un tipo di record `tomcat_CL`.  È possibile recuperare tutti i record di questo tipo con hello ricerca nei log seguente.

    Type=tomcat_CL

Sono supportate anche origini dati JSON annidate, che tuttavia vengono indicizzate in base al campo padre. Ad esempio, hello segue i dati JSON viene restituito da una ricerca Log Analitica come `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni. 
 