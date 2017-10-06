---
title: Connettore di Domino aaaLotus | Documenti Microsoft
description: Questo articolo viene descritto come Lotus Domino connettore tooconfigure Microsoft.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Documentazione tecnica sul connettore Lotus Domino
Questo articolo descrive hello Lotus Domino connettore. articolo Hello applica toohello i seguenti prodotti:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * È necessario usare l'hotfix 4.1.3671.0 o versione successiva ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Per MIM2016 e FIM2010R2, è disponibile come download hello hello connettore [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Panoramica di hello connettore di Lotus Domino
Hello Lotus Domino connettore permette di servizio di sincronizzazione hello toointegrate con il server di Lotus Domino IBM.

Dal punto di vista di alto livello, hello seguenti caratteristiche è supportata dalla versione corrente di hello del connettore hello:

| Funzionalità | Supporto |
| --- | --- |
| Origine dati connessa |Server:  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Client:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Scenari |<li>Gestione del ciclo di vita degli oggetti</li><li>Gestione di gruppi</li><li>Gestione delle password</li> |
| Operazioni |<li>Importazione completa e delta</li><li>Esportazione</li><li>Impostare e modificare la password in Password HTTP</li> |
| Schema |<li>Persona (utente mobile, contatto (persone senza certificato))</li><li>Gruppo</li><li>Risorsa (risorsa, stanza, riunione online)</li><li>Mail-In Database</li><li>Individuazione dinamica degli attributi per gli oggetti supportati</li> |

connettore Lotus Domino Hello Usa hello Lotus Notes client toocommunicate con Server Lotus Domino. Come conseguenza di questa dipendenza, è necessario installare un Client di Lotus Notes supportati nel server di sincronizzazione hello. Hello comunicazione hello client / server hello viene implementata tramite l'interfaccia di hello interoperabilità .NET di Lotus Notes (Interop.domino.dll). Questa interfaccia facilita la comunicazione tra la piattaforma di Microsoft.NET hello e client Lotus Notes hello e supporta l'accesso tooLotus Domino documenti e visualizzazioni. Per l'importazione delta, è anche possibile che interfaccia hello, C++ native viene utilizzato (a seconda di metodo di importazione delta hello selezionata).

### <a name="prerequisites"></a>Prerequisiti
Prima di utilizzare connettore hello, verificare di che aver seguito i prerequisiti nel server di sincronizzazione hello hello:

* Microsoft .NET 4.5.2 Framework o versione successiva
* il client di Lotus Notes Hello deve essere installato sul server di sincronizzazione
* Connettore di Lotus Domino Hello richiede hello predefinito Lotus Domino LDAP dello schema del database (schema.nsf) toobe presente nel server di Directory di Domino hello. Se non è presente, è possibile installarlo in esecuzione o riavviando il servizio LDAP hello sul server di Domino hello.

### <a name="connected-data-source-permissions"></a>Autorizzazioni dell'origine dati connessa
tooperform hello supportate di attività nel connettore Lotus Domino, è necessario essere un membro dei gruppi seguenti:

* Full Access administrators
* Administrators
* Database Administrators

Hello nella tabella seguente sono elencate hello autorizzazioni necessarie per ogni operazione:

| Operazione | Diritti di accesso |
| --- | --- |
| Importa |<li>Leggere documenti pubblici</li><li> Accesso amministratore completo (quando si è membri del gruppo administrators di accesso completo, si dispone automaticamente hello accesso valido tooin ACL.)</li> |
| Esportazione e impostazione della password |Accesso effettivo:  <li>Creare i documenti</li><li>Eliminare documenti</li><li>Leggere documenti pubblici</li><li>Scrivere documenti pubblici</li><li>Replicare o copiare documenti</li>Per operazioni di esportazione, è necessario anche hello seguenti ruoli: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Operazioni dirette e AdminP
Le operazioni di passare direttamente nella directory toohello Domino o tramite hello AdminP elaborare. nelle tabelle seguenti Hello elencati tutti gli oggetti supportati, le operazioni e, se applicabile, hello correlato il metodo di implementazione:

**Rubrica primaria**

| Oggetto | Create | Aggiornamento | Elimina |
| --- | --- | --- | --- |
| Person |AdminP |Diretto |AdminP |
| Gruppo |AdminP |Diretto |AdminP |
| MailInDB |Diretto |Diretto |Diretto |
| Risorsa |AdminP |Diretto |AdminP |

**Rubrica secondaria**

| Oggetto | Create | Aggiornamento | Elimina |
| --- | --- | --- | --- |
| Person |N/D |Diretto |Diretto |
| Gruppo |Diretto |Diretto |Diretto |
| MailInDB |Diretto |Diretto |Diretto |
| Risorsa |N/D |N/D |N/D |

Quando si crea una risorsa, viene creato un documento di Notes. Analogamente, quando viene eliminata una risorsa, il documento di note hello viene eliminato.

### <a name="ports-and-protocols"></a>Porte e protocolli
Il client IBM Lotus Notes e i server Domino comunicano tramite NRPC (Notes Remote Procedure Call) che dovrà usare TCP/IP. numero di porta predefinito Hello è 1352, ma possa essere modificata dall'amministratore di Domino hello.

