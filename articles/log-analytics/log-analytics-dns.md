---
title: soluzione Analitica in Azure Log Analitica aaaDNS | Documenti Microsoft
description: Configurare e utilizzare hello DNS Analitica soluzione di infrastruttura DNS prestazioni, sicurezza e altre operazioni approfondite toogather Analitica di Log.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Raccogliere informazioni approfondite sull'infrastruttura DNS con hello soluzione DNS Analitica anteprima

![Simbolo di Analisi DNS](./media/log-analytics-dns/dns-analytics-symbol.png)

In questo articolo viene descritto come tooset backup e utilizzare hello soluzione Analitica DNS di Azure insights toogather Analitica di Log di Azure nell'infrastruttura DNS prestazioni, sicurezza e altre operazioni.

DNS Analytics consente di:

- Identificare i client che tentano di nomi di dominio dannoso tooresolve.
- Identificare i record di risorse non aggiornati.
- Identificare i nomi di dominio sottoposti frequentemente a query e i client DNS loquaci.
- Visualizzare il carico di richieste nei server DNS.
- Visualizzare gli errori di registrazione di DNS dinamici.

soluzione Hello raccoglie, analizza e correla analitici DNS di Windows e log di controllo e altri dati correlati dal server DNS.

## <a name="connected-sources"></a>Origini connesse

Hello nella tabella seguente vengono descritti hello connesso origini supportate da questa soluzione:

| **Origine connessa** | **Supporto** | **Descrizione** |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | Sì | soluzione Hello raccoglie le informazioni DNS dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | soluzione Hello non raccoglie informazioni DNS dagli agenti Linux diretti. |
| [Gruppo di gestione di System Center Operations Manager](log-analytics-om-agents.md) | Sì | soluzione Hello raccoglie le informazioni DNS dagli agenti in un gruppo di gestione di Operations Manager connesso. Una connessione diretta da toohello agente di Operations Manager hello Operations Management Suite non è necessaria. Dati viene inoltrati dal repository di hello gestione gruppo toohello Operations Management Suite. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | Archiviazione di Azure non verrà usato dalla soluzione hello. |

### <a name="data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati

soluzione Hello raccoglie l'inventario DNS e i dati relativi agli eventi DNS dai server DNS hello in cui è installato un agente di Log Analitica. Questi dati vengono quindi caricati tooLog Analitica e visualizzati nel dashboard di soluzione hello. Eseguendo il cmdlet di PowerShell DNS hello vengono raccolti i dati correlati al magazzino, ad esempio il numero di hello del server DNS, zone e i record di risorse. dati Hello viene aggiornati ogni due giorni. Hello correlati agli eventi di raccolta dei dati quasi in tempo reale da hello [analitiche e di log di controllo](https://technet.microsoft.com/library/dn800669.aspx#enhanc) fornito da avanzata registrazione DNS e diagnostica in Windows Server 2012 R2.

## <a name="configuration"></a>Configurazione

Utilizzare hello soluzione hello tooconfigure delle informazioni seguenti:

- È necessario disporre di un [Windows](log-analytics-windows-agents.md) o [Operations Manager](log-analytics-om-agents.md) agente in ogni server DNS che si desidera toomonitor.
- È possibile aggiungere l'area di lavoro hello DNS Analitica soluzione tooyour Operations Management Suite da hello [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). È inoltre possibile utilizzare il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

soluzione Hello avvia la raccolta dei dati senza necessità di hello di altre operazioni di configurazione. Tuttavia, è possibile utilizzare hello seguente raccolta di dati di configurazione toocustomize.

### <a name="configure-hello-solution"></a>Configurare la soluzione hello

Nel dashboard di soluzione hello, fare clic su **configurazione** pagina di configurazione del DNS Analitica tooopen hello. È possibile apportare due tipi di modifiche di configurazione.

