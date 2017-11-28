---
title: "esportazione aaaImport delle identità del dispositivo IoT Hub di Azure | Documenti Microsoft"
description: "Come toouse hello Azure IoT servizio SDK tooperform operazioni tooimport del Registro di sistema di identità hello ed esportazione bulk le identità del dispositivo. Operazioni di importazione consentono di toocreate, update e delete le identità del dispositivo in blocco."
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
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="ef0bd-104">Gestire in blocco le identità dei dispositivi dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="ef0bd-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="ef0bd-105">Ogni hub IoT è un registro di sistema di identità è possibile utilizzare le risorse per ogni dispositivo toocreate nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="ef0bd-106">Registro di identità Hello consente inoltre di endpoint che utilizzano il dispositivo di toocontrol accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="ef0bd-107">In questo articolo viene descritto come identità del dispositivo tooimport e di esportazione in blocco tooand da un registro di sistema di identità.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="ef0bd-108">Eseguire operazioni di importazione ed esportazione nel contesto di hello di *processi* che consentono operazioni di servizio tooexecute bulk su un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="ef0bd-109">Hello **RegistryManager** classe include hello **ExportDevicesAsync** e **ImportDevicesAsync** metodi che utilizzano hello **processo** Framework.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="ef0bd-110">Questi metodi consentono di tooexport, importazione e sincronizzare interamente hello di un registro di identità hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="ef0bd-111">Informazioni sui processi</span><span class="sxs-lookup"><span data-stu-id="ef0bd-111">What are jobs?</span></span>

<span data-ttu-id="ef0bd-112">Le operazioni del Registro di sistema di identità di hello **processo** sistema hello quando l'operazione:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="ef0bd-113">È un tempo di esecuzione potrebbe richiedere alcuni minuto confrontata toostandard operazioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="ef0bd-114">Restituisce una grande quantità di utente toohello di dati.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="ef0bd-115">Anziché una singola chiamata API in attesa o blocchi nel risultato hello dell'operazione di hello, operazione hello crea in modo asincrono un **processo** per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="ef0bd-116">l'operazione di Hello quindi immediatamente restituisce un **JobProperties** oggetto.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="ef0bd-117">Hello seguente c# codice frammento di codice viene illustrato come toocreate un processo di esportazione:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="ef0bd-118">hello toouse **RegistryManager** classe nel codice c#, aggiungere hello **Microsoft.Azure.Devices** progetto tooyour di pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="ef0bd-119">Hello **RegistryManager** classe si trova in hello **Microsoft.Azure.Devices** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="ef0bd-120">È possibile utilizzare hello **RegistryManager** classe hello stato hello tooquery **processo** utilizzando hello restituito **JobProperties** metadati.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="ef0bd-121">Hello seguente frammento di codice c# viene illustrato come toopoll toosee ogni cinque secondi se hello processo ha terminato l'esecuzione:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="ef0bd-122">Esportare dispositivi</span><span class="sxs-lookup"><span data-stu-id="ef0bd-122">Export devices</span></span>

