---
title: Introduzione alla creazione di report in Azure Active Directory | Microsoft Azure
description: Elenca i vari report disponibili nei report di Azure Active Directory
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
ms.openlocfilehash: 5cd1ae6196d9cd63f97dc9d302442280ece23e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="b552a-103">Introduzione ad Azure Active Directory Reporting</span><span class="sxs-lookup"><span data-stu-id="b552a-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="b552a-104">Che cos'è</span><span class="sxs-lookup"><span data-stu-id="b552a-104">What it is</span></span>
<span data-ttu-id="b552a-105">Azure Active Directory (Azure AD) include la sicurezza, l’attività e i report di controllo per la directory.</span><span class="sxs-lookup"><span data-stu-id="b552a-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="b552a-106">Di seguito è riportato un elenco dei report compresi:</span><span class="sxs-lookup"><span data-stu-id="b552a-106">Here's a list of the reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="b552a-107">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="b552a-107">Security reports</span></span>
* <span data-ttu-id="b552a-108">Accessi da origini sconosciute</span><span class="sxs-lookup"><span data-stu-id="b552a-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="b552a-109">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="b552a-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="b552a-110">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="b552a-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="b552a-111">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="b552a-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="b552a-112">Attività di accesso irregolare</span><span class="sxs-lookup"><span data-stu-id="b552a-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="b552a-113">Accessi da dispositivi potenzialmente infetti</span><span class="sxs-lookup"><span data-stu-id="b552a-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="b552a-114">Utenti con anomalie dell'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="b552a-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="b552a-115">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="b552a-115">Activity reports</span></span>
* <span data-ttu-id="b552a-116">Utilizzo dell'applicazione: riepilogo</span><span class="sxs-lookup"><span data-stu-id="b552a-116">Application usage: summary</span></span>
* <span data-ttu-id="b552a-117">Utilizzo dell'applicazione: dettagliato</span><span class="sxs-lookup"><span data-stu-id="b552a-117">Application usage: detailed</span></span>
* <span data-ttu-id="b552a-118">Dashboard dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b552a-118">Application dashboard</span></span>
* <span data-ttu-id="b552a-119">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="b552a-119">Account provisioning errors</span></span>
* <span data-ttu-id="b552a-120">Dispositivi dell’utente singolo</span><span class="sxs-lookup"><span data-stu-id="b552a-120">Individual user devices</span></span>
* <span data-ttu-id="b552a-121">Attività dell’utente singolo</span><span class="sxs-lookup"><span data-stu-id="b552a-121">Individual user Activity</span></span>
* <span data-ttu-id="b552a-122">Report attività dei gruppi</span><span class="sxs-lookup"><span data-stu-id="b552a-122">Groups activity report</span></span>
* <span data-ttu-id="b552a-123">Report attività di registrazione per la reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="b552a-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="b552a-124">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="b552a-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="b552a-125">Report di controllo</span><span class="sxs-lookup"><span data-stu-id="b552a-125">Audit reports</span></span>
* <span data-ttu-id="b552a-126">Report di controllo della Directory</span><span class="sxs-lookup"><span data-stu-id="b552a-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="b552a-127">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="b552a-128">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="b552a-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="b552a-129">Report sulla pipeline</span><span class="sxs-lookup"><span data-stu-id="b552a-129">Reporting pipeline</span></span>
<span data-ttu-id="b552a-130">La pipeline di report è costituita da tre passaggi principali.</span><span class="sxs-lookup"><span data-stu-id="b552a-130">The reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="b552a-131">Ogni volta che un utente accede o si effettua l'autenticazione, si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b552a-131">Every time a user signs in, or an authentication is made, the following happens:</span></span>

