---
title: 'Sincronizzazione di Azure AD Connect: informazioni su configurazione predefinita di hello | Documenti Microsoft'
description: Questo articolo descrive una configurazione predefinita di hello nella sincronizzazione di Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Sincronizzazione di Azure AD Connect: informazioni su configurazione predefinita di hello
Questo articolo spiega le regole di configurazione out-of-box hello. Documenta le regole di hello e l'impatto di queste regole di configurazione di hello. Inoltre illustrata hello predefinito configurazione della sincronizzazione di Azure AD Connect. obiettivo di Hello è che il lettore hello riconosce come modello di configurazione hello, denominato provisioning dichiarativo, è in esecuzione in un esempio reale. In questo articolo presuppone che sia già stato installato e configura la sincronizzazione di Azure AD Connect hello installazione guidata.

dettagli di hello toounderstand del modello di configurazione hello, leggere [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Regole di out-of-box da on-premise tooAzure AD
Hello espressioni seguenti sono disponibili nella configurazione di hello out-of-box.

### <a name="user-out-of-box-rules"></a>Regole utente predefinite
Queste regole si applicano anche il tipo di oggetto iNetOrgPerson toohello.

Un oggetto utente deve soddisfare hello toobe sincronizzato seguenti:

* Deve disporre di un sourceAnchor.
* Dopo aver hello oggetto è stato creato in Azure AD, quindi non è possibile modificare sourceAnchor. Se il valore di hello è modificato in locale, oggetto hello interrompe la sincronizzazione finché non sourceAnchor hello viene modificato valore precedente tooits indietro.
* Deve avere hello accountEnabled (userAccountControl) attributo popolato. Con una versione di Active Directory locale, questo attributo sarà sempre presente e popolato.

Hello oggetti utente di seguenti è **non** sincronizzato tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Assicurarsi di molti oggetti out-of-box in Active Directory, ad esempio account predefinito administrator hello, non sono sincronizzate.
* `IsPresent([sAMAccountName]) = False`. Verificare che gli oggetti utente senza l'attributo sAMAccountName non vengano sincronizzati. Nella pratica, questo caso si verifica solo in un dominio aggiornato da NT4.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Non sincronizzano l'account del servizio hello utilizzato da sincronizzazione di Azure AD Connect e le versioni precedenti.
* Non sincronizzare gli account di Exchange che non funzionerebbero in Exchange Online.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Non sincronizzare gli oggetti che non funzionerebbero in Exchange Online.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Questa maschera di bit (& H21C07000) sarebbe filtrare hello seguenti oggetti:
  * Cartelle pubbliche abilitate alla posta elettronica
  * Cassetta postale Supervisore sistema
  * Cassetta postale Database cassette postali (cassetta postale di sistema)
  * Gruppo di protezione universale (non si applica a un utente, ma è presente per motivi di compatibilità)
  * Gruppo non universale (non si applica a un utente, ma è presente per motivi di compatibilità)
  * Piano della cassetta postale
  * Cassetta postale di individuazione
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Non sincronizzare oggetti generati dalla replica.

si applica alle regole di attributo Hello:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. attributo sourceAnchor Hello non provengono da una cassetta postale collegata. Si presuppone che se è stata trovata una cassetta postale collegata, account effettivo hello è unita in un secondo momento.
* Gli attributi vengono sincronizzati solo se hello relativi a Exchange attributo **mailNickName** ha un valore.
* Quando sono presenti più foreste, gli attributi vengono utilizzati in hello seguente ordine:
  1. Gli attributi correlati toosign in ingresso (ad esempio userPrincipalName) vengono forniti dalla foresta hello con un account abilitato.
  2. Attributi che possono essere trovati in un elenco indirizzi globale di Exchange (elenco indirizzi globale) vengono forniti dalla foresta hello con una cassetta postale di Exchange.
  3. Se non è possibile trovare una cassetta postale, questi attributi possono provenire da qualsiasi foresta.
  4. Attributi (tecnica non è visibile nell'elenco indirizzi globale hello) vengono forniti dalla foresta hello relativi a Exchange in cui `mailNickname ISNOTNULL`.
  5. Se sono presenti più foreste che soddisfano una di queste regole e hello ordine (Data/ora) di creazione di connettori hello (foreste) viene utilizzato toodetermine quale foresta contribuisce attributi hello.

### <a name="contact-out-of-box-rules"></a>Regole predefinite del contatto
Un oggetto contatto deve soddisfare hello toobe sincronizzato seguenti:

* contatto Hello deve essere abilitati. Viene verificato con hello seguenti regole:
  * `IsPresent([proxyAddresses]) = True)`. attributo proxyAddresses Hello deve essere compilato.
  * Un indirizzo di posta elettronica primario è reperibile nell'attributo proxyAddresses hello o attributo mail hello. Hello presenza di un @ è utilizzato tooverify che il contenuto di hello è un indirizzo di posta elettronica. Una di queste due regole deve essere valutata tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. È presente una voce con "SMTP:" e se è presente, è possibile un @ è stata trovata nella stringa hello?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. È hello attributo mail popolata e se è possibile un @ è stata trovata nella stringa hello?

Hello seguendo gli oggetti contatti è **non** sincronizzato tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Verificare che nessun oggetto contatto contrassegnato come critico venga sincronizzato. Non devono essere presenti oggetti contatto con una configurazione predefinita.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Questi oggetti non funzionerebbero in Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Non sincronizzare oggetti generati dalla replica.

### <a name="group-out-of-box-rules"></a>Regole di gruppo predefinite
Un oggetto gruppo deve soddisfare hello toobe sincronizzato seguenti:

* Deve contenere meno di 50.000 membri. Questo conteggio indica il numero di hello di membri nel gruppo locale hello.
  * Se dispone di più membri prima che la sincronizzazione ha inizio hello prima volta, il gruppo di hello non è sincronizzato.
  * Se l'aumento il numero di hello di membri da quando è stata inizialmente creata, quindi quando raggiunge 50.000 membri che si interrompe la sincronizzazione finché il conteggio di appartenenza hello è inferiore a 50.000 nuovamente.
  * Nota: il conteggio di appartenenza 50.000 hello viene anche applicato da Azure AD. Non è in grado di toosynchronize gruppi con più membri anche se si modifica o rimuovere la regola.
* Se il gruppo di hello è un **gruppo di distribuzione**, quindi deve essere inoltre abilitato posta elettronica. Per informazioni sull’applicazione di questa regola vedere [Regole predefinite del contatto](#contact-out-of-box-rules) .

Hello seguendo gli oggetti di gruppo è **non** sincronizzato tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Assicurarsi di molti oggetti out-of-box in Active Directory, ad esempio il gruppo di amministratori predefinito hello, non sono sincronizzate.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Gruppo legacy usato da DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Gruppo di ruoli.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Non sincronizzare oggetti generati dalla replica.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>Regole predefinite di ForeignSecurityPrincipal
FSP appartengano troppo "any" (\*) oggetto Metaverse hello. Questa unione si verifica in realtà solo per gli utenti e i gruppi di sicurezza. Questa configurazione assicura che l'appartenenza a più foreste venga risolta e rappresentata correttamente in Azure AD.

### <a name="computer-out-of-box-rules"></a>Regole predefinite del computer
Un oggetto computer deve soddisfare hello toobe sincronizzato seguenti:

* `userCertificate ISNOTNULL`. Solo i computer Windows 10 popolano questo attributo. Tutti gli oggetti computer con un valore in questo attributo vengono sincronizzati.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Scenario di conoscenza hello regole out-of-box
Questo esempio usa una distribuzione con una foresta di account (A), una foresta di risorse (R) e una directory di Azure AD.

![Immagine con descrizione dello scenario](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

In questa configurazione, si presuppone che sia un account abilitato nella foresta di account hello e un account disabilitato nella foresta di risorse hello con una cassetta postale collegata.

L'obiettivo con la configurazione predefinita di hello è:

* Gli attributi correlati toosign-in vengono sincronizzati dall'insieme di strutture di hello con account hello abilitato.
* Attributi che possono essere trovati in hello GAL (elenco indirizzi globale) vengono sincronizzati dall'insieme di strutture di hello con cassetta postale hello. Se non si trova una cassetta postale, verrà usata un'altra foresta qualsiasi.
* Se viene trovata una cassetta postale collegata, hello account abilitato collegato deve essere trovata per hello oggetto esportato toobe tooAzure Active Directory.

### <a name="synchronization-rule-editor"></a>Editor delle regole di sincronizzazione
configurazione di Hello può essere visualizzate e modificate con lo strumento hello Editor regole di sincronizzazione (SRE) e un tooit di scelta rapida sono disponibili nel menu start hello.

![Icona dell'editor delle regole di sincronizzazione](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Hello SRE è un strumento del resource kit e viene installato con sincronizzazione di Azure AD Connect. toostart in grado di toobe, è necessario essere un membro del gruppo ADSyncAdmins hello. All'avvio viene visualizzato un pannello simile al seguente:

![Regole di sincronizzazione in ingresso](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

In questo pannello sono riportate tutte le regole di sincronizzazione create per la configurazione. Ogni riga nella tabella hello è una regola di sincronizzazione. toohello a sinistra in tipi di regole, sono elencati due tipi diversi di hello: in ingresso e in uscita. Connessioni in entrata e in uscita è dalla visualizzazione hello del metaverse hello. Si è principalmente corso toofocus su hello in questa panoramica regole connessioni in entrata. elenco delle regole di sincronizzazione Hello dipende dallo schema hello rilevato in Active Directory. In figura hello precedente, stati creati account di hello foresta (fabrikamonline.com) non dispone di tutti i servizi, ad esempio Exchange e Lync e nessuna regola di sincronizzazione per questi servizi. Tuttavia, nella foresta di risorse hello (res.fabrikamonline.com) si trova le regole di sincronizzazione per questi servizi. il contenuto di Hello delle regole di hello è diverso a seconda della versione di hello rilevata. In una distribuzione con Exchange 2013 saranno ad esempio configurati più flussi di attributi rispetto a Exchange 2010/2007.

### <a name="synchronization-rule"></a>Regola di sincronizzazione
Una regola di sincronizzazione è un oggetto di configurazione con un set di attributi trasmessi in flusso quando una condizione risulta soddisfatta. È inoltre toodescribe utilizzato come un oggetto in uno spazio connettore è correlato tooan oggetto Metaverse hello, noto come **join** o **corrispondono**. le regole di sincronizzazione Hello hanno un valore di precedenza che indica come interagiscono tooeach altri. Una regola di sincronizzazione con un valore numerico inferiore ha una precedenza più alta e in un conflitto di flusso di attributo, prevale la priorità superiore hello la risoluzione dei conflitti.

Ad esempio, esaminare hello regola di sincronizzazione **In from AD – User AccountEnabled**. Contrassegnare questa riga hello SRE e selezionare **modifica**.

Poiché questa regola è una regola di out-of-box, viene visualizzato un avviso quando si apre regola hello. È consigliabile non apportare qualsiasi [Modifica regole tooout-of-box](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), quindi viene richiesto che cosa sono le intenzioni. In questo caso, si desidera solo regola hello tooview. Selezionare **No**.

![Avviso delle regole di sincronizzazione](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Una regola di sincronizzazione include quattro sezioni di configurazione: descrizione, filtro per la definizione dell'ambito, regole di unione e trasformazioni.

#### <a name="description"></a>Descrizione
Hello prima sezione fornisce informazioni di base, ad esempio un nome e una descrizione.

![Scheda Description (Descrizione) nell'editor delle regole di sincronizzazione ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

È inoltre possibile trovare informazioni su quale sistema collegato, questa regola è correlata, che tipo di oggetto nella hello connesso sistema a che si applica e hello tipo di oggetto metaverse. tipo di oggetto metaverse Hello è sempre persona indipendentemente dal fatto che quando il tipo di oggetto origine hello è un utente, iNetOrgPerson o contatto. tipo di oggetto metaverse Hello non deve mai cambiare in modo viene creata come un tipo generico. tooJoin, StickyJoin o Provision, è possibile impostare il tipo di collegamento Hello. Questa impostazione funziona insieme sezione regole di unione hello e viene descritta più avanti.

Si può anche vedere che questa regola di sincronizzazione viene usata per la sincronizzazione della password. Se un utente è nell'ambito per questa regola di sincronizzazione, hello viene sincronizzata da toocloud locale (presupponendo che è stata abilitata la funzionalità di sincronizzazione password hello).

#### <a name="scoping-filter"></a>Filtro per la definizione dell'ambito
Hello sezione filtro di ambito è tooconfigure usato quando deve essere applicata una regola di sincronizzazione. Poiché il nome di hello della regola di sincronizzazione si sta esaminando hello indica deve essere applicato solo per gli utenti abilitati, l'ambito di hello viene configurato in questo attributo hello AD **userAccountControl** necessario non hanno hello bit 2 impostato. Quando il motore di sincronizzazione hello trova un utente in Active Directory, si applica questa sincronizzazione regola quando **userAccountControl** è impostato un valore decimale toohello 512 (utente normale abilitato). Non si applica la regola hello quando l'utente hello è **userAccountControl** impostare too514 (utente normale disabilitato).

![Scheda Scoping filter (Filtro di ambito) nell'editor delle regole di sincronizzazione ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

filtro di ambito Hello contiene gruppi e clausole che possono essere annidate. Tutte le clausole all'interno di un gruppo devono essere soddisfatti per tooapply una regola di sincronizzazione. Quando sono definiti più gruppi, almeno un gruppo deve essere soddisfatti per hello regola tooapply. In altri termini, un OR logico viene valutato tra gruppi, mentre un AND logico viene valutato all'interno di un gruppo. Un esempio di questa configurazione è reperibile in hello regola di sincronizzazione in uscita **Out tooAAD – Group Join**. Sono presenti diversi gruppi di filtri di sincronizzazione, ad esempio uno per i gruppi di sicurezza (`securityEnabled EQUAL True`) e uno per i gruppi di distribuzione (`securityEnabled EQUAL False`).

![Scheda Scoping filter (Filtro di ambito) nell'editor delle regole di sincronizzazione ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Questa regola viene utilizzato toodefine cui gruppi devono essere sottoposto a provisioning tooAzure Active Directory. Gruppi di distribuzione devono essere abilitato per la posta toobe sincronizzati con Azure AD, ma per gruppi di sicurezza non è necessario un messaggio di posta elettronica.

#### <a name="join-rules"></a>Regole di unione
terza sezione Hello è usato tooconfigure correlazione tra gli oggetti nello spazio connettore hello tooobjects hello Metaverse. Hello regola esaminata in precedenza non dispone di alcuna configurazione per regole di unione, ma si è toolook continua a **In from AD – User Join**.

![Scheda Join rules (Regole di unione) nell'editor delle regole di sincronizzazione ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

contenuto di Hello della regola di join hello dipende dal hello corrispondente opzione selezionata nell'installazione guidata di hello. Per una regola in ingresso, valutazione hello inizia con un oggetto di nello spazio connettore di origine hello e ogni gruppo di regole di unione hello viene valutato in sequenza. Se un oggetto di origine è toomatch valutata esattamente una oggetto nel metaverse usando una delle regole di unione hello hello, vengono aggiunti oggetti hello. Se la valutazione di tutte le regole ed è presente alcuna corrispondenza, viene utilizzato hello tipo di collegamento nella pagina Descrizione hello. Se questa configurazione è stata impostata troppo**provisioning**, quindi viene creato un nuovo oggetto nella destinazione hello, hello metaverse. un nuovo oggetto toohello metaverse si intende noto anche come troppo tooprovision**progetto** metaverse di toohello un oggetto.

regole di unione Hello vengono valutate solo una volta. Quando vengono aggiunti un oggetto spazio connettore e un oggetto del metaverse, rimangono unite in join come ambito hello di hello regola di sincronizzazione risulta soddisfatta.

Durante la valutazione delle regole di sincronizzazione, nell'ambito deve essere presente una sola regola di sincronizzazione con regole di unione definite. Se per un oggetto vengono trovate più regole di sincronizzazione con regole di unione, viene generato un errore. Per questo motivo, hello consiglia toohave solo una regola di sincronizzazione con join definita se più regole di sincronizzazione sono nell'ambito per un oggetto. Nella configurazione di out-of-box hello per sincronizzazione di Azure AD Connect, queste regole possono trovare esaminando nome hello e individuare quelle con la parola hello **Join** alla fine di hello del nome hello. Una regola di sincronizzazione senza alcuna regola di join definiti applica i flussi di attributi hello quando un'altra regola di sincronizzazione unite oggetti hello o il provisioning di un nuovo oggetto di destinazione hello.

Se si osserva immagine hello precedente, è possibile visualizzare tale regola hello sta tentando di toojoin **objectSID** con **msExchMasterAccountSid** (Exchange) e **msRTCSIP-OriginatorSid** ( Lync), che è quello previsto in una topologia di foresta account-risorse. Trovare hello stessa regola in tutte le foreste. il presupposto di Hello è che ogni insieme di strutture, potrebbe essere un account o una risorsa foresta. Questa configurazione funziona anche se si dispone di account live in una singola foresta e che non sono toobe unita in join.

#### <a name="transformations"></a>Trasformazioni
sezione di trasformazione Hello definisce tutti i flussi di attributi che si applicano toohello oggetto di destinazione quando vengono aggiunti oggetti hello e hello ambito filtro è soddisfatto. Se si torna indietro toohello **In from AD – User AccountEnabled** regola di sincronizzazione, si trova hello seguenti trasformazioni:

![Scheda Transformations (Trasformazioni) nell'editor delle regole di sincronizzazione ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput nel contesto, in una distribuzione di foresta Account-risorse, questa configurazione è previsto toofind un account abilitato nella foresta di account hello e un account disabilitato nella risorsa hello foresta con le impostazioni di Exchange e Lync. Regola di sincronizzazione si sta esaminando Hello contiene attributi di hello necessari per l'accesso e questi attributi del flusso dalla foresta hello in cui è presente un account abilitato. Tutti questi flussi di attributi vengono riuniti in una regola di sincronizzazione.

Una trasformazione può avere diversi tipi: Costante, Diretto ed Espressione.

* Un flusso costante passa sempre un valore hardcoded. In caso di hello precedente, imposta sempre il valore di hello **True** nell'attributo metaverse hello denominato **accountEnabled**.
* Un flusso diretto di flussi sempre il valore di hello dell'attributo di hello nell'attributo di destinazione toohello origine hello come-è.
* il terzo tipo di flusso Hello è l'espressione e che consente di configurazioni più avanzate.

linguaggio delle espressioni Hello è VBA (Visual Basic for Applications), pertanto gli utenti con esperienza di Microsoft Office o VBScript riconosceranno il formato di hello. Gli attributi vengono scritti tra parentesi quadre [attributeName]. I nomi degli attributi e i nomi di funzione tra maiuscole e minuscole, ma valuta le espressioni di hello hello Editor regole di sincronizzazione e fornire un avviso se l'espressione hello non è valida. Tutte le espressioni sono scritte in una singola riga, con funzioni annidate. power hello tooshow del linguaggio di configurazione hello, ecco hello flusso relativo a pwdLastSet, ma con commenti aggiuntivi inseriti:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Vedere [informazioni sulle espressioni di Provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) per ulteriori informazioni sul linguaggio di espressioni hello dei flussi di attributi.

### <a name="precedence"></a>Precedenza
Ora siano presenti alcune singole regole di sincronizzazione, ma hello regole interagiscono nella configurazione di hello. In alcuni casi, un valore di attributo provengono da più toohello di regole di sincronizzazione stesso attributo di destinazione. In questo caso, la precedenza degli attributi è utilizzato toodetermine attributo wins. Ad esempio, esaminare hello attributo sourceAnchor. Questo attributo è toosign in grado di toobe un attributo importante in tooAzure Active Directory. È possibile trovare un flusso di attributi per questo attributo in due diverse regole di sincronizzazione, **In from AD – User AccountEnabled** e **In from AD – User Common**. A causa di precedenza delle regole tooSynchronization, attributo sourceAnchor hello provengono da foresta hello con un account abilitato prima quando sono presenti diversi oggetti toohello unita in join metaverse object. Se non sono presenti account abilitati, quindi Usa motore di sincronizzazione hello hello regola di sincronizzazione di catch-all **In from AD – User Common**. Questa configurazione assicura che anche per gli account disabilitati sia ancora presente un attributo sourceAnchor.

![Regole di sincronizzazione in ingresso](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

precedenza Hello per le regole di sincronizzazione è impostata in gruppi dall'installazione guidata di hello. Tutte le regole in un gruppo hanno hello stesso nome, ma sono directory connessa toodifferent connesso. installazione guidata di Hello offre regola hello **In from AD – User Join** precedenza più alta e si esegue l'iterazione su tutte le directory AD connesse. Ma continua quindi con gruppi di Avanti hello di regole in un ordine predefinito. All'interno di un gruppo, vengono aggiunte regole di hello in hello ordine hello che i connettori sono stati aggiunti nella procedura guidata hello. Se un altro connettore viene aggiunto tramite la procedura guidata hello, regole di sincronizzazione hello vengono riordinate e hello nuovo connettore vengono inseriti ultima in ciascun gruppo.

### <a name="putting-it-all-together"></a>Riassumendo
È ora informazioni sufficienti sulle regole di sincronizzazione toobe toounderstand in grado di funzionamento configurazione hello con hello diverse regole di sincronizzazione. Se si pensa a un utente e hello attributi che hanno contribuito toohello metaverse, hello regole vengono applicate nel seguente ordine hello:

| Nome | Commento |
|:--- |:--- |
| In from AD – User Join |Regola per l'unione degli oggetti dello spazio connettore con il metaverse. |
| In from AD – UserAccount Enabled |Attributi obbligatori per l'accesso tooAzure AD e Office 365. Si vuole che questi attributi dall'account hello abilitato. |
| In from AD – User Common from Exchange |Attributi trovati nel hello elenco indirizzi globale. Si presuppone che la qualità dei dati hello sia migliore nella foresta hello in cui sono stati rilevati hello cassetta postale. |
| In from AD – User Common |Attributi trovati nel hello elenco indirizzi globale. Nel caso in cui sono stati trovati una cassetta postale, qualsiasi altro oggetto unito può contribuire a valore dell'attributo hello. |
| In from AD – User Exchange |Presente solo se è stato rilevato Exchange. Trasmette tutti gli attributi dell'infrastruttura di Exchange. |
| In from AD – User Lync |Presente solo se è stato rilevato Lync. Trasmette tutti gli attributi dell'infrastruttura di Lync. |

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su modello di configurazione hello in [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Altre informazioni su linguaggio delle espressioni hello [informazioni sulle espressioni di Provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Continuare a leggere il funzionamento di configurazione di hello out-of-box in [informazioni su utenti e contatti](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Vedere come una pratica toomake cambiano con provisioning dichiarativo [toomake toohello una modifica la modalità di configurazione predefinite](active-directory-aadconnectsync-change-the-configuration.md).

**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

