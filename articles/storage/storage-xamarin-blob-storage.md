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
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Come toouse archivio Blob di Xamarin
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Panoramica
Xamarin consente agli sviluppatori toouse condivisa c# codebase toocreate iOS, Android e App di Windows Store con le relative interfacce utente native. In questa esercitazione illustra come toouse archiviazione Blob di Azure con un'applicazione di Xamarin. Se si desidera toolearn ulteriori informazioni sull'archiviazione di Azure, prima di entrare nel codice hello, vedere [tooMicrosoft introduzione di archiviazione di Azure](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Creare una nuova applicazione Xamarin
Per questa esercitazione verrà generata un'applicazione destinata ad Android, iOS e Windows. Questa applicazione creerà semplicemente un contenitore nel quale caricherà un BLOB. Visual Studio verrà usato in Windows, ma hello procedurali stesso possono essere applicati quando si crea un'app usando Xamarin Studio in macOS.

Seguire questi passaggi toocreate l'applicazione:

1. Se necessario, scaricare e installare [Xamarin per Visual Studio](https://www.xamarin.com/download).
2. Aprire Visual Studio e creare un'applicazione vuota (nativa portatile): **File > Nuovo > Progetto > Multipiattaforma > Applicazione vuota (nativa portatile)**.
3. La soluzione nel riquadro Esplora soluzioni hello e scegliere **Gestisci pacchetti NuGet per la soluzione**. Cercare **Windowsazure** e installare i hello ultima versione stabile tooall progetti nella soluzione.
4. Compilare ed eseguire il progetto.

È ora un'applicazione che consente di tooclick un pulsante che viene incrementato un contatore.

## <a name="create-container-and-upload-blob"></a>Creare un contenitore e caricare un BLOB
Quindi, sotto il `(Portable)` progetto, si aggiungerà codice troppo`MyClass.cs`. Questo codice crea un contenitore e carica in esso un oggetto BLOB. `MyClass.cs`dovrebbe essere simile hello seguente:

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

Verificare che tooreplace "your_account_name_here" e "your_account_key_here" con il nome account effettivo e la chiave dell'account. 

Il iOS, Android e Windows Phone tutti i progetti presentano riferimenti tooyour progetto portabile, pertanto che è possibile scrivere tutto il codice condiviso in uno posizionare e utilizzarlo in tutti i progetti. È ora possibile aggiungere hello successiva riga di codice tooeach progetto toostart sfruttando:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

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

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

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

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
È ora possibile eseguire questa applicazione in un emulatore Android o Windows Phone. È inoltre possibile eseguire questa applicazione in un emulatore iOS, ma questo richiederà un Mac. Per istruzioni specifiche su come toodo, leggere la documentazione di hello per [la connessione di Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Dopo aver eseguito l'app, verrà creato il contenitore di hello `mycontainer` nell'account di archiviazione. Deve contenere blob hello, `myblob`, che contiene il testo hello, `Hello, world!`. È possibile verificarlo utilizzando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toocreate un'applicazione multipiattaforma con Xamarin che utilizza l'archiviazione di Azure, particolare attenzione su uno scenario nell'archiviazione Blob. È tuttavia possibile svolgere molte altre operazioni, non solo con l'archiviazione BLOB, ma anche con archiviazione tabelle, archiviazione file e archiviazione code. Verificare i seguenti articoli toolearn ulteriori hello:

* [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md)
* [Introduzione all'archiviazione tabelle di Azure con .NET](storage-dotnet-how-to-use-tables.md)
* [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md)
* [Introduzione ad Archiviazione file di Azure in Windows](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

