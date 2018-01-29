---
title: Modificare il nome o il logo di un'app aziendale in Azure Active Directory | Microsoft Docs
description: Come modificare il nome o il logo di un'app aziendale personalizzata in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: curtand
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: 2a1420b3f41ccc435ca128f003bcc23899a284c5
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a>Modificare il nome o il logo di un'app aziendale in Azure Active Directory
Modificare il nome o il logo per un'applicazione aziendale personalizzata in Azure Active Directory (Azure AD) è un'operazione facile. È necessario disporre delle autorizzazioni appropriate per apportare queste modifiche ed essere l'autore dell'app personalizzata.

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a>Come è possibile modificare il nome o il logo di un'app aziendale?
1. Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.
2. Selezionare **Altri servizi**, immettere **Azure Active Directory** nella casella di testo e quindi selezionare **Invio**.
3. Nel pannello **Azure Active Directory - *nomedirectory*** vale a dire il pannello Azure AD per la directory che si sta gestendo, selezionare **Applicazioni aziendali**.

    ![Apertura di app aziendali](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. Nel pannello **Applicazioni aziendali** selezionare **Tutte le applicazioni**. Verrà visualizzato un elenco di app che è possibile gestire.
5. Nel pannello **Applicazioni aziendali - All applications** (Tutte le applicazioni) selezionare un'app.
6. Nel pannello ***nomeapp***, vale a dire il pannello con il nome dell'app selezionata nel titolo, selezionare **Proprietà**.

    ![Selezione del comando Proprietà](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. Nel pannello ***nome app*** **- Proprietà** cercare un file da usare come nuovo logo, modificare il nome dell'app o eseguire entrambe le operazioni.

    ![Modifica del logo dell'app o del comando nameproperties](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. Selezionare il comando **Salva** .

## <a name="next-steps"></a>Passaggi successivi
* [Visualizzare tutti i gruppi personali](active-directory-groups-view-azure-portal.md)
* [Assegnare un utente o gruppo a un'app aziendale](active-directory-coreapps-assign-user-azure-portal.md)
* [Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Disabilitare l'accesso degli utenti per un'app aziendale](active-directory-coreapps-disable-app-azure-portal.md)
