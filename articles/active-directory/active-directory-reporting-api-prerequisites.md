---
title: Prerequisiti di accesso all'API di creazione report di Azure AD. | Documentazione Microsoft
description: Informazioni sui prerequisiti di accesso all'API di creazione report di Azure AD
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
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="b273d-104">Prerequisiti di accesso all'API di creazione report di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b273d-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="b273d-105">Le [API di creazione report di Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) forniscono l'accesso ai dati dal codice tramite un set di API basate su REST.</span><span class="sxs-lookup"><span data-stu-id="b273d-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b273d-106">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="b273d-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b273d-107">L'API di creazione report usa l'autenticazione [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) per autorizzare l'accesso alle API Web.</span><span class="sxs-lookup"><span data-stu-id="b273d-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="b273d-108">Per preparare l'accesso all'API di creazione report, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b273d-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="b273d-109">Creare un'applicazione nel tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b273d-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="b273d-110">Concedere le autorizzazioni appropriate all'applicazione per l'accesso ai dati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b273d-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="b273d-111">Raccogliere le impostazioni di configurazione dalla directory</span><span class="sxs-lookup"><span data-stu-id="b273d-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="b273d-112">Per domande, problemi o suggerimenti, contattare la [Guida per la creazione di report AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b273d-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="b273d-113">Creare un'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="b273d-113">Create an Azure AD application</span></span>
<span data-ttu-id="b273d-114">Per configurare la directory per l'accesso all'API di creazione report di Azure AD, è necessario accedere al portale di gestione con un account di amministratore di sottoscrizione di Azure che è anche membro del ruolo di directory Amministratore globale nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b273d-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b273d-115">Le applicazioni eseguite con credenziali con privilegi "admin" come questa possono essere molto potenti, quindi assicurarsi di proteggere l'ID e il segreto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b273d-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="b273d-116">Nel [portale di Azure classico](https://manage.windowsazure.com)fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b273d-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b273d-118">Nell'elenco **Active Directory** selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="b273d-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b273d-119">Scegliere **Applicazioni**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="b273d-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b273d-121">Nella barra inferiore fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b273d-121">On the bottom bar, click **Add**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="b273d-123">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="b273d-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="b273d-125">Nella finestra di dialogo **Informazioni sull'applicazione** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b273d-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="b273d-127">a.</span><span class="sxs-lookup"><span data-stu-id="b273d-127">a.</span></span> <span data-ttu-id="b273d-128">Nella casella di testo **Nome** digitare un nome (ad esempio: Applicazione dell'API di creazione report).</span><span class="sxs-lookup"><span data-stu-id="b273d-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="b273d-129">b.</span><span class="sxs-lookup"><span data-stu-id="b273d-129">b.</span></span> <span data-ttu-id="b273d-130">Selezionare **Applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="b273d-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="b273d-131">c.</span><span class="sxs-lookup"><span data-stu-id="b273d-131">c.</span></span> <span data-ttu-id="b273d-132">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b273d-132">Click **Next**.</span></span>
7. <span data-ttu-id="b273d-133">Nella finestra di dialogo **Proprietà dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b273d-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="b273d-135">a.</span><span class="sxs-lookup"><span data-stu-id="b273d-135">a.</span></span> <span data-ttu-id="b273d-136">Nella casella di testo **URL di accesso** digitare `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="b273d-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="b273d-137">b.</span><span class="sxs-lookup"><span data-stu-id="b273d-137">b.</span></span> <span data-ttu-id="b273d-138">Nella casella di testo **URI ID app** digitare ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="b273d-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="b273d-139">c.</span><span class="sxs-lookup"><span data-stu-id="b273d-139">c.</span></span> <span data-ttu-id="b273d-140">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="b273d-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="b273d-141">Concedere all'applicazione le autorizzazioni per l'uso dell'API</span><span class="sxs-lookup"><span data-stu-id="b273d-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="b273d-142">Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b273d-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b273d-144">Nell'elenco **Active Directory** selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="b273d-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b273d-145">Scegliere **Applicazioni**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="b273d-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="b273d-147">Nell'elenco delle applicazioni selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="b273d-147">In the applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b273d-149">Nel menu in alto fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="b273d-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b273d-151">Nella sezione **Autorizzazioni per altre applicazioni** per la risorsa **Azure Active Directory** fare clic sull'elenco a discesa **Autorizzazioni applicazione** e selezionare **Lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="b273d-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="b273d-153">Nella barra inferiore fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b273d-153">On the bottom bar, click **Save**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="b273d-155">Raccogliere le impostazioni di configurazione dalla directory</span><span class="sxs-lookup"><span data-stu-id="b273d-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="b273d-156">Questa sezione illustra come ottenere le impostazioni seguenti dalla directory:</span><span class="sxs-lookup"><span data-stu-id="b273d-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="b273d-157">Nome di dominio</span><span class="sxs-lookup"><span data-stu-id="b273d-157">Domain name</span></span>
* <span data-ttu-id="b273d-158">ID client</span><span class="sxs-lookup"><span data-stu-id="b273d-158">Client ID</span></span>
* <span data-ttu-id="b273d-159">Segreto client</span><span class="sxs-lookup"><span data-stu-id="b273d-159">Client secret</span></span>

<span data-ttu-id="b273d-160">Questi valori sono necessari quando si configurano le chiamate all'API di creazione report.</span><span class="sxs-lookup"><span data-stu-id="b273d-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="b273d-161">Ottenere il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="b273d-161">Get your domain name</span></span>
1. <span data-ttu-id="b273d-162">Nel [portale di Azure classico](https://manage.windowsazure.com)fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b273d-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b273d-164">Nell'elenco **Active Directory** selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="b273d-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b273d-165">Nel menu in alto fare clic su **Domini**.</span><span class="sxs-lookup"><span data-stu-id="b273d-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="b273d-167">Nella colonna **Nome di dominio** copiare il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="b273d-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="b273d-169">Ottenere l'ID client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b273d-169">Get the application's client ID</span></span>
1. <span data-ttu-id="b273d-170">Nel [portale di Azure classico](https://manage.windowsazure.com)fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b273d-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b273d-172">Nell'elenco **Active Directory** selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="b273d-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b273d-173">Scegliere **Applicazioni**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="b273d-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b273d-175">Nell'elenco delle applicazioni selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="b273d-175">In the applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b273d-177">Nel menu in alto fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="b273d-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b273d-179">Copiare l' **ID client**.</span><span class="sxs-lookup"><span data-stu-id="b273d-179">Copy your **Client ID**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="b273d-181">Ottenere il segreto client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b273d-181">Get the application's client secret</span></span>
<span data-ttu-id="b273d-182">Per ottenere il segreto client dell'applicazione, è necessario creare una nuova chiave e salvare il relativo valore durante il salvataggio della nuova chiave perché non è più possibile recuperare il valore in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b273d-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="b273d-183">Nel [portale di Azure classico](https://manage.windowsazure.com)fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b273d-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b273d-185">Nell'elenco **Active Directory** selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="b273d-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b273d-186">Scegliere **Applicazioni**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="b273d-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b273d-188">Nell'elenco delle applicazioni selezionare l'applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="b273d-188">In the applications list, select your newly created application.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b273d-190">Nel menu in alto fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="b273d-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b273d-192">Nella sezione **Chiavi** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b273d-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="b273d-194">a.</span><span class="sxs-lookup"><span data-stu-id="b273d-194">a.</span></span> <span data-ttu-id="b273d-195">Nell'elenco delle durate selezionare una durata</span><span class="sxs-lookup"><span data-stu-id="b273d-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="b273d-196">b.</span><span class="sxs-lookup"><span data-stu-id="b273d-196">b.</span></span> <span data-ttu-id="b273d-197">Nella barra inferiore fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b273d-197">On the bottom bar, click **Save**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="b273d-199">c.</span><span class="sxs-lookup"><span data-stu-id="b273d-199">c.</span></span> <span data-ttu-id="b273d-200">Copiare il valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="b273d-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b273d-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b273d-201">Next Steps</span></span>
* <span data-ttu-id="b273d-202">Si desidera accedere ai dati dall'API di creazione report di Azure AD mediante il codice?</span><span class="sxs-lookup"><span data-stu-id="b273d-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="b273d-203">Vedere [Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b273d-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="b273d-204">Per altre informazioni sulla creazione di report di Azure Active Directory, vedere [Guida alla creazione di report in Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b273d-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

