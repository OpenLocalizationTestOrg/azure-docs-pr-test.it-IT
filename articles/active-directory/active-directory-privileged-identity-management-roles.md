---
title: in Azure AD Privileged Identity Management aaaRoles | Documenti Microsoft
description: "Informazioni quali i ruoli vengono utilizzati per le identità con privilegi con hello estensione Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Ruolo amministrativo differente in Azure AD PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

È possibile assegnare gli utenti dell'organizzazione ruoli amministrativi toodifferent in Azure AD. Queste assegnazioni di ruolo controllano quali attività, ad esempio aggiunta o rimozione di utenti o modificare le impostazioni di servizio, gli utenti di hello sono in grado di tooperform in AD Azure, Office 365 e altri Microsoft Online Services e applicazioni connesse.  

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

Un amministratore globale può aggiornare gli utenti che **definitivamente** assegnato tooroles in Azure AD, usando i cmdlet di PowerShell, ad esempio `Add-MsolRoleMember` e `Remove-MsolRoleMember`, o tramite il portale classico di hello come descritto in [ l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management (PIM) gestisce i criteri per l'accesso con privilegi per gli utenti in Azure AD. PIM assegna gli utenti tooone o più ruoli in Azure AD, ed è possibile assegnare un utente toobe in modo permanente nel ruolo hello o idonee per il ruolo di hello. Quando un utente è assegnato in modo permanente il ruolo tooa o attiva un'assegnazione di ruolo idoneo, quindi è possibile gestire Azure Active Directory, Office 365 e altre applicazioni con autorizzazioni hello tootheir ruoli assegnate.

Non vi è alcuna differenza nell'accesso hello dato toosomeone con permanente e un'assegnazione di ruolo idoneo. Hello unica differenza è che alcuni utenti non è necessario che l'accesso tutto il tempo hello. Sono idonee per il ruolo di hello e può attivare e disattivare ogni volta che è necessario.

## <a name="roles-managed-in-pim"></a>Ruoli gestiti in PIM
Privileged Identity Management consente di assegnare ruoli di amministratore toocommon degli utenti, tra cui:

* **Amministratore globale** (noto anche come amministratore della società) ha accesso alle funzionalità di amministrazione tooall. Si può avere più di un amministratore globale nell'organizzazione. persona Hello che effettua l'iscrizione a Office 365 toopurchase automaticamente diventa amministratore globale.
* **amministratore dei ruoli con privilegi** gestisce Azure AD PIM e aggiorna le assegnazioni dei ruoli per gli altri utenti.  
* **Amministratore fatturazione** : effettua acquisti, gestisce le sottoscrizioni, gestisce i ticket di supporto e monitora l'integrità del servizio.
* **Amministratore password** : reimposta le password, gestisce le richieste di servizio e monitora l'integrità del servizio. Gli amministratori di password sono limitate tooresetting le password degli utenti.
* **Amministratore del servizio** : gestisce le richieste di servizio e monitora l'integrità del servizio.
  
  > [!NOTE]
  > Se si utilizza Office 365, quindi prima di assegnare l'utente tooa ruolo di amministratore del servizio di hello, innanzitutto assegnare autorizzazioni amministrative di hello utente tooa servizio, ad esempio Exchange Online.
  > 
  > 
* **amministratore Gestione utenti** reimposta le password, effettua il monitoraggio dell'integrità del servizio e gestisce gli account utente, i gruppi di utenti e le richieste di servizio. gestione salve utente non è possibile eliminare un amministratore globale, creare altri ruoli di amministratore o reimpostare le password per la fatturazione, globali e gli amministratori del servizio.
* **Amministratore di Exchange** dispone di accesso amministrativo tooExchange Online tramite l'interfaccia di amministrazione di Exchange hello EAC () e può eseguire qualsiasi attività in Exchange Online.
* **L'amministratore di SharePoint** dispone di accesso amministrativo tooSharePoint Online tramite Centro di amministrazione di SharePoint Online hello e può eseguire qualsiasi attività in SharePoint Online.
* **Skype per amministratore aziendale** dispone di accesso amministrativo tooSkype per Business tramite hello Skype per centro di amministrazione di Business e possono eseguire qualsiasi attività in Skype for Business Online.

Leggere gli articoli seguenti per altre informazioni sull'[assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md) e sull'[assegnazione dei ruoli di amministratore in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


Da PIM, è possibile [assegnare queste utente tooa ruoli](active-directory-privileged-identity-management-how-to-add-role-to-user.md) in modo che possibilità hello utente [attivare hello ruolo quando necessario](active-directory-privileged-identity-management-how-to-activate-role.md).

Se si desidera toogive un altro utente accesso toomanage in PIM, i ruoli di hello PIM richiede hello utente toohave ulteriori informazioni, vedere [modalità di accesso tooPIM toogive](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Ruoli non gestiti in PIM
I ruoli in Exchange Online o SharePoint Online, ad eccezione di quelli indicati in precedenza, non sono rappresentati in Azure AD e quindi non sono visibili in PIM. Per altre informazioni sulla modifica delle assegnazioni di ruolo specifiche in questi servizi di Office 365, vedere [Autorizzazioni in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

In Azure AD non sono rappresentati neanche i gruppi di risorse e le sottoscrizioni di Azure. toomanage Azure sottoscrizioni, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../billing/billing-add-change-azure-subscription-administrator.md) e per altre informazioni su Azure RBAC vedere [gestire il controllo di accesso](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Ruoli utente e accesso
Per alcune applicazioni e servizi Microsoft, l'assegnazione di un ruolo di utente tooa potrebbe non essere sufficiente tooenable che toobe utente amministratore.

Accesso toohello portale di Azure classico richiede hello utente da un amministratore del servizio o coamministratore di una sottoscrizione di Azure, anche se hello utente non è necessario toomanage hello le sottoscrizioni di Azure.  Ad esempio, le impostazioni di configurazione toomanage per Azure AD nel portale classico di hello, un utente devono essere sia un amministratore globale di Azure AD e CO-amministratore della sottoscrizione di una sottoscrizione di Azure.  sottoscrizioni di tooAzure tooadd gli utenti, vedere toolearn [come tooadd o modificare i ruoli di amministratore di Azure](../billing/billing-add-change-azure-subscription-administrator.md).

Servizi Online possono richiedere tooMicrosoft di accesso utente hello anche essere assegnata una licenza prima di poter aprire il portale del servizio hello o eseguire attività amministrative.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Assegnare un utente di tooa di licenza di Azure AD
1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com) con un account amministratore globale o un coamministratore.
2. Selezionare **tutti gli elementi** dal menu principale di hello.
3. Selezionare la directory di hello desiderato toowork con e che le licenze è associato.
4. Selezionare **Licenze**. verrà visualizzato l'elenco di Hello di licenze disponibili.
5. Piano di licenza Select hello, che contiene le licenze di hello che si desidera toodistribute.
6. Selezionare **Assegna utenti**.
7. Utente di selezionare hello che si desidera tooassign una licenza per.
8. Fare clic su hello **assegnare** pulsante.  Hello utente possa ora accedere tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

