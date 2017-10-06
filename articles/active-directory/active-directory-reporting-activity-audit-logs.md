---
title: "report relativi all'attività aaaAudit nel portale di Azure Active Directory hello | Documenti Microsoft"
description: "Report di attività nel portale di Azure Active Directory hello di controllo toohello introduzione"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Report attività nel portale di Azure Active Directory hello di controllo 

Grazie ai report in Azure Active Directory (Azure AD), è possibile ottenere informazioni hello necessarie toodetermine, svolgimento dell'ambiente.

architettura di reporting in Azure AD Hello è costituita da hello seguenti componenti:

- **Attività** 
    - **Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente
    - **Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.
- **Sicurezza** 
    - **Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente. Per informazioni dettagliate, vedere Accessi a rischio.
    - **Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso. Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.

In questo argomento offre una panoramica delle attività di controllo hello.
 
## <a name="who-can-access-hello-data"></a>Chi può accedere a dati hello?
* Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello
* Gli amministratori globali
* I singoli utenti (non amministratori) possono visualizzare le proprie attività


## <a name="audit-logs"></a>Log di controllo

i log di controllo Hello in Azure Active Directory forniscono i record di attività di sistema per la conformità.  
È il primo dati di controllo di voce punto tooall **log di controllo** in hello **attività** sezione **Azure Active Directory**.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/61.png "Log di controllo")

Un log di controllo è una visualizzazione elenco predefinita che include:

- Hello data e ora dell'occorrenza hello
- Hello iniziatore / attore (*che*) di un'attività 
- attività Hello (*cosa*) 
- destinazione Hello

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/18.png "Log di controllo")

È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/19.png "Log di controllo")

Questo consente toodisplay altri campi o rimuovere campi già visualizzati.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/21.png "Log di controllo")


Facendo clic su un elemento in visualizzazione elenco hello, ottenere tutte le informazioni disponibili su di esso.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/22.png "Log di controllo")


## <a name="filtering-audit-logs"></a>Filtro dei log di controllo

toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di controllo hello utilizzando hello seguenti campi:

- Intervallo di date
- Azione avviata da (attore)
- Categoria
- Activity resource type (Tipo di risorsa dell'attività)
- Attività

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/23.png "Log di controllo")


Hello **intervallo di date** toodefine tooyou di filtro consente un intervallo di tempo per hello ha restituito dati.  
I valori possibili sono:

- 1 mese
- 7 giorni
- 24 ore
- Personalizzate

Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.

Hello **avviato da** filtro consente toodefine è il nome di un attore o il nome dell'entità universal (UPN).

Hello **categoria** filtro consente tooselect di hello filtro seguente:

- Tutti
- Categoria principale
- Directory principale
- Gestione delle password self-service
- Gestione di gruppi self-service
- Provisioning degli account e rollover automatizzato delle password
- Utenti invitati
- Servizio MIM
- Identity Protection
- B2C

Hello **il tipo di risorsa attività** filtro consente tooselect hello seguenti filtri:

- Tutti 
- Gruppo
- Directory
- Utente
- Applicazione
- Criteri
- Dispositivo
- Altre

Quando si seleziona **gruppo** come **il tipo di risorsa attività**, si ottiene tooalso a una categoria di filtro aggiuntivo che consente di fornire un **origine**:

- Azure AD
- O365


Hello **attività** filtro è basato sulla categoria di hello e selezione tipo di risorsa attività effettuata. È possibile selezionare un'attività specifica, è preferibile toosee o scegliere tutte. 

È possibile ottenere l'elenco di hello di tutte le attività di controllo utilizzando l'API Graph https://graph.windows.net/$ hello tenantdomain/attività/auditActivityTypes? api-version = beta, in cui $tenantdomain = il nome di dominio o consultare l'articolo toohello [report di controllo eventi](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Collegamenti ai log di controllo

Inoltre troppo**Azure Active Directory**, hello portale di Azure offre due punti di ingresso aggiuntivi tooaudit dati:

- Utenti e gruppi
- Applicazioni aziendali

### <a name="users-and-groups-audit-logs"></a>Log di controllo di utenti e gruppi

Con l'utente e i report di controllo in base al gruppo, è possibile ottenere risposte tooquestions, ad esempio:

- I tipi di aggiornamenti sono stati gli utenti di applicare hello?

- Quanti utenti sono stati modificati?

- Quante password sono state modificate?

- Quali operazioni ha eseguito un amministratore in una directory?

- Quali sono i gruppi che sono stati aggiunti hello?

- Sono presenti gruppi con modifiche all'appartenenza?

- Sono stati modificati per i proprietari del gruppo hello?

- Le licenze sono state assegnate a un utente o gruppo tooa?

Se si desidera tooreview dati toousers correlati e i gruppi di controllo, è possibile trovare una visualizzazione filtrata in **log di controllo** in hello **attività** sezione di hello **utenti e gruppi**. Per questo punto di ingresso, **Tipo di risorsa attività** preselezionato è **Utenti e gruppi**.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/93.png "Log di controllo")

### <a name="enterprise-applications-audit-logs"></a>Log di controllo di applicazioni aziendali

Report di controllo con basato sull'applicazione, è possibile ottenere risposte tooquestions, ad esempio:

* Quali sono le applicazioni che sono stati aggiunti o aggiornate hello?
* Quali sono le applicazioni che sono state rimosse hello?
* È stata modificata un'entità servizio per un'applicazione?
* Sono stati modificati i nomi di hello delle applicazioni?
* Che ha fornito il consenso tooan applicazione?

Se si desidera controllare i dati di applicazioni correlate tooyour tooreview, è possibile trovare una visualizzazione filtrata in **log di controllo** in hello **attività** sezione di hello **applicazioni aziendali**  blade. Per questo punto di ingresso, il **Tipo di risorsa attività** preselezionato è **Applicazioni aziendali**.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/134.png "Log di controllo")

È possibile filtrare la visualizzazione ulteriormente verso il basso toojust **gruppi** o semplicemente **utenti**.

![Log di controllo](./media/active-directory-reporting-activity-audit-logs/25.png "Log di controllo")


## <a name="next-steps"></a>Passaggi successivi

Per una panoramica di gestione di report, vedere hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).

