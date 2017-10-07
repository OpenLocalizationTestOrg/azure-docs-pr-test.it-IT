---
title: Connettore SQL aaaGeneric | Documenti Microsoft
description: Questo articolo viene descritto come connettore SQL generico tooconfigure Microsoft.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Documentazione tecnica sul connettore Generic SQL
Questo articolo descrive hello connettore SQL generico. articolo Hello applica toohello i seguenti prodotti:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * È necessario usare l'hotfix 4.1.3671.0 o versione successiva ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Per MIM2016 e FIM2010R2, è disponibile come download hello hello connettore [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee questo connettore in azione, vedere hello [connettore SQL generico dettagliate](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) articolo.

## <a name="overview-of-hello-generic-sql-connector"></a>Panoramica di hello connettore SQL generico
Hello connettore SQL generico consente di servizio di sincronizzazione hello toointegrate con un sistema di database che offre connettività ODBC.  

Dal punto di vista di alto livello, hello seguenti caratteristiche è supportata dalla versione corrente di hello del connettore hello:

| Funzionalità | Supporto |
| --- | --- |
| Origine dati connessa |Connettore Hello è supportato con tutti i driver ODBC a 64 bit. È stato testato con seguenti hello: <li>Microsoft SQL Server e QL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 e 11g</li><li>MySQL 5.x</li> |
| Scenari |<li>Gestione del ciclo di vita degli oggetti</li><li>Gestione delle password</li> |
| Operazioni |<li>Importazione completa e importazione ed esportazione differenziale</li><li>Per l'esportazione: Aggiungi, Elimina, Aggiorna e Sostituisci</li><li>Imposta password, Cambia password</li> |
| Schema |<li>Individuazione dinamica di oggetti e attributi</li> |

### <a name="prerequisites"></a>Prerequisiti
Prima di utilizzare connettore hello, verificare di che aver seguito hello sul server di sincronizzazione hello:

* Microsoft .NET 4.5.2 Framework o versione successiva
* Driver client ODBC a 64 bit

### <a name="permissions-in-connected-data-source"></a>Autorizzazioni nell'origine dati connessa
toocreate o eseguire una delle operazioni di hello è supportato nel connettore SQL generico, è necessario disporre di:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Porte e protocolli
Per hello porte necessarie per hello ODBC driver toowork, consultare la documentazione del fornitore del database hello.

## <a name="create-a-new-connector"></a>Creare un nuovo connettore
tooCreate un connettore di SQL generico, in **servizio di sincronizzazione** selezionare **agente di gestione** e **crea**. Seleziona hello **SQL generico (Microsoft)** connettore.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Connettività
Hello connettore utilizza un file DSN ODBC per la connettività. Creare hello DSN file utilizzando **origini dati ODBC** disponibile nel menu start hello in **strumenti di amministrazione**. Nello strumento di amministrazione di hello, creare un **DSN su File** in modo che può essere fornita toohello connettore.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

schermata di connettività Hello è hello innanzitutto quando si crea un nuovo connettore SQL generico. È innanzitutto necessario hello tooprovide le seguenti informazioni:

* Percorso del file DSN
* Autenticazione
  * User Name
  * Password

database Hello deve supportare uno di questi metodi di autenticazione:

* **L'autenticazione di Windows**: hello autenticazione database Usa utente di hello tooverify credenziali Windows hello. Hello nome utente/password specificata è tooauthenticate utilizzate con database hello. Questo account deve database toohello delle autorizzazioni.
* **L'autenticazione di SQL**: hello l'autenticazione di database utilizza hello nome utente/password è definito un database di toohello tooconnect hello connettività dello schermo. Se si archiviano hello nome di utente/password nel file DSN hello, credenziali hello fornite nella schermata di connettività hello hanno la precedenza.
* **L'autenticazione del Database di SQL Azure**: per ulteriori informazioni, vedere [connettersi tooSQL Database usando Azure Active Directory l'autenticazione](../../sql-database/sql-database-aad-authentication.md).

**Nome distinto è ancoraggio**: se si seleziona questa opzione, hello nome distinto viene usato anche come attributo di ancoraggio hello. Può essere utilizzato per un'implementazione semplice, ma dispone anche di hello seguente limitazione:

