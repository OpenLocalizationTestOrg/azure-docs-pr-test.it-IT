---
title: aaaSign iscrizione a Office 365 con account di Azure | Documenti Microsoft
description: Informazioni su come Office 365 toocreate sottoscrizione utilizzando un account di Azure
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Iscriversi a un abbonamento a Office 365 con il proprio account Azure
Se si ha una sottoscrizione Azure, è possibile utilizzare toosign l'account di Azure per una sottoscrizione Office 365. Se si fa parte di un'organizzazione che dispone di una sottoscrizione di Azure, è possibile creare abbonamenti a Office 365 per gli utenti nell'istanza esistente di Azure Active Directory (Azure AD). Effettuare l'iscrizione tooOffice 365 utilizzando un account che disponga delle autorizzazioni di amministratore globale o amministratore fatturazione nel tenant di Azure Active Directory. Per altre informazioni, vedere [Controllare le autorizzazioni dell'account in Azure AD](#RoleInAzureAD) e [Assegnazione dei ruoli di amministratore in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

Se si dispone già di un account Office 365 sia una sottoscrizione di Azure, è possibile [associare un tooan tenant di Office 365 sottoscrizione di Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Ottenere un abbonamento a Office 365 tramite il proprio account Azure

1. Passare toohello [pagina prodotto Office 365](https://products.office.com/business)e selezionare un piano.
2. Fare clic su **Accedi** nell'angolo superiore destro di hello della pagina hello.

    ![screenshot della pagina della versione di valutazione di Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Accedere con le credenziali dell'account Azure. Se si crea una sottoscrizione per l'organizzazione, utilizzare un account di Azure è un membro del ruolo di directory di amministratore globale o amministratore fatturazione hello nel tenant di Azure Active Directory.

    ![Screenshot della pagina di accesso a Office 365](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Fare clic su **Prova adesso**.

    ![Screenshot di conferma dell'ordine per Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. Nella pagina di conferma ordine hello, fare clic su **continua**.

    ![Schermata di conferma ordine hello Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Le impostazioni sono state completate. Se si crea sottoscrizione hello Office 365 per l'organizzazione, utilizzare hello seguente toocheck passaggi che gli utenti di Azure AD sono ora in Office 365.

1. Aprire Centro di amministrazione di Office 365 hello.
2. Espandere **UTENTI** e quindi fare clic su **Utenti attivi**.

    ![Schermata di utenti di centro di amministrazione hello Office 365](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Dopo l'iscrizione, hello abbonamento a Office 365 viene aggiunta toohello stessa istanza di Azure Active Directory che appartiene alla sottoscrizione di Azure. Per altre informazioni, vedere [Altre informazioni su sottoscrizioni di Azure e abbonamenti a Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) e [Associare le sottoscrizioni di Azure ad Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Controllare le autorizzazioni dell'account Microsoft in Azure AD
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **Altri servizi** e quindi cercare **Active Directory**.

    ![Schermata di Active Directory nel portale di Azure hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Fare clic su **Utenti e gruppi** > **Tutti gli utenti**.
4. Selezionare il nome di utente hello. 

    ![Schermata che mostra gli utenti di Azure Active Directory hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Fare clic su **Ruolo directory**.
  
    ![Schermata che illustra il ruolo di directory del portale Azure hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  ruolo Hello **amministratore globale** o **amministratori con autorizzazioni limitate** > **amministratore fatturazione** è toocreate necessario un abbonamento a Office 365 per gli utenti in ambiente Azure Active Directory esistente.

    ![Screenshot che mostra il ruolo di directory del portale di Azure Amministratore fatturazione](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema. 
