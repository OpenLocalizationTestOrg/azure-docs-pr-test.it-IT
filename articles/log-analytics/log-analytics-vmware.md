---
title: soluzione di monitoraggio in Log Analitica aaaVMware | Documenti Microsoft
description: "Informazioni su come soluzione di monitoraggio VMware hello è in grado di gestire i registri e monitorare gli host ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Soluzione di monitoraggio VMware (anteprima) in Log Analytics

![Simbolo di VMware](./media/log-analytics-vmware/vmware-symbol.png)

soluzione di monitoraggio VMware in Log Analitica Hello è una soluzione che consente di creare una registrazione centralizzata e l'approccio di monitoraggio per i log di grandi dimensioni VMware. Questo articolo descrive come è possibile risolvere i problemi, acquisire e gestire gli host ESXi hello in un'unica posizione usando la soluzione hello. Con la soluzione hello, è possibile visualizzare dati dettagliati per tutti gli host ESXi in un'unica posizione. È possibile visualizzare i conteggi di eventi superiore, stato e le tendenze degli host macchina virtuale ed ESXi fornite tramite i log di host ESXi hello. È possibile risolvere il problema visualizzando e cercando i log di host ESXi centralizzati. Inoltre, è possibile creare avvisi basati sulle query di ricerca nei log.

soluzione Hello Usa funzionalità native syslog di hello ESXi host toopush dati tooa destinazione macchina virtuale, che l'agente OMS. Tuttavia, soluzione hello non scriverà file nel Registro di sistema all'interno di destinazione hello macchina virtuale. agente OMS Hello apre la porta 1514 e toothis è in ascolto. Dopo la ricezione di dati hello, l'agente OMS hello inserisce i dati di hello in OMS.

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

* Aggiungere hello VMware monitoraggio soluzione tooyour all'area di lavoro OMS tramite il processo di hello [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Host ESXi VMware supportati
vSphere ESXi Host 5.5 e 6.0

