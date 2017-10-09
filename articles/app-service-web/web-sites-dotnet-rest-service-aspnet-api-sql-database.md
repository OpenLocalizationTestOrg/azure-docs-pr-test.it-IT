---
title: un'API REST in Azure con ASP.NET e database SQL aaaCreate | Documenti Microsoft
description: Un'esercitazione che illustra come un'applicazione che utilizza toodeploy hello tooan ASP.NET Web API app web di Azure tramite Visual Studio.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Creare un servizio REST con l'API Web ASP.NET e il database SQL in Servizio app di Azure
Questa esercitazione viene illustrato come toodeploy ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) utilizzando la procedura guidata Pubblica sito Web hello in Visual Studio 2013 o Visual Studio 2013 Community Edition. 

È possibile aprire un account Azure, gratuitamente, e se si dispone già di Visual Studio 2013, hello SDK installa automaticamente Visual Studio 2013 per Web. Sarà quindi possibile iniziare a sviluppare per Azure del tutto gratuitamente.

In questa esercitazione si presuppone che l'utente non abbia mai utilizzato Azure. Dopo aver completato questa esercitazione, è necessario un'app web semplici backup e in esecuzione nel cloud hello.

Si apprenderà come:

* Come tooenable il computer per lo sviluppo di Azure installando hello Azure SDK.
* Come toocreate un Visual Studio ASP.NET MVC 5 del progetto e pubblicarlo tooan app di Azure.
* Come toouse hello tooenable ASP.NET Web API chiamate all'API REST.
* Come toouse un SQL database toostore dati in Azure.
* Come applicazione toopublish Aggiorna tooAzure.

Compilerai un'applicazione web semplice elenco di contatti che si basa su ASP.NET MVC 5 e utilizza hello ADO.NET Entity Framework per l'accesso al database. completa l'applicazione Hello hello illustrato nella figura riportata di seguito:

