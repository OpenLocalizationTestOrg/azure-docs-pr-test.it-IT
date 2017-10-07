---
title: amministrazione aaaService per ricerca di Azure nel portale di Azure hello
description: Gestire la ricerca di Azure, un servizio di ricerca cloud ospitato in Microsoft Azure, utilizzando hello portale di Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Amministrazione del servizio per ricerca di Azure nel portale di Azure hello
> [!div class="op_single_selector"]
> * [Portale](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Ricerca di Azure è un servizio di ricerca basato sul cloud completamente gestito usato per offrire un'esperienza di ricerca avanzata nelle app personalizzate. Questo articolo descrive hello *servizio amministrazione* attività che è possibile eseguire in hello [portale di Azure](https://portal.azure.com) per un servizio di ricerca che è già stato effettuato il provisioning. *Amministrazione del servizio* semplice in base alla progettazione toohello limitato seguenti attività:

* Gestire e proteggere l'accesso toohello *chiavi api* utilizzate per il servizio tooyour accesso in lettura o scrittura.
* Modifica dell'allocazione di partizioni e repliche hello regolare la capacità del servizio.
* Monitorare l'utilizzo delle risorse, i limiti di toomaximum relativa del livello servizio.

**Non nell'ambito** 

*Gestione dei contenuti* (o un indice di gestione) si riferisce toooperations quali l'analisi dei volumi di query di ricerca traffico toounderstand, individuare gli utenti che le condizioni di cercare e ricerca efficacia risultati guidando toospecific clienti documenti nell'indice. Per avere assistenza in quest'area, visitare [Analisi del traffico di ricerca per Ricerca di Azure](search-traffic-analytics.md).

*Le prestazioni delle query* è oltre l'ambito di hello di questo articolo. Per altre informazioni, vedere [Monitorare l'utilizzo e le statistiche in un servizio Ricerca di Azure](search-monitor-usage.md) e [Prestazioni e ottimizzazione](search-performance-optimization.md).

*L'aggiornamento* non è un'attività amministrativa. Poiché le risorse vengono allocate quando viene eseguito il provisioning servizio hello, lo spostamento tooa altro livello richiede un nuovo servizio. Per informazioni dettagliate vedere [Creare un servizio di Ricerca di Azure nel portale](search-create-service-portal.md).

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Diritti di amministratore
Provisioning o la rimozione delle autorizzazioni servizio hello stesso può essere effettuata da un amministratore della sottoscrizione Azure o un coamministratore.

All'interno di un servizio, tutti gli utenti con accesso toohello URL del servizio e una chiave api di amministrazione dispone di accesso in lettura-scrittura toohello servizio. Accesso in lettura-scrittura fornisce hello possibilità tooadd, eliminare o modificare oggetti server, incluse le chiavi api, gli indici, gli indicizzatori, origini dati, pianificazioni e le assegnazioni di ruolo implementata tramite [ruoli definiti RBAC](#rbac).

