---
title: Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph | Documentazione Microsoft
description: Fornisce un'introduzione all'esecuzione di query su Microsoft Graph per ottenere un elenco di eventi di rischio e le relative informazioni da Azure Active Directory.
services: active-directory
keywords: "azure active directory identity protection, evento di rischio, vulnerabilità, criteri di sicurezza, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="a03b6-104">Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a03b6-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="a03b6-105">Microsoft Graph è l'endpoint API unificato di Microsoft e la posizione in cui risiedono le API di [Azure Active Directory Identity Protection](active-directory-identityprotection.md) .</span><span class="sxs-lookup"><span data-stu-id="a03b6-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="a03b6-106">La prima API, **identityRiskEvents**, consente di eseguire una query in Microsoft Graph per ottenere un elenco di [eventi di rischio](active-directory-identityprotection-risk-events-types.md) e informazioni associate.</span><span class="sxs-lookup"><span data-stu-id="a03b6-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="a03b6-107">Questo articolo fornisce un'introduzione all'esecuzione di query su questa API.</span><span class="sxs-lookup"><span data-stu-id="a03b6-107">This article gets you started querying this API.</span></span> <span data-ttu-id="a03b6-108">Per una presentazione più approfondita, la documentazione completa e l'accesso a Graph Explorer, vedere il [sito di Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="a03b6-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a03b6-109">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="a03b6-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="a03b6-110">Per l'accesso ai dati di Identity Protection tramite Microsoft Graph sono disponibili tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="a03b6-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="a03b6-111">Aggiungere un'applicazione con un segreto client.</span><span class="sxs-lookup"><span data-stu-id="a03b6-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="a03b6-112">Usare questo segreto e qualche altra informazione per eseguire l'autenticazione in Microsoft Graph, dove si riceverà un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a03b6-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="a03b6-113">Usare questo token per inviare richieste all'endpoint API e ottenere dati di Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="a03b6-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="a03b6-114">Ecco gli elementi che occorre avere prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="a03b6-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="a03b6-115">Privilegi di amministratore per creare l'applicazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a03b6-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="a03b6-116">Nome di dominio del tenant, ad esempio contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="a03b6-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="a03b6-117">Aggiungere un'applicazione con un segreto client</span><span class="sxs-lookup"><span data-stu-id="a03b6-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="a03b6-118">[Accedere](https://manage.windowsazure.com) al portale di Azure classico come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a03b6-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="a03b6-119">Nel riquadro di spostamento sinistro fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="a03b6-121">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="a03b6-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="a03b6-122">Scegliere **Applicazioni**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="a03b6-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="a03b6-124">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="a03b6-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="a03b6-126">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="a03b6-128">Nella finestra di dialogo **Informazioni sull'applicazione** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a03b6-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="a03b6-130">a.</span><span class="sxs-lookup"><span data-stu-id="a03b6-130">a.</span></span> <span data-ttu-id="a03b6-131">Nella casella di testo **Nome** digitare un nome per l'applicazione, ad esempio Applicazione API evento di rischio AADIP.</span><span class="sxs-lookup"><span data-stu-id="a03b6-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="a03b6-132">b.</span><span class="sxs-lookup"><span data-stu-id="a03b6-132">b.</span></span> <span data-ttu-id="a03b6-133">Come **Tipo** selezionare **Applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="a03b6-134">c.</span><span class="sxs-lookup"><span data-stu-id="a03b6-134">c.</span></span> <span data-ttu-id="a03b6-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-135">Click **Next**.</span></span>
8. <span data-ttu-id="a03b6-136">Nella finestra di dialogo **Proprietà dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a03b6-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="a03b6-138">a.</span><span class="sxs-lookup"><span data-stu-id="a03b6-138">a.</span></span> <span data-ttu-id="a03b6-139">Nella casella di testo **URL di accesso** digitare `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="a03b6-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="a03b6-140">b.</span><span class="sxs-lookup"><span data-stu-id="a03b6-140">b.</span></span> <span data-ttu-id="a03b6-141">Nella casella di testo **URI ID app** digitare `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="a03b6-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="a03b6-142">c.</span><span class="sxs-lookup"><span data-stu-id="a03b6-142">c.</span></span> <span data-ttu-id="a03b6-143">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-143">Click **Complete**.</span></span>

<span data-ttu-id="a03b6-144">A questo punto è possibile configurare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a03b6-144">Your can now configure your application.</span></span>

