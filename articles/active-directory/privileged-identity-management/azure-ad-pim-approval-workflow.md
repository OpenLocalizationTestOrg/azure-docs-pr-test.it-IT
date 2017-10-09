---
title: "flussi di lavoro di approvazione della gestione delle identità con privilegi aaaAzure | Documenti Microsoft"
description: Informazioni sui flussi di lavoro di approvazione di Privileged Identity Management (PIM)
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Approvazioni (Anteprima)

## <a name="overview"></a>Panoramica

Con approvazioni per Privileged Identity Management, è possibile configurare l'approvazione toorequire ruoli per l'attivazione e scegliere uno o più utenti o gruppi come delegati responsabili approvazione. Continuare a leggere toolearn come ruoli tooconfigure e selezionare i responsabili approvazione.

>[!NOTE]
Tenere presente che questa funzionalità è ancora in fase di sviluppo e che è possibile che si verifichino degli errori. funzionalità di Hello, incluso il testo e convenzioni di denominazione sono soggetti a modifiche e non deve essere considerati finale.


## <a name="key-terminology"></a>Terminologia chiave

*Idonei ruolo utente* : un utente idoneo ruolo è un utente all'interno dell'organizzazione che è stato assegnato il ruolo di Azure AD tooan come idonee (ruolo richiede un'attivazione).

*Delegated Approver (Responsabile approvazione con delega)*: un responsabile approvazione con delega è una o più persone o gruppo all’interno di Azure AD che sono responsabili dell’approvazione delle richieste di l’attivazione del ruolo.

## <a name="scenarios"></a>Scenari

Anteprima privata Hello supporta hello seguenti scenari:

**Come Amministratore dei ruoli con privilegi (PRA), è possibile:**

-   [Abilitare l’approvazione per ruoli specifici](#enable-approval-for-specific-roles)

-   [specificare richieste tooapprove utenti e/o gruppi di responsabile approvazione](#specify-approver-users-and/or-groups-to-approve-requests)

-   [Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi](#view-request-and-approval-history-for-all-privileged-roles)

**Come responsabile approvazione designato, è possibile:**

-   [Visualizzare le approvazioni (richieste) in sospeso](#view-pending-approvals-requests)

-   [Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [Fornire una giustificazione per l’approvazione/il rifiuto](#provide-justification-for-my-approval/rejection) 

**Come Eligible Role User (Utente con ruolo idoneo), è possibile:**

-   [Richiedere l’attivazione di un ruolo che richiede approvazione](#request-activation-of-a-role-that-requires-approval)

-   [visualizzare lo stato di hello di tooactivate la richiesta](#view-the-status-of-your-request-to-activate)

-   [Completare l’attività in Azure AD se l’attivazione è stata approvata](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Navigazione

Sono stati aggiornati approvazioni toosupport di navigazione hello

![](media/azure-ad-pim-approval-workflow/image001.png)

pagina di destinazione predefinita Hello fornisce un pratico accesso tooinformation su PIM e hello nuova documentazione approvazioni.

![](media/azure-ad-pim-approval-workflow/image002.png)

È stata aggiunta anche una nuova sezione per tutti gli utenti di PIM: ’My Audit History’ (Cronologia delle approvazioni personali). Qui è possibile trovare tutte le identità di tooyour rilevanti informazioni hello. Questo include tutte le richieste in sospeso e completate, le decisioni che relative al richieste hello è risolvere e tutte le attivazioni di ruoli precedenti in un'unica posizione.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Abilitare l’approvazione per ruoli specifici

approvazione tooenable per un ruolo specifico, selezionare innanzitutto i ruoli della Directory dal riquadro di spostamento sinistro hello.

![](media/azure-ad-pim-approval-workflow/image004.png)

Individuare e selezionare le impostazioni in hello spostamento a sinistra i ruoli della Directory

![](media/azure-ad-pim-approval-workflow/image006.png)

Selezionare i ruoli privilegiati:

![](media/azure-ad-pim-approval-workflow/image009.png)

Selezionare "Abilita" hello richiedono una sezione di approvazione:

![](media/azure-ad-pim-approval-workflow/image011.png)

Una volta abilitato, blade hello espanderà hello tooshow seguenti dettagli:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Se non si specifica tutti i revisori, hello PRA(s) diventano approvatori predefinito hello. PRA(s) sarebbe necessario tooapprove attivazione tutte le richieste per questo ruolo.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Specificare richieste tooapprove utenti e/o gruppi di responsabile approvazione

approvazione toodelegate, fare clic su hello opzione troppo "Select responsabili approvazione":

![](media/azure-ad-pim-approval-workflow/image015.png)

Quando viene caricato il pannello di selezione responsabili approvazione hello, è possibile cercare un utente o gruppo specifico tramite la barra di ricerca hello a top hello o selezionare dall'elenco pre-popolato hello, quindi fare clic su "Select" al termine:

![](media/azure-ad-pim-approval-workflow/image017.png)

Nota: è possibile selezionare contemporaneamente più utenti o gruppi.

La selezione verrà visualizzato nell'elenco di hello di responsabili approvazione selezionati, come illustrato di seguito:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove un revisore, fare semplicemente clic hello rimuovere pulsante Avanti tootheir il nome.

approvazione tooadd aggiuntivi, il processo di ripetizione hello.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi

cronologia tooview di richiesta e l'approvazione per i ruoli con tutti i privilegi, selezionare la cronologia di controllo dal dashboard hello:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
È possibile ordinare i dati di hello per azione e cercare "Approved di attivazione"

### <a name="view-pending-approvals-requests"></a>Visualizzare le approvazioni (richieste) in sospeso

In qualità di responsabile approvazione con delega riceverà notifiche e-mail quando una richiesta è in attesa di approvazione. tooview queste richieste nel portale PIM hello dalla scheda dashboard (nella nuova navigazione hello) Seleziona hello "in sospeso richieste di approvazione" hello, barra di spostamento a sinistra.

![](media/azure-ad-pim-approval-workflow/image023.png)

Da qui, è possibile visualizzare un elenco delle richieste in attesa di approvazione:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)

Selezionare desidera tooapprove o negare le richieste di hello e fare clic sul pulsante hello nella barra delle azioni che corrisponde a quanto deciso:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Fornire una giustificazione per l’approvazione/il rifiuto

Verrà aprire un nuovo tooapprove pannello o negare più richieste contemporaneamente. Immettere una motivazione per la decisione e fare clic su Approva (o negare) nella parte inferiore di hello o blade hello:

![](media/azure-ad-pim-approval-workflow/image029.png)

Una volta completato il processo di richiesta di hello, icona stato hello rifletterà la decisione presa (in questo esempio, la decisione hello è approvare):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Richiedere l’attivazione di un ruolo che richiede l’approvazione

Richiesta di attivazione di un ruolo che richiede l'approvazione può essere avviata dalla navigazione PIM precedente hello o nuova navigazione hello, come processo hello per ruolo attivazione rimane hello stesso. È sufficiente selezionare un ruolo dall'elenco di hello dei ruoli per attivare:

![](media/azure-ad-pim-approval-workflow/image033.png)

Se un ruolo con privilegi richiede la Multi-Factor Authentication, verrà richiesto di completare prima questa attività:

![](media/azure-ad-pim-approval-workflow/image035.png)

Al termine, fare clic su Attiva e fornire una giustificazione (se richiesta):

![](media/azure-ad-pim-approval-workflow/image037.png)

richiedente Hello verrà visualizzata una notifica che hello richiesta in attesa di approvazione:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Visualizzare lo stato di hello di tooactivate la richiesta

Visualizzazione stato hello di tooactivate una richiesta in sospeso deve essere accessibile dal riquadro di spostamento di nuovo. Barra di spostamento a sinistra di hello, selezionare scheda "Richieste di" hello:

![](media/azure-ad-pim-approval-workflow/image041.png)

stato richiesta Hello predefinite troppo "In sospeso", ma è possibile attivare o disattivare toosee tutti o richieste rifiutate.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Completare l’attività in Azure AD se l’attivazione è stata approvata

Una volta approvata la richiesta di hello, ruolo hello è attiva ed è possibile procedere con le operazioni che richiedono questo ruolo.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Passaggi successivi

Commenti e suggerimenti sono utili toous. Dettagli tooshare libero commenti o suggerimenti con noi qui!