Tutte le interazioni utente con ricerca di Azure rientrano in una delle modalità seguenti: lettura / scrittura del servizio di accesso toohello (diritti di amministratore) o servizio di accesso in sola lettura toohello (diritti query). Per ulteriori informazioni, vedere [gestire le chiavi api hello](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Impostare i ruoli RBAC per l'accesso amministrativo
Azure offre un [modello di autorizzazione basata sui ruoli globale](../active-directory/role-based-access-control-configure.md) per tutti i servizi gestiti tramite il portale di hello o le API di gestione risorse. I ruoli del proprietario, collaboratore e lettore determinano il livello di hello dell'amministrazione del servizio di ruolo assegnato tooeach entità di sicurezza, gruppi e utenti di Active Directory. 

Per la ricerca di Azure, le autorizzazioni RBAC determinano hello attività amministrative seguenti:

| Ruolo | Attività |
| --- | --- |
| Proprietario |Creare o eliminare il servizio di hello o qualsiasi oggetto nel servizio di hello, inclusi le pianificazioni di indicizzatore, origini dati di un indicizzatore, gli indicizzatori, gli indici e le chiavi api.<p>Visualizzare lo stato del servizio, inclusi conteggi e dimensioni.<p>Aggiunta o eliminazione dell'appartenenza al ruolo, che può essere gestita solo da un Proprietario.<p>Gli amministratori delle sottoscrizioni e i proprietari del servizio che il ruolo di proprietari di hello appartenenza automatico. |
| Collaboratore |Stesso livello di accesso del Proprietario, tranne la gestione dei ruoli Controllo degli accessi in base al ruolo. Ad esempio, un Collaboratore può visualizzare e rigenerare `api-key`, ma non può modificare le appartenenze ai ruoli. |
| Reader |Può visualizzare lo stato e le chiavi di query. I membri di questo ruolo non possono modificare la configurazione del servizio né visualizzare le chiavi amministratore. |

Ruoli non concedono l'endpoint del servizio toohello diritti di accesso. Le operazioni del servizio di ricerca, ad esempio la gestione e il popolamento degli indici e le query sui dati di ricerca, sono controllate tramite le chiavi API, non tramite i ruoli. Per altre informazioni, vedere "Autorizzazioni per le operazioni di gestione e per le operazioni di dati" in [Che cos'è il controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Informazioni di sistema e registrazione
Ricerca di Azure non espone i file di log per un singolo servizio tramite il portale di hello o interfacce di programmazione. A livello di base hello e versioni successive, Microsoft consente di monitorare tutti i servizi di ricerca di Azure per la disponibilità del 99,9% per i contratti di servizio (SLA). Se il servizio di hello è lento o velocità effettiva delle richieste scende di sotto delle soglie di contratto di servizio, i team di supporto esaminare toothem disponibili i file di log hello e problema hello indirizzo.

In termini di informazioni generali sul servizio, è possibile ottenere informazioni in hello seguenti modi:

* Nel portale di hello, nel dashboard del servizio hello tramite le notifiche, proprietà e i messaggi di stato.
* Utilizzando [PowerShell](search-manage-powershell.md) o hello [API REST di gestione](https://docs.microsoft.com/rest/api/searchmanagement/) troppo[ottenere proprietà del servizio](https://docs.microsoft.com/rest/api/searchmanagement/services), o lo stato di utilizzo delle risorse di indice.
* Tramite l' [analisi del traffico di ricerca](search-traffic-analytics.md), come indicato prima.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Gestire le chiavi API
Tutte le richieste di servizio di ricerca tooa necessario una chiave api che è stata generata in modo specifico per il servizio. Questa chiave api è unico meccanismo di hello per l'autenticazione dell'endpoint del servizio di ricerca tooyour accesso. 

Una chiave API è una stringa composta da lettere e numeri generati casualmente. Tramite [autorizzazioni RBAC](#rbac), è possibile eliminare o leggere le chiavi di hello, ma è possibile sostituire una chiave con una password definita dall'utente. 

Due tipi di chiavi sono tooaccess utilizzato il servizio di ricerca:

* Amministrazione (valido per qualsiasi operazione di lettura / scrittura per il servizio hello)
* Di query (valida per operazioni di sola lettura, ad esempio le query su un indice)

Una chiave api di amministrazione viene creata quando viene eseguito il provisioning servizio hello. Esistono due chiavi amministratore, definite come *primario* e *secondario* tookeep loro direttamente, ma in realtà sono intercambiabili. Ogni servizio dispone di due chiavi amministratore in modo che uno rollover senza perdere l'accesso tooyour servizio. È possibile rigenerare una chiave di amministrazione, ma non è possibile aggiungere toohello admin totale conteggio di chiavi. È consentito un massimo di due chiavi amministratore per ogni servizio di ricerca.

Le chiavi di query sono progettate per le applicazioni client che chiamano il servizio di ricerca direttamente. È possibile creare backup delle chiavi di query too50. Nel codice dell'applicazione, specificare URL ricerca hello e un servizio di toohello query chiave api tooallow accesso in sola lettura. Il codice dell'applicazione specifica anche l'indice di hello utilizzato dall'applicazione. Endpoint hello insieme, una chiave api per l'accesso in lettura e un indice di destinazione, definire il livello di ambito e accesso hello della connessione hello dall'applicazione client.

tooget o rigenerare le chiavi api, dashboard del servizio aprire hello. Fare clic su **CHIAVI** tooslide aprire pagina di gestione delle chiavi hello. Nella parte superiore della pagina hello hello sono comandi per la rigenerazione o la creazione di chiavi. Per impostazione predefinita, vengono create solo le chiavi amministratore. Le chiavi API di query devono essere create manualmente.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Proteggere le chiavi API
Chiave di sicurezza viene garantita limitando l'accesso tramite il portale di hello o interfacce di gestione risorse (PowerShell o interfaccia della riga di comando). Come indicato, gli amministratori delle sottoscrizioni possono visualizzare e rigenerare tutte le chiavi API. Come precauzione, esaminare toounderstand assegnazioni di ruolo che dispone di chiavi di accesso toohello amministratore.

1. Nel dashboard servizi hello, fare clic su Pannello di accesso icona tooslide hello aprire utenti hello.
   ![][7]
2. In Utenti esaminare le assegnazioni di ruoli esistenti. Come previsto, gli amministratori delle sottoscrizioni dispone già di servizio di accesso completo toohello tramite il ruolo di proprietario hello.
3. Fare clic su toodrill ulteriormente, **amministratori della sottoscrizione** e quindi espandere hello ruolo assegnazione elenco toosee che dispone di diritti di amministrazione di condivisione per il servizio di ricerca.

Autorizzazioni di accesso di un altro modo tooview è tooclick **ruoli** nel pannello utenti hello. In questo modo consente di visualizzare i ruoli disponibili e il numero di hello del ruolo assegnato tooeach utenti o gruppi.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Monitorare l'uso delle risorse
Nel dashboard di hello, il monitoraggio delle risorse è limitato toohello informazioni visualizzate nel dashboard del servizio hello e alcune metriche che è possibile ottenere eseguendo una query del servizio hello. Nel dashboard del servizio hello nella sezione Utilizzo hello, è possibile determinare rapidamente se i livelli di risorse di partizione sono adeguati per l'applicazione.

Utilizza hello API del servizio di ricerca, è possibile ottenere un conteggio nei documenti e indici. Esistono limiti fissi associati a questi conteggi in base a livello di prezzo hello. Per altre informazioni, vedere [Limiti del servizio di ricerca](search-limits-quotas-capacity.md). 

* [Ottenere le statistiche di un indice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Conteggio documenti](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Il comportamento della cache può determinare la dichiarazione di un limite più alto. Ad esempio, quando si utilizza il servizio condiviso hello, si potrebbe visualizzare un documento count su limite di 10.000 documenti hello. sopravvalutazione Hello è temporaneo e verrà rilevato in hello successiva verifica imposizione del limite. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Interruzioni di servizio e ripristino di emergenza

Anche se è possibile recuperare i dati, ricerca di Azure non fornisce il failover immediato del servizio hello se è presente un'interruzione a livello di hello cluster o data center. Se un cluster non riesce in data center di hello, team addetto alle operazioni hello rileverà e toorestore del servizio. Si verificheranno tempi di inattività durante il ripristino del servizio. È possibile richiedere toocompensate crediti di servizio per la mancata disponibilità del servizio per hello [contratto di servizio (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Se il servizio continuo è necessaria nell'evento hello di errori irreversibili di fuori del controllo di Microsoft, è possibile [il provisioning di un servizio aggiuntivo](search-create-service-portal.md) in un'area diversa e implementare una replica geografica strategia tooensure indici sono completamente ridondante in tutti i servizi.

I clienti che utilizzano [indicizzatori](search-indexer-overview.md) toopopulate e aggiornare gli indici in grado di gestire il ripristino di emergenza tramite gli indicizzatori geografica specifica sfruttando hello stessa origine dati. Due servizi in diverse aree geografiche, ognuno dei quali esegue un indicizzatore, Impossibile indicizzare da hello stesso ridondanza geografica tooachieve dell'origine dati. Se si esegue l'indicizzazione da origini dati che hanno anche una ridondanza geografica, tenere presente che gli indicizzatori di Ricerca di Azure possono eseguire solo l'indicizzazione incrementale da repliche primarie. In un evento di failover, essere certi toore punto hello indicizzatore toohello nuova replica primaria. 

Se non si utilizzano gli indicizzatori, utilizzare i codice toopush oggetti e dati toodifferent ricerca servizi delle applicazioni in parallelo. Per altre informazioni, vedere [Prestazioni e ottimizzazione in Ricerca di Azure](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Backup e ripristino

Poiché Ricerca di Azure non è una soluzione di archiviazione dati primaria, Microsoft non fornisce un meccanismo formale per il backup e il ripristino self-service. Se si elimina un indice per errore, il codice dell'applicazione utilizzato per la creazione e la compilazione di un indice è hello fatto opzione di ripristino. 

toorebuild un indice, eliminarlo (se presente), ricreare l'indice di hello nel servizio hello e ricaricare recuperando i dati dall'archivio dati primario. In alternativa, è possibile raggiungere troppo[il supporto tecnico]() toosalvage indici se è presente un'interruzione dell'alimentazione locale.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Aumentare o ridurre la quantità di risorse
Ogni servizio di ricerca viene creato con un minimo di una replica e una partizione. Se l'iscrizione a un [livello che fornisce risorse dedicate](search-limits-quotas-capacity.md), fare clic su hello **scala** riquadro hello servizio dashboard tooadjust utilizzo delle risorse.

Quando si aggiunge la capacità tramite una risorsa, il servizio hello utilizzati automaticamente. Non è necessaria alcuna azione ulteriore da parte dell'utente, ma è un leggero ritardo prima di impatto hello della nuova risorsa hello viene realizzato. Può richiedere 15 minuti o tooprovision altre risorse aggiuntive.

 ![][10]

### <a name="add-replicas"></a>Aggiungere repliche
L'aumento delle query al secondo o il raggiungimento della disponibilità elevata si ottengono mediante l'aggiunta di repliche. Ogni replica dispone di una copia di un indice, pertanto l'aggiunta di una replica più traduce tooone ulteriori indice disponibile per la gestione delle richieste di query. Per una disponibilità elevata, sono necessarie almeno 3 repliche. Per informazioni dettagliate, vedere [Pianificazione della capacità](search-capacity-planning.md).

Un servizio di ricerca con un numero superiore di repliche può eseguire il bilanciamento del carico delle richieste di query su un numero maggiore di indici. Dato un livello di volumi di query, velocità effettiva di query è in corso toobe più velocemente quando sono presenti più copie della richiesta di hello hello indice tooservice disponibili. Se si verificano la latenza delle query, è prevedibile un impatto positivo sulle prestazioni quando repliche aggiuntive hello sono online.

Anche se aumenta la velocità effettiva di query quando si aggiungono repliche, non è precisamente doppio o tripla man mano che si Aggiunta servizio tooyour repliche. Tutte le applicazioni di ricerca sono fattori tooexternal soggetto che influire negativamente sulle prestazioni delle query. Le query più complesse e latenza di rete sono due fattori che contribuiscono toovariations nei tempi di risposta delle query.

### <a name="add-partitions"></a>Aggiungere partizioni
Per la maggior parte delle applicazioni di servizio è indispensabile un numero maggiore di repliche invece che di partizioni. Per i casi in cui è necessario un numero maggiore di documenti, l'iscrizione al servizio Standard permette di aggiungere partizioni. Il livello Basic non offre partizioni aggiuntive.

Livello Standard hello, le partizioni vengono aggiunti in multipli di 12 (in particolare, 1, 2, 3, 4, 6 o 12). Si tratta di un elemento del partizionamento orizzontale. Un indice viene creato in 12 sottopartizioni, tutte archiviabili a propria volta in 1 partizione o equamente distribuibili in 2, 3, 4, 6 o 12 partizioni (in quest'ultimo caso, una per partizione).

### <a name="remove-replicas"></a>Rimuovere repliche
Dopo periodi di alti volumi di query è possibile ridurre le repliche dopo che i carichi di query di ricerca si sono normalizzati, ad esempio al termine di un periodo di vendite per le feste.

toodo, questo spostamento hello replica dispositivo di scorrimento tooa indietro numero inferiore. Non vi sono altre azioni richieste da parte dell'utente. Ridurre il numero di repliche hello cede macchine virtuali nel data center di hello. Le operazioni di query e di inserimento dati verranno ora elaborate su un numero minore di VM rispetto a prima. limite minimo Hello è una replica.

### <a name="remove-partitions"></a>Rimuovere partizioni
A differenza di rimozione di repliche, che richiede alcuno sforzo aggiuntivo da parte dell'utente, potrebbe essere alcuni toodo di lavoro se si utilizza spazio di archiviazione superiore può essere ridotto. Ad esempio, se la soluzione utilizza tre partizioni, downsizing tooone o due partizioni genererà un errore se il nuovo spazio di archiviazione hello è inferiore rispetto a quanto richiesto. Come prevedibile, le scelte effettuate toodelete indici o documenti all'interno di un indice associato di toofree spazio oppure mantenere la configurazione corrente di hello.

Non è disponibile un metodo di rilevamento che indichi quante sottopartizioni di indice sono archiviate su una partizione specifica. Ogni partizione offre circa 25 GB di spazio di archiviazione, pertanto sarà necessario dimensioni tooa di archiviazione tooreduce che possono essere gestite tramite un numero di partizioni che è hello. Se si desidera toorevert tooone partizione, tutte le 12 partizioni saranno necessario toofit.

toohelp con la pianificazione futura, è possibile toocheck archiviazione (tramite [ottenere statistiche dell'indice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee quanto effettivamente utilizzato. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Procedure consigliate su scalabilità e distribuzione
Questo video di 30 minuti esamina le procedure consigliate per gli scenari di distribuzione avanzata, inclusi i carichi di lavoro con distribuzione geografica. È inoltre possibile visualizzare [prestazioni e ottimizzazione in ricerca di Azure](search-performance-optimization.md) per tale hello copertura di pagine della guida punta stesso.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso i concetti di base hello amministrazione del servizio, è consigliabile utilizzare [PowerShell](search-manage-powershell.md) tooautomate attività.

È inoltre consigliabile esaminare hello [articolo prestazioni e ottimizzazione](search-performance-optimization.md).

Un altro si consiglia di video toowatch hello indicato nella sezione precedente hello. Fornisce una copertura più approfondita delle tecniche di hello indicati in questa sezione.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



