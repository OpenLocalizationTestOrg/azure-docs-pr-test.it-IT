---
title: Assegnare un utente ai ruoli di amministratore in Azure Active Directory | Microsoft Docs
description: Illustra come cambiare le informazioni amministrative in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/08/2018
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: dcb52e9de98d881474007410f3db599682e151ce
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a>Assegnare un utente ai ruoli di amministratore in Azure Active Directory
Questo articolo descrive come assegnare un ruolo di amministratore a un utente in Azure Active Directory (Azure AD). Per informazioni sull'aggiunta di nuovi utenti nell'organizzazione, vedere [Aggiungere nuovi utenti ad Azure Active Directory](active-directory-users-create-azure-portal.md). Gli utenti aggiunti non hanno autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare loro dei ruoli in qualsiasi momento.

## <a name="assign-a-role-to-a-user"></a>Assegnare un ruolo a un utente
1. Accedere all'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) con un account amministratore globale per la directory.
2. Selezionare **Utenti e gruppi**.

   ![Apertura di Gestione utenti](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. Selezionare **Tutti gli utenti**.
  
  ![Apertura del gruppo Tutti gli utenti](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. Selezionare un utente dall'elenco.
5. Per l'utente scelto selezionare **Ruolo della directory** e quindi assegnare l'utente a un ruolo nell'elenco **Ruolo della directory**. Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).

      ![Assegnazione di un utente a un ruolo](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. Selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
* [Avvio rapido: Aggiungere o eliminare utenti in Azure Active Directory](add-users-azure-active-directory.md)
* [Gestire i profili utente](active-directory-users-profile-azure-portal.md)
* [Aggiungere utenti guest da un'altra directory](active-directory-b2b-what-is-azure-ad-b2b.md) 
* [Assegnare un utente a un ruolo in Azure AD](active-directory-users-assign-role-azure-portal.md)
* [Ripristinare un utente eliminato](active-directory-users-restore.md)
