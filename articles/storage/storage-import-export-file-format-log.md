---
title: formato di file log di importazione/esportazione aaaAzure | Documenti Microsoft
description: Informazioni sul formato hello hello di file di log creato quando vengono eseguiti i passaggi per un processo del servizio di importazione/esportazione.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Formato dei file di log del servizio Importazione/Esportazione di Azure
Quando hello servizio importazione/esportazione di Microsoft Azure esegue un'azione in un'unità come parte di un processo di importazione o esportazione, i log vengono scritti tooblock BLOB nell'account di archiviazione hello associata a tale processo.  
  
Esistono due log che possono essere scritti dal servizio di importazione/esportazione hello:  
  
-   log degli errori di Hello viene sempre generata in caso di hello di un errore.  
  
-   Hello log dettagliato non è abilitato per impostazione predefinita, ma può essere abilitato per impostazione hello `EnableVerboseLog` proprietà in un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione.  
  
## <a name="log-file-location"></a>Posizione dei file di log  
Hello vengono scritti i log tooblock BLOB nel contenitore hello o la directory virtuale specificata da hello `ImportExportStatesPath` impostazione, è possibile impostare un `Put Job` operazione. Hello percorso toowhich hello registri dipende da come viene specificata l'autenticazione per il processo di hello, nonché hello valore specificato per `ImportExportStatesPath`. È possibile specificare l'autenticazione per il processo di hello tramite una chiave di account di archiviazione o un contenitore di firma di accesso condiviso.  
  
nome Hello del contenitore hello o la directory virtuale può essere sia un nome predefinito hello `waimportexport`, o un altro contenitore o nome della directory virtuale specificati.  
  
tabella Hello seguente mostra le opzioni possibili hello:  
  
|Metodo di autenticazione|Valore dell'elemento `ImportExportStatesPath`|Posizione dei BLOB di log|  
|---------------------------|----------------------------------------------|---------------------------|  
|Chiave dell'account di archiviazione|Valore predefinito|Un contenitore denominato `waimportexport`, ovvero contenitore predefinito hello. ad esempio:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Chiave dell'account di archiviazione|Valore specificato dall'utente|Un contenitore denominato dall'utente hello. ad esempio:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|Firma di accesso condiviso del contenitore|Valore predefinito|Una directory virtuale denominata `waimportexport`, ovvero nome predefinito di hello, sotto il contenitore di hello specificato nella firma di accesso condiviso hello.<br /><br /> Ad esempio, se hello firma di accesso condiviso per il processo di hello è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, percorso log hello sarà`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|Firma di accesso condiviso del contenitore|Valore specificato dall'utente|Una directory virtuale denominata dall'utente hello, sotto il contenitore di hello specificato nella firma di accesso condiviso hello.<br /><br /> Ad esempio, se hello firma di accesso condiviso per il processo di hello è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e hello specificato una directory virtuale è denominata `mylogblobs`, percorso log hello sarà `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
È possibile recuperare l'URL hello errore hello e di log dettagliati dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione. al termine dell'elaborazione dell'unità di hello, sono disponibili log di Hello.  
  
## <a name="log-file-format"></a>Formato di file dei log  
Hello formato per entrambi i log è hello stesso: un blob che contiene le descrizioni XML degli eventi di hello che si è verificato durante la copia di BLOB tra hello disco rigido e account del cliente hello.  
  
log dettagliato Hello contiene informazioni complete sullo stato di hello dell'operazione di copia hello per ogni blob (per un processo di importazione) o un file (per un processo di esportazione), mentre il log degli errori di hello contiene solo le informazioni di hello per BLOB o i file che ha rilevato errori durante hello importare o esportare i processi.  
  
formato del log dettagliato Hello è illustrato di seguito. log degli errori di Hello è hello struttura, ma esclude le operazioni riuscite.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Hello nella tabella seguente descrive gli elementi di hello hello del file di log.  
  