<span data-ttu-id="ef0bd-123">Hello utilizzare **ExportDevicesAsync** metodo tooexport hello intera un tooan del Registro di sistema di IoT hub identità [di archiviazione di Azure](../storage/index.md) contenitore blob utilizzando un [firma di accesso condiviso](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="ef0bd-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="ef0bd-124">Questo metodo consente toocreate backup affidabile dei dati personali dispositivo in un contenitore blob che è possibile controllare.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="ef0bd-125">Hello **ExportDevicesAsync** metodo richiede due parametri:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="ef0bd-126">Una *stringa* che contiene un URI di un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="ef0bd-127">Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in scrittura toohello contenitore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="ef0bd-128">il processo di Hello crea un blob in blocchi in questi dati di dispositivo contenitore toostore hello serializzato esportazione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="ef0bd-129">token SAS Hello deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="ef0bd-130">Oggetto *booleano* che indica se le chiavi di autenticazione tooexclude dai dati di esportazione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="ef0bd-131">Se il valore è **false**, le chiavi di autenticazione sono incluse nell'output di esportazione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="ef0bd-132">In caso contrario, le chiavi vengono esportate come **null**.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="ef0bd-133">Hello seguente frammento di codice c# viene illustrato un processo di esportazione che include le chiavi di autenticazione dispositivo in hello tooinitiate esportare i dati e quindi eseguire il polling per il completamento:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
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

<span data-ttu-id="ef0bd-134">Hello processo archivia l'output nel contenitore blob hello fornito come un blob in blocchi con nome hello **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="ef0bd-135">dati di output di Hello è costituito da dati del dispositivo JSON serializzato, con un dispositivo per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="ef0bd-136">Hello esempio seguente mostra i dati di output hello:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se un dispositivo ha dati doppi, dati doppi hello vengono esportati anche con i dati del dispositivo hello. Hello riportato di seguito in questo formato. <span data-ttu-id="ef0bd-139">Tutti i dati dalla riga di "twinETag" hello fino al fine di hello sono dati doppi.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

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

<span data-ttu-id="ef0bd-140">Se è necessario accedere a dati toothis nel codice, è possibile deserializzare facilmente i dati utilizzando hello **ExportImportDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="ef0bd-141">Hello seguente frammento di codice c# viene illustrato come informazioni sul dispositivo tooread che è stato esportato in precedenza tooa blob in blocchi:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

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
> <span data-ttu-id="ef0bd-142">È inoltre possibile utilizzare hello **GetDevicesAsync** metodo hello **RegistryManager** toofetch classe un elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="ef0bd-143">Tuttavia, questo approccio presenta un limite di 1000 numero hello degli oggetti dispositivo restituiti.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="ef0bd-144">Hello previsto caso d'uso per hello **GetDevicesAsync** metodo è per il debug tooaid gli scenari di sviluppo e non è consigliata per i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="ef0bd-145">Importare dispositivi</span><span class="sxs-lookup"><span data-stu-id="ef0bd-145">Import devices</span></span>

<span data-ttu-id="ef0bd-146">Hello **ImportDevicesAsync** metodo hello **RegistryManager** classe consente operazioni tooperform bulk importazione e la sincronizzazione in un registro di identità hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="ef0bd-147">Ad esempio hello **ExportDevicesAsync** (metodo), hello **ImportDevicesAsync** metodo utilizza hello **processo** framework.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="ef0bd-148">Prestare attenzione con hello **ImportDevicesAsync** metodo perché nel aggiunta tooprovisioning nuovi dispositivi al Registro di sistema di identità, anche possibile aggiornare ed eliminare dispositivi esistenti.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="ef0bd-149">Un'operazione di importazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-149">An import operation cannot be undone.</span></span> <span data-ttu-id="ef0bd-150">Eseguire sempre il backup dei dati esistenti utilizzando hello **ExportDevicesAsync** il contenitore blob tooanother metodo prima di apportare bulk modifica del Registro di sistema di tooyour identità.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="ef0bd-151">Hello **ImportDevicesAsync** metodo accetta due parametri:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="ef0bd-152">Oggetto *stringa* che contiene un URI di un [di archiviazione di Azure](../storage/index.md) blob toouse contenitore come *input* toohello processo.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="ef0bd-153">Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in lettura toohello contenitore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="ef0bd-154">Questo contenitore può contenere un blob con nome hello **devices.txt** hello serializzato dispositivo dati tooimport che contiene il Registro di sistema di identità.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="ef0bd-155">Hello l'importazione dei dati deve contenere informazioni sul dispositivo in hello JSON stesso formato di tale hello **ExportImportDevice** processo viene utilizzato quando viene creato un **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="ef0bd-156">token SAS Hello deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="ef0bd-157">Oggetto *stringa* che contiene un URI di un [di archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contenitore come *output* dal processo di hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="ef0bd-158">Hello processo crea un blob in blocchi in questo contenitore toostore eventuali informazioni sugli errori dall'importazione completata hello **processo**.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="ef0bd-159">token SAS Hello deve includere queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="ef0bd-160">i parametri di Hello due possono puntare toohello nello stesso contenitore di blob.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="ef0bd-161">parametri separati Hello semplicemente consentono maggiore controllo sui dati come contenitore dell'output hello richiede autorizzazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="ef0bd-162">Hello seguente c# codice frammento di codice viene illustrato come tooinitiate un processo di importazione:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="ef0bd-163">Questo metodo può essere anche usato tooimport hello dati per un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="ef0bd-164">formato di Hello per l'input di dati hello è hello stesso come formato di hello indicato in hello **ExportDevicesAsync** sezione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="ef0bd-165">In questo modo, è possibile reimportare dati hello esportata.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="ef0bd-166">Hello **$metadata** è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="ef0bd-167">Importare il comportamento</span><span class="sxs-lookup"><span data-stu-id="ef0bd-167">Import behavior</span></span>

<span data-ttu-id="ef0bd-168">È possibile utilizzare hello **ImportDevicesAsync** seguente di hello tooperform metodo bulk operazioni del Registro di identità:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="ef0bd-169">Registrazione in blocco di nuovi dispositivi</span><span class="sxs-lookup"><span data-stu-id="ef0bd-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="ef0bd-170">Eliminazioni in blocco dei dispositivi esistenti</span><span class="sxs-lookup"><span data-stu-id="ef0bd-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="ef0bd-171">Modifiche dello stato in blocco (abilitare o disabilitare dispositivi)</span><span class="sxs-lookup"><span data-stu-id="ef0bd-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="ef0bd-172">Assegnazione in blocco di nuove chiavi di autenticazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="ef0bd-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="ef0bd-173">Rigenerazione automatica in blocco di chiavi di autenticazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="ef0bd-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="ef0bd-174">Aggiornamento bulk dei dati gemelli</span><span class="sxs-lookup"><span data-stu-id="ef0bd-174">Bulk update of twin data</span></span>

<span data-ttu-id="ef0bd-175">È possibile eseguire qualsiasi combinazione di hello precedenti operazioni all'interno di un singolo **ImportDevicesAsync** chiamare.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="ef0bd-176">Ad esempio, è possibile registrare nuovi dispositivi ed eliminare o aggiornare i dispositivi esistenti in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="ef0bd-177">Quando utilizzato insieme a hello **ExportDevicesAsync** (metodo), è possibile migrare completamente tutti i dispositivi da una tooanother di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="ef0bd-178">Se il file di importazione hello include metadati doppi, questi metadati sovrascrive i metadati di un doppio esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="ef0bd-179">Se il file di importazione hello non include i metadati doppi, quindi solo hello `lastUpdateTime` vengono aggiornati i metadati utilizzando hello l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="ef0bd-180">Hello utilizzo facoltativo **importMode** proprietà nei dati di serializzazione hello importazione per ogni dispositivo toocontrol hello importazione processo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="ef0bd-181">Hello **importMode** proprietà ha hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="ef0bd-182">importMode</span><span class="sxs-lookup"><span data-stu-id="ef0bd-182">importMode</span></span> | <span data-ttu-id="ef0bd-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ef0bd-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef0bd-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-184">**createOrUpdate**</span></span> |<span data-ttu-id="ef0bd-185">Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="ef0bd-186">Se il dispositivo hello esiste già, informazioni esistente viene sovrascritto con hello fornito dati di input senza considerare toohello **ETag** valore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="ef0bd-187">utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="ef0bd-188">valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="ef0bd-189">Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-190">**create**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-190">**create**</span></span> |<span data-ttu-id="ef0bd-191">Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="ef0bd-192">Se il dispositivo hello esiste già, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="ef0bd-193">utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="ef0bd-194">valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="ef0bd-195">Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-196">**update**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-196">**update**</span></span> |<span data-ttu-id="ef0bd-197">Se esiste già un dispositivo con hello specificato **id**, informazioni esistente viene sovrascritto con hello fornito dati di input senza considerare toohello **ETag** valore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="ef0bd-198">Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="ef0bd-200">Se esiste già un dispositivo con hello specificato **id**, informazioni esistente viene sovrascritto con hello fornito dati di input solo se è presente un **ETag** corrispondono.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="ef0bd-201">Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="ef0bd-202">Se è presente un **ETag** mancata corrispondenza, viene scritto il file di log toohello un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="ef0bd-204">Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="ef0bd-205">Se il dispositivo hello esiste già, informazioni esistente viene sovrascritto con hello fornito dati di input solo se è presente un **ETag** corrispondono.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="ef0bd-206">Se è presente un **ETag** mancata corrispondenza, viene scritto il file di log toohello un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="ef0bd-207">utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="ef0bd-208">valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="ef0bd-209">Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-210">**delete**</span></span> |<span data-ttu-id="ef0bd-211">Se esiste già un dispositivo con hello specificato **id**, viene eliminato senza considerare toohello **ETag** valore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="ef0bd-212">Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="ef0bd-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="ef0bd-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="ef0bd-214">Se esiste già un dispositivo con hello specificato **id**, viene eliminato solo se è presente un **ETag** corrispondono.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="ef0bd-215">Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="ef0bd-216">Se è presente una mancata corrispondenza ETag, toohello file di log viene scritto un errore.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="ef0bd-217">Se i dati di serializzazione hello non definiscono in modo esplicito un **importMode** flag per un dispositivo, valore predefinito è troppo**createOrUpdate** hello durante l'operazione di importazione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="ef0bd-218">Importare dispositivi: esempio di provisioning dei dispositivi in blocco</span><span class="sxs-lookup"><span data-stu-id="ef0bd-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="ef0bd-219">Hello esempio c# di codice riportato di seguito viene illustrato come toogenerate più identità dispositivo che:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="ef0bd-220">Includono chiavi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-220">Include authentication keys.</span></span>
* <span data-ttu-id="ef0bd-221">Scrivere i blob in blocchi tooa informazioni tale dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="ef0bd-222">Importare i dispositivi di hello del Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
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

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
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

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="ef0bd-223">Importare dispositivi: esempio di eliminazione in blocco</span><span class="sxs-lookup"><span data-stu-id="ef0bd-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="ef0bd-224">Hello nell'esempio di codice seguente viene illustrato come dispositivi hello toodelete che aggiunti utilizzando hello esempio di codice precedente:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
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

// Step 3: Call import using hello same blob toodelete all devices
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

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="ef0bd-225">Ottenere il contenitore di hello URI SAS</span><span class="sxs-lookup"><span data-stu-id="ef0bd-225">Get hello container SAS URI</span></span>

<span data-ttu-id="ef0bd-226">Hello nell'esempio di codice seguente illustra come toogenerate un [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con lettura, scrittura ed eliminazione di autorizzazioni per un contenitore di blob:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="ef0bd-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef0bd-227">Next steps</span></span>

<span data-ttu-id="ef0bd-228">In questo articolo è stato descritto come tooperform bulk operazioni nel Registro di identità hello in un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef0bd-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="ef0bd-229">Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="ef0bd-230">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="ef0bd-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="ef0bd-231">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="ef0bd-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="ef0bd-232">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="ef0bd-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ef0bd-233">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ef0bd-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ef0bd-234">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ef0bd-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
