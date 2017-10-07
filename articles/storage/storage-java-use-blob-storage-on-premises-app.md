---
title: applicazione aaaOn locale all'archiviazione blob (linguaggio) | Documenti Microsoft
description: Informazioni su come un'applicazione console che carica un'immagine tooAzure, quindi viene visualizzato toocreate hello immagine nel browser. Esempi di codice in Java.
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Applicazione locale con archiviazione BLOB
## <a name="overview"></a>Panoramica
Hello seguente esempio viene illustrato come è possibile utilizzare l'archiviazione di Azure per archiviare le immagini in Azure. codice Hello in questo articolo è per un'applicazione console che carica un'immagine tooAzure e quindi crea un file HTML che visualizza l'immagine di hello nel browser.

## <a name="prerequisites"></a>Prerequisiti
* È installato Java Developer Kit (JDK) v1.6 o versione successiva.
* Hello Azure SDK è installato.
* Hello JAR per hello Azure Libraries for Java e JAR qualsiasi dipendenza applicabile, vengono installati e si trovano nel percorso di compilazione hello utilizzato dal compilatore del linguaggio. Per informazioni sull'installazione hello Azure Libraries for Java, vedere [Download hello Azure SDK per Java](../java-download-azure-sdk.md).
* Account di Archiviazione di Azure configurato. Hello nome account e la chiave per l'account di archiviazione hello da utilizzare per il codice hello in questo articolo. Vedere [come un Account di archiviazione tooCreate](storage-create-storage-account.md#create-a-storage-account) per informazioni sulla creazione di un account di archiviazione e [chiavi di accesso di archiviazione di visualizzazione e copia](storage-create-storage-account.md#view-and-copy-storage-access-keys) per informazioni sul recupero chiave dell'account hello.
* È stato creato un file di immagine locale denominato archiviato in hello path c:\\myimages\\Image1. In alternativa, modificare il **FileInputStream** costruttore toouse esempio hello un nome di percorso e il file di immagine diverso.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload di archiviazione blob di Azure toouse un file
Di seguito viene presentata una procedura dettagliata. Se si desidera tooskip-ahead, viene visualizzato tutto il codice hello più avanti in questo articolo.

Inizio del codice hello includendo le importazioni per classi di archiviazione di Azure core hello, classi di client hello blob di Azure, le classi dei / o Java hello e hello **URISyntaxException** classe.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Dichiarare una classe denominata **StorageSample**e includere una parentesi quadra aperta hello, **{**.

```java
public class StorageSample {
```

All'interno di hello **StorageSample** classe, dichiarare una variabile di stringa contenenti protocollo dell'endpoint predefinito hello, il nome di account di archiviazione e la chiave di accesso di archiviazione, come specificato nell'account di archiviazione di Azure. Sostituire i valori segnaposto hello **il\_account\_nome** e **il\_account\_chiave** con il proprio nome account e la chiave dell'account, rispettivamente.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Aggiungere la dichiarazione per **principale**, includere un **provare** blocco e includere hello necessario aprire le parentesi quadre, **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Dichiarare le variabili di hello dopo il tipo (Buongiorno descrizioni sono per la modalità di utilizzo in questo esempio):

* **CloudStorageAccount**: hello tooinitialize usati account oggetto con il nome di account di archiviazione di Azure e una chiave e toocreate l'oggetto client di blob.
* **CloudBlobClient**: tooaccess hello blob servizio utilizzato.
* **CloudBlobContainer**: toocreate usato un contenitore blob, elencare i BLOB nel contenitore hello e contenitore hello di eliminazione.
* **CloudBlockBlob**: tooupload usato un contenitore di toothe file di immagine locale.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Assegnare un valore toohello **account** variabile.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Assegnare un valore toohello **serviceClient** variabile.

```java
serviceClient = account.createCloudBlobClient();
```

Assegnare un valore toohello **contenitore** variabile. Si otterrà un contenitore tooa riferimento denominato **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Creare il contenitore di hello. Questo metodo creerà contenitore hello se non esiste (e restituire **true**). Se il contenitore di hello esiste, verrà restituito **false**. Un'alternativa troppo**createIfNotExists** è hello **creare** metodo (che verrà restituito un errore se hello contenitore esiste già).

```java
container.createIfNotExists();
```

Impostare l'accesso anonimo per il contenitore di hello.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Ottenere un blob in blocchi toohello riferimento, che rappresenterà il blob hello in archiviazione di Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Hello utilizzare **File** costruttore tooget un file di riferimento toohello creata in locale che verrà caricato. Assicurarsi di che aver creato il file prima di eseguire codice hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Caricare hello file locale tramite una chiamata di toohello **CloudBlockBlob.upload** metodo. primo parametro toohello Hello **CloudBlockBlob.upload** metodo è un **FileInputStream** dell'oggetto che rappresenta hello locale il file che verrà caricato tooAzure archiviazione. secondo parametro Hello è hello dimensione in byte, del file hello.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Chiamare una funzione helper denominata **MakeHTMLPage**, pagina toomake HTML di base che contiene un  **&lt;immagine&gt;**  elemento con la blob hello origine set toohello in di Azure account di archiviazione. codice per Hello **MakeHTMLPage** verrà descritta più avanti in questo articolo.

```java
MakeHTMLPage(container);
```

Stampa un messaggio di stato e informazioni su una pagina HTML creata hello.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Chiude hello **provare** blocco tramite l'inserimento di parentesi quadra chiusa: **}**

Gestire hello le eccezioni seguenti:

* **FileNotFoundException**: possono essere generate da hello **FileInputStream** o **FileOutputStream** costruttori.
* **StorageException**: possono essere generate dalla libreria di archiviazione di hello client di Azure.
* **URISyntaxException**: possono essere generate da hello **ListBlobItem.getUri** metodo.
* **Exception**: gestione eccezioni generica.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Chiudere **main** inserendo una parentesi chiusa: **}**

