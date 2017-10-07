---
title: 'Azure AD Connect: Passaggi successivi e in che modo Azure AD Connect toomanage | Documenti Microsoft'
description: "Informazioni su come tooextend hello configurazione predefinita e le attività operative per Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Passaggi successivi e come toomanage Azure AD Connect
Utilizzare le procedure operative hello in toomeet di Connect di Azure Active Directory (Azure AD) toocustomize questo articolo esigenze dell'organizzazione e ai requisiti.  

## <a name="add-additional-sync-admins"></a>Aggiungere altri amministratori di sincronizzazione
Per impostazione predefinita, solo gli utenti hello hello amministratori locali e installazione sono in grado di toomanage motore di sincronizzazione hello installato. Per altre persone toobe in grado di tooaccess e gestire il motore di sincronizzazione di hello, individuare il gruppo di hello denominato ADSyncAdmins nel server locale hello e aggiungerli toothis gruppo.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Assegnare licenze tooAzure agli utenti di Active Directory Premium ed Enterprise Mobility Suite
Ora che gli utenti sono stati sincronizzati toohello cloud, è necessario tooassign loro una licenza, pertanto è possibile procedere con le app cloud, ad esempio Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign una Azure AD Premium o Enterprise Mobility Suite di licenza

1. Accedi toohello portale di Azure come amministratore.
2. A sinistra di hello, selezionare **Active Directory**.
3. In hello **Active Directory** pagina, fare doppio clic sulla directory hello con gli utenti di hello si desidera ripristinare tooset.
4. Nella parte superiore di hello della pagina directory hello, selezionare **licenze**.
5. In hello **licenze** selezionare **Active Directory Premium** o **Enterprise Mobility Suite**, quindi fare clic su **assegnare**.
6. Nella finestra di dialogo hello selezionare utenti di hello desiderati tooassign licenze per e quindi fare clic su hello segno di spunta icona toosave hello verrà modificata.

## <a name="verify-hello-scheduled-synchronization-task"></a>Verificare l'attività di sincronizzazione pianificato hello
Utilizzare hello toocheck portale Azure hello stato di una sincronizzazione.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>attività di sincronizzazione pianificata hello tooverify
1. Accedi toohello portale di Azure come amministratore.
2. A sinistra di hello, selezionare **Active Directory**.
3. In hello **Active Directory** pagina, fare doppio clic sulla directory hello con gli utenti di hello si desidera ripristinare tooset.
4. Nella parte superiore di hello della pagina directory hello, selezionare **integrazione Directory**.
5. In **integrazione con active directory locale**, hello nota ora dell'ultima sincronizzazione.

<center>![Ora sincronizzazione directory](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Avviare un'attività di sincronizzazione pianificata
Se è necessario toorun un'attività di sincronizzazione, è possibile farlo eseguendo nuovamente tramite procedura guidata di Azure AD Connect hello.  È necessario tooprovide le credenziali di Azure AD.  Nella procedura guidata hello, selezionare hello **personalizzare le opzioni di sincronizzazione** attività e fare clic su **Avanti** toomove guidata hello. Al fine di hello, verificare che hello **avviare il processo di sincronizzazione di hello appena viene completata la configurazione iniziale di hello** casella è selezionata.

<center>![Avviare la sincronizzazione](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Per ulteriori informazioni sulla sincronizzazione di hello Azure AD Connect dell'utilità di pianificazione, vedere [pianificazione di connettersi AD Azure](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Attività aggiuntive disponibili in Azure AD Connect
Dopo l'installazione iniziale di Azure AD Connect, è possibile sempre avviare la procedura guidata hello nuovamente da hello Azure AD Connect inizio pagina o desktop scelta rapida.  Si noterà che attraversa nuovamente la procedura guidata hello sono disponibili alcune nuove opzioni sotto forma di hello di attività aggiuntive.  

Hello nella tabella seguente fornisce un riepilogo di queste attività e una breve descrizione di ogni attività.

![Elenco delle attività aggiuntive](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Attività aggiuntive | Descrizione |
| --- | --- |
| **Scenario di visualizzazione hello selezionato** |Consente di visualizzare la soluzione Azure AD Connect corrente.  Include impostazioni generali, directory sincronizzate e impostazioni di sincronizzazione. |
| **Personalizzazione delle opzioni di sincronizzazione** |Modifica della configurazione corrente di hello quali l'aggiunta di ulteriore configurazione toohello foreste di Active Directory, o l'attivazione di opzioni di sincronizzazione, ad esempio utente, gruppo, dispositivi o write-back password. |
| **Abilitazione modalità di gestione temporanea** |Informazioni relative alla fase non viene sincronizzate immediatamente e non esportati tooAzure Active Directory o Active Directory locale.  Con questa funzionalità, è possibile visualizzare in anteprima le sincronizzazioni hello prima che si verifichino. |

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
