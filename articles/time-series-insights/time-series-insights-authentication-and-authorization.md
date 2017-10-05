---
title: Configurare l'autenticazione e l'autorizzazione per un'applicazione personalizzata che chiama l'API Azure Time Series Insights | Microsoft Docs
description: Questa esercitazione illustra come configurare l'autenticazione e l'autorizzazione per un'applicazione personalizzata che chiama l'API Azure Time Series Insights
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
ms.openlocfilehash: 4dd4865dc556e09a31d2cb7a32768aeb19ba9900
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="25a78-103">Autenticazione e autorizzazione per l'API Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="25a78-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="25a78-104">Questo articolo illustra come configurare un'applicazione personalizzata che chiama l'API Azure Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-104">This article explains how to configure a custom application that calls the Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="25a78-105">Entità servizio</span><span class="sxs-lookup"><span data-stu-id="25a78-105">Service principal</span></span>

<span data-ttu-id="25a78-106">Questa sezione illustra come configurare un'applicazione per accedere all'API Time Series Insights per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-106">This section explains how to configure an application to access the Time Series Insights API on behalf of the application.</span></span> <span data-ttu-id="25a78-107">L'applicazione può quindi eseguire query sui dati o pubblicare dati di riferimento nell'ambiente Time Series Insights con le credenziali dell'applicazione e non con quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="25a78-107">The application can then query data or publish reference data in the Time Series Insights environment with application credentials and not the user credentials.</span></span>

