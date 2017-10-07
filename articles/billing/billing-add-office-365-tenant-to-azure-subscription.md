---
title: tenant di Office 365 aaaUse con una sottoscrizione di Azure | Documenti Microsoft
description: Informazioni su come Office 365 tooadd directory (tenant) tooan sottoscrizione di Azure.
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Associare un tooan tenant di Office 365 sottoscrizione di Azure
Collegare le sottoscrizioni di Azure e Office 365 separate in modo che è possibile accedere a tenant di Office 365 hello dalla sottoscrizione di Azure. toolink delle sottoscrizioni, accedi tooAzure con hello account amministratore del servizio di Azure, aggiungere una directory e aggiungere il tenant di Azure Active Directory toohello account aziendali hello Office 365.

Se si desidera una sottoscrizione di Office 365 per gli utenti nell'istanza di Azure Active Directory o si dispone di un account Office 365 ma non di un account Azure, vedere [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md) (Iscriversi ad Azure con un account Office 365). 

## <a name="before-you-begin"></a>Prima di iniziare
* È necessario disporre delle credenziali hello dell'amministratore del servizio hello sottoscrizione di Azure. Account di coamministratore non può eseguire alcuni passaggi hello in questo articolo. toochange l'amministratore del servizio, vedere [come tooadd o modificare i ruoli di amministratore di Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* È necessario disporre di credenziali di hello di un amministratore globale del tenant di Office 365 hello.
* indirizzo di posta elettronica Hello del messaggio per l'amministratore del servizio non deve essere nel tenant di Office 365 hello.
* indirizzo di posta elettronica Hello del messaggio per l'amministratore del servizio deve corrisponde a quello di qualsiasi amministratore globale del tenant di Office 365 hello.
* Se si utilizza un indirizzo di posta elettronica che è un account Microsoft sia un account aziendale, modificare temporaneamente amministratore del servizio hello di toouse la sottoscrizione di Azure un altro account Microsoft. È possibile creare un account Microsoft in hello [pagina account Microsoft](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Collegamento sottoscrizione tooAzure tenant di Office 365
toohello tenant di Office 365 hello tooassociate sottoscrizione di Azure, seguire questi passaggi:

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Passaggio 1: Aggiungere tooyour tenant di Office 365 sottoscrizione di Azure

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con le credenziali di amministratore hello.

    ![Screenshot dell'accesso ad Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Nel riquadro sinistro hello selezionare **ACTIVE DIRECTORY**. Non deve vedrai tenant hello Office 365. Se è visibile, andare troppo[passaggio 2: impostare la directory hello associata a una sottoscrizione di Azure hello](#Step2).
   
   ![Screenshot della voce di Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Selezionare **NUOVA** > **DIRECTORY** > **CREAZIONE PERSONALIZZATA**.
   
    ![Screenshot di Creazione personalizzata di Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. In hello **Aggiungi directory** pagina **DIRECTORY**selezionare **utilizza directory esistente**. Selezionare quindi **sono pronti toobe uscire ora**e selezionare **completa** ![icona completare](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Screenshot di "Utilizza directory esistente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Dopo essere disconnessi, accedere con le credenziali dell'amministratore di hello globale del tenant Office 365.
   
    ![Screenshot dell'accesso come amministratore globale di Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Selezionare **Continua**.
   
    ![Screenshot della verifica](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Selezionare **Esci ora**.
   
    ![Screenshot della disconnessione](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con le credenziali di amministratore hello.
   
    ![Screenshot dell'accesso ad Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Verrà visualizzato il tenant di Office 365 in dashboard hello.
   
    ![Screenshot del dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Passaggio 2: Impostare la directory hello associato hello sottoscrizione di Azure
   
1. Selezionare **Impostazioni**.
   
    ![Screenshot dell'icona delle impostazioni del portale classico di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Selezionare la sottoscrizione di Azure e quindi **MODIFICA DIRECTORY**.

    ![Screenshot di Modifica directory per la sottoscrizione di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Selezionare **Avanti** ![icona Avanti](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Schermata di "Modifica hello associate nella directory"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Esaminare gli account hello interessata. Tutti i coamministratori e [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) gli utenti con accesso assegnato in gruppi di risorse esistente hello vengono rimossi. avviso Hello ricevuto menziona solo la rimozione di hello dei coamministratori.
      
    ![Schermata che mostra hello account coamministratore toobe rimosso.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermata che mostra un toobe di account utente di esempio è stato rimosso.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Selezionare **Completa** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Passaggio 3: Aggiungere gli account aziendali di Office 365 come tenant di Azure Active Directory toohello coamministratori
   
1. Seleziona hello **amministratori** scheda e quindi selezionare **aggiungere**.
   
    ![Screenshot della scheda Amministratori relativa alle impostazioni nel portale di Azure classico](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Immettere un account aziendale di tenant di Office 365, selezionare hello sottoscrizione di Azure, quindi **completa** ![icona completare](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Screenshot della finestra di dialogo Aggiungi coamministratore di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Tornare indietro toohello **amministratori** scheda. Dovrebbe essere visualizzato come co-amministratore account aziendale di hello.
   
    ![Screenshot della scheda Amministratori](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Test tooAzure di accesso con account di coamministratore hello.
   
    a. Uscire da hello portale di Azure classico.
   
    b. Aprire hello [portale di Azure](https://portal.azure.com/).
   
    c. Immettere le credenziali di hello di CO-amministratore hello e quindi selezionare **Accedi**.
   
    ![Screenshot della pagina di accesso di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.


