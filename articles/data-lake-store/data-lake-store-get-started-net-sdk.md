---
title: applicazioni di toodevelop aaaUse hello .NET SDK in archivio Azure Data Lake | Documenti Microsoft
description: Utilizzare SDK .NET di Azure Data Lake archivio toocreate un account archivio Data Lake ed eseguire operazioni di base in hello archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Introduzione ad Azure Data Lake Store con .NET SDK
> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Informazioni su come hello toouse [Azure Data Lake archivio .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform operazioni di base, ad esempio, creare cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Prerequisiti
* **Visual Studio 2013, 2015 o 2017**. istruzioni di Hello seguente si usa Visual Studio 2015 Update 2.

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Account di Archivio Data Lake di Azure**. Per istruzioni su come toocreate un account, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)

* **Creare un'applicazione di Azure Active Directory**. Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD. Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Creare un'applicazione .NET
1. Aprire Visual Studio e creare un'applicazione console.
2. Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.
3. Da **nuovo progetto**digitare o selezionare hello seguenti valori:

   | Proprietà | Valore |
   | --- | --- |
   | Categoria |Templates/Visual C#/Windows |
   | Modello |Applicazione console |
   | Nome |CreateADLApplication |
4. Fare clic su **OK** progetto hello toocreate.
5. Aggiungere hello Nuget pacchetti tooyour progetto.

   1. Nome del progetto in Esplora soluzioni hello hello destro e fare clic su **Gestisci pacchetti NuGet**.
   2. In hello **Gestione pacchetti Nuget** scheda, assicurarsi che **origine pacchetto** è troppo**nuget.org** e che **Includi versione preliminare** casella di controllo viene selezionato.
   3. Cercare e installare i seguenti pacchetti NuGet hello:

      * `Microsoft.Azure.Management.DataLake.Store` - Questa esercitazione usa v2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - Questa esercitazione usa la versione 2.2.12.

        ![Aggiungere un'origine Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creare un nuovo account di Azure Data Lake")
   4. Chiude hello **Gestione pacchetti Nuget**.
6. Aprire **Program.cs**, eliminare il codice esistente hello e quindi includere hello seguendo le istruzioni tooadd riferimenti toonamespaces.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Dichiarare le variabili di hello come illustrato di seguito e fornire i valori hello per nome di archivio Data Lake e nome di gruppo di risorse hello che esiste già. Assicurarsi inoltre che deve essere presente nel computer di hello hello percorso e il nome locale che qui. Aggiungere hello seguente frammento di codice dopo le dichiarazioni dello spazio dei nomi di hello.

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

In hello rimanenti sezioni dell'articolo hello, è possibile visualizzare come toouse hello .NET metodi tooperform le operazioni disponibili, ad esempio l'autenticazione, il caricamento di file e così via.

## <a name="authentication"></a>Autenticazione

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Se si usa l'autenticazione dell'utente finale (consigliata per questa esercitazione)

Utilizzare con un'applicazione nativa tooauthenticate di esistente AD Azure, l'applicazione **in modo interattivo**, che significa che sarà richiesto tooenter le credenziali di Azure.

Per semplicità, frammento hello seguente utilizza valori predefiniti per ID client e reindirizzamento URI che funzioneranno con qualsiasi sottoscrizione di Azure. toohelp aver completato questa esercitazione più velocemente, è consigliabile che utilizzare questo approccio. Nel seguente frammento di hello, è sufficiente fornire il valore di hello per l'ID del tenant. È possibile recuperare tramite istruzioni hello disponibili all'indirizzo [creare un'applicazione di Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Un paio di aspetti tooknow su questo frammento di codice precedente:

* Questo frammento di codice toohelp completare l'esercitazione hello più velocemente, utilizza una Azure Active Directory ID client e di dominio che è disponibile per impostazione predefinita per tutte le sottoscrizioni di Azure. È quindi possibile **usare questo frammento così com'è nell'applicazione**.
* Tuttavia, se desidera toouse il proprio dominio di Azure AD e ID client dell'applicazione, è necessario creare un'applicazione nativa AD Azure e quindi utilizzare hello Azure AD tenant ID, ID client e URI di reindirizzamento per un'applicazione hello è stato creato. Per istruzioni, vedere [Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Se si usa l'autenticazione da servizio a servizio con il segreto client
Hello seguente frammento di codice può essere utilizzato tooauthenticate applicazione **in modo non interattivo**, utilizzando la chiave privata client hello / chiave per un'entità servizio / dell'applicazione. Usare il frammento con una "app Web" di Azure AD esistente. Per istruzioni su come visualizzare un'applicazione web toocreate hello Azure AD e come tooretrieve hello client ID e segreto client richiesto nel seguente frammento di hello [creare applicazione Active Directory per l'autenticazione al servizio dati Archivio Lake](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Se si usa l'autenticazione da servizio a servizio con il certificato

Come una terza opzione, hello seguente frammento di codice può essere utilizzato tooauthenticate applicazione **in modo non interattivo**, per un'applicazione Azure Active Directory utilizza certificato hello / entità di servizio. Usare il frammento con un'[applicazione di Azure AD con certificati](../azure-resource-manager/resource-group-authenticate-service-principal.md) esistente.

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Creare oggetti client
Hello frammento di codice seguente crea account archivio Data Lake hello e filesystem oggetti client, che vengono utilizzati tooissue richiede toohello servizio.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Elencare tutti gli account Data Lake Store all'interno di una sottoscrizione
Hello frammento di codice seguente sono elencati tutti gli account archivio Data Lake all'interno di una specifica sottoscrizione di Azure.

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a>Creare una directory
Hello seguente mostra un `CreateDirectory` metodo che è possibile utilizzare una directory all'interno di un account archivio Data Lake toocreate.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Caricare un file
Hello seguente mostra un `UploadFile` metodo che è possibile utilizzare tooupload file account archivio Data Lake tooa.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Hello SDK supporta ricorsiva caricamento e download tra un percorso file locale e un percorso di file di archivio Data Lake.    

## <a name="get-file-or-directory-info"></a>Ottenere informazioni su un file o una directory
Hello seguente mostra un `GetItemInfo` metodo che è possibile utilizzare un file o directory disponibili tooretrieve informazioni nell'archivio Data Lake.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Elencare file o directory
Hello seguente mostra un `ListItem` metodo che è possibile utilizzare toolist hello file e directory in un account archivio Data Lake.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Concatenare file
Hello seguente mostra un `ConcatenateFiles` metodo utilizzare file tooconcatenate.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Aggiungere file tooa
Hello seguente mostra un `AppendToFile` metodo da utilizzare accodare il file di tooa dati già archiviati in un account archivio Data Lake.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Scaricare un file
Hello seguente mostra un `DownloadFile` metodo utilizzare toodownload un file da un account archivio Data Lake.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Informazioni di riferimento su .NET SDK con Data Lake Store](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
