---
title: Come aggiungere o rimuovere un ruolo utente | Documentazione Microsoft
description: "Informazioni su come aggiungere ruoli alle identità con privilegi con l'applicazione Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/03/2018
ms.author: billmath
ms.openlocfilehash: 53deb04a33a5f878c5e3f765099c54d30e6ac005
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Come aggiungere o rimuovere un ruolo utente
Con Azure Active Directory, un amministratore globale o un amministratore della società può aggiornare gli utenti assegnati **in modo permanente** ai ruoli in Azure AD. Per questa operazione è necessario usare i cmdlet di PowerShell, ad esempio `Add-MsolRoleMember` e `Remove-MsolRoleMember`. Oppure usare il portale di Azure come descritto in [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).

L'applicazione Azure AD Privileged Identity Management consente agli amministratori dei ruoli con privilegi di effettuare anche assegnazioni di ruolo permanenti. Inoltre, gli amministratori di ruolo con privilegi possono rendere gli utenti **idonei** ai ruoli di amministratore. Un amministratore idoneo può attivare il ruolo quando serve e le relative autorizzazioni scadono al termine delle operazioni.

## <a name="manage-roles-with-pim-in-the-azure-portal"></a>Gestire i ruoli con PIM nel portale di Azure
All'interno dell'organizzazione è possibile assegnare gli utenti a diversi ruoli amministrativi in Azure AD, Office 365 e altri servizi e applicazioni Microsoft.  Per informazioni dettagliate sui ruoli disponibili, vedere [Ruoli in Azure AD PIM](active-directory-privileged-identity-management-roles.md).

Per aggiungere o rimuovere un utente in un ruolo usando Privileged Identity Management, visualizzare il dashboard PIM. Quindi fare clic sul pulsante **Utenti in ruoli amministrativi** o selezionare un ruolo specifico (ad esempio Amministratore globale) dalla tabella dei ruoli.

> [!NOTE]
> Se ancora non è stato abilitato il servizio PIM nel portale di Azure, vedere [Introduzione ad Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) .

Per concedere a un altro utente l'accesso al servizio PIM stesso, vedere [come concedere l'accesso a PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)per informazioni dettagliate sui ruoli utente necessari per l'uso di PIM.

## <a name="add-a-user-to-a-role"></a>Aggiungere un utente a un ruolo
1. Nel [portale di Azure](https://portal.azure.com/)selezionare il riquadro **Azure AD Privileged Identity Management** nel dashboard.
2. Selezionare **Gestione dei ruoli con privilegi**.
3. Selezionare il ruolo che si vuole gestire dalla tabella **Riepilogo del ruolo** .
4. Nel pannello del ruolo selezionare **Aggiungi**.
5. Fare clic su **Seleziona utenti** e cercare l'utente nel pannello **Seleziona utenti**.  
6. Selezionare l'utente nell'elenco dei risultati della ricerca e quindi fare clic su **Fine**.
7. Fare clic su **OK** per salvare la selezione. L'utente selezionato verrà visualizzato nell'elenco come idoneo per il ruolo.

> [!NOTE]
> Per impostazione predefinita, i nuovi utenti in un ruolo sono idonei solo per il ruolo. Se si desidera rendere permanente il ruolo, fare clic sull'utente nell'elenco. Le informazioni relative all'utente verranno visualizzate in un nuovo pannello. Scegliere **Rendi permanente** nel menu delle informazioni dell'utente.  
> Se un utente non riesce a eseguire la registrazione ad Azure Multi-Factor Authentication (MFA) o usa un account Microsoft, in genere @outlook.com, è necessario rendere l'utente permanente in tutti i relativi ruoli. Gli amministratori idonei devono effettuare la registrazione a MFA durante l'attivazione.

Ora che l'utente è idoneo per un ruolo, è necessario comunicargli che può attivarlo in base alle istruzioni fornite in [Come attivare o disattivare un ruolo](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Rimuovere un utente da un ruolo
È possibile rimuovere gli utenti da assegnazioni di idoneità al ruolo, ma è necessario assicurarsi che sia sempre presente almeno un utente con ruolo di amministratore globale permanente.

Per rimuovere un utente specifico da un ruolo, seguire questa procedura:

1. Passare al pannello del ruolo selezionando un ruolo nel dashboard di Azure AD PIM oppure facendo clic sul pulsante **Utenti con ruoli di amministratore** .
2. Selezionare l'utente nell'elenco degli utenti.
3. Fare clic su **Rimuovi**. Verrà visualizzato un messaggio che richiede la conferma.
4. Fare clic su **Sì** per rimuovere il ruolo dall'utente.

Se non si è certi se gli utenti necessitano ancora delle assegnazioni di ruoli, è possibile [avviare una verifica di accesso per il ruolo](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

