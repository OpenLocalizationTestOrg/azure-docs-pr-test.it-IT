---
title: aaaAzure AD v2 Windows Desktop Getting Started - il programma di installazione | Documenti Microsoft
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
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurare il progetto

In questa sezione vengono fornite istruzioni dettagliate su come toocreate un nuovo toodemonstrate progetto come toointegrate un Desktop Windows .NET applicazione (XAML) con *Accedi con Microsoft* in modo per eseguire una query API Web che richiede un token.

un'applicazione Hello creata in questa guida espone un pulsante toograph e Mostra i risultati sullo schermo e un pulsante di disconnessione.

> Se si preferisce toodownload il progetto di Visual Studio di questo esempio invece, [Scaricare un progetto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.


### <a name="create-your-application"></a>Creare l'applicazione
1. In Visual Studio: `File` > `New` > `Project`<br/>
2. In *Modelli* selezionare `Visual C#`
3. Selezionare `WPF App` (o *applicazione WPF* a seconda della versione di hello di Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Aggiungere hello libreria di autenticazione di Microsoft (MSAL) tooyour progetto
1. In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copiare e incollare il seguente hello nella finestra della Console di gestione pacchetti hello:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> pacchetto Hello installa hello libreria di autenticazione di Microsoft (MSAL). MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente toskens utilizzato tooaccess API protette da Azure Active Directory v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Aggiungere codice di hello tooinitialize MSAL
Questo passaggio consente di creare un'interazione toohandle classe alla libreria MSAL, come la gestione dei token.

1. Aprire hello `App.xaml.cs` file e aggiungere il riferimento di hello per la classe di toohello MSAL libreria:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Aggiornare i seguenti toohello di hello App classe:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Creare l'interfaccia utente dell'applicazione
sezione Hello riportata di seguito viene illustrato come un'applicazione può richiedere un server protetto di back-end come Microsoft Graph. Nell'ambito del modello di progetto viene automaticamente creato un file MainWindow.xaml. Aprire il file di questo file e quindi seguire le istruzioni di hello seguenti:

Sostituire l'applicazione `<Grid>` essere seguente hello:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
