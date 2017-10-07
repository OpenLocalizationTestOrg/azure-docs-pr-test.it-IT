---
title: Connettore aaaPowerShell | Documenti Microsoft
description: Questo articolo viene descritto come connettore tooconfigure Microsoft di Windows PowerShell.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Documentazione tecnica sul connettore Windows PowerShell
Questo articolo descrive hello connettore di Windows PowerShell. articolo Hello applica toohello i seguenti prodotti:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * È necessario usare l'hotfix 4.1.3671.0 o versione successiva ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Per MIM2016 e FIM2010R2, è disponibile come download hello hello connettore [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Panoramica di hello connettore di PowerShell
Hello PowerShell connettore permette di servizio di sincronizzazione hello toointegrate con sistemi esterni che offrono API basate su Windows PowerShell. connettore Hello offre un bridge tra funzionalità hello dell'agente di gestione basata su chiamata extensible connectivity hello 2 framework (ECMA2) e Windows PowerShell. Per ulteriori informazioni su hello ECMA framework, vedere hello [Extensible Connectivity 2.2 gestione agente riferimento](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Prerequisiti
Prima di utilizzare connettore hello, verificare di che aver seguito hello sul server di sincronizzazione hello:

* Microsoft .NET 4.5.2 Framework o versione successiva
* Windows PowerShell 2.0, 3.0 o 4.0

criteri di esecuzione Hello nel server del servizio di sincronizzazione di hello devono essere script di Windows PowerShell toorun connettore hello tooallow configurato. A meno che non sono firmate digitalmente l'esecuzione del connettore di hello script hello, configurare i criteri di esecuzione hello eseguendo questo comando:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Creare un nuovo connettore
un connettore di Windows PowerShell nel servizio di sincronizzazione hello toocreate, è necessario fornire una serie di script di Windows PowerShell che eseguono passaggi hello richiesti dal servizio di sincronizzazione hello. A seconda origine dati hello ci si connette funzionalità hello tooand necessarie, è necessario implementare gli script di hello varia. In questa sezione illustra ogni script hello che può essere implementato e quando sono necessarie.

Hello connettore di Windows PowerShell progettato toostore script hello all'interno del database del servizio di sincronizzazione hello. Sebbene sia possibile toorun script che vengono archiviati nel file system di hello, risulta più semplice tooinsert hello corpo ogni script direttamente nella configurazione del connettore toohello.

tooCreate un connettore di PowerShell, in **servizio di sincronizzazione** selezionare **agente di gestione** e **crea**. Seleziona hello **PowerShell (Microsoft)** connettore.