* Il connettore supporta solo un tipo di oggetto. Pertanto, qualsiasi riferimento attributi possono fare riferimento solo hello stesso tipo di oggetto.

**Tipo di esportazione: Sostituzione dell'oggetto**: durante l'esportazione, quando sono stati modificati solo alcuni attributi, viene esportata l'intero oggetto di hello con tutti gli attributi e sostituisce hello oggetto esistente.

### <a name="schema-1-detect-object-types"></a>Schema 1 (rilevare i tipi di oggetto)
In questa pagina si intende tooconfigure come hello connettore è corso toofind hello diversi tipi di oggetti nel database di hello.

Ogni tipo di oggetto viene presentato come una partizione e configurato ulteriormente in **Configurare partizioni e gerarchie**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Il metodo di rilevamento di tipo dell'oggetto**: hello connettore supporta questi metodi di rilevamento di tipo di oggetto.

* **Valore fisso**: È fornire hello elenco di tipi di oggetto con un elenco delimitato da virgole. Ad esempio: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Tabella/vista/Stored Procedure**: fornire hello nomi di tabella/vista/stored procedure hello e quindi hello colonna che fornisce l'elenco di hello dei tipi di oggetto. Se si utilizza una stored procedure, quindi anche fornire parametri per il nel formato hello **[nome]: [direzione]: [valore]**. Fornire ogni parametro in una riga separata (usare Ctrl + Invio tooget una nuova riga).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **Query SQL**: questa opzione consente di una query SQL che restituisce una singola colonna con tipi di oggetto, ad esempio tooprovide `SELECT [Column Name] FROM TABLENAME`. Hello restituito colonna deve essere di tipo stringa (varchar).

### <a name="schema-2-detect-attribute-types"></a>Schema 2 (rilevare i tipi di attributo)
In questa pagina, si sta tooconfigure hello come nomi di attributi e tipi verranno toobe rilevato. opzioni di configurazione Hello sono elencate per ogni tipo di oggetto rilevato nella pagina precedente hello.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Il metodo di rilevamento di tipo attributo**: hello connettore supporta i metodi di rilevamento di tipo attributo con ogni tipo di oggetto rilevato nella schermata di Schema 1.

