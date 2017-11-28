---
title: aaaHow toouse archiviazione Blob da Xamarin | Documenti Microsoft
description: Libreria Client di archiviazione di Azure per Xamarin Hello consente agli sviluppatori toocreate iOS, Android e App di Windows Store con le relative interfacce utente native. Questa esercitazione viene illustrato come toouse Xamarin toocreate un'applicazione che utilizza l'archiviazione Blob di Azure.
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
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="ad279-104">Come toouse archivio Blob di Xamarin</span><span class="sxs-lookup"><span data-stu-id="ad279-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="ad279-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ad279-105">Overview</span></span>
<span data-ttu-id="ad279-106">Xamarin consente agli sviluppatori toouse condivisa c# codebase toocreate iOS, Android e App di Windows Store con le relative interfacce utente native.</span><span class="sxs-lookup"><span data-stu-id="ad279-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="ad279-107">In questa esercitazione illustra come toouse archiviazione Blob di Azure con un'applicazione di Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ad279-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="ad279-108">Se si desidera toolearn ulteriori informazioni sull'archiviazione di Azure, prima di entrare nel codice hello, vedere [tooMicrosoft introduzione di archiviazione di Azure](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad279-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="ad279-109">Creare una nuova applicazione Xamarin</span><span class="sxs-lookup"><span data-stu-id="ad279-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="ad279-110">Per questa esercitazione verrà generata un'applicazione destinata ad Android, iOS e Windows.</span><span class="sxs-lookup"><span data-stu-id="ad279-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="ad279-111">Questa applicazione creerà semplicemente un contenitore nel quale caricherà un BLOB.</span><span class="sxs-lookup"><span data-stu-id="ad279-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="ad279-112">Visual Studio verrà usato in Windows, ma hello procedurali stesso possono essere applicati quando si crea un'app usando Xamarin Studio in macOS.</span><span class="sxs-lookup"><span data-stu-id="ad279-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="ad279-113">Seguire questi passaggi toocreate l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="ad279-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="ad279-114">Se necessario, scaricare e installare [Xamarin per Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="ad279-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="ad279-115">Aprire Visual Studio e creare un'applicazione vuota (nativa portatile): **File > Nuovo > Progetto > Multipiattaforma > Applicazione vuota (nativa portatile)**.</span><span class="sxs-lookup"><span data-stu-id="ad279-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="ad279-116">La soluzione nel riquadro Esplora soluzioni hello e scegliere **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="ad279-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="ad279-117">Cercare **Windowsazure** e installare i hello ultima versione stabile tooall progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="ad279-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="ad279-118">Compilare ed eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="ad279-118">Build and run your project.</span></span>

<span data-ttu-id="ad279-119">È ora un'applicazione che consente di tooclick un pulsante che viene incrementato un contatore.</span><span class="sxs-lookup"><span data-stu-id="ad279-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="ad279-120">Creare un contenitore e caricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="ad279-120">Create container and upload blob</span></span>
<span data-ttu-id="ad279-121">Quindi, sotto il `(Portable)` progetto, si aggiungerà codice troppo`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="ad279-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="ad279-122">Questo codice crea un contenitore e carica in esso un oggetto BLOB.</span><span class="sxs-lookup"><span data-stu-id="ad279-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="ad279-123">`MyClass.cs`dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ad279-123">`MyClass.cs` should look like hello following:</span></span>

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

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="ad279-124">Verificare che tooreplace "your_account_name_here" e "your_account_key_here" con il nome account effettivo e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="ad279-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="ad279-125">Il iOS, Android e Windows Phone tutti i progetti presentano riferimenti tooyour progetto portabile, pertanto che è possibile scrivere tutto il codice condiviso in uno posizionare e utilizzarlo in tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="ad279-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="ad279-126">È ora possibile aggiungere hello successiva riga di codice tooeach progetto toostart sfruttando:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="ad279-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="ad279-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="ad279-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="ad279-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="ad279-128">XamarinApp.iOS > ViewController.cs</span></span>

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
                // Perform any additional setup after loading hello view, typically from a nib.
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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="ad279-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="ad279-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
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
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
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

## <a name="run-hello-application"></a><span data-ttu-id="ad279-130">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="ad279-130">Run hello application</span></span>
<span data-ttu-id="ad279-131">È ora possibile eseguire questa applicazione in un emulatore Android o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ad279-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="ad279-132">È inoltre possibile eseguire questa applicazione in un emulatore iOS, ma questo richiederà un Mac.</span><span class="sxs-lookup"><span data-stu-id="ad279-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="ad279-133">Per istruzioni specifiche su come toodo, leggere la documentazione di hello per [la connessione di Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="ad279-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="ad279-134">Dopo aver eseguito l'app, verrà creato il contenitore di hello `mycontainer` nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ad279-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="ad279-135">Deve contenere blob hello, `myblob`, che contiene il testo hello, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="ad279-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="ad279-136">È possibile verificarlo utilizzando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ad279-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad279-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad279-137">Next steps</span></span>
<span data-ttu-id="ad279-138">In questa esercitazione, si è appreso come toocreate un'applicazione multipiattaforma con Xamarin che utilizza l'archiviazione di Azure, particolare attenzione su uno scenario nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="ad279-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="ad279-139">È tuttavia possibile svolgere molte altre operazioni, non solo con l'archiviazione BLOB, ma anche con archiviazione tabelle, archiviazione file e archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="ad279-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="ad279-140">Verificare i seguenti articoli toolearn ulteriori hello:</span><span class="sxs-lookup"><span data-stu-id="ad279-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="ad279-141">Introduzione all'archiviazione BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="ad279-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ad279-142">Introduzione all'archiviazione tabelle di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="ad279-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ad279-143">Introduzione all'archiviazione code di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="ad279-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ad279-144">Introduzione ad Archiviazione file di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="ad279-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

