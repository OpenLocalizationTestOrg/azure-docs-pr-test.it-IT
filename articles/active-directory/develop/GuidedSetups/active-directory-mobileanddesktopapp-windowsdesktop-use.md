---
title: aaaAzure AD v2 Windows Desktop Getting Started - utilizzo | Documenti Microsoft
description: Come applicazioni .NET per Windows Desktop (XAML) possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="a376d-103">Utilizzare hello libreria di autenticazione di Microsoft (MSAL) tooget un token per hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="a376d-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="a376d-104">In questa sezione viene illustrato come toouse MSAL tooget un token hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="a376d-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="a376d-105">In `MainWindow.xaml.cs`, aggiungere il riferimento hello per la classe di toohello MSAL libreria:</span><span class="sxs-lookup"><span data-stu-id="a376d-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="a376d-106">Sostituire il codice della classe <code>MainWindow</code> con:</span><span class="sxs-lookup"><span data-stu-id="a376d-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="a376d-107">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a376d-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="a376d-108">Acquisizione di un token utente in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="a376d-108">Getting a user token interactive</span></span>
<span data-ttu-id="a376d-109">Chiamare il metodo hello `AcquireTokenAsync` risultati del metodo in una richiesta di conferma finestra hello toosign utente in.</span><span class="sxs-lookup"><span data-stu-id="a376d-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="a376d-110">Le applicazioni in genere richiedono toosign un utente in modo interattivo hello devono tooaccess prima volta che una risorsa protetta o quando una tooacquire operazione invisibile all'utente un token ha esito negativo (ad esempio, la password dell'utente hello scaduto).</span><span class="sxs-lookup"><span data-stu-id="a376d-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="a376d-111">Acquisizione di un token utente in modo invisibile</span><span class="sxs-lookup"><span data-stu-id="a376d-111">Getting a user token silently</span></span>
<span data-ttu-id="a376d-112">`AcquireTokenSilentAsync` gestisce le acquisizioni e i rinnovi dei token senza alcuna interazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a376d-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="a376d-113">Dopo aver `AcquireTokenAsync` per hello prima esecuzione, `AcquireTokenSilentAsync` è hello metodo abituale utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a376d-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="a376d-114">Infine, `AcquireTokenSilentAsync` avrà esito negativo, ad esempio hello utente è disconnesso o è stato modificato la password in un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a376d-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="a376d-115">Quando MSAL rileva hello problema può essere risolto tramite la richiesta un'azione interattiva, viene generato un `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="a376d-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="a376d-116">L'applicazione può gestire questa eccezione in due modi:</span><span class="sxs-lookup"><span data-stu-id="a376d-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="a376d-117">Effettuare una chiamata su `AcquireTokenAsync` immediatamente, dando luogo a chiedere all'utente di hello toosign-in.</span><span class="sxs-lookup"><span data-stu-id="a376d-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="a376d-118">Questo modello è in genere utilizzato nelle applicazioni in linea in cui è presente alcun contenuto offline in un'applicazione hello disponibile per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a376d-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="a376d-119">Hello esempio generato da questa installazione interattiva, si utilizza questo modello: è possibile visualizzarlo in hello azione prima volta che si esegue l'esempio hello: perché nessun utente è già utilizzata un'applicazione hello, `PublicClientApp.Users.FirstOrDefault()` conterrà un valore null e un `MsalUiRequiredException` verrà generata l'eccezione.</span><span class="sxs-lookup"><span data-stu-id="a376d-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="a376d-120">Hello del codice nell'esempio hello quindi handle hello eccezione chiamando `AcquireTokenAsync` risultante in chiedere all'utente di hello toosign-in.</span><span class="sxs-lookup"><span data-stu-id="a376d-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="a376d-121">Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `AcquireTokenSilentAsync` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a376d-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="a376d-122">Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non in linea contenuto disponibile in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a376d-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="a376d-123">In questo caso, è possibile decidere utente hello quando desiderano toosign nella risorsa protetta hello tooaccess toorefresh hello informazioni non aggiornate o l'applicazione può decidere tooretry `AcquireTokenSilentAsync` quando rete viene ripristinata dopo essere stato temporaneamente non disponibile.</span><span class="sxs-lookup"><span data-stu-id="a376d-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="a376d-124">Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta</span><span class="sxs-lookup"><span data-stu-id="a376d-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="a376d-125">Aggiungere nuovo metodo di hello sotto tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="a376d-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="a376d-126">metodo Hello è toomake usato un `GET` richiesta sull'API Graph con un'intestazione di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="a376d-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="a376d-127">Altre informazioni sull'esecuzione di una chiamata REST a un'API protetta</span><span class="sxs-lookup"><span data-stu-id="a376d-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="a376d-128">In questa applicazione di esempio hello `GetHttpContentWithToken` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito.</span><span class="sxs-lookup"><span data-stu-id="a376d-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="a376d-129">Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*.</span><span class="sxs-lookup"><span data-stu-id="a376d-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="a376d-130">Per questo esempio, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a376d-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="a376d-131">Aggiungere un metodo toosign utente hello</span><span class="sxs-lookup"><span data-stu-id="a376d-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="a376d-132">Aggiungere hello seguente metodo tooyour `MainWindow.xaml.cs` toosign utente hello:</span><span class="sxs-lookup"><span data-stu-id="a376d-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="a376d-133">Altre informazioni sulla disconnessione</span><span class="sxs-lookup"><span data-stu-id="a376d-133">More info on Sign-Out</span></span>

