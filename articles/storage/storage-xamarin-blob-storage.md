---
title: Come usare l'archiviazione BLOB da Xamarin | Microsoft Docs
description: La libreria client di Archiviazione di Azure per Xamarin consente agli sviluppatori di creare app per Windows Store, iOS e Android con le proprie interfacce utente native. Questa esercitazione illustra come usare Xamarin per creare un'applicazione che usa l'archiviazione BLOB di Azure.
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0952c0e7189dd360098744a7e19b04cd330cb617
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="e17e3-104">Come usare l'archiviazione BLOB da Xamarin</span><span class="sxs-lookup"><span data-stu-id="e17e3-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="e17e3-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e17e3-105">Overview</span></span>
<span data-ttu-id="e17e3-106">Xamarin consente agli sviluppatori di utilizzare una base di codici C# condivisa per creare applicazioni per Windows Store, iOS e Android con le proprie interfacce utente native.</span><span class="sxs-lookup"><span data-stu-id="e17e3-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="e17e3-107">Questa esercitazione illustra come usare l'archiviazione BLOB di Azure con un'applicazione per Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e17e3-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="e17e3-108">Per maggiori informazioni su Archiviazione di Azure, prima di approfondire il codice, vedere [Introduzione ad Archiviazione di Microsoft Azure](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e17e3-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="e17e3-109">Creare una nuova applicazione Xamarin</span><span class="sxs-lookup"><span data-stu-id="e17e3-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="e17e3-110">Per questa esercitazione verrà generata un'applicazione destinata ad Android, iOS e Windows.</span><span class="sxs-lookup"><span data-stu-id="e17e3-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="e17e3-111">Questa applicazione creerà semplicemente un contenitore nel quale caricherà un BLOB.</span><span class="sxs-lookup"><span data-stu-id="e17e3-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="e17e3-112">Verrà usato Visual Studio in Windows, ma le stesse istruzioni possono essere applicate per la creazione di un'applicazione con Xamarin Studio su macOS.</span><span class="sxs-lookup"><span data-stu-id="e17e3-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="e17e3-113">Attenersi alla procedura seguente per creare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="e17e3-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="e17e3-114">Se necessario, scaricare e installare [Xamarin per Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="e17e3-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="e17e3-115">Aprire Visual Studio e creare un'applicazione vuota (nativa portatile): **File > Nuovo > Progetto > Multipiattaforma > Applicazione vuota (nativa portatile)**.</span><span class="sxs-lookup"><span data-stu-id="e17e3-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="e17e3-116">Nel riquadro Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="e17e3-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="e17e3-117">Cercare **WindowsAzure.Storage** e installare la versione stabile più recente su tutti i progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="e17e3-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="e17e3-118">Compilare ed eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="e17e3-118">Build and run your project.</span></span>

<span data-ttu-id="e17e3-119">A questo punto si disporrà di un'applicazione che consente di fare clic su un pulsante e incrementare un contatore.</span><span class="sxs-lookup"><span data-stu-id="e17e3-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="e17e3-120">Creare un contenitore e caricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="e17e3-120">Create container and upload blob</span></span>
<span data-ttu-id="e17e3-121">Quindi, sotto il progetto `(Portable)`, si aggiungerà codice a `MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="e17e3-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="e17e3-122">Questo codice crea un contenitore e carica in esso un oggetto BLOB.</span><span class="sxs-lookup"><span data-stu-id="e17e3-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="e17e3-123">`MyClass.cs` deve apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="e17e3-123">`MyClass.cs` should look like the following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="e17e3-124">Assicurarsi di sostituire "your_account_name_here" e "your_account_key_here" con il nome e la chiave dell'account effettivi.</span><span class="sxs-lookup"><span data-stu-id="e17e3-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="e17e3-125">Tutti i progetti iOS, Android e Windows Phone contengono riferimenti al progetto portatile, vale a dire che è possibile scrivere tutto il codice condiviso in una posizione e utilizzarlo in tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="e17e3-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="e17e3-126">È ora possibile aggiungere la seguente riga di codice in ogni progetto per iniziare a sfruttare i vantaggi: `MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="e17e3-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="e17e3-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="e17e3-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="e17e3-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="e17e3-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading the view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="e17e3-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="e17e3-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-the-application"></a><span data-ttu-id="e17e3-130">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="e17e3-130">Run the application</span></span>
<span data-ttu-id="e17e3-131">È ora possibile eseguire questa applicazione in un emulatore Android o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e17e3-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="e17e3-132">È inoltre possibile eseguire questa applicazione in un emulatore iOS, ma questo richiederà un Mac.</span><span class="sxs-lookup"><span data-stu-id="e17e3-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="e17e3-133">Per istruzioni specifiche su come eseguire questa operazione, leggere la documentazione relativa alla [connessione di Visual Studio a un Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="e17e3-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="e17e3-134">Dopo aver eseguito l'applicazione, verrà creato il contenitore `mycontainer` nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e17e3-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="e17e3-135">Questo deve contenere il BLOB, `myblob`, che include il testo, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="e17e3-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="e17e3-136">È possibile verificarlo tramite [Esplora archivi di Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e17e3-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e17e3-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e17e3-137">Next steps</span></span>
<span data-ttu-id="e17e3-138">In questa esercitazione è stato illustrato come creare un'applicazione multipiattaforma in Xamarin che usa Archiviazione di Azure, con particolare attenzione a uno scenario di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="e17e3-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="e17e3-139">È tuttavia possibile svolgere molte altre operazioni, non solo con l'archiviazione BLOB, ma anche con archiviazione tabelle, archiviazione file e archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="e17e3-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="e17e3-140">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e17e3-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="e17e3-141">Introduzione all'archiviazione BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="e17e3-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e17e3-142">Introduzione all'archiviazione tabelle di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="e17e3-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="e17e3-143">Introduzione all'archiviazione code di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="e17e3-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="e17e3-144">Introduzione ad Archiviazione file di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="e17e3-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

