---
title: aaaAzure a caldo, raffreddare e lo spazio di archiviazione per i BLOB | Documenti Microsoft
description: Livelli di archiviazione ad accesso frequente, ad accesso sporadico e archivio per account di archiviazione BLOB di Azure.
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
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente, ad accesso sporadico e archivio (anteprima)

## <a name="overview"></a>Panoramica

Archiviazione di Azure offre tre livelli di archiviazione per l'archivio di oggetti BLOB, per consentire di archiviare i dati nel modo economicamente più conveniente in base alla modalità d'uso. Hello Azure **livello di archiviazione a caldo** è ottimizzato per l'archiviazione dei dati che si accede frequentemente. Hello Azure **livello di archiviazione sporadico** è ottimizzato per l'archiviazione dei dati che raramente accesso e archiviati per almeno un mese. Hello [il livello di archiviazione di archivio (anteprima)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) è ottimizzato per l'archiviazione dei dati che raramente accesso e archiviati per almeno sei mesi con i requisiti di latenza flessibile (in ordine di hello di ore). Hello *archivio* livello di archiviazione sono utilizzabili solo a livello di blob hello e non sugli account di archiviazione intero hello. Dati nel livello di archiviazione sporadico hello in grado di tollerare disponibilità leggermente inferiore, ma richiede comunque una durabilità elevata e caratteristiche simili di velocità effettiva e tempo per l'accesso come dati attivi. Per i dati ad accesso sporadico e di archivio, contratti di servizio con una disponibilità leggermente più bassa e costi di accesso più elevati sono compromessi accettabili in cambio di costi di archiviazione molto più bassi.

Oggi, i dati archiviati nel cloud hello sta crescendo a un ritmo esponenziale. toomanage costi per le esigenze di archiviazione di espansione, è utile tooorganize in base agli attributi come frequenza di accesso e pianificato periodo di memorizzazione dei dati. Dati archiviati nel cloud hello possono essere diversi in termini di come viene generato, elaborato e accessibili tramite la relativa durata. Alcuni dati presentano accessi attivi e modifiche continue nel corso della rispettiva durata. Alcuni dati si accede frequentemente in anticipo il ciclo di vita, con accesso eliminazione drasticamente come hello dati età. Alcuni dati rimangono inattivi nel cloud hello e raramente, se mai eseguito una volta archiviati.

Tutti questi scenari di accesso ai dati usufruiscono di un livello differenziato di archiviazione, ottimizzato per un particolare modello di accesso. Con i livelli di archiviazione ad accesso frequente, ad accesso sporadico e archivio, l'archivio BLOB di Azure soddisfa l'esigenza di avere livelli di archiviazione differenziati con modelli di determinazione prezzi distinti.

## <a name="blob-storage-accounts"></a>Account di archiviazione BLOB

**Account di archiviazione BLOB** sono account di archiviazione specializzati per l'archiviazione dei dati non strutturati come BLOB (oggetti) in Archiviazione di Azure. Con l'account di archiviazione Blob, è quindi possibile scegliere tra a caldo e livelli di archiviazione sporadico a livello di account o a caldo, interessanti e archiviare i livelli a livello di blob hello, in base ai modelli di accesso. Archiviare i dati ad accesso sporadico a cui si accede raramente nel hello più basso costo di archiviazione, meno dati sporadico utilizzati di frequente in un'archiviazione inferiore rispetto a caldo e archiviare dati attivi a cui si accede più frequentemente hello più basso costo di accesso di costo. Account di archiviazione BLOB sono account di archiviazione generico esistenti tooyour simile e condividono tutti durabilità grande hello, disponibilità, scalabilità e funzionalità che si utilizza oggi, tra cui la coerenza delle API del 100% per i BLOB in blocchi e aggiungere BLOB.

> [!NOTE]
> Gli account di archiviazione BLOB supportano solo i BLOB in blocchi e i BLOB di aggiunta, non i BLOB di pagine.

Account di archiviazione BLOB esporre hello **livello di accesso** attributo, che consente a livello di archiviazione hello toospecify come **Hot** o **sporadico** a seconda dei dati di hello archiviati in hello account. Se viene apportata una modifica nel modello di utilizzo di hello dei dati, è anche possibile passare tra questi livelli di archiviazione in qualsiasi momento. il livello di archiviazione Hello (anteprima) è applicabile solo a livello di blob hello.

