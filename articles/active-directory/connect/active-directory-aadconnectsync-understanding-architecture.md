---
title: 'Sincronizzazione di Azure AD Connect: informazioni sull''architettura di hello | Documenti Microsoft'
description: Questo argomento descrive l'architettura di hello di sincronizzazione di Azure AD Connect e hello termini utilizzati.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Sincronizzazione di Azure AD Connect: informazioni sull'architettura di hello
Questo argomento illustra l'architettura di base per la sincronizzazione di Azure AD Connect hello. In molti aspetti, è simile predecessori tooits MIIS 2003, 2007 ILM e FIM 2010. Sincronizzazione di Azure AD Connect è evoluzione hello di queste tecnologie. Se si ha familiarità con uno qualsiasi di queste tecnologie precedenti, il contenuto di hello di questo argomento sarà anche tooyou familiarità. Se si toosynchronization nuovi, in questo argomento è per l'utente. Non è tuttavia i dettagli hello tooknow requisito su toobe in questo argomento ha esito positivo nell'esecuzione di personalizzazioni tooAzure AD Connect sincronizzazione (motore di sincronizzazione denominato in questo argomento).

## <a name="architecture"></a>Architettura
il motore di sincronizzazione Hello crea una visualizzazione di oggetti archiviati in più origini dati connesse integrata e gestisce informazioni di identità in tali origini dati. Questa vista integrata è determinata dalle informazioni di identità hello recuperate dalle origini dati connesse e un set di regole che determinano la modalità tooprocess queste informazioni.

### <a name="connected-data-sources-and-connectors"></a>Origini dati connesse e connettori
il motore di sincronizzazione Hello elabora le informazioni di identità da archivi dati diversi, ad esempio Active Directory o un database di SQL Server. Ogni archivio di dati che consente di organizzare i dati in un formato di database e che fornisce i metodi standard di accesso ai dati è un candidato di origine di dati potenziale per il motore di sincronizzazione hello. archivi dati Hello sincronizzate dal motore di sincronizzazione vengono chiamati **origini dati connesse** o **connesso directory** (CD).

il motore di sincronizzazione Hello incapsula l'interazione con un'origine dati connessa all'interno di un modulo denominato un **connettore**. Ogni tipo di origine dati connessa ha un connettore specifico. Hello connettore traduce un'operazione richiesta in formato hello hello dati connessa riconosce l'origine.

Connettori chiamate API tooexchange informazioni di identità (lettura e scrittura) con un'origine dati connessa. È inoltre possibile tooadd un connettore personalizzato mediante il framework di connettività extensible hello. Hello nella figura seguente viene illustrato come un connettore si connette a un motore di sincronizzazione toohello origine dati connessa.

