---
title: Azure AD Privileged Identity Management aaaConfigure | Documenti Microsoft
description: "Un argomento che spiega che cos'è Azure AD Privileged Identity Management e come toouse PIM tooimprove la protezione del cloud."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Che cos'è Azure AD Privileged Identity Management?
Con Azure Active Directory (AD) Privileged Identity Management è possibile gestire, il controllo e monitorare l'accesso all'interno dell'organizzazione. Ciò include tooresources di accesso di Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.  

> [!NOTE]
> Quando gli amministratori con versione di hello P2 Premium di Azure Active Directory è una licenza, Privileged Identity Management è disponibile tooyour intera organizzazione. Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).

Le organizzazioni desidera che il numero di hello toominimize di persone che hanno accesso toosecure informazioni o risorse, in quanto che riduce le possibilità di hello di un utente malintenzionato di accedere. Tuttavia, gli utenti devono comunque toocarry operazioni privilegiate nelle app di Azure, Office 365 o SaaS. Le organizzazioni assegnano agli utenti l'accesso con privilegi in Azure AD senza monitorare le attività svolte con i privilegi amministrativi. Azure AD Privileged Identity Management consente tooresolve questo rischio.  

Azure AD Privileged Identity Management consente di effettuare le operazioni seguenti:  

* Individuare gli utenti amministratori di Azure AD
* Abilitare le connessioni, "just in time" accesso amministrativo tooMicrosoft Online Services quali Office 365 e Intune
* Ottenere report sulla cronologia degli accessi degli amministratori e sulle modifiche alle assegnazioni degli amministratori
* Ottenere avvisi relativi al ruolo con privilegi di accesso tooa
* Richiedi approvazione tooactivate (anteprima)

Azure AD Privileged Identity Management è possibile gestire i ruoli dell'organizzazione di hello incorporato Azure AD, inclusi (ma non è limitato a):  

* Amministratore globale
* Amministratore fatturazione
* Amministratore del servizio  
* Amministratore utenti
* Amministratore password

