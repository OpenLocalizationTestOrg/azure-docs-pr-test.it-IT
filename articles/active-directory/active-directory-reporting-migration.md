---
title: "report relativi all'attività aaaFind nel portale di Azure hello | Documenti Microsoft"
description: "Informazioni su come i report di attività di Azure Active Directory toofind in hello portale di Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Individuare i report di attività nel portale di Azure hello

Se si sposta da hello Azure toohello portale classico portale di Azure, viene visualizzato un nuovo aspetto log attività di Azure Active Directory (Azure AD). In un recente [post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), viene descritto come è possibile visualizzare il log attività nel contesto di hello della risorsa hello si sta lavorando in hello portale di Azure. In questo articolo viene descritto come toofind segnala che è stato utilizzato nel portale di Azure classico nel portale di Azure hello hello.

## <a name="whats-new"></a>Novità

I report nel portale di Azure classico hello sono suddivisi in categorie:

1.  Report sulla sicurezza
2.  Report sull’attività
3.  Report app integrate

### <a name="activity-and-integrated-app-reports"></a>Report attività e app integrate

Basata sul contesto dei report nel portale di Azure hello, i report esistenti vengono uniti in una singola visualizzazione. Una singola API sottostante visualizza hello dati toohello.

Questa vista in hello toosee **Azure Active Directory** pannello, in **attività**selezionare **log di controllo**.

![Log di controllo](./media/active-directory-reporting-migration/482.png "Log di controllo")

Hello i report seguenti è consolidato in questa vista:

-   Report di controllo
-   Attività di reimpostazione password
-   Attività di registrazione reimpostazione password
-   Attività dei gruppi self-service
-   Modifiche del nome del gruppo di Office 365
-   Attività di provisioning dell'account
-   Stato rollover della password
-   Errori di provisioning dell'account


report di utilizzo dell'applicazione Hello è stata migliorata ed è incluso in hello **accessi** visualizzazione. Questa vista in hello toosee **Azure Active Directory** pannello, in **attività**selezionare **accessi**.

![Visualizzazione Accessi](./media/active-directory-reporting-migration/483.png "Visualizzazione Accessi")

Hello **accessi** visualizzazione include tutti gli accessi utente. È possibile utilizzare queste informazioni sull'utilizzo di informazioni tooget applicazione. È inoltre possibile visualizzare informazioni sull'utilizzo dell'applicazione in hello **applicazioni aziendali** panoramica, in hello **GESTISCI** sezione.

![Applicazioni aziendali](./media/active-directory-reporting-migration/484.png "Applicazioni aziendali")

## <a name="access-a-specific-report"></a>Accedere a un report specifico

Sebbene hello portale di Azure offre una visualizzazione singola, è anche possibile esaminare i report specifici.

### <a name="audit-logs"></a>Log di controllo

In commenti e suggerimenti toocustomer risposta, in hello portale di Azure, è possibile utilizzare avanzate dati hello tooaccess filtro desiderati. È un filtro, è possibile utilizzare un *categoria attività*, che sono elencati hello diversi tipi di attività registra in Azure AD. toonarrow risultati toowhat che si sta cercando, è possibile selezionare una categoria.

Ad esempio, se si è interessati solo la reimpostazione della password di tooself servizio correlato di attività, è possibile scegliere hello **la gestione delle Password Self-Service** categoria. categorie di Hello che vedrai si basano sulla risorsa hello in che ci si trova.  

![Le opzioni di categoria nella pagina di log di controllo filtro hello](./media/active-directory-reporting-migration/06.png "opzioni categoria hello filtro registri di controllo pagina")

Le categorie delle attività includono:

- Directory principale
- Gestione delle password self-service
- Gestione gruppi self-service
- Provisioning degli account

### <a name="application-usage"></a>Utilizzo applicazioni

tooview i dettagli sull'utilizzo dell'applicazione per tutte le app o per una singola applicazione, in **attività**selezionare **accessi**. risultati hello toonarrow, sarà possibile filtrare per nome utente o nome dell'applicazione.

