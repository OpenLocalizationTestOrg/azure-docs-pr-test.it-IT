---
title: Come effettuare una chiamata telefonica da Twilio (.NET) | Microsoft Docs
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Esempi di codice scritti in .NET.
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="0e787-104">Come effettuare una chiamata tramite Twilio in un ruolo Web in Azure</span><span class="sxs-lookup"><span data-stu-id="0e787-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="0e787-105">In questa guida viene illustrato come usare Twilio per effettuare una chiamata da una pagina Web ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="0e787-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="0e787-106">L'applicazione risultante chiede all'utente di eseguire una chiamata con il numero e il messaggio specificati, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="0e787-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Modulo di chiamata di Azure con Twilio e ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="0e787-108"><a name="twilio-prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e787-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="0e787-109">Per usare il codice in questo argomento è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e787-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="0e787-110">Ottenere un account Twilio e un token di autenticazione dalla [console di Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="0e787-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="0e787-111">Per iniziare a usare Twilio, effettuare l'iscrizione alla pagina [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="0e787-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="0e787-112">Per informazioni sui prezzi di Twilio, visitare la pagina [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="0e787-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="0e787-113">Per informazioni sull'API fornita da Twilio, vedere [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="0e787-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="0e787-114">Aggiungere la *libreria .NET di Twilio* al ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="0e787-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="0e787-115">Vedere **Per aggiungere le librerie Twilio al progetto di ruolo Web** più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0e787-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="0e787-116">È necessario conoscere le modalità di creazione di un [ruolo Web di base in Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="0e787-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="0e787-117"><a name="howtocreateform"></a>Procedura: Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="0e787-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="0e787-118"><a id="use_nuget"></a>Per aggiungere le librerie Twilio al progetto di ruolo Web:</span><span class="sxs-lookup"><span data-stu-id="0e787-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="0e787-119">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e787-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="0e787-120">Fare clic con il pulsante destro del mouse su **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="0e787-120">Right-click **References**.</span></span>
3. <span data-ttu-id="0e787-121">Scegliere **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="0e787-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="0e787-122">Fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="0e787-122">Click **Online**.</span></span>
5. <span data-ttu-id="0e787-123">Nella casella di ricerca online digitare *twilio*.</span><span class="sxs-lookup"><span data-stu-id="0e787-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="0e787-124">Fare clic su **Install** sul pacchetto Twilio.</span><span class="sxs-lookup"><span data-stu-id="0e787-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="0e787-125">Nel codice seguente viene illustrato come creare un modulo Web per recuperare i dati utente per l'esecuzione di una chiamata.</span><span class="sxs-lookup"><span data-stu-id="0e787-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="0e787-126">In questo esempio viene creato un ruolo Web ASP.NET denominato **TwilioCloud** .</span><span class="sxs-lookup"><span data-stu-id="0e787-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="0e787-127"><a id="howtocreatecode"></a>Procedura: Creare il codice per effettuare la chiamata</span><span class="sxs-lookup"><span data-stu-id="0e787-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="0e787-128">Il codice seguente, chiamato quando l'utente completa il modulo, crea il messaggio di chiamata e genera la chiamata.</span><span class="sxs-lookup"><span data-stu-id="0e787-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="0e787-129">In questo esempio, il codice viene eseguito sul gestore dell'evento onclick del pulsante del modulo.</span><span class="sxs-lookup"><span data-stu-id="0e787-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="0e787-130">Nel codice seguente sostituire i valori segnaposto assegnati a `accountSID` e `authToken` con il proprio account e il token di autenticazione Twilio.</span><span class="sxs-lookup"><span data-stu-id="0e787-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="0e787-131">La chiamata viene effettuata e vengono visualizzati l'endpoint Twilio, la versione dell'API e lo stato della chiamata.</span><span class="sxs-lookup"><span data-stu-id="0e787-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="0e787-132">Nella schermata seguente viene illustrato l'output di un'esecuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="0e787-132">The following screenshot shows output from a sample run.</span></span>

![Risposta a chiamata di Azure tramite Twilio e ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="0e787-134">Per altre informazioni su TwiML, vedere [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="0e787-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="0e787-135">Per altre informazioni su &lt;Say&gt; e altri verbi TwiML, vedere [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="0e787-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="0e787-136"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e787-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="0e787-137">Questo codice ha lo scopo di illustrare le funzionalità di base dell'utilizzo di Twilio in un ruolo Web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="0e787-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="0e787-138">Prima di eseguire la distribuzione in Azure in produzione, può essere necessario aggiungere ulteriori funzionalità per la gestione degli errori o per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="0e787-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="0e787-139">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0e787-139">For example:</span></span>

* <span data-ttu-id="0e787-140">Anziché usare un modulo Web, è possibile usare l'archivio BLOB di Azure o un'istanza di database SQL di Azure per l'archiviazione di numeri di telefono e testo delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="0e787-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="0e787-141">Per informazioni sull'uso dei BLOB in Azure, vedere [Come usare il servizio di archiviazione BLOB di Azure in .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="0e787-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="0e787-142">Per informazioni sull'uso del database SQL, vedere [Come usare il database SQL di Azure in applicazioni .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="0e787-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="0e787-143">È possibile usare `RoleEnvironment.getConfigurationSettings` per recuperare l'ID e il token di autenticazione dell'account Twilio dalle impostazioni di configurazione della distribuzione, anziché impostare i valori hardcoded nel modulo.</span><span class="sxs-lookup"><span data-stu-id="0e787-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="0e787-144">Per informazioni sulla classe `RoleEnvironment`, vedere [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="0e787-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="0e787-145">Leggere le linee guida sulla sicurezza di Twilio all'indirizzo [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="0e787-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="0e787-146">Per altre informazioni su Twilio, visitare la pagina [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="0e787-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="0e787-147"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0e787-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0e787-148">Come usare Twilio per le funzionalità voce ed SMS da Azure</span><span class="sxs-lookup"><span data-stu-id="0e787-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
