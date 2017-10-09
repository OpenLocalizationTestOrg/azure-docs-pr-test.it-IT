---
title: gli avvisi Nagios e Zabbix aaaCollect in OMS Log Analitica | Documenti Microsoft
description: "Nagios e Zabbix sono strumenti di monitoraggio open source. È possibile raccogliere gli avvisi da questi strumenti in Analitica di Log in ordine tooanalyze li insieme gli avvisi generati da altre origini.  In questo articolo viene descritto come tooconfigure hello agente OMS per Linux toocollect avvisi da questi sistemi."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Raccogliere avvisi da Nagios e Zabbix in Log Analytics tramite l'agente OMS per Linux 
[Nagios](https://www.nagios.org/) e [Zabbix](http://www.zabbix.com/) sono strumenti di monitoraggio open source.  È possibile raccogliere gli avvisi da questi strumenti in Analitica di Log in ordine tooanalyze lungo con [gli avvisi generati da altre origini](log-analytics-alerts.md).  In questo articolo viene descritto come tooconfigure hello agente OMS per Linux toocollect avvisi da questi sistemi.
 
## <a name="configure-alert-collection"></a>Configurare la raccolta di avvisi

### <a name="configuring-nagios-alert-collection"></a>Configurazione della raccolta di avvisi Nagios
Eseguire operazioni sugli avvisi di toocollect server Nagios hello hello.

1. Concedere all'utente di hello **omsagent** file di log Nagios toohello accesso in lettura (ad esempio `/var/log/nagios/nagios.log`). Supponendo che i file nagios.log hello è di proprietà di gruppo hello `nagios`, è possibile aggiungere l'utente hello **omsagent** toohello **nagios** gruppo. 

    sudo usermod -a -G nagios omsagent

2.  Modificare i file di configurazione hello (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Verificare che siano presenti e non come commento hello seguenti voci:  

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

3. Riavviare i daemon omsagent hello

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Configurazione della raccolta di avvisi Zabbix
toocollect gli avvisi da un server Zabbix, è necessario toospecify un utente e password in *cancellare il testo*. Non è ideale, ma è consigliabile creare hello utente e concedere le autorizzazioni toomonitor onlu.

Eseguire operazioni sugli avvisi di toocollect server Nagios hello hello.

1. Modificare i file di configurazione hello (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Verificare hello voci seguenti siano presenti e non impostate come commento.  Modificare toovalues hello utente nome e una password per l'ambiente Zabbix.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Riavviare i daemon omsagent hello

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>Record di avvisi
È possibile recuperare record di avvisi da Nagios e Zabbix usando le [ricerche log](log-analytics-log-searches.md) in Log Analytics.

### <a name="nagios-alert-records"></a>Record di avvisi Nagios

Nei record di avvisi raccolti da Nagios, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Nagios**.  Presentano proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*Avviso* |
| SourceSystem |*Nagios* |
| AlertName |Nome dell'avviso hello. |
| AlertDescription | Descrizione dell'avviso hello. |
| AlertState | Stato del servizio hello o dell'host.<br><br>OK<br>WARNING<br>UP<br>DOWN |
| HostName | Nome dell'host hello creati avviso hello. |
| PriorityNumber | Livello di priorità dell'avviso hello. |
| StateType | tipo di Hello dello stato di avviso hello.<br><br>SOFT: problema che non è stato ricontrollato.<br>HARD: problema che è stata ricontrollato un determinato numero di volte.  |
| TimeGenerated |Data e ora avviso hello è stato creato. |


### <a name="zabbix-alert-records"></a>Record di avvisi Zabbix
Nei record di avvisi raccolti da Zabbix, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Zabbix**.  Presentano proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*Avviso* |
| SourceSystem |*Zabbix* |
| AlertName | Nome dell'avviso hello. |
| AlertPriority | Gravità dell'avviso hello.<br><br>non classificata<br>Informazioni<br>Avviso<br>average<br>elevata<br>emergenza  |
| AlertState | Stato di avviso hello.<br><br>0 - lo stato è backup toodate.<br>1: stato sconosciuto.  |
| AlertTypeNumber | Specifica se l'avviso può generare più eventi relativi a problemi.<br><br>0 - lo stato è backup toodate.<br>1: stato sconosciuto.    |
| Commenti | Commenti aggiuntivi per l'avviso. |
| HostName | Nome dell'host hello creati avviso hello. |
| PriorityNumber | Valore che indica la gravità dell'avviso hello.<br><br>0: non classificata<br>1: informazioni<br>2: avviso<br>3: media<br>4: elevata<br>5: emergenza |
| TimeGenerated |Data e ora avviso hello è stato creato. |
| TimeLastModified |Ultima modifica dello stato di hello data e ora dell'avviso hello. |


## <a name="next-steps"></a>Passaggi successivi
* Informazioni sugli [avvisi](log-analytics-alerts.md) in Log Analytics.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni. 
