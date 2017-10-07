---
title: aaaGet avviato con Azure AD Privileged Identity Management | Documenti Microsoft
description: "Informazioni su come toomanage con privilegi di identità con un'applicazione hello Azure Active Directory Privileged Identity Management nel portale di Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Iniziare ad usare Azure AD Privileged Identity Management
Con Azure Active Directory (AD) Privileged Identity Management è possibile gestire, il controllo e monitorare l'accesso all'interno dell'organizzazione. Questo ambito include tooresources di accesso di Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.

In questo articolo indica come tooadd hello tooyour app di Azure AD PIM dashboard del portale di Azure.

## <a name="add-hello-privileged-identity-management-application"></a>Aggiungere un'applicazione hello Privileged Identity Management
Prima di usare Azure AD Privileged Identity Management, è necessario tooadd hello applicazione tooyour dashboard del portale di Azure.

1. Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore globale della directory.
2. Se l'organizzazione dispone di più di una directory, selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure. Selezionare la directory di hello in cui si desidera toouse PIM.
3. Selezionare **più servizi** e utilizzare hello filtro textbox toosearch per **Azure AD Privileged Identity Management**.
4. Controllare **Pin toodashboard** e quindi fare clic su **crea**. verrà visualizzata la finestra di Hello applicazione Privileged Identity Management.

Se si sta hello prima persona toouse Azure AD Privileged Identity Management nella directory, vengono assegnati automaticamente hello **amministratore della sicurezza** e **amministratore del ruolo con privilegi** ruoli nella directory hello. Solo gli amministratori del ruolo con privilegi possono gestire le assegnazioni di ruoli degli utenti. Inoltre, è possibile scegliere hello toorun [guidata impostazioni di sicurezza.](active-directory-privileged-identity-management-security-wizard.md) che vengono illustrati l'esperienza di individuazione e assegnazione iniziale hello.

## <a name="navigate-tooyour-tasks"></a>Passare tooyour attività
Una volta configurato, Azure AD Privileged Identity Management vedrai il pannello di navigazione hello ogni volta che si apre un'applicazione hello. Utilizzare questo tooaccomplish blade le attività di gestione di identità.

![Attività principali per PIM - Screenshot](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Ruoli personali** consente di passare tooa elenco dei ruoli assegnati tooyou. In questa sezione è possibile attivare i ruoli per cui si è idonei.
* **Approva richieste (anteprima)** visualizza un elenco di richieste di attivazione in sospeso dagli utenti della directory. [Altre informazioni.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **(Anteprima) richieste in sospeso** consente di visualizzare qualsiasi corrente tooactivate toohave effettuate le richieste.
* **Controllare l'accesso** accetta tooany in sospeso accesso esamina toocomplete, è necessario se si sta esaminando l'accesso per se stessi o un altro utente.
* **I ruoli della Directory Azure AD** disponibile nella sezione 'Gestisci' hello è dashboard hello per le assegnazioni di ruolo con privilegi amministratori toomanage ruolo, modifica impostazioni di attivazione di ruolo, avvio accesso revisioni e altro ancora. opzioni di Hello in questo dashboard sono disabilitate per tutti gli utenti che non è un ruolo con privilegi di amministratore.

## <a name="next-steps"></a>Passaggi successivi
Hello [Panoramica di Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) include ulteriori dettagli su come è possibile gestire l'accesso amministrativo all'interno dell'organizzazione.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
