---
title: aaaAdd l'autenticazione in iOS con App mobili di Azure
description: "Informazioni su come utenti di tooauthenticate toouse App mobili di Azure di app iOS tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="62e3a-103">Aggiungere app per iOS tooyour autenticazione</span><span class="sxs-lookup"><span data-stu-id="62e3a-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="62e3a-104">In questa esercitazione, si aggiunge l'autenticazione toohello [iOS quick start] progetto che utilizza un provider di identità supportati.</span><span class="sxs-lookup"><span data-stu-id="62e3a-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="62e3a-105">In questa esercitazione si basa sull'hello [iOS quick start] esercitazione, è necessario completare prima.</span><span class="sxs-lookup"><span data-stu-id="62e3a-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="62e3a-106"><a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App</span><span class="sxs-lookup"><span data-stu-id="62e3a-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="62e3a-107"><a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="62e3a-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="62e3a-108">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="62e3a-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="62e3a-109">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="62e3a-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="62e3a-110">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="62e3a-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="62e3a-111">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="62e3a-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="62e3a-112">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="62e3a-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="62e3a-113">reindirizzamento di hello tooenable sul lato server th:</span><span class="sxs-lookup"><span data-stu-id="62e3a-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="62e3a-114">In hello [portale di Azure], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="62e3a-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="62e3a-115">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="62e3a-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="62e3a-116">Fare clic su **Azure Active Directory** in hello **provider di autenticazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="62e3a-117">Set hello **modalità di gestione** troppo**avanzate**.</span><span class="sxs-lookup"><span data-stu-id="62e3a-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="62e3a-118">In hello **consentito URL di reindirizzamento esterno**, immettere `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="62e3a-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="62e3a-119">Hello _appname_ in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="62e3a-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="62e3a-120">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="62e3a-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="62e3a-121">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="62e3a-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="62e3a-122">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="62e3a-122">Click **OK**.</span></span>

7. <span data-ttu-id="62e3a-123">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="62e3a-123">Click **Save**.</span></span>

## <span data-ttu-id="62e3a-124"><a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="62e3a-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="62e3a-125">In Xcode, premere **eseguire** toostart hello app.</span><span class="sxs-lookup"><span data-stu-id="62e3a-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="62e3a-126">Poiché tenta di app hello tooaccess back-end come un utente non autenticato, viene generata un'eccezione, ma hello *TodoItem* tabella richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="62e3a-127"><a name="add-authentication"></a>Aggiungere l'autenticazione tooapp</span><span class="sxs-lookup"><span data-stu-id="62e3a-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="62e3a-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="62e3a-128">**Objective-C**:</span></span>

1. <span data-ttu-id="62e3a-129">Nel Mac, aprire *QSTodoListViewController.m* in Xcode e aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="62e3a-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="62e3a-130">Modifica *google* troppo*microsoftaccount*, *twitter*, *facebook*, o *windowsazureactivedirectory* se non si utilizza Google come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="62e3a-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="62e3a-131">Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="62e3a-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="62e3a-132">Sostituire hello **urlScheme** con un nome univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="62e3a-133">Hello urlScheme deve essere hello stesso come hello protocollo lo schema dell'URL specificato nel hello **consentito URL di reindirizzamento esterno** campo hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="62e3a-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="62e3a-134">Hello urlScheme viene utilizzata da un'applicazione hello autenticazione callback tooswitch tooyour back-dopo la richiesta di autenticazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="62e3a-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="62e3a-135">Sostituire `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="62e3a-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="62e3a-136">Aprire hello `QSAppDelegate.h` file e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="62e3a-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="62e3a-137">Aprire hello `QSAppDelegate.m` file e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="62e3a-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="62e3a-138">Aggiungere il codice direttamente prima della lettura riga hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="62e3a-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="62e3a-139">Sostituire il _appname_ oggi hello urlScheme che è stato utilizzato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="62e3a-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="62e3a-140">Aprire hello `AppName-Info.plist` file (sostituendo AppName con nome hello dell'app) e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="62e3a-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="62e3a-141">Questo codice deve essere inserito all'interno di hello `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="62e3a-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="62e3a-142">Sostituire hello _appname_ stringa (all'interno della matrice per **CFBundleURLSchemes**) con il nome di app hello scelto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="62e3a-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="62e3a-143">È possibile inoltre apportare queste modifiche in hello plist editor, fare clic su hello `AppName-Info.plist` file nell'editor di XCode tooopen hello plist.</span><span class="sxs-lookup"><span data-stu-id="62e3a-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="62e3a-144">Sostituire hello `com.microsoft.azure.zumo` stringa per **CFBundleURLName** con l'Apple identificatore di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="62e3a-145">Premere *eseguire* toostart hello app e quindi l'accesso.</span><span class="sxs-lookup"><span data-stu-id="62e3a-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="62e3a-146">Quando si è connessi, si deve essere elenco di attività in grado di tooview hello e aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="62e3a-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="62e3a-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="62e3a-147">**Swift**:</span></span>