|Elemento XML|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|`DriveLog`|Elemento XML|Rappresenta un log di unità.|  
|`Version`|Attributo, stringa|versione di Hello del formato di log hello.|  
|`DriveId`|String|numero di serie dell'hardware dell'unità di Hello.|  
|`Status`|String|Stato di elaborazione di unità hello. Vedere hello `Drive Status Codes` tabella riportata di seguito per ulteriori informazioni.|  
|`Blob`|Elemento XML nidificato|Rappresenta un BLOB.|  
|`Blob/BlobPath`|String|URI del blob hello Hello.|  
|`Blob/FilePath`|String|Hello percorso relativo toohello file hello unità.|  
|`Blob/Snapshot`|DateTime|versione di Hello snapshot del blob hello, per un solo processo di esportazione.|  
|`Blob/Length`|Integer|lunghezza totale di Hello di blob hello in byte.|  
|`Blob/LastModified`|DateTime|Hello data/ora ultima modifica del blob che hello, per un solo processo di esportazione.|  
|`Blob/ImportDisposition`|String|Hello importare disposition del blob hello, per un solo processo di importazione.|  
|`Blob/ImportDisposition/@Status`|Attributo, stringa|stato Hello di hello disposizione di importazione.|  
|`PageRangeList`|Elemento XML nidificato|Rappresenta un elenco di intervalli di pagine per un BLOB di pagine.|  
|`PageRange`|Elemento XML|Rappresenta un intervallo di pagine.|  
|`PageRange/@Offset`|Attributo, valore integer|Offset iniziale dell'intervallo di pagine hello in blob hello.|  
|`PageRange/@Length`|Attributo, valore integer|Lunghezza in byte dell'intervallo di pagine hello.|  
|`PageRange/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 dell'intervallo di pagine hello.|  
|`PageRange/@Status`|Attributo, stringa|Stato di elaborazione l'intervallo di pagine hello.|  
|`BlockList`|Elemento XML nidificato|Rappresenta un elenco di blocchi per un BLOB in blocchi.|  
|`Block`|Elemento XML|Rappresenta un blocco.|  
|`Block/@Offset`|Attributo, valore integer|Offset iniziale del blocco di hello nel blob hello.|  
|`Block/@Length`|Attributo, valore integer|Lunghezza in byte del blocco di hello.|  
|`Block/@Id`|Attributo, stringa|ID del blocco di Hello.|  
|`Block/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 del blocco di hello.|  
|`Block/@Status`|Attributo, stringa|Stato di elaborazione blocco hello.|  
|`Metadata`|Elemento XML nidificato|Rappresenta i metadati del blob hello.|  
|`Metadata/@Status`|Attributo, stringa|Stato di elaborazione dei metadati del blob hello.|  
|`Metadata/GlobalPath`|String|File dei metadati globali toohello di percorso relativo.|  
|`Metadata/GlobalPath/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 del file di metadati globali hello.|  
|`Metadata/Path`|String|File di metadati toohello percorso relativo.|  
|`Metadata/Path/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 del file di metadati hello.|  
|`Properties`|Elemento XML nidificato|Rappresenta le proprietà del blob hello.|  
|`Properties/@Status`|Attributo, stringa|Stato di elaborazione delle proprietà del blob hello, ad esempio file non viene trovato, completato.|  
|`Properties/GlobalPath`|String|File delle proprietà globali toohello di percorso relativo.|  
|`Properties/GlobalPath/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 del file delle proprietà globali hello.|  
|`Properties/Path`|String|File delle proprietà toohello del percorso relativo.|  
|`Properties/Path/@Hash`|Attributo, stringa|Hash MD5 codificato in base 16 del file di proprietà hello.|  
|`Blob/Status`|String|Stato di elaborazione blob hello.|  
  
# <a name="drive-status-codes"></a>Codici di stato per un'unità  
Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un'unità.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Completed`|unità di Hello ha terminato l'elaborazione senza errori.|  
|`CompletedWithWarnings`|unità di Hello ha terminato l'elaborazione con avvisi in uno o più BLOB per disposizioni di importazione hello specificate per i BLOB hello.|  
|`CompletedWithErrors`|Hello unità ha terminato con errori in uno o più BLOB o blocchi.|  
|`DiskNotFound`|Nessun disco disponibile nell'unità di hello.|  
|`VolumeNotNtfs`|volume di dati su disco hello prima Hello non è in formato NTFS.|  
|`DiskOperationFailed`|Si è verificato un errore sconosciuto durante l'esecuzione di operazioni sulle unità hello.|  
|`BitLockerVolumeNotFound`|Non è stato trovato nessun volume BitLocker crittografabile.|  
|`BitLockerNotActivated`|BitLocker non è abilitato nel volume hello.|  
|`BitLockerProtectorNotFound`|protezione con chiave di Hello password numerica non esiste nel volume hello.|  
|`BitLockerKeyInvalid`|password numerica di Hello specificata non è possibile sbloccare il volume di hello.|  
|`BitLockerUnlockVolumeFailed`|Quando si tenta di volume hello toounlock, si è verificato un errore sconosciuto.|  
|`BitLockerFailed`|Si è verificato un errore sconosciuto durante l'esecuzione di operazioni BitLocker.|  
|`ManifestNameInvalid`|nome del file manifesto Hello non è valido.|  
|`ManifestNameTooLong`|nome del file manifesto Hello è troppo lungo.|  
|`ManifestNotFound`|file manifesto di Hello non viene trovato.|  
|`ManifestAccessDenied`|File manifesto toohello di accesso è negato.|  
|`ManifestCorrupted`|Hello file manifesto è danneggiato (hello contenuto non corrisponde al valore hash).|  
|`ManifestFormatInvalid`|contenuto del manifesto Hello formato richiesto toohello non è conforme.|  
|`ManifestDriveIdMismatch`|Hello unità che ID nel file manifesto hello non corrisponde a una lettura dal disco hello hello.|  
|`ReadManifestFailed`|Si è verificato un errore dei / o del disco durante la lettura dal manifesto hello.|  
|`BlobListFormatInvalid`|elenco di blob di Hello esportazione formato richiesto toohello non è conforme.|  
|`BlobRequestForbidden`|Accedi ai BLOB toohello nell'account di archiviazione hello non è consentito. Potrebbe trattarsi di scadenza tooinvalid chiave dell'account di archiviazione o firma di accesso.|  
|`InternalError`|E si è verificato un errore interno durante l'elaborazione di unità hello.|  
  