![Create Connector](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Connettività
Specificare i parametri di configurazione per la connessione tooa di sistema remoto. Questi valori in modo sicuro sono archiviati dal servizio di sincronizzazione hello e apportati tooyour disponibili script di Windows PowerShell quando si esegue il connettore di hello.

![Connettività](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

È possibile configurare i seguenti parametri di connettività hello:

**Connettività**

| Parametro | Valore predefinito | Scopo |
| --- | --- | --- |
| Server |<Blank> |Nome del server che hello connettore deve connettersi. |
| Domain |<Blank> |Dominio di hello toostore di credenziali da utilizzare quando viene eseguito il connettore di hello. |
| Utente |<Blank> |Nome utente di hello toostore di credenziali da utilizzare quando viene eseguito il connettore di hello. |
| Password |<Blank> |Password di hello toostore di credenziali da utilizzare quando viene eseguito il connettore di hello. |
| Impersonate Connector Account |False |Se è true, il servizio di sincronizzazione hello esegue gli script di Windows PowerShell hello nel contesto di hello di hello credenziali fornite. Quando possibile, è consigliabile che hello **$Credentials** parametro viene passato tooeach script viene utilizzato invece la rappresentazione. Per ulteriori informazioni sulle autorizzazioni aggiuntive che sono necessari toouse questa opzione, vedere [configurazione aggiuntiva per la rappresentazione](#additional-configuration-for-impersonation). |
| Load User Profile When Impersonating |False |Indica al profilo utente di Windows tooload hello delle credenziali del connettore hello durante la rappresentazione. Se l'utente rappresentato hello dispone di un profilo di roaming, connettore hello non carica profilo mobile hello. Per ulteriori informazioni sulle autorizzazioni aggiuntive che sono necessari toouse questo parametro, vedere [configurazione aggiuntiva per la rappresentazione](#additional-configuration-for-impersonation). |
| Logon Type When Impersonating |None |Tipo di accesso durante la rappresentazione. Per ulteriori informazioni, vedere hello [dwLogonType] [ dw] documentazione. |
| Signed Scripts Only |False |Se true, il connettore di Windows PowerShell hello verifica che ogni script presenta una firma digitale valida. Se false, assicurarsi che i criteri di esecuzione di Windows PowerShell del server di servizio di sincronizzazione hello sono RemoteSigned o senza restrizioni. |

**Modulo comune**  
connettore Hello consente nella configurazione di hello toostore condiviso modulo di Windows PowerShell. Quando il connettore hello esegue uno script, hello modulo di Windows PowerShell estratte toohello sistema di file in modo che possa essere importato da ogni script.

Per gli script di importazione, esportazione e la sincronizzazione delle Password, modulo comune hello è cartella MAData toohello estratti del connettore. Per gli script di individuazione dello Schema, convalida, gerarchia e partizione modulo comune hello è cartella toohello estratti % TEMP %. In entrambi i casi, hello estratto modulo di script è denominato in base a impostazioni di nome di Script comune modulo toohello comune.

tooload un modulo denominato FIMPowerShellConnectorModule.psm1 dalla cartella MAData hello, utilizzare l'istruzione hello:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload un modulo denominato FIMPowerShellConnectorModule.psm1 dalla cartella % TEMP % di hello, utilizzare l'istruzione hello:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Convalida dei parametri**  
Lo Script di convalida Hello è uno script facoltativo di Windows PowerShell che può essere utilizzati tooensure che i parametri di configurazione del connettore forniti dall'amministratore di hello siano validi. Server convalida le credenziali di connessione e i parametri di connettività sono gli utilizzi comuni di script di convalida hello. lo script di convalida Hello viene chiamato dopo hello seguenti schede e finestre di dialogo sono stati modificati:

* Connettività
* Global Parameters
* Partition Configuration

lo script di convalida Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |scheda Configurazione Hello o una finestra che ha attivato la richiesta di convalida hello. |
| ConfigParameters |[KeyedCollection][keyk] [stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |

lo script di convalida Hello deve restituire una singola pipeline di toohello ParameterValidationResult oggetto.

**Individuazione dello schema**  
Hello script di individuazione dello Schema è obbligatorio. Questo script restituisce i tipi di oggetto hello, attributi e i vincoli di attributo che hello che servizio di sincronizzazione viene utilizzato quando si configura regole flusso di attributi. Hello script di individuazione dello Schema viene eseguito durante la creazione del connettore e popola dello schema del connettore hello. Viene inoltre utilizzato da hello azione Aggiorna Schema hello Synchronization Service Manager.

script di individuazione dello schema Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |

script Hello deve restituire un singolo [Schema] [ schema] toohello pipeline degli oggetti. oggetto dello Schema Hello è composta da [SchemaType] [ schemaT] gli oggetti che rappresentano i tipi di oggetto (ad esempio: utenti e gruppi). oggetto SchemaType Hello contiene una raccolta di [SchemaAttribute] [ schemaA] gli oggetti che rappresentano gli attributi di hello (ad esempio: nome, cognome e indirizzo postale) di tipo hello.

**Altri parametri**  
Inoltre le impostazioni di configurazione standard toohello, è possibile definire impostazioni di configurazione personalizzate aggiuntive che sono toohello specifico dell'istanza di hello connettore. Questi parametri possono essere specificati nel connettore hello, partizione, o livelli di passaggio eseguito e accessibile da uno script di Windows PowerShell rilevante hello. Impostazioni di configurazione personalizzate possono essere archiviate nel database di servizio di sincronizzazione hello in formato testo normale o può essere crittografati. Servizio di sincronizzazione Hello automaticamente vengono crittografate e decrittografate le impostazioni di configurazione protetta quando necessario.

impostazioni di configurazione personalizzate toospecify, il nome distinto hello di ogni parametro con una virgola (,).

impostazioni di configurazione personalizzate tooaccess da uno script, è necessario suffisso nome hello con un carattere di sottolineatura ( \_ ) e l'ambito di hello del parametro hello (globale o partizioni RunStep). Ad esempio, tooaccess hello parametro FileName globale, utilizzare il frammento di codice:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Capabilities
scheda delle funzionalità di gestione agente progettazione hello Hello definisce il comportamento di hello e le funzionalità del connettore hello. Impossibile modificare le selezioni di Hello effettuate in questa scheda quando è stato creato il connettore di hello. Questa tabella elenca le impostazioni di capacità hello.

![Capabilities](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Funzionalità | Descrizione |
| --- | --- |
| [Distinguished Name Style][dnstyle] (Stile di nome distinto) |Indica se il connettore hello supporta nomi distinti e in tal caso, lo stile. |
| [Export Type][exportT] (Tipo di esportazione) |Determina il tipo di hello di oggetti che vengono presentati toohello script di esportazione. <li>Quando viene modificato l'attributo hello, AttributeReplace – include hello completo set di valori per un attributo multivalore.</li><li>Quando viene modificato l'attributo hello, AttributeUpdate: include solo hello delta tooa attributo multivalore.</li><li>MultivaluedReferenceAttributeUpdate: include un set completo di valori per attributi multivalore non di riferimento e solo i valori differenziali per gli attributi di riferimento con più valori.</li><li>ObjectReplace: include tutti gli attributi per un oggetto quando viene modificato qualsiasi attributo</li> |
| [Data Normalization][DataNorm] (Normalizzazione dei dati) |Indica gli attributi di ancoraggio di hello del servizio di sincronizzazione toonormalize prima tooscripts vengono forniti. |
| [Object Confirmation][oconf] (Conferma degli oggetti) |Configura hello in sospeso il comportamento di importazione in hello servizio di sincronizzazione. <li>Normale: il comportamento predefinito che prevede esportate tutte le modifiche toobe confermato tramite importazione</li><li>NoDeleteConfirmation: quando viene eliminato un oggetto, non viene generata alcuna importazione in sospeso.</li><li>NoAddAndDeleteConfirmation: quando viene creato o eliminato un oggetto, non viene generata alcuna importazione in sospeso.</li> |
| Use DN as Anchor |Se hello stile nome distinto è impostato tooLDAP, attributo di ancoraggio hello per spazio connettore hello è anche il nome distinto di hello. |
| Concurrent Operations of Several Connectors |Se selezionata, è possibile eseguire contemporaneamente più connettori Windows PowerShell. |
| Partitions |Se selezionata, il connettore hello supporta più partizioni e l'individuazione di partizione. |
| Hierarchy |Se selezionata, il connettore di hello supporta una struttura gerarchica di stile LDAP. |
| Enable Import |Se selezionata, il connettore hello Importa i dati tramite gli script di importazione. |
| Enable Delta Import |Se selezionata, può richiedere connettore hello delta da hello Importa gli script. |
| Enable Export |Se selezionata, il connettore hello Esporta i dati tramite script di esportazione. |
| Enable Full Export |Se selezionata, hello esportare il supporto di script esportazione spazio connettore intera hello. toouse che debba essere controllata anche questa opzione, abilitare l'esportazione. |
| No Reference Values In First Export Pass |Se selezionata, gli attributi di riferimento vengono esportati in un secondo passaggio di esportazione. |
| Enable Object Rename |Se selezionata, è possibile modificare i nomi distinti. |
| Delete-Add As Replace |Se selezionata, le operazioni di eliminazione-aggiunta vengono esportate come una singola sostituzione. |
| Enable Password Operations |Se selezionata, gli script di sincronizzazione password sono supportati. |
| Enable Export Password in First Pass |Se selezionata, le password impostata durante il provisioning vengono esportate quando viene creato l'oggetto hello. |

### <a name="global-parameters"></a>Global Parameters
scheda parametri globali Hello hello Management Agent Designer consente gli script di Windows PowerShell hello tooconfigure eseguiti dal connettore hello. È anche possibile configurare valori globali per le impostazioni di configurazione personalizzate definite nella scheda connettività hello.

**Individuazione della partizione**  
Una partizione è uno spazio dei nomi separato all'interno di uno schema condiviso. Ad esempio, in Active Directory ogni dominio è una partizione all'interno di una foresta. Una partizione è un raggruppamento logico di hello per l'importazione e operazioni di esportazione. Queste hanno per contesto la partizione e tutte le operazioni vengono eseguite in questo contesto. Le partizioni dovrebbero toorepresent una gerarchia in LDAP. nome distinto di Hello di una partizione viene utilizzata nell'importazione tooverify tutte restituito oggetti rientrano nell'ambito di hello di una partizione. nome distinto della partizione Hello viene inoltre utilizzato durante il provisioning di hello metaverse toohello connettore spazio toodetermine hello partizione che deve essere associato a un oggetto durante l'esportazione.

script di individuazione partizione Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |

Hello script deve restituire un un singolo [partizione] [ part] oggetto o un elenco [T] della pipeline di toohello oggetti partizione.

**Individuazione della gerarchia**  
script di individuazione gerarchia Hello viene utilizzato solo quando hello funzionalità di stile di nome distinto LDAP. script Hello è tooallow usato è toobrowse e selezionare un set di contenitori che è considerato interno o all'esterno dell'ambito per importare ed esportare le operazioni. script Hello deve fornire solo un elenco di nodi che sono figli diretti di hello radice fornito nodo toohello script.

script di individuazione gerarchia Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| ParentNode |[HierarchyNode][hn] |nodo radice di Hello della gerarchia hello in cui hello script deve restituire gli elementi figlio diretti. |

script Hello deve restituire un oggetto HierarchyNode singolo elemento figlio o un elenco [T] della pipeline di toohello oggetti HierarchyNode figlio.

#### <a name="import"></a>Importa
I connettori che supportano operazioni di importazione devono implementare tre script.

**Avvio dell'importazione**  
Hello iniziare l'importazione dello script viene eseguito all'inizio di hello di un passaggio di esecuzione di importazione. Durante questo passaggio, è possibile stabilire un sistema di origine toohello di connessione ed eseguire i passaggi preparatori prima di importare dati da hello connesso sistema.

avviare l'importazione Hello script riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa script hello tipo hello di eseguire importazione delta o full, partizione, gerarchia, filigrana e dimensioni di pagina previsto. |
| Tipi |[Schema][schema] |Schema per spazio connettore hello che viene importato. |

script Hello deve restituire un singolo [OpenImportConnectionResults] [ oicres] oggetto toohello pipeline, ad esempio:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Importazione dei dati**  
Hello Importa dati script viene chiamato dal connettore hello finché script hello non indica che è presente alcun più tooimport di dati. connettore di Windows PowerShell Hello ha una dimensione di pagina di 9.999 oggetti. Se lo script restituisce più di 9.999 oggetti per l'importazione, è necessario supportare il paging. espone connettore di Hello viene chiamata una proprietà di dati personalizzato che è possibile utilizzare tooa archivio una filigrana in modo che ogni hello ora importare script di dati, lo script riprende l'importazione di oggetti in cui è stata interrotta.

Hello Importa dati script riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Contiene hello filigrana (CustomData) che può essere utilizzato durante l'importazione di paging e l'importazione delta. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa script hello tipo hello di eseguire importazione delta o full, partizione, gerarchia, filigrana e dimensioni di pagina previsto. |
| Tipi |[Schema][schema] |Schema per spazio connettore hello che viene importato. |

Hello Importa dati script necessario scrivere un elenco [[CSEntryChange][csec]] toohello pipeline degli oggetti. Questa raccolta è costituita da attributi CSEntryChange che rappresentano ogni oggetto da importare. Durante l'esecuzione di una importazione completa, questa raccolta deve avere un set completo di oggetti CSEntryChange con tutti gli attributi per ogni oggetto. Durante un'importazione Delta, oggetto CSEntryChange hello deve contenere delta livello di attributo hello per tooimport ogni oggetto o una rappresentazione completa di oggetti hello che sono stati modificati (modalità sostituzione).

**Fine importazione**  
Al termine dell'importazione di hello eseguire hello hello fine Import script viene eseguito. Questo script deve eseguire le necessarie operazioni di pulizia (ad esempio, Chiudi connessioni toosystems e rispondere toofailures).

script di importazione fine Hello riceve hello seguenti parametri dal connettore hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa script hello tipo hello di eseguire importazione delta o full, partizione, gerarchia, filigrana e dimensioni di pagina previsto. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Informa script hello motivo hello importazione hello è stata terminata. |

script Hello deve restituire un singolo [CloseImportConnectionResults] [ cicres] oggetto toohello pipeline, ad esempio:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Esporta
Toohello identici importazione architettura del connettore hello, è necessario implementare tre script connettori che supportano l'esportazione.

**Avvio dell'importazione**  
avviare l'esportazione Hello script viene eseguito all'inizio di hello di un passaggio di esportazione eseguire. Durante questo passaggio, è possibile stabilire un sistema di origine toohello di connessione e prevedono operazioni preparatorie prima dell'esportazione dati toohello connesso sistema.

avviare l'esportazione Hello script riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa script hello tipo hello di esportazione eseguire (delta o full), partizione, gerarchia e dimensioni di pagina previsto. |
| Tipi |[Schema][schema] |Schema per spazio connettore hello esportata. |

script Hello non dovrebbe restituire qualsiasi pipeline toohello di output.

**Esportazione dei dati**  
Servizio di sincronizzazione Hello richiama script di esportazione di dati hello quante volte è necessario tooprocess tutte le esportazioni in sospeso. Se lo spazio connettore hello dispone di più esportazioni in sospeso di hello dimensioni della pagina del connettore, esportare hello script di dati può essere chiamato più volte e possibilmente più volte per hello stesso oggetto.

script di dati di esportazione Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| CSEntries |IList[CSEntryChange][csec] |Elenco di tutti gli spazi connettore hello gli oggetti in sospeso toobe esportazioni elaborati durante questo passaggio. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa script hello tipo hello di esportazione eseguire (delta o full), partizione, gerarchia e dimensioni di pagina previsto. |
| Tipi |[Schema][schema] |Schema per spazio connettore hello esportata. |

Hello script di esportazione dei dati deve restituire un [PutExportEntriesResults] [ peeres] toohello pipeline degli oggetti. Questo oggetto non è necessario le informazioni sul risultato tooinclude per ogni connettore esportati a meno che non si verifica un errore o un attributo di ancoraggio toohello di modifica. Ad esempio, tooreturn una pipeline di toohello PutExportEntriesResults oggetto:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Fine esportazione**  
In conclusione hello dell'esportazione hello eseguito, hello fine esportare toorun script. Questo script deve eseguire le necessarie operazioni di pulizia (ad esempio, Chiudi connessioni toosystems e rispondere toofailures).

script di esportazione fine Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa script hello tipo hello di esportazione eseguire (delta o full), partizione, gerarchia e dimensioni di pagina previsto. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Informa script hello motivo hello esportazione hello è stata terminata. |

script Hello non dovrebbe restituire qualsiasi pipeline toohello di output.

#### <a name="password-synchronization"></a>Sincronizzazione delle password
I connettori Windows PowerShell possono essere usati come destinazione per la modifica o la reimpostazione delle password.

script di password Hello riceve i seguenti parametri dal connettore hello hello:

| Nome | Tipo di dati | Descrizione |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][stringa, [ConfigParameter][cp]] |Tabella di parametri di configurazione per hello connettore. |
| Credenziali |[PSCredential][pscred] |Contiene le credenziali immesse dall'amministratore hello nella scheda connettività hello. |
| Partition |[Partizione][part] |Partizione di directory che hello CSEntry è in. |
| CSEntry |[CSEntry][cse] |Spazio del connettore per oggetto hello che ha ricevuto una modifica della password o reimpostazione. |
| OperationType |String |Indica se l'operazione di hello è una reimpostazione (**SetPassword**) o una modifica (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Flag che specificano hello è destinato il comportamento di reimpostazione della password. Questo parametro è disponibile unicamente se OperationType è **SetPassword**. |
| OldPassword |String |Popolato con la password corrente dell'oggetto hello per le modifiche delle password. Questo parametro è disponibile unicamente se OperationType è **ChangePassword**. |
| NewPassword |String |Compilato con una nuova password dell'oggetto hello che deve essere impostato script hello. |

Hello script password è di qualsiasi pipeline di Windows PowerShell toohello risultati tooreturn non previsto. Se si verifica un errore nello script password hello, deve generare script hello uno dei seguenti eccezioni tooinform hello servizio di sincronizzazione sul problema hello hello:

* [PasswordPolicyViolationException] [ pwdex1] – generata se hello password non soddisfa i criteri di password hello nel sistema hello connesso.
* [PasswordIllFormedException] [ pwdex2] – generata se la password di hello è accettabile per il sistema hello connesso.
* [PasswordExtension] [ pwdex3] : per tutti gli altri errori nello script di hello password generata.

## <a name="sample-connectors"></a>Connettori di esempio
Per una panoramica completa dei connettori di esempio disponibili hello, vedere [insieme connettore di Windows PowerShell connettore esempio][samp].

## <a name="other-notes"></a>Altre note
### <a name="additional-configuration-for-impersonation"></a>Configurazione aggiuntiva per la rappresentazione
Concedere all'utente hello è rappresentato hello seguenti autorizzazioni nel server di servizio di sincronizzazione hello:

Accesso in lettura toohello seguenti chiavi del Registro di sistema:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

hello toodetermine ID di sicurezza (SID) dell'account di servizio del servizio di sincronizzazione hello, eseguire i comandi di PowerShell seguente hello:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Accesso in lettura toohello cartelle del file system seguenti:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Sostituire il nome di hello del connettore di Windows PowerShell hello segnaposto hello {ConnectorName}.

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Per informazioni su come tootroubleshoot tooenable registrazione hello connettore, vedere hello [come tooEnable traccia ETW per i connettori](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
