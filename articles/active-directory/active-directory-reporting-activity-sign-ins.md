---
title: "report attività aaaSign aggiuntivo nel portale di Azure Active Directory hello | Documenti Microsoft"
description: "Report attività di toosign introduzione nel portale di Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Report attività di accesso nel portale di Azure Active Directory hello

Con Azure Active Directory (Azure AD) reporting in hello [portale di Azure](https://portal.azure.com), è possibile ottenere informazioni hello necessarie toodetermine, svolgimento dell'ambiente.

architettura di report in Azure Active Directory Hello è costituita da hello seguenti componenti:

- **Attività** 
    - **Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente
    - **Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.
- **Sicurezza** 
    - **Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente. Per informazioni dettagliate, vedere Accessi a rischio.
    - **Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso. Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.

In questo argomento fornisce una panoramica delle attività di accesso hello.

## <a name="pre-requisite"></a>Prerequisito.

### <a name="who-can-access-hello-data"></a>Chi può accedere a dati hello?
* Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello
* Gli amministratori globali
* Qualsiasi utente (non amministratore) può visualizzare i propri accessi 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Licenza Azure AD è necessario tooaccess attività di accesso?
* Il tenant deve avere una licenza di Azure AD Premium è report le attività di accesso di hello toosee


## <a name="signs-in-activities"></a>Attività di accesso

Con informazioni hello fornite dai report di accesso utente hello, trovare risposte tooquestions, ad esempio:

* Che cos'è hello sign-in schema di un utente?
* Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?
* Qual è stato hello di tali accessi?

La prima voce tooall punto Accedi attività dati **accessi** nella sezione attività hello **Azure Active**.


![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/61.png "Attività di accesso")


Un log di controllo è una visualizzazione elenco predefinita che include:

- utente correlato Hello
- utente hello dell'applicazione Hello è firmato in
- Stato accesso Hello
- ora di accesso Hello

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")

È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/19.png "Attività di accesso")

Questo consente toodisplay altri campi o rimuovere campi già visualizzati.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/42.png "Attività di accesso")

Facendo clic su un elemento in visualizzazione elenco hello, ottenere tutte le informazioni disponibili su di esso.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/43.png "Attività di accesso")


## <a name="filtering-sign-in-activities"></a>Filtro delle attività di accesso

toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di accessi hello utilizzando hello seguenti campi:

- Intervallo di tempo
- Utente
- Applicazione
- Client
- Stato accesso

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/44.png "Attività di accesso")


Hello **intervallo di tempo** toodefine tooyou di filtro consente un intervallo di tempo per hello ha restituito dati.  
I valori possibili sono:

- 1 mese
- 7 giorni
- 24 ore
- Personalizzate

Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.

Hello **utente** filtro consente di nome hello toospecify o hello user principal name (UPN) dell'utente hello è rilevante.

Hello **applicazione** filtro consente nome hello toospecify dell'applicazione hello è rilevante.

Hello **client** filtro consente toospecify informazioni sul dispositivo hello è rilevante.

Hello **stato accesso** filtro consente tooselect di hello filtro seguente:

- Tutti
- Success
- Esito negativo


## <a name="sign-in-activities-shortcuts"></a>Collegamenti alle attività di accesso

Inoltre tooAzure Active Directory, hello portale di Azure fornisce due voce aggiuntiva punti toosign-in attività dati:

- Utenti e gruppi
- Applicazioni aziendali


### <a name="users-and-groups-sign-ins-activities"></a>Attività di accesso di utenti e gruppi

Con informazioni hello fornite dai report di accesso utente hello, trovare risposte tooquestions, ad esempio:

- Che cos'è hello sign-in schema di un utente?
- Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?
- Qual è stato hello di tali accessi?



I dati di toothis punto di ingresso sono hello utente Accedi grafico in hello **Panoramica** sezione nel **utenti e gruppi**.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/45.png "Attività di accesso")

Hello utente Accedi grafico Mostra aggregazioni settimanale di accesso aggiuntivi per tutti gli utenti in un determinato periodo di tempo. valore predefinito di Hello per hello periodo di tempo è 30 giorni.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/46.png "Attività di accesso")

Quando si fa clic in un giorno nel grafico hello di accesso, si ottiene un elenco dettagliato delle attività di accesso hello per il giorno corrente.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")

Ogni riga hello Accedi attività elenco offre che Hello informazioni dettagliate su hello selezionato Accedi, ad esempio:

* Chi ha effettuato l'accesso?
* Qual era hello correlati UPN?
* Individuare l'applicazione è stata hello destinazione Accedi hello?
* Che cos'è l'indirizzo IP hello del Accedi hello?
* Qual era stato hello di Accedi hello?

Hello **accessi** opzione offre una panoramica completa di tutti gli accessi utente.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/51.png "Attività di accesso")



## <a name="usage-of-managed-applications"></a>Utilizzo di applicazioni gestite

Con una visualizzazione dei dati di accesso basata sulle applicazioni, è possibile rispondere a domande come:

* Chi sta usando le applicazioni?
* Quali sono prime 3 applicazioni hello nell'organizzazione?
* Di recente è stata implementata un'applicazione. Come sta andando?

I dati di toothis punto di ingresso sono hello superiore 3 applicazioni dell'organizzazione all'interno di report di 30 giorni ultimo di hello in hello **Panoramica** sezione nel **applicazioni aziendali**.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/64.png "Attività di accesso")

Hello app utilizzo grafico settimanale aggregazioni di accessi per le applicazioni primi 3 in un determinato periodo di tempo. valore predefinito di Hello per hello periodo di tempo è 30 giorni.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/47.png "Attività di accesso")

Se si desidera, è possibile impostare lo stato attivo hello in un'applicazione specifica.


![Report](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Report")

Quando si fa clic in un giorno nel grafico di utilizzo di app hello, ottenere un elenco dettagliato delle attività di accesso hello.


![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/48.png "Attività di accesso")


Hello **accessi** opzione offre una panoramica completa di tutte le applicazioni tooyour eventi di accesso.

![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/49.png "Attività di accesso")



## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooknow ulteriori informazioni sui codici di errore attività di accesso, vedere hello [Accedi attività report codici di errore nel portale di Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).

