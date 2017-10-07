---
title: "gli utenti aaaAdd da altre directory o di una società partner in Azure Active Directory | Documenti Microsoft"
description: Viene illustrato come gli utenti tooadd o modificare le informazioni utente in Azure Active Directory, inclusi gli utenti esterni e guest.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Aggiungere utenti da altre directory o società partner in Azure Active Directory

Questo articolo viene illustrato come gli utenti tooadd da altre directory in Azure Active Directory o aggiungere utenti da società partner. Per informazioni sull'aggiunta di nuovi utenti nell'organizzazione e l'aggiunta di utenti che dispongono di account Microsoft, vedere [aggiungere nuovi utenti tooAzure Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Come gli utenti guest di collaborazione B2B tooadd in Azure AD salve center, consultare [cosa è collaborazione B2B di Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)

Gli utenti aggiunti non dispongono delle autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare ruoli toothem in qualsiasi momento.

## <a name="add-a-user"></a>Aggiungere un utente
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **Active Directory**e quindi aprire la directory.
3. Seleziona hello **utenti** scheda e quindi nella barra dei comandi di hello, selezionare **Aggiungi utente**.
4. In hello **informazioni sull'utente** pagina **tipo di utente**, selezionare:

   * **Utente in un'altra directory di Azure AD** : aggiunge una directory tooyour di account utente che proviene da un'altra directory di Azure AD. È possibile selezionare un utente in un'altra directory solo se si è membri di tale directory.
   * **Gli utenti nelle società partner** -tooinvite e autorizzare directory tooyour di partner aziendale gli utenti (vedere [collaborazione B2B di Azure Active Directory](active-directory-b2b-what-is-azure-ad-b2b.md)). È necessario troppo[carica un file CSV che specifica indirizzi di posta elettronica](active-directory-b2b-references-csv-file-format.md).
5. Utente hello **profilo** pagina, fornire un nome e cognome, un nome descrittivo e un ruolo utente da hello **ruoli** elenco. Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md). Specificare se troppo**abilitare multi-Factor Authentication** per utente hello.
6. In hello **Ottieni password temporanea** selezionare **crea**.

> [!IMPORTANT]
> Se l'organizzazione utilizza più di un dominio, che è necessario conoscere i seguenti problemi quando si aggiunge un account utente di hello:
>
> * gli account utente tooadd con hello stesso nome dell'entità utente (UPN) tra i domini, **prima** aggiungere, ad esempio, geoffgrisso@contoso.onmicrosoft.com, **seguito da** geoffgrisso@contoso.com.
> * **Non** aggiungere geoffgrisso@contoso.com prima di aggiungere geoffgrisso@contoso.onmicrosoft.com.
>

Se si modificano le informazioni per un utente la cui identità è sincronizzato con il servizio Active Directory locale, è possibile modificare le informazioni utente hello in hello portale di Azure classico. toochange hello informazioni utente, utilizzare gli strumenti di gestione di Active Directory locale.

## <a name="add-external-users"></a>Aggiungere utenti esterni
È anche possibile aggiungere utenti da un altro toowhich di directory di Azure AD che si appartiene o dalle società partner caricando un file CSV. un utente esterno, tooadd per **tipo di utente**, specificare **utente in un'altra directory di Microsoft Azure AD** o **utenti nelle società partner**.

Gli utenti di questi due tipi sono originati da un'altra directory e vengono aggiunti come **utenti esterni**. Gli utenti esterni possono collaborare con altri utenti in una directory senza credenziali e i nuovi account tooadd requisito. Gli utenti esterni per l'autenticazione nella home directory quando effettuano l'accesso e che l'autenticazione funziona per qualsiasi altro toowhich directory che siano stati aggiunti.

## <a name="external-user-management-and-limitations"></a>Gestione e limiti dell'utente esterno
Quando si aggiunge un utente da un'altra directory di directory tooyour, tale utente è un utente esterno nella directory. nome utente e nome visualizzato Hello copiati da home directory e utilizzati per gli utenti esterni hello nella directory. In poi, le proprietà dell'account utente esterno hello sono completamente indipendenti. Se le modifiche alle proprietà vengono apportate toohello utente nella home directory, tali modifiche non vengano propagate toohello account utente esterno nella directory.

Hello unico collegamento tra due account hello consiste nel fatto che l'utente hello effettua sempre l'autenticazione nella home directory o con il proprio account Microsoft. Per tale motivo non una password di hello tooreset opzione o abilitare multi-factor authentication per un utente esterno. Attualmente, i criteri di autenticazione hello di hello home directory o account Microsoft sono hello solo uno che viene valutata quando l'accesso dell'utente di hello.

> [!NOTE]
> È ancora possibile disabilitare l'utente esterno di hello nella directory di hello, che blocca l'accesso tooyour directory.
>
>

Se un utente viene eliminato nella home directory o se viene annullato il proprio account Microsoft, utente esterno hello esiste ancora nella directory. Tuttavia, utente hello nella directory non è possibile accedere alle risorse perché non è l'autenticazione con una home directory o un account Microsoft.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Servizi che attualmente supportano l'accesso da parte di utenti esterni di Azure AD
* **Portale di Azure classico**: consente agli utenti esterni che un amministratore di più directory toomanage ciascuna di queste directory.
* **SharePoint Online**: se la condivisione esterna è abilitata, consente tooaccess un utente esterno alle risorse di SharePoint Online autorizzato.
* **Dynamics CRM**: se l'utente hello è concesso in licenza tramite PowerShell, consente a un utente esterno di tooaccess autorizzato risorse di Dynamics CRM.
* **Dynamics AX**: se l'utente hello è concesso in licenza tramite PowerShell, consente un tooaccess utente esterno autorizzato alle risorse in Dynamics AX. limitazioni per Hello [utenti esterni di Azure AD](#known-limitations-of-azure-ad-external-users) tooexternal utenti Dynamics AX nonché applicare.

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere nuovi utenti tooAzure Active Directory](active-directory-create-users.md)
* [Amministrazione di Azure AD](active-directory-administer.md)
* [Gestire password in Azure AD](active-directory-manage-passwords.md)
* [Gestire gruppi in Azure AD](active-directory-manage-groups.md)
