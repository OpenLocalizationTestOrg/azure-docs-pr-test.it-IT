---
title: "aaaGet avviato con la protezione dell'identità Azure Active Directory e Microsoft Graph | Documenti Microsoft"
description: Fornisce un tooquery Introduzione Microsoft Graph per un elenco di eventi di rischio e le informazioni associate da Azure Active Directory.
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="f460c-104">Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f460c-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="f460c-105">Microsoft Graph è hello Microsoft unified endpoint API e hello home di [la protezione di Azure Active Directory identità](active-directory-identityprotection.md) API.</span><span class="sxs-lookup"><span data-stu-id="f460c-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="f460c-106">prima di Hello API, **identityRiskEvents**, consente tooquery Microsoft Graph per un elenco di [gli eventi di rischio](active-directory-identityprotection-risk-events-types.md) e informazioni associate.</span><span class="sxs-lookup"><span data-stu-id="f460c-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="f460c-107">Questo articolo fornisce un'introduzione all'esecuzione di query su questa API.</span><span class="sxs-lookup"><span data-stu-id="f460c-107">This article gets you started querying this API.</span></span> <span data-ttu-id="f460c-108">Per un'introduzione approfondita, la documentazione completa e accesso toohello Esplora grafico, vedere hello [sito Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f460c-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f460c-109">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f460c-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="f460c-110">Esistono tre i dati di protezione dell'identità tooaccessing passaggi tramite Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="f460c-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="f460c-111">Aggiungere un'applicazione con un segreto client.</span><span class="sxs-lookup"><span data-stu-id="f460c-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="f460c-112">Utilizzare il segreto e alcuni altri blocchi di informazioni tooauthenticate tooMicrosoft grafico, in cui si riceve un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f460c-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="f460c-113">Usare questo endpoint toohello API le richieste di token toomake e ottenere dati di protezione dell'identità.</span><span class="sxs-lookup"><span data-stu-id="f460c-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="f460c-114">Ecco gli elementi che occorre avere prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="f460c-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="f460c-115">Applicazione toocreate hello privilegi di amministratore in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f460c-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="f460c-116">nome Hello del dominio del tenant (ad esempio, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f460c-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="f460c-117">Aggiungere un'applicazione con un segreto client</span><span class="sxs-lookup"><span data-stu-id="f460c-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="f460c-118">[Accedi](https://manage.windowsazure.com) tooyour portale di Azure classico come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f460c-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="f460c-119">Nel riquadro di spostamento sinistro hello scegliere **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f460c-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="f460c-121">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="f460c-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="f460c-122">Scegliere dal menu hello in primo piano hello **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f460c-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="f460c-124">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f460c-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="f460c-126">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="f460c-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="f460c-128">In hello **informazioni sull'applicazione** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f460c-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="f460c-130">a.</span><span class="sxs-lookup"><span data-stu-id="f460c-130">a.</span></span> <span data-ttu-id="f460c-131">In hello **nome** casella di testo, digitare un nome per l'applicazione (ad esempio: applicazione dell'API AADIP rischio evento).</span><span class="sxs-lookup"><span data-stu-id="f460c-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="f460c-132">b.</span><span class="sxs-lookup"><span data-stu-id="f460c-132">b.</span></span> <span data-ttu-id="f460c-133">Come **Tipo** selezionare **Applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="f460c-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="f460c-134">c.</span><span class="sxs-lookup"><span data-stu-id="f460c-134">c.</span></span> <span data-ttu-id="f460c-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f460c-135">Click **Next**.</span></span>
8. <span data-ttu-id="f460c-136">In hello **proprietà App** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f460c-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="f460c-138">a.</span><span class="sxs-lookup"><span data-stu-id="f460c-138">a.</span></span> <span data-ttu-id="f460c-139">In hello **Sign-On URL** casella tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="f460c-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="f460c-140">b.</span><span class="sxs-lookup"><span data-stu-id="f460c-140">b.</span></span> <span data-ttu-id="f460c-141">In hello **URI ID App** casella tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="f460c-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="f460c-142">c.</span><span class="sxs-lookup"><span data-stu-id="f460c-142">c.</span></span> <span data-ttu-id="f460c-143">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="f460c-143">Click **Complete**.</span></span>

<span data-ttu-id="f460c-144">A questo punto è possibile configurare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f460c-144">Your can now configure your application.</span></span>

