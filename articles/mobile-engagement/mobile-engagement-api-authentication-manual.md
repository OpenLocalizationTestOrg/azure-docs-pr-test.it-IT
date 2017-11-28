---
title: aaaAuthenticate con l'API REST di Engagement Mobile - installazione manuale
description: Viene descritto come toomanually impostare l'autenticazione per le API REST di Engagement Mobile
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
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="7548d-103">Eseguire l'autenticazione con le API REST di Mobile Engagement - installazione manuale</span><span class="sxs-lookup"><span data-stu-id="7548d-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="7548d-104">Questa è troppo documentazione un'appendice[eseguire l'autenticazione con le API REST di Engagement Mobile](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7548d-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="7548d-105">Assicurarsi di che leggere il primo contesto di hello tooget.</span><span class="sxs-lookup"><span data-stu-id="7548d-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="7548d-106">Descrive un modo alternativo toodo hello iniziali di configurazione per configurare l'autenticazione per utilizzando le API REST di Engagement Mobile hello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7548d-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="7548d-107">istruzioni di Hello seguenti si basano su questo [Guida di Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e personalizzato per ciò che è richiesto per l'autenticazione per le API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7548d-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="7548d-108">Se si desidera toounderstand hello procedura in modo dettagliato, fare riferimento tooit.</span><span class="sxs-lookup"><span data-stu-id="7548d-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="7548d-109">Account di accesso tooyour Account Azure tramite hello [portale classico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="7548d-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="7548d-110">Selezionare **Active Directory** hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="7548d-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![selezionare Active Directory][1]
3. <span data-ttu-id="7548d-112">Scegliere hello **predefinita Active Directory** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7548d-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![scegliere la directory][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="7548d-114">Questo approccio funziona solo quando si utilizza predefinito hello Active Directory del proprio account e non funzionerà se si esegue questo in Active Directory creati nell'account.</span><span class="sxs-lookup"><span data-stu-id="7548d-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="7548d-115">applicazioni di hello tooview nella directory, fare clic su **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7548d-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![visualizzare le applicazioni][3]
5. <span data-ttu-id="7548d-117">Fare clic su **AGGIUNGI**.</span><span class="sxs-lookup"><span data-stu-id="7548d-117">Click on **ADD**.</span></span> 
   
     ![aggiungere un'applicazione][4]
6. <span data-ttu-id="7548d-119">Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**</span><span class="sxs-lookup"><span data-stu-id="7548d-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nuova applicazione][5]
7. <span data-ttu-id="7548d-121">Nome dell'applicazione hello e tipo hello selezionare applicazione come **applicazione WEB, e/o API WEB** e fare clic sul pulsante Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="7548d-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![assegnare un nome all'applicazione][6]
8. <span data-ttu-id="7548d-123">È possibile fornire un URL fittizio come **URL ACCESSO** e **URI ID APP**.</span><span class="sxs-lookup"><span data-stu-id="7548d-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="7548d-124">Non vengono usati per questo scenario e gli URL di hello stessi non vengono convalidati.</span><span class="sxs-lookup"><span data-stu-id="7548d-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![proprietà dell'applicazione][7]
9. <span data-ttu-id="7548d-126">Alla fine di hello di questo, si avrà un'app di Azure ad con nome hello che seguente hello fornite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7548d-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="7548d-127">Questo è il nome **AD\_APP\_NAME** ed è necessario prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="7548d-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Nome dell'applicazione][8]
10. <span data-ttu-id="7548d-129">Fare clic sul nome dell'applicazione hello e fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="7548d-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![configurare l'applicazione][9]
11. <span data-ttu-id="7548d-131">Prendere nota dell'ID CLIENT che verrà utilizzato come hello **CLIENT\_ID** per l'API chiamate.</span><span class="sxs-lookup"><span data-stu-id="7548d-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurare l'applicazione][10]
12. <span data-ttu-id="7548d-133">Scorrere verso il basso toohello **chiavi** sezione e aggiungere una chiave con preferibilmente la durata di 2 anni (scadenza) e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7548d-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurare l'applicazione][11]
13. <span data-ttu-id="7548d-135">Copiare immediatamente valore hello mostrato per la chiave di hello poiché viene visualizzata solo ora e non verrà archiviato in modo non verranno mai più visualizzati.</span><span class="sxs-lookup"><span data-stu-id="7548d-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="7548d-136">In caso di smarrimento sarà necessario toogenerate una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="7548d-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="7548d-137">Si tratterà hello **CLIENT_SECRET** per l'API chiamate.</span><span class="sxs-lookup"><span data-stu-id="7548d-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurare l'applicazione][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="7548d-139">Questa chiave scadrà alla fine di hello della durata di hello specificato toorenew Assicurarsi pertanto di verificare al momento di hello in caso contrario l'autenticazione di API non funzionerà più.</span><span class="sxs-lookup"><span data-stu-id="7548d-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="7548d-140">È possibile anche eliminare e ricreare la chiave se si ritiene che sia stata compromessa.</span><span class="sxs-lookup"><span data-stu-id="7548d-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="7548d-141">Fare clic su **Visualizza endpoint** pulsante che viene ora visualizzato hello **endpoint dell'App** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7548d-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="7548d-142">Nella finestra di dialogo endpoint dell'App hello copiare hello **ENDPOINT TOKEN OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7548d-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="7548d-143">Questo endpoint sarà nel seguente formato in cui hello GUID nell'URL hello è hello il **TENANT_ID** quindi prendere nota di esso:</span><span class="sxs-lookup"><span data-stu-id="7548d-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="7548d-144">Si procederà ora le autorizzazioni di hello tooconfigure per questa app.</span><span class="sxs-lookup"><span data-stu-id="7548d-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="7548d-145">Per questo oggetto è tooopen backup hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7548d-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="7548d-146">Fare clic su **gruppi di risorse** e trovare hello **Mobile Engagement** gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7548d-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="7548d-147">Fare clic su hello **Mobile Engagement** risorse di gruppo e passare toohello **impostazioni** pannello qui.</span><span class="sxs-lookup"><span data-stu-id="7548d-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="7548d-148">Fare clic su **utenti** in hello pannello impostazioni e quindi fare clic su **Aggiungi** tooadd un utente.</span><span class="sxs-lookup"><span data-stu-id="7548d-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="7548d-149">Fare clic su **Selezionare un ruolo**</span><span class="sxs-lookup"><span data-stu-id="7548d-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="7548d-150">Fare clic su **Proprietario**</span><span class="sxs-lookup"><span data-stu-id="7548d-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="7548d-151">Ricerca per nome dell'applicazione hello **AD\_APP\_nome** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="7548d-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="7548d-152">Qui non verrà visualizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7548d-152">You will not see this by default here.</span></span> <span data-ttu-id="7548d-153">Se si trova il, selezionarla e fare clic su **selezionare** nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="7548d-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="7548d-154">In hello **aggiungere accesso** pannello viene visualizzato come **1 utente, 0 gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7548d-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="7548d-155">Fare clic su **OK** su questa modifica hello tooconfirm di blade.</span><span class="sxs-lookup"><span data-stu-id="7548d-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="7548d-156">Configurazione di AAD hello necessario sono stati completati ed è hello toocall di tutti i set di API.</span><span class="sxs-lookup"><span data-stu-id="7548d-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

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