- **Nomi di dominio consentiti**. soluzione Hello non elabora tutte le query di ricerca di hello. ma gestisce un elenco elementi consentiti per i suffissi dei nomi di dominio. query di ricerca Hello che la risoluzione dei nomi di dominio toohello corrispondenti suffissi di nome di dominio in questo elenco non vengono elaborate dalla soluzione hello. Non elabora i nomi di dominio consentito consente dati hello toooptimize inviati tooLog Analitica. Hello predefinito whitelist include nomi di dominio pubblico più diffusi, ad esempio www.google.com e www.facebook.com. È possibile visualizzare l'elenco completo predefinito hello mediante lo scorrimento.

 È possibile modificare hello elenco tooadd un suffisso di nome di dominio che si desidera tooview insights di ricerca per. È inoltre possibile rimuovere un suffisso di nome di dominio che non si desidera tooview insights di ricerca per.

- **Soglia client loquaci**. I client DNS che superano la soglia di hello per numero hello di richieste di ricerca viene evidenziato in hello **client DNS** blade. soglia predefinita Hello è 1.000. È possibile modificare la soglia hello.

    ![Nomi di dominio consentiti](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Management Pack

Se si utilizza l'area di lavoro hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite, hello seguenti management pack è installato:

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)

Se il gruppo di gestione di Operations Manager è Operations Management Suite tooyour connesso, hello seguenti management pack vengono installati in Operations Manager quando si aggiunge questa soluzione. Per i Management Pack seguenti non è necessaria alcuna configurazione o manutenzione:

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS Analytics Configuration (Microsoft.IntelligencePack.Dns.Configuration)

