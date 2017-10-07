---
title: 'Servizio di sincronizzazione Azure AD Connect: informazioni su utenti e contatti | Documentazione Microsoft'
description: Informazioni su utenti e contatti nel Servizio di sincronizzazione Azure AD Connect.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Servizio di sincronizzazione Azure AD Connect: Informazioni su utenti e contatti
I motivi per cui possono essere presenti più foreste Active Directory e sono disponibili più topologie di distribuzione sono diversi. I modelli comuni prevedono una distribuzione account-risorse e foreste sincronizzate tramite Elenco indirizzi globale dopo operazioni di fusione e acquisizione. Anche se esistono modelli puri, sono molto diffusi anche i modelli ibridi. configurazione predefinita di Hello nella sincronizzazione di Azure AD Connect non presume alcun modello specifico, ma a seconda della modalità di corrispondenza utenti selezionata nella Guida all'installazione di hello, è possono osservare comportamenti diversi.

In questo argomento, verranno esaminate come configurazione predefinita di hello si comporta in determinate topologie. Verranno esaminate configurazione hello e hello Editor regole di sincronizzazione può essere utilizzati toolook configurazione hello.

Sono disponibili alcune regole generali configurazione hello presuppone:

* Indipendentemente dall'ordine con cui si importa da origine hello Active Directory, risultato finale hello deve sempre essere hello stesso.
* Un account attivo fornirà sempre le informazioni di accesso, inclusi gli attributi **userPrincipalName** e **sourceAnchor**.
* Un account disabilitato fornirà gli attributi userPrincipalName e sourceAnchor, a meno che non è una cassetta postale collegata, se è presente alcun toobe account attivo trovato.
* Un account con una cassetta postale collegata non verrà usato per gli attributi userPrincipalName e sourceAnchor. Si presuppone che un account attivo venga trovato in seguito.
* Un oggetto contatto potrebbe essere sottoposto a provisioning tooAzure AD come contatto o come un utente. Questa informazione non è nota finché tutte le foreste Active Directory di origine non sono state elaborate.

## <a name="contacts"></a>Contatti
I contatti che rappresentano un utente in una foresta diversa costituiscono una situazione comune dopo un'operazione di acquisizione o fusione in cui la soluzione GALSync collega due o più foreste di Exchange. oggetto contatto Hello viene sempre aggiunto dallo hello connettore spazio toohello metaverse usando l'attributo mail hello. Se è già presente un oggetto contatto o un oggetto utente con hello stesso indirizzo di posta, hello oggetti vengono uniti. Questa è configurata nella regola hello **In from AD – aggiunta contatto**. È inoltre disponibile una regola denominata **In da Active Directory-contatto comune** con un attributo metaverse di attributo flusso toohello **sourceObjectType** con costante hello **contatto**. Questa regola ha una precedenza molto bassa pertanto se un oggetto utente è unita in join toohello stesso oggetto metaverse, quindi regola hello **In from AD – User Common** contribuirà attributo toothis di hello valore utente. Con questa regola, questo attributo avrà il valore di hello contattare se nessun utente è stato aggiunto e hello valore User se è stato trovato almeno un utente.

Per il provisioning di un tooAzure oggetto Active Directory, hello regola in uscita **Out tooAAD-aggiunta contatto** creerà un oggetto contatto se hello attributo metaverse **sourceObjectType** è troppo**contattare** . Se questo attributo viene impostato troppo**utente**, quindi regola di hello **Out tooAAD – User Join** creerà invece un oggetto utente.
È possibile che un oggetto viene promossa da contattare tooUser quando più origine Active Directory vengono importate e sincronizzate.

Ad esempio, in una topologia GALSync si troverà gli oggetti del contatto per tutti gli utenti nella seconda foresta hello quando si importa primo insieme di strutture hello. Verranno quindi installati nuovi oggetti contatto nel connettore AAD hello. Quando successivamente viene importata e sincronizzata hello seconda foresta, verrà trovare hello utenti reali e unirli oggetti metaverse esistenti toohello. È quindi verrà eliminare hello oggetto contatto in AAD e creare un nuovo oggetto utente.

Se si dispone di una topologia in cui gli utenti sono rappresentati come contatti, assicurarsi di selezionare gli utenti toomatch attributo mail hello nella Guida all'installazione di hello. Se si seleziona un'altra opzione, si otterrà una configurazione dipendente dall'ordine. Gli oggetti del contatto verranno sempre join su attributo mail hello, ma gli oggetti utente verranno aggiunto solo in attributo mail hello se questa opzione è stata selezionata nella Guida all'installazione di hello. Si potrebbero essere presenti due oggetti diversi nel metaverse hello con hello stesso attributo di posta elettronica se l'oggetto contatto hello è stato importato prima dell'oggetto utente hello. Durante l'esportazione tooAzure Active Directory, verrà generato un errore. Questo comportamento è previsto e indica dati errati o tale topologia hello non è stato identificato correttamente durante l'installazione di hello.

## <a name="disabled-accounts"></a>Account disabilitati
Gli account disabilitati vengono sincronizzati anche tooAzure Active Directory. Gli account disabilitati sono risorse toorepresent comuni in Exchange, ad esempio le sale riunioni. eccezione Hello è composto da utenti con una cassetta postale collegata; come accennato in precedenza, questi non verrà eseguito il provisioning di un tooAzure account Active Directory.

presupposto Hello è che se viene trovato un account utente disabilitato, quindi non verrà trovato un altro account attivo in un secondo momento e oggetto hello è stato eseguito il provisioning tooAzure Active Directory con hello userPrincipalName e sourceAnchor individuati. Nel caso un altro account attivo verrà aggiunto toohello stesso oggetto metaverse, quindi il userPrincipalName e sourceAnchor verrà utilizzato.

## <a name="changing-sourceanchor"></a>Modifica dell'attributo sourceAnchor
Quando un oggetto è stato esportato tooAzure Active Directory, quindi non è consentito toochange hello sourceAnchor più. Quando è stato attributo metaverse hello esportata oggetto hello **cloudSourceAnchor** viene impostato con hello **sourceAnchor** valore accettato da Azure AD. Se **sourceAnchor** viene modificato e non corrispondere **cloudSourceAnchor**, regola hello **Out tooAAD – User Join** genererà l'errore hello **attributo sourceAnchor è stato modificato**. In questo caso, la configurazione hello o i dati devono essere corretti così hello stesso attributo sourceAnchor sia presente nel metaverse hello nuovamente hello oggetto venga sincronizzato nuovamente.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