![schermata del sito web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Creare il progetto hello
1. Avviare Visual Studio 2013.
2. Da hello **File** dal menu **nuovo progetto**.
3. In hello **nuovo progetto** finestra di dialogo espandere **Visual c#** e selezionare **Web** e quindi selezionare **applicazione Web ASP.NET**. Nome di un'applicazione hello **ContactManager** e fare clic su **OK**.
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. In hello **nuovo progetto ASP.NET** la finestra di dialogo, seleziona hello **MVC** modello di controllo **API Web** e quindi fare clic su **Modifica autenticazione**.
5. In hello **Modifica autenticazione** la finestra di dialogo, fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.
   
    ![No Authentication](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    si sta creando un'applicazione Hello esempio non disporrà di funzionalità che richiedono toolog gli utenti in. Per informazioni sulla funzionalità di autenticazione e autorizzazione tooimplement, vedere hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione. 
6. In hello **nuovo progetto ASP.NET** la finestra di dialogo, verificare che hello **Host nel Cloud hello** è selezionata e fare clic su **OK**.

Se non è stato precedentemente firmato in tooAzure, sarà richiesta toosign in.

1. procedura guidata di configurazione Hello suggerirà un nome univoco basato sul *ContactManager* (vedere l'immagine di hello riportata di seguito). Selezionare un'area nelle vicinanze. È possibile utilizzare [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello più bassa latenza datacenter. 
2. Se non è stato creato un server di database, selezionare **Crea nuovo server**e immettere un nome utente e una password per il database.
   
    ![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Se si dispone di un server di database, utilizzare tale toocreate un nuovo database. Server di database sono una risorsa preziosa, e in genere si desidera toocreate più database nella hello stesso server per il test e sviluppo anziché creare un server di database per ogni database. Verificare che il sito web e il database siano in hello stessa area.

![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Impostare l'intestazione di pagina hello e piè di pagina
1. In **Esplora**, espandere hello *Views\Shared* cartella e aprire hello *layout. cshtml* file.
   
    ![File _Layout.cshtml in Esplora soluzioni][newapp004]
2. Sostituire il contenuto di hello di hello *Views\Shared_Layout.cshtml* file con hello seguente codice:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

markup Hello sopra al nome app hello modifiche da "My App ASP.NET" troppo "contatto Manager" che rimuove i collegamenti di hello troppo**Home**, **su** e **contatto**.

### <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
1. Premere CTRL + F5 toorun un'applicazione hello.
   home page dell'applicazione Hello viene visualizzato nel browser predefinito hello.
    ![home page di tooDo elenco](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Questo è tutto ciò che serve toodo si distribuiranno tooAzure un'applicazione hello toocreate ora. La funzionalità di database verrà aggiunta in un secondo momento.

## <a name="deploy-hello-application-tooazure"></a>Distribuire tooAzure applicazione hello
1. In Visual Studio, fare clic sul progetto hello in **Esplora** e selezionare **pubblica** dal menu di scelta rapida hello.
   
    ![Opzione Pubblica nel menu di scelta rapida del progetto][PublishVSSolution]
   
    Hello **pubblica sul Web** apre la procedura guidata.
2. Fare clic su **Pubblica**.

![Scheda Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio avvia il processo di hello di copia hello toohello di file server di Azure. Hello **Output** finestra Mostra intraprese le azioni di distribuzione e segnala il completamento corretto della distribuzione hello.

1. browser predefinito Hello verrà aperta automaticamente toohello URL del sito hello distribuito.
   
   un'applicazione Hello creato è in esecuzione nel cloud hello.
   
   ![pagina iniziale di elenco tooDo in esecuzione in Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Aggiungere un'applicazione di database toohello
Successivamente, verrà aggiornare hello MVC applicazione tooadd hello possibilità toodisplay e aggiornare i contatti e archiviare dati hello in un database. applicazione Hello tooread e il database di hello Entity Framework toocreate hello e aggiornare i dati nel database di hello.

### <a name="add-data-model-classes-for-hello-contacts"></a>Aggiungere le classi di modello di dati per i contatti hello
Creare innanzitutto un semplice modello di dati nel codice.

1. In **Esplora**, fare clic sulla cartella Modelli hello, fare clic su **Aggiungi**e quindi **classe**.
   
    ![Aggiungi classe nel menu di scelta rapida della cartella Modelli][adddb001]
2. In hello **Aggiungi nuovo elemento** della finestra di dialogo Nome hello nuovo file di classe *Contact.cs*, quindi fare clic su **Aggiungi**.
   
    ![Finestra di dialogo Aggiungi nuovo elemento][adddb002]
3. Sostituire il contenuto di hello del file Contacts.cs hello con hello seguente codice.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

Hello **contattare** classe definisce i dati di hello che verranno archiviati per ogni contatto, oltre a una chiave primaria, ContactID, richiesto dal database hello. È possibile ottenere ulteriori informazioni sui modelli di dati in hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Creare pagine web che consentono di toowork agli utenti di app con i contatti hello
Hello funzionalità di scaffolding di ASP.NET MVC hello può generare automaticamente il codice che esegue creare, leggere, aggiornare ed eliminare azioni (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Aggiungere un Controller e una visualizzazione per i dati di hello
1. In **Esplora**, espandere cartella Controllers hello.
2. Compilare il progetto hello **(Ctrl + MAIUSC + B)**. (È necessario compilare il progetto hello prima di utilizzare il meccanismo di scaffolding). 
3. Fare clic sulla cartella controller hello e fare clic su **Aggiungi**, quindi fare clic su **Controller**.
   
    ![Opzione Aggiungi controller nel menu di scelta rapida della cartella Controllers][addcode001]
4. In hello **aggiungere lo scaffolding** nella finestra di dialogo **Controller MVC con visualizzazioni, mediante Entity Framework** e fare clic su **Aggiungi**.
   
   ![Aggiungi controller](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Impostare il nome di controller hello troppo**HomeController**. Selezionare **Contact** come classe del modello. Fare clic su hello **nuovo contesto dati** pulsante e accettare hello predefinito "ContactManager.Models.ContactManagerContext" hello **nuovo tipo di contesto dati**. Fare clic su **Aggiungi**.

    Una finestra di dialogo verrà chiesto: "un file con nome hello HomeController esiste già. Si desidera tooreplace è? ". Fare clic su **Sì**. Si sta sovrascrivendo hello Home Controller che è stato creato con il nuovo progetto di hello. Si utilizzerà hello nuovo Home Controller per l'elenco di contatti.

    In Visual Studio verranno creati metodi e visualizzazioni di un controller per operazioni CRUD di database per oggetti **Contact** .

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Abilitare le migrazioni, creare database hello, aggiungere dati di esempio e un inizializzatore di dati
attività successiva Hello è hello tooenable [migrazioni Code First](http://curah.microsoft.com/55220) funzionalità nel database di hello toocreate ordine basato sul modello di dati hello è stato creato.

1. In hello **strumenti** dal menu **Gestione pacchetti libreria** e quindi **Package Manager Console**.
   
    ![Console di Gestione pacchetti nel menu Strumenti][addcode008]
2. In hello **Package Manager Console** finestra immettere hello comando seguente:
   
        enable-migrations 
   
    Hello **enable-migrations** comando crea un *migrazioni* cartella e lo inserisce in questa cartella un *Configuration.cs* file che è possibile modificare le migrazioni tooconfigure. 
3. In hello **Package Manager Console** finestra immettere hello comando seguente:
   
        add-migration Initial
   
    Hello **iniziale migrazione aggiungere** comando genera una classe denominata  **&lt;date_stamp&gt;iniziale** che crea database hello. primo parametro Hello ( *iniziale* ) è arbitrario e utilizzati toocreate hello nome del file hello. È possibile visualizzare hello nuovi file di classe in **Esplora**.
   
    In hello **iniziale** classe hello **backup** metodo crea tabella Contacts hello e hello **verso il basso** rilascia metodo (utilizzato quando si desidera che lo stato precedente di tooreturn toohello).
4. Aprire hello *Migrations\Configuration.cs* file. 
5. Aggiungere i seguenti spazi dei nomi hello. 
   
         using ContactManager.Models;
6. Sostituire hello *valore di inizializzazione* metodo con hello seguente codice:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    Questo codice precedente verrà inizializzato database hello con le informazioni di contatto hello. Per ulteriori informazioni sui database hello il seeding, vedere [il debug di Entity Framework (EF) database](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. In hello **Package Manager Console** immettere il comando hello:
   
        update-database
   
    ![Comandi di Console di Gestione pacchetti][addcode009]
   
    Hello **aggiornamento database** esecuzioni hello migrazione prima che crea database hello. Per impostazione predefinita, il database di hello viene creato come database di SQL Server Express LocalDB.
8. Premere CTRL + F5 toorun un'applicazione hello. 

un'applicazione Hello Mostra dati di inizializzazione hello e consente di modificare i dettagli e collegamenti Elimina.

![Visualizzazione MVC dei dati][rxz3]

## <a name="edit-hello-view"></a>Modifica vista hello
1. Aprire hello *Views\Home\Index.cshtml* file. Nel passaggio successivo hello, si sostituirà markup hello generato con il codice che usa [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/). Questo codice recupera l'elenco di hello di contatti da mediante API web e JSON e quindi associa hello contattare toohello dati dell'interfaccia utente utilizzando knockout.js. Per ulteriori informazioni, vedere hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione. 
2. Sostituire il contenuto di hello del file hello con hello seguente codice.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Fare clic sulla cartella del contenuto hello e fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento...** .
   
    ![Opzione Aggiungi foglio di stile nel menu di scelta rapida della cartella Content][addcode005]
4. In hello **Aggiungi nuovo elemento** finestra di dialogo immettere **stile** nella casella di ricerca a destra superiore hello e quindi selezionare **foglio di stile**.
    ![Finestra di dialogo Aggiungi nuovo elemento][rxStyle]
5. File con nome hello *Contacts.css* e fare clic su **Aggiungi**. Sostituire il contenuto di hello del file hello con hello seguente codice.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    Si utilizzerà questo foglio di stile per il layout di hello, colori e stili utilizzati nell'applicazione Gestione contatti hello.
6. Aprire hello *App_Start\BundleConfig.cs* file.
7. Aggiungere i seguenti hello tooregister codice hello [Knockout](http://knockoutjs.com/index.html "KO") plug-in.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    In questo esempio utilizzando knockout toosimplify dinamico il codice JavaScript che gestisce i modelli di schermata hello.
8. Modificare hello di hello contenuto/css voce tooregister *contacts.css* foglio di stile. Modificare hello seguente riga:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Con:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooinstall Knockout.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Aggiungere un controller per l'interfaccia Web API Restful hello
1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella Controllers, quindi scegliere **Aggiungi** e infine **Controller**. 
2. In hello **aggiungere lo scaffolding** finestra di dialogo immettere **Web 2 Controller API con azioni, mediante Entity Framework** e quindi fare clic su **Aggiungi**.
   
    ![Aggiunta di un controller per l'API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. In hello **Aggiungi Controller** finestra di dialogo immettere "ContactsController" come nome del controller. Selezionare "Contact (ContactManager.Models)" per hello **classe modello**.  Mantenere il valore predefinito hello per hello **classe contesto dati**. 
4. Fare clic su **Aggiungi**.

### <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
1. Premere CTRL + F5 toorun un'applicazione hello.
   
    ![Pagina di indice][intro001]
2. Immettere un contatto e fare clic su **Aggiungi**. app Hello restituisce toohello homepage e contatto hello immesso viene visualizzato.
   
    ![Pagina di indice con elementi dell'elenco azioni][addwebapi004]
3. In browser hello, aggiungere **/api/contatti** toohello URL.
   
    URL di Hello risultante sarà simile a http://localhost:1234/api/contatti. API è stato aggiunto a web RESTful Hello restituisce contatti hello archiviato. Firefox e Chrome verranno visualizzati i dati di hello in formato XML.
   
    ![Pagina di indice con elementi dell'elenco azioni][rxFFchrome]

    Internet Explorer verrà chiesto tooopen o salvare i contatti hello.

    ![Finestra di dialogo Salva dell'API Web][addwebapi006]


    È possibile aprire hello restituito contatti in blocco note o un browser.

    Questo output può essere utilizzato da altre applicazioni, ad esempio una pagina Web o un'applicazione per dispositivi mobili.

    ![Finestra di dialogo Salva dell'API Web][addwebapi007]

    **Avviso di sicurezza**: A questo punto, l'applicazione è attacco tooCSRF vulnerabile e non protetti. Più avanti nell'esercitazione di hello verrà rimossa questa vulnerabilità. Per altre informazioni, vedere l'articolo relativo alla [prevenzione delle richieste intersito false (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Aggiunta della protezione XSRF
Falsificazione della richiesta tra siti tra (noto anche come XSRF o CSRF) è un attacco contro applicazioni ospitate da web in base al quale un sito Web dannoso può influenzare l'interazione di hello tra un browser del client e un sito Web considerato attendibile da tale browser. Questi attacchi sono possibili perché browser invierà i token di autenticazione automaticamente con ogni sito Web tooa richiesta. esempio canonico Hello è un cookie di autenticazione, ad esempio, ASP. Ticket di autenticazione basata su form della rete. Tuttavia, i siti Web che usano un meccanismo di autenticazione persistente, ad esempio Autenticazione di Windows, autenticazione di base e così via, possono essere presi di mira da questi attacchi.

Un attacco XSRF è diverso da un attacco di phishing. Attacchi di phishing richiedono l'interazione da vittima hello. In un attacco di phishing, un sito Web dannoso imitino sito Web di destinazione hello e vittima hello è significativo a fornire l'autore dell'attacco toohello informazioni riservate. In un attacco XSRF, non vi è spesso alcuna interazione necessari da vittima hello. Piuttosto, autore dell'attacco hello si basa su browser hello automaticamente l'invio del sito Web di tutti i cookie rilevanti toohello destinazione.

Per ulteriori informazioni, vedere hello [Apri progetto di sicurezza dell'applicazione Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ContactManager**, scegliere **Aggiungi** e quindi fare clic su **Classe**.
2. File con nome hello *ValidateHttpAntiForgeryTokenAttribute.cs* e aggiungere hello seguente codice:
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Aggiungere il seguente hello *utilizzando* toohello istruzione contratti controller in modo che sia accesso toohello **[ValidateHttpAntiForgeryToken]** attributo.
   
        using ContactManager.Filters;
4. Aggiungere hello **[ValidateHttpAntiForgeryToken]** attributo metodi Post toohello di hello **ContactsController** tooprotect da minacce XSRF. Si aggiungerà toohello "PutContact", "PostContact" e **DeleteContact** metodi di azione.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Hello aggiornamento *script* sezione di hello *Views\Home\Index.cshtml* i token XSRF tooinclude codice tooget hello del file.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Pubblicare tooAzure di aggiornamento dell'applicazione hello e Database SQL
un'applicazione hello toopublish, ripetere procedura hello che è eseguita in precedenza.

1. In **Esplora**, fare clic con il pulsante destro progetto hello e selezionare **pubblica**.
   
    ![Pubblica][rxP]
2. Fare clic su hello **impostazioni** scheda.
3. In **ContactsManagerContext(ContactsManagerContext)**, fare clic su hello **v** icona toochange *stringa di connessione remota* toohello stringa di connessione per il contatto hello database. Fare clic su **ContactDB**.
   
    ![Impostazioni](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Casella hello per **eseguire migrazioni Code First (esecuzione all'avvio dell'applicazione)**.
5. Fare clic su **Avanti** e quindi su **Anteprima**. Visual Studio visualizza un elenco di file hello che verranno aggiunti o aggiornati.
6. Fare clic su **Pubblica**.
   Al termine della distribuzione di hello, browser hello apre toohello home page dell'applicazione hello.
   
    ![Pagina di indice senza contatti][intro001]
   
    Visual Studio Hello pubblicare stringa di connessione hello processo configurato automaticamente in hello distribuito *Web. config* database SQL toohello toopoint del file. È anche possibile configurarlo migrazioni Code First tooautomatically hello aggiornamento database toohello versione più recente hello prima hello applicazione accede a database hello dopo la distribuzione.
   
    In seguito a questa configurazione, il primo codice creato hello database eseguendo il codice hello in hello **iniziale** classe creata in precedenza. Era hello prima ora hello tentato tooaccess hello database dell'applicazione dopo la distribuzione.
7. Quando è stato eseguito localmente, app hello tooverify che ha avuto esito positivo di distribuzione del database, immettere un contatto.

Quando viene visualizzata tale elemento hello che immesso viene salvato e visualizzato nella pagina di gestione contatto hello, si sa che è stato archiviato nel database di hello.

![Pagina di indice con contatti][addwebapi004]

un'applicazione Hello è in esecuzione nel cloud hello, utilizzando il Database SQL toostore i dati. Dopo aver completato il test di un'applicazione hello in Azure, è necessario eliminarla. un'applicazione Hello è pubblica e non dispone dell'accesso toolimit un meccanismo.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Un altro modo toostore dati in un'applicazione Azure sono toouse archiviazione di Azure, che forniscono l'archiviazione dei dati non relazionali in formato hello di BLOB e tabelle. Hello seguenti collegamenti fornisce informazioni su API Web, ASP.NET MVC e Azure.

* [Introduzione a Entity Framework con MVC][EFCodeFirstMVCTutorial]
* [Introduzione tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Creare la prima API Web ASP.NET](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Debug di WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Questa applicazione di esempio di esercitazione e hello è stato scritto dal [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) con l'assistenza da Tom Dykstra e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Lasciare commenti e suggerimenti su cosa piace o ciò che si vuole toosee migliorata, non solo informazioni sull'esercitazione hello stesso, ma anche sui prodotti hello che viene illustrato come. I commenti e suggerimenti saranno utili per definire la priorità dei miglioramenti da apportare. Siamo interessati soprattutto individuare il quanta interesse esiste in più di automazione per il processo di hello di configurazione e distribuzione di database delle appartenenze hello. 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