<span data-ttu-id="a376d-134">`SignOutButton_Click`Rimuove hello utente dalla cache utente MSAL: in questo modo efficace utente corrente di MSAL tooforget hello in modo tooacquire una richiesta futura un token riuscirà solo se viene resa toobe interattiva.</span><span class="sxs-lookup"><span data-stu-id="a376d-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="a376d-135">Anche se un'applicazione hello in questo esempio supporta un singolo utente, MSAL supporta scenari in cui più account può essere firmato nella hello contemporaneamente – un esempio è di un'applicazione di posta elettronica in cui un utente dispone di più account.</span><span class="sxs-lookup"><span data-stu-id="a376d-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="a376d-136">Visualizzare informazioni di base sul token</span><span class="sxs-lookup"><span data-stu-id="a376d-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="a376d-137">Aggiungere hello seguente metodo tootooyour `MainWindow.xaml.cs` toodisplay informazioni di base token hello:</span><span class="sxs-lookup"><span data-stu-id="a376d-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="a376d-138">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a376d-138">More Information</span></span>

<span data-ttu-id="a376d-139">Token acquisito tramite *OpenID Connect* contenere anche un piccolo subset delle informazioni pertinenti toohello utente.</span><span class="sxs-lookup"><span data-stu-id="a376d-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="a376d-140">`DisplayBasicTokenInfo`Visualizza le informazioni di base contenute nel token hello: ad esempio, dell'utente hello visualizzare nome e ID, nonché hello stringa di data e hello di scadenza del token che rappresentano i token di accesso hello stesso.</span><span class="sxs-lookup"><span data-stu-id="a376d-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="a376d-141">Queste informazioni vengono visualizzate per si toosee.</span><span class="sxs-lookup"><span data-stu-id="a376d-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="a376d-142">È possibile raggiungere hello *chiamare API di Microsoft Graph* pulsante più volte e visualizzare tale hello stesso token è stato riutilizzato per le richieste successive.</span><span class="sxs-lookup"><span data-stu-id="a376d-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="a376d-143">È inoltre possibile visualizzare la data di scadenza hello estesa quando si decide di MSAL che è ora toorenew hello token.</span><span class="sxs-lookup"><span data-stu-id="a376d-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

