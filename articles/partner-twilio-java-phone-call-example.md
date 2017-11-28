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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="cb862-103">Come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure</span><span class="sxs-lookup"><span data-stu-id="cb862-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="cb862-104">Hello seguente esempio viene illustrato come usare Twilio toomake una chiamata da una pagina web ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb862-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="cb862-105">un'applicazione Hello risultante utente verrà chiesto hello di valori di chiamata telefonica, come illustrato nella seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="cb862-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Modulo di chiamata di Azure con Twilio e Java][twilio_java]

<span data-ttu-id="cb862-107">È necessario seguente hello toodo codice hello toouse in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="cb862-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="cb862-108">Ottenere un account e un token di autenticazione Twilio.</span><span class="sxs-lookup"><span data-stu-id="cb862-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="cb862-109">tooget introduttiva Twilio, valutare al prezzo [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="cb862-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="cb862-110">È possibile iscriversi al [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="cb862-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="cb862-111">Per informazioni sulle API fornita da Twilio hello, vedere [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="cb862-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="cb862-112">Ottenere hello JAR Twilio.</span><span class="sxs-lookup"><span data-stu-id="cb862-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="cb862-113">In [https://github.com/twilio/twilio-java][twilio_java_github], è possibile scaricare origini GitHub hello e creare la propria JAR o scaricare un file JAR preesistente (con o senza dipendenze).</span><span class="sxs-lookup"><span data-stu-id="cb862-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="cb862-114">codice Hello in questo argomento è stato scritto utilizzando hello predefinite JAR TwilioJava 3.3.8 con dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cb862-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="cb862-115">Aggiungere hello JAR tooyour percorso di compilazione Java.</span><span class="sxs-lookup"><span data-stu-id="cb862-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="cb862-116">Se si usa Eclipse toocreate questa applicazione Java, includere hello Twilio JAR nel file di distribuzione dell'applicazione (WAR) con funzionalità di distribuzione di assembly di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cb862-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="cb862-117">Se non si utilizza Eclipse toocreate questa applicazione Java, verificare che sia incluso all'interno di hello hello JAR Twilio stesso ruolo di Azure come percorso di classe Java toohello dell'applicazione e aggiunta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb862-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="cb862-118">Verificare che l'archivio chiavi cacerts contiene un certificato di autorità di certificazione sicura Equifax hello con 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Buongiorno seriale numero è 35:DE:F4:CF e impronta digitale SHA1 di hello è D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="cb862-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="cb862-119">Questo è certificato di autorità di certificazione certificato hello per hello [https://api.twilio.com] [ twilio_api_service] servizio, che viene chiamato quando si utilizza Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="cb862-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="cb862-120">Per informazioni sull'aggiunta di archivio cacert del JDK tooyour questa autorità di certificazione certificato, vedere [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="cb862-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="cb862-121">Inoltre, avere familiarità con informazioni hello [la creazione di un hello Hello World applicazione mediante Azure Toolkit per Eclipse][azure_java_eclipse_hello_world], o con altre tecniche per l'hosting di applicazioni Java in Azure se si non si usa Eclipse, è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="cb862-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="cb862-122">Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="cb862-122">Create a web form for making a call</span></span>
<span data-ttu-id="cb862-123">Hello seguente codice mostra come toocreate un web form dati utente tooretrieve per effettuare una chiamata.</span><span class="sxs-lookup"><span data-stu-id="cb862-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="cb862-124">Ai fini di questo esempio, è stato creato un nuovo progetto Web dinamico denominato **TwilioCloud** ed è stato aggiunto il file JSP **callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="cb862-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="cb862-125">Creare una chiamata di hello toomake codice hello</span><span class="sxs-lookup"><span data-stu-id="cb862-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="cb862-126">Hello codice riportato di seguito, viene chiamato al termine del modulo hello visualizzato da callform.jsp utente hello, Crea messaggio hello e genera l'errore chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="cb862-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="cb862-127">Ai fini di questo esempio, un file JSP hello denominato **makecall.jsp** ed è stato aggiunto toohello **TwilioCloud** progetto.</span><span class="sxs-lookup"><span data-stu-id="cb862-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="cb862-128">(Utilizzare l'account di Twilio e l'autenticazione del token anziché i valori segnaposto hello assegnati troppo**accountSID** e **authToken** codice hello riportato di seguito.)</span><span class="sxs-lookup"><span data-stu-id="cb862-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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

<span data-ttu-id="cb862-129">Inoltre toomaking hello chiamata, makecall.jsp Visualizza lo stato della chiamata di hello endpoint Twilio hello e versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="cb862-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="cb862-130">Un esempio è hello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="cb862-130">An example is hello following screen shot:</span></span>

![Risposta a chiamata di Azure tramite Twilio e Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="cb862-132">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="cb862-132">Run hello application</span></span>
<span data-ttu-id="cb862-133">Seguenti sono hello toorun passaggi di alto livello dell'applicazione. i dettagli relativi questi passaggi sono reperibile in [la creazione di un hello Hello World applicazione mediante Azure Toolkit per Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="cb862-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="cb862-134">Esportare il toohello TwilioCloud WAR Azure **approot** cartella.</span><span class="sxs-lookup"><span data-stu-id="cb862-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="cb862-135">Modificare **startup.cmd** toounzip il WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="cb862-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="cb862-136">Compilare l'applicazione hello emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="cb862-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="cb862-137">Avviare la distribuzione nell'emulatore di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="cb862-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="cb862-138">Aprire un browser ed eseguire **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="cb862-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="cb862-139">Immettere i valori in formato hello, fare clic su **effettua questa chiamata**e quindi visualizzare i risultati di hello nella makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="cb862-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="cb862-140">Quando si è pronti toodeploy tooAzure, ricompilare per toohello distribuzione cloud, distribuire tooAzure ed eseguire http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp nel browser hello (il valore sostitutivo per *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="cb862-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb862-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb862-141">Next steps</span></span>
<span data-ttu-id="cb862-142">Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb862-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="cb862-143">Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cb862-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="cb862-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cb862-144">For example:</span></span>

* <span data-ttu-id="cb862-145">Anziché utilizzare un web form, è possibile usare BLOB di archiviazione di Azure o i numeri di telefono toostore Database SQL e chiamare testo.</span><span class="sxs-lookup"><span data-stu-id="cb862-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="cb862-146">Per informazioni sull'utilizzo di BLOB di archiviazione di Azure in Java, vedere [come tooUse hello servizio di archiviazione Blob da Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="cb862-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="cb862-147">Per informazioni sull'utilizzo di Database SQL in Java, vedere [con Database SQL in Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="cb862-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="cb862-148">È possibile utilizzare **RoleEnvironment.getConfigurationSettings** tooretrieve ID dell'account Twilio hello e l'autenticazione del token da impostazioni di configurazione della distribuzione, anziché a livello di codice i valori hello in makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="cb862-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="cb862-149">Per informazioni su hello **RoleEnvironment** classe, vedere [Using hello libreria di Runtime del servizio di Azure in JSP] [ azure_runtime_jsp] e la documentazione di pacchetto di Runtime del servizio Azure hello in [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="cb862-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="cb862-150">codice makecall.jsp Hello assegna un URL fornito Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variabile.</span><span class="sxs-lookup"><span data-stu-id="cb862-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="cb862-151">Questo URL fornisce una risposta di Twilio Markup Language (TwiML) che informano Twilio come tooproceed con hello chiama.</span><span class="sxs-lookup"><span data-stu-id="cb862-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="cb862-152">Ad esempio, può contenere i hello TwiML che viene restituito un  **&lt;pronuncia&gt;**  verbo risultante in testo non viene pronunciata toohello chiamata destinatario.</span><span class="sxs-lookup"><span data-stu-id="cb862-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="cb862-153">Anziché utilizzare l'URL fornito Twilio hello, è possibile creare una richiesta del tooTwilio toorespond proprio servizio. Per ulteriori informazioni, vedere [come tooUse Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="cb862-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="cb862-154">Ulteriori informazioni su TwiML sono reperibile in [http://www.twilio.com/docs/api/twiml][twiml]e altre informazioni su  **&lt;pronuncia&gt;**  e altri verbi Twilio sono reperibile in [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="cb862-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="cb862-155">Leggere le indicazioni sulla sicurezza in hello Twilio [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="cb862-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="cb862-156">Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="cb862-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="cb862-157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cb862-157">See Also</span></span>
* <span data-ttu-id="cb862-158">[Come tooUse Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="cb862-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="cb862-159">[Aggiunta di un archivio certificati Autorità di certificazione di Java di toohello certificato][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="cb862-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
