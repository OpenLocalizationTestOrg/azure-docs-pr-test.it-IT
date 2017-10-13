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
ms.openlocfilehash: 495e926a1975128707212ba571d47cfc7c9507b3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Servizio di sincronizzazione Azure AD Connect: Informazioni su utenti e contatti
I motivi per cui possono essere presenti più foreste Active Directory e sono disponibili più topologie di distribuzione sono diversi. I modelli comuni prevedono una distribuzione account-risorse e foreste sincronizzate tramite Elenco indirizzi globale dopo operazioni di fusione e acquisizione. Anche se esistono modelli puri, sono molto diffusi anche i modelli ibridi. La configurazione predefinita nel servizio di sincronizzazione Azure AD Connect non presuppone alcun modello specifico, ma è possibile osservare diversi comportamenti in base all'opzione di corrispondenza utenti selezionata nella guida all'installazione.

Questo argomento illustra il comportamento della configurazione predefinita in determinate topologie. Sarà anche possibile esaminare la configurazione tramite l'editor delle regole di sincronizzazione.

La configurazione presuppone le regole generali seguenti:

* Indipendentemente dall'ordine di importazione dalle directory di Active Directory di origine, il risultato finale sarà sempre lo stesso.
* Un account attivo fornirà sempre le informazioni di accesso, inclusi gli attributi **userPrincipalName** e **sourceAnchor**.
* Un account disabilitato fornirà gli attributi userPrincipalName e sourceAnchor, a meno che non si tratti di una cassetta postale collegata, se non è presente alcun account attivo da trovare.
* Un account con una cassetta postale collegata non verrà usato per gli attributi userPrincipalName e sourceAnchor. Si presuppone che un account attivo venga trovato in seguito.
* È possibile eseguire il provisioning di un oggetto contatto in Azure AD come contatto o come utente. Questa informazione non è nota finché tutte le foreste Active Directory di origine non sono state elaborate.

## <a name="contacts"></a>Contatti
I contatti che rappresentano un utente in una foresta diversa costituiscono una situazione comune dopo un'operazione di acquisizione o fusione in cui la soluzione GALSync collega due o più foreste di Exchange. L'oggetto contatto viene sempre aggiunto dallo spazio connettore allo spazio metaverse usando l'attributo mail. Se è già presente un oggetto contatto o un oggetto utente con lo stesso indirizzo di posta elettronica, gli oggetti vengono uniti. Questo comportamento è configurato nella regola **In ingresso da Active Directory - Aggiunta contatto**. Esiste anche una regola denominata **In ingresso da Active Directory - Contatto comune** con un flusso dell'attributo all'attributo metaverse **sourceObjectType** con la costante **Contact**. Questa regola presenta una precedenza molto bassa, quindi se un oggetto utente viene aggiunto allo stesso oggetto metaverse, la regola **In ingresso da Active Directory - Utente comune** fornirà il valore Utente a questo attributo. Con questa regola l'attributo avrà il valore Contact solo se non sono stati aggiunti utenti e il valore User se è stato trovato almeno un utente.

Per eseguire il provisioning di un oggetto in Azure AD, la regola in uscita **In uscita ad Azure AD - Unione contatto** creerà un oggetto contatto se l'attributo metaverse **sourceObjectType** è impostato su **Contatto**. Se questo attributo è impostato su **Utente**, la regola **In uscita ad Azure AD - Unione utente** creerà un oggetto utente.
È possibile che un oggetto venga innalzato di livello da Contact a User quando vengono importate e sincronizzate più directory di Active Directory di origine.

Ad esempio, in una topologia GALSync saranno presenti oggetti contatto per tutti gli oggetti della seconda foresta quando si importa la prima. Verranno quindi inseriti nuovi oggetti contatto nel connettore AAD. Quando in seguito si importa e si sincronizza la seconda foresta, saranno presenti gli utenti effettivi che verranno aggiunti agli oggetti metaverse esistenti. Si procederà quindi all'eliminazione dell'oggetto contatto in Azure AD e verrà creato un nuovo oggetto utente.

In una topologia in cui gli utenti sono rappresentati come contatti, nella guida all'installazione assicurarsi di selezionare la corrispondenza degli utenti in base all'attributo Mail. Se si seleziona un'altra opzione, si otterrà una configurazione dipendente dall'ordine. L'aggiunta degli oggetti contatto verrà sempre eseguita in base all'attributo Mail, ma gli oggetti utente verranno aggiunti in base all'attributo Mail solo se questa opzione è stata selezionata nella guida all'installazione. Se l'oggetto contatto viene importato prima dell'oggetto utente, nell'oggetto metaverse potrebbero essere presenti due oggetti diversi con lo stesso attributo Mail. Durante l'esportazione in Azure AD, verrà generato un errore. Si tratta di un comportamento da progettazione che indica che sono presenti dati non validi o che durante l'installazione la topologia non è stata identificata correttamente.

## <a name="disabled-accounts"></a>Account disabilitati
Anche gli account disabilitati vengono sincronizzati con Azure AD. Gli account disabilitati in genere rappresentano le risorse in Exchange, ad esempio le sale riunioni. Fanno eccezione gli utenti con una cassetta postale collegata. Come indicato in precedenza, per questi non verrà mai eseguito il provisioning di un account in Azure AD.

Si presuppone che se viene trovato un account utente disabilitato, non verrà trovato un altro account attivo successivamente e verrà effettuato il provisioning dell'oggetto in Azure AD con gli attributi userPrincipalName e sourceAnchor trovati. Se un altro account attivo viene aggiunto allo stesso oggetto metaverse, verranno usati i relativi attributi userPrincipalName e sourceAnchor.

## <a name="changing-sourceanchor"></a>Modifica dell'attributo sourceAnchor
Dopo che un oggetto è stato esportato in Azure AD, non è più possibile modificarne l'attributo sourceAnchor. Dopo che l'oggetto è stato esportato, l'attributo metaverse **cloudSourceAnchor** viene impostato sul valore **sourceAnchor** accettato da Azure AD. Se **sourceAnchor** viene modificato e non corrisponde a **cloudSourceAnchor**, la regola **In uscita ad Azure AD - Unisci utente** genera un errore indicante che **l'attributo sourceAnchor è stato modificato**. In questo caso, è necessario correggere la configurazione o i dati in modo che lo stesso attributo sourceAnchor sia di nuovo presente nell'oggetto metaverse prima che l'oggetto venga sincronizzato di nuovo.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

