---
title: "le sottoscrizioni di gestione delle identità aaaPrivileged - Azure | Documenti Microsoft"
description: Illustra la sottoscrizione hello e requisiti per la gestione e l'utilizzo di Azure AD Privileged Identity Management nel tenant di licenza
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Requisiti di sottoscrizione di Azure Active Directory Privileged Identity Management

Azure AD Privileged Identity Management è disponibile come parte della versione di hello P2 Premium di Azure AD. Per ulteriori informazioni su hello altre funzionalità di P2 e mette a confronto tooPremium P1, vedere [edizioni di Azure Active Directory](../active-directory-editions.md).

>[!NOTE]
Quando Azure Active Directory (Azure AD) Privileged Identity Management è stato in anteprima, non vi sono controlli alcuna licenza per un servizio di hello tootry tenant.  Ora che Azure AD Privileged Identity Management ha raggiunto la disponibilità generale, una sottoscrizione di valutazione o a pagamento deve essere presente per hello tenant toocontinue con Privileged Identity Management dopo dicembre 2016.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Confermare la sottoscrizione di valutazione o a pagamento

Se non si è certi se l'organizzazione ha una versione di valutazione o acquistare una sottoscrizione, quindi è possibile verificare se è associata una sottoscrizione nel tenant utilizzando i comandi di hello inclusi in Azure Active Directory modulo per Windows PowerShell V1. 
1. Aprire una finestra di PowerShell.
2. Immettere `Connect-MsolService` tooauthenticate come utente nel tenant.
3. Immettere `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Questo comando Recupera un elenco di sottoscrizioni hello nel tenant. Se sono state che non restituite righe, che è necessario un P2 Azure AD Premium tooobtain versione di valutazione, acquistare una sottoscrizione di Azure AD Premium P2 o sottoscrizione di EMS E5 toouse Azure AD Privileged Identity Management.  tooget una versione di valutazione e iniziare a utilizzare Azure AD Privileged Identity Management, leggere [Guida introduttiva di Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Se questo comando restituisce una riga in cui SkuPartNumber è "AAD_PREMIUM_P2" o "EMSPREMIUM" e IsTrial è "True", indica che una versione di valutazione di Azure AD Premium P2 è presente nel tenant di hello.  Se non è abilitato lo stato della sottoscrizione hello e non è un acquisto della sottoscrizione Azure AD Premium P2 o E5 EMS, è necessario acquistare una sottoscrizione di Azure AD Premium P2 o EMS E5 sottoscrizione toocontinue utilizzando Azure AD Privileged Identity Management.

Azure AD Premium P2 è disponibile tramite un [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), hello e [programma Cloud Solution Provider](https://partner.microsoft.com/en-US/cloud-solution-provider). I sottoscrittori di Azure e Office 365 possono acquistare Azure AD Premium P2 anche online.  Ulteriori informazioni sui prezzi di Azure AD Premium e come tooorder online è reperibile in [dei prezzi di Azure Active Directory](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management non è disponibile nel tenant

Azure AD Privileged Identity Management non sarà più disponibile nel tenant se:
- L'organizzazione usava Azure AD Privileged Identity Management nella versione di anteprima e non è stata acquistata la sottoscrizione di Azure AD Premium P2 o a EMS E5.
- L'organizzazione era in possesso di una sottoscrizione di valutazione ad Azure AD Premium P2 o EMS E5 che è scaduta.
- L'organizzazione era in possesso di una sottoscrizione a pagamento che è scaduta.

Quando scade una sottoscrizione di Azure AD Premium P2 o EMS E5 oppure un'organizzazione che stava usando la versione di anteprima di Azure AD Privileged Identity Management non acquista una sottoscrizione di Azure AD Premium P2 o EMS E5:

- I ruoli tooAzure AD assegnazioni di ruolo permanente rimarranno invariati.
- Hello estensione Azure AD Privileged Identity Management nel portale di Azure hello, nonché i cmdlet di API Graph hello e le interfacce di PowerShell di Azure AD Privileged Identity Management, non sarà disponibile per gli utenti con privilegi tooactivate ruoli, gestire accesso con privilegi oppure eseguire l'accesso revisioni dei ruoli con privilegi.
- Le assegnazioni dei ruoli di Azure AD idonei vengono rimossi, come gli utenti non saranno in grado di tooactivate privilegiato ruoli.
- Eventuali verifiche di accesso dei ruoli di Azure AD in corso termineranno e le impostazioni di configurazione di Azure AD Privileged Identity Management verranno rimosse.
- Azure AD Privileged Identity Management non invierà più messaggi di posta elettronica sulle modifiche di assegnazioni di ruoli.

## <a name="next-steps"></a>Passaggi successivi

- [Introduzione ad Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Ruoli in Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-roles.md)
