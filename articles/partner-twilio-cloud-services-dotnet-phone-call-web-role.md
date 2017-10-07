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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Come toomake un telefono chiamata tramite Twilio in un ruolo web in Azure
Questa guida illustra come toouse Twilio toomake una chiamata da una pagina web ospitato in Azure. un'applicazione Hello risultante richiede hello utente toomake di una chiamata con hello dato numero e il messaggio, come illustrato nella seguente schermata hello.

![Modulo di chiamata di Azure con Twilio e ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Prerequisiti
Sarà necessario seguente hello toodo codice hello toouse in questo argomento:

1. Acquisizione di un account di Twilio e l'autenticazione token da hello [Twilio Console][twilio_console]. tooget avviato con Twilio, sign in [https://www.twilio.com/try-twilio][try_twilio]. Per informazioni sui prezzi di Twilio, visitare la pagina [http://www.twilio.com/pricing][twilio_pricing]. Per informazioni sulle API fornita da Twilio hello, vedere [http://www.twilio.com/voice/api][twilio_api].
2. Aggiungere hello *libreria .NET di Twilio* ruolo web tooyour. Vedere **tooadd hello Twilio librerie tooyour progetto del ruolo web**, più avanti in questo argomento.

È necessario conoscere le modalità di creazione di un [ruolo Web di base in Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Procedura: Creare un modulo Web per effettuare una chiamata
<a id="use_nuget"></a>tooadd hello Twilio librerie tooyour progetto ruolo web:

1. Aprire la soluzione in Visual Studio.
2. Fare clic con il pulsante destro del mouse su **Riferimenti**.
3. Scegliere **Manage NuGet Packages**.
4. Fare clic su **Online**.
5. Nella casella di ricerca hello online, digitare *twilio*.
6. Fare clic su **installare** pacchetto Twilio hello.

Hello seguente codice mostra come toocreate un web form dati utente tooretrieve per effettuare una chiamata. In questo esempio viene creato un ruolo Web ASP.NET denominato **TwilioCloud** .

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

## <a id="howtocreatecode"></a>Procedura: creare hello codice toomake hello chiamata
Hello codice riportato di seguito, viene chiamato al termine del modulo hello utente hello, Crea messaggio hello e genera l'errore chiamata hello. In questo esempio, il codice di hello viene eseguito nel gestore dell'evento onclick hello del pulsante hello in form di hello. (Utilizzare l'account di Twilio e l'autenticazione del token anziché i valori segnaposto hello assegnati troppo`accountSID` e `authToken` codice hello riportato di seguito.)

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

viene effettuata la chiamata Hello e vengono visualizzati lo stato della chiamata di hello endpoint Twilio hello e versione dell'API. Hello seguente schermata Mostra output da un esempio di esecuzione.

![Risposta a chiamata di Azure tramite Twilio e ASP.NET][twilio_dotnet_basic_form_output]

Per altre informazioni su TwiML, vedere [http://www.twilio.com/docs/api/twiml][twiml]. Per altre informazioni su &lt;Say&gt; e altri verbi TwiML, vedere [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Passaggi successivi
Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in un ruolo web ASP.NET in Azure. Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità. ad esempio:

* Anziché utilizzare un web form, è possibile utilizzare l'archiviazione Blob di Azure o un numeri di telefono toostore istanza Database SQL di Azure e chiamare testo. Per informazioni sull'utilizzo di BLOB in Azure, vedere [come toouse hello servizio di archiviazione Blob di Azure in .NET][howto_blob_storage_dotnet]. Per informazioni sull'utilizzo di Database SQL, vedere [come toouse Database SQL di Azure in applicazioni .NET][howto_sql_azure_dotnet].
* È possibile utilizzare `RoleEnvironment.getConfigurationSettings` ID dell'account Twilio tooretrieve hello e l'autenticazione del token da impostazioni di configurazione della distribuzione, anziché a livello di codice i valori hello del modulo. Per informazioni su hello `RoleEnvironment` classe, vedere [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Leggere le istruzioni di sicurezza Twilio hello in [https://www.twilio.com/docs/security][twilio_docs_security].
* Per altre informazioni su Twilio, visitare la pagina [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Vedere anche
* [Come toouse Twilio per le funzionalità audio e SMS da Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

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
