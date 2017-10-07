---
title: un processo di esportazione di importazione/esportazione di Azure - v1 aaaRepairing | Documenti Microsoft
description: "Informazioni su come un processo di esportazione che è stato creato ed eseguito con toorepair hello importazione/esportazione di Azure service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Riparazione di un processo di esportazione
Al termine di un processo di esportazione, è possibile eseguire hello dello strumento di importazione/esportazione di Microsoft Azure da sito locale:  
  
1.  Scaricare i file che il servizio di importazione/esportazione di Azure hello è stato Impossibile tooexport.  
  
2.  Verificare che i file hello hello unità siano stati esportati correttamente.  
  
È necessario disporre della connettività tooAzure archiviazione toouse questa funzionalità.  
  
comando Hello per il ripristino di un processo di importazione è **RepairExport**.

## <a name="repairexport-parameters"></a>Parametri di RepairExport

Hello seguenti parametri possono essere specificati con **RepairExport**:  
  
|.|Descrizione|  
|---------------|-----------------|  
|**/r:<RepairFile\>**|Obbligatorio. File di correzione toohello percorso, che tiene traccia dell'avanzamento hello di correzione hello e consente un ripristino interrotto tooresume. Ogni unità deve contenere un solo file di ripristino. Quando si avvia un ripristino per una determinata unità, verrà passato in hello percorso tooa file di ripristino non esiste ancora. tooresume un ripristino interrotto, è necessario passare nel nome hello di un file di ripristino esistente. è necessario specificare sempre Hello Ripristina file corrispondente toohello unità di destinazione.|  
|**/logdir:&lt;LogDirectory\>**|Facoltativo. directory dei log Hello. File di log dettagliati verranno scritti toothis directory. Se non viene specificata alcuna directory di log, la directory corrente hello da utilizzare come directory dei log hello.|  
|**/d:&lt;TargetDirectory\>**|Obbligatorio. Hello directory toovalidate e il ripristino. Si tratta in genere directory radice di hello dell'unità di esportazione di hello, ma potrebbe anche essere una condivisione di file di rete contenente una copia dei file hello esportata.|  
|**/bk:<BitLockerKey\>**|Facoltativo. Specificare la chiave di BitLocker hello se si desidera toounlock strumento hello vengono archiviati in cui i file esportati hello crittografato.|  
|**/sn:&lt;StorageAccountName\>**|Obbligatorio. processo di esportazione nome Hello hello dell'account di archiviazione per hello.|  
|**/sk:<StorageAccountKey\>**|**Obbligatorio** solo se non è specificata una firma di accesso condiviso del contenitore. processo di esportazione chiave Hello per l'account di archiviazione hello per hello.|  
|**/csas:<ContainerSas\>**|**Richiesto** se e solo se chiave dell'account di archiviazione hello non è specificato. contenitore di Hello SAS per accedere agli oggetti BLOB hello associato al processo di esportazione hello.|  
|**/CopyLogFile:\><DriveCopyLogFile**|Obbligatorio. Hello percorso toohello unità Copia file di log. file Hello viene generato dal servizio di importazione/esportazione di Azure hello e può essere scaricato dall'archiviazione blob hello associata al processo hello. file di log di copia Hello contiene informazioni sui blob non riuscito o i file che sono toobe riparato.|  
|**/ManifestFile:<DriveManifestFile\>**|Facoltativo. file manifesto dell'unità di Hello percorso toohello esportazione. Questo file è generato dal servizio di importazione/esportazione di Azure hello e archiviato nell'unità di esportazione hello e, facoltativamente in un blob nell'account di archiviazione hello associata al processo hello.<br /><br /> Hello contenuto del file nell'unità di esportazione hello verranno verificati con hash MD5 hello contenute nel file hello. Tutti i file toobe determinato danneggiato verrà scaricato e riscritto toohello directory di destinazione.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Utilizzo di RepairExport toocorrect modalità esportazioni non riuscita  
È possibile utilizzare i file toodownload hello strumento di importazione/esportazione di Azure che non è stato possibile tooexport. file di log di copia Hello conterrà un elenco di file che non è stato possibile tooexport.  
  
le cause degli errori nelle esportazioni Hello includono hello le possibilità seguenti:  
  
-   Unità danneggiate  
  
-   chiave dell'account di archiviazione Hello modificato durante il processo di trasferimento hello  
  
strumento hello toorun **RepairExport** modalità, è innanzitutto necessario tooconnect hello unità contenente hello file esportati tooyour computer. Successivamente, eseguire lo strumento di importazione/esportazione di Azure, specifica di hello percorso toothat unità con hello hello `/d` parametro. È necessario anche file di log di copia dell'unità di toospecify hello percorso toohello che è stato scaricato. Hello seguente esempio di riga di comando seguente esegue hello strumento toorepair eventuali file non tooexport:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Hello Ecco un esempio di un file di log di copia che mostra un blocco in hello tooexport di blob non riuscita:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
file di log di copia Hello indica che si è verificato un errore durante uno dei file toohello di blocchi del blob hello nell'unità di esportazione hello download hello servizio importazione/esportazione di Azure. altri componenti del file hello scaricato correttamente Hello e lunghezza del file hello è stata impostata correttamente. In questo caso, alla quale strumento hello aprire file hello in unità hello, scaricare blocco hello dall'account di archiviazione hello e scriverlo toohello intervallo del file a partire dall'offset 65536 con lunghezza 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>Utilizzo di RepairExport toovalidate contenuti dell'unità  
È inoltre possibile utilizzare importazione/esportazione di Azure con hello **RepairExport** opzione toovalidate hello contenuto unità hello siano corretto. file manifesto di Hello in ogni unità di esportazione contiene MD5s per il contenuto dell'unità hello hello.  
  
Hello servizio importazione/esportazione di Azure inoltre possibile salvare i file manifesto hello tooa account di archiviazione durante il processo di esportazione hello. Hello percorso dei file manifesto hello è disponibile tramite hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione quando il processo di hello è stata completata. Vedere [formato del File manifesto del servizio di importazione/esportazione](storage-import-export-file-format-metadata-and-properties.md) per ulteriori informazioni sul formato hello di un file manifesto dell'unità.  
  
Hello esempio seguente viene illustrato come toorun hello strumento di importazione/esportazione di Azure con hello **/ManifestFile** e **/CopyLogFile** parametri:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Hello Ecco un esempio di un file manifesto:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Dopo il processo di ripristino di completamento hello, hello strumento leggerà ciascun file a cui fa riferimento nel file manifesto hello e verificare l'integrità del file hello con hash MD5 hello. Per il manifesto hello sopra, analizzerà hello seguenti componenti.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Qualsiasi componente mancata verifica hello verrà scaricati dallo strumento hello e riscritti toohello lo stesso file nell'unità di hello.  
  
## <a name="next-steps"></a>Passaggi successivi
 
* [Impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup-v1.md)   
* [Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)   
* [Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)   
* [Riparazione di un processo di importazione](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
