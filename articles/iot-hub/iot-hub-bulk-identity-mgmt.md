---
title: "Importare o esportare le identità dei dispositivi dell'hub IoT di Azure | Microsoft Docs"
description: "Come usare Azure IoT SDK per servizi per eseguire operazioni in blocco sul registro delle identità per importare ed esportare le identità dei dispositivi. Le operazioni di importazione consentono di creare, aggiornare ed eliminare in blocco le identità dei dispositivi."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="9bc45-104">Gestire in blocco le identità dei dispositivi dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="9bc45-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="9bc45-105">Ogni hub IoT ha un registro delle identità che è possibile usare per creare le risorse per ogni dispositivo nel servizio.</span><span class="sxs-lookup"><span data-stu-id="9bc45-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="9bc45-106">e per consentire di controllare gli accessi agli endpoint per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="9bc45-107">Questo articolo descrive come importare ed esportare in blocco le identità del dispositivo in/da un registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="9bc45-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="9bc45-108">Le operazioni di importazione ed esportazione vengono eseguite nel contesto di *processi* che consentono di eseguire operazioni del servizio in blocco a fronte di un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9bc45-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="9bc45-109">La classe **RegistryManager** include i metodi **ExportDevicesAsync** e **ImportDevicesAsync** che usano il framework di **processi**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="9bc45-110">Questi metodi consentono di esportare, importare e sincronizzare un intero registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9bc45-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="9bc45-111">Informazioni sui processi</span><span class="sxs-lookup"><span data-stu-id="9bc45-111">What are jobs?</span></span>

<span data-ttu-id="9bc45-112">Le operazioni del registro delle identità usano il sistema di gestione dei **processi** quando l'operazione:</span><span class="sxs-lookup"><span data-stu-id="9bc45-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="9bc45-113">Ha un tempo di esecuzione potenzialmente lungo rispetto alle operazioni di runtime standard.</span><span class="sxs-lookup"><span data-stu-id="9bc45-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="9bc45-114">Restituisce all'utente una grande quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="9bc45-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="9bc45-115">Invece di avere una singola chiamata API in attesa o che blocca il risultato dell'operazione, quest'ultima crea in modo asincrono un **processo** per tale hub IoT,</span><span class="sxs-lookup"><span data-stu-id="9bc45-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="9bc45-116">quindi restituisce immediatamente un oggetto **JobProperties**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="9bc45-117">Il frammento di codice C# seguente mostra come creare un processo di esportazione:</span><span class="sxs-lookup"><span data-stu-id="9bc45-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="9bc45-118">Per usare la classe il **RegistryManager** nel codice c#, aggiungere il pacchetto NuGet **Microsoft.Azure.Devices** al progetto.</span><span class="sxs-lookup"><span data-stu-id="9bc45-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="9bc45-119">La classe **RegistryManager** si trova nello spazio dei nomi **Microsoft.Azure.Devices**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="9bc45-120">È possibile usare la classe **RegistryManager** per eseguire query sullo stato del **processo** usando i metadati di **JobProperties** restituiti.</span><span class="sxs-lookup"><span data-stu-id="9bc45-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="9bc45-121">Il frammento di codice C# seguente mostra come eseguire il polling ogni cinque secondi per vedere se il processo ha terminato l'esecuzione:</span><span class="sxs-lookup"><span data-stu-id="9bc45-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="9bc45-122">Esportare dispositivi</span><span class="sxs-lookup"><span data-stu-id="9bc45-122">Export devices</span></span>

