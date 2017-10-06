---
title: aaaAzure archiviazione interessante per i BLOB | Documenti Microsoft
description: "I livelli di archiviazione per l'archivio BLOB di Azure offrono un'archiviazione economicamente conveniente per dati oggetto in base ai modelli di accesso. livello di archiviazione sporadico Hello è ottimizzata per i dati che si accede con minore frequenza."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a>Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente e sporadico
## <a name="overview"></a>Panoramica
L'Archiviazione di Azure offre due livelli di archiviazione per l'archivio di oggetti BLOB, per consentire di archiviare i dati nel modo economicamente più conveniente in base alla modalità d'uso. Hello Azure **livello di archiviazione a caldo** è ottimizzato per l'archiviazione dei dati che si accede frequentemente. Hello Azure **livello di archiviazione sporadico** è ottimizzato per l'archiviazione dei dati sono raramente accessibile e lunga durata. Dati nel livello di archiviazione sporadico hello in grado di tollerare disponibilità leggermente inferiore, ma richiede comunque una durabilità elevata e caratteristiche simili di velocità effettiva e tempo per l'accesso come dati attivi. Per i dati ad accesso sporadico, contratti di servizio con una disponibilità leggermente più bassa e costi di accesso più elevati sono compromessi accettabili in cambio di costi di archiviazione molto più bassi.

Oggi, i dati archiviati nel cloud hello sta crescendo a un ritmo esponenziale. toomanage costi per le esigenze di archiviazione di espansione, è utile tooorganize in base agli attributi come frequenza di accesso e pianificato periodo di memorizzazione dei dati. Dati archiviati nel cloud hello possono essere diversi in termini di come viene generato, elaborato e accessibili tramite la relativa durata. Alcuni dati presentano accessi attivi e modifiche continue nel corso della rispettiva durata. Alcuni dati si accede frequentemente in anticipo il ciclo di vita, con accesso eliminazione drasticamente come hello dati età. Alcuni dati rimangono inattivi nel cloud hello e raramente, se mai eseguito una volta archiviati.

Tutti questi scenari di accesso ai dati descritti sopra usufruiscono di un livello differenziato di archiviazione ottimizzato per un particolare modello di accesso. Con l'introduzione di hello di livelli di archiviazione di frequente e sporadico, i Blob di Azure archiviazione ora soddisfa la necessità di livelli differenziati di archiviazione con separare prezzi modelli.

## <a name="blob-storage-accounts"></a>Account di archiviazione BLOB
**Account di archiviazione BLOB** sono account di archiviazione specializzati per l'archiviazione dei dati non strutturati come BLOB (oggetti) in Archiviazione di Azure. Con l'account di archiviazione Blob, è ora possibile scegliere tra toostore livelli di archiviazione di frequente e sporadico sporadico dati utilizzati meno di frequente a un costo di archiviazione inferiore e si accede più frequentemente di archivio dati attivi in un accesso più basso costo. Account di archiviazione BLOB sono account di archiviazione generico esistenti tooyour simile e condividono tutti durabilità grande hello, disponibilità, scalabilità e funzionalità che si utilizza oggi, tra cui la coerenza delle API 100% per i BLOB in blocchi e BLOB di aggiunta.

> [!NOTE]
> Gli account di archiviazione BLOB supportano solo i BLOB in blocchi e i BLOB di aggiunta, non i BLOB di pagine.
> 
> 

Account di archiviazione BLOB esporre hello **livello di accesso** attributo, che consente a livello di archiviazione hello toospecify come **Hot** o **sporadico** a seconda dei dati di hello archiviati in hello account. Se viene apportata una modifica nel modello di utilizzo di hello dei dati, è anche possibile passare tra questi livelli di archiviazione in qualsiasi momento.

