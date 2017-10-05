---
title: Come usare il pacchetto di contenuto Power BI di Azure Active Directory | Microsoft Docs
description: Informazioni su come usare il pacchetto di contenuto Power BI di Azure Active Directory
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5c642bb814a279756e8391f12fdc86b6ec0b4a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="3c1ae-103">Come usare il pacchetto di contenuto Power BI di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c1ae-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="3c1ae-104">Comprendere in che modo gli utenti adottano e usano le funzionalità di Azure Active Directory è fondamentale per l'amministratore IT.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin.</span></span> <span data-ttu-id="3c1ae-105">Consente di pianificare l'infrastruttura IT e la comunicazione per incrementare l'utilizzo e sfruttare al meglio le funzionalità di AAD.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-105">It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="3c1ae-106">Il pacchetto di contenuto Power BI per Azure Active Directory consente di analizzare ulteriormente i dati per comprendere come usarli per ottenere informazioni più approfondite sulle attività svolte nell'istanza di Azure Active Directory per le varie funzionalità sulle quali si fa particolare affidamento.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-106">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="3c1ae-107">Con l'integrazione delle API di Azure Active Directory in Power BI, è possibile scaricare facilmente i pacchetti di contenuto preesistenti e ottenere informazioni dettagliate per tutte le attività all'interno di Azure Active Directory usando l'esperienza di visualizzazione avanzata offerta da Power BI.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-107">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="3c1ae-108">È possibile creare dashboard personalizzati e condividerli con altri utenti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-108">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="3c1ae-109">Questo argomento offre istruzioni dettagliate su come installare e usare il pacchetto di contenuto nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-109">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="3c1ae-110">Installare</span><span class="sxs-lookup"><span data-stu-id="3c1ae-110">Installation</span></span>  

