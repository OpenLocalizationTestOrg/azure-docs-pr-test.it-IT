---
title: '.NET SDK: Operazioni del file system in Azure Data Lake Store | Microsoft Docs'
description: Usare Azure Data Lake Store con .NET SDK per eseguire operazioni del file system, come la creazione di cartelle, in Data Lake Store.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2017
ms.author: nitinme
ms.openlocfilehash: a5d446986f810993d65c7e73eb95eeb2283c39a3
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="filesystem-operations-on-azure-data-lake-store-using-net-sdk"></a>Operazioni del file system in Azure Data Lake Store con .NET SDK
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-data-operations-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-data-operations-rest-api.md)
> * [Python](data-lake-store-data-operations-python.md)
>
>

Questo articolo fornisce informazioni per l'esecuzione di operazioni del file system in Data Lake Store con .NET SDK. Le operazioni del file system includono la creazione di cartelle in un account Data Lake Store, il caricamento di file, il download di file e così via.

Per istruzioni su come eseguire le operazioni di gestione di account in Data Lake Store con .NET SDK, vedere [Operazioni di gestione di account in Data Lake Store con .NET SDK](data-lake-store-get-started-net-sdk.md).

## <a name="prerequisites"></a>Prerequisiti
* **Visual Studio 2013, 2015 o 2017**. Le istruzioni seguenti fanno riferimento a Visual Studio 2017.

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Account di Archivio Data Lake di Azure**. Per istruzioni su come creare un account, vedere [Introduzione ad Azure Data Lake Store tramite il portale di Azure](data-lake-store-get-started-portal.md)

## <a name="create-a-net-application"></a>Creare un'applicazione .NET
Il codice di esempio disponibile in [GitHub](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted) offre una descrizione dei processi di creazione dei file nell'archivio, concatenazione dei file, download di un file ed eliminazione di alcuni file nell'archivio. Questa sezione dell'articolo descrive in modo dettagliato le parti principali del codice.

1. Aprire Visual Studio e creare un'applicazione console.
2. Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.
3. In **Nuovo progetto**digitare o selezionare i valori seguenti:

   | Proprietà | Valore |
   | --- | --- |
   | Categoria |Templates/Visual C#/Windows |
   | Modello |Applicazione console |
   | Nome |CreateADLApplication |

4. Fare clic su **OK** per creare il progetto.

5. Aggiungere i pacchetti NuGet al progetto.

   1. Fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e scegliere **Gestisci pacchetti NuGet**.
   2. Nella scheda **Gestione pacchetti NuGet** assicurarsi che **Origine pacchetto** sia impostato su **nuget.org** e che la casella di controllo **Includi versione preliminare** sia selezionata.
   3. Cercare e installare i pacchetti NuGet seguenti:

      * `Microsoft.Azure.DataLake.Store` - Questa esercitazione usa la versione 1.0.0.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - Questa esercitazione usa la versione 2.3.1.
    
    Chiudere **Gestione pacchetti NuGet**.

6. Aprire **Program.cs**, eliminare il codice esistente e quindi includere le istruzioni seguenti per aggiungere riferimenti agli spazi dei nomi.

        using System;
        using System.IO;using System.Threading;
        using System.Linq;
        using System.Text;
        using System.Collections.Generic;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
                
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.DataLake.Store;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

7. Dichiarare le variabili come illustrato di seguito e fornire i valori per i segnaposto. Assicurarsi anche che il percorso locale e il nome file forniti siano presenti nel computer.

        namespace SdkSample
        {
            class Program
            {
                private static string _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; //Replace this value with the name of your existing Data Lake Store account.        
            }
        }

Nelle sezioni rimanenti dell'articolo è possibile vedere come usare i metodi .NET disponibili per eseguire operazioni come autenticazione, caricamento di file e così via.

## <a name="authentication"></a>Autenticazione

* Per l'autenticazione dell'utente finale per l'applicazione, vedere [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md) (Autenticazione dell'utente finale con Data Lake Store tramite .NET SDK).
* Per l'autenticazione da servizio a servizio per l'applicazione, vedere [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md) (Autenticazione da servizio a servizio con Data Lake Store tramite .NET SDK).


## <a name="create-client-object"></a>Creare un oggetto client
Il frammento di codice seguente crea l'oggetto client del file system di Data Lake Store, usato per inviare richieste al servizio.

    // Create client objects
    AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);

## <a name="create-a-file-and-directory"></a>Creare un file e una directory
Aggiungere il frammento di codice seguente all'applicazione. Questo frammento di codice aggiunge un file ed eventuali directory padre ancora inesistenti.

    // Create a file - automatically creates any parent directories that don't exist
    
    string fileName = "/Test/testFilename1.txt";
    using (var streamWriter = new StreamWriter(client.CreateFile(fileName, IfExists.Overwrite)))
    {
        streamWriter.WriteLine("This is test data to write");
        streamWriter.WriteLine("This is line 2");
    }

## <a name="append-to-a-file"></a>Aggiungere a un file
Il frammento di codice seguente accoda dati a un file esistente nell'account Data Lake Store.

    // Append to existing file
    using (var streamWriter = new StreamWriter(client.GetAppendStream(fileName)))
    {
        streamWriter.WriteLine("This is the added line");
    }

## <a name="read-a-file"></a>Leggere un file
Il frammento di codice seguente legge il contenuto di un file in Data Lake Store.

    //Read file contents
    using (var readStream = new StreamReader(client.GetReadStream(fileName)))
    {
        string line;
        while ((line = readStream.ReadLine()) != null)
        {
            Console.WriteLine(line);
        }
    }

## <a name="get-file-properties"></a>Ottenere le proprietà dei file
Il frammento di codice seguente restituisce le proprietà associate a un file o una directory.

    // Get file properties
    var directoryEntry = client.GetDirectoryEntry(fileName);
    PrintDirectoryEntry(directoryEntry);

La definizione del metodo `PrintDirectoryEntry` è disponibile come parte dell'esempio [su GitHub](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted). 

## <a name="rename-a-file"></a>Rinominare un file
Il frammento di codice seguente rinomina un file esistente in un account Data Lake Store.

    // Rename a file
    string destFilePath = "/Test/testRenameDest3.txt";
    client.Rename(fileName, destFilePath, true);

## <a name="enumerate-a-directory"></a>Enumerare una directory
Il frammento di codice seguente enumera le directory in un account Data Lake Store

    // Enumerate directory
    foreach (var entry in client.EnumerateDirectory("/Test"))
    {
        PrintDirectoryEntry(entry);
    }

La definizione del metodo `PrintDirectoryEntry` è disponibile come parte dell'esempio [su GitHub](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted).

## <a name="delete-directories-recursively"></a>Eliminare directory in modo ricorsivo
Il frammento di codice seguente elimina una directory e tutte le relative sottodirectory in modo ricorsivo.

    // Delete a directory and all it's subdirectories and files
    client.DeleteRecursive("/Test");

## <a name="samples"></a>Esempi
Ecco alcuni esempi che illustrano come usare l'SDK del file system di Data Lake Store.
* [Esempio di base in Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted)
* [Esempio avanzato in Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-samples)

## <a name="see-also"></a>Vedere anche
* [Operazioni di gestione di account in Data Lake Store con .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Informazioni di riferimento su .NET SDK con Data Lake Store](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet)

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