* <span data-ttu-id="b552a-132">In primo luogo, l'utente viene autenticato (con esito positivo o negativo) e il risultato viene archiviato nei database del servizio Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b552a-132">First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.</span></span>
* <span data-ttu-id="b552a-133">A intervalli regolari, tutti gli accessi recenti vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="b552a-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="b552a-134">A questo punto, la sicurezza e gli algoritmi relativi ad attività anomale eseguono la ricerca di attività sospette in tutti gli accessi recenti.</span><span class="sxs-lookup"><span data-stu-id="b552a-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="b552a-135">Dopo l'elaborazione, i report vengono scritti, memorizzati nella cache e gestiti nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b552a-135">After processing, the reports are written, cached, and served in the Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="b552a-136">Tempi per la generazione di report</span><span class="sxs-lookup"><span data-stu-id="b552a-136">Report generation times</span></span>
<span data-ttu-id="b552a-137">A causa della grande quantità di autenticazioni e accessi elaborati dalla piattaforma di Azure AD, gli accessi più recenti elaborati sono, in media, di un'ora prima.</span><span class="sxs-lookup"><span data-stu-id="b552a-137">Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="b552a-138">In rari casi, ci potrebbero volere fino a 8 ore per elaborare gli accessi più recenti.</span><span class="sxs-lookup"><span data-stu-id="b552a-138">In rare cases, it may take up to 8 hours to process the most recent sign-ins.</span></span>

<span data-ttu-id="b552a-139">È possibile trovare l’accesso più recente elaborato esaminando il testo della Guida nella parte superiore di ogni report.</span><span class="sxs-lookup"><span data-stu-id="b552a-139">You can find the most recent processed sign-in by examining the help text at the top of each report.</span></span>

