---
title: aaaConfigure autenticazione e autorizzazione per un'applicazione personalizzata che chiama hello Azure ora serie Insights API | Documenti Microsoft
description: In questa esercitazione viene illustrato come tooconfigure autenticazione e autorizzazione per un'applicazione personalizzata che chiama hello Azure ora serie Insights API
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="7f3ba-103">Autenticazione e autorizzazione per l'API Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="7f3ba-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="7f3ba-104">In questo articolo viene illustrato come un'applicazione personalizzata che chiama tooconfigure hello Azure ora serie Insights API.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="7f3ba-105">Entità servizio</span><span class="sxs-lookup"><span data-stu-id="7f3ba-105">Service principal</span></span>

<span data-ttu-id="7f3ba-106">Questa sezione viene illustrato come tooconfigure tooaccess un'applicazione hello ora serie Insights API per conto di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="7f3ba-107">un'applicazione Hello può quindi eseguire query sui dati o pubblicare dati di riferimento nell'ambiente di tempo serie Insights hello con le credenziali dell'applicazione e non le credenziali utente hello.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="7f3ba-108">Quando si dispone di un'applicazione che richiede tooaccess ora serie Insights, è necessario configurare un'applicazione Azure Active Directory e assegnare criteri di accesso ai dati hello nell'ambiente di tempo serie Insights hello.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="7f3ba-109">Questo approccio è preferibile toorunning hello app con le proprie credenziali perché:</span><span class="sxs-lookup"><span data-stu-id="7f3ba-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="7f3ba-110">È possibile assegnare le autorizzazioni di identità app toohello che sono diverse dalle autorizzazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="7f3ba-111">In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="7f3ba-112">Ad esempio, è possibile consentire hello app tooonly leggere i dati in un ambiente di Insights di serie di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="7f3ba-113">Non si dispone delle credenziali dell'applicazione hello toochange se Modifica responsabilità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="7f3ba-114">Quando si esegue uno script automatico, è possibile utilizzare un certificato o l'autenticazione chiave tooautomate un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="7f3ba-115">Questo articolo illustra come quelli passaggi tooperform hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="7f3ba-116">Si concentra in un'applicazione single-tenant in cui un'applicazione hello è toorun previsti in una sola organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="7f3ba-117">Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="7f3ba-118">flusso di programma di installazione di Hello è costituito da tre passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="7f3ba-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="7f3ba-119">Creare un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="7f3ba-120">Autorizzare l'ambiente di applicazione tooaccess hello ora serie Insights.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="7f3ba-121">Utilizzare l'ID applicazione hello e la chiave tooacquire toohello un token `"https://api.timeseries.azure.com/"` destinatario o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="7f3ba-122">token Hello può quindi essere utilizzato toocall hello ora serie Insights API.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="7f3ba-123">Ecco i passaggi dettagliati hello:</span><span class="sxs-lookup"><span data-stu-id="7f3ba-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="7f3ba-124">Nel portale di Azure hello, selezionare **Azure Active Directory** > **registrazioni di App** > **nuova registrazione applicazione**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Registrazione di una nuova applicazione in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="7f3ba-126">Assegnare un'applicazione hello toobe di tipo un nome, selezionare hello **app Web / API**, selezionare qualsiasi URI valido per **Sign-on URL**, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Creare un'applicazione hello in Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="7f3ba-128">Selezionare l'applicazione appena creata e copiare il relativo editor di testo preferito tooyour ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Copiare l'ID dell'applicazione hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="7f3ba-130">Selezionare **chiavi**, immettere nome chiave hello, scadenza hello select e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Selezionare le chiavi dell'applicazione](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Immettere nome della chiave hello e la scadenza e fare clic su Salva](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="7f3ba-133">Editor di testo preferito tooyour chiave hello copia.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Chiave dell'applicazione hello copia](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="7f3ba-135">Per ambiente ora serie Insights hello, selezionare **i criteri di accesso dati** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Aggiungere nuovi dati accesso criteri toohello ora serie Insights ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="7f3ba-137">In hello **Seleziona utente** la finestra di dialogo, nome dell'applicazione hello Incolla (dal passaggio 2) o ID dell'applicazione (dal passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="7f3ba-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Trovare un'applicazione nella finestra di dialogo Seleziona utente hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="7f3ba-139">Ruolo selezionare hello (**lettore** per eseguire query sui dati, **collaboratore** per eseguire query sui dati e la modifica di dati di riferimento) e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Selezionare lettore o collaboratore nella finestra di dialogo selezionare il ruolo di hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="7f3ba-141">Salvare il criterio di hello facendo **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="7f3ba-142">Utilizzare l'ID dell'applicazione hello (dal passaggio 3) e token hello tooacquire chiave (dal passaggio 5) dell'applicazione per conto di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="7f3ba-143">Hello token può quindi essere passato in hello `Authorization` intestazione quando l'applicazione hello chiama hello ora serie Insights API.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="7f3ba-144">Se si usa c#, è possibile utilizzare i seguenti token hello tooacquire di codice per conto di un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="7f3ba-145">Per un esempio completo, vedere [Eseguire query sui dati tramite C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7f3ba-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="7f3ba-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f3ba-146">Next steps</span></span>

<span data-ttu-id="7f3ba-147">Utilizzare l'ID applicazione hello e la chiave nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f3ba-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="7f3ba-148">Per esempio di codice che chiama hello ora serie Insights API, vedere [eseguire query sui dati utilizzando il linguaggio c#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7f3ba-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7f3ba-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7f3ba-149">See also</span></span>

* <span data-ttu-id="7f3ba-150">[Le query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) per riferimento API di Query completo hello</span><span class="sxs-lookup"><span data-stu-id="7f3ba-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="7f3ba-151">Creare un servizio principale in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7f3ba-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
