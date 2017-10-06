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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Creare un bridge tra WebView di Android e Mobile Engagement SDK per Android nativo
> [!div class="op_single_selector"]
> * [Bridge Android](mobile-engagement-bridge-webview-native-android.md)
> * [Bridge iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Alcune App per dispositivi mobili sono progettati come un'applicazione ibrida in cui l'app hello stessa viene sviluppata utilizzando lo sviluppo di Android native ma alcune o tutte le schermate di hello viene eseguite in un WebView Android. È comunque possibile utilizzare Mobile Engagement SDK Android all'interno di tali applicazioni e di questa esercitazione viene descritto come toogo su questa operazione. codice di esempio Hello seguente si basa sull'hello documentazione Android [qui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Viene descritto come questo approccio documentato può essere utilizzato tooimplement hello stesso per metodi di Mobile Engagement Android SDK comunemente utilizzati in modo che Webview da un'applicazione ibrida può inoltre iniziare richieste tootrack eventi, processi e app-info, errori durante l'invio tramite pipe tramite il nostro Android SDK. 

1. Prima di tutto, è necessario tooensure che sono già state completate tramite il nostro [esercitazione introduttiva](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement SDK Android nell'applicazione ibrida. Una volta eseguita, il `OnCreate` metodo avrà un aspetto simile hello seguenti.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Verificare che l'app ibrida visualizzi WebView sulla schermata. Hello il codice sarà simile toohello seguente in cui è in corso il caricamento un file HTML locale **Sample.html** in Ciao Webview hello `onCreate` metodo dello schermo. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Creare un file di bridge denominato **WebAppInterface** che consente di creare un wrapper per alcuni comunemente utilizzati i metodi di Mobile Engagement SDK Android usando hello `@JavascriptInterface` approccio descritto in hello [documentazione Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. Quando abbiamo creato hello sopra file bridge, dobbiamo tooensure che è associato il nostro Webview. Per questo toohappen, è necessario tooedit il `SetWebview` metodo in modo che rispecchi hello seguente:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. In hello sopra frammento di codice, è stato chiamato `addJavascriptInterface` tooassociate il bridge di classe con il nostro Webview e anche creato un handle chiamato **EngagementJs** metodi hello toocall dal file bridge hello. 
6. Creare ora hello seguente file denominato **Sample.html** nel progetto in una cartella denominata **asset** che vengono caricati in Webview hello e in cui si chiamerà i metodi di hello dal file bridge hello.
   
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
7. Esempio hello nota punti sui file HTML hello precedente:
   
   * Contiene un set di caselle di input in cui è possibile fornire dati toobe utilizzati come nomi per l'evento, processo, l'errore, AppInfo. Quando si fa clic su hello pulsante Avanti tooit, toohello Javascript che questo toohello chiamata Mobile Engagement SDK Android chiama i metodi di hello da hello bridge file toopass viene eseguita una chiamata. 
   * Ci stiamo tag su alcuni eventi toohello statico informazioni supplementari, processi e persino errori toodemonstrate come questa operazione. Queste informazioni aggiuntive viene inviata come stringa di un formato JSON che, se si osserva hello `WebAppInterface` file, viene analizzato e inserire in un Android `Bundle` e viene passato insieme a eventi, i processi, errori di invio. 
   * Un processo di Engagement Mobile viene avviato con nome hello specificata nella casella di input hello, eseguito per 10 secondi e arrestato. 
   * Un appinfo Engagement Mobile o un tag viene passato come chiave statica hello e il valore di hello immesse nell'input hello come valore di hello per tag hello con 'cliente'. 
8. Esecuzione hello app e visualizzato sarà hello seguente. Ora di fornire un nome per un evento di verifica come hello seguenti e fare clic su **inviare** sotto di essa. 
   
    ![][1]
9. Se si passa toohello **monitoraggio** scheda della finestra dell'app e l'aspetto in **eventi -> Dettagli**, verrà visualizzato questo evento visualizzati insieme hello statico app-info che viene inviato. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