> [!NOTE]
> Modifica livello di archiviazione hello può comportare costi aggiuntivi. Vedere hello [determinazione dei prezzi e fatturazione](#pricing-and-billing) sezione per ulteriori dettagli.

### <a name="hot-access-tier"></a>Livello di accesso frequente

Scenari di utilizzo di esempio per il livello di archiviazione a caldo di hello includono:

* Dati a cui sono in uso attivo o toobe previsto accede (lettura da e scritti) frequentemente.
* Dati che sono preconfigurati per l'elaborazione e l'eventuale livello di archiviazione sporadico toohello di migrazione.

### <a name="cool-access-tier"></a>Livello di accesso sporadico

Scenari di utilizzo di esempio per il livello di archiviazione sporadico hello includono:

* Set di dati di backup e ripristino di emergenza a breve termine.
* Contenuti multimediali precedenti non visualizzati più frequentemente, ma sono previsto toobe disponibile immediatamente quando si accede.
* Grandi set di dati che devono toobe archiviati in modo efficace costo mentre raccolte più dati per l'elaborazione futura. *ad esempio*, archiviazione a lungo termine di dati scientifici, dati di telemetria non elaborati di un impianto di produzione.

### <a name="archive-access-tier-preview"></a>Livello di accesso archivio (anteprima)

[Spazio di archiviazione](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) con i costi di archiviazione minimo hello superiore toohot costi rispetto il recupero di dati e archiviazione sporadico.

Se un BLOB si trova nel livello archivio, non è possibile leggerlo, copiarlo, sovrascriverlo, modificarlo o creare snapshot del BLOB. Tuttavia, si potrebbe utilizzare toodelete operazioni esistenti, elenco, ottenere le proprietà o i metadati del blob o modificare livello hello del blob di. dati tooread in spazio di archiviazione, è innanzitutto necessario modificare il livello di hello di hello blob toohot o cool. Questo processo è noto come reidratazione e può richiedere fino a too15 ore toocomplete per BLOB è minore di 50 GB. Tempo aggiuntivo necessario per i BLOB di dimensioni maggiori varia con limite di velocità effettiva di hello blob.

Durante la riattivazione, è possibile controllare hello "stato di archiviazione" blob proprietà tooconfirm se è stato modificato a livello di hello. stato Hello legge "reidratare-in sospeso-a-hot" o "reidratare-in sospeso-a-cool" in base al livello di destinazione hello. Dopo il completamento, hello "archiviare lo stato" proprietà blob verrà rimossa e hello "livello di accesso" proprietà blob riflette il livello di frequente o sporadico hello.  

Scenari di utilizzo di esempio per il livello di archiviazione di archivio hello includono:

* Set di dati di backup, archiviazione e ripristino di emergenza a lungo termine
* Dati originali (non elaborati) che devono essere conservati, anche dopo che sono stati elaborati in un formato utilizzabile finale, *ad esempio*, file multimediali non elaborati dopo la transcodifica in altri formati.
* Conformità e dell'archivio dati che deve toobe archiviati per lungo tempo e si accede quasi. *ad esempio*, filmati di videocamere di sicurezza, vecchie radiografie/risonanze magnetiche per le organizzazioni sanitarie, registrazioni audio e trascrizioni di chiamate di clienti per i servizi finanziari.

### <a name="recommendations"></a>Raccomandazioni

Per informazioni sugli account di archiviazione, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) .

Per le applicazioni che richiedono solo bloccano o si accodano nell'archiviazione blob, è consigliabile utilizzare account di archiviazione Blob, tootake sfruttare hello si differenzino solo modello di determinazione dei prezzi di archiviazione a livelli. È presente, tuttavia, che questo potrebbe non essere possibile in determinate circostanze in cui utilizza l'archiviazione generica account sarebbe hello toogo modo, ad esempio:

* È necessario toouse tabelle, code, o i file e si desidera che i BLOB archiviati in hello stesso account di archiviazione. Si noti che non vi sia alcun vantaggio dalle tecniche di toostoring in hello che stesso account diverso con hello stesso chiavi condivise.

* È comunque necessario modello di distribuzione classica toouse hello. Sono disponibili tramite modello di distribuzione Azure Resource Manager hello solo account di archiviazione BLOB.

* È necessario toouse BLOB di pagine. Gli account di archiviazione BLOB non supportano i BLOB di pagine. A meno che non vi siano esigenze specifiche per usare i BLOB di pagine, è consigliabile usare i BLOB in blocchi.

