---
title: integrazione di aaaDirectory tra Azure multi-Factor Authentication e Active Directory
description: "Si tratta hello Azure multi-factor authentication pagina in cui viene descritto come toointegrate hello Server Azure multi-Factor Authentication con Active Directory, è possibile sincronizzare le directory hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Integrazione di directory tra il server Azure MFA e Active Directory
Utilizzare sezione integrazione Directory hello di hello Azure MFA Server toointegrate con Active Directory o un'altra directory LDAP. È possibile configurare gli attributi toomatch hello schema di directory e configurare la sincronizzazione automatica di utente.

## <a name="settings"></a>Impostazioni
Per impostazione predefinita, hello Server Azure multi-Factor Authentication (MFA) è configurata tooimport o sincronizzare utenti da Active Directory.  Nella scheda Integrazione Directory Hello consente si toooverride hello comportamento predefinito e tooa toobind altra directory LDAP, una directory ADAM o un controller di dominio Active Directory specifico.  Fornisce inoltre hello all'uso dell'autenticazione LDAP tooproxy LDAP o per il binding LDAP come destinazione RADIUS, preautenticazione per l'autenticazione IIS o autenticazione primaria per il portale per gli utenti.  Hello nella tabella seguente vengono descritte le singole impostazioni hello.

![Impostazioni](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Funzionalità | Descrizione |
| --- | --- |
| Usa Active Directory |Selezionare toouse di opzione Usa Active Directory hello Active Directory per l'importazione e la sincronizzazione.  Questo è l'impostazione predefinita hello. <br>Nota: Per Active Directory integration toowork correttamente, join domain tooa di hello computer e accedere con un account di dominio. |
| Includi domini trusted |Controllare **Includi domini Trusted** toohave hello agente tentativo tooconnect toodomains considerato attendibile da hello dominio corrente, un altro dominio nella foresta hello o i domini coinvolti in un trust tra foreste.  Se non l'importazione o la sincronizzazione degli utenti da uno qualsiasi dei hello domini trusted, deselezionare prestazioni tooimprove di hello casella di controllo.  valore predefinito di Hello è selezionata. |
| Usa configurazione LDAP specifica |Selezionare hello utilizza LDAP opzione toouse hello impostazioni LDAP specificate per l'importazione e la sincronizzazione. Nota: Quando si seleziona utilizza LDAP, interfaccia utente di hello riferimenti cambia da Active Directory tooLDAP. |
| Pulsante Modifica |pulsante di modifica Hello consente le impostazioni di configurazione di hello corrente LDAP toomodified. |
| Usa query con ambito di attributi |Indica se è necessario usare le query con ambito di attributi.  Query per ambito attributo consentono ricerche efficienti nelle directory record validi in base alle voci di hello nell'attributo di un altro record.  Hello del Server Azure multi-Factor Authentication Usa attributo ambito query tooefficiently query hello gli utenti che sono membri di un gruppo di sicurezza.   <br>Nota: in alcuni casi le query con ambito di attributi sono supportate ma non è consigliabile usarle.  Ad esempio, è possibile che in Active Directory si verifichino problemi con le query con ambito di attributi quando un gruppo di sicurezza include membri appartenenti a più di un dominio. In questo caso, deselezionare la casella di controllo di hello. |

Hello nella tabella seguente descrive le impostazioni di configurazione LDAP hello.

| Funzionalità | Descrizione |
| --- | --- |
| Server |Immettere nome host hello o l'indirizzo IP del server hello directory LDAP hello.  È anche possibile specificare un server di backup separato da un punto e virgola. <br>Nota: se per Tipo di binding è selezionato SSL, è necessario un nome host completo. |
| Nome distinto di base |Immettere nome distinto di hello hello base dell'oggetto di directory da cui avviare tutte le query di directory.  Ad esempio, dc=abc,dc=com. |
| Tipo di binding - Query |Selezionare il tipo di binding appropriato hello da utilizzare durante l'associazione di directory LDAP di hello toosearch.  Il tipo selezionato viene usato per le importazioni, la sincronizzazione e la risoluzione del nome utente. <br><br>  Anonimo: consente di eseguire un binding anonimo.  Non vengono usati un nome distinto di binding e una password di binding.  Funziona solo se la directory LDAP hello consente il binding anonimo e le autorizzazioni consentono l'esecuzione di query hello degli attributi e i record appropriati hello.  <br><br> Semplice - nome distinto di binding e Password di binding vengono passati come testo normale toobind toohello elenco LDAP.  Equivale a scopo di test, può essere raggiunto tooverify che hello server e tale account di binding hello disponga di accesso appropriato hello. Dopo l'installazione del certificato appropriato hello, è possibile utilizzare SSL.  <br><br> SSL - nome distinto di binding e Password di binding vengono crittografati mediante SSL toobind toohello LDAP directory.  Installare un certificato in locale che hello trust directory LDAP.  <br><br> Windows - nome utente di binding e Password di binding vengono utilizzati toosecurely connettere tooan controller di dominio Active Directory o directory ADAM.  Se il nome utente di binding viene lasciato vuoto, hello effettuato l'accesso dell'account utente è toobind utilizzato. |
| Tipo di binding - Autenticazioni |Selezionare il tipo di binding appropriato hello da utilizzare quando si esegue l'autenticazione di binding LDAP.  Vedere le descrizioni dei tipi di binding hello in tipo di binding - query.  In questo modo, ad esempio, per il binding anonimo toobe usato per le query mentre il binding SSL viene utilizzato toosecure le autenticazioni di binding LDAP. |
| Nome distinto di binding o nome utente di binding |Immettere il nome distinto del record utente hello hello per hello account toouse durante l'associazione di directory LDAP toohello.<br><br>nome distinto di binding Hello viene utilizzato solo quando il tipo di binding è semplice o SSL.  <br><br>Immettere nome utente di hello di toouse account di Windows hello durante l'associazione di directory LDAP toohello quando è di tipo di binding Windows.  Se lasciato vuoto, hello effettuato l'accesso dell'account utente è toobind utilizzato. |
| Password di binding |Immettere la password di binding hello per hello nome distinto di binding o nome utente da una directory LDAP di toohello toobind utilizzato.  password hello tooconfigure per hello servizio AdSync di multi-Factor Authentication Server, abilitare la sincronizzazione e assicurarsi che il servizio hello sia in esecuzione nel computer locale hello.  password Hello viene salvata in hello Windows archiviati i nomi utente e password in hello account hello che servizio AdSync di multi-Factor Authentication Server è in esecuzione come.  password Hello viene salvata anche hello account hello interfaccia utente è in esecuzione come hello account hello servizio Server multi-Factor Authentication in Server di multi-Factor Authentication è in esecuzione come.  <br><br>Poiché la password di hello viene archiviata solo in Windows archiviati i nomi utente e password del server locale hello, ripetere questo passaggio in ogni Server di multi-Factor Authentication che richiede una password di accesso toohello. |
| Limite dimensione query |Specificare il limite di dimensione hello per il numero massimo di hello di utenti che restituisce una ricerca nella directory.  Questo limite deve corrispondere la configurazione hello nella directory LDAP hello.  Per le ricerche estese dove non è supportato il paging, importazione e la sincronizzazione tenta tooretrieve gli utenti in batch.  Se il limite di dimensioni di hello specificato è superiore al limite di hello configurato nella directory LDAP hello, alcuni utenti potrebbero essere perso. |
| Pulsante Test |Fare clic su **Test** server LDAP di tootest associazione toohello.  <br><br>Non è necessario hello tooselect **utilizza LDAP** opzione tootest associazione. In questo modo hello associazione toobe testata prima che si utilizza configurazione LDAP hello. |

## <a name="filters"></a>Filtri
I filtri consentono di record di tooqualify tooset criteri quando si esegue una ricerca nella directory.  Impostazione filtro hello, è possibile definire l'ambito hello oggetti toosynchronize.  

![Filtri](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Azure multi-Factor Authentication è hello le tre opzioni di filtro seguenti:

* **Filtro contenitore** -specificare criteri di filtro hello record contenitore tooqualify quando si esegue una ricerca nella directory.  Per Active Directory e ADAM, in genere si usa (|(objectClass=organizationalUnit)(objectClass=container)).  Per le altre directory LDAP, utilizzare criteri di filtro che qualificano ciascun tipo di oggetto contenitore, in base allo schema di directory hello.  <br>Nota: se viene lasciato vuoto, per impostazione predefinita viene usato ((objectClass=organizationalUnit)(objectClass=container)).
* **Filtro gruppo di sicurezza** -specificare criteri di filtro hello tooqualify record gruppi di sicurezza quando si esegue una ricerca nella directory.  Per Active Directory e ADAM, in genere si usa (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).  Per le altre directory LDAP, utilizzare criteri di filtro che qualificano ciascun tipo di oggetto gruppo di sicurezza, a seconda dello schema di directory hello.  <br>Nota: se viene lasciato vuoto, per impostazione predefinita viene usato (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).
* **Filtro utente** -specificare criteri di filtro hello record utente tooqualify quando si esegue una ricerca nella directory.  Per Active Directory e ADAM, in genere si usa (&(objectClass=user)(objectCategory=person)).  Per le altre directory LDAP, utilizzare (objectClass = inetOrgPerson) o simile, a seconda dello schema di directory hello. <br>Nota: se viene lasciato vuoto, per impostazione predefinita viene usato (&(objectCategory=person)(objectClass=user)).

## <a name="attributes"></a>Attributi
È possibile personalizzare gli attributi per una directory specifica in base alle necessità.  In questo modo si tooadd di attributi personalizzati e ottimizzare hello tooonly hello attributi per la sincronizzazione che è necessario. Utilizzare il nome di hello di hello attricute come definito nello schema di directory hello per valore hello di ogni campo attributo. Hello nella tabella seguente fornisce informazioni aggiuntive su ogni funzionalità.

Gli attributi possono essere immessi manualmente e non sono necessari toomatch un attributo nell'elenco di attributi hello.

![Attributi](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Funzionalità | Descrizione |
| --- | --- |
| Identificatore univoco |Immettere il nome dell'attributo hello dell'attributo hello che funge da identificatore univoco di hello del contenitore, gruppo di sicurezza e i record utente.  In Active Directory si usa in genere objectGUID. In altre implementazioni LDAP è possibile usare entryUUID o un valore simile.  valore predefinito di Hello è objectGUID. |
| Tipo di identificatore univoco |Selezionare il tipo di hello di attributo dell'identificatore univoco hello.  In Active Directory, l'attributo objectGUID hello è di tipo GUID. In altre implementazioni LDAP è possibile usare il tipo Stringa o Matrice di byte ASCII.  valore predefinito di Hello è GUID. <br><br>È importante tooset questo tipo correttamente dopo gli elementi di sincronizzazione viene fatto riferimento con l'identificatore univoco. Tipo di identificatore univoco di Hello è toodirectly utilizzato trova hello oggetto directory di hello.  L'impostazione di questo tipo tooString quando in realtà directory hello archiviato valore hello come matrice di byte di caratteri ASCII impedisce sincronizzazione non funzionerà correttamente. |
| Nome distinto |Immettere il nome dell'attributo hello dell'attributo hello contenente hello nome distinto per ogni record.  In Active Directory si usa in genere distinguishedName. In altre implementazioni LDAP è possibile usare entryDN o un valore simile.  valore predefinito di Hello è distinguishedName. <br><br>Se non esiste un attributo contenente solo nome distinto di hello, attributo adspath hello può essere utilizzato.  Hello "LDAP: / /\<server\>/" parte del percorso hello viene automaticamente rimossa, lasciando solo hello nome distinto dell'oggetto hello. |
| Nome contenitore |Immettere il nome dell'attributo hello dell'attributo hello che contiene il nome di hello in un record contenitore.  il valore di Hello di questo attributo viene visualizzato in hello gerarchia contenitori durante l'importazione da Active Directory o l'aggiunta di elementi di sincronizzazione.  valore predefinito di Hello è nome. <br><br>Se contenitori diversi usano attributi diversi per i relativi nomi, utilizzare un punto e virgola tooseparate più attributi di nome contenitore.  primo attributo Hello nome contenitore trovato in un oggetto contenitore è usato toodisplay il relativo nome. |
| Nome gruppo di sicurezza |Immettere il nome dell'attributo hello dell'attributo hello che contiene il nome di hello in un record del gruppo di sicurezza.  il valore di Hello di questo attributo viene visualizzato nell'elenco gruppo di sicurezza hello durante l'importazione da Active Directory o l'aggiunta di elementi di sincronizzazione.  valore predefinito di Hello è nome. |
| Username |Immettere il nome dell'attributo hello dell'attributo hello che contiene il nome utente hello in un record utente.  il valore di Hello di questo attributo viene utilizzato come nome utente Server multi-Factor Authentication hello.  Può specificare un secondo attributo come un backup toohello prima.  secondo attributo Hello viene utilizzata solo se hello primo attributo non contiene un valore per l'utente hello.  Hello predefiniti sono userPrincipalName e sAMAccountName. |
| Nome |Immettere il nome dell'attributo hello dell'attributo hello che contiene nome hello in un record utente.  valore predefinito di Hello è givenName. |
| Cognome |Immettere il nome dell'attributo hello dell'attributo hello che contiene il cognome di hello in un record utente.  valore predefinito di Hello è sn. |
| Indirizzo di posta elettronica |Immettere il nome dell'attributo hello dell'attributo hello che contiene l'indirizzo di posta elettronica hello in un record utente.  Indirizzo di posta elettronica viene utilizzato toosend iniziale e l'aggiornamento utente toohello messaggi di posta elettronica.  valore predefinito di Hello è posta elettronica. |
| Gruppo utenti |Immettere il nome dell'attributo hello dell'attributo hello che contiene il gruppo di utenti hello in un record utente.  Gruppo di utenti può essere utilizzato toofilter utenti nell'agente hello e nei report nel portale di gestione di multi-Factor Authentication Server hello. |
| Descrizione |Immettere il nome dell'attributo hello dell'attributo hello che contiene la descrizione hello in un record utente.  La descrizione viene usata solo per le ricerche.  valore predefinito di Hello è description. |
| Lingua telefonata |Immettere il nome dell'attributo hello dell'attributo hello che contiene nome breve di hello language toouse hello per le chiamate vocali per utente hello. |
| Lingua SMS |Immettere il nome dell'attributo hello dell'attributo hello che contiene nome breve di hello language toouse hello per i messaggi di testo SMS per l'utente hello. |
| Lingua app mobile |Immettere il nome dell'attributo hello dell'attributo hello che contiene nome breve di hello language toouse hello per i messaggi di testo app telefono per l'utente hello. |
| Lingua token OATH |Immettere il nome dell'attributo hello dell'attributo hello che contiene nome breve di hello language toouse hello per i messaggi di testo del token OATH per l'utente hello. |
| Telefono ufficio |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di telefono hello business in un record utente.  valore predefinito di Hello è telephoneNumber. |
| Telefono abitazione |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di telefono dell'abitazione hello in un record utente.  valore predefinito di Hello è homePhone. |
| Cercapersone |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di cercapersone hello in un record utente.  valore predefinito di Hello è pager. |
| Cellulare |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di telefono cellulare hello in un record utente.  valore predefinito di Hello è mobile. |
| Fax |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di fax hello in un record utente.  valore predefinito di Hello è facsimileTelephoneNumber. |
| Telefono IP |Immettere il nome dell'attributo hello dell'attributo hello che contiene il numero di telefono hello IP in un record utente.  valore predefinito di Hello è ipPhone. |
| Personalizzate |Immettere il nome dell'attributo hello dell'attributo hello che contiene un numero di telefono personalizzato in un record utente.  valore predefinito di Hello è vuoto. |
| Estensione |Immettere il nome dell'attributo hello dell'attributo hello contenente hello numero di telefono interno in un record utente.  il valore di Hello del campo estensione hello viene usato come hello estensione toohello primaria solo numero di telefono.  valore predefinito di Hello è vuoto. <br><br>Se l'attributo di estensione hello non è specificato, le estensioni possono essere incluse come parte dell'attributo phone hello. In questo caso, anteporre estensione hello con una 'x' in modo che si ottiene analizzato correttamente.  Ad esempio, 555-123-4567 x890 comporta 555-123-4567 come numero di telefono hello e 890 come estensione hello. |
| Pulsante Ripristina impostazioni predefinite |Fare clic su **Ripristina impostazioni predefinite** tooreturn tutti gli attributi di eseguire il valore predefinito tootheir.  impostazioni predefinite di Hello dovrebbero funzionare correttamente con hello schema normale di Active Directory o ADAM. |

Fare clic su attributi tooedit, **modifica** nella scheda attributi hello.  Verrà visualizzata una finestra in cui è possibile modificare gli attributi di hello. Seleziona hello **...**  Avanti tooany attributo tooopen una finestra in cui è possibile scegliere quali toodisplay di attributi.

![Modifica attributi](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Sincronizzazione
La sincronizzazione mantiene i database utente di Azure MFA hello sincronizzato con gli utenti di hello in Active Directory o un'altra directory Lightweight Directory Access Protocol (LDAP). il processo di Hello è simile agli utenti di tooimporting manualmente da Active Directory, ma esegue periodicamente il polling per l'utente di Active Directory e gruppo di sicurezza modifica tooprocess.  Permette anche di disattivare o rimuovere gli utenti che sono stati rimossi da un contenitore, da un gruppo di sicurezza o da Active Directory.

Hello servizio ADSync di multi-Factor Authentication è un servizio di Windows che esegue hello periodicamente il polling di Active Directory.  Non si tratta toobe confusa con Azure AD Sync o Azure AD Connect.  Hello ADSync di multi-Factor Authentication, anche se basati su una base di codice simili, è toohello specifico del Server Azure multi-Factor Authentication.  Viene installato nello stato arrestato e avviato dal servizio Server multi-Factor Authentication quando configurato hello toorun.  Se si dispone di una configurazione del Server multi-Factor Authentication multiserver, hello ADSync di multi-Factor Authentication può essere eseguito solo in un unico server.

Hello servizio ADSync di multi-Factor Authentication utilizza hello estensione del server LDAP DirSync fornita da polling tooefficiently Microsoft per le modifiche.  Il chiamante del controllo DirSync deve avere hello "directory get changes" controllo esteso di destra e DS-Replication-Get-Changes diritto di accesso.  Per impostazione predefinita, questi diritti vengono assegnati toohello gli account Administrator e LocalSystem nei controller di dominio.  Hello servizio AdSync di multi-Factor Authentication è configurato toorun come LocalSystem per impostazione predefinita.  È pertanto più semplice servizio di hello toorun in un controller di dominio.  Se si configura hello servizio tooalways eseguire una sincronizzazione completa, può essere eseguito come un account con autorizzazioni minori.  Si tratta di una procedura meno efficiente, ma che richiede meno privilegi per l'account.

Se la directory LDAP hello supporta ed è configurato per DirSync, quindi il polling di modifiche apportate al gruppo di sicurezza e utente funzionerà hello uguale a quanto accade con Active Directory.  Se non supporta la directory LDAP hello hello controllo DirSync, viene eseguita una sincronizzazione completa durante ogni ciclo.

![Sincronizzazione](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Hello nella tabella seguente contiene informazioni aggiuntive su ciascuna delle impostazioni di tabulazione sincronizzazione hello.

| Funzionalità | Descrizione |
| --- | --- |
| Abilita sincronizzazione con Active Directory |Se selezionata, hello servizio Server multi-Factor Authentication esegue periodicamente il polling Active Directory per le modifiche. <br><br>Nota: è necessario aggiungere almeno un elemento di sincronizzazione e un comando Sincronizza ora deve essere eseguito prima di hello multi-Factor Authentication Server servizio verrà avviato l'elaborazione delle modifiche. |
| Sincronizza ogni |Specificare hello intervallo di tempo hello attesa tra il polling e l'elaborazione delle modifiche del servizio Server di multi-Factor Authentication. <br><br> Nota: l'intervallo di hello specificato è il tempo di hello tra inizio hello di ogni ciclo.  Se hello ora elaborazione delle modifiche supera l'intervallo hello, servizio hello rieseguirà subito il polling. |
| Rimuovi utenti non più presenti in Active Directory |Se selezionata, hello servizio Server multi-Factor Authentication elaborerà Tombstone utente eliminato di Active Directory e Rimuovi hello correlati Server multi-Factor Authentication utente. |
| Esegui sempre una sincronizzazione completa |Se selezionata, hello servizio Server multi-Factor Authentication eseguirà sempre una sincronizzazione completa.  Se è deselezionata, hello servizio Server multi-Factor Authentication eseguirà una sincronizzazione incrementale cercando solo gli utenti che sono stati modificati.  valore predefinito di Hello è deselezionata. <br><br>Se è deselezionata, Azure MFA Server esegue la sincronizzazione incrementale solo quando directory hello supporta controllo DirSync hello e hello account associazione toohello directory dispone di query incrementali DirSync tooperform di autorizzazioni.  Se sono coinvolti più domini nella sincronizzazione hello hello account non dispone delle autorizzazioni appropriate di hello o Server di autenticazione a più fattori di Azure esegue una sincronizzazione completa. |
| Richiedi l'approvazione dell'amministratore per la disabilitazione o la rimozione di più di X utenti |Gli elementi di sincronizzazione possono essere configurato toodisable o rimuovere gli utenti che non sono più un membro del gruppo di protezione o del contenitore dell'elemento hello.  Come misura di sicurezza, l'approvazione dell'amministratore è possibile richiedere quando hello numero di utenti toodisable o rimuovere supera una soglia.  Se questa opzione è selezionata, viene richiesta l'approvazione per la soglia specificata.  valore predefinito di Hello è 5 e intervallo di hello è 1 too999. <br><br> L'approvazione viene facilitata inviando prima una tooadministrators di notifica di posta elettronica. notifica tramite posta elettronica Hello fornisce le istruzioni per verificare e approvare la disabilitazione di hello e la rimozione degli utenti.  Quando viene avviata l'interfaccia utente di multi-Factor Authentication Server hello, richiederà per l'approvazione. |

Hello **Sincronizza** pulsante consente una sincronizzazione completa per la sincronizzazione di hello toorun gli elementi specificati.  È necessario eseguire una sincronizzazione completa ogni volta che vengono aggiunti, modificati, rimossi o riordinati elementi di sincronizzazione.  È inoltre hello necessario per il servizio AdSync di multi-Factor Authentication è operativa perché consente di impostare hello punto da cui il servizio hello eseguirà il polling per le modifiche incrementali iniziale.  Se sono state apportate modifiche toosynchronization elementi ma non è ancora stata eseguita una sincronizzazione completa, sarà richiesta tooSynchronize ora.

Hello **rimuovere** pulsante consente hello amministratore toodelete uno o più elementi di sincronizzazione dall'elenco degli elementi sincronizzazione hello Server multi-Factor Authentication.

> [!WARNING]
> Dopo la rimozione, un record di elemento di sincronizzazione non può più essere recuperato. Sarà necessario sincronizzazione hello tooadd record dell'elemento nuovamente se è stato eliminato per errore.

elemento di sincronizzazione Hello o gli elementi di sincronizzazione rimossi dal Server multi-Factor Authentication.  Hello servizio Server multi-Factor Authentication non elaborerà più gli elementi di sincronizzazione hello.

i pulsanti Sposta su e Sposta giù Hello consentono amministratore hello ordine hello toochange degli elementi di sincronizzazione hello.  Hello ordine è importante perché hello stesso utente può essere un membro di più di un elemento di sincronizzazione (ad esempio, un contenitore e un gruppo di sicurezza).  le impostazioni di Hello utente toohello applicati durante la sincronizzazione derivano dal hello primo elemento di sincronizzazione utente di hello elenco toowhich hello è associata.  Pertanto, è consigliabile inserire gli elementi di sincronizzazione di hello in ordine di priorità.

> [!TIP]
> Dopo aver rimosso elementi di sincronizzazione è opportuno eseguire una sincronizzazione completa.  Dopo aver ordinato gli elementi di sincronizzazione è opportuno eseguire una sincronizzazione completa.  Fare clic su **Sincronizza** tooperform una sincronizzazione completa.

## <a name="multi-factor-auth-servers"></a>Server Multi-Factor Authentication
Server multi-Factor Authentication aggiuntivi può essere impostato tooserve come proxy RADIUS di backup, proxy LDAP o per l'autenticazione IIS. configurazione di sincronizzazione Hello è condivisa tra tutti gli agenti di hello. Tuttavia, solo uno di questi agenti potrebbe essere servizio multi-Factor Authentication Server hello in esecuzione. Questa scheda consente di hello tooselect Server multi-Factor Authentication che deve essere abilitata per la sincronizzazione.

![Server Multi-Factor Authentication](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