### <a name="not-supported"></a>Non supportate
Hello dopo operazioni non è supportato dalla versione corrente di hello del connettore Lotus Domino hello:

* Spostamento di cassette postali tra server.

## <a name="create-a-new-connector"></a>Creare un nuovo connettore
### <a name="client-software-installation-and-configuration"></a>Installazione e configurazione del software client
Lotus Notes deve essere installato nel server di hello **prima** hello connettore è installato.

Quando si esegue l'installazione, assicurarsi di selezionare **Single User Install**. Hello predefinito **multiutente installare** non funziona.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Nella pagina di funzionalità hello, installa solo hello richiesta la funzionalità di Lotus Notes e **accesso unico Client**. Accesso singolo è necessario per toolog in grado di hello connettore toobe sul server di Domino toohello.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Nota:** inizio Lotus Notes una volta a un utente che si trova in hello nello stesso server hello account utilizzare come account del servizio del connettore hello. Verificare inoltre che client di Lotus Notes hello tooclose nel server di hello. Non può essere in esecuzione in hello hello ora stesso connettore tenta tooconnect toohello Domino server.

### <a name="create-connector"></a>Create Connector
un connettore Lotus Domino tooCreate nella **servizio di sincronizzazione** selezionare **agente di gestione** e **crea**. Seleziona hello **Lotus Domino (Microsoft)** connettore.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Se la versione del servizio di sincronizzazione offre hello possibilità tooconfigure **architettura**, assicurarsi che il connettore hello sia impostato tooits predefinito valore toorun in **processo**.