![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="f460c-146">Concedere il hello toouse di autorizzazione applicazione API</span><span class="sxs-lookup"><span data-stu-id="f460c-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="f460c-147">Nella pagina dell'applicazione, nel menu hello nella parte superiore di hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="f460c-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="f460c-149">In hello **autorizzazioni tooother applicazioni** fare clic su **aggiungere applicazione**.</span><span class="sxs-lookup"><span data-stu-id="f460c-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="f460c-151">In hello **autorizzazioni tooother applicazioni** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f460c-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="f460c-153">a.</span><span class="sxs-lookup"><span data-stu-id="f460c-153">a.</span></span> <span data-ttu-id="f460c-154">Selezionare **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="f460c-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="f460c-155">b.</span><span class="sxs-lookup"><span data-stu-id="f460c-155">b.</span></span> <span data-ttu-id="f460c-156">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f460c-156">Click **Complete**.</span></span>
4. <span data-ttu-id="f460c-157">Fare clic su **Autorizzazioni applicazione: 0** e quindi selezionare **Legge tutte le informazioni sugli eventi di rischio dell'identità**.</span><span class="sxs-lookup"><span data-stu-id="f460c-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="f460c-159">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f460c-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="f460c-161">Ottenere una chiave di accesso</span><span class="sxs-lookup"><span data-stu-id="f460c-161">Get an access key</span></span>
1. <span data-ttu-id="f460c-162">Nella pagina dell'applicazione hello **chiavi** , selezionare 1 anno come durata.</span><span class="sxs-lookup"><span data-stu-id="f460c-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="f460c-164">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f460c-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="f460c-166">Nella sezione chiavi hello, copiare il valore di hello della chiave appena creato e quindi incollarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="f460c-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Creazione di un'applicazione](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="f460c-168">Se si perde la chiave, si hanno tooreturn toothis sezione e creare una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="f460c-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="f460c-169">Mantenere la chiave segreta, perché chiunque ne fosse a conoscenza potrà accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="f460c-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="f460c-170">In hello **proprietà** sezione, hello copia **ID Client**e quindi incollarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="f460c-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="f460c-171">Autenticare tooMicrosoft grafico e hello query identità rischio eventi API</span><span class="sxs-lookup"><span data-stu-id="f460c-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="f460c-172">A questo punto saranno disponibili:</span><span class="sxs-lookup"><span data-stu-id="f460c-172">At this point, you should have:</span></span>

* <span data-ttu-id="f460c-173">ID client hello è stato copiato in precedenza</span><span class="sxs-lookup"><span data-stu-id="f460c-173">hello client ID you copied above</span></span>
* <span data-ttu-id="f460c-174">chiave di Hello che è stato copiato in precedenza</span><span class="sxs-lookup"><span data-stu-id="f460c-174">hello key you copied above</span></span>
* <span data-ttu-id="f460c-175">nome di Hello del dominio del tenant</span><span class="sxs-lookup"><span data-stu-id="f460c-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="f460c-176">tooauthenticate, inviare un post richiesta troppo`https://login.microsoft.com` con i seguenti parametri nel corpo di hello hello:</span><span class="sxs-lookup"><span data-stu-id="f460c-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="f460c-177">grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="f460c-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="f460c-178">resource: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="f460c-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="f460c-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="f460c-179">client_id: <your client ID></span></span>
* <span data-ttu-id="f460c-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="f460c-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="f460c-181">Sono necessari valori di tooprovide per hello **client_id** hello e **client_secret** parametro.</span><span class="sxs-lookup"><span data-stu-id="f460c-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="f460c-182">Se la richiesta riesce, verrà restituito un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f460c-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="f460c-183">hello toocall API, creare un'intestazione con hello seguente parametro:</span><span class="sxs-lookup"><span data-stu-id="f460c-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="f460c-184">Per l'autenticazione, è possibile trovare il tipo di token hello e token di accesso in hello ha restituito un token.</span><span class="sxs-lookup"><span data-stu-id="f460c-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="f460c-185">Inviare questa intestazione come toohello una richiesta API URL seguente:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="f460c-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="f460c-186">risposta Hello, se ha esito positivo, è una raccolta di identità rischi e i dati in formato JSON OData, che può essere analizzato e gestito secondo necessità hello associati.</span><span class="sxs-lookup"><span data-stu-id="f460c-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="f460c-187">Di seguito è riportato il codice di esempio per l'autenticazione e la chiamata API hello tramite Powershell.</span><span class="sxs-lookup"><span data-stu-id="f460c-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="f460c-188">Aggiungere semplicemente l'ID client, la chiave e il dominio del tenant.</span><span class="sxs-lookup"><span data-stu-id="f460c-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f460c-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f460c-189">Next steps</span></span>
<span data-ttu-id="f460c-190">Complimenti, il primo tooMicrosoft chiamata grafico appena creata.</span><span class="sxs-lookup"><span data-stu-id="f460c-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="f460c-191">Ora è possibile eseguire una query eventi di rischio di identità e utilizzare dati hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="f460c-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="f460c-192">toolearn ulteriori informazioni su Microsoft Graph e come applicazioni toobuild utilizzando hello API Graph, estrarre hello [documentazione](https://graph.microsoft.io/docs) e molto altro ancora su hello [sito Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f460c-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="f460c-193">Assicurarsi inoltre che hello toobookmark [API di Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) pagina che elenca tutti hello identità API di protezione disponibili nel grafico.</span><span class="sxs-lookup"><span data-stu-id="f460c-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="f460c-194">Quando si aggiungono nuovi modi toowork con la protezione dell'identità tramite l'API, si verrà visualizzato nella pagina.</span><span class="sxs-lookup"><span data-stu-id="f460c-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f460c-195">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f460c-195">Additional resources</span></span>
* [<span data-ttu-id="f460c-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f460c-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="f460c-197">Tipi di eventi di rischio rilevati da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f460c-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="f460c-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f460c-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="f460c-199">Overview of Microsoft Graph (Panoramica di Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="f460c-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="f460c-200">Azure AD Identity Protection Service Root (Radice del servizio Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="f460c-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