* Si utilizza una versione di hello [API REST di servizi di archiviazione](https://msdn.microsoft.com/library/azure/dd894041.aspx) che è precedente a 2014-02-14 o una libreria client con una versione inferiore a 4. x e non può aggiornare l'applicazione.

> [!NOTE]
> Gli account di archiviazione BLOB sono attualmente supportati in tutte le aree di Azure.
 

## <a name="blob-level-tiering-feature-preview"></a>Funzionalità di suddivisione in livelli a livello di BLOB (anteprima)

BLOB a livello di suddivisione in livelli consente ora livello hello toochange dei dati a livello di oggetto hello utilizzando una singola operazione chiamata [impostare livello Blob](/rest/api/storageservices/set-blob-tier). È possibile modificare facilmente hello livello di accesso di un blob tra hello a caldo, sporadico o livelli di archiviazione come modifica di modelli di utilizzo, senza dati toomove tra gli account. Tutte le modifiche ai livelli sono immediate, ad eccezione della riattivazione di un BLOB dal livello archivio. BLOB in tutti gli archivi di tre livelli possono coesistere all'interno di hello stesso account. Tutti i blob che non dispone di un livello in modo esplicito assegnato eredita livello hello impostazione livello di accesso account hello.

toouse queste funzionalità in anteprima, seguire le istruzioni hello hello [annuncio sul blog di archiviazione di Azure e Blob a livello di suddivisione in livelli](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering).

Seguire Hello sono elencate alcune restrizioni da applicare durante l'anteprima per la suddivisione in livelli a livello di blob:

* Il livello archivio è supportato solo nei nuovi account di archiviazione BLOB creati nell'area Stati Uniti orientali 2 dopo la registrazione dell'anteprima.

* La suddivisione in livelli a livello di BLOB è supportata solo nei nuovi account di archiviazione BLOB creati in aree pubbliche dopo la registrazione dell'anteprima.

* La suddivisione in livelli a livello di BLOB e il livello archivio sono supportati unicamente nell'[archiviazione con ridondanza locale] (../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage). [Archiviazione con ridondanza geografica](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) e [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) sarà supportato in hello future.

* Non è possibile modificare il livello di hello di un blob con snapshot.

* Non è possibile copiare o creare uno snapshot di un BLOB nel livello archivio.

## <a name="comparison-of-hello-storage-tiers"></a>Confronto tra i livelli di archiviazione hello

Hello nella tabella seguente viene illustrato un confronto tra i livelli di archiviazione di frequente e sporadico hello. livello a livello di blob di archiviazione Hello non è in anteprima, pertanto vi sono contratti di servizio per il.

| | **Livello di archiviazione ad accesso frequente** | **Livello di archiviazione ad accesso sporadico** |
| ---- | ----- | ----- |
| **Disponibilità** | 99,9% | 99% |
| **Disponibilità** <br> **(letture RA-GRS)**| 99,99% | 99,9% |
| **Costi di utilizzo** | Costi di archiviazione più elevati e costi di accesso e transazione più bassi | Costi di archiviazione più bassi e costi di accesso e transazione più elevati |
| **Dimensioni minime oggetti** | N/D | N/D |
| **Durata archiviazione minima** | N/D | N/D |
| **Latency** <br> **(Tempo toofirst byte)** | millisecondi | millisecondi |
| **Obiettivi di scalabilità e prestazioni** | Uguali a quelli degli account di archiviazione di uso generico | Uguali a quelli degli account di archiviazione di uso generico |

> [!NOTE]
> Archiviazione BLOB account hello supporto stesso destinazioni di prestazioni e scalabilità, come gli account di archiviazione generico. Per ulteriori informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) .


## <a name="pricing-and-billing"></a>Prezzi e fatturazione
Account di archiviazione BLOB usano un modello di determinazione dei prezzi per l'archiviazione di blob in base a livello di archiviazione hello. Quando si utilizza un account di archiviazione Blob, si applica hello fatturazione considerazioni seguenti:

* **I costi di archiviazione**: inoltre toohello quantità di dati archiviati, il costo di hello archiviazione dei dati varia a seconda di livello di archiviazione hello. costo per gigabyte Hello è inferiore per livello di archiviazione sporadico hello rispetto a livello di archiviazione a caldo di hello.

* **I costi di accesso ai dati**: per i dati nel livello di archiviazione sporadico hello, viene effettuato un addebito di accesso ai dati per gigabyte per letture e scritture.