![Pagina Filtra eventi di accesso](./media/active-directory-reporting-migration/07.png "Pagina Filtra eventi di accesso")

### <a name="security-reports"></a>Report sulla sicurezza

#### <a name="azure-ad-anomalous-activity-reports"></a>Report di Anomalie dell'attività di Azure AD

Sicurezza di Azure AD attività anomale report dal portale di Azure classico hello sono stati consolidati tooprovide con a una vista centrale. Questa visualizzazione mostra tutti gli eventi di rischio correlati alla sicurezza che Azure AD è in grado di rilevare e segnalare.

Hello nella tabella seguente elenca i report di sicurezza di attività anomale hello Azure AD e corrispondenti tipi di eventi di rischio in hello portale di Azure.

| Report di Anomalie dell'attività di Azure AD |  Tipo di evento di rischio di Identity Protection|
| :--- | :--- |
| Utenti con credenziali perse | Credenziali perse |
| Attività di accesso irregolare | Comunicazione Impossibile tooatypical percorsi |
| Accessi da dispositivi potenzialmente infetti | Accessi da dispositivi infetti|
| Accessi da origini sconosciute | Accessi da indirizzi IP anonimi |
| Accessi da indirizzi IP con attività sospette | Accessi da indirizzi IP con attività sospette |
| - | Accessi da posizioni non note |

sicurezza di Azure AD attività anomale seguenti Hello report non sono inclusi come eventi di rischio in hello portale di Azure:

* Accessi dopo più errori
* Accessi da più aree geografiche

Questi report sono ancora disponibili nel portale di Azure classico hello, ma sarà deprecate in un momento nel futuro hello.

Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Eventi di rischio rilevati

Nel portale di Azure hello, è possibile accedere a report sugli eventi di rischio rilevati in hello **Azure Active Directory** pannello, in **sicurezza**. Eventi di rischio rilevati vengono rilevati in hello seguenti report:   

- Utenti a rischio
- Accessi a rischio

![Report di sicurezza](./media/active-directory-reporting-migration/04.png "Report di sicurezza")

Per altre informazioni sui report di sicurezza, vedere:

- [Utenti dei report di rischio per la sicurezza nel portale di Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Report accessi rischiosa nel portale di Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Report attività hello portale di Azure classico e hello portale di Azure

tabella Hello in questa sezione sono elencati i report esistenti nel portale di Azure classico hello. Viene inoltre descritto come ottenere hello stesse informazioni nel portale di Azure hello.

tooview tutti i dati, in hello del controllo **Azure Active Directory** pannello, in **attività**, andare troppo**log di controllo**.

![Log di controllo](./media/active-directory-reporting-migration/61.png "Log di controllo")

| portale di Azure classico                 | toofind in hello portale di Azure                                                         |
| ---                                  | ---                                                                        |
| Log di controllo                           | Per **Categoria attività** selezionare **Core directory** (Directory principale).                       |
| Attività di reimpostazione password              | Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service). |
| Attività di registrazione reimpostazione password | Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).     |
| Attività dei gruppi self-service         | Per **Categoria attività** selezionare **Gestione gruppi self-service**.        |
| Attività di provisioning dell'account        | Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).         |
| Stato rollover della password             | Per **Categoria attività** selezionare **Automatic App Password Rollover** (Rollover password app automatico).      |
| Errori di provisioning dell'account          | Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).        |
| Modifiche del nome del gruppo di Office 365         | Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service). Per **Activity Resource Type** (Tipo di risorsa attività) selezionare **Gruppo**. Per **Origine attività** selezionare **O365 groups** (Gruppi di O365).|

hello tooview **utilizzo dell'applicazione** hello report **Azure Active Directory** pannello, in **GESTISCI**selezionare **applicazioni aziendali**, quindi selezionare **accessi**.


![Report degli accessi alle applicazioni aziendali](./media/active-directory-reporting-migration/199.png "Report degli accessi alle applicazioni aziendali")

## <a name="next-steps"></a>Passaggi successivi

Per una panoramica di gestione di report, vedere hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).
