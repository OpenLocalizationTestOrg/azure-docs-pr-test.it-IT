---
title: Eseguire l'autenticazione con le API REST di Mobile Engagement - installazione manuale
description: Descrive come configurare manualmente l'autenticazione per le API REST di Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="8b5b6-103">Eseguire l'autenticazione con le API REST di Mobile Engagement - installazione manuale</span><span class="sxs-lookup"><span data-stu-id="8b5b6-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="8b5b6-104">Questo è un documento in appendice per [eseguire l'autenticazione con le API REST di Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8b5b6-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="8b5b6-105">Leggerlo prima per capire il contesto.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="8b5b6-106">Il documento descrive un modo alternativo per eseguire l'installazione singola al fine di configurare l'autenticazione per le API REST di Mobile Engagement tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="8b5b6-107">Le istruzioni che seguono si basano sulla [guida di Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e sono state adattate ai requisiti per l'autenticazione per le API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="8b5b6-108">Consultare la guida per comprendere bene la seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="8b5b6-109">Accedere all'account di Azure tramite il [portale classico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="8b5b6-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="8b5b6-110">Selezionare **Active Directory** dal riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-110">Select **Active Directory** from the left pane.</span></span>
   
     ![selezionare Active Directory][1]
3. <span data-ttu-id="8b5b6-112">Scegliere la **directory predefinita di Active Directory** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![scegliere la directory][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="8b5b6-114">Questo approccio funziona solo se si utilizza la directory predefinita di Active Directory del proprio account e non funzionerà se si esegue il processo da una directory di Active Directory creata nell'account.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="8b5b6-115">Per visualizzare le applicazioni nella directory, fare clic su **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![visualizzare le applicazioni][3]
5. <span data-ttu-id="8b5b6-117">Fare clic su **AGGIUNGI**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-117">Click on **ADD**.</span></span> 
   
     ![aggiungere un'applicazione][4]
6. <span data-ttu-id="8b5b6-119">Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**</span><span class="sxs-lookup"><span data-stu-id="8b5b6-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nuova applicazione][5]
7. <span data-ttu-id="8b5b6-121">Inserire il nome dell'applicazione e selezionare il tipo di applicazione come **APPLICAZIONE WEB E/O API WEB** , quindi fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![assegnare un nome all'applicazione][6]
8. <span data-ttu-id="8b5b6-123">È possibile fornire un URL fittizio come **URL ACCESSO** e **URI ID APP**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="8b5b6-124">Questi valori non vengono usati per questo scenario e gli URL non vengono convalidati.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![proprietà dell'applicazione][7]
9. <span data-ttu-id="8b5b6-126">Alla fine della procedura si otterrà un'app AAD con il nome specificato in precedenza simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="8b5b6-127">Questo è il nome **AD\_APP\_NAME** ed è necessario prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Nome dell'applicazione][8]
10. <span data-ttu-id="8b5b6-129">Fare clic sul nome dell'applicazione, poi fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-129">Click on the app name and click on **Configure**.</span></span>
    
      ![configurare l'applicazione][9]
11. <span data-ttu-id="8b5b6-131">Prendere nota dell'ID CLIENT che verrà usato come **CLIENT\_ID** per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurare l'applicazione][10]
12. <span data-ttu-id="8b5b6-133">Scorrere fino alla sezione **Chiavi** e aggiungere una chiave preferibilmente con 2 anni di durata (scadenza), quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurare l'applicazione][11]
13. <span data-ttu-id="8b5b6-135">Copiare immediatamente il valore visualizzato per la chiave perché viene visualizzato soltanto ora e non verrà archiviato, quindi non verrà mai più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="8b5b6-136">In caso di smarrimento sarà necessario generare una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="8b5b6-137">Questo sarà il **CLIENT_SECRET** per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurare l'applicazione][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="8b5b6-139">Questa chiave scadrà alla fine della durata specificata. Ricordarsi di rinnovarla al momento opportuno, altrimenti l'autenticazione API non funzionerà più.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="8b5b6-140">È possibile anche eliminare e ricreare la chiave se si ritiene che sia stata compromessa.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="8b5b6-141">Fare ora clic sul pulsante **VISUALIZZA ENDPOINT** per aprire la finestra di dialogo **Endpoint dell'app**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="8b5b6-142">Nella finestra di dialogo Endpoint dell'app, copiare l' **ENDPOINT TOKEN OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="8b5b6-143">L'endpoint avrà il formato seguente, in cui il GUID nell'URL è il **TENANT_ID** e si deve prenderne nota:</span><span class="sxs-lookup"><span data-stu-id="8b5b6-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="8b5b6-144">A questo punto si potranno configurare le autorizzazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="8b5b6-145">A tal fine, aprire il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b5b6-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="8b5b6-146">Fare clic su **Gruppi di risorse** e individuare il gruppo di risorse **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="8b5b6-147">Fare clic sul gruppo di risorse **Mobile Engagement** e passare al pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="8b5b6-148">Fare clic su **Utenti** nel pannello Impostazioni e fare clic su **Aggiungi** per aggiungere un utente.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="8b5b6-149">Fare clic su **Selezionare un ruolo**</span><span class="sxs-lookup"><span data-stu-id="8b5b6-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="8b5b6-150">Fare clic su **Proprietario**</span><span class="sxs-lookup"><span data-stu-id="8b5b6-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="8b5b6-151">Cercare il nome dell'applicazione **AD\_APP\_NAME** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="8b5b6-152">Qui non verrà visualizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-152">You will not see this by default here.</span></span> <span data-ttu-id="8b5b6-153">Dopo aver trovato il nome, selezionarlo e fare clic su **Seleziona** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="8b5b6-154">Nel pannello **Aggiungi accesso** viene visualizzato come **1 utente, 0 gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="8b5b6-155">Fare clic su **OK** nel pannello per confermare la modifica.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="8b5b6-156">Ora la configurazione di AAD necessaria è terminata e tutto è pronto per le chiamate API.</span><span class="sxs-lookup"><span data-stu-id="8b5b6-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



