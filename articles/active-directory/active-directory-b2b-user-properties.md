---
title: aaaProperties di un utente di collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Le proprietà di un utente di Collaborazione B2B di Azure Active Directory sono configurabili"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Proprietà di un utente di Collaborazione B2B di Azure Active Directory

Un utente di Collaborazione B2B (business-to-business ) di Azure Active Directory (Azure AD) è un utente con UserType = Guest. L'utente guest in genere da un'organizzazione partner e dispone di privilegi in hello si invitano directory, per impostazione predefinita limitati.

A seconda di hello si invitano esigenze dell'organizzazione, un utente di collaborazione B2B di Azure AD può essere in uno dei seguenti stati di account hello:

- Stato 1: Incluso in un'istanza esterna di Azure AD e rappresentato come un utente guest in hello si invitano dell'organizzazione. In questo caso, hello B2B utente accede utilizzando un account di Azure AD a cui appartiene il tenant invitato toohello. Se l'organizzazione partner hello non usa Azure AD, l'utente guest hello in Azure AD viene ancora creata. requisiti di Hello sono che essi riscattare gli invito e Azure AD verifica indirizzo di posta elettronica. Questa disposizione è detta anche tenancy JIT o "virale".

- Stato 2: Incluso in un account Microsoft e rappresentato come un utente guest organizzazione host hello. In questo caso, l'utente guest hello accede con un account Microsoft. Hello invitato social identità utente (google.com o simile), che non è un account Microsoft, viene creato come un account Microsoft durante il riscatto di offerta.

- Stato 3: Incluso in Active Directory di hello host organizzazione locale e sincronizzati con Azure dell'organizzazione di hello host Active Directory. Durante questa versione, è necessario usare PowerShell toomanually modifica hello UserType di tali utenti nel cloud hello.

- Stato 4: Ospitati in Azure dell'organizzazione host Active Directory con UserType = Guest e le credenziali che gestisce l'organizzazione host hello.

  ![visualizzazione iniziali del mittente hello](media/active-directory-b2b-user-properties/redemption-diagram.png)


Viene ora illustrato l'aspetto dell'utente di Collaborazione B2B di Azure AD nello stato 1 in Azure AD.

### <a name="before-invitation-redemption"></a>Prima del riscatto dell'invito

![Prima del riscatto dell'offerta](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Dopo il riscatto dell'invito

![Dopo il riscatto dell'offerta](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Proprietà chiave dell'utente di collaborazione Azure AD B2B hello
### <a name="usertype"></a>UserType
Questa proprietà indica la relazione hello di tenancy di hello utente toohello host. I valori possibili per questa proprietà sono due.
- Membro: Questo valore indica un dipendente dell'organizzazione host hello e un utente Payroll dell'organizzazione hello. Ad esempio, l'utente si aspetta toohave accedere ai siti solo toointernal. e non viene considerato un collaboratore esterno.

- Guest: Questo valore indica che un utente che non è considerato interno toohello aziendale, ad esempio un collaboratore esterno, partner, clienti o utente simile. Questo utente non essere previsto tooreceive memo interno un CEO o ricevere i vantaggi aziendali, ad esempio.

  > [!NOTE]
  > Hello UserType non ha alcuna relazione toohow hello utente consente l'accesso, ruolo della directory hello di utente hello e così via. Questa proprietà è semplicemente indica hello relazione toohello host organizzazione utente e consente l'organizzazione hello criteri tooenforce che dipendono da questa proprietà.

### <a name="source"></a>Sorgente
Questa proprietà indica la modalità hello utente effettua l'accesso.

- Utente invitato: l'utente è stato invitato ma non ha ancora riscattato l'invito.

- Active Directory esterno: L'utente è incluso in un'organizzazione esterna e per eseguire l'autenticazione utilizzando un account di Azure AD che appartiene toohello un'altra organizzazione. Questo tipo di accesso corrisponde tooState 1.

- Account Microsoft: l'utente è incluso in un account Microsoft ed esegue l'autenticazione con un account Microsoft. Questo tipo di accesso corrisponde tooState 2.

- Windows Server Active Directory: L'utente ha effettuato l'accesso da Active Directory locale che appartiene toothis organizzazione. Questo tipo di accesso corrisponde tooState 3.

- Azure Active Directory: L'utente esegue l'autenticazione con un account di Azure AD a cui appartiene l'organizzazione toothis. Questo tipo di accesso corrisponde tooState 4.
  > [!NOTE]
  > Source e UserType sono proprietà indipendenti. Un valore di Source non implica un valore UserType specifico.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Possibilità di aggiungere utenti B2B di Azure AD come membri anziché come guest
In genere, utente B2B di Azure AD è sinonimo di utente guest. Un utente di Collaborazione B2B di Azure AD viene quindi aggiunto come utente con UserType = Guest per impostazione predefinita. Tuttavia, in alcuni casi, organizzazione partner hello è che un membro di un'organizzazione di più grande organizzazione toowhich hello host appartiene anche. In caso affermativo, organizzazione host hello possibile tootreat gli utenti nell'organizzazione partner hello come membri anziché guest. Utilizzare tooadd le API di Azure AD B2B invito Manager hello o invitare un utente da un'organizzazione hello partner dell'organizzazione toohello host come un membro.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filtro per gli utenti guest nella directory hello

![Filtrare gli utenti guest](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Convertire UserType
Attualmente, è possibile che gli utenti tooconvert UserType dal membro tooGuest e viceversa tramite PowerShell. Tuttavia, hello proprietà UserType dovrebbe toorepresent hello relazione toohello organizzazione utente. Pertanto, il valore di hello di questa proprietà deve cambiare solo se la relazione hello dell'organizzazione di hello utente toohello viene modificata. Se viene modificata la relazione hello dell'utente hello, devono essere risolti problemi, ad esempio se è necessario modificare hello nome principale (UPN)? Utente hello continueranno toohave accesso toohello stesse risorse? È necessario assegnare una cassetta postale all'utente? Pertanto, non è consigliabile modificare hello UserType utilizzando PowerShell come attività atomiche. Se questa proprietà non sarà più modificabile con PowerShell, non è consigliabile creare una dipendenza da questo valore.

## <a name="remove-guest-user-limitations"></a>Rimuovere le limitazioni dell'utente guest
Potrebbero essere presenti i casi in cui si desidera toogive i privilegi più elevati di utenti guest. È possibile aggiungere un ruolo di tooany utente guest e anche rimuovere le restrizioni degli utenti guest di hello predefinito in hello directory toogive hello un utente stesso privilegi come membri.

È possibile tooturn off limitazioni utente guest valore predefinito di hello in modo che un utente guest nella directory aziendale hello hello delle stesse autorizzazioni necessarie per un utente del membro.

![Rimuovere le limitazioni dell'utente guest](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Controllo e creazione di report di un utente di Collaborazione B2B](active-directory-b2b-auditing-and-reporting.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)
