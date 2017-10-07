---
title: aaaHow tooMake una telefonata da Twilio (linguaggio) | Documenti Microsoft
description: Informazioni su come un telefono toomake chiamata da una pagina web l'utilizzo di Twilio in un'applicazione Java in Azure.
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure
Hello seguente esempio viene illustrato come usare Twilio toomake una chiamata da una pagina web ospitata in Azure. un'applicazione Hello risultante utente verrà chiesto hello di valori di chiamata telefonica, come illustrato nella seguente cattura di schermata hello.

![Modulo di chiamata di Azure con Twilio e Java][twilio_java]

È necessario seguente hello toodo codice hello toouse in questo argomento:

1. Ottenere un account e un token di autenticazione Twilio. tooget introduttiva Twilio, valutare al prezzo [http://www.twilio.com/pricing][twilio_pricing]. È possibile iscriversi al [https://www.twilio.com/try-twilio][try_twilio]. Per informazioni sulle API fornita da Twilio hello, vedere [http://www.twilio.com/api][twilio_api].
2. Ottenere hello JAR Twilio. In [https://github.com/twilio/twilio-java][twilio_java_github], è possibile scaricare origini GitHub hello e creare la propria JAR o scaricare un file JAR preesistente (con o senza dipendenze).
   codice Hello in questo argomento è stato scritto utilizzando hello predefinite JAR TwilioJava 3.3.8 con dipendenze.
3. Aggiungere hello JAR tooyour percorso di compilazione Java.
4. Se si usa Eclipse toocreate questa applicazione Java, includere hello Twilio JAR nel file di distribuzione dell'applicazione (WAR) con funzionalità di distribuzione di assembly di Eclipse. Se non si utilizza Eclipse toocreate questa applicazione Java, verificare che sia incluso all'interno di hello hello JAR Twilio stesso ruolo di Azure come percorso di classe Java toohello dell'applicazione e aggiunta dell'applicazione.
5. Verificare che l'archivio chiavi cacerts contiene un certificato di autorità di certificazione sicura Equifax hello con 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Buongiorno seriale numero è 35:DE:F4:CF e impronta digitale SHA1 di hello è D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Questo è certificato di autorità di certificazione certificato hello per hello [https://api.twilio.com] [ twilio_api_service] servizio, che viene chiamato quando si utilizza Twilio APIs. Per informazioni sull'aggiunta di archivio cacert del JDK tooyour questa autorità di certificazione certificato, vedere [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java][add_ca_cert].

Inoltre, avere familiarità con informazioni hello [la creazione di un hello Hello World applicazione mediante Azure Toolkit per Eclipse][azure_java_eclipse_hello_world], o con altre tecniche per l'hosting di applicazioni Java in Azure se si non si usa Eclipse, è consigliabile.

## <a name="create-a-web-form-for-making-a-call"></a>Creare un modulo Web per effettuare una chiamata
Hello seguente codice mostra come toocreate un web form dati utente tooretrieve per effettuare una chiamata. Ai fini di questo esempio, è stato creato un nuovo progetto Web dinamico denominato **TwilioCloud** ed è stato aggiunto il file JSP **callform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Creare una chiamata di hello toomake codice hello
Hello codice riportato di seguito, viene chiamato al termine del modulo hello visualizzato da callform.jsp utente hello, Crea messaggio hello e genera l'errore chiamata hello. Ai fini di questo esempio, un file JSP hello denominato **makecall.jsp** ed è stato aggiunto toohello **TwilioCloud** progetto. (Utilizzare l'account di Twilio e l'autenticazione del token anziché i valori segnaposto hello assegnati troppo**accountSID** e **authToken** codice hello riportato di seguito.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

Inoltre toomaking hello chiamata, makecall.jsp Visualizza lo stato della chiamata di hello endpoint Twilio hello e versione dell'API. Un esempio è hello cattura di schermata seguente:

![Risposta a chiamata di Azure tramite Twilio e Java][twilio_java_response]

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
Seguenti sono hello toorun passaggi di alto livello dell'applicazione. i dettagli relativi questi passaggi sono reperibile in [la creazione di un hello Hello World applicazione mediante Azure Toolkit per Eclipse][azure_java_eclipse_hello_world].

1. Esportare il toohello TwilioCloud WAR Azure **approot** cartella. 
2. Modificare **startup.cmd** toounzip il WAR TwilioCloud.
3. Compilare l'applicazione hello emulatore di calcolo.
4. Avviare la distribuzione nell'emulatore di calcolo hello.
5. Aprire un browser ed eseguire **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Immettere i valori in formato hello, fare clic su **effettua questa chiamata**e quindi visualizzare i risultati di hello nella makecall.jsp.

Quando si è pronti toodeploy tooAzure, ricompilare per toohello distribuzione cloud, distribuire tooAzure ed eseguire http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp nel browser hello (il valore sostitutivo per *your_hosted_name*).

## <a name="next-steps"></a>Passaggi successivi
Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in Java in Azure. Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità. ad esempio:

* Anziché utilizzare un web form, è possibile usare BLOB di archiviazione di Azure o i numeri di telefono toostore Database SQL e chiamare testo. Per informazioni sull'utilizzo di BLOB di archiviazione di Azure in Java, vedere [come tooUse hello servizio di archiviazione Blob da Java][howto_blob_storage_java]. Per informazioni sull'utilizzo di Database SQL in Java, vedere [con Database SQL in Java][howto_sql_azure_java].
* È possibile utilizzare **RoleEnvironment.getConfigurationSettings** tooretrieve ID dell'account Twilio hello e l'autenticazione del token da impostazioni di configurazione della distribuzione, anziché a livello di codice i valori hello in makecall.jsp. Per informazioni su hello **RoleEnvironment** classe, vedere [Using hello libreria di Runtime del servizio di Azure in JSP] [ azure_runtime_jsp] e la documentazione di pacchetto di Runtime del servizio Azure hello in [http://dl.windowsazure.com/javadoc][azure_javadoc].
* codice makecall.jsp Hello assegna un URL fornito Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variabile. Questo URL fornisce una risposta di Twilio Markup Language (TwiML) che informano Twilio come tooproceed con hello chiama. Ad esempio, può contenere i hello TwiML che viene restituito un  **&lt;pronuncia&gt;**  verbo risultante in testo non viene pronunciata toohello chiamata destinatario. Anziché utilizzare l'URL fornito Twilio hello, è possibile creare una richiesta del tooTwilio toorespond proprio servizio. Per ulteriori informazioni, vedere [come tooUse Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java]. Ulteriori informazioni su TwiML sono reperibile in [http://www.twilio.com/docs/api/twiml][twiml]e altre informazioni su  **&lt;pronuncia&gt;**  e altri verbi Twilio sono reperibile in [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Leggere le indicazioni sulla sicurezza in hello Twilio [https://www.twilio.com/docs/security][twilio_docs_security].

Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Vedere anche
* [Come tooUse Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java]
* [Aggiunta di un archivio certificati Autorità di certificazione di Java di toohello certificato][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