## <a name="blob-status-codes"></a>Codici di stato per un BLOB  
Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un blob.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Completed`|blob di Hello ha terminato l'elaborazione senza errori.|  
|`CompletedWithErrors`|blob Hello ha terminato l'elaborazione con errori in uno o più intervalli di pagine o blocchi, metadati o proprietà.|  
|`FileNameInvalid`|nome del file Hello non è valido.|  
|`FileNameTooLong`|nome del file Hello è troppo lungo.|  
|`FileNotFound`|non è stato trovato il file Hello.|  
|`FileAccessDenied`|File toohello accesso negato.|  
|`BlobRequestFailed`|richiesta di servizio Blob Hello tooaccess hello blob non riuscita.|  
|`BlobRequestForbidden`|richiesta del servizio Blob Hello tooaccess hello blob non è consentito. Potrebbe trattarsi di scadenza tooinvalid chiave dell'account di archiviazione o firma di accesso.|  
|`RenameFailed`|Impossibile blob hello toorename (per un processo di importazione) o file hello (per un processo di esportazione).|  
|`BlobUnexpectedChange`|Si è verificato una modifica imprevista con blob hello (per un processo di esportazione).|  
|`LeasePresent`|È presente su blob hello un lease.|  
|`IOFailed`|Un disco o un errore dei / o di rete si è verificato durante l'elaborazione hello blob.|  
|`Failed`|Si è verificato un errore sconosciuto durante l'elaborazione hello blob.|  
  
## <a name="import-disposition-status-codes"></a>Codici di stato per una disposizione di importazione  
Hello nella tabella seguente sono elencati i codici di stato hello per la risoluzione di una disposizione di importazione.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Created`|Hello blob è stato creato.|  
|`Renamed`|blob Hello è stato rinominato in base a disposizione di importazione rename. Hello `Blob/BlobPath` elemento contiene hello URI per il blob rinominato hello.|  
|`Skipped`|Hello blob è stato ignorato `no-overwrite` disposizione di importazione.|  
|`Overwritten`|è stato sovrascritto da un blob esistente per ogni blob Hello `overwrite` disposizione di importazione.|  
|`Cancelled`|Un errore precedente ha arrestato un'ulteriore elaborazione della disposizione di importazione hello.|  
  
