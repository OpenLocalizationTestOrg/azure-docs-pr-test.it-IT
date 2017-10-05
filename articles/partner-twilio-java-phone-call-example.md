---
title: Come effettuare una chiamata telefonica da Twilio (Java) | Microsoft Docs
description: Informazioni su come effettuare una chiamata telefonica da una pagina Web usando Twilio con un'applicazione Java in Azure.
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
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="7b056-103">Come effettuare una chiamata tramite Twilio in un'applicazione Java in Azure</span><span class="sxs-lookup"><span data-stu-id="7b056-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="7b056-104">Nell'esempio seguente viene illustrato come è possibile usare Twilio per effettuare una chiamata da una pagina Web ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b056-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="7b056-105">L'applicazione risultante chiederà all'utente di inserire i valori relativi alla chiamata telefonica, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="7b056-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Modulo di chiamata di Azure con Twilio e Java][twilio_java]

<span data-ttu-id="7b056-107">Per usare il codice in questo argomento è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7b056-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="7b056-108">Ottenere un account e un token di autenticazione Twilio.</span><span class="sxs-lookup"><span data-stu-id="7b056-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="7b056-109">Per informazioni sui prezzi di Twilio, vedere la pagina [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="7b056-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="7b056-110">È possibile iscriversi al [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="7b056-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="7b056-111">Per informazioni sull'API fornite da Twilio, vedere [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="7b056-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="7b056-112">Ottenere il file JAR di Twilio.</span><span class="sxs-lookup"><span data-stu-id="7b056-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="7b056-113">Dall'indirizzo [https://github.com/twilio/twilio-java][twilio_java_github] è possibile scaricare i file di origine disponibili in GitHub e creare un file JAR personalizzato o scaricarne uno precompilato, con o senza dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7b056-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="7b056-114">Il codice in questo argomento è stato scritto utilizzando il JAR precompilato TwilioJava-3.3.8-with-dependencies.</span><span class="sxs-lookup"><span data-stu-id="7b056-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="7b056-115">Aggiungere il file JAR al percorso di compilazione Java.</span><span class="sxs-lookup"><span data-stu-id="7b056-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="7b056-116">Se si usa Eclipse per creare l'applicazione Java, includere il JAR di Twilio nel file WAR per la distribuzione dell'applicazione usando l'assembly di distribuzione di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7b056-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="7b056-117">Se non si utilizza Eclipse per creare l'applicazione Java, verificare che il JAR di Twilio sia incluso nello stesso ruolo di Azure dell'applicazione Java e che sia stato aggiunto al percorso della classe dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7b056-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="7b056-118">Verificare che l'archivio chiavi cacerts del JDK contenga il certificato Equifax Secure Certificate Authority con ID digitale MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (il numero di serie è 35:DE:F4:CF e l'ID digitale SHA1 è D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="7b056-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="7b056-119">Si tratta del certificato dell'Autorità di certificazione (CA) per il servizio [https://api.twilio.com][twilio_api_service], che viene chiamato quando si usano le API Twilio.</span><span class="sxs-lookup"><span data-stu-id="7b056-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="7b056-120">Per informazioni sull'aggiunta di questo certificato CA archivio cacert del JDK, vedere [aggiungere un certificato all'archivio di certificati CA Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="7b056-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="7b056-121">Inoltre, avere familiarità con le informazioni relative a [creazione di un Hello World applicazione mediante Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], o con altre tecniche per l'hosting di applicazioni Java in Azure se si è non usa Eclipse, è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="7b056-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="7b056-122">Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="7b056-122">Create a web form for making a call</span></span>
<span data-ttu-id="7b056-123">Nel codice seguente viene illustrato come creare un modulo Web per recuperare i dati utente per l'esecuzione di una chiamata.</span><span class="sxs-lookup"><span data-stu-id="7b056-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="7b056-124">Ai fini di questo esempio, è stato creato un nuovo progetto Web dinamico denominato **TwilioCloud** ed è stato aggiunto il file JSP **callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7b056-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
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

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="7b056-125">Creare il codice per l'esecuzione della chiamata</span><span class="sxs-lookup"><span data-stu-id="7b056-125">Create the code to make the call</span></span>
<span data-ttu-id="7b056-126">Il codice seguente, chiamato quando l'utente completa il modulo visualizzato da callform.jsp, crea il messaggio di chiamata e genera la chiamata.</span><span class="sxs-lookup"><span data-stu-id="7b056-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="7b056-127">Ai fini di questo esempio, il file JSP è denominato **makecall.jsp** ed è stato aggiunto al progetto **TwilioCloud**.</span><span class="sxs-lookup"><span data-stu-id="7b056-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="7b056-128">Nel codice seguente sostituire i valori segnaposto assegnati a **accountSID** e **authToken** con il proprio account e il token di autenticazione Twilio.</span><span class="sxs-lookup"><span data-stu-id="7b056-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

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
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
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

<span data-ttu-id="7b056-129">Oltre ad eseguire la chiamata, makecall.jsp visualizza l'endpoint Twilio, la versione dell'API e lo stato della chiamata.</span><span class="sxs-lookup"><span data-stu-id="7b056-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="7b056-130">Nella schermata di seguito viene visualizzato un esempio:</span><span class="sxs-lookup"><span data-stu-id="7b056-130">An example is the following screen shot:</span></span>

![Risposta a chiamata di Azure tramite Twilio e Java][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="7b056-132">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="7b056-132">Run the application</span></span>
<span data-ttu-id="7b056-133">Ecco i passaggi principali per eseguire l'applicazione. i dettagli relativi questi passaggi sono reperibile in [creazione di un Hello World applicazione mediante Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="7b056-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="7b056-134">Esportare il file WAR TwilioCloud nella cartella **approot** di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b056-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="7b056-135">Modificare **startup.cmd** per decomprimere il file WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="7b056-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="7b056-136">Compilare l'applicazione per l'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="7b056-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="7b056-137">Avviare la distribuzione nell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="7b056-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="7b056-138">Aprire un browser ed eseguire **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7b056-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="7b056-139">Immettere i valori nel modulo, fare clic su **Make this call**e quindi visualizzare i risultati in makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="7b056-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="7b056-140">Quando si è pronti a distribuire l'applicazione in Azure, ricompilare per la distribuzione nel cloud, distribuire in Azure ed eseguire http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp nel browser, sostituendo *your_hosted_name* con il proprio valore.</span><span class="sxs-lookup"><span data-stu-id="7b056-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b056-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b056-141">Next steps</span></span>
<span data-ttu-id="7b056-142">Questo codice ha lo scopo di illustrare le funzionalità di base dell'utilizzo di Twilio con Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b056-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="7b056-143">Prima di eseguire la distribuzione in Azure in produzione, può essere necessario aggiungere ulteriori funzionalità per la gestione degli errori o per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="7b056-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="7b056-144">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7b056-144">For example:</span></span>

* <span data-ttu-id="7b056-145">Anziché utilizzare un modulo Web, è possibile utilizzare l'archiviazione BLOB o un database SQL di Azure per l'archiviazione di numeri di telefono e testo delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="7b056-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="7b056-146">Per informazioni sull'utilizzo di BLOB di archiviazione di Azure in Java, vedere [illustrato come utilizzare il servizio di archiviazione Blob da Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="7b056-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="7b056-147">Per informazioni sull'utilizzo di Database SQL in Java, vedere [con Database SQL in Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="7b056-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="7b056-148">È possibile usare **RoleEnvironment.getConfigurationSettings** per recuperare l'ID e il token di autenticazione dell'account Twilio dalle impostazioni di configurazione della distribuzione, anziché impostare i valori come hardcoded in makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="7b056-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="7b056-149">Per informazioni di **RoleEnvironment** classe, vedere [utilizzando la libreria di Runtime del servizio Azure in JSP] [ azure_runtime_jsp] e la documentazione di pacchetto di Runtime del servizio di Azure all'indirizzo [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="7b056-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="7b056-150">Il codice makecall.jsp assegna un URL fornito Twilio, [http://twimlets.com/message][twimlet_message_url]al **Url** variabile.</span><span class="sxs-lookup"><span data-stu-id="7b056-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="7b056-151">Tale URL fornisce una risposta TwiML (Twilio Markup Language) che indica a Twilio in che modo eseguire la chiamata.</span><span class="sxs-lookup"><span data-stu-id="7b056-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="7b056-152">Ad esempio, la risposta TwiML restituita può contenere un verbo **&lt;Say&gt;** che offre una versione parlata del testo al destinatario della chiamata.</span><span class="sxs-lookup"><span data-stu-id="7b056-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="7b056-153">Anziché utilizzare l'URL fornito Twilio, è possibile creare il proprio servizio per rispondere alla richiesta di Twilio; Per ulteriori informazioni, vedere [come usare Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="7b056-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="7b056-154">Ulteriori informazioni su TwiML sono reperibile in [http://www.twilio.com/docs/api/twiml][twiml]e altre informazioni su  **&lt;pronuncia&gt;**  e altri verbi Twilio sono reperibile in [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="7b056-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="7b056-155">Leggere le linee guida sulla sicurezza di Twilio all'indirizzo [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="7b056-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="7b056-156">Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="7b056-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="7b056-157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7b056-157">See Also</span></span>
* <span data-ttu-id="7b056-158">[Come usare Twilio per funzionalità voce ed SMS in Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="7b056-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="7b056-159">[Aggiunta di un certificato nell'archivio certificati Autorità di certificazione di Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="7b056-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

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
