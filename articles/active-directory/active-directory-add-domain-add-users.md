---
title: Assegnare gli utenti a un dominio personalizzato in Azure Active Directory | Documentazione Microsoft
description: Come popolare un dominio personalizzato in Azure Active Directory con gli account utente.
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a>Assegnare utenti a un dominio personalizzato
Dopo aver aggiunto il dominio personalizzato in Azure Active Directory, è necessario aggiungere gli account utente del dominio per poter iniziare l'autenticazione.

> [!IMPORTANT]
> Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo. Per informazioni su come gestire i nomi di dominio nell'interfaccia di amministrazione di Azure AD, vedere [Gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Utenti sincronizzati da una directory locale
Se è già stata impostata una connessione tra Active Directory locale e Azure Active Directory, la sincronizzazione può popolare gli account. Per altre informazioni sulla sincronizzazione di Azure Active Directory con Active Directory locale, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-the-cloud"></a>Utenti aggiunti e gestiti nel cloud
Per modificare il dominio di un account utente esistente:

1. Aprire il portale di Azure classico usando un account amministratore globale o amministratore utenti.
2. Aprire la directory.
3. Selezionare la scheda **Utenti** ,
4. Selezionare l'utente dall'elenco.
5. Modificare il dominio dell'utente e quindi selezionare **Salva**.

Questa operazione può essere eseguita anche usando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o l'[API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Selezionare un dominio personalizzato durante la creazione di un nuovo utente
1. Aprire il portale di Azure classico usando un account amministratore globale o amministratore utenti.
2. Aprire la directory.
3. Selezionare la scheda **Utenti** ,
4. Sulla barra dei comandi selezionare **Aggiungi**.
5. Quando si aggiunge il nome utente, scegliere il dominio personalizzato dall'elenco di domini.
6. Selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
* [Uso di nomi di dominio personalizzati per semplificare l'esperienza di accesso degli utenti](active-directory-add-domain.md)
* [Gestire i nomi di dominio personalizzati](active-directory-add-manage-domain-names.md)
* [Informazioni sui concetti relativi alla gestione dei domini in Azure AD](active-directory-add-domain-concepts.md)

