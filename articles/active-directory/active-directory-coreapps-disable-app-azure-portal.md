---
title: aaaDisable accessi degli utenti per un'applicazione aziendale in Azure Active Directory | Documenti Microsoft
description: Come toodisable un'applicazione aziendale in modo che nessun utente possono accedere tooit in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Disabilitare gli accessi utente per un'app aziendale in Azure Active Directory
È facile toodisable un'applicazione aziendale in modo che nessun utente possono accedere tooit in Azure Active Directory (Azure AD). È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.

## <a name="how-do-i-disable-user-sign-ins"></a>Come è possibile disabilitare l'accesso degli utenti?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.
3. In hello **Azure Active Directory** -  ***nomedirectory*** blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **leapplicazioniaziendali**.

    ![Apertura di app aziendali](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**. Viene visualizzato un elenco di App hello che è possibile gestire.
5. In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.
6. In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **proprietà**.

    ![Selezione di hello tutti i comandi di applicazioni](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. In hello ***appname*** - **proprietà** pannello seleziona **n** per **abilitato per gli utenti toosign?**.
8. Seleziona hello **salvare** comando.

## <a name="next-steps"></a>Passaggi successivi
* [Visualizzare tutti i gruppi personali](active-directory-groups-view-azure-portal.md)
* [Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)
* [Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Modificare il nome di hello o logo di un'applicazione aziendale](active-directory-coreapps-change-app-logo-user-azure-portal.md)
