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
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="98c35-103">Introduzione ad Azure Active Directory Reporting</span><span class="sxs-lookup"><span data-stu-id="98c35-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="98c35-104">Che cos'è</span><span class="sxs-lookup"><span data-stu-id="98c35-104">What it is</span></span>
<span data-ttu-id="98c35-105">Azure Active Directory (Azure AD) include la sicurezza, l’attività e i report di controllo per la directory.</span><span class="sxs-lookup"><span data-stu-id="98c35-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="98c35-106">Di seguito è riportato un elenco di report hello inclusi:</span><span class="sxs-lookup"><span data-stu-id="98c35-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="98c35-107">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="98c35-107">Security reports</span></span>
* <span data-ttu-id="98c35-108">Accessi da origini sconosciute</span><span class="sxs-lookup"><span data-stu-id="98c35-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="98c35-109">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="98c35-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="98c35-110">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="98c35-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="98c35-111">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="98c35-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="98c35-112">Attività di accesso irregolare</span><span class="sxs-lookup"><span data-stu-id="98c35-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="98c35-113">Accessi da dispositivi potenzialmente infetti</span><span class="sxs-lookup"><span data-stu-id="98c35-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="98c35-114">Utenti con anomalie dell'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="98c35-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="98c35-115">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="98c35-115">Activity reports</span></span>
* <span data-ttu-id="98c35-116">Utilizzo dell'applicazione: riepilogo</span><span class="sxs-lookup"><span data-stu-id="98c35-116">Application usage: summary</span></span>
* <span data-ttu-id="98c35-117">Utilizzo dell'applicazione: dettagliato</span><span class="sxs-lookup"><span data-stu-id="98c35-117">Application usage: detailed</span></span>
* <span data-ttu-id="98c35-118">Dashboard dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="98c35-118">Application dashboard</span></span>
* <span data-ttu-id="98c35-119">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="98c35-119">Account provisioning errors</span></span>
* <span data-ttu-id="98c35-120">Dispositivi dell’utente singolo</span><span class="sxs-lookup"><span data-stu-id="98c35-120">Individual user devices</span></span>
* <span data-ttu-id="98c35-121">Attività dell’utente singolo</span><span class="sxs-lookup"><span data-stu-id="98c35-121">Individual user Activity</span></span>
* <span data-ttu-id="98c35-122">Report attività dei gruppi</span><span class="sxs-lookup"><span data-stu-id="98c35-122">Groups activity report</span></span>
* <span data-ttu-id="98c35-123">Report attività di registrazione per la reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="98c35-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="98c35-124">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="98c35-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="98c35-125">Report di controllo</span><span class="sxs-lookup"><span data-stu-id="98c35-125">Audit reports</span></span>
* <span data-ttu-id="98c35-126">Report di controllo della Directory</span><span class="sxs-lookup"><span data-stu-id="98c35-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="98c35-127">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="98c35-128">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="98c35-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="98c35-129">Report sulla pipeline</span><span class="sxs-lookup"><span data-stu-id="98c35-129">Reporting pipeline</span></span>
<span data-ttu-id="98c35-130">Hello reporting pipeline è costituita da tre passaggi principali.</span><span class="sxs-lookup"><span data-stu-id="98c35-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="98c35-131">Ogni volta che un utente accede o un'autenticazione viene effettuata, si verifica hello segue:</span><span class="sxs-lookup"><span data-stu-id="98c35-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="98c35-132">Innanzitutto, hello viene autenticato (esito positivo o negativo) e hello risultato viene archiviato nel database del servizio di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="98c35-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="98c35-133">A intervalli regolari, tutti gli accessi recenti vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="98c35-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="98c35-134">A questo punto, la sicurezza e gli algoritmi relativi ad attività anomale eseguono la ricerca di attività sospette in tutti gli accessi recenti.</span><span class="sxs-lookup"><span data-stu-id="98c35-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="98c35-135">Dopo l'elaborazione, hello report vengono scritti, memorizzato nella cache e gestite nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="98c35-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="98c35-136">Tempi per la generazione di report</span><span class="sxs-lookup"><span data-stu-id="98c35-136">Report generation times</span></span>
<span data-ttu-id="98c35-137">A causa di toohello volume elevato di autenticazioni e aggiuntivi elaborata hello piattaforma Azure AD di accedere, hello più recenti accessi elaborati sono, in Media, un'ora prima.</span><span class="sxs-lookup"><span data-stu-id="98c35-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="98c35-138">In rari casi, potrebbe richiedere fino a too8 ore tooprocess hello più recenti accessi.</span><span class="sxs-lookup"><span data-stu-id="98c35-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="98c35-139">È possibile trovare Accedi elaborato più recente di hello esaminando il testo della Guida hello nella parte superiore di hello di ogni report.</span><span class="sxs-lookup"><span data-stu-id="98c35-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Testo della Guida nella parte superiore di hello di ogni report](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="98c35-141">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="98c35-142">introduttiva</span><span class="sxs-lookup"><span data-stu-id="98c35-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="98c35-143">Accedere a hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="98c35-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="98c35-144">In primo luogo, è necessario toosign in hello [portale di Azure classico](https://manage.windowsazure.com) come amministratore globale o di conformità.</span><span class="sxs-lookup"><span data-stu-id="98c35-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="98c35-145">Si deve anche essere un amministratore del servizio di sottoscrizione di Azure o un coamministratore, oppure può essere utilizzato in hello "accesso tooAzure AD" sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="98c35-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="98c35-146">Passare tooReports</span><span class="sxs-lookup"><span data-stu-id="98c35-146">Navigate tooReports</span></span>
<span data-ttu-id="98c35-147">Report tooview, passare scheda report toohello nella parte superiore di hello della directory.</span><span class="sxs-lookup"><span data-stu-id="98c35-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="98c35-148">Se questa è la prima volta che la visualizzazione dei report di hello, è necessario la finestra di dialogo di tooagree tooa prima di poter visualizzare i report di hello.</span><span class="sxs-lookup"><span data-stu-id="98c35-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="98c35-149">Si tratta di tooensure è che gli amministratori del tooview organizzazione questi dati, che possono essere considerati informazioni private, in alcuni paesi.</span><span class="sxs-lookup"><span data-stu-id="98c35-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![Nella finestra di dialogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="98c35-151">Esplorare ogni report</span><span class="sxs-lookup"><span data-stu-id="98c35-151">Explore each report</span></span>
<span data-ttu-id="98c35-152">Spostarsi in ogni report toosee hello i dati vengono raccolti ed elaborati hello accessi.</span><span class="sxs-lookup"><span data-stu-id="98c35-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="98c35-153">È possibile trovare un [qui tutti i report di hello](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Tutti i report](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="98c35-155">Scaricare il report di hello in formato CSV</span><span class="sxs-lookup"><span data-stu-id="98c35-155">Download hello reports as CSV</span></span>
<span data-ttu-id="98c35-156">Ogni report può essere scaricato come file CSV (valori delimitati da virgole).</span><span class="sxs-lookup"><span data-stu-id="98c35-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="98c35-157">È possibile utilizzare questi file in Excel, Power BI o programmi toofurther analizzare i dati di analisi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="98c35-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="98c35-158">toodownload qualsiasi report in un formato CSV, passare toohello report e fare clic su "Download" nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="98c35-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![Pulsante di download](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="98c35-160">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="98c35-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98c35-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="98c35-162">Personalizzare gli avvisi per attività di accesso anomala.</span><span class="sxs-lookup"><span data-stu-id="98c35-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="98c35-163">Spostarsi sulla scheda "Configurazione" toohello della directory.</span><span class="sxs-lookup"><span data-stu-id="98c35-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="98c35-164">Sezione "Notifiche" toohello di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="98c35-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="98c35-165">Abilitare o disabilitare la sezione "Notifiche tramite posta elettronica di accessi anomali" hello.</span><span class="sxs-lookup"><span data-stu-id="98c35-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Hello sezione notifiche](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="98c35-167">Integrazione con hello API Azure AD Reporting</span><span class="sxs-lookup"><span data-stu-id="98c35-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="98c35-168">Vedere [introduzione hello API Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="98c35-169">Assegnare la Multi-Factor Authentication agli utenti.</span><span class="sxs-lookup"><span data-stu-id="98c35-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="98c35-170">Selezionare un utente in un report.</span><span class="sxs-lookup"><span data-stu-id="98c35-170">Select a user in a report.</span></span>

<span data-ttu-id="98c35-171">Fare clic su hello "Abilita autenticazione a più fattori" in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="98c35-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![pulsante di multi-Factor Authentication Hello in basso hello hello](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="98c35-173">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="98c35-174">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="98c35-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="98c35-175">Eventi di controllo</span><span class="sxs-lookup"><span data-stu-id="98c35-175">Audit events</span></span>
<span data-ttu-id="98c35-176">Informazioni su quali eventi vengono controllati nella directory hello [Azure Active Directory Reporting gli eventi di controllo](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="98c35-177">Integrazione di API</span><span class="sxs-lookup"><span data-stu-id="98c35-177">API Integration</span></span>
<span data-ttu-id="98c35-178">Vedere [introduzione hello API Reporting](active-directory-reporting-api-getting-started.md) hello e [documentazione di riferimento API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="98c35-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="98c35-179">Ottenere un contatto</span><span class="sxs-lookup"><span data-stu-id="98c35-179">Get in touch</span></span>
<span data-ttu-id="98c35-180">Inviare un messaggio di posta elettronica all'indirizzo [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) per commenti, richieste di assistenza o eventuali domande.</span><span class="sxs-lookup"><span data-stu-id="98c35-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="98c35-181">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="98c35-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

