---
title: Aggiungere l'autenticazione in iOS con le app per dispositivi mobili di Azure
description: "Informazioni su come usare le app per dispositivi mobili di Azure per autenticare gli utenti dell'app iOS tramite vari provider di identità, tra cui AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="f613e-103">Aggiungere l'autenticazione all'app iOS</span><span class="sxs-lookup"><span data-stu-id="f613e-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="f613e-104">Questa esercitazione illustra come aggiungere l'autenticazione al progetto di [avvio rapido di iOS] tramite un provider di identità supportato.</span><span class="sxs-lookup"><span data-stu-id="f613e-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="f613e-105">Questa esercitazione è basata sull'esercitazione relativa all' [avvio rapido di iOS] , che deve essere completata per prima.</span><span class="sxs-lookup"><span data-stu-id="f613e-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="f613e-106"><a name="register"></a>Registrare l'app per l'autenticazione e configurare il servizio app</span><span class="sxs-lookup"><span data-stu-id="f613e-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="f613e-107"><a name="redirecturl"></a>Aggiungere l'app agli URL di reindirizzamento esterni consentiti</span><span class="sxs-lookup"><span data-stu-id="f613e-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="f613e-108">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="f613e-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="f613e-109">In questo modo il sistema di autenticazione reindirizza all'app al termine del processo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="f613e-110">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="f613e-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="f613e-111">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="f613e-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="f613e-112">Lo schema deve essere univoco per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f613e-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="f613e-113">Per abilitare il reindirizzamento sul lato server:</span><span class="sxs-lookup"><span data-stu-id="f613e-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="f613e-114">Nel [portale di Azure] selezionare il servizio app.</span><span class="sxs-lookup"><span data-stu-id="f613e-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="f613e-115">Fare clic sull'opzione di menu **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="f613e-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="f613e-116">Fare clic su **Azure Active Directory** nella sezione **Provider di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="f613e-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="f613e-117">Impostare **Modalità di gestione** su **Avanzata**.</span><span class="sxs-lookup"><span data-stu-id="f613e-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="f613e-118">In **URL di reindirizzamento esterni consentiti** specificare `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="f613e-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="f613e-119">Il valore _appname_ in questa stringa è lo schema URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f613e-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="f613e-120">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="f613e-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="f613e-121">È opportuno prendere nota della stringa scelta perché sarà necessario modificare il codice dell'applicazione per dispositivi mobili con lo schema URL in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="f613e-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="f613e-122">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f613e-122">Click **OK**.</span></span>

7. <span data-ttu-id="f613e-123">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="f613e-123">Click **Save**.</span></span>

## <span data-ttu-id="f613e-124"><a name="permissions"></a>Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="f613e-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="f613e-125">In Xcode fare clic su **Esegui** per avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="f613e-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="f613e-126">Viene generata un'eccezione perché l'app prova ad accedere al back-end come utente non autenticato, mentre ora la tabella *TodoItem* richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="f613e-127"><a name="add-authentication"></a>Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="f613e-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="f613e-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="f613e-128">**Objective-C**:</span></span>

