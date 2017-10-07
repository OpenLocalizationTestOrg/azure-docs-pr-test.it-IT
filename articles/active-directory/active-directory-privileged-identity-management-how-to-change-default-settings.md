---
title: impostazioni di attivazione ruolo toomanage aaaHow | Documenti Microsoft
description: "Informazioni su come toochange hello le impostazioni predefinite per le identità con privilegi con hello estensione di Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Come impostazioni di attivazione toomanage ruolo in Azure AD Privileged Identity Management
Un amministratore con privilegi di ruolo è possibile personalizzare Azure AD Privileged Identity Management (PIM) nella propria organizzazione, inclusa la modifica esperienza hello per un utente che è l'attivazione di un'assegnazione di ruolo idoneo.

## <a name="manage-hello-role-activation-settings"></a>Gestire le impostazioni di attivazione di hello ruolo
1. Passare toohello [portale di Azure](https://portal.azure.com) e seleziona hello **Azure AD Privileged Identity Management** app dal dashboard hello.
2. Selezionare **Gestione dei ruoli con privilegi** > **Impostazioni** > **Ruoli con privilegi**.
3. Scegliere il ruolo di hello le cui impostazioni si desidera toomanage.

Nella pagina Impostazioni di hello per ogni ruolo, esistono una serie di impostazioni che è possibile configurare. Queste impostazioni incidono solo sugli utenti che sono amministratori idonei, non sugli amministratori permanenti.

**Le attivazioni**: tempo hello, espresso in ore, per cui un ruolo rimane attivo prima che scada. Questo valore può essere compreso tra 1 e 72 ore.

**Le notifiche**: È possibile scegliere se consentire o meno inviato dal sistema di hello tooadmins messaggi di posta elettronica conferma che è stato attivato un ruolo. Questa opzione può essere utile per il rilevamento di attivazioni non autorizzate o dannose.

**Evento imprevisto/richiesta Ticket**: È possibile scegliere se toorequire admins idonei tooinclude un ticket numero quando si attiva il proprio ruolo. Questa opzione può essere utile quando si eseguono i controlli di accesso dei ruoli.

**Multi-Factor Authentication**: È possibile o meno toorequire utenti tooverify la propria identità con autenticazione a più fattori prima di poter attivare i relativi ruoli. Hanno solo una volta per ogni sessione, non ogni volta che si attiva un ruolo tooverify. Esistono due suggerimenti tookeep presente quando si abilita l'autenticazione a più fattori:

* Gli utenti che dispongono di account Microsoft per gli indirizzi di posta elettronica (in genere @outlook.com, ma non sempre) non è possibile registrare per Azure MFA. Se si desidera tooassign ruoli toousers con account Microsoft, si deve renderli amministratori permanenti o disabilitare l'autenticazione a più fattori per tale ruolo.
* Non è possibile disabilitare l'autenticazione MFA per i ruoli con privilegi elevati per Azure AD e Office365. Si tratta di una funzionalità di sicurezza poiché è necessaria una protezione elevata per questi ruoli:  
  
  * Amministratore di applicazioni
  * Amministratore server proxy applicazione
  * Amministratore fatturazione  
  * Amministratore di conformità  
  * Amministratore del servizio CRM
  * Responsabile approvazione per l'accesso a Customer Lockbox
  * Ruolo con autorizzazioni di scrittura nella directory  
  * Amministratore di Exchange  
  * Amministratore globale
  * Amministratore del servizio Intune
  * Amministratore della cassetta postale  
  * Supporto partner - Livello 1  
  * Supporto partner - Livello 2  
  * Amministratore dei ruoli con privilegi   
  * Amministratore della sicurezza  
  * Amministratore di SharePoint  
  * Amministratore di Skype for Business  
  * Amministratore account utente  

Per ulteriori informazioni sull'utilizzo di autenticazione a più fattori con PIM vedere [come autenticazione a più fattori tooRequire](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