![Testo della Guida nella parte superiore di ogni report](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="b552a-141">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="b552a-142">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b552a-142">Getting started</span></span>
### <a name="sign-into-the-azure-classic-portal"></a><span data-ttu-id="b552a-143">Accedere al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b552a-143">Sign into the Azure classic portal</span></span>
<span data-ttu-id="b552a-144">Innanzitutto, è necessario accedere al [Portale di Azure classico](https://manage.windowsazure.com) .come amministratore globale o di conformità.</span><span class="sxs-lookup"><span data-stu-id="b552a-144">First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="b552a-145">Si deve anche essere un amministratore o coamministratore del servizio di sottoscrizione di Azure oppure usare la sottoscrizione di Azure "Accesso ad Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="b552a-145">You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.</span></span>

### <a name="navigate-to-reports"></a><span data-ttu-id="b552a-146">Passare al report</span><span class="sxs-lookup"><span data-stu-id="b552a-146">Navigate to Reports</span></span>
<span data-ttu-id="b552a-147">Per visualizzare i report, passare alla scheda report nella parte superiore della directory.</span><span class="sxs-lookup"><span data-stu-id="b552a-147">To view Reports, navigate to the Reports tab at the top of your directory.</span></span>

<span data-ttu-id="b552a-148">Se questa è la prima volta in cui vengono visualizzati i report, è necessario accettare una finestra di dialogo prima di poter visualizzare i report.</span><span class="sxs-lookup"><span data-stu-id="b552a-148">If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports.</span></span> <span data-ttu-id="b552a-149">Questo serve a verificare che agli amministratori dell'azienda sia consentito visualizzare i dati, che possono essere considerati informazioni riservate in alcuni paesi.</span><span class="sxs-lookup"><span data-stu-id="b552a-149">This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.</span></span>

![Nella finestra di dialogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="b552a-151">Esplorare ogni report</span><span class="sxs-lookup"><span data-stu-id="b552a-151">Explore each report</span></span>
<span data-ttu-id="b552a-152">Passare a ogni report per visualizzare i dati che raccolti e gli accessi elaborati.</span><span class="sxs-lookup"><span data-stu-id="b552a-152">Navigate into each report to see the data being collected and the sign-ins processed.</span></span> <span data-ttu-id="b552a-153">È possibile trovare un [elenco di tutti i report qui](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-153">You can find a [list of all the reports here](active-directory-reporting-guide.md).</span></span>

![Tutti i report](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a><span data-ttu-id="b552a-155">Scaricare i report in formato CSV</span><span class="sxs-lookup"><span data-stu-id="b552a-155">Download the reports as CSV</span></span>
<span data-ttu-id="b552a-156">Ogni report può essere scaricato come file CSV (valori delimitati da virgole).</span><span class="sxs-lookup"><span data-stu-id="b552a-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="b552a-157">È possibile utilizzare questi file in Excel, PowerBI o programmi di analisi di terze parti per un'ulteriore analisi dei dati</span><span class="sxs-lookup"><span data-stu-id="b552a-157">You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.</span></span>

<span data-ttu-id="b552a-158">Per scaricare tutti i report in un formato CSV, passare al report e fare clic su "Download" nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b552a-158">To download any report as a CSV, navigate to the report and click "Download" at the bottom.</span></span>

![Pulsante di download](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="b552a-160">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b552a-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b552a-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="b552a-162">Personalizzare gli avvisi per attività di accesso anomala.</span><span class="sxs-lookup"><span data-stu-id="b552a-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="b552a-163">Passare alla scheda "Configurazione" della directory.</span><span class="sxs-lookup"><span data-stu-id="b552a-163">Navigate to the "Configure" tab of your directory.</span></span>

<span data-ttu-id="b552a-164">Scorrere fino alla sezione "Notifiche".</span><span class="sxs-lookup"><span data-stu-id="b552a-164">Scroll to the "Notifications" section.</span></span>

<span data-ttu-id="b552a-165">Abilitare o disabilitare la sezione "Notifiche tramite posta elettronica di Accessi anomali".</span><span class="sxs-lookup"><span data-stu-id="b552a-165">Enable or disable the "Email Notifications of Anomalous sign-ins" section.</span></span>

![La sezione delle notifiche](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a><span data-ttu-id="b552a-167">Integrazione con l'API di creazione report di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b552a-167">Integrate with the Azure AD Reporting API</span></span>
<span data-ttu-id="b552a-168">Vedere la pagina relativa all' [Introduzione all'API di creazione report](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-168">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="b552a-169">Assegnare la Multi-Factor Authentication agli utenti.</span><span class="sxs-lookup"><span data-stu-id="b552a-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="b552a-170">Selezionare un utente in un report.</span><span class="sxs-lookup"><span data-stu-id="b552a-170">Select a user in a report.</span></span>

<span data-ttu-id="b552a-171">Fare clic sul pulsante "Abilita autenticazione a più fattori" nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="b552a-171">Click the "Enable MFA" button at the bottom of the screen.</span></span>

![Pulsante Multi-Factor Authentication nella parte inferiore dello schermo](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="b552a-173">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="b552a-174">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="b552a-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="b552a-175">Eventi di controllo</span><span class="sxs-lookup"><span data-stu-id="b552a-175">Audit events</span></span>
<span data-ttu-id="b552a-176">Informazioni su quali eventi vengono controllati nella directory in [Eventi di controllo per il report di Azure Active Directory](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-176">Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="b552a-177">Integrazione di API</span><span class="sxs-lookup"><span data-stu-id="b552a-177">API Integration</span></span>
<span data-ttu-id="b552a-178">Vedere [Introduzione all'API di creazione report](active-directory-reporting-api-getting-started.md) e la [documentazione di riferimento sulle API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="b552a-178">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="b552a-179">Ottenere un contatto</span><span class="sxs-lookup"><span data-stu-id="b552a-179">Get in touch</span></span>
<span data-ttu-id="b552a-180">Inviare un messaggio di posta elettronica all'indirizzo [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) per commenti, richieste di assistenza o eventuali domande.</span><span class="sxs-lookup"><span data-stu-id="b552a-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="b552a-181">Per ulteriori informazioni sul Report di AD Azure, consultare [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b552a-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

