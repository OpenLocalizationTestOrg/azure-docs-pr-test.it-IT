---
title: aaaHow tooactivate o disattivare un ruolo | Documenti Microsoft
description: Informazioni su come tooactivate ruoli per privileged Identity con un'applicazione hello Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Come tooactivate o disattivare i ruoli in Azure AD Privileged Identity Management
Gestione di identità con privilegi di Azure Active Directory (AD) semplifica la modalità di gestione di aziende tooresources di accesso con privilegi in Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.  

Se sono state apportate idoneo per un ruolo amministrativo, significa che è possibile attivare il ruolo quando è necessario azioni tooperform con privilegi. Se ad esempio si gestiscono occasionalmente le funzionalità di Office 365, è possibile che gli amministratori dei ruoli con privilegi dell'organizzazione non configurino l'utente come amministratore globale permanente perché tale ruolo interessa anche altri servizi. L'utente è invece considerato idoneo per ruoli di Azure AD, ad esempio amministratore di Exchange Online. È possibile richiedere tooactivate tale ruolo quando sono necessari relativi privilegi, e quindi sarà necessario controllo dell'amministratore per un periodo di tempo predeterminato.

Questo articolo è per gli amministratori che devono tooactivate proprio ruolo in Azure AD Privileged Identity Management (PIM). Illustra hello passaggi tooactivate un ruolo quando è necessario disporre delle autorizzazioni hello e disattivare il ruolo di hello al termine. Inoltre, gli amministratori di ruolo con privilegi possono richiedere l'approvazione tooactivate un ruolo (anteprima). Altre informazioni sui [Flussi di lavoro di approvazione di PIM](./privileged-identity-management/azure-ad-pim-approval-workflow.md).

## <a name="add-hello-privileged-identity-management-application"></a>Aggiungere un'applicazione hello Privileged Identity Management
Utilizzare un'applicazione hello Azure AD Privileged Identity Management hello [portale di Azure](https://portal.azure.com/) toorequest attivazione di un ruolo, anche se si ha intenzione di toooperate in un altro portale o PowerShell. Se non si dispone di un'applicazione hello Azure AD Privileged Identity Management nel portale di Azure, seguire questi passaggi tooget avviato.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure e selezionare hello directory in cui sarà necessario essere operativo.
3. Selezionare **più servizi** e utilizzare hello filtro textbox toosearch per **Azure AD Privileged Identity Management**.
4. Controllare **Pin toodashboard** e quindi fare clic su **crea**. verrà visualizzata la finestra di Hello applicazione Privileged Identity Management.

## <a name="activate-a-role"></a>Attivare un ruolo
Quando è necessario tootake in un ruolo, è possibile richiedere l'attivazione selezionando hello **ruoli personali** colonna di navigazione a sinistra dell'opzione di navigazione in un'applicazione hello Azure AD Privileged Identity Management.

1. Accedi toohello [portale di Azure](https://portal.azure.com/) e selezionare hello Azure AD Privileged Identity Management.
2. Selezionare **Ruoli personali**. Nel raggruppamento nella parte superiore di hello della pagina hello hello è visualizzato un elenco dei ruoli assegnati idonei.
3. Selezionare un ruolo tooactivate.
4. Selezionare **Attiva**. Hello **richiedere l'attivazione di ruolo** pannello viene visualizzato.
5. Alcuni ruoli richiedono l'autenticazione a più fattori (MFA) prima di poter attivare il ruolo di hello. È sufficiente tooauthenticate una volta per sessione.
   
    ![Schermata Verifica con MFA prima dell'attivazione del ruolo][2]
6. Immettere il motivo di hello per la richiesta di attivazione hello nel campo di testo hello.  Alcuni ruoli richiedono toosupply un numero di ticket problemi.
7. Selezionare **OK**.  Se il ruolo di hello non richiedono l'approvazione, viene ora attivato e ruolo hello viene visualizzato nell'elenco di hello i ruoli attivi (direttamente sotto l'elenco di hello di assegnazioni di ruolo idonei). Se hello [ruolo richiede l'approvazione](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, una notifica di tipo avviso popup verrà visualizzata brevemente in hello nell'angolo superiore destro del browser per informare l'utente hello richiesta è in attesa di approvazione.

    ![Notifica di richiesta in sospeso - schermata][3]

## <a name="deactivate-a-role"></a>Disattivare un ruolo
Un ruolo attivato si disattiva automaticamente quando viene raggiunto il limite di tempo (durata idonea).

Dopo aver completato le attività di amministrazione in anticipo, è possibile disattivare un ruolo applicazione Azure AD Privileged Identity Management hello manualmente.  Selezionare **ruoli personali**, scegliere il ruolo di hello termine tramite da hello **le assegnazioni di ruolo Active** raggruppamento e selezionare **disattiva**.  

## <a name="cancel-a-pending-request"></a>Annullare una richiesta in sospeso
In caso di hello non richiedono l'attivazione di un ruolo che richiede l'approvazione, è possibile annullare una richiesta in sospeso in qualsiasi momento. È sufficiente seleziona hello **ruoli personali** colonna di navigazione a sinistra dell'opzione di navigazione in un'applicazione hello Azure AD Privileged Identity Management.

1. Accedi toohello [portale di Azure](https://portal.azure.com/) e selezionare hello Azure AD Privileged Identity Management.
2. Selezionare **Ruoli personali**. Nel raggruppamento nella parte superiore di hello della pagina hello hello è visualizzato un elenco dei ruoli assegnati idonei.
3. Selezionare un ruolo.
4. Seleziona hello **l'attivazione è in attesa di approvazione** intestazione nel pannello dettagli di hello ruolo attivazione.
5. Selezionare **Annulla** nella parte superiore di hello di hello **in attesa di approvazione** blade.

   ![Annullare la richiesta in sospeso - schermata][4]

## <a name="next-steps"></a>Passaggi successivi
Se si è interessati a ottenere maggiori su Azure AD Privileged Identity Management, hello collegamenti seguenti ulteriori informazioni sono disponibili.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
