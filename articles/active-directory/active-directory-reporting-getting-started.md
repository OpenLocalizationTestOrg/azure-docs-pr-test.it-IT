---
title: Introduzione alla creazione di report in Azure Active Directory | Microsoft Azure
description: Gli elenchi di hello vari report disponibili in Azure Active Directory reporting
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Introduzione ad Azure Active Directory Reporting
## <a name="what-it-is"></a>Che cos'è
Azure Active Directory (Azure AD) include la sicurezza, l’attività e i report di controllo per la directory. Di seguito è riportato un elenco di report hello inclusi:

### <a name="security-reports"></a>Report sulla sicurezza
* Accessi da origini sconosciute
* Accessi dopo più errori
* Accessi da più aree geografiche
* Accessi da indirizzi IP con attività sospette
* Attività di accesso irregolare
* Accessi da dispositivi potenzialmente infetti
* Utenti con anomalie dell'attività di accesso

### <a name="activity-reports"></a>Report sull’attività
* Utilizzo dell'applicazione: riepilogo
* Utilizzo dell'applicazione: dettagliato
* Dashboard dell'applicazione
* Errori di provisioning dell'account
* Dispositivi dell’utente singolo
* Attività dell’utente singolo
* Report attività dei gruppi
* Report attività di registrazione per la reimpostazione password
* Attività di reimpostazione password

### <a name="audit-reports"></a>Report di controllo
* Report di controllo della Directory

> [!TIP]
> Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Funzionamento
### <a name="reporting-pipeline"></a>Report sulla pipeline
Hello reporting pipeline è costituita da tre passaggi principali. Ogni volta che un utente accede o un'autenticazione viene effettuata, si verifica hello segue:

* Innanzitutto, hello viene autenticato (esito positivo o negativo) e hello risultato viene archiviato nel database del servizio di hello Azure Active Directory.
* A intervalli regolari, tutti gli accessi recenti vengono elaborati. A questo punto, la sicurezza e gli algoritmi relativi ad attività anomale eseguono la ricerca di attività sospette in tutti gli accessi recenti.
* Dopo l'elaborazione, hello report vengono scritti, memorizzato nella cache e gestite nel portale di Azure classico hello.

### <a name="report-generation-times"></a>Tempi per la generazione di report
A causa di toohello volume elevato di autenticazioni e aggiuntivi elaborata hello piattaforma Azure AD di accedere, hello più recenti accessi elaborati sono, in Media, un'ora prima. In rari casi, potrebbe richiedere fino a too8 ore tooprocess hello più recenti accessi.

È possibile trovare Accedi elaborato più recente di hello esaminando il testo della Guida hello nella parte superiore di hello di ogni report.

![Testo della Guida nella parte superiore di hello di ogni report](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>introduttiva
### <a name="sign-into-hello-azure-classic-portal"></a>Accedere a hello portale di Azure classico
In primo luogo, è necessario toosign in hello [portale di Azure classico](https://manage.windowsazure.com) come amministratore globale o di conformità. Si deve anche essere un amministratore del servizio di sottoscrizione di Azure o un coamministratore, oppure può essere utilizzato in hello "accesso tooAzure AD" sottoscrizione di Azure.

### <a name="navigate-tooreports"></a>Passare tooReports
Report tooview, passare scheda report toohello nella parte superiore di hello della directory.

Se questa è la prima volta che la visualizzazione dei report di hello, è necessario la finestra di dialogo di tooagree tooa prima di poter visualizzare i report di hello. Si tratta di tooensure è che gli amministratori del tooview organizzazione questi dati, che possono essere considerati informazioni private, in alcuni paesi.

![Nella finestra di dialogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Esplorare ogni report
Spostarsi in ogni report toosee hello i dati vengono raccolti ed elaborati hello accessi. È possibile trovare un [qui tutti i report di hello](active-directory-reporting-guide.md).

![Tutti i report](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Scaricare il report di hello in formato CSV
Ogni report può essere scaricato come file CSV (valori delimitati da virgole). È possibile utilizzare questi file in Excel, Power BI o programmi toofurther analizzare i dati di analisi di terze parti.

toodownload qualsiasi report in un formato CSV, passare toohello report e fare clic su "Download" nella parte inferiore di hello.

![Pulsante di download](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Personalizzare gli avvisi per attività di accesso anomala.
Spostarsi sulla scheda "Configurazione" toohello della directory.

Sezione "Notifiche" toohello di scorrimento.

Abilitare o disabilitare la sezione "Notifiche tramite posta elettronica di accessi anomali" hello.

![Hello sezione notifiche](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Integrazione con hello API Azure AD Reporting
Vedere [introduzione hello API Reporting](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Assegnare la Multi-Factor Authentication agli utenti.
Selezionare un utente in un report.

Fare clic su hello "Abilita autenticazione a più fattori" in basso hello hello.

![pulsante di multi-Factor Authentication Hello in basso hello hello](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Altre informazioni
### <a name="audit-events"></a>Eventi di controllo
Informazioni su quali eventi vengono controllati nella directory hello [Azure Active Directory Reporting gli eventi di controllo](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Integrazione di API
Vedere [introduzione hello API Reporting](active-directory-reporting-api-getting-started.md) hello e [documentazione di riferimento API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Ottenere un contatto
Inviare un messaggio di posta elettronica all'indirizzo [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) per commenti, richieste di assistenza o eventuali domande.

> [!TIP]
> Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).
> 
> 