![Architettura 1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

I dati possono scorrere in una direzione o nell'altra, ma non in entrambe contemporaneamente. In altre parole, un connettore può essere configurato tooallow dati tooflow dal motore di toosync origine dati connessa hello o da origine dati connessa toohello motore di sincronizzazione, ma solo una di queste operazioni può verificarsi in qualsiasi momento per un oggetto e l'attributo. direzione Hello può essere diverso per oggetti diversi e per attributi diversi.

tooconfigure un connettore, specificare i tipi di oggetti di hello che si desidera toosynchronize. Specifica i tipi di oggetto hello definisce l'ambito di hello di oggetti che sono inclusi nel processo di sincronizzazione hello. passaggio successivo Hello è tooselect hello attributi toosynchronize, noto come un elenco di inclusione di attributo. Queste impostazioni possono essere modificate nelle regole di business di risposta toochanges tooyour qualsiasi momento. Quando si utilizza l'installazione guidata di Azure AD Connect hello, queste impostazioni vengono configurate automaticamente.

origine dati connessa tooa di tooexport oggetti, elenco di inclusione attributo hello deve includere almeno hello minimo attributi toocreate richiesto, digitare un oggetto specifico in un'origine dati connessa. Ad esempio, hello **sAMAccountName** attributo deve essere incluso in hello attributo inclusione elenco tooexport un oggetto utente tooActive Directory perché tutti gli oggetti utente in Active Directory devono avere un **sAMAccountName**  attributo definito. Installazione guidata di hello esegue nuovamente, questa configurazione.

Se l'origine dati connessa hello utilizza i componenti strutturali, ad esempio oggetti tooorganize partizioni o contenitori, è possibile limitare le aree di hello nell'origine dati connessa hello che vengono utilizzate per una determinata soluzione.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Struttura interna dello spazio dei nomi del motore di sincronizzazione hello
spazio dei nomi del motore di sincronizzazione intera Hello è costituito da due spazi dei nomi che archiviano informazioni di identità hello. Hello due spazi dei nomi sono:

* spazio connettore Hello (CS)
* Hello metaverse (MV)

Hello **spazio connettore** è un'area di gestione temporanea che contiene le rappresentazioni di oggetti da un attributi di hello e di origine dati connessa specificati nell'elenco di inclusione attributo hello designato hello. il motore di sincronizzazione Hello utilizza toodetermine di spazio connettore hello cosa è cambiato in hello connesso dati di origine e toostage le modifiche in arrivo. il motore di sincronizzazione Hello utilizza inoltre toostage di spazio connettore hello in uscita delle modifiche per l'origine dati connessa toohello di esportazione. il motore di sincronizzazione Hello gestisce uno spazio connettore distinti come area di gestione temporanea per ogni connettore.

Tramite un'area di gestione temporanea, il motore di sincronizzazione hello rimane indipendenti dalla origini dati hello connesso e non è interessato dalle loro disponibilità e l'accessibilità. Di conseguenza, è possibile elaborare le informazioni di identità in qualsiasi momento utilizzando i dati di hello nell'area di gestione temporanea hello. il motore di sincronizzazione Hello può richiedere solo hello le modifiche apportate all'interno di origine dati connessa hello hello ultima sessione di comunicazione terminata o push solo informazioni di tooidentity modifiche hello che hello origine dati connessa non ha ancora ricevuto, riducendo in traffico di rete Hello tra il motore di sincronizzazione hello e origine dati connessa hello.

Inoltre, il motore di sincronizzazione archivia le informazioni di stato su tutti gli oggetti che temporaneamente nello spazio connettore hello. Quando viene ricevuti nuovi dati, il motore di sincronizzazione valuta sempre se dati hello sono già stati sincronizzati.

Hello **metaverse** è un'area di archiviazione che contiene informazioni di identità hello aggregato da più origini dati connesse, offrendo una singola visualizzazione globale e integrata di tutti gli oggetti combinati. Oggetti Metaverse vengono creati in base alle informazioni di identità hello vengono recuperate dalle origini dati connesse hello e un set di regole che consentono di processo di sincronizzazione toocustomize hello.

Hello illustrazione seguente mostra lo spazio dei nomi dello spazio connettore di hello e spazio dei nomi metaverse hello all'interno del motore di sincronizzazione hello.

![Architettura 2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Oggetti identità del motore di sincronizzazione
gli oggetti di Hello nel motore di sincronizzazione hello sono rappresentazioni di oggetti nell'origine dati connessa hello o hello visualizzazione integrata che motore di sincronizzazione dispone di tali oggetti. Ogni oggetto del motore di sincronizzazione deve avere un identificatore univoco globale (GUID). I GUID garantiscono l'integrità dei dati ed esprimono le relazioni tra gli oggetti.

### <a name="connector-space-objects"></a>Oggetti dello spazio connettore
Quando il motore di sincronizzazione comunica con un'origine dati connessa, legge le informazioni sull'identità hello nell'origine dati connessa hello e utilizza tale toocreate informazioni una rappresentazione dell'oggetto identità hello nello spazio connettore hello. Non è possibile creare o eliminare tali oggetti singolarmente. È tuttavia possibile eliminare manualmente tutti gli oggetti in uno spazio connettore.

Tutti gli oggetti nello spazio connettore hello dispongono di due attributi:

* Un identificatore univoco globale (GUID)
* Un nome distinto (noto anche come DN)

Se connesso hello origine dati assegna un oggetto toohello attributo univoco, quindi gli oggetti nello spazio connettore hello possono anche avere un attributo di ancoraggio. attributo di ancoraggio Hello identifica in modo univoco un oggetto origine dati connessa hello. il motore di sincronizzazione Hello utilizza hello ancoraggio toolocate hello corrispondente rappresentazione di questo oggetto nell'origine dati connessa hello. Motore di sincronizzazione si presuppone che definiscono hello di un oggetto mai le modifiche nel corso della durata dell'oggetto hello hello.

Molti dei connettori hello utilizzano toogenerate un identificatore univoco noto un ancoraggio automaticamente per ogni oggetto quando viene importato. Ad esempio, hello Active Directory Connector utilizza hello **objectGUID** attributo per un ancoraggio. Per le origini dati connesse che non si specifica un identificatore univoco definito chiaramente, è possibile specificare la generazione di ancoraggio come parte della configurazione del connettore hello.

Case, ancoraggio hello viene compilato da uno o più attributi univoci di un oggetto tipo, né di e che le modifiche in modo univoco che identifica l'oggetto di hello nello spazio connettore di hello (ad esempio, un dipendente o un ID utente).

Un oggetto spazio connettore può essere uno dei seguenti hello:

* Un oggetto di staging
* Un segnaposto

### <a name="staging-objects"></a>Oggetti di staging
Un oggetto di gestione temporanea rappresenta un'istanza di hello tipi di oggetto dall'origine dati connessa hello designato. Inoltre toohello GUID e il nome distinto di hello, un oggetto di gestione temporanea ha sempre un valore che indica il tipo di oggetto hello.

Gli oggetti di gestione temporanea che sono stati importati sempre avere un valore per l'attributo di ancoraggio hello. Gli oggetti di gestione temporanea che sono stato appena eseguito il provisioning del motore di sincronizzazione e il processo di hello di viene creato nell'origine dati connessa hello non dispone di un valore per l'attributo di ancoraggio hello.

Gli oggetti di gestione temporanea contengono anche i valori correnti degli attributi di business e necessari dal processo di sincronizzazione hello tooperform del motore di sincronizzazione di informazioni operative. Informazioni operative includono flag che indicano il tipo di hello di aggiornamenti che vengono gestiti nell'oggetto di gestione temporanea hello. Se un oggetto di gestione temporanea ha ricevuto nuove informazioni sull'identità dall'origine dati connessa hello che non è ancora stato elaborato, l'oggetto hello è contrassegnata come **in sospeso importazione**. Se un oggetto di gestione temporanea ha nuove informazioni di identità non sono ancora stato origine dati connessa toohello esportato, viene contrassegnato come **in sospeso esportazione**.

Un oggetto di staging può essere un oggetto di importazione o un oggetto di esportazione. il motore di sincronizzazione Hello crea un oggetto di importazione utilizzando le informazioni sull'oggetto ricevuti dall'origine dati connessa hello. Quando il motore di sincronizzazione riceve informazioni sull'esistenza hello di un nuovo oggetto che corrisponde a uno dei tipi di oggetto hello selezionati nel connettore hello, crea un oggetto di importazione nello spazio connettore hello come una rappresentazione dell'oggetto hello nell'origine dati connessa hello.

Hello nella figura riportata di seguito viene illustrato un oggetto di importazione che rappresenta un oggetto origine dati connessa hello.

![Architettura 3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

il motore di sincronizzazione Hello crea un oggetto di esportazione usando le informazioni sull'oggetto nel metaverse hello. Esportare gli oggetti sono l'origine dati connessa toohello esportato durante hello successiva sessione di comunicazione. Dal punto di vista hello del motore di sincronizzazione hello, esportare gli oggetti non esistono nell'origine dati connessa hello ancora. Attributo di ancoraggio hello per un oggetto di esportazione, pertanto, non è disponibile. Dopo aver ricevuto oggetto hello dal motore di sincronizzazione, origine dati connessa hello crea un valore univoco per l'attributo di ancoraggio hello dell'oggetto hello.

Hello nella figura seguente viene illustrato come un oggetto di esportazione viene creato utilizzando le informazioni di identità nel metaverse hello.

![Architettura 4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

il motore di sincronizzazione Hello confermata esportazione hello dell'oggetto hello reimportazione oggetto hello dall'origine dati connessa hello. Esportare gli oggetti diventano Importa oggetti quando il motore di sincronizzazione li riceve durante l'importazione di Avanti hello da tale origine dati connessa.

### <a name="placeholders"></a>Segnaposto
il motore di sincronizzazione Hello utilizza gli oggetti toostore un spazio dei nomi flat. Tuttavia, alcune origini dati connesse, ad esempio Active Directory, usano uno spazio dei nomi gerarchico. informazioni tootransform da uno spazio dei nomi gerarchico in uno spazio dei nomi flat, motore di sincronizzazione Usa gerarchia hello toopreserve di segnaposto.

Ogni segnaposto rappresenta un componente (ad esempio, un'unità organizzativa) del nome gerarchica di un oggetto che non è stato importato nel motore di sincronizzazione, ma è necessario tooconstruct hello gerarchica nome. Vengono inseriti spazi vuoti creati da riferimenti nel tooobjects di origine dati connessa hello che non sono di gestione temporanea degli oggetti nello spazio connettore hello.

il motore di sincronizzazione Hello utilizza inoltre gli oggetti a cui fa riferimento toostore segnaposto che non sono ancora stati importati. Ad esempio, se la sincronizzazione è configurato tooinclude hello manager attributo hello *Abbie Spencer* dell'oggetto e il valore ricevuto hello è un oggetto che non è stato importato, ad esempio *CN = Lee Sperry, CN = Users, DC = fabrikam, DC = com*, informazioni sulla gestione di hello viene memorizzati come segnaposto nello spazio connettore hello. Se l'oggetto di gestione di hello in un secondo momento viene importato, oggetto segnaposto hello viene sovrascritto dal hello oggetto che rappresenta il gestore di hello di gestione temporanea.

### <a name="metaverse-objects"></a>Oggetti del metaverse
Un oggetto metaverse contiene hello aggregato Visualizza hello oggetti nello spazio connettore hello di gestione temporanea con il motore di sincronizzazione. Motore di sincronizzazione crea gli oggetti metaverse usando informazioni hello nell'importazione di oggetti. Diversi oggetti di spazio connettore possono essere collegato tooa metaverse singolo oggetto, ma un oggetto spazio connettore non può essere collegato toomore rispetto a un oggetto metaverse.

Gli oggetti del metaverse non possono essere creati o eliminati manualmente. il motore di sincronizzazione Hello Elimina automaticamente gli oggetti metaverse privi di un oggetto spazio connettore di collegamento tooany nello spazio connettore hello.

toomap gli oggetti all'interno di un connesso tooa corrispondente oggetto tipo di origine dati all'interno di hello metaverse, motore di sincronizzazione fornisce uno schema estensibile con un set predefinito di tipi di oggetti e attributi associati. È possibile creare nuovi tipi di oggetto e attributi per gli oggetti del metaverse. Gli attributi possono essere a valore singolo o multivalore e tipi di attributo hello possono essere valori booleani, riferimenti, numeri e stringhe.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relazioni tra oggetti di staging e oggetti del metaverse
All'interno dello spazio dei nomi motore sincronizzazione hello, flusso di dati hello è abilitato per la relazione di collegamento hello tra gli oggetti di gestione temporanea e metaverse. Oggetto che è una gestione temporanea viene chiamato l'oggetto metaverse tooa collegato un **aggiunti a un oggetto** (o **oggetto connettore**). Viene chiamato un oggetto di gestione temporanea che non è un oggetto metaverse tooa collegato un **disgiunto oggetto** (o **oggetti sezionatore**). condizioni di Hello aggiunto e disgiunto sono toonot preferito deve essere confuso con hello connettori responsabili per l'importazione ed esportazione di dati da una directory connessa.

Segnaposto non sono mai oggetto metaverse tooa collegato

Un oggetto collegato è costituito da un oggetto di gestione temporanea e il relativo oggetto metaverse singolo tooa di relazione collegata. Gli oggetti aggiunti sono valori di attributo utilizzati toosynchronize tra un oggetto spazio connettore e un oggetto metaverse.

Quando un oggetto di gestione temporanea diventa un oggetto unito durante la sincronizzazione, gli attributi possono avvenire tra hello oggetto e oggetto metaverse hello di gestione temporanea. Il flusso degli attributi è bidirezionale e viene configurato usando le regole di importazione degli attributi e le regole di esportazione degli attributi.

Un oggetto spazio connettore singolo può essere collegato tooonly metaverse di un oggetto. Tuttavia, ogni oggetto metaverse può essere toomultiple collegato gli oggetti che lo spazio connettore hello stesso o in spazi connettore diversi, come illustrato nella seguente figura hello.

![Architettura 5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Hello collegato relazione tra l'oggetto di gestione temporanea hello e un oggetto del metaverse è persistente e può essere rimosse solo le regole specificate.

Un oggetto separato è un oggetto di gestione temporanea che non è un oggetto metaverse tooany collegato. attributo di Hello non sono valori di un oggetto separato elaborato qualsiasi ulteriore all'interno di hello metaverse. Hello attributo dal motore di sincronizzazione non vengono aggiornati i valori di hello oggetto corrispondente nell'origine dati connessa hello.

Usando gli oggetti separati è possibile archiviare le informazioni sull'identità nel motore di sincronizzazione ed elaborarle in seguito. Mantenere un oggetto di gestione temporanea come oggetto separato nello spazio connettore hello presenta numerosi vantaggi. Poiché system hello ha già preconfigurato informazioni hello necessario su questo oggetto, non è necessario toocreate una rappresentazione di questo oggetto nuovamente durante hello successivamente importare da origine dati connessa hello. In questo modo, il motore di sincronizzazione ha sempre uno snapshot completo dell'origine dati connessa hello, anche se è presente alcuna origine dati connessa di toohello connessione corrente. Gli oggetti separati possono essere convertiti in oggetti collegati e viceversa, in base alle regole di hello specificate.

Un oggetto di importazione viene creato come oggetto separato. Un oggetto di esportazione deve essere un oggetto unito. la logica di sistema Hello applica questa regola ed elimina ogni oggetto di esportazione che non è un oggetto collegato.

## <a name="sync-engine-identity-management-process"></a>Processo di gestione delle identità del motore di sincronizzazione
processo di gestione delle identità Hello controlla la modalità di aggiornamento delle informazioni di identità tra origini dati connesse diversi. La gestione delle identità viene eseguita in tre processi:

* Importazione
* Sincronizzazione
* Esporta

Durante il processo di importazione hello, motore di sincronizzazione valuta hello informazioni di identità in ingresso da un'origine dati connessa. Quando vengono rilevate modifiche, crea nuovi oggetti di gestione temporanea o gli oggetti di gestione temporanea esistenti nello spazio connettore hello per la sincronizzazione degli aggiornamenti.

Durante il processo di sincronizzazione di hello, motore di sincronizzazione aggiorna hello metaverse tooreflect modifiche che si sono verificati nello spazio connettore hello e aggiorna hello connettore spazio tooreflect modifiche che si sono verificati nel metaverse hello.

Durante il processo di esportazione hello, motore di sincronizzazione effettuato il push delle modifiche che sono gestiti in oggetti di gestione temporanea e che siano contrassegnate come in sospeso di esportazione.

Hello seguente figura mostra dove ogni processi hello viene eseguito come flussi di informazioni di identità da tooanother origine dati connessa.

![Architettura 6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Processo di importazione
Durante il processo di importazione hello, motore di sincronizzazione restituisce le informazioni sugli aggiornamenti tooidentity. Motore di sincronizzazione confronta le informazioni sull'identità hello ricevuti dall'origine dati connessa hello con informazioni di identità hello su un oggetto di gestione temporanea e determina se l'oggetto di gestione temporanea hello richiede aggiornamenti. Se è necessario tooupdate hello oggetto con i nuovi dati di gestione temporanea, hello oggetto di gestione temporanea viene contrassegnata come in sospeso di importazione.

Per gli oggetti nello spazio connettore hello prima della sincronizzazione di gestione temporanea, il motore di sincronizzazione è grado di elaborare solo informazioni di identità di hello sono stato modificato. Questo processo fornisce hello seguenti vantaggi:

* **Sincronizzazione efficiente**. Hello dati elaborati durante la sincronizzazione viene ridotto al minimo.
* **Risincronizzazione efficiente**. È possibile modificare come motore di sincronizzazione elabora le informazioni di identità senza origine di dati di riconnessione hello sincronizzazione motore toohello.
* **Sincronizzazione toopreview opportunità**. È possibile visualizzare l'anteprima di sincronizzazione tooverify che supposizioni su processo di gestione delle identità hello siano corretti.

Per ogni oggetto specificato in hello connettore, il motore di sincronizzazione hello tenta innanzitutto toolocate una rappresentazione dell'oggetto hello nello spazio connettore hello di hello connettore. Motore di sincronizzazione esamina tutti gli oggetti di gestione temporanea nello spazio connettore hello e tenta di toofind un oggetto di gestione temporanea corrispondente con un attributo di ancoraggio corrispondente. Se nessun oggetto di gestione temporanea esistente corrisponda un attributo di ancoraggio, sincronizzazione motore tentativi toofind un oggetto di gestione temporanea corrispondente con hello stesso nome distinto.

Quando il motore di sincronizzazione rileva un oggetto di gestione temporanea corrispondente tramite il nome distinto, ma non per ancoraggio, hello speciali conseguenze seguenti:

* Se l'oggetto hello si trova nello spazio connettore hello non dispone di alcun anchor, quindi il motore di sincronizzazione rimuove l'oggetto dallo spazio connettore hello e segni hello oggetto metaverse è collegato tooas **ritentare il provisioning sincronizzazione successiva eseguire**. Quindi, viene creato il nuovo oggetto di importazione hello.
* Se l'oggetto hello si trova nello spazio connettore hello è un ancoraggio, motore di sincronizzazione si presuppone che l'oggetto è stato rinominato o eliminato nella directory connessa hello. Assegna un nome distinto temporaneo di nuovo per l'oggetto spazio connettore di hello in modo che è possibile inserire la oggetto di hello in arrivo. Hello vecchio oggetto diventa quindi **temporanei**, in attesa di hello connettore tooimport hello ridenominazione o eliminazione tooresolve hello situazione.

Se il motore di sincronizzazione individua un oggetto di gestione temporanea corrispondente toohello l'oggetto specificato in hello connettore, determina il tipo di modifiche tooapply. Ad esempio motore di sincronizzazione è possibile rinominare o eliminare oggetto hello nell'origine dati connessa hello oppure potrebbe aggiornare solo i valori di attributo dell'oggetto hello.

Gli oggetti di staging con dati aggiornati vengono contrassegnati come pending import. Sono disponibili tipi di diversi di importazioni in sospeso. In base al risultato di hello hello processo di importazione, un oggetto di gestione temporanea nello spazio connettore hello presenta uno dei seguenti tipi di importazione in sospeso hello:

* **Nessuno**. Nessun tooany modifiche degli attributi hello di hello oggetto di gestione temporanea sono disponibili. Il motore di sincronizzazione non contrassegna questo tipo come importazione in sospeso.
* **Add**. oggetto di gestione temporanea Hello è un nuovo oggetto di importazione nello spazio connettore hello. Motore di sincronizzazione questo tipo viene contrassegnata come in sospeso di importazione per un'ulteriore elaborazione nel metaverse hello.
* **Update**. Motore di sincronizzazione rileva un oggetto di gestione temporanea corrispondente nello spazio connettore hello e contrassegna questo tipo come in sospeso di importazione in modo che gli aggiornamenti toohello attributi possono essere elaborati in hello metaverse. Gli aggiornamenti includono la ridenominazione degli oggetti.
* **Delete**. Motore di sincronizzazione rileva un oggetto di gestione temporanea corrispondente nello spazio connettore hello e contrassegna questo tipo come in sospeso di importazione in modo che hello aggiunti a un oggetto può essere eliminato.
* **Delete/Add**. Motore di sincronizzazione rileva un oggetto di gestione temporanea corrispondente nello spazio connettore hello, ma i tipi di oggetto hello non corrispondono. In questo caso, viene inserita temporaneamente una modifica di eliminazione/aggiunta. A delete-aggiungere modifiche indica toohello motore di sincronizzazione che deve verificarsi una risincronizzazione completezza di questo oggetto perché l'oggetto toothis si applicano diversi set di regole, quando cambia il tipo di oggetto hello.

Se l'impostazione hello lo stato di importazione di un oggetto di gestione temporanea in sospeso, è possibile tooreduce hello in modo significativo quantità di dati elaborati durante la sincronizzazione perché consente hello sistema tooprocess solo gli oggetti che hanno aggiornato i dati.

### <a name="synchronization-process"></a>Processo di sincronizzazione
La sincronizzazione è costituita da due processi correlati:

* Sincronizzazione in entrata, quando viene aggiornato il contenuto di hello del metaverse hello utilizzando i dati di hello nello spazio connettore hello.
* Sincronizzazione in uscita, quando viene aggiornato il contenuto di hello di spazio connettore hello utilizzando i dati nel metaverse hello.

Hello informazioni inserite nello spazio connettore hello hello il processo di sincronizzazione in entrata creata in hello metaverse hello integrato visualizzazione di dati archiviati in origini dati connesse hello hello. Tutti gli oggetti di gestione temporanea o solo quelli con informazioni sull'importazione in sospeso vengono aggregati, a seconda della configurazione delle regole di hello.

aggiornamenti di processo di sincronizzazione in uscita Hello esportano gli oggetti quando modificare oggetti metaverse.

Sincronizzazione in entrata Crea vista hello integrato nel metaverse hello di informazioni di identità hello viene ricevute da origini dati connesse hello. Motore di sincronizzazione può elaborare le informazioni di identità in qualsiasi momento utilizzando hello più recenti informazioni di identità che ha da hello connesso origine dati.

**Sincronizzazione in ingresso**

Sincronizzazione in entrata include hello seguenti processi:

* **Eseguire il provisioning** (chiamato anche **proiezione** se è importante toodistinguish questo processo di provisioning di sincronizzazione in uscita). il motore di sincronizzazione Hello crea un nuovo oggetto metaverse basato su un oggetto di gestione temporanea e li collega. Il provisioning è un'operazione a livello di oggetto.
* **Join**. il motore di sincronizzazione Hello collega un gestione temporanea oggetto tooan metaverse oggetto esistente. Un join è un'operazione a livello di oggetto.
* **Importazione del flusso degli attributi**. Motore di sincronizzazione aggiorna i valori di attributo hello, denominati flusso di attributi, dell'oggetto hello hello Metaverse. L'importazione del flusso degli attributi è un'operazione a livello di attributo che richiede un collegamento tra un oggetto di staging e un oggetto del metaverse.

Eseguire il provisioning è hello solo processo che crea oggetti nel metaverse hello. Il provisioning ha effetto solo sugli oggetti di importazione che sono oggetti separati. Durante il provisioning, il motore di sincronizzazione crea un oggetto metaverse corrispondente tipo di oggetto toohello dell'oggetto di importazione hello e stabilisce un collegamento tra gli oggetti, creando così un oggetto collegato.

il processo di aggiunta di Hello definisce anche un collegamento tra oggetti di importazione e l'oggetto metaverse. differenza Hello join ed eseguire il provisioning è che il processo di aggiunta di hello richiede l'oggetto di importazione hello oggetto metaverse esistenti tooan collegato, in cui il processo di provisioning hello crea un nuovo oggetto metaverse.

Motore di sincronizzazione prova toojoin importazione tooa metaverse oggetto in base ai criteri specificati nella configurazione di regole di sincronizzazione hello.

Durante il provisioning di hello e i processi di join, il motore di sincronizzazione consente di collegare un oggetto metaverse tooa oggetto separato, rendendoli unita in join. Al termine di queste operazioni a livello di oggetto, il motore di sincronizzazione può aggiornare i valori di attributo hello di oggetto metaverse associato hello. Questo processo viene chiamato importazione del flusso degli attributi.

Importa flusso di attributi si verifica in tutti gli oggetti di importazione dei nuovi dati e oggetto metaverse tooa collegato.

**Sincronizzazione in uscita**

La sincronizzazione in uscita aggiorna gli oggetti di esportazione quando un oggetto del metaverse viene modificato, ma non eliminato. obiettivo di Hello di sincronizzazione in uscita è tooevaluate se gli oggetti toometaverse modifiche richiedono aggiornamenti toostaging oggetti negli spazi connettore hello. In alcuni casi, aggiornare hello modifiche possono richiedere che tutti gli spazi connettore oggetti gestione temporanea. Gli oggetti di staging modificati vengono contrassegnati come pending export e in questo modo diventano oggetti di esportazione. Questi oggetti vengono inseriti in un secondo momento all'origine dati connessa toohello durante il processo di esportazione hello di esportazione.

La sincronizzazione in uscita include tre processi:

* **Provisioning**
* **Deprovisioning**
* **Esportazione del flusso degli attributi**

Il provisioning e il deprovisioning sono entrambi operazioni a livello di oggetto. Il deprovisioning dipende dal provisioning perché solo il provisioning può avviarlo. Deprovisioning viene attivato quando si configurano rimuove hello collegamento tra un oggetto metaverse e un oggetto di esportazione.

Il provisioning viene sempre attivato quando le modifiche vengono applicate tooobjects hello Metaverse. Quando gli oggetti toometaverse vengono apportate modifiche, il motore di sincronizzazione eseguire una delle seguenti attività come parte del processo di provisioning hello hello:

* Creare gli oggetti aggiunti, in cui un oggetto del metaverse è oggetto esportazione tooa collegato appena creato.
* Rinominare un oggetto unito.
* Separare i collegamenti tra un oggetto del metaverse e gli oggetti di staging, creando un oggetto separato.

Se il provisioning richiede toocreate motore di sincronizzazione un nuovo oggetto connettore, hello oggetto metaverse hello toowhich di gestione temporanea è collegato è sempre un oggetto di esportazione, perché hello oggetto non esiste ancora nell'origine dati connessa hello.

Se il provisioning richiede del motore di sincronizzazione toodisjoin aggiunti a un oggetto, crea un oggetto separato, deprovisioning è attivato. processo di deprovisioning Hello hello oggetto verrà eliminato.

Durante l'annullamento dell'implementazione, l'eliminazione di un oggetto di esportazione non elimina fisicamente oggetto hello. Hello oggetto viene contrassegnato come **eliminato**, ovvero l'operazione di eliminazione hello preconfigurato sull'oggetto hello.

Flusso di attributi di esportazione si verifica anche durante il processo di sincronizzazione in uscita hello, analogamente toohello che Importa flusso di attributi si verifica durante la sincronizzazione in ingresso. L'esportazione del flusso dagli attributi viene eseguita solo tra gli oggetti del metaverse e di esportazione uniti.

### <a name="export-process"></a>Processo di esportazione
Durante il processo di esportazione hello, motore di sincronizzazione esamina tutti gli oggetti di esportazione che sono contrassegnati come in sospeso di esportazione nello spazio connettore hello e quindi invia gli aggiornamenti toohello l'origine dati collegata.

il motore di sincronizzazione Hello può determinare l'esito positivo hello di un'esportazione, ma non sufficientemente può determinare che il processo di gestione identità hello è stato completato. Gli oggetti nell'origine dati connessa hello possono sempre essere modificati da altri processi. Poiché il motore di sincronizzazione non dispone di un'origine dati connessa toohello di connessione permanente, non è sufficiente toomake scontati proprietà hello di un oggetto origine dati connessa hello basato solo su una notifica di esportazione ha esito positivo.

Ad esempio, un processo in hello origine dati collegata possibile eseguire il attributi dell'oggetto hello modifica i valori originali tootheir (vale a dire, origine dati connessa hello poteva sovrascrivere i valori hello immediatamente dopo l'inserimento dei dati hello la disconnessione dal motore di sincronizzazione e correttamente applicate nell'origine dati connessa hello).

archivi di motore di sincronizzazione Hello esportazione e importano di informazioni sullo stato relative a ogni oggetto di gestione temporanea. Se i valori degli attributi hello specificati nell'elenco di inclusione attributo hello sono state modificate dall'ultima esportazione hello, hello archiviazione dell'importazione ed esportazione di stato Abilita sincronizzazione motore tooreact in modo appropriato. Motore di sincronizzazione utilizza hello importazione processo tooconfirm valori di attributo che sono stati origine dati connessa toohello esportato. Un confronto tra hello importato e informazioni esportate, come illustrato nella seguente illustrazione, hello consentono toodetermine motore di sincronizzazione se hello esportazione è stata completata o se è necessario toobe ripetuto.

![Architettura 7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Se, ad esempio, il motore di sincronizzazione Esporta attributo C, che ha un valore pari a 5, origine dati collegata tooa, C = 5 archivia nella propria memoria lo stato di esportazione. Ogni esportazione aggiuntivi su questo oggetto è dovuta in un'origine dati connessa di tentativo tooexport C = 5 toohello nuovo motore di sincronizzazione si presuppone che questo valore non è stato applicato in modo permanente toohello oggetto (ovvero, a meno che non recentemente è stato importato un valore diverso da hello origine dati collegata). memoria esportazione Hello viene cancellata quando C = 5 viene ricevuto durante un'operazione di importazione in oggetto hello.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

