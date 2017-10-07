---
title: dominio personalizzato aaaAssign utenti tooa in Azure Active Directory | Documenti Microsoft
description: Come toopopulate un dominio personalizzato in Azure Active Directory con account utente.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Assegnare gli utenti tooa personalizzato dominio
Dopo aver aggiunto il tooAzure personalizzato di dominio Active Directory, è necessario aggiungere gli account utente di hello per questo dominio, in modo da poter iniziare tuttavia l'autenticazione.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità toomanage i nomi di dominio nel centro di amministrazione di hello Azure AD, vedere [gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Utenti sincronizzati da una directory locale
Se è già stato di una connessione tra locale Active Directory e Azure Active Directory, sincronizzazione può popolare account hello. Per ulteriori informazioni su come toosynchronize Azure Active Directory con Active Directory locale, vedere [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Gli utenti aggiunti e gestiti nel cloud hello
dominio di hello toochange per un account utente esistente:

1. Hello aprirlo portale di Azure classico utilizzando un account che è un amministratore globale o un amministratore di utente.
2. Aprire la directory.
3. Seleziona hello **utenti** scheda.
4. Selezionare hello utente dall'elenco di hello.
5. Modificare il dominio hello per utente hello e quindi selezionare **salvare**.

Questa operazione può anche essere eseguita tramite [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Selezionare un dominio personalizzato durante la creazione di un nuovo utente
1. Hello aprirlo portale di Azure classico utilizzando un account che è un amministratore globale o un amministratore di utente.
2. Aprire la directory.
3. Seleziona hello **utenti** scheda.
4. Nella barra dei comandi di hello, selezionare **Aggiungi**.
5. Quando si aggiunge il nome di utente hello, scegliere dominio personalizzato hello dall'elenco di domini hello.
6. Selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
* [Utilizzo di dominio personalizzato nomi toosimplify hello esperienza di accesso per gli utenti](active-directory-add-domain.md)
* [Gestire i nomi di dominio personalizzati](active-directory-add-manage-domain-names.md)
* [Informazioni sui concetti relativi alla gestione dei domini in Azure AD](active-directory-add-domain-concepts.md)