<span data-ttu-id="3c1ae-111">**Per installare il pacchetto di contenuto di Power BI:**</span><span class="sxs-lookup"><span data-stu-id="3c1ae-111">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="3c1ae-112">Accedere a [Power BI](https://app.powerbi.com/groups/me/getdata/services) con l'account di Power BI, ovvero lo stesso account di Office 365 o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-112">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="3c1ae-113">Selezionare **Recupera dati** nella parte inferiore del riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-113">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="3c1ae-115">Nella casella **Servizi** fare clic su **Ottieni**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-115">In the **Services** box, click **Get**.</span></span>
   
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="3c1ae-117">Cercare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-117">Search for **Azure Active Directory**.</span></span>

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="3c1ae-119">Quando richiesto, digitare l'ID tenant di Azure AD e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-119">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="3c1ae-120">Un modo rapido per ottenere l'ID del tenant di Office 365 / Azure AD consiste nell'accedere al portale di Azure AD, eseguire il drill-down fino alla directory e copiare l'ID dall'URL seguente: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="3c1ae-120">A quick way to get the Tenant Id for your Office 365 / Azure AD tenant is to login to the Azure AD Portal, drill down to the directory and copy the ID from the following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="3c1ae-122">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-122">Click **Sign-in**.</span></span> 
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="3c1ae-124">Immettere il nome utente e la password, quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-124">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="3c1ae-126">Nella finestra di dialogo di consenso dell'app, fare clic su **Accetta**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-126">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="3c1ae-127">Fare clic sul dashboard dei log attività di Azure Active Directory, dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-127">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="3c1ae-129">Operazioni eseguibili con il pacchetto di contenuto</span><span class="sxs-lookup"><span data-stu-id="3c1ae-129">What can I do with this content pack?</span></span>

<span data-ttu-id="3c1ae-130">Prima di esaminare le operazioni eseguibili con questo pacchetto di contenuto, verrà illustrata una breve anteprima dei diversi report presenti nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-130">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="3c1ae-131">I dati dei report si riferiscono agli **ultimi 30 giorni**.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-131">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="3c1ae-132">Report inclusi in questa versione del pacchetto di contenuto dei log di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c1ae-132">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="3c1ae-133">**Report di utilizzo e tendenza delle app**: informazioni approfondite sulle app usate nell'organizzazione e su quali vengono usate più frequentemente e quando.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-133">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="3c1ae-134">Con questo report è possibile ottenere informazioni dettagliate sull'uso di un'app implementata di recente nell'organizzazione oppure scoprire quali app vengono usate maggiormente.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-134">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="3c1ae-135">In questo modo è possibile migliorare l'utilizzo se emerge che l'app non viene usata.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-135">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="3c1ae-136">**Accessi in base a posizioni e utenti**: informazioni dettagliate su tutti gli accessi eseguiti con l'identità di Azure e sull'identità degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-136">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="3c1ae-137">È così possibile esaminare in dettaglio i singoli accessi e rispondere a domande come:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-137">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="3c1ae-138">Da dove ha effettuato l'accesso questo utente?</span><span class="sxs-lookup"><span data-stu-id="3c1ae-138">From where did this user sign-ins?</span></span>
- <span data-ttu-id="3c1ae-139">Quale utente ha il maggior numero di accessi e da dove accede?</span><span class="sxs-lookup"><span data-stu-id="3c1ae-139">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="3c1ae-140">L'accesso è stato eseguito correttamente?</span><span class="sxs-lookup"><span data-stu-id="3c1ae-140">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="3c1ae-141">È possibile esaminare i dettagli facendo clic su una data o posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-141">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="3c1ae-142">**Utenti univoci per ogni app**: ottenere una visualizzazione di tutti gli utenti univoci che usano un'app specifica.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-142">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="3c1ae-143">Comprende solo gli utenti che hanno completato "*correttamente*" l'accesso a un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-143">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="3c1ae-144">**Accessi dei dispositivi**: visualizzazione del tipo del sistema operativo e dei browser usati dagli utenti dell'organizzazione con informazioni dettagliate sugli utenti stessi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-144">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="3c1ae-145">User Name</span><span class="sxs-lookup"><span data-stu-id="3c1ae-145">User Name</span></span>
- <span data-ttu-id="3c1ae-146">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="3c1ae-146">IP Address</span></span>
- <span data-ttu-id="3c1ae-147">Località</span><span class="sxs-lookup"><span data-stu-id="3c1ae-147">Location</span></span> 
- <span data-ttu-id="3c1ae-148">Stato accesso</span><span class="sxs-lookup"><span data-stu-id="3c1ae-148">Sign-in status</span></span> 

<span data-ttu-id="3c1ae-149">Con questo report è possibile comprendere i diversi profili dei dispositivi usati all'interno dell'organizzazione e determinare i criteri dei dispositivi in base alle funzioni usate</span><span class="sxs-lookup"><span data-stu-id="3c1ae-149">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="3c1ae-150">**Grafico a imbuto SSPR**: informazioni su come vengono reimpostate le password all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-150">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="3c1ae-151">È possibile ottenere informazioni sul numero di reimpostazioni delle password tentate tramite lo strumento SSPR e quante di esse hanno avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-151">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="3c1ae-152">Analizzare gli errori di reimpostazione delle password usando il grafico a imbuto SSPR e comprendere perché si sono verificati determinati errori.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-152">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="3c1ae-153">Questo report offre una comprensione più approfondita della modalità d'uso dello strumento SSPR all'interno dell'organizzazione in modo da prendere decisioni efficaci.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-153">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="3c1ae-154">Personalizzazione del pacchetto di contenuto per le attività di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c1ae-154">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="3c1ae-155">**Modificare la visualizzazione**: è possibile modificare la visualizzazione di un report facendo clic su **Modifica Report** e selezionando la visualizzazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-155">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="3c1ae-158">**Aggiungere altri campi**: è possibile aggiungere o rimuovere un campo per il report selezionando l'oggetto visivo per il quale si intende aggiungere o rimuovere il campo.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-158">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="3c1ae-159">Nell'esempio seguente viene aggiunto il campo "Stato accesso" alla vista tabella.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-159">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="3c1ae-161">**Aggiungere visualizzazioni al dashboard**: è possibile personalizzare il dashboard aggiungendo visualizzazioni personalizzate del report.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-161">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="3c1ae-162">Nell'esempio seguente, un nuovo filtro denominato "Stato di accesso" è stato aggiunto e incluso nel report.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-162">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="3c1ae-163">È stata anche modificata la visualizzazione da grafico a barre a grafico a linee. Questo nuovo oggetto visivo può essere aggiunto al dashboard.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-163">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="3c1ae-166">**Condivisione del dashboard**: dopo aver creato il contenuto desiderato, è possibile condividere il dashboard con gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-166">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="3c1ae-167">Si noti che quando si condivide il report, gli utenti possono vedere i campi selezionati nel report stesso.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-167">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="3c1ae-169">Pianificazione di un aggiornamento giornaliero dei report di Power BI</span><span class="sxs-lookup"><span data-stu-id="3c1ae-169">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="3c1ae-170">Per pianificare un aggiornamento giornaliero dei report di Power BI, passare a **Set di dati > Impostazioni > Pianifica aggiornamenti** e procedere come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-170">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="3c1ae-172">Aggiornamento alla versione più recente del pacchetto di contenuto</span><span class="sxs-lookup"><span data-stu-id="3c1ae-172">Updating to newer version of content pack</span></span>

<span data-ttu-id="3c1ae-173">Se si vuole aggiornare il pacchetto di contenuto per ottenere una versione più recente:</span><span class="sxs-lookup"><span data-stu-id="3c1ae-173">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="3c1ae-174">Scaricare il nuovo pacchetto di contenuto e configurarlo in base alle istruzioni riportate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-174">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="3c1ae-175">Dopo aver configurato il pacchetto, passare a **Origine dati > Impostazioni > Credenziali origine dati** e immettere nuovamente le credenziali come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="3c1ae-175">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="3c1ae-177">Quando la nuova versione del pacchetto di contenuto è pronta per l'uso, è possibile rimuovere la versione precedente, se necessario, eliminando i report e i set di dati sottostanti associati.</span><span class="sxs-lookup"><span data-stu-id="3c1ae-177">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="3c1ae-178">Se i problemi persistono</span><span class="sxs-lookup"><span data-stu-id="3c1ae-178">Still having issues?</span></span> 

<span data-ttu-id="3c1ae-179">Vedere la [Guida per la risoluzione dei problemi](active-directory-reporting-troubleshoot-content-pack.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-179">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="3c1ae-180">Per informazioni generali su Power BI, vedere questi [articoli della Guida](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-180">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="3c1ae-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c1ae-181">Next steps</span></span>

<span data-ttu-id="3c1ae-182">Per una panoramica della creazione di report, vedere [Creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3c1ae-182">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
