<span data-ttu-id="22d9b-101">Se si dispone di un URL di firma di accesso condiviso che concede l'accesso alle risorse in un account di archiviazione, è possibile usare la firma di accesso condiviso in una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="22d9b-101">If you possess a shared access signature (SAS) URL that grants you access to resources in a storage account, you can use the SAS in a connection string.</span></span> <span data-ttu-id="22d9b-102">Poiché la firma di accesso condiviso contiene le informazioni necessarie per autenticare la richiesta, una stringa di connessione con una firma di accesso condiviso fornisce il protocollo, l'endpoint di servizio e le credenziali necessarie per accedere alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="22d9b-102">Because the SAS contains the information required to authenticate the request, a connection string with a SAS provides the protocol, the service endpoint, and the necessary credentials to access the resource.</span></span>

<span data-ttu-id="22d9b-103">Per creare una stringa di connessione che include una firma di accesso condiviso, specificare la stringa nel seguente formato:</span><span class="sxs-lookup"><span data-stu-id="22d9b-103">To create a connection string that includes a shared access signature, specify the string in the following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="22d9b-104">Ogni endpoint di servizio è facoltativo anche se la stringa di connessione deve contenerne almeno uno.</span><span class="sxs-lookup"><span data-stu-id="22d9b-104">Each service endpoint is optional, although the connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="22d9b-105">La procedura consigliata prevede l'uso di HTTPS con la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="22d9b-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="22d9b-106">Se si specifica una firma di accesso condiviso in una stringa di connessione all'interno di un file di configurazione, potrebbe essere necessario codificare caratteri speciali nell'URL.</span><span class="sxs-lookup"><span data-stu-id="22d9b-106">If you are specifying a SAS in a connection string in a configuration file, you may need to encode special characters in the URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="22d9b-107">Esempio di firma di accesso condiviso del servizio</span><span class="sxs-lookup"><span data-stu-id="22d9b-107">Service SAS example</span></span>
<span data-ttu-id="22d9b-108">Ecco un esempio di stringa di connessione che include una firma di accesso condiviso del servizio per l'archiviazione BLOB:</span><span class="sxs-lookup"><span data-stu-id="22d9b-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="22d9b-109">Ecco invece un esempio della stessa stringa di connessione con la codifica dei caratteri speciali:</span><span class="sxs-lookup"><span data-stu-id="22d9b-109">And here's an example of the same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="22d9b-110">Esempio di firma di accesso condiviso dell'account</span><span class="sxs-lookup"><span data-stu-id="22d9b-110">Account SAS example</span></span>
<span data-ttu-id="22d9b-111">Ecco un esempio di stringa di connessione che include una firma di accesso condiviso dell'account per l'archivio BLOB e file.</span><span class="sxs-lookup"><span data-stu-id="22d9b-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="22d9b-112">Si noti che sono specificati gli endpoint per entrambi i servizi:</span><span class="sxs-lookup"><span data-stu-id="22d9b-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="22d9b-113">Ecco invece un esempio della stessa stringa di connessione con la codifica dell'URL:</span><span class="sxs-lookup"><span data-stu-id="22d9b-113">And here's an example of the same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