#### <a name="prepare-a-linux-server"></a>Preparazione di un server Linux
Creare un tooreceive di macchina virtuale del sistema operativo Linux tutti i dati syslog da host ESXi hello. Hello [agente Linux di OMS](log-analytics-linux-agents.md) è un punto di raccolta per tutti i dati di syslog host ESXi hello. È possibile utilizzare più ESXi host tooforward registri tooa single server Linux e come hello di esempio seguente.  

   ![flusso Syslog](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Configurazione della raccolta di Syslog
1. Configurare l'inoltro di Syslog per VSphere. Per configurare syslog forwarding toohelp di informazioni dettagliate, vedere [configurazione syslog in ESXi 5. x e 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Andare troppo**configurazione Host ESXi** > **Software** > **impostazioni avanzate** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. In hello *Syslog.global.logHost* campo, aggiungere il numero porta del server e hello Linux *1514*. Ad esempio, `tcp://hostname:1514` o `tcp://123.456.789.101:1514`
3. Apre il firewall di host ESXi hello per syslog. **Configurazione host ESXi** > **Software** > **Profilo di sicurezza** > **Firewall** e aprire **Proprietà**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Controllare hello vSphere Console tooverify che tale syslog è configurato correttamente. Conferma hello ESXI ospitare tale porta **1514** è configurato.
5. Scaricare e installare hello agente OMS per Linux su server Linux hello. Per ulteriori informazioni, vedere hello [documentazione per l'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Dopo aver installato l'agente OMS per Linux hello, andare toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d directory e copia hello vmware_esxi.conf file toohello /etc/opt/microsoft/omsagent/conf/omsagent.d e hello hello Modifica/gruppo proprietario e le autorizzazioni del file hello. ad esempio:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Riavviare hello agente OMS per Linux eseguendo `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Verificare la connettività di hello tra i server Linux hello e host ESXi hello utilizzando hello `nc` comando hello ESXi Host. ad esempio:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Nel portale di OMS hello, eseguire una ricerca di log di `Type=VMware_CL`. Quando il servizio OMS raccoglie dati di syslog hello, mantiene il formato syslog hello. Nel portale di hello, vengono acquisiti alcuni campi specifici, ad esempio *Hostname* e *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Se i risultati della ricerca log visualizzazione sono simili immagine toohello precedente, impostare in dashboard di soluzioni OMS VMware monitoraggio hello toouse.  

## <a name="vmware-data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati VMware
soluzione di monitoraggio VMware Hello raccoglie diversi dati di log e le metriche delle prestazioni dagli host ESXi utilizzando gli agenti di hello OMS per Linux che è stata abilitata.

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati.

| Piattaforma | Agente OMS per Linux | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |ogni 3 minuti |

Hello nella tabella seguente sono riportati esempi di campi di dati raccolti da hello soluzione di monitoraggio di VMware:

| nome campo | Descrizione |
| --- | --- |
| Device_s |Dispositivi di archiviazione VMware |
| ESXIFailure_s |tipi di errore |
| EventTime_t |quando si è verificato l'evento |
| HostName_s |nome dell'host ESXi |
| Operation_s |creazione o eliminazione di una VM |
| ProcessName_s |nome dell'evento |
| ResourceId_s |nome dell'host di VMware hello |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |stato SCSI VMware |
| SyslogMessage_s |dati Syslog |
| UserName_s |utente che ha creato o eliminato la VM |
| VMName_s |Nome della VM. |
| Computer |computer host |
| TimeGenerated |dati hello ora è stati generati |
| DataCenter_s |data center di VMware |
| StorageLatency_s |latenza di archiviazione (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Panoramica della soluzione di monitoraggio VMware
riquadro VMware Hello viene visualizzato nel portale di OMS hello. che fornisce una visualizzazione dettagliata degli errori. Quando si fa clic su riquadro hello, entra in una visualizzazione dashboard.

![riquadro](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Passare a visualizzazione dashboard hello
In hello **VMware** visualizzazione dashboard, i pannelli sono organizzati per:

* Conteggio stato di errore
* Host principali per conteggio degli eventi
* Conteggi eventi principali
* Attività macchine virtuali
* Eventi dischi host ESXi

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Fare clic su qualsiasi tooopen pannello riquadro di ricerca Log Analitica che mostra informazioni dettagliate specifiche per il pannello hello.

Da qui è possibile modificare toomodify query di ricerca hello per elementi specifici. Per un'esercitazione sui concetti fondamentali di hello di ricerca OMS, estrarre hello [esercitazione ricerca log OMS.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Individuazione degli eventi host ESXi
Un singolo host ESXi genera più log, in base ai loro processi. Hello soluzione di monitoraggio VMware centralizza li e un riepilogo di conteggio degli eventi di hello. Questa vista centralizzata aiuta a comprendere quale host ESXi ha un volume elevato di eventi e quali eventi si verificano più di frequente nell'ambiente.

![event](./media/log-analytics-vmware/events.png)

È possibile approfondire più nel dettaglio facendo clic su un host ESXi o un tipo di evento.

Quando si fa clic su un nome host ESXi, vengono visualizzate informazioni da tale host ESXi. Se si desidera toonarrow risultati con il tipo di evento hello, aggiungere `“ProcessName_s=EVENT TYPE”` nella query di ricerca. È possibile selezionare **ProcessName** nel filtro di ricerca hello. Sono pertanto informazioni hello.

![drill](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Individuazione di elevate attività delle VM
È possibile creare ed eliminare una macchina virtuale su qualsiasi host ESXi. È utile per un amministratore tooidentify quanti macchine virtuali consente di creare un host ESXi. Che a sua volta, consente di toounderstand prestazioni e la pianificazione della capacità. Quando si gestisce un ambiente, è indispensabile tenere traccia degli eventi di attività delle VM.

![drill](./media/log-analytics-vmware/vmactivities1.png)

Se si desidera toosee host ESXi ulteriori dati creazione della macchina virtuale, fare clic su un nome host ESXi.

![drill](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Query di ricerca comuni
soluzione Hello include altre query utili che consentono di gestire gli host ESXi, ad esempio lo spazio di archiviazione ad alta latenza dell'archiviazione ed errore di percorso.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![query](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Salvataggio delle query
Il salvataggio delle query di ricerca è una funzionalità standard di OMS e può aiutare a conservare eventuali query utili. Dopo aver creato una query che utile, salvarlo facendo hello **Preferiti**. Una query salvata consente facilmente riutilizzarla in seguito da hello [My Dashboard](log-analytics-dashboards.md) pagina in cui è possibile creare dashboard personalizzati.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Creazione di avvisi da query
Dopo aver creato le query, è possibile toouse hello query tooalert quando si verificano eventi specifici. Vedere [gli avvisi nel registro Analitica](log-analytics-alerts.md) per informazioni su come toocreate avvisi. Per esempi di query e altri esempi di query di avviso, vedere hello [monitoraggio VMware utilizzando OMS Log Analitica](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) post di blog.

## <a name="frequently-asked-questions"></a>Domande frequenti
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>Cosa è necessario toodo in host ESXi hello impostazione? Quali saranno le conseguenze per l'ambiente esistente?
soluzione di Hello utilizza il meccanismo di inoltro hello nativo Syslog Host ESXi. Non è necessario software aggiuntivo di Microsoft nei log di hello Host ESXi toocapture hello. Deve essere un ambiente esistente tooyour di basso impatto. Tuttavia, è necessario tooset syslog inoltro, che è una funzionalità ESXI.

### <a name="do-i-need-toorestart-my-esxi-host"></a>È necessario toorestart dell'host ESXi?
No. Questo processo non richiede un riavvio. In alcuni casi, vSphere aggiornare correttamente hello syslog. In tal caso, l'accesso host ESXi toohello e ricaricare hello syslog. Nuovamente, non è necessario host hello toorestart, pertanto questo processo non è stato ambiente tooyour arresto improvviso.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>È possibile aumentare o diminuire hello volume dei dati di log inviati tooOMS?
Sì. È possibile utilizzare le impostazioni a livello di Log Host ESXi hello in vSphere. Raccolta di log si basa sull'hello *info* livello. In tal caso, se si desidera tooaudit VM creazione o eliminazione, è necessario hello tookeep *info* livello nell'Hostd. Per ulteriori informazioni, vedere hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Motivo per cui Hostd non fornisce dati tooOMS? Il log impostazione tooinfo.
Si è verificato un errore di host ESXi hello syslog timestamp. Per ulteriori informazioni, vedere hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Dopo aver applicato la soluzione alternativa hello, Hostd dovrebbe funzionare normalmente.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>È possibile avere più ESXi host inoltro syslog dati tooa singola macchina virtuale con omsagent?
Sì. È possibile avere più ESXi host inoltro tooa singola macchina virtuale con omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Perché non sono visualizzati dati che pervengono al servizio OMS?
Possono esserci diversi motivi:

* host ESXi Hello non viene eseguita correttamente dati toohello macchina virtuale in esecuzione omsagent. tootest, eseguire hello alla procedura seguente:

  1. tooconfirm, accedere a host ESXi toohello tramite ssh ed eseguire hello comando seguente:`nc -z ipaddressofVM 1514`

      Se il problema persiste, le impostazioni di vSphere in hello configurazione avanzata sono probabilmente non corretta. Vedere [configurare syslog raccolta](#configure-syslog-collection) per informazioni su come tooset backup hello ESXi host per l'inoltro syslog.
  2. Se la connettività porta syslog ha esito positivo, ma non viene visualizzato ancora tutti i dati, quindi ricaricare syslog hello in host ESXi hello utilizzando ssh hello toorun comando seguente:` esxcli system syslog reload`
* macchina virtuale con l'agente OMS Hello non è impostato correttamente. tootest, eseguire hello alla procedura seguente:

  1. OMS è in ascolto sulla porta toohello 1514 e inserisce i dati in OMS. tooverify è aperto, eseguire hello comando seguente:`netstat -a | grep 1514`
  2. La porta `1514/tcp` dovrebbe risultare aperta. In caso contrario, verificare che omsagent hello sia installato correttamente. Se non è possibile visualizzare le informazioni sulla porta hello, porta syslog hello non è aperta nel hello macchina virtuale.

     1. Verificare che hello agente OMS è in esecuzione utilizzando `ps -ef | grep oms`. Se non è in esecuzione, avviare il processo di hello eseguendo il comando hello` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Aprire hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` file.

         Verificare che utente appropriata hello e impostazione del gruppo sia valido, in modo analogo:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Se non esiste o hello utente file hello e impostazione di gruppo non è corretto, intraprendere l'azione correttiva da [preparazione di un server Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [ricerche nei Log](log-analytics-log-searches.md) nel Log Analitica tooview in dettaglio i dati di host VMware.
* [Creare dashboard personalizzati](log-analytics-dashboards.md) che mostrino i dati dell'host VMware.
* [Creare avvisi](log-analytics-alerts.md) quando si verificano eventi specifici relativi all'host VMware.
