---
title: aaaHow tooperform una revisione accesso | Documenti Microsoft
description: Informazioni su come tooperform una revisione con hello applicazione Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Come tooperform esaminare un accesso in Azure AD Privileged Identity Management
Gestione di identità con privilegi di Azure Active Directory (AD) semplifica la modalità di gestione di aziende tooresources di accesso con privilegi in Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.  

Se si sono assegnati ruoli amministrativi tooan, l'amministratore del ruolo con privilegi potrebbe essere richiesto tooregularly confermare che è necessario tale ruolo per il processo. È possibile che venga visualizzato un messaggio di posta elettronica che include un collegamento oppure è possibile passare retta toohello [portale di Azure](https://portal.azure.com). Seguire i passaggi di hello in questo articolo di tooperform esaminare automatica dei ruoli assegnati.

Se si è un ruolo con privilegi di amministratore interessato revisioni di accesso, ottenere ulteriori dettagli in [come toostart un accesso esaminare](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Aggiungere un'applicazione hello Privileged Identity Management
È possibile utilizzare un'applicazione hello Azure AD Privileged Identity Management (PIM) in hello [portale di Azure](https://portal.azure.com/) tooperform la revisione.  Se non si dispone di un'applicazione hello Azure AD Privileged Identity Management nel portale, seguire questi passaggi tooget avviato.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure e selezionare hello directory in cui sarà necessario essere operativo.
3. Selezionare **più servizi** e utilizzare hello filtro textbox toosearch per **Azure AD Privileged Identity Management**.
4. Controllare **Pin toodashboard** e quindi fare clic su **crea**. verrà aperto Hello applicazione Privileged Identity Management.

## <a name="approve-or-deny-access"></a>Approvare o negare l'accesso
Quando si approvare o negare l'accesso, si sta indica semplicemente revisore hello se questo ruolo è comunque usare o non. Scegliere **Approva** se si desidera toostay nel ruolo hello o **Deny** se l'accesso non necessario hello più. Lo stato non cambia immediatamente, fino a quando il revisore hello applica risultati hello.
Seguire questi passaggi toofind e completare hello accesso revisione:

1. Nell'applicazione PIM hello, selezionare **accesso con privilegi di revisione**. Nel caso di eventuali revisioni in sospeso di accesso, vengono visualizzate in hello che Azure AD Access revisioni del pannello.
2. Selezionare una revisione hello desiderato toocomplete.
3. A meno che non è stata creata la revisione di hello, è visualizzato come hello solo utente in revisione hello. Selezionare il nome tooyour successivo di hello segno di spunta.
4. Scegliere **Approva** o **Nega**. Potrebbe essere necessario un motivo per la decisione in hello tooinclude **fornire un motivo** casella di testo.  
5. Chiude hello **ruoli di Azure AD verifica** blade.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
