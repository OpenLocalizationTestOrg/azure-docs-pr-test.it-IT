---
title: autenticazione aaaAdd in Apache Cordova con App per dispositivi mobili | Documenti Microsoft
description: "Informazioni su come toouse App per dispositivi mobili degli utenti di Azure App Service tooauthenticate dell'app Apache Cordova tramite un'ampia varietà di provider di identità, tra cui Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="efdce-103">Aggiungere app Apache Cordova tooyour di autenticazione</span><span class="sxs-lookup"><span data-stu-id="efdce-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="efdce-104">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="efdce-104">Summary</span></span>
<span data-ttu-id="efdce-105">In questa esercitazione è aggiungere progetto di avvio rapido di autenticazione toohello todolist in Apache Cordova tramite un provider di identità supportati.</span><span class="sxs-lookup"><span data-stu-id="efdce-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="efdce-106">In questa esercitazione si basa sull'hello [Introduzione a Mobile app] esercitazione, è necessario completare prima.</span><span class="sxs-lookup"><span data-stu-id="efdce-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="efdce-107"><a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App</span><span class="sxs-lookup"><span data-stu-id="efdce-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="efdce-108">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="efdce-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="efdce-109"><a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="efdce-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="efdce-110">A questo punto, è possibile verificare che tale back-end tooyour l'accesso anonimo è stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="efdce-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="efdce-111">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="efdce-111">In Visual Studio:</span></span>

* <span data-ttu-id="efdce-112">Progetto aperto hello creato dopo avere completato l'esercitazione hello [Introduzione a Mobile app].</span><span class="sxs-lookup"><span data-stu-id="efdce-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="efdce-113">Eseguire l'applicazione in hello **emulatore Android di Google**.</span><span class="sxs-lookup"><span data-stu-id="efdce-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="efdce-114">Verificare che sia visualizzato un errore di connessione imprevisto dopo l'avvio dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="efdce-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="efdce-115">Aggiornare quindi gli utenti di hello app tooauthenticate prima di richiedere risorse di back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="efdce-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="efdce-116"><a name="add-authentication"></a>Aggiungere app toohello authentication</span><span class="sxs-lookup"><span data-stu-id="efdce-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="efdce-117">Aprire il progetto in **Visual Studio**, quindi aprire hello `www/index.html` file per la modifica.</span><span class="sxs-lookup"><span data-stu-id="efdce-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="efdce-118">Individuare hello `Content-Security-Policy` metatag nella sezione di intestazione hello.</span><span class="sxs-lookup"><span data-stu-id="efdce-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="efdce-119">Aggiungere hello OAuth host toohello elenco di origini consentite.</span><span class="sxs-lookup"><span data-stu-id="efdce-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="efdce-120">Provider</span><span class="sxs-lookup"><span data-stu-id="efdce-120">Provider</span></span> | <span data-ttu-id="efdce-121">Nome del provider SDK</span><span class="sxs-lookup"><span data-stu-id="efdce-121">SDK Provider Name</span></span> | <span data-ttu-id="efdce-122">Host OAuth</span><span class="sxs-lookup"><span data-stu-id="efdce-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="efdce-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efdce-123">Azure Active Directory</span></span> | <span data-ttu-id="efdce-124">aad</span><span class="sxs-lookup"><span data-stu-id="efdce-124">aad</span></span> | <span data-ttu-id="efdce-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="efdce-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="efdce-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="efdce-126">Facebook</span></span> | <span data-ttu-id="efdce-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="efdce-127">facebook</span></span> | <span data-ttu-id="efdce-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="efdce-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="efdce-129">Google</span><span class="sxs-lookup"><span data-stu-id="efdce-129">Google</span></span> | <span data-ttu-id="efdce-130">Google</span><span class="sxs-lookup"><span data-stu-id="efdce-130">google</span></span> | <span data-ttu-id="efdce-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="efdce-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="efdce-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="efdce-132">Microsoft</span></span> | <span data-ttu-id="efdce-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="efdce-133">microsoftaccount</span></span> | <span data-ttu-id="efdce-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="efdce-134">https://login.live.com</span></span> |
   | <span data-ttu-id="efdce-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="efdce-135">Twitter</span></span> | <span data-ttu-id="efdce-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="efdce-136">twitter</span></span> | <span data-ttu-id="efdce-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="efdce-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="efdce-138">Ecco un esempio di Content-Security-Policy implementato per Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="efdce-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="efdce-139">Sostituire `https://login.microsoftonline.com` con host OAuth hello hello tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="efdce-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="efdce-140">Per ulteriori informazioni sui tag meta di criteri di sicurezza contenuto hello, vedere hello [documentazione di criteri di sicurezza contenuto].</span><span class="sxs-lookup"><span data-stu-id="efdce-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="efdce-141">Alcuni provider di autenticazione non richiedono modifiche a Content-Security-Policy quando viene usato in dispositivi mobili appropriati.</span><span class="sxs-lookup"><span data-stu-id="efdce-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="efdce-142">Ad esempio, non sono richieste modifiche a Content-Security-Policy quando si usa l'autenticazione di Google in un dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="efdce-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="efdce-143">Aprire hello `www/js/index.js` per la modifica del file, individuare hello `onDeviceReady()` (metodo), e creazione di client hello in codice aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="efdce-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="efdce-144">Questo codice sostituisce il codice esistente hello Crea riferimento a tabella hello e aggiorna hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="efdce-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="efdce-145">metodo di Login () Hello avvia l'autenticazione con il provider di hello.</span><span class="sxs-lookup"><span data-stu-id="efdce-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="efdce-146">Hello Login () è una funzione asincrona che restituisce una promessa di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="efdce-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="efdce-147">rest Hello di inizializzazione hello viene inserito in risposta promessa hello in modo che non viene eseguita fino al completamento di metodo di hello Login ().</span><span class="sxs-lookup"><span data-stu-id="efdce-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="efdce-148">Nel codice hello appena aggiunto, sostituire `SDK_Provider_Name` con nome hello del provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="efdce-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="efdce-149">Ad esempio, per Azure Active Directory usare `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="efdce-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="efdce-150">Eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="efdce-150">Run your project.</span></span>  <span data-ttu-id="efdce-151">Al termine dell'inizializzazione progetto hello, l'applicazione Mostra pagina di accesso OAuth hello per hello provider di autenticazione scelto.</span><span class="sxs-lookup"><span data-stu-id="efdce-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="efdce-152"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efdce-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="efdce-153">Per altre informazioni, vedere [Autenticazione e autorizzazione] con il servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="efdce-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="efdce-154">Continuare l'esercitazione hello aggiungendo [le notifiche Push] tooyour app di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="efdce-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="efdce-155">Informazioni su come toouse hello SDK.</span><span class="sxs-lookup"><span data-stu-id="efdce-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="efdce-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="efdce-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="efdce-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="efdce-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="efdce-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="efdce-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[Introduzione a Mobile app]: app-service-mobile-cordova-get-started.md
[documentazione di criteri di sicurezza contenuto]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[le notifiche Push]: app-service-mobile-cordova-get-started-push.md
[Autenticazione e autorizzazione]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
