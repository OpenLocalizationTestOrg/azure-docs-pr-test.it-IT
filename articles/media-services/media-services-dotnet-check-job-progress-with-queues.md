---
title: aaaUse coda di Azure storage toomonitor servizi multimediali notifiche dei processi con .NET | Documenti Microsoft
description: Informazioni su come le notifiche del processo toouse coda di Azure storage toomonitor servizi multimediali. Nell'esempio di codice Hello viene scritto in c# e utilizza hello Media Services SDK per .NET.
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
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="4179b-104">Utilizzare le notifiche processo della coda di Azure storage toomonitor servizi multimediali con .NET</span><span class="sxs-lookup"><span data-stu-id="4179b-104">Use Azure Queue storage toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="4179b-105">Quando si eseguono i processi di codifica, spesso richiedono un avanzamento del processo tootrack modo.</span><span class="sxs-lookup"><span data-stu-id="4179b-105">When you run encoding jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="4179b-106">È possibile configurare le notifiche di servizi multimediali toodeliver troppo[l'archiviazione delle code di Azure](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4179b-106">You can configure Media Services toodeliver notifications too[Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="4179b-107">È possibile monitorare lo stato del processo per ottenere notifiche da hello l'archiviazione delle code.</span><span class="sxs-lookup"><span data-stu-id="4179b-107">You can monitor job progress by getting notifications from hello Queue storage.</span></span> 

<span data-ttu-id="4179b-108">I messaggi recapitati tooQueue archiviazione è possibile accedere da qualsiasi in HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="4179b-108">Messages delivered tooQueue storage can be accessed from anywhere in hello world.</span></span> <span data-ttu-id="4179b-109">architettura di messaggistica di coda archiviazione Hello è altamente scalabile e affidabile.</span><span class="sxs-lookup"><span data-stu-id="4179b-109">hello Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="4179b-110">Tra i vari metodi disponibili è preferibile usare il polling dell'archiviazione code per i messaggi.</span><span class="sxs-lookup"><span data-stu-id="4179b-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="4179b-111">Uno scenario comune per le notifiche di servizi in ascolto tooMedia è se si sta sviluppando un sistema di gestione dei contenuti che necessita di tooperform completamento alcune attività aggiuntive dopo un processo di codifica (ad esempio, tootrigger hello passaggio successivo, un flusso di lavoro o toopublish contenuto).</span><span class="sxs-lookup"><span data-stu-id="4179b-111">One common scenario for listening tooMedia Services notifications is if you are developing a content management system that needs tooperform some additional task after an encoding job completes (for example, tootrigger hello next step in a workflow, or toopublish content).</span></span>

<span data-ttu-id="4179b-112">Questo argomento viene illustrato come i messaggi di notifica tooget dall'archiviazione di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="4179b-112">This topic shows how tooget notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="4179b-113">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="4179b-113">Considerations</span></span>
<span data-ttu-id="4179b-114">Considerare i seguenti hello durante lo sviluppo di applicazioni di servizi multimediali che usano l'archiviazione delle code:</span><span class="sxs-lookup"><span data-stu-id="4179b-114">Consider hello following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="4179b-115">Il servizio di archiviazione code non garantisce un recapito ordinato dei messaggi di tipo FIFO (First-In-First-Out).</span><span class="sxs-lookup"><span data-stu-id="4179b-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="4179b-116">Per altre informazioni, vedere [Analogie e differenze tra le code di Azure e le code del bus di servizio](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="4179b-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="4179b-117">Archiviazione code non è un servizio di push.</span><span class="sxs-lookup"><span data-stu-id="4179b-117">Queue storage is not a push service.</span></span> <span data-ttu-id="4179b-118">È necessario coda hello toopoll.</span><span class="sxs-lookup"><span data-stu-id="4179b-118">You have toopoll hello queue.</span></span>
* <span data-ttu-id="4179b-119">È possibile disporre di un qualsiasi numero di code.</span><span class="sxs-lookup"><span data-stu-id="4179b-119">You can have any number of queues.</span></span> <span data-ttu-id="4179b-120">Per altre informazioni, vedere [API REST del servizio di accodamento](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="4179b-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="4179b-121">L'archiviazione delle code con alcune limitazioni e le specifiche toobe comunicata.</span><span class="sxs-lookup"><span data-stu-id="4179b-121">Queue storage has some limitations and specifics toobe aware of.</span></span> <span data-ttu-id="4179b-122">Queste sono descritte in [Analogie e differenze tra le code di Azure e le code del bus di servizio di Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="4179b-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="4179b-123">Esempio di codice .NET</span><span class="sxs-lookup"><span data-stu-id="4179b-123">.NET code example</span></span>

<span data-ttu-id="4179b-124">esempio di codice Hello in questa sezione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4179b-124">hello code example in this section does hello following:</span></span>

1. <span data-ttu-id="4179b-125">Definisce hello **EncodingJobMessage** classe che esegue il mapping di formato di messaggio di notifica toohello.</span><span class="sxs-lookup"><span data-stu-id="4179b-125">Defines hello **EncodingJobMessage** class that maps toohello notification message format.</span></span> <span data-ttu-id="4179b-126">codice Hello deserializza i messaggi ricevuti dalla coda hello in oggetti di hello **EncodingJobMessage** tipo.</span><span class="sxs-lookup"><span data-stu-id="4179b-126">hello code deserializes messages received from hello queue into objects of hello **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="4179b-127">Carica hello servizi multimediali e le informazioni sull'account di archiviazione dal file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="4179b-127">Loads hello Media Services and Storage account information from hello app.config file.</span></span> <span data-ttu-id="4179b-128">esempio di codice Hello utilizza questo hello toocreate informazioni **CloudMediaContext** e **CloudQueue** oggetti.</span><span class="sxs-lookup"><span data-stu-id="4179b-128">hello code example uses this information toocreate hello **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="4179b-129">Crea coda hello che riceve i messaggi di notifica su hello processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="4179b-129">Creates hello queue that receives notification messages about hello encoding job.</span></span>
4. <span data-ttu-id="4179b-130">Crea punto di fine è stato eseguito il mapping di coda toohello notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="4179b-130">Creates hello notification end point that is mapped toohello queue.</span></span>
5. <span data-ttu-id="4179b-131">Allega processo toohello punto finale di notifica hello e invia i processi di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="4179b-131">Attaches hello notification end point toohello job and submits hello encoding job.</span></span> <span data-ttu-id="4179b-132">È possibile avere più processo tooa punti di fine associati di notifica.</span><span class="sxs-lookup"><span data-stu-id="4179b-132">You can have multiple notification end points attached tooa job.</span></span>
6. <span data-ttu-id="4179b-133">Passa **NotificationJobState.FinalStatesOnly** toohello **AddNew** metodo.</span><span class="sxs-lookup"><span data-stu-id="4179b-133">Passes **NotificationJobState.FinalStatesOnly** toohello **AddNew** method.</span></span> <span data-ttu-id="4179b-134">(In questo esempio, si intende solo stato finale di elaborazione dei processi di hello.)</span><span class="sxs-lookup"><span data-stu-id="4179b-134">(In this example, we are only interested in final states of hello job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="4179b-135">Se si passa **NotificationJobState.All**, ottenere tutti hello seguendo le notifiche di modifica dello stato: in coda, pianificato, elaborazione e terminato.</span><span class="sxs-lookup"><span data-stu-id="4179b-135">If you pass **NotificationJobState.All**, you get all of hello following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="4179b-136">Tuttavia, come indicato in precedenza, il servizio di archiviazione code non garantisce un recapito ordinato.</span><span class="sxs-lookup"><span data-stu-id="4179b-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="4179b-137">i messaggi tooorder, utilizzare hello **Timestamp** proprietà (definito in hello **EncodingJobMessage** tipo nel seguente esempio hello).</span><span class="sxs-lookup"><span data-stu-id="4179b-137">tooorder messages, use hello **Timestamp** property (defined on hello **EncodingJobMessage** type in hello example below).</span></span> <span data-ttu-id="4179b-138">Sono possibili i messaggi duplicati.</span><span class="sxs-lookup"><span data-stu-id="4179b-138">Duplicate messages are possible.</span></span> <span data-ttu-id="4179b-139">toocheck dei duplicati, utilizzare hello **proprietà ETag** (definito in hello **EncodingJobMessage** tipo).</span><span class="sxs-lookup"><span data-stu-id="4179b-139">toocheck for duplicates, use hello **ETag property** (defined on hello **EncodingJobMessage** type).</span></span> <span data-ttu-id="4179b-140">È possibile inoltre che alcune notifiche di modifica dello stato vengano ignorate.</span><span class="sxs-lookup"><span data-stu-id="4179b-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="4179b-141">Attende hello processo tooget toohello completata stato controllando coda hello ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4179b-141">Waits for hello job tooget toohello finished state by checking hello queue every 10 seconds.</span></span> <span data-ttu-id="4179b-142">Elimina i messaggi man mano che vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="4179b-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="4179b-143">Elimina coda hello e hello notifica finale.</span><span class="sxs-lookup"><span data-stu-id="4179b-143">Deletes hello queue and hello notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="4179b-144">Hello toomonitor consigliata che dello stato di un processo è in ascolto toonotification messaggi, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="4179b-144">hello recommended way toomonitor a job’s state is by listening toonotification messages, as shown in hello following example.</span></span>
>
> <span data-ttu-id="4179b-145">In alternativa, è possibile verificare sullo stato di un processo utilizzando hello **IJob.State** proprietà.</span><span class="sxs-lookup"><span data-stu-id="4179b-145">Alternatively, you could check on a job’s state by using hello **IJob.State** property.</span></span>  <span data-ttu-id="4179b-146">Un messaggio di notifica sul completamento di un processo può arrivare prima stato hello in **IJob** è troppo**completato**.</span><span class="sxs-lookup"><span data-stu-id="4179b-146">A notification message about a job’s completion may arrive before hello state on **IJob** is set too**Finished**.</span></span> <span data-ttu-id="4179b-147">Hello **IJob.State** proprietà riflette lo stato di accurate hello con un leggero ritardo.</span><span class="sxs-lookup"><span data-stu-id="4179b-147">hello **IJob.State**  property reflects hello accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4179b-148">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4179b-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4179b-149">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4179b-149">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="4179b-150">Creare una nuova cartella (cartella può essere un punto qualsiasi nell'unità locale) e copiare un file MP4 che si desidera tooencode e flusso o il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="4179b-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="4179b-151">In questo esempio viene utilizzato il percorso di "C:\Media" hello.</span><span class="sxs-lookup"><span data-stu-id="4179b-151">In this example, hello "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="4179b-152">Codice</span><span class="sxs-lookup"><span data-stu-id="4179b-152">Code</span></span>

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

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
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

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
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

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
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
                // Specify how often you want tooget messages from hello queue.
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

                        // Display hello message information.
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
                    // Delete hello message after we've read it.
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
<span data-ttu-id="4179b-153">Hello precedente hello di esempio prodotto dopo l'output.</span><span class="sxs-lookup"><span data-stu-id="4179b-153">hello preceding example produced hello following output.</span></span> <span data-ttu-id="4179b-154">I valori possono variare.</span><span class="sxs-lookup"><span data-stu-id="4179b-154">Your values will vary.</span></span>

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
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="4179b-155">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="4179b-155">Next step</span></span>
<span data-ttu-id="4179b-156">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="4179b-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4179b-157">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4179b-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