![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="a03b6-146">Concedere all'applicazione le autorizzazioni per l'uso dell'API</span><span class="sxs-lookup"><span data-stu-id="a03b6-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="a03b6-147">Nella pagina dell'applicazione scegliere **Configura**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="a03b6-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="a03b6-149">Nella sezione **Autorizzazioni per altre applicazioni** fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="a03b6-151">Nella finestra di dialogo **Autorizzazioni per altre applicazioni** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a03b6-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="a03b6-153">a.</span><span class="sxs-lookup"><span data-stu-id="a03b6-153">a.</span></span> <span data-ttu-id="a03b6-154">Selezionare **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="a03b6-155">b.</span><span class="sxs-lookup"><span data-stu-id="a03b6-155">b.</span></span> <span data-ttu-id="a03b6-156">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-156">Click **Complete**.</span></span>
4. <span data-ttu-id="a03b6-157">Fare clic su **Autorizzazioni applicazione: 0** e quindi selezionare **Legge tutte le informazioni sugli eventi di rischio dell'identità**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="a03b6-159">Fare clic su **Salva** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="a03b6-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="a03b6-161">Ottenere una chiave di accesso</span><span class="sxs-lookup"><span data-stu-id="a03b6-161">Get an access key</span></span>
1. <span data-ttu-id="a03b6-162">Nella sezione **Chiavi** della pagina dell'applicazione selezionare 1 anno come durata.</span><span class="sxs-lookup"><span data-stu-id="a03b6-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="a03b6-164">Fare clic su **Salva** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="a03b6-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="a03b6-166">Nella sezione Chiavi copiare il valore della chiave appena creata e quindi incollarla in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="a03b6-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="a03b6-168">Se si perde la chiave, si dovrà tornare a questa sezione e crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="a03b6-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="a03b6-169">Mantenere la chiave segreta, perché chiunque ne fosse a conoscenza potrà accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="a03b6-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="a03b6-170">Nella sezione **Proprietà** copiare l'**ID client** e conservarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="a03b6-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="a03b6-171">Autenticarsi in Microsoft Graph ed eseguire query sull'API eventi di rischio per le identità</span><span class="sxs-lookup"><span data-stu-id="a03b6-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="a03b6-172">A questo punto saranno disponibili:</span><span class="sxs-lookup"><span data-stu-id="a03b6-172">At this point, you should have:</span></span>

* <span data-ttu-id="a03b6-173">L'ID client copiato in precedenza</span><span class="sxs-lookup"><span data-stu-id="a03b6-173">The client ID you copied above</span></span>
* <span data-ttu-id="a03b6-174">La chiave copiata in precedenza</span><span class="sxs-lookup"><span data-stu-id="a03b6-174">The key you copied above</span></span>
* <span data-ttu-id="a03b6-175">Il nome di dominio del tenant</span><span class="sxs-lookup"><span data-stu-id="a03b6-175">The name of your tenant's domain</span></span>

<span data-ttu-id="a03b6-176">Per autenticarsi, inviare una richiesta POST a `https://login.microsoft.com` includendo nel corpo i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="a03b6-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="a03b6-177">grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="a03b6-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="a03b6-178">resource: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="a03b6-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="a03b6-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="a03b6-179">client_id: <your client ID></span></span>
* <span data-ttu-id="a03b6-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="a03b6-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="a03b6-181">È necessario fornire i valori per i parametri **client_id** e **client_secret**.</span><span class="sxs-lookup"><span data-stu-id="a03b6-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="a03b6-182">Se la richiesta riesce, verrà restituito un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a03b6-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="a03b6-183">Per chiamare l'API, creare un'intestazione con il parametro seguente:</span><span class="sxs-lookup"><span data-stu-id="a03b6-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="a03b6-184">Quando si esegue l'autenticazione, è possibile trovare il tipo di token e il token di accesso nel token restituito.</span><span class="sxs-lookup"><span data-stu-id="a03b6-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="a03b6-185">Inviare questa intestazione come richiesta all'URL dell'API seguente: `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="a03b6-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="a03b6-186">La risposta, se la richiesta riesce, è una raccolta di eventi di rischio per le identità e di dati associati nel formato JSON OData, che può essere analizzato e gestito secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="a03b6-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="a03b6-187">Ecco il codice di esempio per autenticarsi e chiamare l'API con Powershell.</span><span class="sxs-lookup"><span data-stu-id="a03b6-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="a03b6-188">Aggiungere semplicemente l'ID client, la chiave e il dominio del tenant.</span><span class="sxs-lookup"><span data-stu-id="a03b6-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="a03b6-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a03b6-189">Next steps</span></span>
<span data-ttu-id="a03b6-190">È appena stata creata la prima chiamata a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a03b6-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="a03b6-191">Ora è possibile eseguire query per ottenere un elenco di eventi di rischio per le identità e usare i dati come si preferisce.</span><span class="sxs-lookup"><span data-stu-id="a03b6-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="a03b6-192">Per altre informazioni su Microsoft Graph e su come creare applicazioni usando l'API Graph, vedere la [documentazione](https://graph.microsoft.io/docs) e molto altro nel [sito di Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="a03b6-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="a03b6-193">Assicurarsi inoltre di creare un segnalibro alla pagina dell'API [Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) che include l'elenco di tutte le API Identity Protection disponibili in Graph.</span><span class="sxs-lookup"><span data-stu-id="a03b6-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="a03b6-194">In questa pagina sono visualizzate le nuove modalità aggiunte via via per l'utilizzo di Identity Protection tramite l'API.</span><span class="sxs-lookup"><span data-stu-id="a03b6-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a03b6-195">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a03b6-195">Additional resources</span></span>
* [<span data-ttu-id="a03b6-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a03b6-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="a03b6-197">Tipi di eventi di rischio rilevati da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a03b6-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="a03b6-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a03b6-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="a03b6-199">Overview of Microsoft Graph (Panoramica di Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="a03b6-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="a03b6-200">Azure AD Identity Protection Service Root (Radice del servizio Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a03b6-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

