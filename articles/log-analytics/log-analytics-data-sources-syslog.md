---
title: aaaCollect e analizzare i messaggi Syslog in OMS Log Analitica | Documenti Microsoft
description: "Syslog è un protocollo di registrazione di eventi che è tooLinux comuni. In questo articolo viene descritto come raccolta tooconfigure dei messaggi Syslog in Analitica di Log e i dettagli dei record di hello che ha creato nel repository OMS hello."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Origini dati Syslog in Log Analytics
Syslog è un protocollo di registrazione di eventi che è tooLinux comuni.  Applicazioni invierà i messaggi che possono essere archiviati nel computer locale hello o recapitati tooa Syslog agente di raccolta.  Quando viene installato l'agente OMS per Linux hello, configura hello locale Syslog daemon tooforward messaggi toohello dell'agente.  agente Hello invia quindi tooLog messaggio hello Analitica in cui viene creato un record corrispondente nel repository OMS hello.  

> [!NOTE]
> Log Analitica supporta la raccolta di messaggi inviati dal rsyslog o syslog-ng, dove rsyslog è daemon predefinito hello. il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog. dati di syslog toocollect da questa versione di queste distribuzioni, hello [daemon rsyslog](http://rsyslog.com) deve essere installato e configurato tooreplace sysklog.
>
>

![Raccolta Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Configurazione di Syslog
Hello agente OMS per Linux verrà raccolti solo gli eventi con strutture di hello e livelli di gravità che vengono specificati nella configurazione.  Tramite il portale di OMS hello o mediante la gestione di file di configurazione di agenti di Linux, è possibile configurare Syslog.

### <a name="configure-syslog-in-hello-oms-portal"></a>Configurare Syslog nel portale OMS hello
Configurare Syslog da hello [menu dati nelle impostazioni di registro Analitica](log-analytics-data-sources.md#configuring-data-sources).  Questa configurazione viene recapitata toohello i file di configurazione in ogni agente Linux.

È possibile aggiungere una nuova funzionalità digitando il nome corrispondente e facendo clic su **+**.  Per ogni struttura, verranno raccolti solo i messaggi con livelli di gravità hello selezionato.  Controllare i livelli di gravità di hello per funzionalità di hello specifico che si desidera toocollect.  È possibile fornire eventuali criteri aggiuntivi toofilter messaggi.

![Configurare Syslog](media/log-analytics-data-sources-syslog/configure.png)

Per impostazione predefinita, tutte le modifiche di configurazione vengono automaticamente spostate tooall agenti.  Se si desidera tooconfigure Syslog manualmente in ogni agente Linux, quindi deselezionare la casella di hello *Apply below macchine Linux di configurazione toomy*.

### <a name="configure-syslog-on-linux-agent"></a>Configurare Syslog sull'agente Linux
Quando hello [agente OMS è installato in un client Linux](log-analytics-linux-agents.md), l'installazione di un file di configurazione di syslog predefinito che definisce la funzione hello e gravità hello messaggi che vengono raccolti.  È possibile modificare questa configurazione hello toochange di file.  file di configurazione Hello è diversa a seconda di hello Syslog daemon che hello client è installato.

> [!NOTE]
> Se si modifica la configurazione di syslog hello, è necessario riavviare i daemon syslog hello hello modifiche tootake effetto.
>
>

#### <a name="rsyslog"></a>rsyslog
Hello file di configurazione per rsyslog si trova in **/etc/rsyslog.d/95-omsagent.conf**.  I contenuti predefiniti sono visualizzati di seguito.  Consente di raccogliere i messaggi syslog inviati dall'agente locale hello per tutte le funzioni con un livello di avviso o versione successiva.

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

È possibile rimuovere una funzionalità di gestione tramite la rimozione della sezione del file di configurazione hello.  È possibile limitare i livelli di gravità di hello vengono raccolti per una particolare funzionalità modificando la voce di tale funzionalità.  Ad esempio, toolimit hello utente struttura toomessages con gravità maggiore o di errore è modificherebbe dalla riga di hello toohello di file di configurazione seguente:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
file di configurazione Hello per syslog-ng è percorso **/etc/syslog-ng/syslog-ng.conf**.  I contenuti predefiniti sono visualizzati di seguito.  Consente di raccogliere i messaggi syslog inviati dall'agente locale hello per tutte le funzioni e tutti i livelli di gravità.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

È possibile rimuovere una funzionalità di gestione tramite la rimozione della sezione del file di configurazione hello.  È possibile limitare i livelli di gravità di hello vengono raccolti per una particolare funzionalità rimuovendole dal relativo elenco.  Ad esempio, toolimit hello utente struttura toojust i messaggi di avviso e critici, è necessario modificare la sezione di hello toohello di file di configurazione seguente:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Raccolta dei dati da altre porte Syslog
agente OMS Hello è in attesa per i messaggi Syslog nel client locale di hello sulla porta 25224.  Quando viene installato l'agente di hello, una configurazione predefinita di syslog è applicata e hello seguente posizione:

* Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

È possibile modificare il numero di porta hello creando due file di configurazione: un file di configurazione FluentD e un file ng di rsyslog o syslog a seconda di daemon Syslog hello è stato installato.  

* file di configurazione FluentD Hello deve essere un nuovo file si trova: `/etc/opt/microsoft/omsagent/conf/omsagent.d` e sostituire il valore di hello in hello **porta** voce con il numero di porta personalizzato.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Per rsyslog, è necessario creare un nuovo file di configurazione si trova: `/etc/rsyslog.d/` e sostituire hello valore % SYSLOG_PORT % con il numero di porta personalizzato.  

    > [!NOTE]
    > Se si modifica questo valore nel file di configurazione hello `95-omsagent.conf`, verrà sovrascritto quando l'agente di hello applica una configurazione predefinita.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello syslog-ng configurazione deve essere modificato tramite la copia di configurazione di esempio hello illustrato di seguito e aggiunta hello personalizzate impostazioni modificate toohello fine del file di configurazione di syslog ng.conf hello nella `/etc/syslog-ng/`.  Eseguire **non** utilizzare etichetta predefinita hello **% WORKSPACE_ID % _oms** o **% WORKSPACE_ID_OMS**, definire un oggetto personalizzato toohelp etichetta distinguere le modifiche.  

    > [!NOTE]
    > Se si modificano i valori predefiniti di hello nel file di configurazione di hello, verranno sovrascritti quando l'agente di hello applica una configurazione predefinita.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Dopo aver completato le modifiche di hello, hello Syslog e hello servizio dell'agente OMS è necessario riavviare toobe tooensure hello configurazione modifiche diventano effettive.   

## <a name="syslog-record-properties"></a>Proprietà dei record Syslog
Dispongono del tipo di record Syslog **Syslog** e dispone di proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Computer |Computer in cui hello eventi raccolti da. |
| Facility |Definisce la parte hello del sistema hello che ha generato il messaggio hello. |
| HostIP |Indirizzo IP del sistema hello invio messaggio hello. |
| HostName |Nome del sistema hello invio messaggio hello. |
| SeverityLevel |Livello di gravità dell'evento hello. |
| SyslogMessage |Testo del messaggio hello. |
| ProcessID |ID del processo di hello che ha generato il messaggio hello. |
| EventTime |Data e ora di hello evento è stato generato. |

## <a name="log-queries-with-syslog-records"></a>Query di log con record Syslog
Hello nella tabella seguente vengono forniti esempi di query di log che recuperano record Syslog.

| Query | Descrizione |
|:--- |:--- |
| Type=Syslog |Tutti i record Syslog. |
| Type=Syslog SeverityLevel=error |Tutti i record Syslog con livello di gravità errore. |
| Type=Syslog &#124; measure count() by Computer |Numero di record Syslog per computer. |
| Type=Syslog &#124; measure count() by Facility |Numero di record Syslog per funzionalità. |

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> | Query | Descrizione |
|:--- |:--- |
| syslog |Tutti i record Syslog. |
| Syslog &#124; where SeverityLevel == "error" |Tutti i record Syslog con livello di gravità errore. |
| Syslog &#124; summarize AggregatedValue = count() by Computer |Numero di record Syslog per computer. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |Numero di record Syslog per funzionalità. |

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.
* Utilizzare [campi personalizzati](log-analytics-custom-fields.md) tooparse dati da record syslog in singoli campi.
* [Configurare gli agenti Linux](log-analytics-linux-agents.md) toocollect altri tipi di dati.