Per ulteriori informazioni sulla modalità di aggiornamento dei management pack di soluzione, vedere [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Utilizzare una soluzione Analitica DNS hello

Questa sezione vengono illustrate tutte le funzioni di dashboard hello e come toouse li.

Dopo aver aggiunto l'area di lavoro tooyour soluzione hello, riquadro soluzione hello nella pagina Panoramica di Operations Management Suite hello fornisce un riepilogo rapido dell'infrastruttura DNS. Include il numero di hello del server DNS in cui sono stati raccolti dati di hello. Include inoltre hello numero di richieste da client tooresolve dannoso domini hello nelle ultime 24 ore. Quando si fa clic su riquadro hello, apre il dashboard di soluzione hello.

![Riquadro DNS Analytics](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Dashboard della soluzione

dashboard di soluzione Hello Mostra le informazioni riepilogative per hello varie funzionalità della soluzione hello. Sono inoltre disponibili collegamenti toohello dettagliate di visualizzazione per le analisi forensi e la diagnosi. Per impostazione predefinita, per hello dati hello sono illustrati negli ultimi sette giorni. È possibile modificare l'intervallo di data e ora di hello utilizzando hello **controllo selezione data e ora**, come illustrato nella seguente immagine hello:

![Controllo di selezione di data e ora](./media/log-analytics-dns/dns-time.png)

dashboard di soluzione Hello Mostra hello seguenti pannelli:

**Sicurezza DNS**. Report hello client DNS che si sta tentando di toocommunicate con domini dannoso. Usando i feed di Microsoft threat intelligence, Analitica DNS possono rilevare gli indirizzi IP che si sta tentando di domini dannoso tooaccess client. In molti casi, i dispositivi infetti da malware "chiamate in uscita" toohello "comando e controllo" centro del dominio dannoso di hello risolvendo hello il nome di dominio di malware.

![Pannello Sicurezza DNS](./media/log-analytics-dns/dns-security-blade.png)

Quando si fa clic su un indirizzo IP del client nell'elenco di hello, ricerca di Log viene visualizzata la Dettagli ricerca hello di query rispettivi hello. Nell'esempio seguente di hello, Analitica DNS ha rilevato che la comunicazione hello è stata eseguita con un [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Ricerca log: risultati con IRCbot](./media/log-analytics-dns/ircbot.png)

informazioni di Hello consentono tooidentify di:

- Client IP che ha avviato la comunicazione hello.
- Nome di dominio che si risolve toohello IP dannosi.
- Risolve gli indirizzi IP che hello nome di dominio.
- Indirizzo IP dannoso.
- Gravità del problema hello.
- Motivo della black list IP dannosi hello.
- Data e ora di rilevamento.

**Domini sottoposti a query**. Fornisce hello nomi di dominio più frequenti sottoposte a query per i client DNS hello nell'ambiente in uso. È possibile visualizzare l'elenco di hello di tutti i nomi di dominio hello eseguire una query. È anche possibile drill-down nei dettagli richiesta di ricerca hello di un nome di dominio specifico in Log Search.

![Pannello Domini sottoposti a query](./media/log-analytics-dns/domains-queried-blade.png)

**Client DNS**. Report hello client *la violazione del limite di hello* per numero di query in hello periodo di tempo scelto. È possibile visualizzare l'elenco di hello di tutti i client DNS hello e i dettagli di hello delle query hello effettuate in Log Search.

![Pannello Client DNS](./media/log-analytics-dns/dns-clients-blade.png)

**Registrazioni di DNS dinamici**. Segnala gli errori di registrazione dei nomi. Tutti gli errori di registrazione per l'indirizzo [record di risorse](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (tipo A e AAAA) sono evidenziati client hello gli indirizzi IP che ha effettuato hello richieste di registrazione. È quindi possibile utilizzare questo causa principale di informazioni toofind hello di errore durante la registrazione di hello attenendosi alla procedura seguente:

1. Trovare il fuso orario hello è autorevole per nome hello hello client sta tentando di tooupdate.

2. Utilizzare hello soluzione toocheck hello informazioni di inventario di tale area.

3. Verificare che l'aggiornamento dinamico hello per zona hello è abilitato.

4. Controllare se la zona hello è configurata per l'aggiornamento dinamico protetto o non.

    ![Pannello Registrazioni di DNS dinamici](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Richieste di registrazione del nome**. riquadro superiore di Hello Mostra una linea di tendenza di esito positivo e negativo richieste di aggiornamento dinamico DNS. riquadro inferiore Hello Elenca i client di primi 10 hello che inviano richieste non riuscite di aggiornamento DNS server DNS toohello, ordinati in base al numero di hello di errori.

![Pannello Richieste di registrazione del nome ](./media/log-analytics-dns/name-reg-req-blade.png)

**Query DDI Analytics di esempio**. Contiene un elenco di query di ricerca più comuni hello che recuperano dati analitica non elaborato direttamente.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Query di esempio](./media/log-analytics-dns/queries.png)

È possibile usare queste query come punto di partenza per creare le proprie query per l'elaborazione di report personalizzati. le query Hello collegano toohello pagina di ricerca nei Log Analitica DNS in cui vengono visualizzati i risultati:

- **Elenco di server DNS**. Visualizza un elenco di tutti i server DNS con i nomi di dominio completo, i nomi di dominio, i nomi foresta e gli IP server associati.
- **Elenco di zone DNS**. Mostra un elenco di tutte le zone DNS con nome zona associata hello, lo stato di aggiornamento dinamico, server dei nomi e stato della firma DNSSEC.
- **Record di risorse inutilizzati**. Mostra un elenco di tutti i record di risorse inutilizzate/aggiornata hello. Questo elenco contiene nome record di risorsa hello, tipo di record di risorse, server DNS hello associata, ora di generazione di record e nome della zona. È possibile utilizzare questo elenco tooidentify hello record di risorse DNS che non sono più in uso. In base a queste informazioni, è quindi possibile rimuovere tali voci dai server DNS hello.
- **Carico query server DNS**. Mostra le informazioni in modo che sia possibile ottenere una prospettiva di hello che caricare DNS sui server DNS. Queste informazioni consentono di pianificare la capacità di hello per i server hello. È possibile passare toohello **metriche** scheda visualizzazione grafica tooa toochange hello vista. Questa vista consente di comprendere come hello caricare DNS viene distribuito tra i server DNS. e mostra le tendenze nella frequenza di query DNS per ogni server.

    ![Ricerca log: risultati relativi alle query nei server DNS](./media/log-analytics-dns/dns-servers-query-load.png)

- **Carico query zone DNS**. Mostra le statistiche di zona query al secondo di DNS di tutte le zone hello hello nei server DNS hello gestiti da soluzioni hello. Fare clic su hello **metriche** scheda visualizzazione hello toochange dalla visualizzazione di grafica tooa record dettagliate dei risultati di hello.
- **Eventi di configurazione**. Mostra tutti gli eventi di modifica configurazione DNS hello e i messaggi associati. È quindi possibile filtrare questi eventi in base al tempo di hello evento, ID di evento, il server DNS, o alla categoria attività. dati Hello consentono di controllare i server DNS toospecific le modifiche apportate a orari specifici.
- **Log analitico DNS**. Mostra tutti gli eventi analitici di hello in tutti i server DNS hello gestiti da soluzione hello. È quindi possibile filtrare questi eventi in base al tempo di hello evento, ID di evento, il server DNS, indirizzo IP del client che ha effettuato hello query di ricerca e categoria di tipi di attività di query. Gli eventi analitici di server DNS abilitano l'attività di rilevamento nel server DNS hello. Ogni volta che il server di hello invia o riceve le informazioni DNS viene registrato un evento di analisi.

### <a name="search-by-using-dns-analytics-log-search"></a>Eseguire una ricerca usando la Ricerca log di DNS Analytics

Nella pagina di ricerca di Log hello, è possibile creare una query. È possibile filtrare i risultati usando i controlli facet. È anche possibile creare query avanzate tootransform, filtro e report sui risultati. Avviare utilizzando hello seguente query:

1. In hello **casella search**, tipo `Type=DnsEvents` tooview tutti gli eventi DNS generati dal server DNS hello gestiti da soluzione hello di hello. dati del log hello per tutti gli eventi correlati toolookup query, le registrazioni dinamiche e modifiche di configurazione dell'elenco dei risultati di Hello.

    ![Ricerca log: eventi DNS](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. dati del log tooview hello per le query di ricerca, selezionare **LookUpQuery** come hello **sottotipo** filtro dal controllo del facet hello a sinistra di hello. Viene visualizzata una tabella che elenca tutti gli eventi query di ricerca hello per hello periodo di tempo selezionato.

    b. dati del log tooview hello per le registrazioni dinamiche, selezionare **DynamicRegistration** come hello **sottotipo** filtro dal controllo del facet hello a sinistra di hello. Viene visualizzata una tabella che elenca tutti gli eventi di registrazione dinamica hello per hello periodo di tempo selezionato.

    c. dati del log tooview hello per le modifiche di configurazione, selezionare **ConfigurationChange** come hello **sottotipo** filtro dal controllo del facet hello a sinistra di hello. Viene visualizzata una tabella che elenca tutti gli eventi di modifica configurazione hello per hello periodo di tempo selezionato.

2. In hello **casella search**, tipo `Type=DnsInventory` tooview tutti hello dati correlate all'inventario DNS per i server DNS hello gestiti da soluzione hello. elenco dei risultati di Hello dati hello del log per i server DNS e zone DNS i record di risorse.

    ![Ricerca log: inventario DNS](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Commenti e suggerimenti

È possibile indicare commenti e suggerimenti in diversi modi:

- **UserVoice**. Pubblicare un post nel idee per toowork funzionalità DNS Analitica. Visitare hello [pagina Operations Management Suite UserVoice](https://aka.ms/dnsanalyticsuservoice).
- **Partecipare alla coorte**. Siamo sempre interessati in presenza di nuovi clienti join nostri coorti tooget anticipata toonew le funzionalità di accesso e contribuire a migliorare Analitica DNS. Per partecipare, compilare questo [rapido sondaggio](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Passaggi successivi

[Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate DNS i record del log.