Creare un metodo denominato **MakeHTMLPage** pagina toocreate HTML di base. Questo metodo ha un parametro di tipo **CloudBlobContainer**, che sarà utilizzato tooiterate tramite elenco hello di BLOB caricato. Questo metodo genererà eccezioni di tipo **FileNotFoundException**, che possono essere generate da hello **FileOutputStream** costruttore e **URISyntaxException**, che può essere generate da hello **ListBlobItem.getUri** metodo. Includere la parentesi di apertura, **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Creare un file locale denominato **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Scrivere il file locale toohello, aggiunta in hello  **&lt;html&gt;**,  **&lt;intestazione&gt;**, e  **&lt;corpo&gt;**  elementi.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Scorrere l'elenco di hello di BLOB caricato. Per ogni blob, nella pagina HTML hello creare un  **&lt;img&gt;**  elemento con il relativo **src** attributo inviato a messaggi hello URI del blob hello presenti nell'account di archiviazione Azure.
Anche se in questo esempio è stata aggiunta una sola immagine, se se ne aggiungono altre, il codice le itererà tutte.

Per maggior semplicità, in questo esempio si presume che ogni BLOB caricato sia un'immagine. Se è stato aggiornato BLOB diversi da immagini o BLOB di pagine anziché i BLOB in blocchi, è possibile modificare codice hello in base alle esigenze.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Chiude hello  **&lt;corpo&gt;**  elemento e hello  **&lt;html&gt;**  elemento.

```java
stream.println("</body>");
stream.println("</html>");
```

File locale hello Chiudi.

```java
stream.close();
```

Chiudere **MakeHTMLPage** inserendo una parentesi chiusa: **}**

Chiudere **StorageSample** inserendo una parentesi chiusa: **}**

di seguito Hello è codice completo di hello per questo esempio. Tenere presente i valori di segnaposto hello toomodify **il\_account\_nome** e **il\_account\_chiave** toouse nome account e account chiave, rispettivamente.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

In aggiunta toouploading l'archiviazione di tooAzure file di immagine locale, codice di esempio hello crea namedindex.html un file locale, che è possibile aprire in toosee il browser l'immagine caricata.

Poiché il codice hello contiene il nome account e la chiave dell'account, assicurarsi che il codice sorgente sia protetto.

## <a name="toodelete-a-container"></a>toodelete un contenitore
Poiché vengono addebitati per l'archiviazione, è opportuno toodelete il **gettingstarted** contenitore dopo aver completato la sperimentazione con questo esempio. toodelete un contenitore, utilizzare hello **CloudBlobContainer.delete** metodo.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

hello toocall **CloudBlobContainer.delete** (metodo), il processo di hello di inizializzazione **CloudStorageAccount**, **ClodBlobClient**, e  **CloudBlobContainer** oggetti è hello uguale a quello mostrato per la **createIfNotExist** metodo. Hello seguito è riportato un esempio completo che elimina hello contenitore denominato **gettingstarted**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Per una panoramica di altri metodi e classi di archiviazione blob, vedere [come archiviazione di Blob da Java toouse](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori informazioni sulle attività di archiviazione più complesse.

* [Azure Storage SDK per Java](https://github.com/azure/azure-storage-java)
* [Riferimento all'SDK del client di archiviazione di Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)

