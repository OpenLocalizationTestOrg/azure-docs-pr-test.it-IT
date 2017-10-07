---
title: un'app di Azure line-of-business con l'autenticazione di Azure Active Directory aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un ASP.NET MVC line-of-business app in Azure App Service che esegue l'autenticazione con Azure Active Directory
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory
In questo articolo illustra come app toocreate un .NET line-of-business in [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) utilizzando hello [autenticazione / autorizzazione](../app-service/app-service-authentication-overview.md) funzionalità. Viene inoltre illustrato come hello toouse [API di Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dati della directory in un'applicazione hello.

tenant di Azure Active Directory Hello in uso può essere una directory di Azure-only. In alternativa, può essere [sincronizzati con Active Directory locale](../active-directory/active-directory-aadconnect.md) toocreate un'esperienza single sign-on per i processi di lavoro locali e remoti. In questo articolo Usa directory predefinita hello per l'account di Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Obiettivo di compilazione
Si creerà una semplice applicazione di line-of-business Create-lettura, aggiornamento ed eliminazione (CRUD) nelle App Web di servizio App che tiene traccia elementi di lavoro con hello seguenti caratteristiche:

* Autenticazione degli utenti con Azure Active Directory
* Esecuzione di query su utenti e gruppi della directory tramite l' [API Graph di Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Utilizzare hello ASP.NET MVC *Nessuna autenticazione* modello

Se è necessario il Controllo degli accessi in base al ruolo per l'applicazione line-of-business in Azure, vedere il [passaggio successivo](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Elementi necessari
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

È necessario hello seguenti toocomplete questa esercitazione:

* Un tenant di Azure Active Directory con utenti in diversi gruppi
* Autorizzazioni toocreate applicazioni nel tenant di Azure Active Directory hello
* Visual Studio 2013 Update 4 o versione successiva
* [Azure SDK 2.8.1 o versione successiva](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Creare e distribuire un tooAzure app web
1. In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.
2. Selezionare **Applicazione Web ASP.NET**, assegnare un nome al progetto e fare clic su **OK**.
3. Seleziona hello **MVC** modello, quindi modificare anche l'autenticazione di hello**Nessuna autenticazione**. Assicurarsi che **Host nel Cloud hello** è selezionata e fare clic su **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. In hello **Crea servizio App** finestra di dialogo, fare clic su **aggiungere un account** (e quindi **aggiungere un account** nell'elenco a discesa hello) toolog in tooyour account Azure.
5. Dopo aver eseguito l'accesso, configurare l'app Web. Creare un gruppo di risorse e un nuovo piano di servizio App facendo clic sul rispettivo hello **New** pulsante. Fare clic su **esplorare servizi di Azure aggiuntivi** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. In hello **servizi** scheda, fare clic su  **+**  tooadd un Database SQL per l'app. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. In **configurare il Database SQL**, fare clic su **New** toocreate un'istanza di SQL Server.
8. In **Configura SQL Server**configurare l'istanza di SQL Server. Quindi, fare clic su **OK**, **OK**, e **crea** tookick off della creazione dell'app hello in Azure.
9. In **attività di servizio App di Azure**, è possibile visualizzare al termine della creazione dell'app hello. Fare clic su  **pubblica &lt;* appname*> toothis App Web adesso * *, quindi fare clic su **pubblica**. 
   
    Al termine del processo di Visual Studio, viene aperto hello pubblicare app nel browser hello. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Configurare l'autenticazione e l'accesso alla directory
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra hello **servizi App** > **&lt;*appname*> * * > **autenticazione / autorizzazione**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Attivare l'autenticazione di Azure Active Directory facendo clic su **Attivato** > **Azure Active Directory** > **Rapida** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Fare clic su **salvare** nella barra dei comandi di hello.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Una volta che le impostazioni di autenticazione hello vengono salvate correttamente, tenta di spostarsi app tooyour nuovamente nel browser hello. Le impostazioni predefinite imporre l'autenticazione al hello intera app. Se non già effettuato l'accesso, verrà reindirizzato tooa schermata di accesso. Dopo aver effettuato l'accesso, verrà visualizzata l'app protetta tramite HTTPS. Successivamente, è necessario accedere a tooenable toodirectory dati. 
5. Passare toohello [portale classico](https://manage.windowsazure.com).
6. Scegliere dal menu a sinistra hello **Active Directory** > **Directory predefinita** > **applicazioni**  >   **&lt;* appname*> * *.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Si tratta di un'applicazione hello Azure Active Directory creati per si tooenable hello autorizzazione servizio App o funzionalità di autenticazione.
7. Fare clic su **utenti** e **gruppi** toomake certi di disporre di alcuni utenti e gruppi nella directory hello. In caso contrario, creare alcuni utenti e gruppi di test.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Fare clic su **configura** tooconfigure questa applicazione.
9. Scorrere verso il basso toohello **chiavi** sezione e aggiungere una chiave, selezionare una durata. Fare quindi clic su **Autorizzazioni delegate** e selezionare **Leggi i dati della directory**. 
   Fare clic su **Salva**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Una volta che le impostazioni vengono salvate, scorre all'indietro toohello **chiavi** sezione e fare clic su hello **copia** chiave del pulsante toocopy hello client. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Se si abbandona questa pagina a questo punto, non sarà in grado di tooaccess chiave mai più di questo client.
    > 
    > 
11. Successivamente, è necessario tooconfigure app web con questa chiave. Accedi toohello [Esplora inventario risorse di Azure](https://resources.azure.com) con l'account di Azure.
12. Nella parte superiore di hello della pagina hello, fare clic su **lettura/scrittura** modifiche toomake hello Esplora inventario risorse di Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Trovare le impostazioni di autenticazione per l'app, si trova in sottoscrizioni di hello >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **provider** > **Microsoft**  >  **siti** > **&lt;*appname*> * * > **config**  >  **authsettings**.
14. Fare clic su **Modifica**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Nel riquadro di modifica di hello, impostare hello `clientSecret` e `additionalLoginParams` proprietà come indicato di seguito.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Fare clic su **inserire** in hello toosubmit superiore le modifiche.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. A questo punto, tootest se si dispone dell'autorizzazione di hello token tooaccess hello API di Graph di Azure Active Directory, semplicemente passare a  **https://&lt;*appname*>.azurewebsites.net/.auth/me** nel Browser. Se è stato configurato tutto correttamente, si noterà hello `access_token` proprietà hello risposta JSON.
    
    Hello `~/.auth/me` percorso dell'URL è gestito dall'autenticazione del servizio App / toogive di autorizzazione per tutte le informazioni di hello correlati sessione tooyour autenticato. Per altre informazioni, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Hello `access_token` ha un periodo di scadenza. L'autenticazione/autorizzazione del servizio app offre tuttavia funzionalità di aggiornamento del token con `~/.auth/refresh`. Per ulteriori informazioni su come toouse, vedere [archivio dei Token di servizio App](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Ora si eseguirà un'operazione utile con i dati della directory.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Aggiungere app tooyour funzionalità line-of-business
Verrà creato un semplice progetto di gestione degli elementi di lavoro CRUD.  

1. Nella cartella ~\Models hello, creare un file di classe denominato WorkItem.cs e sostituire `public class WorkItem {...}` con hello seguente codice:
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Creare hello progetto toomake una nuova logica di scaffolding toohello accessibile di modello in Visual Studio.
3. Aggiungere un nuovo elemento di scaffolding `WorkItemsController` toohello ~\Controllers cartella (fare doppio clic su **controller**, punto troppo**Aggiungi**e selezionare **nuovo elemento di scaffolding**). 
4. Selezionare **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**.
5. Modello selezionare hello creato, quindi fare clic su  **+**  e quindi **Aggiungi** tooadd un contesto dei dati, quindi fare clic su **Aggiungi**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. In ~\Views\WorkItems\Create.cshtml (un elemento di scaffolding automaticamente), trovare hello `Html.BeginForm` metodo di supporto e hello modifiche evidenziate di seguito:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Si noti che `token` e `tenant` vengono utilizzati da hello `AadPicker` toomake oggetto chiamate API di Graph di Azure Active Directory. Si aggiungerà `AadPicker` in un secondo momento.     
   
   > [!NOTE]
   > È anche possibile ottenere `token` e `tenant` dal lato client hello con `~/.auth/me`, ma che potrebbe essere una chiamata di server aggiuntive. ad esempio:
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. Modificare hello stesso con ~ \Views\WorkItems\Edit.cshtml.
8. Hello `AadPicker` oggetto è definito in uno script che è necessario tooadd tooyour progetto. Fare clic sulla cartella ~\Scripts hello, scegliere troppo**Aggiungi**, fare clic su **file JavaScript**. Tipo `AadPickerLibrary` filename hello e fare clic su **OK**.
9. Copiare il contenuto di hello da [qui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.
   
   Nello script hello, hello `AadPicker` object chiama [API di Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch per utenti e gruppi corrispondenti hello input.  
10. ~\Scripts\AadPickerLibrary.js utilizza inoltre hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/). Pertanto, è necessario tooadd jQuery dell'interfaccia utente tooyour project. Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.
11. In Gestione pacchetti NuGet hello, fare clic su Sfoglia, tipo **jquery ui** in hello barra di ricerca, quindi fare clic su **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Nel riquadro di destra hello, fare clic su **installare**, quindi fare clic su **OK** tooproceed.
13. Aprire ~\App_Start\BundleConfig.cs e apportare hello modifiche evidenziate di seguito:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Sono presenti più efficiente modi toomanage JavaScript e il file CSS nell'app. Tuttavia, per motivi di semplicità si deve toopiggyback in bundle hello che vengono caricati con ogni visualizzazione.
14. Infine, in ~ \Global.asax, aggiungere hello successiva riga di codice in hello `Application_Start()` metodo. `Ctrl`+`.`su ogni errore di risoluzione dei nomi troppo risolvere questo problema.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > È necessario questa riga di codice perché il modello MVC predefinito hello utilizza <code>[ValidateAntiForgeryToken]</code> effetti su alcune delle azioni hello. A causa di toohello comportamento descritto dalla [Brock Allen](https://twitter.com/BrockLAllen) in [MVC 4, AntiForgeryToken e attestazioni](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) POST HTTP potrebbe non riuscire convalida token antifalsificazione perché:
    > 
    > * Azure Active Directory non invia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, è richiesto per impostazione predefinita dal token antifalsificazione hello.
    > * Se Azure Active Directory è una directory è stata sincronizzata con AD FS, trust hello ADFS per impostazione predefinita non inviare hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider attestazione, sebbene sia possibile configurare manualmente ADFS toosend questa attestazione.
    > 
    > `ClaimTypes.NameIdentifies`Specifica l'attestazione hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, che fornisce funzionalità di Azure Active Directory.  
    > 
    > 
15. A questo punto, pubblicare le modifiche. Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.
16. Fare clic su **impostazioni**, assicurarsi che vi sia un tooyour di stringa di connessione del Database SQL, selezionare **aggiornamento Database** toomake hello modifiche dello schema per il modello e fare clic su **pubblica** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. In browser hello passare toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e fare clic su **Crea nuovo**.
18. Fare clic nella hello **AssignedToName** casella. Gli utenti e i gruppi del tenant di Azure Active Directory verranno visualizzati in un elenco a discesa. È possibile digitare toofilter o utilizzare hello `Up` o `Down` oppure fare clic tooselect hello utente o gruppo. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Fare clic su **crea** modifiche hello toosave. Quindi, fare clic su **modifica** lavoro hello creato elemento tooobserve hello stesso comportamento.

A questo punto è in esecuzione un'app line-of-business in Azure con accesso alla directory. È molto più che è possibile eseguire con hello API Graph. Vedere [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Informazioni di riferimento sull'API Graph di Azure AD).

<a name="next"></a>

## <a name="next-step"></a>Passaggio successivo
Se è necessario il controllo di accesso basato sui ruoli (RBAC) per l'app line-of-business in azure, vedere [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) per un esempio del team di Azure Active Directory hello. Viene illustrato come tooenable ruoli per l'applicazione in Azure Active Directory e quindi autorizzare gli utenti con hello `[Authorize]` effetto.

Se l'app line-of-business deve accedere a dati locali tooon, vedere [accesso risorse locali mediante connessioni ibride in Azure App Service](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Altre risorse
* [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md)
* [Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure](web-sites-authentication-authorization.md)
* [Creare un'app line-of-business in Azure con l'autenticazione di AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Autenticazione del servizio App e hello API Azure AD Graph](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Esempi e documentazione su Microsoft Azure Active Directory](https://github.com/AzureADSamples)
* [Token e tipi di attestazioni supportati di Azure Active Directory](http://msdn.microsoft.com/library/azure/dn195587.aspx)
