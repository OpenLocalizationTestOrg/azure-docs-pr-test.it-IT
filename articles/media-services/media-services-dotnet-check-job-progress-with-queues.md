---
title: Usare l'archiviazione code di Azure per monitorare le notifiche dei processi di Servizi multimediali con .NET | Microsoft Docs
description: "Informazioni su come usare l'archiviazione code di Azure per monitorare le notifiche dei processi di Servizi multimediali. L'esempio di codice è scritto in C# e usa l'SDK di Servizi multimediali per .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="ea9f9-104">Usare l'archiviazione code di Azure per monitorare le notifiche dei processi di Servizi multimediali con .NET</span><span class="sxs-lookup"><span data-stu-id="ea9f9-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="ea9f9-105">Quando si eseguono processi di codifica, spesso è necessario monitorarne l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="ea9f9-106">È possibile configurare Servizi multimediali per recapitare le notifiche ad [archiviazione code di Azure](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="ea9f9-107">È possibile controllare l'avanzamento del processo ottenendo le notifiche da archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="ea9f9-108">È possibile accedere ai messaggi distribuiti al servizio di archiviazione di accodamento da ogni parte del mondo.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="ea9f9-109">L'architettura di messaggistica di archiviazione code è affidabile e altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="ea9f9-110">Tra i vari metodi disponibili è preferibile usare il polling dell'archiviazione code per i messaggi.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="ea9f9-111">Può essere necessario ascoltare le notifiche di Servizi multimediali quando, ad esempio, si sta sviluppando un sistema di gestione dei contenuti ed è necessario che il sistema effettui alcune attività aggiuntive dopo il completamento di un processo di codifica (ad esempio, deve attivare il passaggio successivo di un flusso di lavoro o pubblicare contenuti).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="ea9f9-112">Questo argomento illustra come ricevere messaggi di notifica da archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="ea9f9-113">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="ea9f9-113">Considerations</span></span>
<span data-ttu-id="ea9f9-114">Quando si sviluppano applicazioni di Servizi multimediali che usano l'archiviazione code, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ea9f9-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="ea9f9-115">Il servizio di archiviazione code non garantisce un recapito ordinato dei messaggi di tipo FIFO (First-In-First-Out).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="ea9f9-116">Per altre informazioni, vedere [Analogie e differenze tra le code di Azure e le code del bus di servizio](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="ea9f9-117">Archiviazione code non è un servizio di push.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-117">Queue storage is not a push service.</span></span> <span data-ttu-id="ea9f9-118">È necessario eseguire il polling della coda.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-118">You have to poll the queue.</span></span>
* <span data-ttu-id="ea9f9-119">È possibile disporre di un qualsiasi numero di code.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-119">You can have any number of queues.</span></span> <span data-ttu-id="ea9f9-120">Per altre informazioni, vedere [API REST del servizio di accodamento](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="ea9f9-121">Archiviazione code presenta alcune limitazioni e specifiche da tenere presenti.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="ea9f9-122">Queste sono descritte in [Analogie e differenze tra le code di Azure e le code del bus di servizio di Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="ea9f9-123">Esempio di codice .NET</span><span class="sxs-lookup"><span data-stu-id="ea9f9-123">.NET code example</span></span>

<span data-ttu-id="ea9f9-124">L'esempio di codice contenuto in questa sezione effettua quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ea9f9-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="ea9f9-125">Definisce la classe **EncodingJobMessage** che esegue il mapping al formato del messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="ea9f9-126">Il codice deserializza i messaggi ricevuti dalla coda in oggetti del tipo **EncodingJobMessage** .</span><span class="sxs-lookup"><span data-stu-id="ea9f9-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="ea9f9-127">Carica informazioni sugli account di Servizi multimediali e di archiviazione dal file app.config</span><span class="sxs-lookup"><span data-stu-id="ea9f9-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="ea9f9-128">La coda di esempio usa queste informazioni per creare gli oggetti **CloudMediaContext** e **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="ea9f9-129">Crea la coda che riceve i messaggi di notifica relativi al processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="ea9f9-130">Crea l'endpoint di notifica di cui viene eseguito il mapping alla coda.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="ea9f9-131">Collega l'endpoint di notifica al processo e invia il processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="ea9f9-132">A un processo possono essere collegati anche più endpoint di notifica.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="ea9f9-133">Passa **NotificationJobState.FinalStatesOnly** al metodo **AddNew**.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="ea9f9-134">(In questo esempio vanno notati solo gli stati finali dell'elaborazione dei processi.)</span><span class="sxs-lookup"><span data-stu-id="ea9f9-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="ea9f9-135">Se si passa **NotificationJobState.All**, si ricevono tutte le notifiche di modifica dello stato: in coda, pianificate, in elaborazione e completate.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="ea9f9-136">Tuttavia, come indicato in precedenza, il servizio di archiviazione code non garantisce un recapito ordinato.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="ea9f9-137">Per ordinare i messaggi, usare la proprietà **Timestamp** (definita nel tipo **EncodingJobMessage** nell'esempio seguente).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="ea9f9-138">Sono possibili i messaggi duplicati.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-138">Duplicate messages are possible.</span></span> <span data-ttu-id="ea9f9-139">Per verificare la presenza di duplicati, usare la **proprietà ETag** (definita nel tipo **EncodingJobMessage**).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="ea9f9-140">È possibile inoltre che alcune notifiche di modifica dello stato vengano ignorate.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="ea9f9-141">Attende che il processo abbia raggiunto lo stato Completato controllando la coda ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="ea9f9-142">Elimina i messaggi man mano che vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="ea9f9-143">Elimina la coda e l'endpoint di notifica.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9f9-144">Il modo migliore per monitorare lo stato di un processo è quello di ascoltare i messaggi di notifica, come illustrato nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="ea9f9-145">In alternativa, è possibile controllare lo stato di un processo usando la proprietà **IJob.State** .</span><span class="sxs-lookup"><span data-stu-id="ea9f9-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="ea9f9-146">Un messaggio di notifica relativo al completamento del processo potrebbe essere ricevuto prima che lo stato in **IJob** sia impostato su **Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="ea9f9-147">La proprietà **IJob.State** riflette lo stato esatto con un leggero ritardo.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ea9f9-148">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea9f9-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="ea9f9-149">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ea9f9-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="ea9f9-150">Creare una nuova cartella, in un punto qualsiasi nell'unità locale, e copiare un file con estensione mp4 di cui eseguire codifica e streaming o il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="ea9f9-151">In questo esempio viene usato il percorso "C:\Media".</span><span class="sxs-lookup"><span data-stu-id="ea9f9-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="ea9f9-152">Codice</span><span class="sxs-lookup"><span data-stu-id="ea9f9-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want to get messages from the queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display the message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete the message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="ea9f9-153">Il precedente esempio ha prodotto l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-153">The preceding example produced the following output.</span></span> <span data-ttu-id="ea9f9-154">I valori possono variare.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="ea9f9-155">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="ea9f9-155">Next step</span></span>
<span data-ttu-id="ea9f9-156">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ea9f9-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ea9f9-157">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ea9f9-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
