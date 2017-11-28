---
title: aaaTask preimpostato per Azure Media Indexer
description: "Questo argomento offre una panoramica del set di impostazioni delle attività per Azure Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Set di impostazioni delle attività per Azure Media Indexer

Azure Media Indexer è un processore di contenuti multimediali utilizzare hello tooperform seguenti attività: eseguire la ricerca i file di supporto e contenuto, generare tracce sottotitoli codificate chiuse e parole chiave, indicizzare i file di asset che fanno parte dell'attività.

In questo argomento descrive hello predefinito di attività che è necessario tooyour toopass processo di indicizzazione. Per un esempio completo, vedere [Indicizzazione di file multimediali con Azure Media Indexer](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>File XML di configurazione di Azure Media Indexer

Hello nella tabella seguente vengono illustrati gli elementi e attributi di file XML di configurazione hello.

|Nome|Valore richiesto|Descrizione|
|---|---|---|
|Input|true|File di asset che si desidera tooindex.<br/>Azure Media Indexer supporta i seguenti formati di file multimediali hello: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>È possibile specificare il nome di file hello (s) in hello **nome** o **elenco** attributo di hello **input** elemento (come illustrato di seguito). Se non si specifica quale tooindex di file di asset, file primario hello viene selezionato. Se è impostato alcun file di asset primario, viene indicizzato hello primo file di asset di input hello.<br/><br/>tooexplicitly specificare nome del file hello asset, eseguire:<br/>```<input name="TestFile.wmv" />```<br/><br/>È anche possibile indicizzare più file di asset contemporaneamente (backup di file too10). toodo questo:<br/>- Creare un file di testo (file manifesto) con estensione lst.<br/>-Aggiungere un elenco di tutti i nomi di file di asset hello nel file manifesto toothis asset di input.<br/>-Aggiungere (caricare) manifesto file toohello asset.<br/>-Specificare il nome di hello del file manifesto di hello nell'attributo list di input hello.<br/>```<input list="input.lst">```<br/><br/>**Nota:** se si aggiunta più di 10 file di manifesto toohello file, un processo di indicizzazione hello avrà esito negativo con codice di errore hello 2006.|
|metadata|false|Metadati per hello specificati file di asset.<br/>```<metadata key="..." value="..." />```<br/><br/>È possibile fornire i valori per le chiavi predefinite. <br/><br/>Attualmente, è supportato hello seguenti chiavi:<br/><br/>**titolo** e **descrizione** -utilizzato tooupdate hello lingua modello tooimprove riconoscimento vocale.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**username** e **password**: usate per l'autenticazione quando si scaricano file da Internet tramite http o https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Hello nome utente e gli URL di supporto tooall nel manifesto di input hello vengono applicati i valori di password.|
|funzionalità<br/><br/>Aggiunto nella versione 1.2. Funzionalità supportata solo hello è attualmente il riconoscimento vocale ("ASR").|false|funzionalità di riconoscimento vocale Hello è hello le chiavi delle impostazioni seguenti:<br/><br/>Language:<br/>-hello riconosciuto nel file multimediale hello toobe di linguaggio naturale.<br/>- Inglese, spagnolo<br/><br/>CaptionFormats:<br/>-un elenco delimitato da punto e virgola di hello desiderato formati di output didascalia (se presente)<br/>- ttml;sami;webvtt<br/><br/><br/>GenerateAIB:<br/>-Un flag booleano che specifica se è o meno un file AIB (da utilizzare obbligatoriamente con IFilter Indexer del cliente hello e SQL Server). Per altre informazioni, vedere Uso dei file AIB con Azure Media Indexer e SQL Server.<br/>- True; false<br/><br/>GenerateKeywords:<br/>- Flag booleano che specifica se sia o meno necessario un file XML di parole chiave.<br/>- True; false|

## <a name="azure-media-indexer-configuration-xml-example"></a>Esempio di file XML di configurazione di Azure Media Indexer

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Passaggi successivi

Vedere [Indicizzazione di file multimediali con Azure Media Indexer](media-services-index-content.md).