## <a name="just-in-time-administrator-access"></a>Accesso amministratore just-in-time
In passato, è possibile assegnare un ruolo di amministratore utente tooan tramite hello portale di Azure classico o Windows PowerShell. Di conseguenza, tale utente diventa un **amministratore permanente**, sempre attiva nel ruolo hello assegnato. Azure AD Privileged Identity Management è stato introdotto il concetto di hello di un **admin idonei**. Gli amministratori idonei devono essere utenti che necessitano dell'accesso con privilegi in modo occasionale, non con cadenza quotidiana. ruolo Hello è inattivo fino a quando l'utente hello richiede l'accesso, quindi il completamento di un processo di attivazione e diventare amministratore attivo per un periodo di tempo prestabilito.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Abilitare Privileged Identity Management per la directory
Iniziare a usare Azure AD Privileged Identity Management nel hello [portale di Azure](https://portal.azure.com/).

> [!NOTE]
> È necessario essere un amministratore globale con un account aziendale (ad esempio, @yourdomain.com), non un account Microsoft (ad esempio, @outlook.com), tooenable Azure AD Privileged Identity Management per una directory.

1. Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore globale della directory.
2. Se l'organizzazione dispone di più di una directory, selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure. Selezionare la directory di hello in cui si userà Azure AD Privileged Identity Management.
3. Selezionare **più servizi** e utilizzare hello filtro textbox toosearch per **Azure AD Privileged Identity Management**.
4. Controllare **Pin toodashboard** e quindi fare clic su **crea**. verrà visualizzata la finestra di Hello applicazione Privileged Identity Management.

Se si sta hello prima persona toouse Azure AD Privileged Identity Management nella directory, hello [guidata impostazioni di sicurezza](active-directory-privileged-identity-management-security-wizard.md) illustra esperienza iniziale assegnazione hello. Dopo che diventa automaticamente anche hello innanzitutto **amministratore della sicurezza** e **amministratore del ruolo con privilegi** della directory hello.

Solo l'amministratore dei ruoli con privilegi può gestire l'accesso per gli altri amministratori. È possibile [assegna toomanage di possibilità hello altri utenti nelle PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Dashboard amministratore di Privileged Identity Management
In Azure AD Privileged Identity Management è disponibile un dashboard dell'amministratore che visualizza informazioni importanti, tra cui:

* Avvisi che segnalano sicurezza tooimprove opportunità
* numero di Hello degli utenti viene assegnato il ruolo con privilegi di tooeach  
* numero di Hello del gruppo amministratori idonei e permanenti
* Un grafo di attivazioni del ruolo con privilegi nella directory

![Dashboard PIM - Schermata][2]

## <a name="privileged-role-management"></a>Gestione dei ruoli con privilegi
Con Azure AD Privileged Identity Management, è possibile gestire gli amministratori di hello aggiungendo o rimuovendo ruolo tooeach amministratori permanenti o idoneo.

![Aggiunta/Rimozione di amministratori PIM - Schermata][3]

## <a name="configure-hello-role-activation-settings"></a>Configurare le impostazioni di attivazione di hello ruolo
Utilizzando hello [le impostazioni del ruolo](active-directory-privileged-identity-management-how-to-change-default-settings.md) è possibile configurare proprietà di attivazione ruolo idonei hello tra cui:

* durata Hello del periodo di attivazione di hello ruolo
* notifica di attivazione del ruolo Hello
* informazioni di Hello un utente devono tooprovide durante il processo di attivazione del ruolo hello
* Ticket di servizio o numero dell'evento imprevisto
* [Requisiti del flusso di lavoro di approvazione - Anteprima](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Impostazioni di PIM - Attivazione dell'amministratore - Schermata][4]

Si noti che nell'immagine di hello, hello pulsanti che consentono di **multi-Factor Authentication** sono disabilitati. Per determinati ruoli con privilegi elevati, è necessaria l'autenticazione MFA per una protezione avanzata.

## <a name="role-activation"></a>Attivazione del ruolo
troppo[attivare un ruolo](active-directory-privileged-identity-management-how-to-activate-role.md), un amministratore idoneo richiede una scadenza "attivazione" per il ruolo di hello. attivazione di Hello può essere richieste mediante hello **attivare il ruolo** opzione in Azure AD Privileged Identity Management.

Un amministratore che desidera tooactivate un ruolo deve tooinitialize Azure AD Privileged Identity Management nel portale di Azure hello.

L'attivazione del ruolo è personalizzabile. Nelle impostazioni di PIM hello, è possibile determinare la lunghezza hello dell'attivazione hello e quali salve informazioni ruolo di hello tooactivate tooprovide.

![Richiesta di attivazione del ruolo dell'amministratore PIM - Schermata][5]

## <a name="review-role-activity"></a>Verificare l'attività del ruolo
Esistono due modi tootrack utilizzano dipendenti e gli amministratori con privilegi di ruoli. utilizza prima opzione Hello [cronologia controlli ruoli della Directory](active-directory-privileged-identity-management-how-to-use-audit-log.md). cronologia controlli Hello registra il rilevamento delle modifiche nelle assegnazioni di ruolo con privilegi e della cronologia di attivazione di ruolo.

![Cronologia di attivazione PIM - Schermata][6]

seconda opzione Hello è tooset backup regolari [accedere revisioni](active-directory-privileged-identity-management-how-to-start-security-review.md). Questi controlli di accesso possono essere eseguiti da e assegnati revisore (ad esempio, un team di gestione) o dipendenti hello è possono esaminare se stessi. Si tratta di hello migliore modo toomonitor che richiede comunque l'accesso e che non esegue più.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM alla scadenza della sottoscrizione
Controlla il precedente tooreaching generale disponibilità PIM AD Azure è stato in anteprima e si sono verificati alcuna licenza toopreview un tenant Azure AD PIM.  Ora che Azure AD PIM ha raggiunto la disponibilità generale, le licenze di valutazione o a pagamento devono essere assegnate toohello gli amministratori di hello tenant toocontinue usare PIM.  Se l'organizzazione non acquistare Azure AD Premium P2 o la versione di valutazione scade, principalmente tutte le funzionalità di Azure AD PIM hello non saranno disponibili nel tenant.  È possibile leggere altre in hello [requisiti di sottoscrizione di Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