> [!NOTE]
> Modifica livello di archiviazione hello può comportare costi aggiuntivi. Vedere hello [prezzi e fatturazione](storage-blob-storage-tiers.md#pricing-and-billing) sezione per ulteriori dettagli.
> 
> 

Scenari di utilizzo di esempio per il livello di archiviazione a caldo di hello includono:

* Dati a cui sono in uso attivo o toobe previsto accede (lettura da e scritti) frequentemente.
* Dati che sono preconfigurati per l'elaborazione e l'eventuale livello di archiviazione sporadico toohello di migrazione.

Scenari di utilizzo di esempio per il livello di archiviazione sporadico hello includono:

* Set di dati di backup, archiviazione e ripristino di emergenza.
* Contenuti multimediali precedenti non visualizzati più frequentemente, ma sono previsto toobe disponibile immediatamente quando si accede.
* Grandi set di dati che devono toobe archiviati in modo efficace costo mentre raccolte più dati per l'elaborazione futura. *ad esempio*, archiviazione a lungo termine di dati scientifici, dati di telemetria non elaborati di un impianto di produzione.
* Dati originali (non elaborati) che devono essere conservati, anche dopo che sono stati elaborati in un formato utilizzabile finale, *ad esempio*, file multimediali non elaborati dopo la transcodifica in altri formati.
* Conformità e dell'archivio dati che deve toobe archiviati per lungo tempo e si accede quasi. *ad esempio*, filmati di videocamere di sicurezza, vecchie radiografie/risonanze magnetiche per le organizzazioni sanitarie, registrazioni audio e trascrizioni di chiamate di clienti per i servizi finanziari.

Per informazioni sugli account di archiviazione, vedere [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md) .

Per le applicazioni che richiedono solo bloccano o si accodano nell'archiviazione blob, è consigliabile utilizzare account di archiviazione Blob, tootake sfruttare hello si differenzino solo modello di determinazione dei prezzi di archiviazione a livelli. È presente, tuttavia, che questo potrebbe non essere possibile in determinate circostanze in cui utilizza l'archiviazione generica account sarebbe hello toogo modo, ad esempio:

* È necessario toouse tabelle, code, o i file e si desidera che i BLOB archiviati in hello stesso account di archiviazione. Si noti che non vi sia alcun vantaggio dalle tecniche di toostoring in hello che stesso account diverso con hello stesso chiavi condivise.
* È comunque necessario modello di distribuzione classica toouse hello. Sono disponibili tramite modello di distribuzione Azure Resource Manager hello solo account di archiviazione BLOB.
* È necessario toouse BLOB di pagine. Gli account di archiviazione BLOB non supportano i BLOB di pagine. A meno che non vi siano esigenze specifiche per usare i BLOB di pagine, è consigliabile usare i BLOB in blocchi.
* Si utilizza una versione di hello [API REST di servizi di archiviazione](https://msdn.microsoft.com/library/azure/dd894041.aspx) che è precedente a 2014-02-14 o una libreria client con una versione inferiore a 4. x e non può aggiornare l'applicazione.

> [!NOTE]
> Gli account di archiviazione BLOB sono attualmente supportati in tutte le aree di Azure.
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a>Confronto tra i livelli di archiviazione hello
Hello nella tabella seguente vengono evidenziate confronto hello tra due livelli di archiviazione hello:

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><strong><center>Livello di archiviazione ad accesso frequente</center></strong></td>
    <td><strong><center>Livello di archiviazione ad accesso sporadico</center></strong></td
</tr>
<tr>
    <td><strong><center>Disponibilità</center></strong></td>
    <td><center>99.9%</center></td>
    <td><center>99%</center></td>
</tr>
<tr>
    <td><strong><center>Disponibilità<br>(letture RA-GRS)</center></strong></td>
    <td><center>99,99%</center></td>
    <td><center>99,9%</center></td>
</tr>
<tr>
    <td><strong><center>Addebiti per utilizzo</center></strong></td>
    <td><center>Costi di archiviazione più elevati<br>Costi di accesso e transazione più bassi</center></td>
    <td><center>Costi di archiviazione più bassi<br>Costi di accesso e transazione più elevati</center></td>
</tr>
<tr>
    <td><strong><center>Dimensioni minime oggetti<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Durata archiviazione minima<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Latenza<br>(Tempo toofirst byte)<center></strong></td>
    <td colspan="2"><center>millisecondi</center></td>
</tr>
<tr>
    <td><strong><center>Obiettivi di scalabilità e prestazioni<center></strong></td>
    <td colspan="2"><center>Uguali a quelli degli account di archiviazione di uso generico</center></td>
</tr>
</tbody>
</table>

> [!NOTE]
> Archiviazione BLOB account hello supporto stesso destinazioni di prestazioni e scalabilità, come gli account di archiviazione generico. Per ulteriori informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) .
> 
> 

## <a name="pricing-and-billing"></a>Prezzi e fatturazione
Account di archiviazione BLOB di utilizzare un nuovo modello di determinazione dei prezzi per l'archiviazione di blob in base a livello di archiviazione hello. Quando si utilizza un account di archiviazione Blob, si applica hello fatturazione considerazioni seguenti:

* **I costi di archiviazione**: inoltre toohello quantità di dati archiviati, il costo di hello archiviazione dei dati varia a seconda di livello di archiviazione hello. costo per gigabyte Hello è inferiore per livello di archiviazione sporadico hello rispetto a livello di archiviazione a caldo di hello.
* **I costi di accesso ai dati**: per i dati nel livello di archiviazione sporadico hello, verrà addebitato un costo di accesso ai dati per gigabyte per letture e scritture.
* **Costi di transazione**: è previsto un addebito per ogni transazione per entrambi i livelli. Tuttavia, il costo per transazione hello per il livello di archiviazione sporadico hello è superiore a quello per il livello di archiviazione a caldo di hello.
* **Costi di trasferimento dei dati di replica geografica**: si applica solo tooaccounts con la replica geografica configurata, tra cui GRS e RA-GRS. Il trasferimento dati con la replica geografica comporta un addebito per gigabyte.
* **Costi di trasferimento dati in uscita**: i trasferimenti dati in uscita (dati che vengono trasferiti al di fuori di un'area di Azure) vengono fatturati in base all'utilizzo di larghezza di banda per singolo gigabyte, come per gli account di archiviazione di uso generico.
* **Modifica livello di archiviazione hello**: modifica il livello di archiviazione hello da toohot sporadico comporteranno un tooreading uguale carica tutti i dati di hello esistenti nell'account di archiviazione hello per ogni transizione. Nelle hello invece modificare il livello di archiviazione hello da toocool a caldo è gratuitamente.

> [!NOTE]
> In ordine tooallow utenti tootry out hello nuovi livelli di archiviazione e convalidare funzionalità dopo il lancio, saranno applicate spese hello per modificare il livello di archiviazione hello dalla toohot sporadico fino al 30 giugno 2016. A partire da 2016 1 ° luglio, hello addebito sarà transizioni tooall applicato da toohot sporadico. Per ulteriori informazioni sui prezzi per gli account di archiviazione Blob hello, vedere [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) pagina. Per ulteriori informazioni sui dati in uscita hello gli addebiti di trasferimento, vedere [dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/) pagina.
> 
> 

## <a name="quick-start"></a>Avvio rapido
In questa sezione verrà illustrato hello seguenti scenari con hello portale di Azure:

* Come toocreate un account di archiviazione Blob.
* Come toomanage un account di archiviazione Blob.

### <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Creare un account di archiviazione Blob tramite hello portale di Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, selezionare **New** > **dati e archiviazione** > **account di archiviazione**.
3. Immettere un nome per l'account di archiviazione.
   
    Questo nome deve essere globalmente univoco. viene utilizzato come parte dell'URL hello oggetti hello tooaccess nell'account di archiviazione hello.  
4. Selezionare **Gestione risorse** come modello di distribuzione hello.
   
    Archiviazione a livelli può essere utilizzato solo con gli account di archiviazione di gestione delle risorse; si tratta di hello consigliata il modello di distribuzione di nuove risorse. Per ulteriori informazioni, consultare hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).  
5. Nell'elenco a discesa tipo di Account di hello, selezionare **nell'archiviazione Blob**.
   
    Questo è possibile specificare il tipo di hello dell'account di archiviazione. Archiviazione a livelli non è disponibile in spazio di memorizzazione generica. è disponibile solo in hello account di tipo di archiviazione Blob.     
   
    Si noti che quando si seleziona questa opzione, il livello di prestazioni hello viene impostato tooStandard. Archiviazione a livelli non è disponibile con livello di prestazioni Premium hello.
6. Selezionare l'opzione replication hello per account di archiviazione hello: **LRS**, **GRS**, o **RA-GRS**. valore predefinito di Hello è **RA-GRS**.
   
    Ridondanza locale = archiviazione localmente ridondante; Archiviazione con ridondanza geografica = archiviazione con ridondanza geografica (2 aree); RA-GRS è l'archiviazione con ridondanza geografica e accesso in lettura (2 aree con lettura access toohello secondo).
   
    Per altre informazioni sulle opzioni di replica di Archiviazione di Azure, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).