<span data-ttu-id="9bc45-123">Usare il metodo **ExportDevicesAsync** per esportare un intero registro delle identità di un hub IoT in un contenitore BLOB di [Archiviazione di Azure](../storage/index.md) con una [firma di accesso condiviso](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="9bc45-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="9bc45-124">Questo metodo consente di creare backup affidabili delle informazioni sui dispositivi in un contenitore BLOB che si controlla.</span><span class="sxs-lookup"><span data-stu-id="9bc45-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="9bc45-125">Il metodo **ExportDevicesAsync** richiede due parametri:</span><span class="sxs-lookup"><span data-stu-id="9bc45-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="9bc45-126">Una *stringa* che contiene un URI di un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="9bc45-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="9bc45-127">Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in scrittura al contenitore.</span><span class="sxs-lookup"><span data-stu-id="9bc45-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="9bc45-128">Il processo crea un BLOB in blocchi in questo contenitore per archiviare i dati di esportazione del dispositivo serializzati.</span><span class="sxs-lookup"><span data-stu-id="9bc45-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="9bc45-129">Il token di firma di accesso condiviso deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="9bc45-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="9bc45-130">Oggetto *booleano* che indica se si vogliono escludere le chiavi di autenticazione dai dati di esportazione.</span><span class="sxs-lookup"><span data-stu-id="9bc45-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="9bc45-131">Se il valore è **false**, le chiavi di autenticazione sono incluse nell'output di esportazione.</span><span class="sxs-lookup"><span data-stu-id="9bc45-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="9bc45-132">In caso contrario, le chiavi vengono esportate come **null**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="9bc45-133">I frammenti di codice C# seguenti illustrano come inizializzare un processo di esportazione che include chiavi di autenticazione di dispositivi nei dati di esportazione e quindi eseguire il polling del completamento:</span><span class="sxs-lookup"><span data-stu-id="9bc45-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="9bc45-134">Il processo archivia l'output nel contenitore BLOB specificato come BLOB in blocchi con il nome **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="9bc45-135">I dati di output sono costituiti da dati del dispositivo serializzati in formato JSON, con un dispositivo per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="9bc45-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="9bc45-136">Nell'esempio seguente vengono descritti i dati di output:</span><span class="sxs-lookup"><span data-stu-id="9bc45-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se un dispositivo contiene dati gemelli, allora anche i dati gemelli vengono esportati con i dati del dispositivo. Questo formato è illustrato nell'esempio seguente. <span data-ttu-id="9bc45-139">Tutti i dati dalla riga di "twinETag" fino alla fine sono dati gemelli.</span><span class="sxs-lookup"><span data-stu-id="9bc45-139">All data from the "twinETag" line until the end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="9bc45-140">Se è necessario accedere ai dati nel codice, è possibile deserializzarli facilmente con la classe **ExportImportDevice** .</span><span class="sxs-lookup"><span data-stu-id="9bc45-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="9bc45-141">Il frammento di codice C# seguente mostra come leggere le informazioni sul dispositivo esportate precedentemente in un BLOB in blocchi:</span><span class="sxs-lookup"><span data-stu-id="9bc45-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="9bc45-142">È anche possibile usare il metodo **GetDevicesAsync** della classe **RegistryManager** per recuperare un elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9bc45-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="9bc45-143">Questo approccio presenta tuttavia un limite rigido pari a un numero di 1000 oggetti dispositivo restituiti.</span><span class="sxs-lookup"><span data-stu-id="9bc45-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="9bc45-144">Il caso d'uso previsto per il metodo **GetDevicesAsync** è destinato a scenari di sviluppo per facilitare il debug e non è consigliabile per i carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="9bc45-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="9bc45-145">Importare dispositivi</span><span class="sxs-lookup"><span data-stu-id="9bc45-145">Import devices</span></span>

<span data-ttu-id="9bc45-146">Il metodo **ImportDevicesAsync** nella classe **RegistryManager** consente di eseguire operazioni di importazione e sincronizzazione in blocco nel registro delle identità di un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9bc45-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="9bc45-147">In modo analogo al metodo **ExportDevicesAsync**, il metodo **ImportDevicesAsync** usa il framework **Job**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="9bc45-148">Prestare attenzione quando si usa il metodo **ImportDevicesAsync** in quanto, oltre a eseguire il provisioning dei dispositivi nuovi nel registro delle identità, può anche aggiornare ed eliminare dispositivi esistenti.</span><span class="sxs-lookup"><span data-stu-id="9bc45-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="9bc45-149">Un'operazione di importazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="9bc45-149">An import operation cannot be undone.</span></span> <span data-ttu-id="9bc45-150">Eseguire sempre il backup dei dati esistenti usando il metodo **ExportDevicesAsync** in un altro contenitore BLOB, prima di apportare modifiche in blocco al registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="9bc45-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="9bc45-151">Il metodo **ImportDevicesAsync** usa due parametri:</span><span class="sxs-lookup"><span data-stu-id="9bc45-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="9bc45-152">Una *stringa* che contiene un URI di un contenitore BLOB di [Archiviazione di Azure](../storage/index.md) come *input* del processo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="9bc45-153">Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in lettura al contenitore.</span><span class="sxs-lookup"><span data-stu-id="9bc45-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="9bc45-154">Questo contenitore deve includere un BLOB con il nome **devices.txt** che contiene i dati serializzati del dispositivo da importare nel registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="9bc45-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="9bc45-155">I dati di importazione devono contenere informazioni sul dispositivo nello stesso formato JSON usato dal processo **ExportImportDevice** quando viene creato il BLOB **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="9bc45-156">Il token di firma di accesso condiviso deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="9bc45-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="9bc45-157">Una *stringa* che contiene un URI di un contenitore BLOB di [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) da usare come *output* del processo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="9bc45-158">Il processo crea un BLOB in blocchi in questo contenitore per archiviare qualsiasi informazione sull'errore dal **processo**di importazione completato.</span><span class="sxs-lookup"><span data-stu-id="9bc45-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="9bc45-159">Il token di firma di accesso condiviso deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="9bc45-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="9bc45-160">I due parametri possono puntare allo stesso contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="9bc45-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="9bc45-161">I parametri separati consentono semplicemente un maggiore controllo dei dati, perché il contenitore di output richiede autorizzazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9bc45-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="9bc45-162">Il frammento di codice C# seguente mostra come avviare un processo di importazione:</span><span class="sxs-lookup"><span data-stu-id="9bc45-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="9bc45-163">Questo metodo può essere usato anche per importare i dati per il dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="9bc45-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="9bc45-164">Il formato per i dati di input è uguale al formato visualizzato nella sezione **ExportDevicesAsync**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="9bc45-165">In questo modo, è possibile reimportare i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="9bc45-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="9bc45-166">Il **$metadata** è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="9bc45-167">Importare il comportamento</span><span class="sxs-lookup"><span data-stu-id="9bc45-167">Import behavior</span></span>

<span data-ttu-id="9bc45-168">È possibile usare il metodo **ImportDevicesAsync** per eseguire le operazioni in blocco seguenti nel registro delle identità:</span><span class="sxs-lookup"><span data-stu-id="9bc45-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="9bc45-169">Registrazione in blocco di nuovi dispositivi</span><span class="sxs-lookup"><span data-stu-id="9bc45-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="9bc45-170">Eliminazioni in blocco dei dispositivi esistenti</span><span class="sxs-lookup"><span data-stu-id="9bc45-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="9bc45-171">Modifiche dello stato in blocco (abilitare o disabilitare dispositivi)</span><span class="sxs-lookup"><span data-stu-id="9bc45-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="9bc45-172">Assegnazione in blocco di nuove chiavi di autenticazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="9bc45-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="9bc45-173">Rigenerazione automatica in blocco di chiavi di autenticazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="9bc45-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="9bc45-174">Aggiornamento bulk dei dati gemelli</span><span class="sxs-lookup"><span data-stu-id="9bc45-174">Bulk update of twin data</span></span>

<span data-ttu-id="9bc45-175">È possibile eseguire una combinazione qualsiasi delle operazioni precedenti in un'unica chiamata **ImportDevicesAsync** .</span><span class="sxs-lookup"><span data-stu-id="9bc45-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="9bc45-176">Ad esempio, è possibile registrare nuovi dispositivi ed eliminare o aggiornare contemporaneamente quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="9bc45-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="9bc45-177">Insieme con il metodo **ExportDevicesAsync** , è possibile eseguire la migrazione completa di tutti i dispositivi da un hub IoT all'altro.</span><span class="sxs-lookup"><span data-stu-id="9bc45-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="9bc45-178">Se il file di importazione include metadati gemelli, questi metadati sovrascrivono i metadati gemelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="9bc45-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="9bc45-179">Se il file di importazione non include i metadati gemelli, allora solo i metadati `lastUpdateTime` vengono aggiornati usando l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="9bc45-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="9bc45-180">Usare la proprietà facoltativa **importMode** nei dati di serializzazione dell'importazione per ogni dispositivo per controllare il processo di importazione per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="9bc45-181">La proprietà **importMode** include le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9bc45-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="9bc45-182">importMode</span><span class="sxs-lookup"><span data-stu-id="9bc45-182">importMode</span></span> | <span data-ttu-id="9bc45-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9bc45-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9bc45-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="9bc45-184">**createOrUpdate**</span></span> |<span data-ttu-id="9bc45-185">Se non esiste un dispositivo con l' **ID**specificato, viene registrato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9bc45-186">Se il dispositivo esiste già, le informazioni esistenti vengono sovrascritte con i dati di input specificati senza tener conto del valore **ETag** .</span><span class="sxs-lookup"><span data-stu-id="9bc45-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="9bc45-187">L'utente può facoltativamente specificare i dati gemelli con i dati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="9bc45-188">L'ETag del gemello, se specificato, viene elaborato in modo indipendente dal valore etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="9bc45-189">Se è presente una mancata corrispondenza con l'etag del gemello esistente, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-190">**create**</span><span class="sxs-lookup"><span data-stu-id="9bc45-190">**create**</span></span> |<span data-ttu-id="9bc45-191">Se non esiste un dispositivo con l' **ID**specificato, viene registrato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9bc45-192">Se il dispositivo esiste già, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="9bc45-193">L'utente può facoltativamente specificare i dati gemelli con i dati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="9bc45-194">L'ETag del gemello, se specificato, viene elaborato in modo indipendente dal valore etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="9bc45-195">Se è presente una mancata corrispondenza con l'etag del gemello esistente, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-196">**update**</span><span class="sxs-lookup"><span data-stu-id="9bc45-196">**update**</span></span> |<span data-ttu-id="9bc45-197">Se esiste già un dispositivo con l'**ID** specificato, le informazioni esistenti vengono sovrascritte con i dati di input specificati senza tener conto del valore **ETag**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="9bc45-198">Se il dispositivo non esiste, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9bc45-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="9bc45-200">Se esiste già un dispositivo con l'**ID** specificato, le informazioni esistenti vengono sovrascritte con i dati di input specificati solo se viene rilevata una corrispondenza con **ETag**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="9bc45-201">Se il dispositivo non esiste, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="9bc45-202">In caso di mancata corrispondenza con **ETag** , viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9bc45-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="9bc45-204">Se non esiste un dispositivo con l' **ID**specificato, viene registrato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9bc45-205">Se il dispositivo esiste già, le informazioni esistenti vengono sovrascritte con i dati di input specificati solo se viene rilevata una corrispondenza con **ETag** .</span><span class="sxs-lookup"><span data-stu-id="9bc45-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="9bc45-206">In caso di mancata corrispondenza con **ETag** , viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="9bc45-207">L'utente può facoltativamente specificare i dati gemelli con i dati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="9bc45-208">L'ETag del gemello, se specificato, viene elaborato in modo indipendente dal valore etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bc45-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="9bc45-209">Se è presente una mancata corrispondenza con l'etag del gemello esistente, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="9bc45-210">**delete**</span></span> |<span data-ttu-id="9bc45-211">Se esiste già un dispositivo con l'**ID** specificato, viene eliminato senza tener conto del valore **ETag**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="9bc45-212">Se il dispositivo non esiste, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="9bc45-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9bc45-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="9bc45-214">Se esiste già un dispositivo con l'**ID** specificato, viene eliminato solo se viene rilevata una corrispondenza con **ETag**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="9bc45-215">Se il dispositivo non esiste, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="9bc45-216">In caso di mancata corrispondenza con ETag, viene scritto un errore nel file di log.</span><span class="sxs-lookup"><span data-stu-id="9bc45-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="9bc45-217">Se i dati di serializzazione non definiscono in modo esplicito un flag **importMode** per un dispositivo, durante l'operazione di importazione l'impostazione predefinita è **createOrUpdate**.</span><span class="sxs-lookup"><span data-stu-id="9bc45-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="9bc45-218">Importare dispositivi: esempio di provisioning dei dispositivi in blocco</span><span class="sxs-lookup"><span data-stu-id="9bc45-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="9bc45-219">Il campione di codice C# seguente illustra come generare più identità dei dispositivi che:</span><span class="sxs-lookup"><span data-stu-id="9bc45-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="9bc45-220">Includono chiavi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9bc45-220">Include authentication keys.</span></span>
* <span data-ttu-id="9bc45-221">Scrivono le informazioni del dispositivo in un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="9bc45-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="9bc45-222">Importano i dispositivi nel registro delle identità.</span><span class="sxs-lookup"><span data-stu-id="9bc45-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="9bc45-223">Importare dispositivi: esempio di eliminazione in blocco</span><span class="sxs-lookup"><span data-stu-id="9bc45-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="9bc45-224">L'esempio di codice seguente illustra come eliminare i dispositivi aggiunti con l'esempio di codice precedente:</span><span class="sxs-lookup"><span data-stu-id="9bc45-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using the same blob to delete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="9bc45-225">Recuperare l'URI di firma di accesso condiviso del contenitore</span><span class="sxs-lookup"><span data-stu-id="9bc45-225">Get the container SAS URI</span></span>

<span data-ttu-id="9bc45-226">Il codice di esempio seguente illustra come generare un [URI di firma di accesso condiviso](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con autorizzazioni di lettura, scrittura ed eliminazione per un contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="9bc45-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="9bc45-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bc45-227">Next steps</span></span>

<span data-ttu-id="9bc45-228">In questo articolo si è appreso come eseguire operazioni in blocco sul registro delle identità in un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9bc45-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="9bc45-229">Per ulteriori informazioni sulla gestione dell'hub IoT di Azure, consultare questi collegamenti:</span><span class="sxs-lookup"><span data-stu-id="9bc45-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="9bc45-230">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="9bc45-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="9bc45-231">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="9bc45-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="9bc45-232">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="9bc45-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9bc45-233">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="9bc45-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="9bc45-234">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9bc45-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
