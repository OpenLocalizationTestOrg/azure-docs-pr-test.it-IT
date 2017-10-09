---
title: 'Azure AD Connect: Informazioni sul provisioning dichiarativo | Documentazione Microsoft'
description: Illustra hello dichiarativa configurazione modello di provisioning in Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Servizio di sincronizzazione Azure AD Connect: Informazioni sul provisioning dichiarativo
In questo argomento viene illustrato il modello di configurazione hello in Azure AD Connect. modello di Hello è denominato Provisioning dichiarativo e consente una modifica alla configurazione con facilità toomake. Molte operazioni descritte in questo argomento sono avanzate e non necessarie per la maggior parte degli scenari dei clienti.

## <a name="overview"></a>Panoramica
Provisioning dichiarativo è l'elaborazione di oggetti provenienti da una directory di origine connesso e determina come gli attributi e oggetto hello devono essere trasformati da una destinazione tooa di origine. Elaborazione di un oggetto in una pipeline di sincronizzazione e della pipeline hello è stesso hello per le regole in entrata e in uscita. Una regola in ingresso di un metaverse toohello di spazio connettore e una regola in uscita non dallo spazio connettore tooa di hello metaverse.

![Pipeline di sincronizzazione](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

pipeline di Hello include diversi moduli diversi. Ognuno di essi è responsabile di un concetto nella sincronizzazione degli oggetti.

![Pipeline di sincronizzazione](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Origine, l'oggetto di origine hello
* [Ambito](#scope), consente di trovare tutte le regole di sincronizzazione che si trovano nell'ambito
* [Join](#join), determina la relazione tra spazio connettore e metaverse
* [Trasformazione](#transform), calcola la modalità di trasformazione e il flusso degli attributi
* [Precedenza](#precedence), risolve i conflitti tra attributi
* Destinazione, l'oggetto di destinazione hello

## <a name="scope"></a>Scope
modulo ambito Hello è la valutazione di un oggetto e determina le regole di hello nell'ambito e devono essere incluso nell'elaborazione di hello. A seconda di valori di attributi hello sull'oggetto hello, le regole di sincronizzazione diversi sono toobe valutata nell'ambito. Ad esempio, un utente disabilitato senza alcuna cassetta postale di Exchange ha regole diverse rispetto a un utente abilitato che ha una cassetta postale.  
![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

ambito Hello è definito come clausole e gruppi. clausole Hello sono all'interno di un gruppo. Tra tutte le clausole in un gruppo viene usato un operatore logico AND. Ad esempio, (department =IT AND country = Denmark). Viene usato un operatore logico OR tra gruppi.

![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
ambito Hello in questa immagine deve essere letto come (reparto IT e country = = Danimarca) o (country = Svezia). Se il gruppo 1 o 2 viene valutata tootrue, regola hello è nell'ambito.

modulo di ambito Hello supporta hello seguenti operazioni.

| Operazione | Descrizione |
| --- | --- |
| EQUAL, NOTEQUAL |Confronto tra stringhe che restituisce se corrisponde al valore nell'attributo hello toohello uguale. Per gli attributi multivalore, vedere ISIN e ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Un confronto tra stringhe che restituisce se il valore è minore del valore di hello nell'attributo hello. |
| CONTAINS, NOTCONTAINS |Confronto tra stringhe che restituisce se il valore è reperibile in qualche punto all'interno del valore di attributo hello. |
| STARTSWITH, NOTSTARTSWITH |Confronto tra stringhe che restituisce se il valore è l'inizio di hello del valore di hello nell'attributo hello. |
| ENDSWITH, NOTENDSWITH |Confronto tra stringhe che restituisce se il valore è espresso in fine hello del valore di hello nell'attributo hello. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Confronto tra stringhe che restituisce se il valore è maggiore del valore di hello nell'attributo hello. |
| ISNULL, ISNOTNULL |Valuta se hello attributo è assente dall'oggetto hello. Se l'attributo hello non è presente e pertanto è null, la regola hello è nell'ambito. |
| ISIN, ISNOTIN |Valuta se è presente nell'attributo hello definito valore hello. Questa operazione è una variante di più valori hello di uguale e NOTEQUAL. attributo Hello è previsto un attributo multivalore toobe e se il valore di hello è reperibile in uno dei valori di attributo hello, regola hello è nell'ambito. |
| ISBITSET, ISNOTBITSET |Valuta se un determinato bit è impostato. Ad esempio, può essere utilizzato tooevaluate bit hello in userAccountControl toosee se un utente è abilitato o disabilitato. |
| ISMEMBEROF, ISNOTMEMBEROF |il valore di Hello deve contenere un gruppo di tooa DN nello spazio connettore hello. Se l'oggetto hello è un membro del gruppo di hello specificato, la regola hello è nell'ambito. |

## <a name="join"></a>Join
modulo di join Hello nella pipeline di sincronizzazione hello è responsabile dell'individuazione relazione hello tra oggetto hello hello origine e un oggetto nella destinazione hello. In una regola in ingresso, questa relazione sarebbe un oggetto in uno spazio connettore, la ricerca di un oggetto di relazione tooan hello Metaverse.  
![Join tra cs e mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
obiettivo di Hello toosee se è già presente un oggetto nel metaverse hello, creato da un altro connettore, deve essere associato. Ad esempio, in una risorsa di account utente di foreste hello dalla foresta di account hello deve essere unito a utente hello dalla foresta di risorse hello.

I join vengono utilizzati principalmente sui toohello insieme di regole in entrata toojoin connettore spazio oggetti stesso oggetto metaverse.

Hello join vengono definiti come uno o più gruppi. All'interno di un gruppo sono presenti clausole. Tra tutte le clausole in un gruppo viene usato un operatore logico AND. Viene usato un operatore logico OR tra gruppi. gruppi di Hello vengono elaborati in ordine da toobottom superiore. Quando un gruppo ha individuato esattamente una corrispondenza con un oggetto nella destinazione hello, nessun altra regole di unione vengono valutate. Se zero o più di un oggetto viene trovato, l'elaborazione continua toohello successivo gruppo di regole. Per questo motivo, le regole di hello devono essere create in ordine di hello più esplicito di primo e più fuzzy alla fine di hello.  
![Definizione join](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
join Hello in questa immagine vengono elaborati dal toobottom superiore. Pipeline di sincronizzazione hello prima rileva se viene trovata una corrispondenza in employeeID. In caso contrario, seconda regola hello rileva se il nome di account hello può essere utilizzato toojoin hello oggetti insieme. Se non è una corrispondenza sia, regola di terza e ultima hello è una corrispondenza fuzzy più utilizzando hello nome dell'utente.

Se la valutazione di tutte le regole di join e è presente esattamente una corrispondenza, hello **tipo di collegamento** su hello **descrizione** codici da utilizzare. Se questa opzione è impostata troppo**provisioning**, viene creato un nuovo oggetto di destinazione hello.  
![Provisioning o join](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Un oggetto deve avere una sola regola di sincronizzazione con regole di join nell'ambito. Se sono presenti più regole di sincronizzazione in cui è definito il join, si verificherà un errore. Precedenza non è usato tooresolve join conflitti. Un oggetto deve disporre di una regola di join nell'ambito per gli attributi tooflow con hello stessa direzione in ingresso/in uscita. Se è necessario tooflow gli attributi in ingresso e in uscita toohello stesso oggetto, è necessario disporre di un in ingresso e una regola di sincronizzazione in uscita con join.

Join in uscita presenta un comportamento speciale quando viene tentata tooprovision uno spazio connettore di oggetto tooa destinazione. attributo DN Hello è try toofirst utilizzato un join inversa. Se è già presente un oggetto nello spazio connettore di destinazione hello con hello stesso DN, hello oggetti vengono uniti.

modulo di join Hello viene valutato solo una volta quando una nuova regola di sincronizzazione fornito nell'ambito. Quando un oggetto è stato aggiunto, non è separare anche se i criteri di join hello non è più soddisfatta. Se si desidera toodisjoin un oggetto, regola di sincronizzazione hello che fanno parte di oggetti hello necessario uscire dall'ambito.

### <a name="metaverse-delete"></a>Eliminazione di metaverse
Rimane purché è una regola di sincronizzazione nell'ambito con un oggetto metaverse **tipo di collegamento** impostare troppo**provisioning** o **StickyJoin**. Un StickyJoin viene utilizzato quando un connettore non è consentito tooprovision un nuovo oggetto metaverse toohello, ma quando è stato aggiunto, è necessario eliminarlo in origine hello prima dell'eliminazione oggetto metaverse hello.

Quando viene eliminato un oggetto del metaverse, tutti gli oggetti associati a una regola di sincronizzazione in uscita contrassegnata per il **provisioning** vengono contrassegnati per l'eliminazione.

## <a name="transformations"></a>Trasformazioni
le trasformazioni di Hello sono utilizzati toodefine funzionamento del flusso di attributi dalla destinazione di toohello origine hello. Hello flussi possono avere uno dei seguenti hello **flusso tipi**: diretto, una costante o espressione. In un flusso diretto, il valore dell'attributo viene passato così com'è, senza altre trasformazioni. Valore specificato di hello di imposta un valore costante. Un'espressione Usa hello dichiarativa provisioning espressione language tooexpress come cui deve essere trasformazione hello. Hello dettagli per il linguaggio delle espressioni hello è reperibile in hello [la comprensione di linguaggio delle espressioni di provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) argomento.

![Provisioning o join](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Hello **applicare una sola volta** casella di controllo definisce che hello attributo deve essere impostato solo quando l'oggetto hello viene inizialmente creato. Ad esempio, questa configurazione può essere utilizzato tooset una password iniziale per un nuovo oggetto utente.

### <a name="merging-attribute-values"></a>Unione di valori degli attributi
Nei flussi di attributi hello è un'impostazione toodetermine se gli attributi multivalore devono essere uniti da più diversi connettori. valore predefinito di Hello è **aggiornamento**, che indica la regola di sincronizzazione hello con precedenza più alta hanno la precedenza.

![Tipi di unione](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Sono disponibili anche **Merge** (Unisci) e **MergeCaseInsensitive** (Unisci senza distinzione maiuscole/minuscole). Queste opzioni consentono di toomerge valori provenienti da origini diverse. Ad esempio, può essere attributo usato toomerge hello membro o proxyAddresses da foreste diverse. Quando si utilizza questa opzione, tutti sincronizzare le regole di ambito per un oggetto deve utilizzare hello stesso di tipo merge. Non è possibile definire **Update** (Aggiorna) da un connettore e **Merge** (Unisci) da un altro. In questo caso, viene visualizzato un errore.

differenza tra Hello **Merge** e **MergeCaseInsensitive** è come tooprocess duplicare i valori di attributo. il motore di sincronizzazione Hello garantisce valori duplicati non vengono inseriti nell'attributo di destinazione hello. Con **MergeCaseInsensitive**, valori con solo una differenza duplicati nel caso in cui non verranno toobe presente. Ad esempio, non verrà visualizzato sia "SMTP:bob@contoso.com"e"smtp:bob@contoso.com" nell'attributo di destinazione hello. **Merge** cercate solo valori esatti hello e più valori in cui è presente solo una differenza nel caso potrebbe essere presente.

opzione Hello **sostituire** è hello identico **aggiornamento**, ma non viene utilizzato.

### <a name="control-hello-attribute-flow-process"></a>Processo del flusso di controllo hello attributo
Quando più regole di sincronizzazione in entrata vengono configurate toocontribute toohello stesso attributo metaverse, la priorità è riga confermata hello toodetermine utilizzato. regola di sincronizzazione Hello con precedenza più alta (valore numerico inferiore) verrà valore hello toocontribute. Hello che stesso accade per le regole in uscita. regola di sincronizzazione Hello con precedenza più alta wins e contribuiscono hello valore toohello connesso directory.

In alcuni casi, invece di fornire un valore, la regola di sincronizzazione hello deve determinare il comportamento altre regole. In questo caso vengono usati alcuni valori letterali speciali.

Per le regole di sincronizzazione in entrata, hello letterale **NULL** può essere utilizzato tooindicate che flusso hello non è toocontribute alcun valore. Un'altra regola con una precedenza inferiore può fornire un valore. Se nessuna regola ha fornito un valore, l'attributo metaverse hello viene rimossa. Per una regola in uscita, se **NULL** è hello finale dopo che sono state elaborate tutte le regole di sincronizzazione, il valore di hello viene rimosso in una directory connessa hello.

valore letterale Hello **AuthoritativeNull** è troppo simile**NULL** ma con una differenza hello che non le regole di precedenza inferiore possono fornire un valore.

Un flusso dell'attributo può anche usare **IgnoreThisFlow**. È simile tooNULL nel senso hello indica non c'è niente toocontribute. differenza Hello è che non rimuove un valore già esistente nella destinazione hello. È ad esempio il flusso di attributi di hello è ancora presente.

Di seguito è fornito un esempio:

In *Out tooAD - ibrida di Exchange utente* è reperibile hello seguendo flusso:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Questa espressione deve essere letto come: se la cassetta postale dell'utente hello si trova in Azure AD, quindi il flusso attributo hello tooAD di Azure AD. In caso contrario, non passano indietro nulla tooActive Directory. In questo caso, consigliabile mantenere valore esistente hello in Active Directory.

### <a name="importedvalue"></a>ImportedValue
funzione Hello ImportedValue è diversa rispetto a tutte le altre funzioni, poiché il nome dell'attributo hello deve essere racchiusi tra virgolette doppie anziché le parentesi quadre:  
`ImportedValue("proxyAddresses")`.

In genere durante la sincronizzazione un attributo utilizza il valore previsto hello, anche se non è stato esportato ancora o è stato ricevuto un errore durante l'esportazione ("alto tower hello"). Una sincronizzazione in ingresso presuppone che un attributo che non ha ancora raggiunto una directory connessa la raggiungerà prima o poi. In alcuni casi, è importante tooonly sincronizzare un valore che è stato confermato dalla directory connessa di hello ("ologrammi e delta di importazione").

Un esempio di questa funzione è reperibile in hello out-of-box regola di sincronizzazione *In from AD – User Common da Exchange*. In Configurazione ibrida di Exchange, il valore di hello aggiunto da Exchange online deve essere sincronizzato solo quando è stato confermato che il valore di hello è stato esportato correttamente:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Precedenza
Quando tenta di diverse regole di sincronizzazione toocontribute hello stessa destinazione toohello valore di attributo, il valore di precedenza hello è riga confermata hello toodetermine utilizzato. regola di Hello con precedenza più alta, più basso valore numerico, verrà attributo hello toocontribute un conflitto.

![Tipi di unione](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Questo tipo di ordinamento può essere utilizzato toodefine più preciso per un piccolo subset di oggetti i flussi dell'attributo. Ad esempio, hello out-di--regole predefinite assicurarsi che gli attributi da un account abilitato (**User AccountEnabled**) hanno la precedenza da altri account.

È possibile definire la precedenza tra i connettori. Che consente innanzitutto connettori migliori toocontribute i valori dei dati.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Più oggetti da hello stesso spazio connettore
Se si dispone di diversi oggetti in hello connettore stesso spazio toohello aggiunti a un oggetto metaverse stesso, deve essere regolata la precedenza. Se diversi oggetti presenti nell'ambito di hello stessa regola di sincronizzazione, il motore di sincronizzazione hello non toodetermine in grado di precedenza. È ambiguo l'oggetto di origine sono incoraggiati a contribuire hello valore toohello metaverse. Questa configurazione viene segnalata come ambigua anche se gli attributi di hello in origine hello presentano hello stesso valore.  
![Più oggetti uniti toohello stesso oggetto mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

Per questo scenario, è necessario ambito hello toochange delle regole di sincronizzazione hello in modo che gli oggetti origine hello regole di sincronizzazione diverso nell'ambito. Che consente la priorità di diversi toodefine.  
![Più oggetti uniti toohello stesso oggetto mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su linguaggio delle espressioni hello [informazioni sulle espressioni di Provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Vedere come dichiarativa provisioning è usato out-of-box in [informazioni su configurazione predefinita di hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Vedere come una pratica toomake cambiano con provisioning dichiarativo [toomake toohello una modifica la modalità di configurazione predefinite](active-directory-aadconnectsync-change-the-configuration.md).
* Continuare a utenti e contatti interagiscono in tooread [informazioni su utenti e contatti](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

**Argomenti di riferimento**

* [Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni](active-directory-aadconnectsync-functions-reference.md)