* **Costi di transazione**: è previsto un addebito per ogni transazione per entrambi i livelli. Tuttavia, il costo per transazione hello per il livello di archiviazione sporadico hello è superiore a quello per il livello di archiviazione a caldo di hello.

* **Costi di trasferimento dei dati di replica geografica**: si applica solo tooaccounts con la replica geografica configurata, tra cui GRS e RA-GRS. Il trasferimento dati con la replica geografica comporta un addebito per gigabyte.

* **Costi di trasferimento dati in uscita**: i trasferimenti dati in uscita (dati che vengono trasferiti al di fuori di un'area di Azure) vengono fatturati in base all'utilizzo di larghezza di banda per singolo gigabyte, come per gli account di archiviazione di uso generico.

* **Modifica livello di archiviazione hello**: modifica il livello di archiviazione hello da toohot sporadico comporta un tooreading uguale carica tutti i dati di hello esistenti nell'account di archiviazione hello per ogni transizione. In hello invece modificare il livello di archiviazione hello da toocool a caldo è gratuitamente.

> [!NOTE]
> Per altri dettagli sui prezzi per gli account di archiviazione Blob hello, vedere [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) pagina. Per ulteriori informazioni sugli addebiti di trasferimento dati in uscita hello, vedere [dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/) pagina.

## <a name="quickstart"></a>Guida introduttiva

In questa sezione viene descritto come hello seguenti scenari con hello portale di Azure:

* Come toocreate un account di archiviazione Blob.
* Come toomanage un account di archiviazione Blob.

Non è possibile impostare tooarchive livello di accesso hello in hello seguono esempi poiché questa impostazione si applica l'account di archiviazione intero toohello. Il livello archivio può essere impostato solo per un BLOB specifico.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Creare un account di archiviazione Blob tramite hello portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel menu Hub hello, selezionare **New** > **dati e archiviazione** > **account di archiviazione**.

3. Immettere un nome per l'account di archiviazione.
   
    Questo nome deve essere globalmente univoco. viene utilizzato come parte dell'URL hello oggetti hello tooaccess nell'account di archiviazione hello.  

4. Selezionare **Gestione risorse** come modello di distribuzione hello.
   
    Archiviazione a livelli può essere utilizzato solo con gli account di archiviazione di gestione delle risorse; si tratta di hello consigliata il modello di distribuzione di nuove risorse. Per ulteriori informazioni, consultare hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).  

5. Nell'elenco a discesa tipo di Account di hello, selezionare **nell'archiviazione Blob**.
   
    Questo è possibile specificare il tipo di hello dell'account di archiviazione. Archiviazione a livelli non è disponibile in spazio di memorizzazione generica. è disponibile solo in hello account di tipo di archiviazione Blob.     
   
    Si noti che quando si seleziona questa opzione, il livello di prestazioni hello viene impostato tooStandard. Archiviazione a livelli non è disponibile con livello di prestazioni Premium hello.