### <a name="connectivity"></a>Connettività
Nella pagina connettività hello, è necessario specificare il nome di server Lotus Domino hello e immettere le credenziali di accesso hello.  
![Connettività](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

proprietà del Server di Domino Hello supporta due formati per nome del server hello:

* ServerName
* ServerName/DirectoryName

Hello **nomeserver/nomedirectory** è hello formato preferito per questo attributo perché offre tempi di risposta quando contatti connettore hello hello Server Domino.

Hello fornito UserID file viene archiviato nel database di configurazione hello del servizio di sincronizzazione hello.

Per **Delta Import** sono disponibili queste opzioni:

* **Nessuno**. Hello connettore non esegue qualsiasi importazione delta.
* **Add/Update**. importazione delta di Hello connettore fa aggiungere e operazioni di aggiornamento. Per l'eliminazione è necessaria un'operazione **Full Import** (Importazione completa). Questa operazione utilizza l'interoperabilità .net hello.
* **Add/Update/Delete**. importazione delta di Hello connettore fa aggiungere, aggiornare ed eliminare le operazioni. Questa operazione utilizza interfacce C++ native hello.

In **le opzioni dello Schema** è hello le opzioni seguenti:

* **Default Schema**. Hello connettore rileva schema hello dal server di Domino hello. Questa selezione è l'opzione predefinita di hello.
* **DSML-Schema**. Utilizzato solo se il server di Domino hello non espone schema hello. È quindi possibile creare un file DSML con schema hello e importarlo invece. Per altre informazioni su DSML, vedere [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Quando si fa clic su Avanti, vengono verificati hello ID utente e i parametri di configurazione delle password.

### <a name="global-parameters"></a>Global Parameters
Nella pagina parametri globali hello, configurare hello fuso orario e l'importazione di hello e opzione di operazione di esportazione.  
![Global Parameters](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Hello **fuso orario del Server Domino** parametro definisce il percorso di hello del Server di Domino.

Questa opzione di configurazione è necessario toosupport **importazione delta** operazioni perché consente di servizio di sincronizzazione hello determinare le modifiche tra le importazioni ultime due hello.

>[!Note]
A partire da schermo parametri globali di hello marzo 2017 aggiornamento hello include database della posta elettronica dell'utente di hello opzione toodelete hello durante l'eliminazione dell'utente hello.

![Eliminare la cassetta postale di un utente](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Impostazioni di importazione, metodo
Hello **eseguire importazione completa da** presenta le seguenti opzioni:

* Ricerca
* View (Recommended)

**Ricerca** è utilizzando l'indicizzazione di Domino, ma è comune che gli indici di hello non vengono aggiornati in tempo reale e dati hello restituiti dal server hello non sono sempre corretti. Per un sistema con molte modifiche, questa opzione in genere non funziona bene e fornisce false eliminazioni in alcune situazioni. **Search** è tuttavia più veloce di **View**.

**Visualizzazione** è hello opzione consigliata in quanto fornisce lo stato corretto hello dei dati. È leggermente più lenta rispetto a Search.

#### <a name="creation-of-virtual-contact-objects"></a>Creazione di oggetti Virtual Contact
Hello **abilitare la creazione di \_oggetto contatto** presenta le seguenti opzioni:

* Nessuno
* Non-Reference Values
* Reference and Non-Reference Values

Nel Domino, gli attributi di riferimento possono contenere molti formati diversi tooreference altri oggetti. variazioni diverse in grado di toorepresent toobe, hello implementa connettore \_contattare gli oggetti, noto anche come **contatti virtuale** (VC). Questi oggetti vengono creati in modo che possa essere aggiunto oggetti tooexisting MV o proiettati come nuovi oggetti. Ciò consente di conservare i riferimenti agli attributi.

Se questa impostazione è abilitata e se il contenuto di hello di un attributo di riferimento non è un formato di nome distinto, un \_viene creato l'oggetto contatto. Ad esempio, un attributo member di un gruppo può contenere un indirizzo SMTP. È anche possibile toohave shortName e altri attributi presenti negli attributi di riferimento. Per questo scenario, selezionare **Non-Reference Values**. Questa configurazione è l'impostazione più comune di hello per le implementazioni di Domino.

Quando Lotus Domino è toohave configurato separate le rubriche con diversi nomi distinti che rappresentano hello stesso oggetto, è possibile tooalso creare \_gli oggetti contatto per tutti i valori di riferimento che si trovano in una Rubrica. Per questo scenario, selezionare hello **riferimento e i valori di Non riferimento** opzione.

Se si dispone di più valori nell'attributo hello **FullName** nel Domino, quindi anche desiderate creazione hello tooenable dei contatti virtuale in modo che i riferimenti possono essere risolti. Ad esempio, questo attributo può avere più valori dopo un matrimonio o un divorzio. Selezionare la casella di controllo di hello **Abilita... FullName has multiple values** per questo scenario.

Unendo in attributi corretti hello hello \_oggetti contatto sarebbe oggetto unita in join toohello MV.

Questi oggetti hanno VC =\_contatto aggiunto tootheir DN.

#### <a name="import-settings-conflict-object"></a>Impostazioni di importazione, oggetto conflict
**Exclude Conflict Object**

In un'implementazione di Domino di grandi dimensioni, è possibile che più oggetti sono hello stesso DN a causa di problemi di tooreplication. In questi casi, il connettore hello sarebbe due oggetti con UniversalIDs diverso ma stesso DN. Questo conflitto causerebbe un oggetto temporaneo viene creato nello spazio connettore hello. Hello connettore può ignorare gli oggetti di hello selezionato nel Domino come vittime di replica. indicazione di Hello è tookeep selezionata questa casella di controllo.

#### <a name="export-settings"></a>Esportazione impostazioni
Se hello opzione **AdminP utilizzare per l'aggiornamento dei riferimenti** non è selezionata, quindi l'esportazione di attributi di riferimento, ad esempio membro, è una chiamata diretta e non utilizza processo AdminP hello. Utilizzare questa opzione solo quando AdminP non è stato configurato toomaintain l'integrità referenziale.

#### <a name="routing-information"></a>Informazioni di routing
Nel Domino, è possibile che un attributo di riferimento dispone di informazioni di routing incorporate come toohello un suffisso DN. Attributo del membro hello in un gruppo può, ad esempio, contenere **CN =example/organization@ABC**. suffisso Hello @ABC hello informazioni di routing. informazioni di routing Hello viene utilizzate dal Domino toosend messaggi di posta elettronica toohello corretto Domino sistema, che può essere un sistema in un'altra organizzazione. Nel campo di informazioni di Routing hello, è possibile specificare i suffissi di routing hello usati all'interno dell'organizzazione hello nell'ambito di hello connettore. Se uno di questi valori viene trovato il suffisso in un attributo di riferimento, le informazioni di routing hello viene rimosso dal riferimento hello. Se il suffisso di routing hello su un valore di riferimento non può essere compensata tooone di tali valori specificati, un \_viene creato l'oggetto contatto. Questi \_vengono creati oggetti contatto con **RO = @<RoutingSuffix>**  inseriti hello DN. Per questi \_oggetti contatto hello gli attributi seguenti viene inoltre aggiunti tooallow aggiunta oggetto reale tooa se necessario: \_routingName, \_contactName, \_displayName e UniversalID.

#### <a name="additional-address-books"></a>Altre rubriche
Se non si dispone **assistenza directory** installato, che fornisce il nome di hello di rubriche secondario, quindi è possibile immettere manualmente le liste di distribuzione.

#### <a name="multivalued-transformation"></a>Trasformazione multivalore
Molti attributi in Lotus Domino sono di tipo multivalore. Hello corrispondente metaverse gli attributi sono in genere singolo valore. Configurando hello importazione e l'opzione operazione di esportazione hello abiliti hello connettore toohelp con la conversione di hello necessarie di attributi hello interessata.

**Export**  
opzione di operazione di esportazione Hello supporta due modalità:

* Append item
* Replace item

**Sostituire l'elemento** : quando si seleziona questa opzione, connettore hello sempre remove hello corrente di valori di attributo hello in Domino e sostituirli con i valori hello fornito. Hello fornito con valori può essere a valore singolo o multivalore.

Esempio: hello Assistente di un oggetto person presenta hello seguenti valori:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Se un nuovo Assistente denominato **David Alexander** è assegnato l'oggetto person toothis, il risultato di hello è:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**Aggiungere l'elemento** : quando si seleziona questa opzione, il connettore hello mantiene i valori esistenti di hello nell'attributo hello Domino e inserire nuovi valori nella parte superiore di hello dell'elenco di dati hello.

Esempio: hello Assistente di un oggetto person presenta hello seguenti valori:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Se un nuovo Assistente denominato **David Alexander** è assegnato l'oggetto person toothis, il risultato di hello è:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**Import (Importa) (Import (Importa)a)**  
opzione di operazione di importazione Hello supporta due modalità:

* Default
* Valore di tooSingle multivalore

**Predefinito** : quando si seleziona l'opzione predefinita di hello, tutti i valori di hello tutti gli attributi vengono importati.

**Valore di tooSingle multivalore** : quando si seleziona questa opzione, un attributo multivalore viene convertito in un attributo a valore singolo. Se esiste più di un valore, viene utilizzato il valore di hello in primo piano hello (questo valore è in genere anche hello più recente).

Esempio: hello Assistente di un oggetto person presenta hello seguenti valori:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Hello più recente aggiornamento toothis attributo è **David Alexander**. Poiché hello opzione operazione di importazione viene impostato tooMultivalued tooSingle valore, connettore Importa solo **David Alexander** nello spazio connettore hello.

attributi di membro di gruppo toohello e toohello persona fullname, non si applica attributi multivalore Hello logica tooconvert in attributi a valore singolo.

È anche possibile tooconfigure importare ed esportare le regole di trasformazione per gli attributi multivalore per ogni attributo, come una regola di eccezione toohello globale. tooconfigure questa opzione, immettere [objecttype]. [attributename] in hello **importare l'elenco di esclusione attributo** e **esportare l'elenco di esclusione attributo** caselle di testo. Ad esempio, se si immette Person.Assistant e flag globale di hello impostato tooimport tutti i valori, l'unico hello primo valore viene importato per Assistente hello.

#### <a name="certifiers"></a>File di certificazione
Tutte le unità di organizzazione/aziendale sono elencate dal connettore hello. toobe tooexport in grado di persona oggetti toohello primario Rubrica, un certificatore con la password è obbligatorio.

Se dispone di rilascio degli attestati tutti hello la stessa password, hello **Password per tutti i Certifers** può essere utilizzato. È quindi possibile immettere qui la password di hello e specificare solo file certificatore hello.

Se si importa solo, quindi non si dispone toospecify qualsiasi rilascio degli attestati.

### <a name="configure-provisioning-hierarchy"></a>Configurare una gerarchia di provisioning
Quando si configura il connettore di Lotus Domino hello, ignorare questa pagina della finestra di dialogo. connettore Lotus Domino Hello non supporta il provisioning di gerarchia.  
![Gerarchia di provisioning](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurare partizioni e gerarchie
Quando si configurano le partizioni e gerarchie, è necessario selezionare hello primario Rubrica chiamata NAB=names.nsf. Inoltre toohello Rubrica primario, è possibile selezionare rubriche secondario se presenti.  
![Partitions](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Selezionare gli attributi
Quando si configurano gli attributi, è necessario selezionare tutti quelli con prefisso **\_MMS\_**. Questi attributi sono richiesti quando si esegue il provisioning di nuovi oggetti tooLotus Domino

![Attributi](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Gestione del ciclo di vita degli oggetti
In questa sezione viene fornita una panoramica di hello diversi oggetti di Domino.

### <a name="person-objects"></a>Oggetti person
oggetto person Hello rappresenta gli utenti nell'organizzazione e unità organizzative. Inoltre gli attributi predefiniti toohello, amministratore di Domino hello possono aggiungere l'oggetto Person tooa di attributi personalizzati. Come minimo, un oggetto Person deve includere tutti gli attributi obbligatori. Per un elenco completo degli attributi obbligatori, vedere [Proprietà di Lotus Notes](#lotus-notes-properties). è necessario soddisfare tooregister un oggetto person, hello seguenti prerequisiti:

* Rubrica di Hello (nsf) sono stata configurata e deve essere hello primario la Rubrica.
* È necessario hello O/OU certificatore Id e hello password tooregister un determinato utente hello organizzazione / unità organizzativa.
* È necessario definire un set specifico di proprietà di Lotus Notes per un oggetto person. Queste proprietà vengono utilizzate per il provisioning oggetto person hello. Per ulteriori informazioni, vedere sezione hello denominata [Lotus Notes proprietà](#lotus-notes-properties) più avanti in questo documento.
* password HTTP iniziale Hello per una persona è un attributo e un set durante il provisioning.
* oggetto person Hello deve essere uno dei seguenti tre tipi supportati hello:
  1. Normal User, ha un file di posta elettronica e un file di ID utente
  2. Roaming User, un tipo Normal User che include tutti i file di database mobili
  3. Contact, utente senza file di ID

Persone (ad eccezione dei contatti) possono essere raggruppate in a utenti e utenti di International ulteriormente come definito dal valore hello di hello \_MMS\_IDRegType proprietà. Queste persone utilizzare hello Client Notes tooaccess server Lotus Domino, avere un Id di note e un documento di persona. Se usano la posta elettronica di Notes, hanno anche un file di posta elettronica. utente Hello deve essere registrato toobecome attivo. Per altre informazioni, vedere:

* [Configurazione degli utenti Lotus Notes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Registrazione degli utenti](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Gestione degli utenti](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Ridenominazione degli utenti](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Tutte queste operazioni vengono eseguite in Lotus Domino e quindi importare nel servizio di sincronizzazione hello.

### <a name="resources-and-rooms"></a>Risorse e chat
Una risorsa è un altro tipo di database di Lotus Domino. Le risorse possono essere sale riunioni con vari tipi di apparecchiature, ad esempio i proiettori. Esistono sottotipi di risorse supportate dal connettore Lotus Domino definiti dall'attributo di tipo di risorsa hello:

| Type of Resource | Resource Type Attribute |
| --- | --- |
| Room |1 |
| Resource (Other) |2 |
| Online Meeting |3 |

Per hello toowork di tipo oggetto risorsa, è necessario seguente hello:

* Database di prenotazione delle risorse deve essere già esistente nel server di Domino hello connesso
* sito Hello è già definito per hello risorsa

database di prenotazione delle risorse Hello contiene tre tipi di documenti:

* Site Profile
* Risorsa
* Reservation

Per ulteriori informazioni sulla configurazione del database di prenotazione delle risorse, vedere [impostazione hello prenotazioni risorsa database](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Create, Update, and Delete Resources**  
Hello operazioni Create, Update e Delete vengono eseguite dal connettore Lotus Domino hello nel database di prenotazione delle risorse hello. Le risorse vengono create come documenti nel NSF (vale a dire hello primario Rubrica). Per altri informazioni sulla modifica e l'eliminazione di risorse, vedere [Editing and deleting Resource documents](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html) (Modifica ed eliminazione di documenti di Resource).

**Import and Export operation for Resources**  
Hello risorse può essere importati tooand esportato dal servizio di sincronizzazione hello, come qualsiasi altro tipo di oggetto. Hello Selezionare tipo di oggetto come risorsa durante la configurazione. Perché l'operazione di esportazione abbia esito positivo, è necessario avere i dettagli per Resource type, Conference Database e Site name.

### <a name="mail-in-databases"></a>Database di posta elettronica in ingresso
Un Database di posta elettronica è un database progettato tooreceive messaggi di posta elettronica. Si tratta di una cassetta postale di Lotus Domino che non è associata a un account utente di Lotus Domino specifico, ovvero non ha un proprio file di ID e password. Un database di posta elettronica in ingresso ha una proprietà UserID univoca ("nome breve") associata ad esso e il proprio indirizzo di posta elettronica.

Se è necessario avere una cassetta postale separata con il proprio indirizzo di posta elettronica che può essere condiviso tra diversi utenti, ad esempio group@contoso.com, viene creato un database di posta elettronica in ingresso. cassetta postale toothis di Hello accesso viene controllata tramite il controllo elenco accesso (ACL), che contiene i nomi di hello degli utenti Notes hello consentiti cassetta postale hello tooopen.

Per un elenco di attributi di hello necessario, vedere sezione hello denominata [gli attributi obbligatori](#mandatory-attributes) più avanti in questo articolo.

Quando un database è progettata tooreceive un messaggio di posta, viene creato un documento di posta elettronica nel Database in Lotus Domino. Questo documento deve trovarsi nella Directory di Domino di ogni server che archivia una copia del database hello. Per una descrizione dettagliata della creazione di un documento per il database di posta elettronica, vedere [Creating a Mail-In Database document](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)(Creazione di un documento del database di posta elettronica in ingresso).

Prima di creare un Database di posta elettronica, database hello deve essere già esistente (deve essere stato creato mediante Amministrazione Lotus) nel server di Domino hello.

### <a name="group-management"></a>Gestione di gruppi
È possibile ottenere una panoramica dettagliata della gestione dei gruppi di Lotus Domino hello da hello seguenti risorse:

* [Uso di gruppi](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Creazione di un gruppo](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Creazione e modifica dei gruppi](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Gestione dei gruppi](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Ridenominazione di un gruppo](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Gestione delle password
Per un utente di Lotus Domino registrato esistono due tipi di password:

1. Password utente (archiviata nel file User.id)
2. Password Internet/HTTP

connettore Lotus Domino Hello supporta solo le operazioni con password HTTP.

gestione delle password tooperform, è consigliabile abilitare la gestione delle password per il connettore di hello in hello progettazione agente di gestione. gestione delle password tooenable, seleziona **abilitare la gestione delle password** su hello **Configura estensioni** nella pagina.  
![Configurare le estensioni](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

supporto di connettore Lotus Domino Hello dopo operazioni sulle password Internet:

* Impostazione della Password: Impostazione della password imposta una nuova password Internet/HTTP utente hello nel Domino. Per impostazione predefinita è sbloccato account hello. flag di sbloccare Hello viene esposto nell'interfaccia WMI hello del motore di sincronizzazione hello.
* Modifica Password: In questo scenario, un utente potrebbe essere necessario password hello toochange o la password richiesta toochange dopo un periodo di tempo specificato. Per questa risorsa, tootake operazione sia (hello vecchia e nuova password hello) sono obbligatori. Una volta modificata, hello nuova password viene aggiornata nel Lotus Domino.

Per altre informazioni, vedere:

* [Utilizzo di funzionalità di blocco hello Internet](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Gestione delle password in Internet](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Informazioni di riferimento
In questa sezione sono elencati, ad esempio le descrizioni degli attributi e i requisiti relativi agli attributi per il connettore Lotus Domino hello.

### <a name="lotus-notes-properties"></a>Proprietà di Lotus Notes
Quando si esegue il provisioning di directory di Lotus Domino tooyour oggetti Person, gli oggetti necessario un set specifico di proprietà con valori specifici popolati. Questi valori sono necessari solo per le operazioni Create.

Hello nella tabella seguente sono elencate queste proprietà e viene fornita una descrizione di essi.

| Proprietà | Description |
| --- | --- |
| \_MMS_AltFullName |Hello alternativo nome completo dell'utente. |
| \_MMS_AltFullNameLanguage |Hello toobe di lingua utilizzata per specificare hello alternativo cognome dell'utente. |
| \_MMS_CertDaysToExpire |Hello numero di giorni da hello data corrente prima di certificato hello della scadenza. Se non specificato, data predefinita hello è di due anni da hello data corrente. |
| \_MMS_Certifier |Proprietà che contiene il nome di gerarchia organizzativa hello di certificatore hello. Ad esempio: OU=OrganizationUnit,O=Org,C=Country. |
| \_MMS_IDPath |Se hello proprietà è vuota, nessun file di identificazione utente viene creato in locale nel Server di sincronizzazione hello. Se la proprietà hello contiene un nome di file, viene creato un file di ID utente nella cartella madata hello. proprietà Hello può anche contenere un percorso completo. |
| \_MMS_IDRegType |Le persone possono essere classificate come contatti, utenti USA e utenti internazionali. Hello nella tabella seguente sono elencati i possibili valori hello: <li>0 - Contatto</li><li>1 - Utente Stati Uniti</li><li>2 - Utente internazionale</li> |
| \_MMS_IDStoreType |Proprietà obbligatoria per US Users e International Users. proprietà Hello contiene un valore intero che specifica se l'ID utente hello è archiviato come allegato di rubrica Notes hello o nel file di posta elettronica della persona hello. Se il file di ID utente hello è allegato nella Rubrica hello, può eventualmente essere creato come un file con \_MMS_IDPath. <li>Empty (Vuoto): file di ID archiviato nell'insieme di credenziali degli ID, nessun file di identificazione (utilizzato per i contatti).</li><li> 1 - attachment nella Rubrica di hello note. Hello \_MMS_Password deve essere impostata per utente identificazione i file allegati</li><li>2 - Archiviare l'ID nel file di posta elettronica della persona. Hello \_MMS_UseAdminP deve essere impostato come posta elettronica di hello toolet toofalse file creato durante la registrazione di persona hello. Hello \_MMS_Password deve essere impostata per il file di identificazione dell'utente.</li> |
| \_MMS_MailQuotaSizeLimit |numero di Hello di megabyte consentiti per i database del file hello posta elettronica. |
| \_MMS_MailQuotaWarningThreshold |numero di Hello di megabyte consentiti per il database di file tramite posta elettronica hello prima viene emesso un avviso. |
| \_MMS_MailTemplateName |file modello posta elettronica Hello che il file di posta elettronica dell'utente di hello toocreate utilizzato. Se viene specificato un modello, viene creato il file di posta elettronica hello utilizzando hello di modello specificato. Se viene specificato alcun modello, file di modello predefinito di hello è utilizzato toocreate hello. |
| \_MMS_OU |Proprietà facoltativa che è il nome dell'unità Organizzativa hello in certificatore hello. Questa proprietà deve essere vuota per i contatti. |
| \_MMS_Password |Proprietà obbligatoria per gli utenti. proprietà Hello contiene password hello per file di hello identificazione dell'oggetto hello. |
| \_MMS_UseAdminP |Proprietà deve essere set tootrue se il file di posta elettronica hello deve essere creato dal processo AdminP hello sul server di Domino hello (processo di esportazione toohello asincrona). Se toofalse è impostata, il file di posta elettronica hello viene creato con hello utente di Domino (sincrono nel processo di esportazione hello). |

Per un utente con un file di identificazione associati, hello \_proprietà MMS_Password deve contenere un valore. Per l'accesso alla posta elettronica tramite il client di Lotus Notes hello, hello server di posta elettronica e la proprietà corso di un utente deve contenere un valore.

tooaccess di posta elettronica tramite un Web browser, le proprietà seguenti hello deve contenere valori:

* Corso - proprietà obbligatoria che contiene il percorso di hello sul server di Lotus Domino hello dove si trova il file di posta elettronica hello.
* Server di posta elettronica - proprietà obbligatoria che contiene il nome di hello del server di Lotus Domino hello. Questo valore è hello Nome toouse durante la creazione di file di posta elettronica di Lotus hello sul server di Domino hello.
* HTTPPassword - proprietà facoltativa che contiene la password di accesso Web di hello per oggetto hello.

tooaccess hello Server Domino senza funzionalità di posta elettronica, hello proprietà HTTPPassword deve contenere un valore. proprietà corso Hello e hello proprietà server di posta elettronica può essere vuoto.

Con \_MMS_ IDStoreType = 2 (id di archivio nel file di posta elettronica), hello proprietà MailSystem di NotesRegistrationclass è impostato tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Attributi obbligatori
connettore Lotus Domino Hello supporta principalmente questi tipi di oggetti (tipi di documento):

* Gruppo
* Mail-In Database
* Person
* Contact (Person senza file di certificazione)
* Risorsa

Questa sezione sono elencati gli attributi di hello che sono obbligatori per ogni server di Domino tooa tooexport oggetto supportato.

| Tipo di oggetto | Attributi obbligatori |
| --- | --- |
| Gruppo |<li>ListName</li> |
| Main-In Database |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Person |<li>LastName</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Contact (Person senza file di certificazione) |<li>\_MMS_IDRegType</li> |
| Risorsa |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Sito</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Domande e problemi comuni
### <a name="schema-detection-does-not-work"></a>Il rilevamento dello schema non funziona
schema hello toodetect in grado di toobe, è necessario che se il file schema.nsf hello è presente nel server di Domino hello. Questo file viene visualizzata solo se LDAP è installato nel server di hello. Se non è possibile rilevare schema hello, verificare i seguenti aspetti di hello:

* schema.nsf file Hello è presente nella cartella radice hello di hello Server Domino
* utente Hello dispone di autorizzazioni toosee hello schema.nsf file.
* Forzare il riavvio del server LDAP hello. Aprire **Lotus Domino Console** e utilizzare **indicare ReloadSchema LDAP** schema hello tooreload di comando.

### <a name="not-all-secondary-address-books-are-visible"></a>Non tutte le rubriche secondarie sono visibili
Hello Domino connettore si basa sulla funzionalità hello **Directory assistenza** toobe toofind in grado di hello secondario rubriche. Se mancano rubriche secondario di hello, verificare se [Directory assistenza](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) è stato abilitato e configurato nel Server di Domino hello.

### <a name="custom-attributes-in-domino"></a>Attributi personalizzati in Domino
Esistono diversi modi nello schema di Domino tooextend hello viene visualizzato come un attributo personalizzato utilizzabile da hello connettore.

**Approccio 1: Estendere lo schema di Lotus Domino**

1. Creare una copia del modello di Directory di Domino {PUBNAMES. NTFS} seguendo [procedura](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (non personalizzare directory di IBM Lotus Domino predefinita hello modello):
2. Aprire hello copia di directory modello Domino {CONTOSO. Modello NTFS} che è stato creato nella finestra di progettazione di Domino e seguire questi passaggi:
   * Fare clic su Shared Elements (Elementi condivisi) ed espandere Subforms (Sottomaschere).
   * Fare doppio clic su sottomaschera InheritableSchema ${ObjectName} (dove {ObjectName} è hello Nome classe hello predefinito strutturale di oggetti, ad esempio: persona).
   * Nome attributo hello da tooadd nello schema {MyPersonAtrribute} e attributo toothat corrispondente. Creare un campo da seleziona hello **crea** Menu e quindi selezionare **campo** dal menu.
   * Nel campo aggiunto hello, impostarne le proprietà selezionando il relativo tipo, stile, dimensioni, tipo di carattere e altri parametri correlati nella finestra proprietà di campo.
   * Attributo di hello Keep stesso valore predefinito come nome hello assegnato per l'attributo (ad esempio, se il nome dell'attributo è MyPersonAttribute, mantenere il valore predefinito hello con hello stesso nome).
   * Salvare sottomaschera InheritableSchema di hello ${ObjectName} con i valori aggiornati.
3. Sostituire hello modello Directory Domino {PUBNAMES. NTFS} con il modello personalizzato nuova di hello {CONTOSO. NTFS} seguendo [procedura](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Chiudere Amministrazione Domino e aprire hello toorestart Domino Console servizio LDAP e hello tooReload Schema LDAP:
   * Nella Console di Domino, inserire il comando hello in **comando Domino** testo archiviato servizio LDAP di hello toorestart - [riavviare LDAP attività](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * schema LDAP tooreload comando indicare LDAP - indicare ReloadSchema LDAP
5. Aprire Amministrazione Domino e selezionare gli utenti e gruppi toosee scheda aggiunta attributo verrà riportato nel domino Aggiungi persona.
6. Aprire Schema.nsf dalla scheda **Files** e verificare che l'attributo aggiunto sia riportato nella classe di oggetti LDAP dominoPerson.

**Approccio 2: Creare un auxClass con attributo personalizzato e associare con la classe oggetto hello**

1. Creare una copia del modello di Directory di Domino {PUBNAMES. NTFS} seguendo [procedura](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (non personalizzare mai directory di IBM Lotus Domino predefinita hello modello):
2. Aprire hello copia di directory modello Domino {CONTOSO. Modello NTFS} è stato creato, nella finestra di progettazione di Domino.
3. Nel riquadro di sinistra hello, selezionare codice condiviso e quindi form secondari.
4. Fare clic su New Subform.
5. Hello le seguenti proprietà hello toospecify sottomaschera nuovo hello:
   * Con nuova sottomaschera hello aperto, scegliere progettazione - proprietà sottomaschera
   * Avanti toohello proprietà Name, immettere un nome per la classe oggetto ausiliario hello - ad esempio, TestSubform.
   * Mantieni proprietà Options hello "Includi sottomaschera Insert... finestra di dialogo"
   * Deselezionare le proprietà di opzioni hello "Rendering pass-through HTML nelle note."
   * Lasciare hello altri hello stesso, proprietà e chiudere proprietà sottomaschera hello.
   * Salvare e chiudere sottomaschera nuovo hello.
6. Hello seguenti tooadd una classe di un oggetto ausiliario hello toodefine campo:
   * Aprire sottomaschera hello che è stato creato.
   * Scegliere Create - Field.
   * TooName successivo nella scheda di hello nozioni di base della finestra di dialogo campo hello, specificare un nome qualsiasi, ad esempio: {MyPersonTestAttribute}.
   * Nel campo aggiunto hello, impostarne le proprietà selezionando il relativo tipo, stile, dimensione, carattere e le proprietà correlate.
   * Attributo di hello Keep stesso valore predefinito come nome hello assegnato per l'attributo (ad esempio, se il nome dell'attributo è MyPersonTestAttribute, mantenere il valore predefinito hello con hello stesso nome).
   * Salvare sottomaschera hello con i valori aggiornati e hello seguenti:
     * Nel riquadro di sinistra hello, selezionare codice condiviso e quindi form secondari
     * Selezionare nuova sottomaschera hello e scegliere progettazione - proprietà di progettazione.
     * Fare clic sulla scheda terzo hello da hello sinistra e selezionare **propagare tale divieto di modifica della progettazione**.
7. Aprire sottomaschera ExtensibleSchema ${ObjectName}, (dove {ObjectName} è il nome di hello della classe oggetto strutturale hello predefinito, ad esempio: persona).
8. Inserisci risorsa selezionare hello sottomaschera (che è stato creato, ad esempio: TestSubform) e salvare sottomaschera ExtensibleSchema di hello ${ObjectName}.
9. Sostituire hello modello Directory Domino {PUBNAMES. NTFS} con il modello personalizzato nuova di hello {CONTOSO. NTFS} seguendo [procedura](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Chiudere Amministrazione Domino e aprire hello toorestart Domino Console servizio LDAP e hello tooReload Schema LDAP:
    * Nella Console di Domino, inserire il comando hello in **comando Domino** testo archiviato servizio LDAP di hello toorestart - [riavviare LDAP attività](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * schema LDAP tooreload indicare LDAP comando **indicare LDAP ReloadSchema**.
11. Aprire Amministrazione Domino e selezionare gli utenti e gruppi toosee scheda aggiunta attributo verrà riportato nel domino Aggiungi utente (con altri utenti di tabulazione).
12. Aprire Schema.nsf dalla scheda **Files** e vedere che l'attributo aggiunto è riportato nella classe di oggetti ausiliaria LDAP TestSubform.

**Approccio 3: Aggiungere hello attributo personalizzato toohello ExtensibleObject classe**

1. Apri file {Schema.nsf} inserito nella directory radice hello
2. Selezionare le classi di oggetti LDAP dal menu a sinistra di hello in **tutti i documenti di Schema** e fare clic su **classe Aggiungi oggetto** pulsante:
3. Specificare il nome LDAP nel formato hello {zzzExtensibleSchema} (dove zzz è hello Nome classe hello predefinito strutturale di oggetti, ad esempio persona). Schema di hello tooextend per classe di oggetti utente, ad esempio, fornire nome LDAP {PersonExtensibleSchema}.
4. Fornire il nome di classe dell'oggetto di livello superiore, per cui si desidera schema hello tooextend. Schema di hello tooextend per classe di oggetti utente, ad esempio, fornire il nome di classe superiore dell'oggetto {dominoPerson}:
5. Fornire una OID corrispondente toohello oggetto classe valida.
6. Selezionare gli attributi estesi/personalizzato in campi obbligatori o facoltativi i tipi di attributo in base ai requisiti di hello:
7. Dopo l'aggiunta necessari attributi toohello ExtensibleObjectClass, fare clic su **Salva e Chiudi**.
8. Viene creata una ExtensibleObjectClass per la rispettiva classe di oggetti predefinita con attributi estesi.

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Per informazioni su come tootroubleshoot tooenable registrazione hello connettore, vedere hello [come tooEnable traccia ETW per i connettori](http://go.microsoft.com/fwlink/?LinkId=335731).
