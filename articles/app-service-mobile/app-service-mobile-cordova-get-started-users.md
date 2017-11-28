---
title: Aggiungere l'autenticazione in Apache Cordova con App per dispositivi mobili| Documentazione Microsoft
description: "Informazioni su come usare App per dispositivi mobili nel servizio app di Azure per autenticare gli utenti dell'app Apache Cordova tramite vari provider di identità, tra cui Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="b8eb0-103">Aggiungere l'autenticazione all'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="b8eb0-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="b8eb0-104">Summary</span><span class="sxs-lookup"><span data-stu-id="b8eb0-104">Summary</span></span>
<span data-ttu-id="b8eb0-105">Questa esercitazione consente di aggiungere l'autenticazione al progetto introduttivo TodoList in Apache Cordova tramite un provider di identità supportato.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="b8eb0-106">Questa esercitazione è basata sull'esercitazione relativa alla [Introduzione alle app per dispositivi mobili] , che deve essere completata per prima.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="b8eb0-107"><a name="register"></a>Registrare l'app per l'autenticazione e configurare il servizio app</span><span class="sxs-lookup"><span data-stu-id="b8eb0-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="b8eb0-108">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="b8eb0-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="b8eb0-109"><a name="permissions"></a>Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="b8eb0-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b8eb0-110">A questo punto, è possibile verificare che l'accesso anonimo al back-end è stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="b8eb0-111">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b8eb0-111">In Visual Studio:</span></span>

* <span data-ttu-id="b8eb0-112">Aprire il progetto creato dopo avere completato l'esercitazione [Introduzione alle app per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="b8eb0-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="b8eb0-113">Eseguire l'applicazione nell'**emulatore Android di Google**.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="b8eb0-114">Verificare che dopo l'avvio dell'applicazione venga visualizzato un errore di connessione imprevisto.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="b8eb0-115">A questo punto, aggiornare l'app per autenticare gli utenti prima di richiedere risorse al back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="b8eb0-116"><a name="add-authentication"></a>Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="b8eb0-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="b8eb0-117">Aprire il progetto in **Visual Studio**, quindi aprire il file `www/index.html` per la modifica.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="b8eb0-118">Individuare il meta tag `Content-Security-Policy` nella sezione di intestazione.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="b8eb0-119">Aggiungere l'host di OAuth all'elenco di origini consentite.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="b8eb0-120">Provider</span><span class="sxs-lookup"><span data-stu-id="b8eb0-120">Provider</span></span> | <span data-ttu-id="b8eb0-121">Nome del provider SDK</span><span class="sxs-lookup"><span data-stu-id="b8eb0-121">SDK Provider Name</span></span> | <span data-ttu-id="b8eb0-122">Host OAuth</span><span class="sxs-lookup"><span data-stu-id="b8eb0-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="b8eb0-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8eb0-123">Azure Active Directory</span></span> | <span data-ttu-id="b8eb0-124">aad</span><span class="sxs-lookup"><span data-stu-id="b8eb0-124">aad</span></span> | <span data-ttu-id="b8eb0-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b8eb0-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="b8eb0-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="b8eb0-126">Facebook</span></span> | <span data-ttu-id="b8eb0-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="b8eb0-127">facebook</span></span> | <span data-ttu-id="b8eb0-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="b8eb0-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="b8eb0-129">Google</span><span class="sxs-lookup"><span data-stu-id="b8eb0-129">Google</span></span> | <span data-ttu-id="b8eb0-130">Google</span><span class="sxs-lookup"><span data-stu-id="b8eb0-130">google</span></span> | <span data-ttu-id="b8eb0-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="b8eb0-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="b8eb0-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="b8eb0-132">Microsoft</span></span> | <span data-ttu-id="b8eb0-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="b8eb0-133">microsoftaccount</span></span> | <span data-ttu-id="b8eb0-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="b8eb0-134">https://login.live.com</span></span> |
   | <span data-ttu-id="b8eb0-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="b8eb0-135">Twitter</span></span> | <span data-ttu-id="b8eb0-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="b8eb0-136">twitter</span></span> | <span data-ttu-id="b8eb0-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="b8eb0-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="b8eb0-138">Ecco un esempio di Content-Security-Policy implementato per Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="b8eb0-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="b8eb0-139">Sostituire `https://login.microsoftonline.com` con l'host di OAuth indicato nella tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="b8eb0-140">Per altre informazioni sul metatag content-security-policy, vedere la [documentazione su Content-Security-Policy].</span><span class="sxs-lookup"><span data-stu-id="b8eb0-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="b8eb0-141">Alcuni provider di autenticazione non richiedono modifiche a Content-Security-Policy quando viene usato in dispositivi mobili appropriati.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="b8eb0-142">Ad esempio, non sono richieste modifiche a Content-Security-Policy quando si usa l'autenticazione di Google in un dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="b8eb0-143">Aprire il file `www/js/index.js` per la modifica, individuare il metodo `onDeviceReady()` e nel codice di creazione del client aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b8eb0-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="b8eb0-144">Questo codice sostituisce il codice esistente che crea il riferimento alla tabella e aggiorna l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="b8eb0-145">Il metodo login() inizia l'autenticazione con il provider.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="b8eb0-146">Il metodo login() è una funzione asincrona che restituisce una promessa JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="b8eb0-147">Il resto dell'inizializzazione viene inserito nella risposta della promessa in modo che non venga eseguita finché non viene completato il metodo login().</span><span class="sxs-lookup"><span data-stu-id="b8eb0-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="b8eb0-148">Nel codice aggiunto, sostituire `SDK_Provider_Name` con il nome del provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="b8eb0-149">Ad esempio, per Azure Active Directory usare `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="b8eb0-150">Eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-150">Run your project.</span></span>  <span data-ttu-id="b8eb0-151">Al termine dell'inizializzazione del progetto, nell'applicazione viene visualizzata la pagina di accesso di OAuth per il provider di autenticazione scelto.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="b8eb0-152"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8eb0-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="b8eb0-153">Per altre informazioni, vedere [Autenticazione e autorizzazione] con il servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="b8eb0-154">Continuare l'esercitazione aggiungendo [Notifiche Push] all'app Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="b8eb0-155">Informazioni su come usare gli SDK.</span><span class="sxs-lookup"><span data-stu-id="b8eb0-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="b8eb0-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="b8eb0-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="b8eb0-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="b8eb0-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="b8eb0-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="b8eb0-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="b8eb0-159">[Introduzione alle app per dispositivi mobili]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b8eb0-160">[documentazione su Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="b8eb0-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="b8eb0-161">[Notifiche Push]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="b8eb0-162">[Autenticazione e autorizzazione]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="b8eb0-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="b8eb0-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="b8eb0-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b8eb0-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