6. Selezionare l'opzione replication hello per account di archiviazione hello: **LRS**, **GRS**, o **RA-GRS**. valore predefinito di Hello è **RA-GRS**.
   
    Ridondanza locale = archiviazione localmente ridondante; Archiviazione con ridondanza geografica = archiviazione con ridondanza geografica (2 aree); RA-GRS è l'archiviazione con ridondanza geografica e accesso in lettura (2 aree con lettura access toohello secondo).
   
    Per altre informazioni sulle opzioni di replica di Archiviazione di Azure, vedere [Replica di Archiviazione di Azure](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

7. Livello di archiviazione destro selezionare hello per le proprie esigenze: hello Set **livello di accesso** tooeither **sporadico** o **Hot**. valore predefinito di Hello è **Hot**. 

8. Selezionare la sottoscrizione di hello in cui si desidera toocreate hello nuovo account di archiviazione.

9. Specificare un nuovo gruppo di risorse o selezionarne uno esistente. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

10. Selezionare l'area di hello per l'account di archiviazione.

11. Fare clic su **crea** account di archiviazione toocreate hello.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Modificare il livello di archiviazione hello di un account di archiviazione Blob tramite hello portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. account di archiviazione tooyour toonavigate, selezionare tutte le risorse, quindi selezionare l'account di archiviazione.

3. Nel pannello impostazioni hello, fare clic su **configurazione** configurazione dell'account hello tooview e/o di modifica.

4. Livello di archiviazione destro selezionare hello per le proprie esigenze: hello Set **livello di accesso** tooeither **sporadico** o **Hot**...

5. Fare clic su Salva nella parte superiore di hello del pannello hello.

> [!NOTE]
> Modifica livello di archiviazione hello può comportare costi aggiuntivi. Vedere hello [prezzi e fatturazione](#pricing-and-billing) sezione per ulteriori dettagli.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>La valutazione e la migrazione di account di archiviazione tooBlob
scopo di questa sezione Hello è toohelp utenti toomake una graduale transizione toousing account di archiviazione Blob. Esistono due scenari utente:

* Si dispone di un account di archiviazione generico esistente e si desidera tooevaluate tooa una modifica account di archiviazione Blob con livello di hello storage destra.
* Si è deciso di toouse un account di archiviazione Blob o già uno e desiderano tooevaluate se è necessario utilizzare il livello di archiviazione di frequente o sporadico hello.

In entrambi i casi, hello primo ordine di importanza tooestimate hello costi di archiviazione e accesso ai dati archiviati in un account di archiviazione Blob e vengono confrontati con i costi correnti.

## <a name="evaluating-blob-storage-account-tiers"></a>Valutazione dei livelli di account di archiviazione BLOB

Ordine tooestimate hello costo di archiviazione e accesso ai dati archiviati in un account di archiviazione Blob, è necessario tooevaluate il modello di utilizzo esistenti o approssimativa del modello di utilizzo previsto. In generale, si desidera tooknow:

* Utilizzo dell'archiviazione: quanti dati vengono archiviati e come cambia questo valore ogni mese?

* Il modello accesso di archiviazione - la quantità di dati è in corso di lettura e scritta toohello account (inclusi i nuovi dati)? Quante transazioni vengono usate per accedere ai dati e che di che tipi di transazioni si tratta?

## <a name="monitoring-existing-storage-accounts"></a>Monitoraggio degli account di archiviazione esistenti

toomonitor di archiviazione esistente account e raccogliere dati, è possibile avvalersi della Analitica di archiviazione di Azure che esegue la registrazione e fornisce dati di metrica per un account di archiviazione. Archiviazione Analitica può archiviare le metriche che includono transazioni aggregate le statistiche e dati sulla capacità toohello le richieste del servizio di archiviazione Blob per sia gli account di archiviazione generico come account di archiviazione Blob. Questi dati vengono archiviati in tabelle note in hello stesso account di archiviazione.

Per altre informazioni, vedere [Informazioni sulle metriche di Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343258.aspx) e [Schema di tabella della metrica di Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Account di archiviazione BLOB esporre endpoint del servizio tabelle hello solo per l'archiviazione e accesso ai dati di metrica hello per tale account.

utilizzo dell'archiviazione hello toomonitor per hello servizio di archiviazione Blob, è necessario tooenable metrica relativi alla capacità hello.
Con questa opzione, dati relativi alla capacità vengono registrati ogni giorno per il servizio di un account di archiviazione Blob e registrati come una voce della tabella che viene scritto toohello *$MetricsCapacityBlob* tabella all'interno di hello stesso account di archiviazione.

schema di accesso dati hello toomonitor di hello servizio di archiviazione Blob, è necessario metrica oraria transazione tooenable hello a livello di API. Con questa opzione, per ogni API le transazioni vengono aggregate ogni ora e registrate come una voce della tabella che viene scritto toohello *$MetricsHourPrimaryTransactionsBlob* tabella all'interno di hello stesso account di archiviazione. Hello *$MetricsHourSecondaryTransactionsBlob* record della tabella hello endpoint secondario toohello di transazioni quando si utilizza l'account di archiviazione RA-GRS.

> [!NOTE]
> Se è disponibile un account di archiviazione per utilizzo generico in cui sono archiviati sia BLOB di pagine e dischi di macchina virtuale insieme a dati di BLOB in blocchi e di aggiunta, questo processo di stima non è applicabile. In questo modo non si dispone di alcun modo per distinguere la capacità e delle transazioni le metriche basate solo sul tipo hello del blob per blocchino e BLOB di aggiunta, che può essere eseguita la migrazione tooa account di archiviazione Blob.

tooget una buona approssimazione del modello di accesso e utilizzo dei dati, è consigliabile scegliere un periodo di memorizzazione per le metriche di hello rappresentativo relativa all'utilizzo normale ed estrapolare. Un'opzione è tooretain dati di metrica hello per 7 giorni e i dati di hello raccogliere ogni settimana, per l'analisi alla fine hello hello mese. Un'altra opzione è ultimi 30 giorni di dati di metrica hello tooretain per hello e raccogliere e analizzare dati hello alla fine di hello del periodo di 30 giorni hello.

Per informazioni dettagliate sull'abilitazione, la raccolta e la visualizzazione dei dati di metrica, vedere [Abilitazione di Metriche di archiviazione di Azure e visualizzazione dei dati delle metriche](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

> [!NOTE]
> Anche l'archiviazione, l'accesso e il download dei dati di analisi vengono addebitati come avviene per i dati utente normali.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilizzo di costi tooestimate metriche di utilizzo

### <a name="storage-costs"></a>Costi di archiviazione

Hello ultima voce nella tabella delle metriche di capacità hello *$MetricsCapacityBlob* con la chiave di riga hello *'data'* Mostra hello capacità di archiviazione utilizzata dai dati utente. Hello ultima voce nella tabella delle metriche di capacità hello *$MetricsCapacityBlob* con la chiave di riga hello *'analitica'* Mostra hello capacità di archiviazione utilizzata dai registri analitica hello.

Questa capacità totale utilizzata per entrambi i log di analitica e dati utente (se abilitati) può quindi essere tooestimate hello costo della memorizzazione dei dati nell'account di archiviazione hello utilizzato. Hello stesso metodo utilizzabili per la stima dei costi di archiviazione per il blocco e aggiungere oggetti BLOB negli account di archiviazione generico.

### <a name="transaction-costs"></a>Costi di transazione

somma Hello *'TotalBillableRequests'*, in tutte le voci per un'API in transazione hello tabella delle metriche indica numero totale di hello di transazioni dell'API particolare. *Ad esempio*, numero totale di hello *'GetBlob'* le transazioni in un periodo specifico possono essere calcolate dalla somma di hello delle richieste fatturabili totali per tutte le voci con la chiave di riga hello *' utente. GetBlob'*.

Ordine tooestimate dei costi di transazione per l'account di archiviazione Blob, è necessario toobreak verso il basso le transazioni hello in tre gruppi poiché essi vengono determinati in modo diverso.

* Transazioni di scrittura, ad esempio *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* e *'CopyBlob'*.
* Transazioni di eliminazione, ad esempio *'DeleteBlob'* e *'DeleteContainer'*.
* Tutte le altre transazioni.

Ordine tooestimate dei costi di transazione per gli account di archiviazione generico, è necessario tooaggregate tutte le transazioni, indipendentemente dalla hello operazione/API.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Costi di trasferimento dati con replica geografica e di accesso ai dati

Mentre analitica di archiviazione non fornisce quantità hello di dati sono leggervi e scritto tooa account di archiviazione, è possibile stimare approssimativamente esaminando tabella delle metriche di transazione hello. somma Hello *'TotalIngress'* tra tutte le voci per un'API nella metrica di transazione hello tabella indica hello totale in ingresso in byte dei dati per quel particolare API. Allo stesso modo hello somma *'TotalEgress'* indica hello quantità totale di dati in uscita, in byte.

Ordine tooestimate hello dati accesso dei costi per gli account di archiviazione Blob, è necessario toobreak verso il basso le transazioni hello in due gruppi. 

* è possibile stimare quantità Hello dei dati recuperati dall'account di archiviazione hello esaminando sommando hello *'TotalEgress'* per principalmente hello *'GetBlob'* e *'CopyBlob'* operazioni.

* quantità di Hello di dati scritti toohello account di archiviazione può essere stimata esaminando sommando hello *'TotalIngress'* per principalmente hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* e *'AppendBlock'* operazioni.

Hello costi di trasferimento dati-replica geografica per gli account di archiviazione possono inoltre essere calcolati usando stima hello per quantità hello dei dati scritti quando si utilizza un account di archiviazione GRS o RA-GRS Blob.

> [!NOTE]
> Per un esempio più dettagliato sul calcolo dei costi di hello per l'utilizzo di livello di archiviazione di frequente o sporadico hello, dare un'occhiata hello domanda *'quali sono i livelli di accesso a caldo e Cool e come è necessario determinare quali uno toouse'?* in hello [pagina prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).
 
## <a name="migrating-existing-data"></a>Migrazione di dati esistenti

Un account di archiviazione BLOB serve per archiviare solo BLOB in blocchi e BLOB di aggiunta. Account di archiviazione generico esistenti, che consentono di toostore tabelle, code, i file, dischi, nonché BLOB, non può essere convertito tooBlob gli account di archiviazione. toouse hello livelli di archiviazione, è necessario toocreate nuovi account di archiviazione Blob e si esegue la migrazione dei dati esistenti in account hello appena creato.

È possibile utilizzare i seguenti dati esistenti di metodi toomigrate in account di archiviazione Blob da dispositivi di archiviazione locale, dal provider di archiviazione cloud di terze parti o dagli account di archiviazione generico esistenti in Azure hello:

### <a name="azcopy"></a>AzCopy

AzCopy è un'utilità della riga di comando di Windows progettata per prestazioni elevate copia dei dati tooand da archiviazione di Azure. È possibile utilizzare dati toocopy AzCopy nell'account di archiviazione Blob dall'account di archiviazione generico esistenti o tooupload dai dispositivi di archiviazione locale all'account di archiviazione Blob.

Per ulteriori informazioni, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Libreria di spostamento dei dati

Libreria di spostamento dei dati di archiviazione Azure per .NET è basata su hello core data movement framework che alimenta AzCopy. libreria Hello è progettata per prestazioni elevate, affidabile e tooAzCopy simili operazioni di trasferimento di dati semplice. In questo modo tootake tutti i vantaggi di hello funzionalità AzCopy nell'applicazione in modo nativo senza toodeal con in esecuzione e il monitoraggio di istanze esterne di AzCopy.

Per altre dettagli, vedere [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)

### <a name="rest-api-or-client-library"></a>API REST o libreria client

È possibile creare un'applicazione personalizzata di toomigrate i dati in un account di archiviazione Blob mediante una delle librerie client di Azure hello o hello API REST di servizi di archiviazione di Azure. Archiviazione di Azure fornisce librerie client avanzate per più linguaggi e piattaforme, ad esempio .NET, Java, C++, Node.js, PHP, Ruby e Python. le librerie client Hello offrono funzionalità avanzate come la logica di riesecuzione, registrazione e Caricamenti paralleli. È inoltre possibile sviluppare direttamente su hello API REST, che può essere chiamato da qualsiasi linguaggio che effettua le richieste HTTP/HTTPS.

Per altri dettagli, vedere [Introduzione all'archivio BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> BLOB crittografato con la crittografia lato client archiviare metadati relative a crittografia archiviati con blob hello. È essenziale che qualsiasi meccanismo di copia è necessario assicurarsi che i metadati del blob, hello particolarmente hello metadati correlati alla crittografia, vengono mantenuti. Se si copiano BLOB hello senza metadati, il contenuto di blob hello non è possibile recuperare nuovamente. Per informazioni dettagliate sui metadati correlati alla crittografia, vedere [Crittografia lato client per Archiviazione di Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).
 
## <a name="faq"></a>domande frequenti

1. **Gli account di archiviazione esistenti sono ancora disponibili?**
   
    Sì, gli account di archiviazione esistenti sono ancora disponibili e non hanno subito variazioni di prezzo o di funzionalità.  Non dispongono hello possibilità toochoose un livello di archiviazione ma non dispongano di funzionalità di suddivisione in livelli in hello future.

2. **Perché e quando iniziare a usare gli account di archiviazione BLOB?**
   
    Account di archiviazione BLOB sono specializzati per l'archiviazione BLOB e consentono di toointroduce nuove funzionalità basate su blob. In futuro, account di archiviazione Blob sono hello consigliato modo per l'archiviazione di BLOB, le funzionalità future quali archiviazione gerarchica e suddivisione in livelli verrà introdotte in base a questo tipo di conto. È invece backup tooyou quando si desidera toomigrate in base alle esigenze aziendali.

3. **È possibile convertire il tooa di account di archiviazione account di archiviazione Blob esistente?**
   
    No. L'account di archiviazione BLOB è un tipo diverso di account di archiviazione ed è necessario crearne uno nuovo ed eseguire la migrazione dei dati come illustrato in precedenza.

4. **È possibile archiviare gli oggetti in due livelli di archiviazione in hello stesso account?**
   
    Hello *'Livello di accesso'* attributo indica il valore di hello del livello di archiviazione hello impostato a livello di account e si applica a oggetti tooall in tale account. Tuttavia, funzionalità di suddivisione in livelli (anteprima) di hello a livello di blob consentirà si tooset hello livello di accesso sui blob specifico e questo percorso sostituirà impostazione livello di accesso hello account hello. 

5. **È possibile modificare il livello di archiviazione hello il Blob dell'account di archiviazione?**
   
    Sì. È possibile modificare il livello di archiviazione hello impostazione hello *'Livello di accesso'* attributo nell'account di archiviazione hello. Modifica livello di archiviazione hello applica tooall archiviati nell'account hello. Modifica livello di archiviazione hello da toocool attivo non è soggetta a eventuali addebiti, durante la modifica da toohot sporadico comportano un per costo GB per la lettura di tutti i dati nell'account hello hello.

6. **Frequenza con cui è possibile modificare il livello di archiviazione hello il Blob dell'account di archiviazione?**
   
    Anche se non si applica una limitazione per la frequenza con cui può essere modificato il livello di archiviazione di hello, tenere presente che modifica il livello di archiviazione hello da toohot sporadico può comportare costi significativi. Non è consigliabile modificare il livello di archiviazione hello frequentemente.

7. **BLOB hello nel livello di archiviazione sporadico hello si comportano in modo diverso rispetto a quelli nel livello di archiviazione a caldo hello hello?**
   
    I BLOB nel livello di archiviazione a caldo hello prevedono hello latenza stesso come BLOB negli account di archiviazione generico. I BLOB nel livello di archiviazione sporadico hello con una latenza simile (in millisecondi) come BLOB negli account di archiviazione generico.
   
    BLOB nel livello di archiviazione sporadico hello hanno un livello di servizio disponibilità di leggermente inferiore (SLA) di BLOB hello archiviati nel livello di archiviazione a caldo di hello. Per informazioni dettagliate, vedere [Contratto di Servizio per Archiviazione](https://azure.microsoft.com/support/legal/sla/storage).

8. **È possibile archiviare i BLOB di pagine e i dischi delle macchine virtuali negli account di archiviazione BLOB?**
   
    Gli account di archiviazione BLOB supportano solo i BLOB in blocchi e i BLOB di aggiunta, non i BLOB di pagine. Dischi di macchina virtuale di Azure sono supportati da BLOB di pagine e di conseguenza gli account di archiviazione Blob non possono essere utilizzato toostore dischi della macchina virtuale. È tuttavia possibile toostore backup di dischi di macchina virtuale hello come BLOB in blocchi in un account di archiviazione Blob.

9. **È necessario toochange l'account di archiviazione Blob di toouse applicazioni esistente?**
   
    Gli account di archiviazione BLOB offrono una coerenza API al 100% con gli account di archiviazione di uso generico per i BLOB in blocchi e i BLOB di aggiunta. Fino a quando l'applicazione utilizza i BLOB in blocchi o BLOB di aggiunta e si utilizza versione 2014-02-14 hello di hello [API REST di servizi di archiviazione](https://msdn.microsoft.com/library/azure/dd894041.aspx) o versione successiva l'applicazione funziona. Se si utilizza una versione precedente del protocollo hello, quindi è necessario aggiornare la nuova versione hello toouse applicazione in modo da toowork perfettamente con entrambi i tipi di account di archiviazione. In generale, è consigliabile sempre utilizzare indipendentemente dal tipo di account di archiviazione è utilizzare la versione più recente hello.

10. **L'esperienza utente è diversa?**
    
    Account di archiviazione BLOB sono molto simili tooa generico account di archiviazione per l'archiviazione a blocchi e BLOB di aggiunta e supportano tutte le funzionalità chiave hello dell'archiviazione di Azure, inclusi l'affidabilità e disponibilità, scalabilità, prestazioni e sicurezza. Diverso da hello caratteristiche e restrizioni specifiche tooBlob account di archiviazione e relativi livelli di archiviazione indicati sopra, tutto ciò che resta altro hello stesso.

## <a name="next-steps"></a>Passaggi successivi

### <a name="evaluate-blob-storage-accounts"></a>Valutare gli account di archiviazione BLOB

[Verificare la disponibilità degli account di archiviazione BLOB in base all'area](https://azure.microsoft.com/regions/#services)

[Valutare l'utilizzo degli account di archiviazione attuali abilitando le metriche di Archiviazione di Azure](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Verificare i prezzi di Archiviazione di Azure per i BLOB in base all'area](https://azure.microsoft.com/pricing/details/storage/)

[Verificare i prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Iniziare a usare gli account di archiviazione BLOB

[Introduzione all'archivio BLOB di Azure](storage-dotnet-how-to-use-blobs.md)

[Lo spostamento di dati tooand da archiviazione di Azure](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Trasferimento dati con l'utilità della riga di comando di AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Visualizzare ed esplorare gli account di archiviazione](http://storageexplorer.com/)