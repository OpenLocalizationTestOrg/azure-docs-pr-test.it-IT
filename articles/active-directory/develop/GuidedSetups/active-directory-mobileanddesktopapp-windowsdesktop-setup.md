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
## <a name="set-up-your-project"></a><span data-ttu-id="8c012-103">Configurare il progetto</span><span class="sxs-lookup"><span data-stu-id="8c012-103">Set up your project</span></span>

<span data-ttu-id="8c012-104">In questa sezione vengono fornite istruzioni dettagliate su come toocreate un nuovo toodemonstrate progetto come toointegrate un Desktop Windows .NET applicazione (XAML) con *Accedi con Microsoft* in modo per eseguire una query API Web che richiede un token.</span><span class="sxs-lookup"><span data-stu-id="8c012-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="8c012-105">un'applicazione Hello creata in questa guida espone un pulsante toograph e Mostra i risultati sullo schermo e un pulsante di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="8c012-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="8c012-106">Se si preferisce toodownload il progetto di Visual Studio di questo esempio invece,</span><span class="sxs-lookup"><span data-stu-id="8c012-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="8c012-107">[Scaricare un progetto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8c012-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="8c012-108">Creare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c012-108">Create your application</span></span>
1. <span data-ttu-id="8c012-109">In Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="8c012-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="8c012-110">In *Modelli* selezionare `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="8c012-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="8c012-111">Selezionare `WPF App` (o *applicazione WPF* a seconda della versione di hello di Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8c012-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="8c012-112">Aggiungere hello libreria di autenticazione di Microsoft (MSAL) tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="8c012-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="8c012-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="8c012-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="8c012-114">Copiare e incollare il seguente hello nella finestra della Console di gestione pacchetti hello:</span><span class="sxs-lookup"><span data-stu-id="8c012-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="8c012-115">pacchetto Hello installa hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="8c012-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="8c012-116">MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente toskens utilizzato tooaccess API protette da Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="8c012-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="8c012-117">Aggiungere codice di hello tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="8c012-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="8c012-118">Questo passaggio consente di creare un'interazione toohandle classe alla libreria MSAL, come la gestione dei token.</span><span class="sxs-lookup"><span data-stu-id="8c012-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="8c012-119">Aprire hello `App.xaml.cs` file e aggiungere il riferimento di hello per la classe di toohello MSAL libreria:</span><span class="sxs-lookup"><span data-stu-id="8c012-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="8c012-120">Aggiornare i seguenti toohello di hello App classe:</span><span class="sxs-lookup"><span data-stu-id="8c012-120">Update hello App class toohello following:</span></span>
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

## <a name="create-your-applications-ui"></a><span data-ttu-id="8c012-121">Creare l'interfaccia utente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c012-121">Create your application’s UI</span></span>
<span data-ttu-id="8c012-122">sezione Hello riportata di seguito viene illustrato come un'applicazione può richiedere un server protetto di back-end come Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="8c012-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="8c012-123">Nell'ambito del modello di progetto viene automaticamente creato un file MainWindow.xaml.</span><span class="sxs-lookup"><span data-stu-id="8c012-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="8c012-124">Aprire il file di questo file e quindi seguire le istruzioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c012-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="8c012-125">Sostituire l'applicazione `<Grid>` essere seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8c012-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
