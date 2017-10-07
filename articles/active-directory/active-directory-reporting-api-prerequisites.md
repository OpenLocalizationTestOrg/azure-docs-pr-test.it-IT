---
title: aaaPrerequisites tooaccess hello Azure AD reporting API. | Microsoft Docs
description: Informazioni sulle API reporting di hello prerequisiti tooaccess hello Azure AD
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="feb4e-104">Prerequisiti tooaccess hello Azure AD API di creazione di report</span><span class="sxs-lookup"><span data-stu-id="feb4e-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="feb4e-105">Hello [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornire i dati di toohello accesso a livello di codice tramite un set di API basata su REST.</span><span class="sxs-lookup"><span data-stu-id="feb4e-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="feb4e-106">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="feb4e-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="feb4e-107">Hello reporting Usa API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web toohello di tooauthorize accesso API.</span><span class="sxs-lookup"><span data-stu-id="feb4e-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="feb4e-108">tooprepare toohello l'accesso API di report, è necessario:</span><span class="sxs-lookup"><span data-stu-id="feb4e-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="feb4e-109">Creare un'applicazione nel tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="feb4e-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="feb4e-110">GRANT hello applicazione delle autorizzazioni appropriate tooaccess hello dati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="feb4e-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="feb4e-111">Raccogliere le impostazioni di configurazione dalla directory</span><span class="sxs-lookup"><span data-stu-id="feb4e-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="feb4e-112">Per domande, problemi o suggerimenti, contattare la [Guida per la creazione di report AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="feb4e-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="feb4e-113">Creare un'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="feb4e-113">Create an Azure AD application</span></span>
<span data-ttu-id="feb4e-114">tooconfigure la directory tooaccess hello Azure AD reporting API, è necessario accedere toohello portale di Azure classico con un account di amministratore di sottoscrizione di Azure che è anche un membro del ruolo della directory hello amministratore globale nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="feb4e-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="feb4e-115">Le applicazioni in esecuzione con le credenziali con privilegi "admin" simile al seguente possono essere molto potente, pertanto essere protetto le credenziali ID/chiave privata che tookeep hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="feb4e-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="feb4e-116">In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="feb4e-118">Da hello **active directory** elenco, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="feb4e-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="feb4e-119">Scegliere dal menu hello in primo piano hello **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="feb4e-121">Nella barra inferiore hello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="feb4e-123">In hello **cosa si desidera toodo?** finestra di dialogo, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="feb4e-125">In hello **informazioni sull'applicazione** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="feb4e-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="feb4e-127">a.</span><span class="sxs-lookup"><span data-stu-id="feb4e-127">a.</span></span> <span data-ttu-id="feb4e-128">In hello **nome** casella di testo, digitare un nome (ad esempio: applicazione di Reporting API).</span><span class="sxs-lookup"><span data-stu-id="feb4e-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="feb4e-129">b.</span><span class="sxs-lookup"><span data-stu-id="feb4e-129">b.</span></span> <span data-ttu-id="feb4e-130">Selezionare **Applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="feb4e-131">c.</span><span class="sxs-lookup"><span data-stu-id="feb4e-131">c.</span></span> <span data-ttu-id="feb4e-132">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-132">Click **Next**.</span></span>
7. <span data-ttu-id="feb4e-133">In hello **proprietà App** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="feb4e-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="feb4e-135">a.</span><span class="sxs-lookup"><span data-stu-id="feb4e-135">a.</span></span> <span data-ttu-id="feb4e-136">In hello **Sign-on URL** casella tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="feb4e-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="feb4e-137">b.</span><span class="sxs-lookup"><span data-stu-id="feb4e-137">b.</span></span> <span data-ttu-id="feb4e-138">In hello **URI ID App** casella tipo ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="feb4e-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="feb4e-139">c.</span><span class="sxs-lookup"><span data-stu-id="feb4e-139">c.</span></span> <span data-ttu-id="feb4e-140">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="feb4e-141">Concedere il hello toouse di autorizzazione applicazione API</span><span class="sxs-lookup"><span data-stu-id="feb4e-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="feb4e-142">In hello [portale di Azure classico](https://manage.windowsazure.com/)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="feb4e-144">Da hello **active directory** elenco, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="feb4e-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="feb4e-145">Scegliere dal menu hello in primo piano hello **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="feb4e-147">Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="feb4e-147">In hello applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="feb4e-149">Scegliere dal menu hello in primo piano hello **configura**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="feb4e-151">In hello **autorizzazioni tooother applicazioni** sezione hello **Azure Active Directory** risorse, fare clic su hello **autorizzazioni applicazione** elenco a discesa, quindi Selezionare **lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="feb4e-153">Nella barra inferiore hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="feb4e-155">Raccogliere le impostazioni di configurazione dalla directory</span><span class="sxs-lookup"><span data-stu-id="feb4e-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="feb4e-156">In questa sezione illustra come hello tooget seguendo le impostazioni dalla directory:</span><span class="sxs-lookup"><span data-stu-id="feb4e-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="feb4e-157">Nome di dominio</span><span class="sxs-lookup"><span data-stu-id="feb4e-157">Domain name</span></span>
* <span data-ttu-id="feb4e-158">ID client</span><span class="sxs-lookup"><span data-stu-id="feb4e-158">Client ID</span></span>
* <span data-ttu-id="feb4e-159">Segreto client</span><span class="sxs-lookup"><span data-stu-id="feb4e-159">Client secret</span></span>

<span data-ttu-id="feb4e-160">Questi valori è necessario quando si configurano le chiamate API di creazione report toohello.</span><span class="sxs-lookup"><span data-stu-id="feb4e-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="feb4e-161">Ottenere il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="feb4e-161">Get your domain name</span></span>
1. <span data-ttu-id="feb4e-162">In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="feb4e-164">Da hello **active directory** elenco, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="feb4e-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="feb4e-165">Scegliere dal menu hello in primo piano hello **domini**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="feb4e-167">In hello **nome di dominio** colonna, copiare il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="feb4e-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="feb4e-169">Ottenere l'ID client dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="feb4e-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="feb4e-170">In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="feb4e-172">Da hello **active directory** elenco, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="feb4e-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="feb4e-173">Scegliere dal menu hello in primo piano hello **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="feb4e-175">Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="feb4e-175">In hello applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="feb4e-177">Scegliere dal menu hello in primo piano hello **configura**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="feb4e-179">Copiare l' **ID client**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-179">Copy your **Client ID**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="feb4e-181">Ottenere segreto client dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="feb4e-181">Get hello application's client secret</span></span>
<span data-ttu-id="feb4e-182">tooget client dell'applicazione privata, è necessario toocreate una nuova chiave e salvare il relativo valore quando si salvano nuova chiave hello perché non è possibile tooretrieve questo valore in un secondo momento più.</span><span class="sxs-lookup"><span data-stu-id="feb4e-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="feb4e-183">In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="feb4e-185">Da hello **active directory** elenco, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="feb4e-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="feb4e-186">Scegliere dal menu hello in primo piano hello **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="feb4e-188">Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="feb4e-188">In hello applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="feb4e-190">Scegliere dal menu hello in primo piano hello **configura**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="feb4e-192">In hello **chiavi** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="feb4e-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="feb4e-194">a.</span><span class="sxs-lookup"><span data-stu-id="feb4e-194">a.</span></span> <span data-ttu-id="feb4e-195">Elenco di durata hello, selezionare una durata</span><span class="sxs-lookup"><span data-stu-id="feb4e-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="feb4e-196">b.</span><span class="sxs-lookup"><span data-stu-id="feb4e-196">b.</span></span> <span data-ttu-id="feb4e-197">Nella barra inferiore hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="feb4e-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="feb4e-199">c.</span><span class="sxs-lookup"><span data-stu-id="feb4e-199">c.</span></span> <span data-ttu-id="feb4e-200">Copia valore chiave hello.</span><span class="sxs-lookup"><span data-stu-id="feb4e-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feb4e-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="feb4e-201">Next Steps</span></span>
* <span data-ttu-id="feb4e-202">È ad esempio tooaccess hello dati da Azure AD hello sarebbe reporting API in modo a livello di codice?</span><span class="sxs-lookup"><span data-stu-id="feb4e-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="feb4e-203">Estrarre [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="feb4e-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="feb4e-204">Se si desidera toofind ulteriori informazioni sui report di Azure Active Directory, vedere hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="feb4e-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

