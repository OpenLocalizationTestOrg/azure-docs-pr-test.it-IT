---
title: iOS aaaBridge WebView con iOS native di Mobile Engagement SDK
description: Viene descritto come ponte tra WebView che eseguono Javascript e hello native Engagement Mobile iOS SDK toocreate
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
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Creare un bridge tra WebView di iOS e Mobile Engagement SDK per iOS nativo
> [!div class="op_single_selector"]
> * [Bridge Android](mobile-engagement-bridge-webview-native-android.md)
> * [Bridge iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Alcune App per dispositivi mobili sono progettati come un'applicazione ibrida in cui hello app stessa viene sviluppata utilizzando lo sviluppo iOS native Objective-C, ma alcune o tutte le schermate di hello viene eseguite in un iOS WebView. È comunque possibile utilizzare iOS Mobile Engagement SDK all'interno di tali applicazioni e di questa esercitazione viene descritto come toogo su questa operazione. 

Esistono due approcci tooachieve questo anche se entrambi sono documentati:

* Il primo viene descritto in questo [collegamento](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) e comporta la registrazione di `UIWebViewDelegate` nella visualizzazione Web e il rilevamento con cancellazione immediata di una modifica del percorso eseguito in JavaScript. 
* In secondo luogo uno si basa su questo [WWDC 2013 sessione](https://developer.apple.com/videos/play/wwdc2013/615), un approccio che è più chiara di hello prima e che verrà seguito di questa Guida. Si noti che questo approccio funziona solo con iOS7 e versioni successive. 

Completare i passaggi hello per iOS hello bridge di esempio:

1. Prima di tutto, è necessario tooensure che sono già state completate tramite il nostro [esercitazione introduttiva](mobile-engagement-ios-get-started.md) toointegrate hello, iOS Mobile Engagement SDK nell'applicazione ibrida. Facoltativamente, è anche possibile abilitare la registrazione come indicato di seguito di test in modo che è possibile vedere i metodi SDK hello è attivati da webview hello. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Verificare che l'app ibrida visualizzi WebView sulla schermata. È possibile aggiungere toohello `Main.storyboard` dell'applicazione hello. 
3. Associare questa webview con il **ViewController** facendo clic e trascinando hello webview da hello Visualizza Controller scena toohello `ViewController.h` modifica schermata posizionarla sotto hello `@interface` riga. 
4. Dopo aver eseguito questa operazione viene visualizzata una finestra di dialogo con la richiesta di un nome. Specificare come nome hello **webView**. Il `ViewController.h` file dovrebbe essere simile hello seguente:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Microsoft aggiornerà hello `ViewController.m` file in un secondo momento, ma prima di tutto si creerà i file di bridge hello che crea un wrapper sull'alcuni iOS Mobile Engagement comunemente utilizzati i metodi SDK. Creare un nuovo file di intestazione denominato **EngagementJsExports.h** che utilizza hello `JSExport` meccanismo descritto nel suddetto hello [sessione](https://developer.apple.com/videos/play/wwdc2013/615) metodi di tooexpose hello iOS nativo. 
   
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
6. Successivamente, si creerà hello seconda parte file hello del bridge. Creare un file denominato **EngagementJsExports.m** che conterrà l'implementazione di hello la creazione di wrapper effettivo hello mediante la chiamata di metodi SDK hello Engagement Mobile iOS. Si noti inoltre che ci stiamo analisi hello `extras` passati da hello webview javascript e l'inserimento in un `NSMutableDictionary` toobe oggetto passato con il metodo Engagement SDK hello chiamate.  
   
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
7. Ora si passerà nuovamente toohello **ViewController.m** e aggiornarlo con hello seguente codice: 
   
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
8. Punti seguenti hello nota hello **ViewController.m** file:
   
   * In hello `loadWebView` (metodo), è sta il caricamento di un file HTML locale denominato **LocalPage.html** il cui codice verranno esaminate successivamente. 
   * In hello `webViewDidFinishLoad` (metodo), ci stiamo selezionandola hello `JsContext` e associa la classe wrapper. In questo modo i metodi di chiamata i wrapper SDK utilizzo handle hello **EngagementJs** da hello webView. 
9. Creare un file denominato **LocalPage.html** con hello seguente codice:
   
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
                       // Example of how extras info can be passed with hello Engagement logs
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
10. Esempio hello nota punti sui file HTML hello precedente:
    
    * Contiene un set di caselle di input in cui è possibile fornire dati toobe utilizzati come nomi per l'evento, processo, l'errore, AppInfo. Quando si fa clic su hello pulsante Avanti tooit, viene eseguita una chiamata toohello Javascript che chiama infine metodi hello da hello bridge file toopass questo toohello chiamata iOS Mobile Engagement SDK. 
    * Ci stiamo tag su alcuni eventi toohello statico informazioni supplementari, processi e persino errori toodemonstrate come questa operazione. Queste informazioni aggiuntive viene inviata come stringa di un formato JSON che, se si osserva hello `EngagementJsExports.m` file, vengono analizzati e passati insieme a eventi, i processi, errori di invio. 
    * Un processo di Engagement Mobile viene avviato con nome hello specificata nella casella di input hello, eseguito per 10 secondi e arrestato. 
    * Un appinfo Engagement Mobile o un tag viene passato come chiave statica hello e il valore di hello immesse nell'input hello come valore di hello per tag hello con 'cliente'. 
11. Esecuzione hello app e visualizzato sarà hello seguente. Ora di fornire un nome per un evento di verifica come hello seguenti e fare clic su **inviare** tooit successivo. 
    
     ![][1]
12. Se si passa toohello **monitoraggio** scheda della finestra dell'app e l'aspetto in **eventi -> Dettagli**, verrà visualizzato questo evento visualizzati insieme hello statico app-info che viene inviato. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
