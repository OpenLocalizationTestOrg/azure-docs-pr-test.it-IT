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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Gestire in blocco le identità dei dispositivi dell'hub IoT

Ogni hub IoT è un registro di sistema di identità è possibile utilizzare le risorse per ogni dispositivo toocreate nel servizio hello. Registro di identità Hello consente inoltre di endpoint che utilizzano il dispositivo di toocontrol accesso toohello. In questo articolo viene descritto come identità del dispositivo tooimport e di esportazione in blocco tooand da un registro di sistema di identità.

Eseguire operazioni di importazione ed esportazione nel contesto di hello di *processi* che consentono operazioni di servizio tooexecute bulk su un hub IoT.

Hello **RegistryManager** classe include hello **ExportDevicesAsync** e **ImportDevicesAsync** metodi che utilizzano hello **processo** Framework. Questi metodi consentono di tooexport, importazione e sincronizzare interamente hello di un registro di identità hub IoT.

## <a name="what-are-jobs"></a>Informazioni sui processi

Le operazioni del Registro di sistema di identità di hello **processo** sistema hello quando l'operazione:

* È un tempo di esecuzione potrebbe richiedere alcuni minuto confrontata toostandard operazioni di runtime.
* Restituisce una grande quantità di utente toohello di dati.

Anziché una singola chiamata API in attesa o blocchi nel risultato hello dell'operazione di hello, operazione hello crea in modo asincrono un **processo** per l'hub IoT. l'operazione di Hello quindi immediatamente restituisce un **JobProperties** oggetto.

Hello seguente c# codice frammento di codice viene illustrato come toocreate un processo di esportazione:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> hello toouse **RegistryManager** classe nel codice c#, aggiungere hello **Microsoft.Azure.Devices** progetto tooyour di pacchetto NuGet. Hello **RegistryManager** classe si trova in hello **Microsoft.Azure.Devices** dello spazio dei nomi.

È possibile utilizzare hello **RegistryManager** classe hello stato hello tooquery **processo** utilizzando hello restituito **JobProperties** metadati.

Hello seguente frammento di codice c# viene illustrato come toopoll toosee ogni cinque secondi se hello processo ha terminato l'esecuzione:

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

## <a name="export-devices"></a>Esportare dispositivi

