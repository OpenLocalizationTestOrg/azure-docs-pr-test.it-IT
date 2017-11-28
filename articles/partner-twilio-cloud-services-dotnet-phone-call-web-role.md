---
title: aaaHow toomake una telefonata da Twilio (.NET) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Esempi di codice scritti in .NET.
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
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="74db8-104">Come toomake un telefono chiamata tramite Twilio in un ruolo web in Azure</span><span class="sxs-lookup"><span data-stu-id="74db8-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="74db8-105">Questa guida illustra come toouse Twilio toomake una chiamata da una pagina web ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="74db8-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="74db8-106">un'applicazione Hello risultante richiede hello utente toomake di una chiamata con hello dato numero e il messaggio, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="74db8-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Modulo di chiamata di Azure con Twilio e ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="74db8-108"><a name="twilio-prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="74db8-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="74db8-109">Sarà necessario seguente hello toodo codice hello toouse in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="74db8-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="74db8-110">Acquisizione di un account di Twilio e l'autenticazione token da hello [Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="74db8-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="74db8-111">tooget avviato con Twilio, sign in [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="74db8-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="74db8-112">Per informazioni sui prezzi di Twilio, visitare la pagina [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="74db8-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="74db8-113">Per informazioni sulle API fornita da Twilio hello, vedere [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="74db8-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="74db8-114">Aggiungere hello *libreria .NET di Twilio* ruolo web tooyour.</span><span class="sxs-lookup"><span data-stu-id="74db8-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="74db8-115">Vedere **tooadd hello Twilio librerie tooyour progetto del ruolo web**, più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="74db8-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="74db8-116">È necessario conoscere le modalità di creazione di un [ruolo Web di base in Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="74db8-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="74db8-117"><a name="howtocreateform"></a>Procedura: Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="74db8-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="74db8-118"><a id="use_nuget"></a>tooadd hello Twilio librerie tooyour progetto ruolo web:</span><span class="sxs-lookup"><span data-stu-id="74db8-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="74db8-119">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74db8-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="74db8-120">Fare clic con il pulsante destro del mouse su **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="74db8-120">Right-click **References**.</span></span>
3. <span data-ttu-id="74db8-121">Scegliere **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="74db8-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="74db8-122">Fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="74db8-122">Click **Online**.</span></span>
5. <span data-ttu-id="74db8-123">Nella casella di ricerca hello online, digitare *twilio*.</span><span class="sxs-lookup"><span data-stu-id="74db8-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="74db8-124">Fare clic su **installare** pacchetto Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="74db8-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="74db8-125">Hello seguente codice mostra come toocreate un web form dati utente tooretrieve per effettuare una chiamata.</span><span class="sxs-lookup"><span data-stu-id="74db8-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="74db8-126">In questo esempio viene creato un ruolo Web ASP.NET denominato **TwilioCloud** .</span><span class="sxs-lookup"><span data-stu-id="74db8-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="74db8-127"><a id="howtocreatecode"></a>Procedura: creare hello codice toomake hello chiamata</span><span class="sxs-lookup"><span data-stu-id="74db8-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="74db8-128">Hello codice riportato di seguito, viene chiamato al termine del modulo hello utente hello, Crea messaggio hello e genera l'errore chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="74db8-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="74db8-129">In questo esempio, il codice di hello viene eseguito nel gestore dell'evento onclick hello del pulsante hello in form di hello.</span><span class="sxs-lookup"><span data-stu-id="74db8-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="74db8-130">(Utilizzare l'account di Twilio e l'autenticazione del token anziché i valori segnaposto hello assegnati troppo`accountSID` e `authToken` codice hello riportato di seguito.)</span><span class="sxs-lookup"><span data-stu-id="74db8-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="74db8-131">viene effettuata la chiamata Hello e vengono visualizzati lo stato della chiamata di hello endpoint Twilio hello e versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="74db8-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="74db8-132">Hello seguente schermata Mostra output da un esempio di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="74db8-132">hello following screenshot shows output from a sample run.</span></span>

![Risposta a chiamata di Azure tramite Twilio e ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="74db8-134">Per altre informazioni su TwiML, vedere [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="74db8-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="74db8-135">Per altre informazioni su &lt;Say&gt; e altri verbi TwiML, vedere [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="74db8-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="74db8-136"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74db8-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="74db8-137">Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in un ruolo web ASP.NET in Azure.</span><span class="sxs-lookup"><span data-stu-id="74db8-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="74db8-138">Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="74db8-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="74db8-139">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="74db8-139">For example:</span></span>

* <span data-ttu-id="74db8-140">Anziché utilizzare un web form, è possibile utilizzare l'archiviazione Blob di Azure o un numeri di telefono toostore istanza Database SQL di Azure e chiamare testo.</span><span class="sxs-lookup"><span data-stu-id="74db8-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="74db8-141">Per informazioni sull'utilizzo di BLOB in Azure, vedere [come toouse hello servizio di archiviazione Blob di Azure in .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="74db8-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="74db8-142">Per informazioni sull'utilizzo di Database SQL, vedere [come toouse Database SQL di Azure in applicazioni .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="74db8-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="74db8-143">È possibile utilizzare `RoleEnvironment.getConfigurationSettings` ID dell'account Twilio tooretrieve hello e l'autenticazione del token da impostazioni di configurazione della distribuzione, anziché a livello di codice i valori hello del modulo.</span><span class="sxs-lookup"><span data-stu-id="74db8-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="74db8-144">Per informazioni su hello `RoleEnvironment` classe, vedere [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="74db8-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="74db8-145">Leggere le istruzioni di sicurezza Twilio hello in [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="74db8-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="74db8-146">Per altre informazioni su Twilio, visitare la pagina [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="74db8-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="74db8-147"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="74db8-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="74db8-148">Come toouse Twilio per le funzionalità audio e SMS da Azure</span><span class="sxs-lookup"><span data-stu-id="74db8-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
