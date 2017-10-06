---
title: aaaBridge WebView Android con native Mobile Engagement SDK Android
description: Viene descritto come ponte tra WebView toocreate esecuzione di Javascript e hello native Mobile Engagement SDK Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="128c2-103">Creare un bridge tra WebView di Android e Mobile Engagement SDK per Android nativo</span><span class="sxs-lookup"><span data-stu-id="128c2-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="128c2-104">Bridge Android</span><span class="sxs-lookup"><span data-stu-id="128c2-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="128c2-105">Bridge iOS</span><span class="sxs-lookup"><span data-stu-id="128c2-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="128c2-106">Alcune App per dispositivi mobili sono progettati come un'applicazione ibrida in cui l'app hello stessa viene sviluppata utilizzando lo sviluppo di Android native ma alcune o tutte le schermate di hello viene eseguite in un WebView Android.</span><span class="sxs-lookup"><span data-stu-id="128c2-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="128c2-107">È comunque possibile utilizzare Mobile Engagement SDK Android all'interno di tali applicazioni e di questa esercitazione viene descritto come toogo su questa operazione.</span><span class="sxs-lookup"><span data-stu-id="128c2-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="128c2-108">codice di esempio Hello seguente si basa sull'hello documentazione Android [qui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="128c2-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="128c2-109">Viene descritto come questo approccio documentato può essere utilizzato tooimplement hello stesso per metodi di Mobile Engagement Android SDK comunemente utilizzati in modo che Webview da un'applicazione ibrida può inoltre iniziare richieste tootrack eventi, processi e app-info, errori durante l'invio tramite pipe tramite il nostro Android SDK.</span><span class="sxs-lookup"><span data-stu-id="128c2-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="128c2-110">Prima di tutto, è necessario tooensure che sono già state completate tramite il nostro [esercitazione introduttiva](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement SDK Android nell'applicazione ibrida.</span><span class="sxs-lookup"><span data-stu-id="128c2-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="128c2-111">Una volta eseguita, il `OnCreate` metodo avrà un aspetto simile hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="128c2-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="128c2-112">Verificare che l'app ibrida visualizzi WebView sulla schermata.</span><span class="sxs-lookup"><span data-stu-id="128c2-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="128c2-113">Hello il codice sarà simile toohello seguente in cui è in corso il caricamento un file HTML locale **Sample.html** in Ciao Webview hello `onCreate` metodo dello schermo.</span><span class="sxs-lookup"><span data-stu-id="128c2-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="128c2-114">Creare un file di bridge denominato **WebAppInterface** che consente di creare un wrapper per alcuni comunemente utilizzati i metodi di Mobile Engagement SDK Android usando hello `@JavascriptInterface` approccio descritto in hello [documentazione Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="128c2-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="128c2-115">Quando abbiamo creato hello sopra file bridge, dobbiamo tooensure che è associato il nostro Webview.</span><span class="sxs-lookup"><span data-stu-id="128c2-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="128c2-116">Per questo toohappen, è necessario tooedit il `SetWebview` metodo in modo che rispecchi hello seguente:</span><span class="sxs-lookup"><span data-stu-id="128c2-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="128c2-117">In hello sopra frammento di codice, è stato chiamato `addJavascriptInterface` tooassociate il bridge di classe con il nostro Webview e anche creato un handle chiamato **EngagementJs** metodi hello toocall dal file bridge hello.</span><span class="sxs-lookup"><span data-stu-id="128c2-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="128c2-118">Creare ora hello seguente file denominato **Sample.html** nel progetto in una cartella denominata **asset** che vengono caricati in Webview hello e in cui si chiamerà i metodi di hello dal file bridge hello.</span><span class="sxs-lookup"><span data-stu-id="128c2-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="128c2-119">Esempio hello nota punti sui file HTML hello precedente:</span><span class="sxs-lookup"><span data-stu-id="128c2-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="128c2-120">Contiene un set di caselle di input in cui è possibile fornire dati toobe utilizzati come nomi per l'evento, processo, l'errore, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="128c2-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="128c2-121">Quando si fa clic su hello pulsante Avanti tooit, toohello Javascript che questo toohello chiamata Mobile Engagement SDK Android chiama i metodi di hello da hello bridge file toopass viene eseguita una chiamata.</span><span class="sxs-lookup"><span data-stu-id="128c2-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="128c2-122">Ci stiamo tag su alcuni eventi toohello statico informazioni supplementari, processi e persino errori toodemonstrate come questa operazione.</span><span class="sxs-lookup"><span data-stu-id="128c2-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="128c2-123">Queste informazioni aggiuntive viene inviata come stringa di un formato JSON che, se si osserva hello `WebAppInterface` file, viene analizzato e inserire in un Android `Bundle` e viene passato insieme a eventi, i processi, errori di invio.</span><span class="sxs-lookup"><span data-stu-id="128c2-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="128c2-124">Un processo di Engagement Mobile viene avviato con nome hello specificata nella casella di input hello, eseguito per 10 secondi e arrestato.</span><span class="sxs-lookup"><span data-stu-id="128c2-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="128c2-125">Un appinfo Engagement Mobile o un tag viene passato come chiave statica hello e il valore di hello immesse nell'input hello come valore di hello per tag hello con 'cliente'.</span><span class="sxs-lookup"><span data-stu-id="128c2-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="128c2-126">Esecuzione hello app e visualizzato sarà hello seguente.</span><span class="sxs-lookup"><span data-stu-id="128c2-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="128c2-127">Ora di fornire un nome per un evento di verifica come hello seguenti e fare clic su **inviare** sotto di essa.</span><span class="sxs-lookup"><span data-stu-id="128c2-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="128c2-128">Se si passa toohello **monitoraggio** scheda della finestra dell'app e l'aspetto in **eventi -> Dettagli**, verrà visualizzato questo evento visualizzati insieme hello statico app-info che viene inviato.</span><span class="sxs-lookup"><span data-stu-id="128c2-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