1. <span data-ttu-id="f613e-129">In Mac aprire *QSTodoListViewController.m* in Xcode e aggiungere il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="f613e-130">Modificare *google* in *microsoftaccount*, *twitter*, *facebook* o *windowsazureactivedirectory* se non si usa Google come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f613e-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="f613e-131">Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="f613e-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="f613e-132">Sostituire **urlScheme** con un nome univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="f613e-133">Il valore di urlScheme deve corrispondere a quello del protocollo dello schema URL specificato nel campo **URL di reindirizzamento esterni consentiti** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f613e-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="f613e-134">urlScheme viene usato dal callback di autenticazione per tornare all'applicazione dopo aver completato la richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="f613e-135">Sostituire `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="f613e-136">Aprire il file `QSAppDelegate.h` e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="f613e-137">Aprire il file `QSAppDelegate.m` e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="f613e-138">Aggiungere questo codice direttamente prima della riga `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="f613e-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="f613e-139">Sostituire _appname_ con il valore di urlScheme usato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f613e-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="f613e-140">Aprire il file `AppName-Info.plist` (sostituendo AppName con il nome dell'app) e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="f613e-141">Questo codice deve essere inserito all'interno dell'elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="f613e-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="f613e-142">Sostituire la stringa _appname_ (all'interno della matrice per **CFBundleURLSchemes**) con il nome app scelto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f613e-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="f613e-143">È possibile apportare queste modifiche anche nell'editor Plist. Fare clic sul file `AppName-Info.plist` in XCode per aprire l'editor Plist.</span><span class="sxs-lookup"><span data-stu-id="f613e-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="f613e-144">Sostituire la stringa `com.microsoft.azure.zumo` per **CFBundleURLName** con l'identificatore del bundle Apple.</span><span class="sxs-lookup"><span data-stu-id="f613e-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="f613e-145">Fare clic su *Run* (Esegui) per avviare l'app e quindi accedere.</span><span class="sxs-lookup"><span data-stu-id="f613e-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="f613e-146">Una volta eseguito l'accesso, dovrebbe essere possibile visualizzare l'elenco Todo e apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="f613e-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="f613e-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="f613e-147">**Swift**:</span></span>

1. <span data-ttu-id="f613e-148">In Mac aprire *ToDoTableViewController.swift* in Xcode e aggiungere il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="f613e-149">Modificare *google* in *microsoftaccount*, *twitter*, *facebook* o *windowsazureactivedirectory* se non si usa Google come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f613e-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="f613e-150">Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="f613e-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="f613e-151">Sostituire **urlScheme** con un nome univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="f613e-152">Il valore di urlScheme deve corrispondere a quello del protocollo dello schema URL specificato nel campo **URL di reindirizzamento esterni consentiti** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f613e-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="f613e-153">urlScheme viene usato dal callback di autenticazione per tornare all'applicazione dopo aver completato la richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f613e-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="f613e-154">Rimuovere le righe `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` alla fine di `viewDidLoad()` in *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="f613e-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="f613e-155">Aggiungere una chiamata a `loginAndGetData()` al posto di tali righe:</span><span class="sxs-lookup"><span data-stu-id="f613e-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="f613e-156">Aprire il file `AppDelegate.swift` e aggiungere la riga seguente alla classe `AppDelegate`:</span><span class="sxs-lookup"><span data-stu-id="f613e-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="f613e-157">Sostituire _appname_ con il valore di urlScheme usato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f613e-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="f613e-158">Aprire il file `AppName-Info.plist` (sostituendo AppName con il nome dell'app) e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f613e-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="f613e-159">Questo codice deve essere inserito all'interno dell'elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="f613e-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="f613e-160">Sostituire la stringa _appname_ (all'interno della matrice per **CFBundleURLSchemes**) con il nome app scelto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f613e-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="f613e-161">È possibile apportare queste modifiche anche nell'editor Plist. Fare clic sul file `AppName-Info.plist` in XCode per aprire l'editor Plist.</span><span class="sxs-lookup"><span data-stu-id="f613e-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="f613e-162">Sostituire la stringa `com.microsoft.azure.zumo` per **CFBundleURLName** con l'identificatore del bundle Apple.</span><span class="sxs-lookup"><span data-stu-id="f613e-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="f613e-163">Fare clic su *Run* (Esegui) per avviare l'app e quindi accedere.</span><span class="sxs-lookup"><span data-stu-id="f613e-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="f613e-164">Una volta eseguito l'accesso, dovrebbe essere possibile visualizzare l'elenco Todo e apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="f613e-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="f613e-165">L'autenticazione del servizio app usa la comunicazione tra app di Apple.</span><span class="sxs-lookup"><span data-stu-id="f613e-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="f613e-166">Per altre informazioni su questo argomento, vedere la [documentazione Apple][2]</span><span class="sxs-lookup"><span data-stu-id="f613e-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="f613e-167">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f613e-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="f613e-168">[avvio rapido di iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f613e-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

