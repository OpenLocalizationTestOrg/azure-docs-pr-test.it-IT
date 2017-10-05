---
title: Creare un bridge tra WebView di iOS e Mobile Engagement SDK per iOS nativo
description: Viene descritto come creare un bridge tra WebView che esegue JavaScript e Mobile Engagement SDK per iOS nativo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="d65f3-103">Creare un bridge tra WebView di iOS e Mobile Engagement SDK per iOS nativo</span><span class="sxs-lookup"><span data-stu-id="d65f3-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d65f3-104">Bridge Android</span><span class="sxs-lookup"><span data-stu-id="d65f3-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="d65f3-105">Bridge iOS</span><span class="sxs-lookup"><span data-stu-id="d65f3-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="d65f3-106">Alcune app per dispositivi mobili vengono progettate come app ibride dove l'app stessa è sviluppata con Objective-C iOS nativo, ma le schermate vengono restituite, totalmente o in parte, in WebView di iOS.</span><span class="sxs-lookup"><span data-stu-id="d65f3-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="d65f3-107">È comunque possibile usare Mobile Engagement SDK per iOS all'interno di tali app e questa esercitazione illustra come farlo.</span><span class="sxs-lookup"><span data-stu-id="d65f3-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="d65f3-108">Esistono due approcci per ottenere questo risultato anche se non è disponibile una documentazione al riguardo:</span><span class="sxs-lookup"><span data-stu-id="d65f3-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="d65f3-109">Il primo viene descritto in questo [collegamento](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) e comporta la registrazione di `UIWebViewDelegate` nella visualizzazione Web e il rilevamento con cancellazione immediata di una modifica del percorso eseguito in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d65f3-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="d65f3-110">Il secondo, che si basa su questa [sessione WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), rappresenta un approccio più lineare rispetto al primo ed è quello che viene adottato in questa guida.</span><span class="sxs-lookup"><span data-stu-id="d65f3-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="d65f3-111">Si noti che questo approccio funziona solo con iOS7 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d65f3-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="d65f3-112">Seguire la procedura riportata sotto per un esempio di bridge iOS:</span><span class="sxs-lookup"><span data-stu-id="d65f3-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="d65f3-113">Prima di tutto, è necessario verificare di aver terminato l' [esercitazione introduttiva](mobile-engagement-ios-get-started.md) per integrare Mobile Engagement SDK per iOS nell'app ibrida.</span><span class="sxs-lookup"><span data-stu-id="d65f3-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="d65f3-114">Si può anche scegliere di abilitare la registrazione test per poter vedere i metodi SDK quando vengono attivati da WebView.</span><span class="sxs-lookup"><span data-stu-id="d65f3-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="d65f3-115">Verificare che l'app ibrida visualizzi WebView sulla schermata.</span><span class="sxs-lookup"><span data-stu-id="d65f3-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="d65f3-116">È possibile aggiungerla a `Main.storyboard` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d65f3-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="d65f3-117">Associare questa WebView a **ViewController** facendo clic sulla WebView e trascinandola dalla finestra del controller alla schermata di modifica `ViewController.h` per posizionarla appena sotto la riga `@interface`.</span><span class="sxs-lookup"><span data-stu-id="d65f3-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="d65f3-118">Dopo aver eseguito questa operazione viene visualizzata una finestra di dialogo con la richiesta di un nome.</span><span class="sxs-lookup"><span data-stu-id="d65f3-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="d65f3-119">Assegnare il nome **webView**.</span><span class="sxs-lookup"><span data-stu-id="d65f3-119">Provide the name as **webView**.</span></span> <span data-ttu-id="d65f3-120">Il file `ViewController.h` deve apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="d65f3-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="d65f3-121">Il file `ViewController.m` sarà aggiornato in un secondo momento e prima viene creato il file bridge che a sua volta genera un wrapper su alcuni metodi comunemente usati di Mobile Engagement SDK per iOS.</span><span class="sxs-lookup"><span data-stu-id="d65f3-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="d65f3-122">Creare un nuovo file di intestazione denominato **EngagementJsExports.h** che usa il meccanismo `JSExport` descritto nella [sessione](https://developer.apple.com/videos/play/wwdc2013/615) indicata sopra per esporre i metodi nativi iOS.</span><span class="sxs-lookup"><span data-stu-id="d65f3-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. <span data-ttu-id="d65f3-123">Successivamente, viene creata la seconda parte del file bridge.</span><span class="sxs-lookup"><span data-stu-id="d65f3-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="d65f3-124">Creare un file denominato **EngagementJsExports.m** contenente l'implementazione di creazione dei wrapper effettivi chiamando i metodi Mobile Engagement SDK per iOS.</span><span class="sxs-lookup"><span data-stu-id="d65f3-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="d65f3-125">Si noti anche che è in corso l'analisi di `extras` passati da JavaScript di WebView e il relativo inserimento in un oggetto `NSMutableDictionary` da passare con le chiamate ai metodi Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="d65f3-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. <span data-ttu-id="d65f3-126">Si torna quindi a **ViewController.m** e lo si aggiorna con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d65f3-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. <span data-ttu-id="d65f3-127">Notare i punti seguenti sul file **ViewController.m** :</span><span class="sxs-lookup"><span data-stu-id="d65f3-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="d65f3-128">Nel metodo `loadWebView` si sta caricando un file HTML locale chiamato **LocalPage.html** il cui codice verrà esaminato successivamente.</span><span class="sxs-lookup"><span data-stu-id="d65f3-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="d65f3-129">Dal metodo `webViewDidFinishLoad` viene catturato `JsContext` e lo si associa alla classe wrapper.</span><span class="sxs-lookup"><span data-stu-id="d65f3-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="d65f3-130">Questo consente la chiamata ai metodi wrapper SDK tramite l'handle **EngagementJs** da WebView.</span><span class="sxs-lookup"><span data-stu-id="d65f3-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="d65f3-131">Creare un file denominato **LocalPage.html** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d65f3-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with the Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. <span data-ttu-id="d65f3-132">Notare i punti seguenti riguardanti il file HTML indicato sopra:</span><span class="sxs-lookup"><span data-stu-id="d65f3-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="d65f3-133">Contiene un set di caselle di input in cui è possibile fornire i dati da usare come nomi per Event, Job, Error e AppInfo.</span><span class="sxs-lookup"><span data-stu-id="d65f3-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="d65f3-134">Quando si fa clic sul pulsante accanto, viene eseguita una chiamata a JavaScript che a sua volta chiama i metodi dal file bridge per passare la chiamata a Mobile Engagement SDK per iOS.</span><span class="sxs-lookup"><span data-stu-id="d65f3-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="d65f3-135">Vengono aggiunte alcune informazioni statiche extra agli eventi, ai processi e anche agli errori per mostrare come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="d65f3-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="d65f3-136">Queste informazioni aggiuntive vengono inviate come stringa JSON che, guardando il file `EngagementJsExports.m` , viene analizzata e passata con l'invio di Events, Jobs ed Errors.</span><span class="sxs-lookup"><span data-stu-id="d65f3-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="d65f3-137">Un processo di Mobile Engagement viene avviato con il nome specificato nella casella di input, viene eseguito per 10 secondi, quindi arrestato.</span><span class="sxs-lookup"><span data-stu-id="d65f3-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="d65f3-138">Un appinfo o tag Mobile Engagement viene passato con 'customer_name' come chiave statica e con il valore immesso nell'input come valore del tag.</span><span class="sxs-lookup"><span data-stu-id="d65f3-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="d65f3-139">Eseguire l'app per visualizzare quanto segue.</span><span class="sxs-lookup"><span data-stu-id="d65f3-139">Run the app and you will see the following.</span></span> <span data-ttu-id="d65f3-140">Assegnare un nome a un evento test simile a quello seguente, quindi fare clic sul pulsante **Send** accanto.</span><span class="sxs-lookup"><span data-stu-id="d65f3-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="d65f3-141">È possibile visualizzare questo evento insieme alle informazioni app statiche inviate passando alla scheda **Monitoraggio** dell'app e guardando in **Eventi -> Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="d65f3-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