* **Tabella/vista/Stored Procedure**: specificare il nome di hello di hello tabella/vista/stored procedure che devono essere nomi di attributo hello toofind utilizzato. Se si utilizza una stored procedure, quindi anche fornire parametri per il nel formato hello **[nome]: [direzione]: [valore]**. Fornire ogni parametro in una riga separata (usare Ctrl + Invio tooget una nuova riga). i nomi di attributo hello toodetect in un attributo multivalore, fornire un elenco delimitato da virgole delle tabelle o viste. Gli scenari multivalore non sono supportati quando le tabelle padre e figlio hanno gli stessi nomi di colonna.
* **Query SQL**: questa opzione consente di una query SQL che restituisce una singola colonna con i nomi di attributo, ad esempio tooprovide `SELECT [Column Name] FROM TABLENAME`. Hello restituito colonna deve essere di tipo stringa (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Schema 3 (definire ancoraggio e DN)
Questa pagina consente tooconfigure ancoraggio e l'attributo DN per ogni tipo di oggetto rilevato. È possibile selezionare più attributi toomake hello ancoraggio univoco.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Non sono elencati gli attributi multivalore e booleani.
* Attributo stesso non è possibile utilizzare per DN e ancoraggio, a meno che non **DN è ancoraggio** è selezionata nella pagina connettività hello.
* Se **DN è ancoraggio** è selezionata nella pagina connettività hello, questa pagina richiede l'unico attributo hello DN. Questo attributo verrà utilizzato anche come attributo di ancoraggio hello.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Schema 4 (definire tipo di attributo, riferimento e direzione)
Questa pagina consente di tipo di attributo hello tooconfigure, ad esempio integer, binary o valore booleano e direzione per ogni attributo. Tutti gli attributi della pagina **Schema 2** sono elencati con i relativi attributi multivalore.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Tipo di dati**: toomap hello attributo tipo toothose tipi noti dal motore di sincronizzazione hello utilizzati. valore predefinito di Hello è hello toouse dello stesso tipo, come rilevato nello schema SQL hello, ma DateTime e il riferimento non sono facilmente rilevabili. Per gli utenti, è necessario toospecify **DateTime** o **riferimento**.
* **Direzione**: È possibile impostare hello attributo direzione tooImport, l'esportazione o la soluzione del problema. ImportExport è il valore predefinito.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Note:

* Se un tipo di attributo non è rilevabile da hello connettore, viene utilizzato il tipo di dati stringa hello.
* **Nested tables** possono essere considerate tabelle di database di una colonna. Oracle archivia le righe di hello di una tabella nidificata in nessun ordine particolare. Tuttavia, quando si recupera la tabella nidificata hello in una variabile di PL/SQL, righe hello figurano pedici consecutivi a partire da 1. Che consente di righe tooindividual di accesso di tipo matrice.
* **VARRYS** non sono supportati nel connettore hello.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Schema 5 (definire la partizione per gli attributi di riferimento)
In questa pagina si configura, per tutti gli attributi di riferimento, a quale partizione (tipo di oggetto) fa riferimento un attributo.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Se si utilizza **DN è ancoraggio**, è necessario utilizzare hello stesso tipo di oggetto come hello uno da cui si fa riferimento. Non è possibile fare riferimento a un altro tipo di oggetto.

>[!NOTE]
Aggiornamento di marzo 2017 hello è ora disponibile un'opzione per a partire da "*" quando questa opzione è selezionata, quindi tutti i tipi di membro possibili verranno importati.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 A partire da maggio 2017 hello "*" aka **qualsiasi opzione** è stata modificata toosupport importare ed esportare il flusso. Se si desidera toouse questa opzione la tabella/vista multivalore deve avere un attributo che contiene il tipo di oggetto hello.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Se "*" è selezionata, quindi è necessario specificare anche il nome di hello della colonna di hello con tipo di oggetto hello.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Dopo l'importazione verrà visualizzato un codice simile immagine toohello riportata di seguito:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Global Parameters
pagina parametri globali Hello è usato tooconfigure importazione Delta, il formato di data/ora e il metodo di Password.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Hello connettore SQL generico supporta hello dei seguenti metodi per l'importazione Delta:

* **Trigger**: vedere l'articolo relativo alla [generazione di visualizzazioni delta con trigger](https://technet.microsoft.com/library/cc708665.aspx).
* **Watermark**(Limite): approccio generico che può essere usato con qualsiasi database. query di filigrana Hello viene pre-popolato in base fornitore hello del database. In ogni tabella o visualizzazione usata deve essere presente una colonna Watermark. Questa colonna deve essere rilevati relativi dipendenti e gli inserimenti e aggiornamenti di tabelle toohello come (multivalore o figlio) le tabelle. è necessario sincronizzare gli orologi di Hello tra il servizio di sincronizzazione e il server di database di hello. In caso contrario, potrebbero essere omesse alcune voci nell'importazione delta hello.  
  Limitazione:
  * La strategia Watermark (Limite) non supporta gli oggetti eliminati.
* **Snapshot**(funziona solo con Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)
* **Change Tracking**(funziona solo con Microsoft SQL Server) [Informazioni sul rilevamento delle modifiche (SQL Server)](https://msdn.microsoft.com/library/bb933875.aspx)  
  Limitazioni:
  * Attributo DN & di ancoraggio deve essere parte della chiave primaria per l'oggetto selezionato di hello nella tabella hello.
  * La query SQL non è supportata durante l'importazione e l'esportazione con il rilevamento delle modifiche.

**Parametri aggiuntivi**: specificare hello fuso orario del Server Database che indica dove si trova il server di Database. Questo valore viene utilizzato toosupport hello vari formati di data e ora di attributi.

Hello connettore archivia sempre data e data e ora in formato UTC. toobe toocorrectly in grado di convertire volte e data hello, hello fuso orario del server di database hello e formato hello utilizzato deve essere specificato. formato Hello deve essere espressa nel formato .net.

Durante l'esportazione è necessario fornire a ogni attributo di tempo data toohello connettore in formato ora UTC.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Configurazione delle password**: connettore hello fornisce funzionalità di sincronizzazione delle password e supporta imposta e modifica la password.

Hello Connector fornisce due metodi di sincronizzazione delle password toosupport:

* **Stored Procedure**: questo metodo richiede due stored procedure toosupport Set e modificare la password. Digitare tutti i parametri per l'aggiunta e modifica password hello in **impostare Password SP** e **modificare Password SP** parametri rispettivamente come per ogni esempio seguente.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Estensione password**: questo metodo richiede una DLL di estensione delle Password (è necessario hello tooprovide nome di DLL di estensione che implementa hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface). Assembly dell'estensione per la password deve essere posizionato nella cartella di estensione in modo che il connettore hello in grado di caricare hello DLL in fase di esecuzione.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

È inoltre tooenable hello, la gestione delle Password in hello **configurare estensione** pagina.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurare partizioni e gerarchie
Nella pagina partizioni e gerarchie hello selezionare tutti i tipi di oggetto. Ogni tipo di oggetto si trova nella propria partizione.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

È inoltre possibile sostituire i valori hello definiti in hello **connettività** o **parametri globali** pagina.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Configurare gli ancoraggi
Questa pagina è di sola lettura poiché ancoraggio hello è già stato definito. Hello attributo di ancoraggio selezionato viene sempre aggiunto con tooensure tipo di oggetto hello rimane univoco tra i tipi di oggetto.

![ancoraggi](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Configurare il parametro per l'esecuzione dei passaggi
Questi passaggi vengono configurati per profili di esecuzione hello connettore hello. Queste configurazioni hello l'effettiva operazione di importazione ed esportazione di dati.

### <a name="full-and-delta-import"></a>Importazione completa e delta
Il connettore Generic SQL supporta l'importazione completa e delta usando questi metodi:

* Tabella
* View
* Stored Procedure
* Query SQL

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Table/View**  
gli attributi multivalore tooimport per un oggetto, sono presenti nome tabella/vista delimitato da virgole di hello tooprovide **viste delle tabelle/nome di multivalore** e condizioni di join rispettivi in hello **condizioneJoin**con la tabella padre hello.

Esempio: Si desidera oggetto dipendente di tooimport hello e tutti i relativi attributi multivalore. Sono presenti due tabelle denominate Employee (tabella principale) e Department (multivalore).
Hello seguenti:

* Digitare **Employee** in **Table/View/SP**.
* Digitare Department in **Name of Multi-Valued table/views**.
* Digitare la condizione di join hello tra dipendente e reparto **condizione di Join**, ad esempio `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Stored procedure**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Se si dispone di quantità di dati, si consiglia di paginazione tooimplement con le Stored procedure.
* Per l'impaginazione toosupport Stored Procedure, è necessario tooprovide indice iniziale e finale. Vedere: [Paging in modo efficiente di grandi quantità di dati](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndex e @EndIndex vengono sostituiti in fase di esecuzione con il rispettivo valore di dimensione della pagina configurato nella pagina **Configure Step** (Passaggio di configurazione). Ad esempio, quando il connettore hello recupera prima e dimensioni di pagina hello è 500, in tale situazione @StartIndex sarà 1 e @EndIndex 500. Questi valori aumentare quando connettore consente di recuperare pagine successive e modificare hello @StartIndex & @EndIndex valore.
* tooexecute Stored Procedure con parametri, specificare i parametri di hello in `[Name]:[Direction]:[Value]` formato. Immettere ogni parametro in una riga separata (usare Ctrl + Invio tooget una nuova riga).
* Il connettore Generic SQL supporta anche l'operazione di importazione dai server collegati in Microsoft SQL Server. Se devono essere recuperati da una tabella nel server collegato, tabella deve essere fornita nel formato hello:`[ServerName].[Database].[Schema].[TableName]`
* Il connettore Generic SQL supporta solo gli oggetti che presentano una struttura simile (sia nome alias che tipo di dati) tra le informazioni sui passaggi esecuzione e il rilevamento dello schema. Se selezionata hello oggetto dello schema e le informazioni fornite in fase di esecuzione è diverso, il connettore SQL toosupport Impossibile questo tipo di scenari.

**Query SQL**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Le query con più set di risultati non sono supportate.
* Query SQL supporta hello paginazione e fornisce l'inizio e fine dell'indice come una variabile toosupport la paginazione.

### <a name="delta-import"></a>Importazione differenziale
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

La configurazione dell'importazione differenziale richiede un numero maggiore di operazioni di configurazione rispetto all'importazione completa.

* Se si sceglie approccio Trigger o di uno Snapshot di hello le modifiche delta tootrack, quindi specificare una tabella di cronologia o Snapshot del database in **nome tabella di cronologia o Snapshot del database** casella.
* È inoltre necessario tooprovide condizione di join tra la tabella di cronologia e la tabella padre, ad esempio`Employee.ID=History.EmployeeID`
* transazione di hello tootrack nella tabella padre hello dalla tabella di cronologia hello, è necessario fornire nome della colonna hello che contiene informazioni sull'operazione di hello (aggiunta/aggiornamento/eliminazione).
* Se si sceglie di filigrana tootrack le modifiche delta, quindi fornire nome della colonna che contiene informazioni sull'operazione hello in hello **nome colonna di acqua contrassegno**.
* Hello **modificare l'attributo di tipo** colonna è obbligatoria per il tipo di modifica di hello. Questa colonna esegue il mapping di una modifica che si verifica nella tabella primaria hello o tabella multivalore tooa cambiare tipo nella visualizzazione delta hello. Questa colonna può contenere i tipo di modifica di hello Modify_Attribute per modificare a livello di attributo o un'aggiunta, modifica o eliminazione cambiare tipo per un tipo di modifica a livello di oggetto. Se è diverso dal valore predefinito di hello Aggiungi, modifica o eliminazione, quindi è possibile definire tali valori usando questa opzione.

### <a name="export"></a>Esporta
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

Il connettore Generic SQL supporta l'esportazione tramite quattro metodi supportati, ad esempio:

* Tabella
* View
* Stored Procedure
* Query SQL

**Table/View**  
Se si sceglie l'opzione di tabella/vista hello, connettore hello genera hello rispettive query toodo hello esportazione.

**Stored procedure**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Se si sceglie l'opzione di Stored Procedure hello, esportazione richiede tre diverse Stored procedure tooperform Insert/Update/Delete operazioni.

* **Aggiungere il nome del provider**: SP questo viene eseguito se qualsiasi oggetto proviene tooconnector per l'inserimento nella tabella corrispondente hello.
* **Aggiornare il nome del provider**: SP questo viene eseguito se qualsiasi oggetto proviene tooconnector per l'aggiornamento nella tabella corrispondente hello.
* **Eliminare il nome del provider**: SP questo viene eseguito se qualsiasi oggetto proviene tooconnector per l'eliminazione nella tabella corrispondente hello.
* Attributo selezionato da hello utilizzato come toohello stored procedure valore parametro. Ad esempio, `EmployeeName: INPUT: @EmployeeName` (EmployeeName è selezionato nello schema connettore hello e connettore hello sostituisce rispettivo valore hello durante questa operazione di esportazione)
* toorun stored procedure con parametri, specificare i parametri in `[Name]:[Direction]:[Value]` formato. Immettere ogni parametro in una riga separata (usare Ctrl + Invio tooget una nuova riga).

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Se si sceglie l'opzione di query SQL hello, esportazione richiede che tre diverse operazioni Insert/Update/Delete tooperform una query.

* **Query di Accodamento**: questa query viene eseguita se qualsiasi oggetto proviene tooconnector per l'inserimento nella tabella corrispondente hello.
* **Query di aggiornamento**: questa query viene eseguita se qualsiasi oggetto proviene tooconnector per l'aggiornamento nella tabella corrispondente hello.
* **Query di eliminazione**: questa query viene eseguita se qualsiasi oggetto proviene tooconnector per l'eliminazione nella tabella corrispondente hello.
* Attributo selezionato da hello utilizzato come una parametro del valore toohello query, ad esempio`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Per informazioni su come tootroubleshoot tooenable registrazione hello connettore, vedere hello [come tooEnable traccia ETW per i connettori](http://go.microsoft.com/fwlink/?LinkId=335731).