<span data-ttu-id="25a78-108">Quando un'applicazione deve accedere a Time Series Insights, è necessario configurare un'applicazione Azure Active Directory a cui assegnare i criteri di accesso ai dati nell'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-108">When you have an application that needs to access Time Series Insights, you must set up an Azure Active Directory application and assign the data access policies in the Time Series Insights environment.</span></span> <span data-ttu-id="25a78-109">Questo approccio è preferibile all'esecuzione dell'app con le credenziali dell'utente per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25a78-109">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="25a78-110">È possibile assegnare all'identità dell'app autorizzazioni diverse rispetto a quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="25a78-110">You can assign permissions to the app identity that are different from your own permissions.</span></span> <span data-ttu-id="25a78-111">Tali autorizzazioni sono in genere limitate alle specifiche operazioni che devono essere eseguite dall'app.</span><span class="sxs-lookup"><span data-stu-id="25a78-111">Typically, these permissions are restricted to exactly what the app needs to do.</span></span> <span data-ttu-id="25a78-112">Ad esempio, è possibile consentire all'app solo di leggere i dati in un particolare ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-112">For example, you can allow the app to only read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="25a78-113">Non è necessario modificare le credenziali dell'app in caso di cambiamento delle responsabilità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="25a78-113">You don't have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="25a78-114">È possibile usare un certificato o una chiave dell'applicazione per automatizzare l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="25a78-114">You can use a certificate or an application key to automate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="25a78-115">Questo articolo illustra come eseguire questa procedura tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25a78-115">This article shows you how to perform those steps through the Azure portal.</span></span> <span data-ttu-id="25a78-116">È incentrato su un'applicazione con un tenant singolo dove si prevede che l'applicazione venga eseguita all'interno di una sola organizzazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-116">It focuses on a single-tenant application where the application is intended to run in only one organization.</span></span> <span data-ttu-id="25a78-117">Le applicazioni con un tenant singolo si usano in genere per applicazioni line-of-business eseguite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="25a78-118">Il flusso di configurazione è costituito da tre passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="25a78-118">The setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="25a78-119">Creare un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25a78-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="25a78-120">Autorizzare questa applicazione ad accedere all'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-120">Authorize this application to access the Time Series Insights environment.</span></span>
3. <span data-ttu-id="25a78-121">Usare l'ID e la chiave dell'applicazione per acquisire un token per un destinatario o una risorsa `"https://api.timeseries.azure.com/"`.</span><span class="sxs-lookup"><span data-stu-id="25a78-121">Use the application ID and key to acquire a token to the `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="25a78-122">Il token può quindi essere usato per chiamare l'API Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-122">The token can then be used to call the Time Series Insights API.</span></span>

<span data-ttu-id="25a78-123">Ecco di seguito i passaggi dettagliati:</span><span class="sxs-lookup"><span data-stu-id="25a78-123">Here are the detailed steps:</span></span>

1. <span data-ttu-id="25a78-124">Nel portale di Azure selezionare **Azure Active Directory** > **Registrazioni per l'app** > **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="25a78-124">In the Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Registrazione di una nuova applicazione in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="25a78-126">Assegnare un nome all'applicazione, selezionare il tipo **App Web/API**, selezionare un URI valido in **URL di accesso** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="25a78-126">Give the application a name, select the type to be **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Creare l'applicazione in Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="25a78-128">Selezionare l'applicazione appena creata e copiare il relativo ID in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="25a78-128">Select your newly created application and copy its application ID to your favorite text editor.</span></span>

   ![Copiare l'ID applicazione](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="25a78-130">Selezionare **Chiavi**, immettere il nome della chiave, selezionare la scadenza e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="25a78-130">Select **Keys**, enter the key name, select the expiration, and click **Save**.</span></span>

   ![Selezionare le chiavi dell'applicazione](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Immettere il nome e la scadenza della chiave e fare clic su Salva](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="25a78-133">Copiare la chiave in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="25a78-133">Copy the key to your favorite text editor.</span></span>

   ![Copiare la chiave dell'applicazione](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="25a78-135">Per l'ambiente Time Series Insights, selezionare **Criteri di accesso ai dati** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="25a78-135">For the Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Aggiungere nuovi criteri di accesso ai dati per l'ambiente Time Series Insights](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="25a78-137">Nella finestra di dialogo **Seleziona utente** incollare il nome dell'applicazione (dal passaggio 2) o l'ID dell'applicazione (dal passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="25a78-137">In the **Select User** dialog box, paste the application name (from step 2) or application ID (from step 3).</span></span>

   ![Trovare un'applicazione nella finestra di dialogo Seleziona utente](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="25a78-139">Selezionare il ruolo (**Lettore** per eseguire query sui dati, **Collaboratore** per eseguire query sui dati e modificare i dati di riferimento) e fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="25a78-139">Select the role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Selezionare Lettore o Collaboratore nella finestra di dialogo Selezionare un ruolo](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="25a78-141">Salvare il criterio facendo clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="25a78-141">Save the policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="25a78-142">Usare l'ID dell'applicazione (dal passaggio 3) e la chiave dell'applicazione (dal passaggio 5) per acquisire il token per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-142">Use the application ID (from step 3) and application key (from step 5) to acquire the token on behalf of the application.</span></span> <span data-ttu-id="25a78-143">Il token può quindi essere passato nell'intestazione `Authorization` quando l'applicazione chiama l'API Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="25a78-143">The token can then be passed in the `Authorization` header when the application calls the Time Series Insights API.</span></span>

    <span data-ttu-id="25a78-144">Se si usa C#, è possibile usare il codice seguente per acquisire il token per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-144">If you're using C#, you can use the following code to acquire the token on behalf of the application.</span></span> <span data-ttu-id="25a78-145">Per un esempio completo, vedere [Eseguire query sui dati tramite C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="25a78-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set the resource URI to the Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of the application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="25a78-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25a78-146">Next steps</span></span>

<span data-ttu-id="25a78-147">Usare l'ID e la chiave dell'applicazione nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="25a78-147">Use the application ID and key in your application.</span></span> <span data-ttu-id="25a78-148">Per un esempio di codice che chiama l'API Time Series Insights, vedere [Eseguire query sui dati tramite C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="25a78-148">For sample code that calls the Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="25a78-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="25a78-149">See also</span></span>

* <span data-ttu-id="25a78-150">[API di query](/rest/api/time-series-insights/time-series-insights-reference-queryapi) per informazioni di riferimento complete sulle API di query</span><span class="sxs-lookup"><span data-stu-id="25a78-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for the full Query API reference</span></span>
* [<span data-ttu-id="25a78-151">Creare un'entità servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25a78-151">Create a service principal in the Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
