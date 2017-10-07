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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="cd6a1-104">Applicazione locale con archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="cd6a1-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="cd6a1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cd6a1-105">Overview</span></span>
<span data-ttu-id="cd6a1-106">Hello seguente esempio viene illustrato come è possibile utilizzare l'archiviazione di Azure per archiviare le immagini in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="cd6a1-107">codice Hello in questo articolo è per un'applicazione console che carica un'immagine tooAzure e quindi crea un file HTML che visualizza l'immagine di hello nel browser.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd6a1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cd6a1-108">Prerequisites</span></span>
* <span data-ttu-id="cd6a1-109">È installato Java Developer Kit (JDK) v1.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="cd6a1-110">Hello Azure SDK è installato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="cd6a1-111">Hello JAR per hello Azure Libraries for Java e JAR qualsiasi dipendenza applicabile, vengono installati e si trovano nel percorso di compilazione hello utilizzato dal compilatore del linguaggio.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="cd6a1-112">Per informazioni sull'installazione hello Azure Libraries for Java, vedere [Download hello Azure SDK per Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="cd6a1-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="cd6a1-113">Account di Archiviazione di Azure configurato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="cd6a1-114">Hello nome account e la chiave per l'account di archiviazione hello da utilizzare per il codice hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="cd6a1-115">Vedere [come un Account di archiviazione tooCreate](storage-create-storage-account.md#create-a-storage-account) per informazioni sulla creazione di un account di archiviazione e [chiavi di accesso di archiviazione di visualizzazione e copia](storage-create-storage-account.md#view-and-copy-storage-access-keys) per informazioni sul recupero chiave dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="cd6a1-116">È stato creato un file di immagine locale denominato archiviato in hello path c:\\myimages\\Image1.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="cd6a1-117">In alternativa, modificare il **FileInputStream** costruttore toouse esempio hello un nome di percorso e il file di immagine diverso.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="cd6a1-118">tooupload di archiviazione blob di Azure toouse un file</span><span class="sxs-lookup"><span data-stu-id="cd6a1-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="cd6a1-119">Di seguito viene presentata una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="cd6a1-120">Se si desidera tooskip-ahead, viene visualizzato tutto il codice hello più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="cd6a1-121">Inizio del codice hello includendo le importazioni per classi di archiviazione di Azure core hello, classi di client hello blob di Azure, le classi dei / o Java hello e hello **URISyntaxException** classe.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="cd6a1-122">Dichiarare una classe denominata **StorageSample**e includere una parentesi quadra aperta hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="cd6a1-123">All'interno di hello **StorageSample** classe, dichiarare una variabile di stringa contenenti protocollo dell'endpoint predefinito hello, il nome di account di archiviazione e la chiave di accesso di archiviazione, come specificato nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="cd6a1-124">Sostituire i valori segnaposto hello **il\_account\_nome** e **il\_account\_chiave** con il proprio nome account e la chiave dell'account, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="cd6a1-125">Aggiungere la dichiarazione per **principale**, includere un **provare** blocco e includere hello necessario aprire le parentesi quadre, **{**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="cd6a1-126">Dichiarare le variabili di hello dopo il tipo (Buongiorno descrizioni sono per la modalità di utilizzo in questo esempio):</span><span class="sxs-lookup"><span data-stu-id="cd6a1-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="cd6a1-127">**CloudStorageAccount**: hello tooinitialize usati account oggetto con il nome di account di archiviazione di Azure e una chiave e toocreate l'oggetto client di blob.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="cd6a1-128">**CloudBlobClient**: tooaccess hello blob servizio utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="cd6a1-129">**CloudBlobContainer**: toocreate usato un contenitore blob, elencare i BLOB nel contenitore hello e contenitore hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="cd6a1-130">**CloudBlockBlob**: tooupload usato un contenitore di toothe file di immagine locale.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="cd6a1-131">Assegnare un valore toohello **account** variabile.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="cd6a1-132">Assegnare un valore toohello **serviceClient** variabile.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="cd6a1-133">Assegnare un valore toohello **contenitore** variabile.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="cd6a1-134">Si otterrà un contenitore tooa riferimento denominato **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="cd6a1-135">Creare il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-135">Create hello container.</span></span> <span data-ttu-id="cd6a1-136">Questo metodo creerà contenitore hello se non esiste (e restituire **true**).</span><span class="sxs-lookup"><span data-stu-id="cd6a1-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="cd6a1-137">Se il contenitore di hello esiste, verrà restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="cd6a1-138">Un'alternativa troppo**createIfNotExists** è hello **creare** metodo (che verrà restituito un errore se hello contenitore esiste già).</span><span class="sxs-lookup"><span data-stu-id="cd6a1-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="cd6a1-139">Impostare l'accesso anonimo per il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="cd6a1-140">Ottenere un blob in blocchi toohello riferimento, che rappresenterà il blob hello in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="cd6a1-141">Hello utilizzare **File** costruttore tooget un file di riferimento toohello creata in locale che verrà caricato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="cd6a1-142">Assicurarsi di che aver creato il file prima di eseguire codice hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="cd6a1-143">Caricare hello file locale tramite una chiamata di toohello **CloudBlockBlob.upload** metodo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="cd6a1-144">primo parametro toohello Hello **CloudBlockBlob.upload** metodo è un **FileInputStream** dell'oggetto che rappresenta hello locale il file che verrà caricato tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="cd6a1-145">secondo parametro Hello è hello dimensione in byte, del file hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="cd6a1-146">Chiamare una funzione helper denominata **MakeHTMLPage**, pagina toomake HTML di base che contiene un  **&lt;immagine&gt;**  elemento con la blob hello origine set toohello in di Azure account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="cd6a1-147">codice per Hello **MakeHTMLPage** verrà descritta più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="cd6a1-148">Stampa un messaggio di stato e informazioni su una pagina HTML creata hello.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="cd6a1-149">Chiude hello **provare** blocco tramite l'inserimento di parentesi quadra chiusa: **}**</span><span class="sxs-lookup"><span data-stu-id="cd6a1-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cd6a1-150">Gestire hello le eccezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd6a1-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="cd6a1-151">**FileNotFoundException**: possono essere generate da hello **FileInputStream** o **FileOutputStream** costruttori.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="cd6a1-152">**StorageException**: possono essere generate dalla libreria di archiviazione di hello client di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="cd6a1-153">**URISyntaxException**: possono essere generate da hello **ListBlobItem.getUri** metodo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="cd6a1-154">**Exception**: gestione eccezioni generica.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="cd6a1-155">Chiudere **main** inserendo una parentesi chiusa: **}**</span><span class="sxs-lookup"><span data-stu-id="cd6a1-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cd6a1-156">Creare un metodo denominato **MakeHTMLPage** pagina toocreate HTML di base.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="cd6a1-157">Questo metodo ha un parametro di tipo **CloudBlobContainer**, che sarà utilizzato tooiterate tramite elenco hello di BLOB caricato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="cd6a1-158">Questo metodo genererà eccezioni di tipo **FileNotFoundException**, che possono essere generate da hello **FileOutputStream** costruttore e **URISyntaxException**, che può essere generate da hello **ListBlobItem.getUri** metodo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="cd6a1-159">Includere la parentesi di apertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="cd6a1-160">Creare un file locale denominato **index.html**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="cd6a1-161">Scrivere il file locale toohello, aggiunta in hello  **&lt;html&gt;**,  **&lt;intestazione&gt;**, e  **&lt;corpo&gt;**  elementi.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="cd6a1-162">Scorrere l'elenco di hello di BLOB caricato.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="cd6a1-163">Per ogni blob, nella pagina HTML hello creare un  **&lt;img&gt;**  elemento con il relativo **src** attributo inviato a messaggi hello URI del blob hello presenti nell'account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="cd6a1-164">Anche se in questo esempio è stata aggiunta una sola immagine, se se ne aggiungono altre, il codice le itererà tutte.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="cd6a1-165">Per maggior semplicità, in questo esempio si presume che ogni BLOB caricato sia un'immagine.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="cd6a1-166">Se è stato aggiornato BLOB diversi da immagini o BLOB di pagine anziché i BLOB in blocchi, è possibile modificare codice hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="cd6a1-167">Chiude hello  **&lt;corpo&gt;**  elemento e hello  **&lt;html&gt;**  elemento.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="cd6a1-168">File locale hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="cd6a1-169">Chiudere **MakeHTMLPage** inserendo una parentesi chiusa: **}**</span><span class="sxs-lookup"><span data-stu-id="cd6a1-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cd6a1-170">Chiudere **StorageSample** inserendo una parentesi chiusa: **}**</span><span class="sxs-lookup"><span data-stu-id="cd6a1-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cd6a1-171">di seguito Hello è codice completo di hello per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="cd6a1-172">Tenere presente i valori di segnaposto hello toomodify **il\_account\_nome** e **il\_account\_chiave** toouse nome account e account chiave, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

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

<span data-ttu-id="cd6a1-173">In aggiunta toouploading l'archiviazione di tooAzure file di immagine locale, codice di esempio hello crea namedindex.html un file locale, che è possibile aprire in toosee il browser l'immagine caricata.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="cd6a1-174">Poiché il codice hello contiene il nome account e la chiave dell'account, assicurarsi che il codice sorgente sia protetto.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="cd6a1-175">toodelete un contenitore</span><span class="sxs-lookup"><span data-stu-id="cd6a1-175">toodelete a container</span></span>
<span data-ttu-id="cd6a1-176">Poiché vengono addebitati per l'archiviazione, è opportuno toodelete il **gettingstarted** contenitore dopo aver completato la sperimentazione con questo esempio.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="cd6a1-177">toodelete un contenitore, utilizzare hello **CloudBlobContainer.delete** metodo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="cd6a1-178">hello toocall **CloudBlobContainer.delete** (metodo), il processo di hello di inizializzazione **CloudStorageAccount**, **ClodBlobClient**, e  **CloudBlobContainer** oggetti è hello uguale a quello mostrato per la **createIfNotExist** metodo.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="cd6a1-179">Hello seguito è riportato un esempio completo che elimina hello contenitore denominato **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="cd6a1-180">Per una panoramica di altri metodi e classi di archiviazione blob, vedere [come archiviazione di Blob da Java toouse](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cd6a1-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd6a1-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd6a1-181">Next steps</span></span>
<span data-ttu-id="cd6a1-182">Seguire questi toolearn collegamenti ulteriori informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="cd6a1-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="cd6a1-183">Azure Storage SDK per Java</span><span class="sxs-lookup"><span data-stu-id="cd6a1-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="cd6a1-184">Riferimento all'SDK del client di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cd6a1-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="cd6a1-185">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cd6a1-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="cd6a1-186">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cd6a1-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

