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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilizzare hello libreria di autenticazione di Microsoft (MSAL) tooget un token per hello Microsoft Graph API

In questa sezione viene illustrato come toouse MSAL tooget un token hello Microsoft Graph API.

1.  In `MainWindow.xaml.cs`, aggiungere il riferimento hello per la classe di toohello MSAL libreria:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Sostituire il codice della classe <code>MainWindow</code> con:
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
### <a name="more-information"></a>Altre informazioni
#### <a name="getting-a-user-token-interactive"></a>Acquisizione di un token utente in modo interattivo
Chiamare il metodo hello `AcquireTokenAsync` risultati del metodo in una richiesta di conferma finestra hello toosign utente in. Le applicazioni in genere richiedono toosign un utente in modo interattivo hello devono tooaccess prima volta che una risorsa protetta o quando una tooacquire operazione invisibile all'utente un token ha esito negativo (ad esempio, la password dell'utente hello scaduto).

#### <a name="getting-a-user-token-silently"></a>Acquisizione di un token utente in modo invisibile
`AcquireTokenSilentAsync` gestisce le acquisizioni e i rinnovi dei token senza alcuna interazione da parte dell'utente. Dopo aver `AcquireTokenAsync` per hello prima esecuzione, `AcquireTokenSilentAsync` è hello metodo abituale utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.
Infine, `AcquireTokenSilentAsync` avrà esito negativo, ad esempio hello utente è disconnesso o è stato modificato la password in un altro dispositivo. Quando MSAL rileva hello problema può essere risolto tramite la richiesta un'azione interattiva, viene generato un `MsalUiRequiredException`. L'applicazione può gestire questa eccezione in due modi:

1.  Effettuare una chiamata su `AcquireTokenAsync` immediatamente, dando luogo a chiedere all'utente di hello toosign-in. Questo modello è in genere utilizzato nelle applicazioni in linea in cui è presente alcun contenuto offline in un'applicazione hello disponibile per l'utente hello. Hello esempio generato da questa installazione interattiva, si utilizza questo modello: è possibile visualizzarlo in hello azione prima volta che si esegue l'esempio hello: perché nessun utente è già utilizzata un'applicazione hello, `PublicClientApp.Users.FirstOrDefault()` conterrà un valore null e un `MsalUiRequiredException` verrà generata l'eccezione. Hello del codice nell'esempio hello quindi handle hello eccezione chiamando `AcquireTokenAsync` risultante in chiedere all'utente di hello toosign-in.

2.  Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `AcquireTokenSilentAsync` in un secondo momento. Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non in linea contenuto disponibile in un'applicazione hello. In questo caso, è possibile decidere utente hello quando desiderano toosign nella risorsa protetta hello tooaccess toorefresh hello informazioni non aggiornate o l'applicazione può decidere tooretry `AcquireTokenSilentAsync` quando rete viene ripristinata dopo essere stato temporaneamente non disponibile.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta

1. Aggiungere nuovo metodo di hello sotto tooyour `MainWindow.xaml.cs`. metodo Hello è toomake usato un `GET` richiesta sull'API Graph con un'intestazione di autorizzazione:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Altre informazioni sull'esecuzione di una chiamata REST a un'API protetta

In questa applicazione di esempio hello `GetHttpContentWithToken` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito. Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*. Per questo esempio, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Aggiungere un metodo toosign utente hello

1. Aggiungere hello seguente metodo tooyour `MainWindow.xaml.cs` toosign utente hello:

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
### <a name="more-info-on-sign-out"></a>Altre informazioni sulla disconnessione

`SignOutButton_Click`Rimuove hello utente dalla cache utente MSAL: in questo modo efficace utente corrente di MSAL tooforget hello in modo tooacquire una richiesta futura un token riuscirà solo se viene resa toobe interattiva.
Anche se un'applicazione hello in questo esempio supporta un singolo utente, MSAL supporta scenari in cui più account può essere firmato nella hello contemporaneamente – un esempio è di un'applicazione di posta elettronica in cui un utente dispone di più account.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Visualizzare informazioni di base sul token

1. Aggiungere hello seguente metodo tootooyour `MainWindow.xaml.cs` toodisplay informazioni di base token hello:

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
### <a name="more-information"></a>Altre informazioni

Token acquisito tramite *OpenID Connect* contenere anche un piccolo subset delle informazioni pertinenti toohello utente. `DisplayBasicTokenInfo`Visualizza le informazioni di base contenute nel token hello: ad esempio, dell'utente hello visualizzare nome e ID, nonché hello stringa di data e hello di scadenza del token che rappresentano i token di accesso hello stesso. Queste informazioni vengono visualizzate per si toosee. È possibile raggiungere hello *chiamare API di Microsoft Graph* pulsante più volte e visualizzare tale hello stesso token è stato riutilizzato per le richieste successive. È inoltre possibile visualizzare la data di scadenza hello estesa quando si decide di MSAL che è ora toorenew hello token.
<!--end-collapse-->