## <a name="page-rangeblock-status-codes"></a>Codici di stato per un intervallo/blocco di pagine  
Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un intervallo di pagine o un blocco.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Completed`|intervallo di pagine Hello o un blocco ha terminato l'elaborazione senza errori.|  
|`Committed`|blocco di Hello è stato eseguito il commit, ma non in hello completo perché altri blocchi necessario non è riuscita o inserire l'elenco completo di blocco non è riuscita.|  
|`Uncommitted`|blocco Hello è stato caricato ma non è stato eseguito il commit.|  
|`Corrupted`|intervallo di pagine Hello o un blocco è danneggiato (hello contenuto non corrisponde al valore hash).|  
|`FileUnexpectedEnd`|È stata rilevata una fine imprevista del file.|  
|`BlobUnexpectedEnd`|È stata rilevata una fine imprevista del BLOB.|  
|`BlobRequestFailed`|Hello richiesta del servizio Blob tooaccess hello intervallo di pagine o blocchi non sono riuscita.|  
|`IOFailed`|Un disco o un errore dei / o di rete durante l'elaborazione di intervallo di pagine hello o un blocco.|  
|`Failed`|Si è verificato un errore sconosciuto durante l'elaborazione di intervallo di pagine hello o un blocco.|  
|`Cancelled`|Un errore precedente ha arrestato l'ulteriore elaborazione dell'intervallo di pagine hello o un blocco.|  
  
## <a name="metadata-status-codes"></a>Codici di stato per i metadati  
Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di metadati blob.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Completed`|metadati Hello ha terminato l'elaborazione senza errori.|  
|`FileNameInvalid`|nome di file di metadati Hello non è valido.|  
|`FileNameTooLong`|nome di file di metadati Hello è troppo lungo.|  
|`FileNotFound`|file di metadati Hello non viene trovato.|  
|`FileAccessDenied`|File di metadati toohello accesso negato.|  
|`Corrupted`|file di metadati Hello è danneggiato (hello contenuto non corrisponde al valore hash).|  
|`XmlReadFailed`|contenuto dei metadati Hello formato richiesto toohello non è conforme.|  
|`XmlWriteFailed`|La scrittura dei metadati di hello che XML non è riuscita.|  
|`BlobRequestFailed`|richiesta di servizio Blob Hello tooaccess hello metadati non riuscita.|  
|`IOFailed`|Si è verificato un errore dei / o disco o di rete durante l'elaborazione dei metadati hello.|  
|`Failed`|Si è verificato un errore sconosciuto durante l'elaborazione dei metadati hello.|  
|`Cancelled`|Un errore precedente ha arrestato un'ulteriore elaborazione dei metadati hello.|  
  
## <a name="properties-status-codes"></a>Codici di stato delle proprietà  
Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione delle proprietà del blob.  
  
|Codice di stato|Descrizione|  
|-----------------|-----------------|  
|`Completed`|proprietà Hello hanno terminato l'elaborazione senza errori.|  
|`FileNameInvalid`|nome del file Hello proprietà non è valido.|  
|`FileNameTooLong`|nome del file delle proprietà Hello è troppo lungo.|  
|`FileNotFound`|file di proprietà Hello non viene trovato.|  
|`FileAccessDenied`|File delle proprietà toohello di accesso è negato.|  
|`Corrupted`|file delle proprietà Hello è danneggiato (hello contenuto non corrisponde al valore hash).|  
|`XmlReadFailed`|contenuto di proprietà Hello formato richiesto toohello non è conforme.|  
|`XmlWriteFailed`|Scrittura delle proprietà hello che XML non è riuscita.|  
|`BlobRequestFailed`|richiesta del servizio Blob Hello tooaccess hello proprietà non è riuscita.|  
|`IOFailed`|Si è verificato un errore dei / o disco o di rete durante l'elaborazione hello proprietà.|  
|`Failed`|Si è verificato un errore sconosciuto durante l'elaborazione hello proprietà.|  
|`Cancelled`|Un errore precedente ha arrestato un'ulteriore elaborazione delle proprietà hello.|  
  
## <a name="sample-logs"></a>Esempi di log  
Hello Ecco un esempio di log dettagliato.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
log degli errori corrispondente Hello è illustrato di seguito.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 log degli errori di seguire Hello per un processo di importazione contiene un errore relativo a un file non trovato nell'unità di importazione hello. Si noti che è stato hello dei componenti successivi `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hello seguenti log degli errori per un processo di esportazione indica che il contenuto di blob hello è stata scritta correttamente toohello unità, ma che si è verificato un errore durante l'esportazione delle proprietà del blob hello.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Passaggi successivi
 
* [Storage Import/Export REST API](/rest/api/storageimportexport/) (API REST di importazione/esportazione dell'archiviazione)
