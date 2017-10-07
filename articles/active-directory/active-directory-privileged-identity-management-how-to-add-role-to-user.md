---
title: aaaHow tooadd o rimuovere un ruolo utente | Documenti Microsoft
description: "Informazioni su come identità di tooprivileged tooadd ruoli con hello applicazione Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Come tooadd o rimuovere un ruolo utente
Con Azure Active Directory (Active Directory), un amministratore globale (o l'amministratore della società) può aggiornare gli utenti che **definitivamente** assegnato tooroles in Azure AD. Per questa operazione è necessario usare i cmdlet di PowerShell, ad esempio `Add-MsolRoleMember` e `Remove-MsolRoleMember`. O hello portale di Azure classico possono usare come descritto in [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).

Hello applicazione Azure AD Privileged Identity Management consente agli amministratori di ruolo con privilegi toomake permanente le assegnazioni di ruolo, nonché. Inoltre, gli amministratori di ruolo con privilegi possono rendere gli utenti **idonei** ai ruoli di amministratore. Un amministratore idoneo può attivare il ruolo di hello quando hanno bisogno, e quindi le relative autorizzazioni scadono una volta completati.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Gestire ruoli PIM in hello portale di Azure
All'interno dell'organizzazione, è possibile assegnare gli utenti ruoli amministrativi toodifferent in Azure AD, applicazioni e servizi di Microsoft Office 365 e altri.  Ulteriori informazioni sui ruoli disponibile hello sono reperibile in [ruoli in Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd o rimuovere un utente in un ruolo con Privileged Identity Management, visualizzare il dashboard PIM hello. Quindi fare clic su hello **gli utenti nei ruoli di amministratore** pulsante o selezionare un ruolo specifico (ad esempio, un amministratore globale) dalla tabella ruoli hello.

> [!NOTE]
> Se è ancora stata abilitata PIM in hello portale di Azure, andare troppo[Guida introduttiva di Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) per informazioni dettagliate.

Se si desidera toogive tooPIM di accesso un altro utente stesso, i ruoli di hello che richiede di PIM hello utente toohave ulteriori informazioni, vedere [modalità di accesso tooPIM toogive](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Aggiungere un ruolo di utente tooa
1. In hello [portale di Azure](https://portal.azure.com/)selezionare hello **Azure AD Privileged Identity Management** riquadro nel dashboard di hello.
2. Selezionare **Gestione dei ruoli con privilegi**.
3. In hello **riepilogo ruolo** tabella, il ruolo di hello selezionare da toomanage.
4. Nel pannello dei ruoli hello, selezionare **Aggiungi**.
5. Fare clic su **selezionare utenti** e la ricerca per utente hello hello **selezionare utenti** blade.  
6. Selezionare hello utente dall'elenco dei risultati di ricerca hello e fare clic su **eseguita**.
7. Fare clic su **OK** toosave la selezione. Hello l'utente selezionato verrà visualizzata nell'elenco di hello come idoneo per il ruolo di hello.

> [!NOTE]
> Nuovi utenti in un ruolo solo sono idonei per il ruolo di hello per impostazione predefinita. Se si desidera ruolo hello toomake permanente, fare clic su utente hello nell'elenco di hello. informazioni dell'utente Hello verranno visualizzato in un nuovo pannello. Selezionare **verificare autorizzazioni** nel menu di informazioni utente hello.  
> Se un utente non è possibile registrare per Azure multi-Factor Authentication (MFA) o utilizza un account Microsoft (in genere @outlook.com), è necessario toomake li permanenti in tutti i relativi ruoli. Amministratori idonei sono frequenti tooregister per l'autenticazione a più fattori durante l'attivazione.

Ora che hello utente è idoneo per un ruolo, informare gli utenti che si può essere attivato in base a istruzioni toohello [come tooactivate o disattivare un ruolo](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Rimuovere un utente da un ruolo
È possibile rimuovere gli utenti da assegnazioni di idoneità al ruolo, ma è necessario assicurarsi che sia sempre presente almeno un utente con ruolo di amministratore globale permanente.

Seguire questi tooremove passaggi, un utente specifico da un ruolo:

1. Passare toohello ruolo nell'elenco di ruoli hello selezionando un ruolo nel dashboard di Azure AD PIM hello o facendo clic su hello **gli utenti nei ruoli di amministratore** pulsante.
2. Fare clic sull'utente hello nell'elenco di utenti hello.
3. Fare clic su **Rimuovi**. Un messaggio chiederà tooconfirm.
4. Fare clic su **Sì** ruolo hello tooremove utente hello.

Se non si è certi gli utenti devono comunque le assegnazioni di ruolo, è quindi possibile [avviare una revisione di accesso per il ruolo di hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

