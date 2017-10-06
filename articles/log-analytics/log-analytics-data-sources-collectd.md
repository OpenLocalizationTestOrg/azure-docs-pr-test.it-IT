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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Raccogliere dati da CollectD su agenti Linux in Log Analytics
[CollectD](https://collectd.org/) è un daemon Linux open source che, a intervalli regolari, raccoglie metriche sulle prestazioni dalle applicazioni e informazioni a livello di sistema. Applicazioni di esempio includono Nginx hello Java Virtual Machine (JVM) e il MySQL Server. Questo articolo fornisce informazioni sulla raccolta di dati sulle prestazioni da CollectD in Log Analytics.

Un elenco completo dei plug-in disponibili è contenuto nella [Tabella dei plug-in](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Panoramica di CollectD](media/log-analytics-data-sources-collectd/overview.png)

Hello configurazione CollectD seguente è incluso in hello agente OMS per Linux tooroute CollectD dati toohello agente OMS per Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Inoltre, se si utilizza un versioni collectD prima 5.5 hello seguente configurazione invece di utilizzare.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

configurazione CollectD Hello Usa predefinito hello`write_http` plug-in toosend prestazioni dati di metrica sulla porta 26000 tooOMS agente per Linux. 

> [!NOTE]
> Questa porta può essere configurato tooa personalizzato porta, se necessario.

Hello agente OMS per Linux inoltre in ascolto sulla porta 26000 per le metriche CollectD e quindi li converte tooOMS metriche di schema. esempio Hello è hello agente OMS per Linux configurazione `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Versioni supportate
- Log Analytics supporta attualmente CollectD versione 4.8 e versioni successive.
- Per la raccolta di metriche CollectD è necessario l'agente OMS per Linux v1.1.0-217 o versione successiva.


## <a name="configuration"></a>Configurazione
di seguito Hello sono raccolta tooconfigure passaggi di base dei dati CollectD nel Log Analitica.

1. Configurare CollectD toosend dati toohello agente OMS per Linux tramite plug-in write_http hello.  
2. Configurare hello agente OMS per Linux toolisten per hello CollectD dati sulla porta appropriata hello.
3. Riavviare CollectD e l'agente OMS per Linux.

### <a name="configure-collectd-tooforward-data"></a>Configurare CollectD tooforward dati 

1. tooroute CollectD dati toohello agente OMS per Linux, `oms.conf` toobe esigenze aggiunta directory di configurazione del tooCollectD. destinazione Hello di questo file dipende dalla distribuzione Linux hello del computer.

    Se la directory di configurazione di CollectD si trova in /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Se la directory di configurazione di CollectD si trova in /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Per le versioni CollectD precedenti 5.5 è tag hello toomodify in `oms.conf` come illustrato in precedenza.
    >

2. Copiare la directory di configurazione omsagent dell'area di lavoro collectd.conf toohello desiderato.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Riavviare CollectD e l'agente OMS per Linux con hello i comandi seguenti.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD metriche tooLog conversione degli schemi Analitica
toomaintain un comune modello tra le metriche delle infrastrutture già raccolti dall'agente OMS per Linux e hello nuova metrica raccolte CollectD hello seguente mapping dello schema viene utilizzato:

| Campo metrica CollectD | Campo Log Analytics |
|:--|:--|
| host | Computer |
| plugin | Nessuno |
| plugin_instance | Nome dell'istanza<br>Se **plugin_instance** è *null*, InstanceName="*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>Se **type_instance** è *null*, CounterName=**blank** |
| dsnames[] | CounterName |
| dstypes | Nessuno |
| values[] | CounterValue |

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni. 
* Utilizzare [campi personalizzati](log-analytics-custom-fields.md) tooparse dati da record syslog in singoli campi.

