---
title: Creare un bridge tra WebView di Android e Mobile Engagement SDK per Android nativo
description: Viene descritto come creare un bridge tra WebView che esegue JavaScript e Mobile Engagement SDK nativo per Android
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="f9100-103">Creare un bridge tra WebView di Android e Mobile Engagement SDK per Android nativo</span><span class="sxs-lookup"><span data-stu-id="f9100-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9100-104">Bridge Android</span><span class="sxs-lookup"><span data-stu-id="f9100-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="f9100-105">Bridge iOS</span><span class="sxs-lookup"><span data-stu-id="f9100-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="f9100-106">Alcune app per dispositivi mobili vengono progettate come app ibride dove l'app stessa è sviluppata con Android nativo, ma le schermate vengono restituite, totalmente o in parte, in WebView di Android.</span><span class="sxs-lookup"><span data-stu-id="f9100-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="f9100-107">È comunque possibile usare Mobile Engagement SDK per Android all'interno di tali app e questa esercitazione illustra come farlo.</span><span class="sxs-lookup"><span data-stu-id="f9100-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="f9100-108">Il codice di esempio riportato sotto si basa sulla documentazione Android disponibile [qui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="f9100-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="f9100-109">Si descrive come usare questo approccio documentato per implementare gli stessi metodi comunemente usati per Mobile Engagement SDK per Android in modo che WebView possa avviare richieste da un'app ibrida per tenere traccia di eventi, processi, errori e informazioni app durante il piping via SDK per Android.</span><span class="sxs-lookup"><span data-stu-id="f9100-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="f9100-110">Prima di tutto, è necessario verificare di aver terminato l' [esercitazione introduttiva](mobile-engagement-android-get-started.md) per integrare Mobile Engagement SDK per Android nell'app ibrida.</span><span class="sxs-lookup"><span data-stu-id="f9100-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="f9100-111">Al termine dell'operazione, il metodo `OnCreate` avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="f9100-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="f9100-112">Verificare che l'app ibrida visualizzi WebView sulla schermata.</span><span class="sxs-lookup"><span data-stu-id="f9100-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="f9100-113">Il codice sarà simile al seguente, dove è in corso il caricamento del file HTML locale **Sample.html** in WebView nel metodo `onCreate` della schermata.</span><span class="sxs-lookup"><span data-stu-id="f9100-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="f9100-114">Creare un file bridge denominato **WebAppInterface** per generare un wrapper su alcuni metodi comunemente usati di Mobile Engagement SDK per Android tramite l'approccio `@JavascriptInterface` descritto nella [documentazione Android](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="f9100-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="f9100-115">Dopo aver creato il file bridge di cui sopra, è necessario verificare che sia associato a WebView.</span><span class="sxs-lookup"><span data-stu-id="f9100-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="f9100-116">A tale scopo, è necessario modificare il metodo `SetWebview` che deve somigliare al seguente:</span><span class="sxs-lookup"><span data-stu-id="f9100-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="f9100-117">Nel frammento precedente, `addJavascriptInterface` è stato chiamato per associare la classe bridge a WebView ed è stato creato anche un handle denominato **EngagementJs** per chiamare i metodi dal file bridge.</span><span class="sxs-lookup"><span data-stu-id="f9100-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="f9100-118">Creare nel progetto il seguente file denominato **Sample.html** all'interno di una cartella dal nome **assets**, che viene caricata in WebView e in cui verranno chiamati i metodi dal file bridge.</span><span class="sxs-lookup"><span data-stu-id="f9100-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="f9100-119">Notare i punti seguenti riguardanti il file HTML indicato sopra:</span><span class="sxs-lookup"><span data-stu-id="f9100-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="f9100-120">Contiene un set di caselle di input in cui è possibile fornire i dati da usare come nomi per Event, Job, Error e AppInfo.</span><span class="sxs-lookup"><span data-stu-id="f9100-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="f9100-121">Quando si fa clic sul pulsante accanto, viene eseguita una chiamata a JavaScript che a sua volta chiama i metodi dal file bridge per passare la chiamata a Mobile Engagement SDK per Android.</span><span class="sxs-lookup"><span data-stu-id="f9100-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="f9100-122">Vengono aggiunte alcune informazioni statiche extra agli eventi, ai processi e anche agli errori per mostrare come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f9100-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="f9100-123">Queste informazioni aggiuntive vengono inviate come stringa JSON che, guardando il file `WebAppInterface`, viene analizzata e inserita in un `Bundle` Android, quindi passata con l'invio di Events, Jobs ed Errors.</span><span class="sxs-lookup"><span data-stu-id="f9100-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="f9100-124">Un processo di Mobile Engagement viene avviato con il nome specificato nella casella di input, viene eseguito per 10 secondi, quindi arrestato.</span><span class="sxs-lookup"><span data-stu-id="f9100-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="f9100-125">Un appinfo o tag Mobile Engagement viene passato con 'customer_name' come chiave statica e con il valore immesso nell'input come valore del tag.</span><span class="sxs-lookup"><span data-stu-id="f9100-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="f9100-126">Eseguire l'app per visualizzare quanto segue.</span><span class="sxs-lookup"><span data-stu-id="f9100-126">Run the app and you will see the following.</span></span> <span data-ttu-id="f9100-127">Assegnare un nome a un evento test simile a quello seguente, quindi fare clic su **Send** sotto.</span><span class="sxs-lookup"><span data-stu-id="f9100-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="f9100-128">È possibile visualizzare questo evento insieme alle informazioni app statiche inviate passando alla scheda **Monitoraggio** dell'app e guardando in **Eventi -> Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="f9100-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
