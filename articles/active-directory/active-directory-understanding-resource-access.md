---
title: accesso alle risorse aaaUnderstanding in Azure | Documenti Microsoft
description: In questo argomento vengono illustrati i concetti sull'utilizzo di accesso alle risorse di sottoscrizione amministratori toocontrol in hello portale completo di Azure
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Informazioni sull'accesso alle risorse in Azure
> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Hello Azure portale fornisce [controllo di accesso basato sui ruoli](role-based-access-control-configure.md) in modo le risorse di Azure possono essere gestite in modo più preciso.
> 
> 

Nell'ottobre del 2013, hello portale di Azure classico e API di gestione dei servizi sono state integrate con Azure Active Directory in ordine toolay hello lavoro di base per migliorare l'esperienza utente hello per la gestione delle risorse tooAzure di accesso. Azure Active Directory offre già potenti funzionalità per la gestione degli utenti, per la sincronizzazione della directory locale, per l'autenticazione a più fattori e il controllo di accesso alle applicazioni. Naturalmente, queste funzionalità dovrebbero essere rese disponibili per la gestione delle risorse di Azure a livello generale.

La fatturazione costituisce il punto di partenza per il controllo di accesso in Azure. proprietario Hello di un account Azure, accedere visitando hello [centro account Azure](https://account.windowsazure.com/subscriptions), è hello amministratore dell'account. Le sottoscrizioni sono un contenitore per la fatturazione, ma vengono utilizzate anche come limite di sicurezza: ogni sottoscrizione dispone di un servizio amministratore (SA) che è possibile aggiungere, rimuovere e modificare le risorse di Azure nella sottoscrizione specificata mediante hello [portale di Azure classico](https://manage.windowsazure.com/). hello è Hello predefinito SA di una nuova sottoscrizione, ma hello AA modificabili SA hello in hello centro account Azure.

<br><br>![Account Azure][1]

Le sottoscrizioni dispongono anche di un'associazione a una directory. directory Hello definisce un set di utenti. Può trattarsi di utenti da hello aziendale o dell'istituto di istruzione che ha creato la directory hello o possono essere utenti esterni (vale a dire Accounts Microsoft). Le sottoscrizioni sono accessibili da un subset di tali utenti di directory che sono stati assegnati come servizio amministratore (SA) o coamministratore (CA); Hello solo eccezione è che, per motivi di compatibilità, Accounts Microsoft (precedentemente Windows Live ID) possono essere assegnati come SA o CA senza essere presenti nella directory hello.

<br><br>![Controllo di accesso in Azure][2]

Funzionalità disponibili nel portale di Azure classico hello consentono associazioni di sicurezza che sono firmati con una directory di hello toochange Account Microsoft che è associata una sottoscrizione utilizzando hello **modifica Directory** comando hello **Sottoscrizioni** pagina **impostazioni**. Si noti che questa operazione ha implicazioni sul controllo di accesso hello della sottoscrizione in questione.

> [!NOTE]
> Hello **modifica Directory** comando in hello Azure classico portale non è disponibile toousers che ha effettuato l'accesso usando un account aziendale o dell'istituto di istruzione perché tali account possono accedere solo toohello directory toowhich appartengono.
> 
> 

<br><br>![Flusso di accesso utente semplice][3]

Nel caso più semplice hello, un'organizzazione (ad esempio Contoso) viene applica la fatturazione e il controllo di accesso hello stesso set di sottoscrizioni. Directory di hello è toosubscriptions associato che appartengono a un singolo Account Azure. Una volta eseguito correttamente l'accesso toohello portale di Azure classico, gli utenti visualizzeranno due raccolte di risorse (in arancione nella figura precedente hello):

* Directory in cui è presente l'account utente (originato o aggiunto come entità esterna). Si noti directory hello usata per l'accesso non è pertinente toothis calcolo, pertanto le directory verranno sempre visualizzate indipendentemente dal fatto in cui connesso.
* Le risorse che fanno parte delle sottoscrizioni associate con directory hello usata per l'accesso e a cui hello utente può accedere (in cui sono un SA o CA).

<br><br>![Utente con più sottoscrizioni e directory][4]

Gli utenti con le sottoscrizioni in più directory hanno hello possibilità tooswitch hello contesto corrente del portale di Azure classico hello utilizzando il filtro di sottoscrizione hello. In realtà hello, il risultato è una directory diversa tooa di account di accesso separato, ma questa operazione viene eseguita senza problemi utilizzando single sign-on (SSO).

Operazioni quali lo spostamento di risorse tra sottoscrizioni possono risultare più difficoltose a causa della visualizzazione a directory singola delle sottoscrizioni. trasferimento di risorse tooperform hello, potrebbe essere necessario toofirst utilizzare hello **modifica Directory** comando nella pagina sottoscrizioni hello **impostazioni** tooassociate hello sottoscrizioni toohello stessa directory .

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sugli amministratori toochange per una sottoscrizione di Azure, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Per ulteriori informazioni sulla correlazione tooyour sottoscrizione di Azure da parte di Azure Active Directory, vedere [delle sottoscrizioni Azure sono associate con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Per ulteriori informazioni su come tooassign ruoli in Azure AD, vedere [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