1. <span data-ttu-id="62e3a-148">Nel Mac, aprire *ToDoTableViewController.swift* in Xcode e aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="62e3a-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="62e3a-149">Modifica *google* troppo*microsoftaccount*, *twitter*, *facebook*, o *windowsazureactivedirectory* se non si utilizza Google come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="62e3a-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="62e3a-150">Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="62e3a-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="62e3a-151">Sostituire hello **urlScheme** con un nome univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="62e3a-152">Hello urlScheme deve essere hello stesso come hello protocollo lo schema dell'URL specificato nel hello **consentito URL di reindirizzamento esterno** campo hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="62e3a-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="62e3a-153">Hello urlScheme viene utilizzata da un'applicazione hello autenticazione callback tooswitch tooyour back-dopo la richiesta di autenticazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="62e3a-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="62e3a-154">Rimuovere le righe di hello `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` alla fine di `viewDidLoad()` in *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="62e3a-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="62e3a-155">Aggiungere una chiamata troppo`loginAndGetData()` al loro posto:</span><span class="sxs-lookup"><span data-stu-id="62e3a-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="62e3a-156">Aprire hello `AppDelegate.swift` file e aggiungere hello seguente riga toohello `AppDelegate` classe:</span><span class="sxs-lookup"><span data-stu-id="62e3a-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="62e3a-157">Sostituire hello _appname_ oggi hello urlScheme che è stato utilizzato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="62e3a-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="62e3a-158">Aprire hello `AppName-Info.plist` file (sostituendo AppName con nome hello dell'app) e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="62e3a-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="62e3a-159">Questo codice deve essere inserito all'interno di hello `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="62e3a-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="62e3a-160">Sostituire hello _appname_ stringa (all'interno della matrice per **CFBundleURLSchemes**) con il nome di app hello scelto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="62e3a-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="62e3a-161">È possibile inoltre apportare queste modifiche in hello plist editor, fare clic su hello `AppName-Info.plist` file nell'editor di XCode tooopen hello plist.</span><span class="sxs-lookup"><span data-stu-id="62e3a-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="62e3a-162">Sostituire hello `com.microsoft.azure.zumo` stringa per **CFBundleURLName** con l'Apple identificatore di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="62e3a-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="62e3a-163">Premere *eseguire* toostart hello app e quindi l'accesso.</span><span class="sxs-lookup"><span data-stu-id="62e3a-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="62e3a-164">Quando si è connessi, si deve essere elenco di attività in grado di tooview hello e aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="62e3a-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="62e3a-165">L'autenticazione del servizio app usa la comunicazione tra app di Apple.</span><span class="sxs-lookup"><span data-stu-id="62e3a-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="62e3a-166">Per ulteriori informazioni su questo argomento, vedere toohello [documentazione di Apple][2]</span><span class="sxs-lookup"><span data-stu-id="62e3a-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portale di Azure]: https://portal.azure.com

[iOS quick start]: app-service-mobile-ios-get-started.md