7. Livello di archiviazione destro selezionare hello per le proprie esigenze: hello Set **livello di accesso** tooeither **sporadico** o **Hot**. valore predefinito di Hello è **Hot**.
8. Selezionare la sottoscrizione di hello in cui si desidera toocreate hello nuovo account di archiviazione.
9. Specificare un nuovo gruppo di risorse o selezionarne uno esistente. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
10. Selezionare l'area di hello per l'account di archiviazione.
11. Fare clic su **crea** account di archiviazione toocreate hello.

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Modificare il livello di archiviazione hello di un account di archiviazione Blob tramite hello portale di Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. account di archiviazione tooyour toonavigate, selezionare tutte le risorse, quindi selezionare l'account di archiviazione.
3. Nel pannello impostazioni hello, fare clic su **configurazione** configurazione dell'account hello tooview e/o di modifica.
4. Livello di archiviazione destro selezionare hello per le proprie esigenze: hello Set **livello di accesso** tooeither **sporadico** o **Hot**.
5. Fare clic su Salva nella parte superiore di hello del pannello hello.

> [!NOTE]
> Modifica livello di archiviazione hello può comportare costi aggiuntivi. Vedere hello [prezzi e fatturazione](storage-blob-storage-tiers.md#pricing-and-billing) sezione per ulteriori dettagli.
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>La valutazione e la migrazione di account di archiviazione tooBlob
scopo di questa sezione Hello è toohelp utenti toomake una graduale transizione toousing account di archiviazione Blob. Esistono due scenari utente:

* Si dispone di un account di archiviazione generico esistente e si desidera tooevaluate tooa una modifica account di archiviazione Blob con livello di hello storage destra.
* Si è deciso di toouse un account di archiviazione Blob o già uno e desiderano tooevaluate se è necessario utilizzare il livello di archiviazione di frequente o sporadico hello.

In entrambi i casi, hello primo ordine di importanza tooestimate hello costi di archiviazione e accesso ai dati archiviati in un account di archiviazione Blob e vengono confrontati con i costi correnti.

### <a name="evaluating-blob-storage-account-tiers"></a>Valutazione dei livelli di account di archiviazione BLOB
Ordine tooestimate hello costo di archiviazione e accesso ai dati archiviati in un account di archiviazione Blob, si devono tooevaluate il modello di utilizzo esistenti o approssimativa del modello di utilizzo previsto. In generale, si desidererà tooknow:

* Utilizzo dell'archiviazione: quanti dati vengono archiviati e come cambia questo valore ogni mese?
* Il modello accesso di archiviazione - la quantità di dati è in corso di lettura e scritta toohello account (inclusi i nuovi dati)? Quante transazioni vengono usate per accedere ai dati e che di che tipi di transazioni si tratta?

#### <a name="monitoring-existing-storage-accounts"></a>Monitoraggio degli account di archiviazione esistenti
toomonitor di archiviazione esistente account e raccogliere dati, è possibile avvalersi della Analitica di archiviazione di Azure che esegue la registrazione e fornisce dati di metrica per un account di archiviazione.
Archiviazione Analitica può archiviare le metriche che includono transazioni aggregate le statistiche e dati sulla capacità toohello le richieste del servizio di archiviazione Blob per sia gli account di archiviazione generico come account di archiviazione Blob.
Questi dati vengono archiviati in tabelle note in hello stesso account di archiviazione.

Per altre informazioni, vedere [Informazioni sulle metriche di Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343258.aspx) e [Schema di tabella della metrica di Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Account di archiviazione BLOB esporre endpoint del servizio tabelle hello solo per l'archiviazione e accesso ai dati di metrica hello per tale account.
> 
> 

utilizzo dell'archiviazione hello toomonitor per hello servizio di archiviazione Blob, è necessario tooenable metrica relativi alla capacità hello.
Con questa opzione, dati relativi alla capacità vengono registrati ogni giorno per il servizio di un account di archiviazione Blob e registrati come una voce della tabella che viene scritto toohello *$MetricsCapacityBlob* tabella all'interno di hello stesso account di archiviazione.

schema di accesso dati hello toomonitor di hello servizio di archiviazione Blob, è necessario metrica oraria transazione tooenable hello a livello di API.
Con questa opzione, per ogni API le transazioni vengono aggregate ogni ora e registrate come una voce della tabella che viene scritto toohello *$MetricsHourPrimaryTransactionsBlob* tabella all'interno di hello stesso account di archiviazione. Hello *$MetricsHourSecondaryTransactionsBlob* record della tabella hello endpoint secondario toohello di transazioni in caso di account di archiviazione RA-GRS.

> [!NOTE]
> Se è disponibile un account di archiviazione per utilizzo generico in cui sono archiviati sia BLOB di pagine e dischi di macchina virtuale insieme a dati di BLOB in blocchi e di aggiunta, questo processo di stima non è applicabile. In questo modo è non possibile in alcun modo di distinzione capacità e delle transazioni le metriche basate solo sul tipo hello del blob per bloccano e aggiungere oggetti BLOB che può essere eseguita la migrazione tooa account di archiviazione Blob.
> 
> 

tooget una buona approssimazione del modello di accesso e utilizzo dei dati, è consigliabile scegliere un periodo di memorizzazione per le metriche di hello rappresentativo relativa all'utilizzo normale ed estrapolare.
Un'opzione è tooretain dati di metrica hello per 7 giorni e i dati di hello raccogliere ogni settimana, per l'analisi alla fine hello hello mese.
Un'altra opzione è ultimi 30 giorni di dati di metrica hello tooretain per hello e raccogliere e analizzare dati hello alla fine di hello del periodo di 30 giorni hello.

Per informazioni dettagliate sull'abilitazione, la raccolta e la visualizzazione dei dati di metrica, vedere, [Abilitazione della metrica di archiviazione di Azure e visualizzazione dei dati di metrica](storage-enable-and-view-metrics.md).

> [!NOTE]
> Anche l'archiviazione, l'accesso e il download dei dati di analisi vengono addebitati come lo sono i dati utente normali.
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilizzo di costi tooestimate metriche di utilizzo
##### <a name="storage-costs"></a>Costi di archiviazione
Hello ultima voce nella tabella delle metriche di capacità hello *$MetricsCapacityBlob* con la chiave di riga hello *'data'* Mostra hello capacità di archiviazione utilizzata dai dati utente.
Hello ultima voce nella tabella delle metriche di capacità hello *$MetricsCapacityBlob* con la chiave di riga hello *'analitica'* Mostra hello capacità di archiviazione utilizzata dai registri analitica hello.

Questa capacità totale utilizzata per entrambi i log di analitica e dati utente (se abilitati) può quindi essere tooestimate hello costo della memorizzazione dei dati nell'account di archiviazione hello utilizzato.
Hello stesso metodo utilizzabili per la stima dei costi di archiviazione per il blocco e aggiungere oggetti BLOB negli account di archiviazione generico.

##### <a name="transaction-costs"></a>Costi di transazione
somma Hello *'TotalBillableRequests'*, in tutte le voci per un'API in transazione hello tabella delle metriche indica numero totale di hello di transazioni dell'API particolare. *ad esempio*, numero totale di hello *'GetBlob'* le transazioni in un periodo specifico possono essere calcolate dalla somma di hello delle richieste fatturabili totali per tutte le voci con la chiave di riga hello *' utente. GetBlob'*.

Ordine tooestimate dei costi di transazione per l'account di archiviazione Blob, è necessario toobreak verso il basso le transazioni hello in tre gruppi poiché essi vengono determinati in modo diverso.

* Transazioni di scrittura, ad esempio *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* e *'CopyBlob'*.
* Transazioni di eliminazione, ad esempio *'DeleteBlob'* e *'DeleteContainer'*.
* Tutte le altre transazioni.

Ordine tooestimate dei costi di transazione per gli account di archiviazione generico, è necessario tooaggregate tutte le transazioni, indipendentemente dalla hello operazione/API.

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Costi di trasferimento dati con replica geografica e di accesso ai dati
Mentre analitica di archiviazione non fornisce quantità hello di dati sono leggervi e scritto tooa account di archiviazione, è possibile stimare approssimativamente esaminando tabella delle metriche di transazione hello.
somma Hello *'TotalIngress'* tra tutte le voci per un'API nella metrica di transazione hello tabella indica hello totale in ingresso in byte dei dati per quel particolare API.
Allo stesso modo hello somma *'TotalEgress'* indica hello quantità totale di dati in uscita, in byte.

Ordine tooestimate hello dati accesso dei costi per gli account di archiviazione Blob, sarà necessario toobreak verso il basso le transazioni hello in due gruppi.

* è possibile stimare quantità Hello dei dati recuperati dall'account di archiviazione hello esaminando sommando hello *'TotalEgress'* per principalmente hello *'GetBlob'* e *'CopyBlob'* operazioni.
* quantità di Hello di dati scritti toohello account di archiviazione può essere stimata esaminando sommando hello *'TotalIngress'* per principalmente hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* e *'AppendBlock'* operazioni.

Hello costi di trasferimento dati-replica geografica per gli account di archiviazione possono inoltre essere calcolati usando stima hello per quantità hello di dati scritti in caso di un account di archiviazione GRS o RA-GRS Blob.

> [!NOTE]
> Per un esempio più dettagliato sul calcolo dei costi di hello per l'utilizzo di livello di archiviazione di frequente o sporadico hello, per dare un'occhiata hello domanda *'quali sono i livelli di accesso a caldo e Cool e come è necessario determinare quali uno toouse'?* in hello [pagina prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).
> 
> 

### <a name="migrating-existing-data"></a>Migrazione di dati esistenti
Un account di archiviazione BLOB serve per archiviare solo BLOB in blocchi e BLOB di aggiunta. Account di archiviazione generico esistenti, che consentono di toostore tabelle, code, i file e i dischi, nonché BLOB, non può essere convertito tooBlob gli account di archiviazione. toouse hello livelli di archiviazione, sarà anche necessario toocreate nuovi account di archiviazione Blob ed eseguire la migrazione dei dati esistenti nell'account hello appena creato.

È possibile utilizzare i seguenti dati esistenti di metodi toomigrate in account di archiviazione Blob da dispositivi di archiviazione locale, dal provider di archiviazione cloud di terze parti o dagli account di archiviazione generico esistenti in Azure hello:

#### <a name="azcopy"></a>AzCopy
AzCopy è un'utilità della riga di comando di Windows progettata per prestazioni elevate copia dei dati tooand da archiviazione di Azure. È possibile utilizzare dati toocopy AzCopy nell'account di archiviazione Blob dall'account di archiviazione generico esistenti o tooupload dai dispositivi di archiviazione locale all'account di archiviazione Blob.

Per ulteriori informazioni, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

#### <a name="data-movement-library"></a>Libreria di spostamento dei dati
Libreria di spostamento dei dati di archiviazione Azure per .NET è basata su hello core data movement framework che alimenta AzCopy. libreria Hello è progettata per prestazioni elevate, tooAzCopy simili operazioni di trasferimento di dati semplici e affidabili. In questo modo tootake tutti i vantaggi di hello funzionalità AzCopy nell'applicazione in modo nativo senza toodeal con in esecuzione e il monitoraggio di istanze esterne di AzCopy.

Per altre dettagli, vedere [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)

#### <a name="rest-api-or-client-library"></a>API REST o libreria client
È possibile creare un'applicazione personalizzata di toomigrate i dati in un account di archiviazione Blob mediante una delle librerie client di Azure hello o hello API REST di servizi di archiviazione di Azure. Archiviazione di Azure fornisce librerie client avanzate per più linguaggi e piattaforme, ad esempio .NET, Java, C++, Node.js, PHP, Ruby e Python. le librerie client Hello offrono funzionalità avanzate come la logica di riesecuzione, registrazione e Caricamenti paralleli. È inoltre possibile sviluppare direttamente su hello API REST, che può essere chiamato da qualsiasi linguaggio che effettua le richieste HTTP/HTTPS.

Per altri dettagli, vedere [Introduzione all'archivio BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> BLOB crittografato con la crittografia lato client archiviare metadati relative a crittografia archiviati con blob hello. È essenziale che qualsiasi meccanismo di copia è necessario assicurarsi che i metadati del blob, hello particolarmente hello metadati correlati alla crittografia, vengono mantenuti. Se si copiano BLOB hello senza metadati, il contenuto di blob hello non sarà più recuperabile. Per informazioni dettagliate sui metadati correlati alla crittografia, vedere [Crittografia lato client per Archiviazione di Azure](storage-client-side-encryption.md).
> 
> 

## <a name="faqs"></a>Domande frequenti
1. **Gli account di archiviazione esistenti sono ancora disponibili?**
   
    Sì, gli account di archiviazione esistenti sono ancora disponibili e non hanno subito variazioni di prezzo o di funzionalità.  Non dispongono hello possibilità toochoose un livello di archiviazione ma non dispongano di funzionalità di suddivisione in livelli in hello future.
2. **Perché e quando iniziare a usare gli account di archiviazione BLOB?**
   
    Account di archiviazione BLOB sono specializzati per l'archiviazione BLOB e consentono di toointroduce nuove funzionalità basate su blob. In futuro, account di archiviazione Blob sono hello consigliato modo per l'archiviazione di BLOB, le funzionalità future quali archiviazione gerarchica e suddivisione in livelli verrà introdotte in base a questo tipo di conto. È invece backup tooyou quando si desidera toomigrate in base alle esigenze aziendali.
3. **È possibile convertire il tooa di account di archiviazione account di archiviazione Blob esistente?**
   
    No. Account di archiviazione BLOB è un tipo di account di archiviazione diverso e sarà necessario toocreate è nuovo e la migrazione dei dati, come descritto in precedenza.
4. **È possibile archiviare gli oggetti in due livelli di archiviazione in hello stesso account?**
   
    Hello *'Livello di accesso'* attributo che indica il livello di archiviazione hello è impostato un livello di account e si applica a oggetti tooall in tale account. È possibile impostare l'attributo di livello di accesso hello a livello di oggetto.
5. **È possibile modificare il livello di archiviazione hello il Blob dell'account di archiviazione?**
   
    Sì. Si sarà in grado di toochange livello di archiviazione hello dall'impostazione hello *'Livello di accesso'* attributo nell'account di archiviazione hello. Modifica livello di archiviazione hello applicherà tooall archiviati nell'account hello. Livello di archiviazione hello modifica da toocool a caldo non genererà eventuali addebiti, durante la modifica da toohot sporadico comporteranno un per costo GB per la lettura di tutti i dati nell'account hello hello.
6. **Frequenza con cui è possibile modificare il livello di archiviazione hello il Blob dell'account di archiviazione?**
   
    Anche se non si applica una limitazione per la frequenza con cui può essere modificato il livello di archiviazione di hello, tenere presente che modifica il livello di archiviazione hello da toohot sporadico daranno luogo ad addebiti significativi. Non è consigliabile modificare il livello di archiviazione hello frequentemente.
7. **BLOB hello nel livello di archiviazione sporadico hello comporterà in modo diverso rispetto a quelli nel livello di archiviazione a caldo hello hello?**
   
    I BLOB nel livello di archiviazione a caldo hello prevedono hello latenza stesso come BLOB negli account di archiviazione generico. I BLOB nel livello di archiviazione sporadico hello con una latenza simile (in millisecondi) come BLOB negli account di archiviazione generico.
   
    BLOB nel livello di archiviazione sporadico hello avrà un leggermente disponibilità del servizio (SLA) più basso hello BLOB archiviati nel livello di archiviazione a caldo di hello. Per informazioni dettagliate, vedere [Contratto di Servizio per Archiviazione](https://azure.microsoft.com/support/legal/sla/storage).
8. **È possibile archiviare i BLOB di pagine e i dischi delle macchine virtuali negli account di archiviazione BLOB?**
   
    Gli account di archiviazione BLOB supportano solo i BLOB in blocchi e i BLOB di aggiunta, non i BLOB di pagine. Dischi di macchina virtuale di Azure sono supportati da BLOB di pagine e di conseguenza gli account di archiviazione Blob non possono essere utilizzato toostore dischi della macchina virtuale. È tuttavia possibile toostore backup di dischi di macchina virtuale hello come BLOB in blocchi in un account di archiviazione Blob.
9. **È necessario toochange l'account di archiviazione Blob di toouse applicazioni esistente?**
   
    Gli account di archiviazione BLOB offrono una coerenza API al 100% con gli account di archiviazione di uso generico per i BLOB in blocchi e i BLOB di aggiunta. Fino a quando l'applicazione utilizza i BLOB in blocchi o BLOB di aggiunta e si utilizza versione 2014-02-14 hello di hello [API REST di servizi di archiviazione](https://msdn.microsoft.com/library/azure/dd894041.aspx) o versione successiva l'applicazione funziona. Se si utilizza una versione precedente del protocollo hello, quindi occorre tooupdate la nuova versione hello toouse applicazione in modo da toowork senza problemi con entrambi i tipi di account di archiviazione. In generale, è consigliabile sempre utilizzare indipendentemente dal tipo di account di archiviazione è utilizzare la versione più recente hello.
10. **L'esperienza utente sarà diversa?**
    
    Account di archiviazione BLOB sono molto simili tooa generico account di archiviazione per l'archiviazione a blocchi e BLOB di aggiunta e supportano tutte le funzionalità chiave hello dell'archiviazione di Azure, inclusi l'affidabilità e disponibilità, scalabilità, prestazioni e sicurezza. Diverso da hello caratteristiche e restrizioni specifiche tooBlob account di archiviazione e relativi livelli di archiviazione indicati sopra, tutto ciò che resta altro hello stesso.

## <a name="next-steps"></a>Passaggi successivi
### <a name="evaluate-blob-storage-accounts"></a>Valutare gli account di archiviazione BLOB
[Verificare la disponibilità degli account di archiviazione BLOB in base all'area](https://azure.microsoft.com/regions/#services)

[Valutare l'utilizzo degli account di archiviazione attuali abilitando le metriche di Archiviazione di Azure](storage-enable-and-view-metrics.md)

[Verificare i prezzi di Archiviazione di Azure per i BLOB in base all'area](https://azure.microsoft.com/pricing/details/storage/)

[Verificare i prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Iniziare a usare gli account di archiviazione BLOB
[Introduzione all'archivio BLOB di Azure](storage-dotnet-how-to-use-blobs.md)

[Lo spostamento di dati tooand da archiviazione di Azure](storage-moving-data.md)

[Trasferimento dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md)

[Visualizzare ed esplorare gli account di archiviazione](http://storageexplorer.com/)