Hello utilizzare **ExportDevicesAsync** metodo tooexport hello intera un tooan del Registro di sistema di IoT hub identità [di archiviazione di Azure](../storage/index.md) contenitore blob utilizzando un [firma di accesso condiviso](../storage/common/storage-security-guide.md#data-plane-security).

Questo metodo consente toocreate backup affidabile dei dati personali dispositivo in un contenitore blob che è possibile controllare.

Hello **ExportDevicesAsync** metodo richiede due parametri:

* Una *stringa* che contiene un URI di un contenitore BLOB. Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in scrittura toohello contenitore. il processo di Hello crea un blob in blocchi in questi dati di dispositivo contenitore toostore hello serializzato esportazione. token SAS Hello deve includere queste autorizzazioni:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* Oggetto *booleano* che indica se le chiavi di autenticazione tooexclude dai dati di esportazione. Se il valore è **false**, le chiavi di autenticazione sono incluse nell'output di esportazione. In caso contrario, le chiavi vengono esportate come **null**.

Hello seguente frammento di codice c# viene illustrato un processo di esportazione che include le chiavi di autenticazione dispositivo in hello tooinitiate esportare i dati e quindi eseguire il polling per il completamento:

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

Hello processo archivia l'output nel contenitore blob hello fornito come un blob in blocchi con nome hello **devices.txt**. dati di output di Hello è costituito da dati del dispositivo JSON serializzato, con un dispositivo per ogni riga.

Hello esempio seguente mostra i dati di output hello:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se un dispositivo ha dati doppi, dati doppi hello vengono esportati anche con i dati del dispositivo hello. Hello riportato di seguito in questo formato. Tutti i dati dalla riga di "twinETag" hello fino al fine di hello sono dati doppi.

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

Se è necessario accedere a dati toothis nel codice, è possibile deserializzare facilmente i dati utilizzando hello **ExportImportDevice** classe. Hello seguente frammento di codice c# viene illustrato come informazioni sul dispositivo tooread che è stato esportato in precedenza tooa blob in blocchi:

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
> È inoltre possibile utilizzare hello **GetDevicesAsync** metodo hello **RegistryManager** toofetch classe un elenco dei dispositivi. Tuttavia, questo approccio presenta un limite di 1000 numero hello degli oggetti dispositivo restituiti. Hello previsto caso d'uso per hello **GetDevicesAsync** metodo è per il debug tooaid gli scenari di sviluppo e non è consigliata per i carichi di lavoro.

## <a name="import-devices"></a>Importare dispositivi

Hello **ImportDevicesAsync** metodo hello **RegistryManager** classe consente operazioni tooperform bulk importazione e la sincronizzazione in un registro di identità hub IoT. Ad esempio hello **ExportDevicesAsync** (metodo), hello **ImportDevicesAsync** metodo utilizza hello **processo** framework.

Prestare attenzione con hello **ImportDevicesAsync** metodo perché nel aggiunta tooprovisioning nuovi dispositivi al Registro di sistema di identità, anche possibile aggiornare ed eliminare dispositivi esistenti.

> [!WARNING]
> Un'operazione di importazione non può essere annullata. Eseguire sempre il backup dei dati esistenti utilizzando hello **ExportDevicesAsync** il contenitore blob tooanother metodo prima di apportare bulk modifica del Registro di sistema di tooyour identità.

Hello **ImportDevicesAsync** metodo accetta due parametri:

* Oggetto *stringa* che contiene un URI di un [di archiviazione di Azure](../storage/index.md) blob toouse contenitore come *input* toohello processo. Questo URI deve contenere un token di firma di accesso condiviso che concede l'accesso in lettura toohello contenitore. Questo contenitore può contenere un blob con nome hello **devices.txt** hello serializzato dispositivo dati tooimport che contiene il Registro di sistema di identità. Hello l'importazione dei dati deve contenere informazioni sul dispositivo in hello JSON stesso formato di tale hello **ExportImportDevice** processo viene utilizzato quando viene creato un **devices.txt** blob. token SAS Hello deve includere queste autorizzazioni:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* Oggetto *stringa* che contiene un URI di un [di archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contenitore come *output* dal processo di hello. Hello processo crea un blob in blocchi in questo contenitore toostore eventuali informazioni sugli errori dall'importazione completata hello **processo**. token SAS Hello deve includere queste autorizzazioni:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> i parametri di Hello due possono puntare toohello nello stesso contenitore di blob. parametri separati Hello semplicemente consentono maggiore controllo sui dati come contenitore dell'output hello richiede autorizzazioni aggiuntive.

Hello seguente c# codice frammento di codice viene illustrato come tooinitiate un processo di importazione:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Questo metodo può essere anche usato tooimport hello dati per un doppio dispositivo hello. formato di Hello per l'input di dati hello è hello stesso come formato di hello indicato in hello **ExportDevicesAsync** sezione. In questo modo, è possibile reimportare dati hello esportata. Hello **$metadata** è facoltativo.

## <a name="import-behavior"></a>Importare il comportamento

È possibile utilizzare hello **ImportDevicesAsync** seguente di hello tooperform metodo bulk operazioni del Registro di identità:

* Registrazione in blocco di nuovi dispositivi
* Eliminazioni in blocco dei dispositivi esistenti
* Modifiche dello stato in blocco (abilitare o disabilitare dispositivi)
* Assegnazione in blocco di nuove chiavi di autenticazione del dispositivo
* Rigenerazione automatica in blocco di chiavi di autenticazione del dispositivo
* Aggiornamento bulk dei dati gemelli

È possibile eseguire qualsiasi combinazione di hello precedenti operazioni all'interno di un singolo **ImportDevicesAsync** chiamare. Ad esempio, è possibile registrare nuovi dispositivi ed eliminare o aggiornare i dispositivi esistenti in hello contemporaneamente. Quando utilizzato insieme a hello **ExportDevicesAsync** (metodo), è possibile migrare completamente tutti i dispositivi da una tooanother di hub IoT.

Se il file di importazione hello include metadati doppi, questi metadati sovrascrive i metadati di un doppio esistenti hello. Se il file di importazione hello non include i metadati doppi, quindi solo hello `lastUpdateTime` vengono aggiornati i metadati utilizzando hello l'ora corrente.

Hello utilizzo facoltativo **importMode** proprietà nei dati di serializzazione hello importazione per ogni dispositivo toocontrol hello importazione processo al dispositivo. Hello **importMode** proprietà ha hello le opzioni seguenti:

| importMode | Descrizione |
| --- | --- |
| **createOrUpdate** |Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato. <br/>Se il dispositivo hello esiste già, informazioni esistente viene sovrascritto con hello fornito dati di input senza considerare toohello **ETag** valore. <br> utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello. valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello. Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore. |
| **create** |Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato. <br/>Se il dispositivo hello esiste già, il file di log toohello viene scritto un errore. <br> utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello. valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello. Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore. |
| **update** |Se esiste già un dispositivo con hello specificato **id**, informazioni esistente viene sovrascritto con hello fornito dati di input senza considerare toohello **ETag** valore. <br/>Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore. |
| **updateIfMatchETag** |Se esiste già un dispositivo con hello specificato **id**, informazioni esistente viene sovrascritto con hello fornito dati di input solo se è presente un **ETag** corrispondono. <br/>Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore. <br/>Se è presente un **ETag** mancata corrispondenza, viene scritto il file di log toohello un errore. |
| **createOrUpdateIfMatchETag** |Se non esiste un dispositivo con hello specificato **id**, è stato appena registrato. <br/>Se il dispositivo hello esiste già, informazioni esistente viene sovrascritto con hello fornito dati di input solo se è presente un **ETag** corrispondono. <br/>Se è presente un **ETag** mancata corrispondenza, viene scritto il file di log toohello un errore. <br> utente Hello è possibile specificare facoltativamente dati doppi insieme ai dati del dispositivo hello. valore etag del doppi Hello, se specificato, viene elaborata in modo indipendente dal valore etag del dispositivo hello. Se è presente una mancata corrispondenza con l'etag della coppia di hello esistente, il file di log toohello viene scritto un errore. |
| **delete** |Se esiste già un dispositivo con hello specificato **id**, viene eliminato senza considerare toohello **ETag** valore. <br/>Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore. |
| **deleteIfMatchETag** |Se esiste già un dispositivo con hello specificato **id**, viene eliminato solo se è presente un **ETag** corrispondono. Se il dispositivo di hello non esiste, il file di log toohello viene scritto un errore. <br/>Se è presente una mancata corrispondenza ETag, toohello file di log viene scritto un errore. |

> [!NOTE]
> Se i dati di serializzazione hello non definiscono in modo esplicito un **importMode** flag per un dispositivo, valore predefinito è troppo**createOrUpdate** hello durante l'operazione di importazione.

## <a name="import-devices-example--bulk-device-provisioning"></a>Importare dispositivi: esempio di provisioning dei dispositivi in blocco

Hello esempio c# di codice riportato di seguito viene illustrato come toogenerate più identità dispositivo che:

* Includono chiavi di autenticazione.
* Scrivere i blob in blocchi tooa informazioni tale dispositivo.
* Importare i dispositivi di hello del Registro di sistema di hello identità.

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

## <a name="import-devices-example--bulk-deletion"></a>Importare dispositivi: esempio di eliminazione in blocco

Hello nell'esempio di codice seguente viene illustrato come dispositivi hello toodelete che aggiunti utilizzando hello esempio di codice precedente:

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

## <a name="get-hello-container-sas-uri"></a>Ottenere il contenitore di hello URI SAS

Hello nell'esempio di codice seguente illustra come toogenerate un [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con lettura, scrittura ed eliminazione di autorizzazioni per un contenitore di blob:

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

## <a name="next-steps"></a>Passaggi successivi

In questo articolo è stato descritto come tooperform bulk operazioni nel Registro di identità hello in un hub IoT. Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:

* [Metriche di Hub IoT][lnk-metrics]
* [Monitoraggio delle operazioni][lnk-monitor]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
