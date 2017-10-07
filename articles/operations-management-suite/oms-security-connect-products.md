---
title: aaaConnecting la sicurezza prodotti toohello sicurezza Operations Management Suite (OMS) e la soluzione di controllo | Documenti Microsoft
description: Questo documento consente si tooconnect i prodotti di sicurezza tooOperations protezione del gruppo di gestione e di soluzione di controllo utilizzando il formato di eventi comuni.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>La connessione la sicurezza prodotti toohello sicurezza Operations Management Suite (OMS) e la soluzione di controllo 
Questo documento consente di connettersi ai prodotti di sicurezza in hello sicurezza OMS e la soluzione di controllo. è supportata le seguenti origini Hello:

- Eventi Common Event Format (CEF)
- Eventi ASA Cisco


## <a name="what-is-cef"></a>Informazioni su CEF
Il formato di evento comuni (CEF) è un formato standard di settore sopra i messaggi Syslog, utilizzati da molti sicurezza fornitori tooallow evento interoperabilità tra piattaforme diverse. Soluzione di controllo e sicurezza OMS supporta inserimenti di dati utilizzo CEF, che consentono di tooconnect i prodotti di sicurezza con la sicurezza di OMS. 

Connettendo il tooOMS di origine dati, verranno tootake in grado di sfruttare hello funzionalità che fanno parte della piattaforma seguenti:

- Ricerca e controllo
- Controllo
- Avviso
- Intelligence per le minacce
- Errori rilevanti

## <a name="collection-of-security-solution-logs"></a>Raccolta di log di soluzioni per la sicurezza

La soluzione per la sicurezza per OMS supporta la raccolta di log tramite CEF sui log Syslog e [ASA Cisco](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). In questo esempio, l'origine hello (computer che genera log hello) è un computer Linux in esecuzione il daemon syslog-ng e destinazione hello è sicurezza OMS. il computer Linux tooprepare hello che occorre hello tooperform seguente attività:

- Scaricare hello agente OMS per Linux e versione 1.2.0-25 o versione successiva.
- Consultare la sezione hello **Guida all'installazione rapida** da [questo articolo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall e area di lavoro tooyour hello onboard agente.

In genere, l'agente di hello è installato in un computer diverso da hello uno per i log di hello vengono generati. Computer agente di inoltro hello registri toohello richiederà in genere hello alla procedura seguente:

- Configurare la registrazione del prodotto/macchina tooforward hello gli eventi necessari toohello daemon syslog (rsyslog o syslog-ng) hello sul computer agente hello.
- Abilitare il daemon syslog hello nei hello agente macchina tooreceive messaggi provenienti da un sistema remoto.

Nel computer agente hello, gli eventi di hello devono toobe inviato dalla porta UDP di toolocal daemon syslog hello 25226. agente Hello è in attesa di eventi in ingresso su questa porta. di seguito Hello è una configurazione di esempio per l'invio di tutti gli eventi dall'agente di toohello hello sistema locale (è possibile modificare hello configurazione toofit le impostazioni locali):

1. Finestra terminal aprire hello e passare toohello directory */etc/syslog-ng /* 
2. Creare un nuovo file *sicurezza-config-omsagent. conf* e aggiungere hello seguente contenuto: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Scaricare il file hello *security_events.conf* e posizionare */etc/opt/microsoft/omsagent/conf/omsagent.d/* nel computer dell'agente OMS hello.
4. Digitare il comando hello seguito daemon syslog di hello toorestart: *per syslog-ng eseguire:*
    
    ```
    sudo service rsyslog restart
    ```

    *Per eseguire rsyslog:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Digitare il comando hello sotto toorestart hello agente OMS:

    *Per eseguire syslog-ng:*
    
    ```
    sudo service omsagent restart
    ```

    *Per eseguire rsyslog:*
    
    ```
    systemctl restart omsagent
    ```
6. Digitare comando hello seguente ed esaminare tooconfirm risultato hello che non siano presenti errori nel log dell'agente OMS hello:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Esaminare gli eventi di sicurezza raccolti

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Al termine del hello configurazione, eventi di protezione hello inizierà toobe caricamento dalla sicurezza di OMS. toovisualize tali eventi, aprire hello ricerca Log, digitare il comando di hello *tipo = CommonSecurityLog* in hello campo ricerca e premere INVIO. Hello esempio seguente viene illustrato il risultato di hello di questo comando, si noti che la sicurezza OMS in questo caso i registri di protezione da più fornitori già caricamento:
   
![Valutazione baseline di Sicurezza e controllo di OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

È possibile limitare la ricerca per un unico fornitore, ad esempio, Cisco online registra toovisualize, tipo: *tipo = CommonSecurityLog DeviceVendor = Cisco*. Hello "CommonSecurityLog" è predefinite campi per qualsiasi intestazione CEF inclusi extensios base hello, mentre un'altra estensione, se si tratta di "Custom Extension" o, non verrà inserito nel campo "AdditionalExtensions". È possibile utilizzare i campi tooget dedicato di funzionalità di hello campi personalizzati da esso. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Accesso ai computer senza valutazione baseline
OMS supporta profilo di base membro di dominio hello in Windows Server 2008 R2 fino tooWindows Server 2012 R2. La baseline di Windows Server 2016 non è ancora definitiva e verrà aggiunta non appena pubblicata. Tutti gli altri sistemi operativi analizzati tramite OMS Security and Audit valutazione della linea di base vengono visualizzate in hello **computer privi di valutazione della linea di base** sezione.

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come tooconnect il tooOMS soluzione CEF. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

