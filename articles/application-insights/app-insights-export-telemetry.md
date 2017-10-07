---
title: esportazione di aaaContinuous di telemetria da Application Insights | Documenti Microsoft
description: Esportare toostorage di dati di diagnostica e utilizzo in Microsoft Azure e scaricarlo da qui.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Esportare i dati di telemetria da Application Insights
Desidera tookeep dati di telemetria per oltre il periodo di memorizzazione standard di hello? o elaborarli in un modo particolare? A tale scopo, l'esportazione continua è ideale. gli eventi di Hello che viene visualizzato nel portale Application Insights hello possono essere esportati toostorage in Microsoft Azure in formato JSON. Da qui è possibile scaricare i dati e scrivere qualsiasi tipo di codice è necessario tooprocess è.  

L'uso dell'esportazione continua può comportare un costo aggiuntivo. Controllare il [modello di prezzi](http://azure.microsoft.com/pricing/details/application-insights/).

Prima di configurare l'esportazione continua, sono disponibili alcune alternative tooconsider potrebbe essere necessario:

* pulsante Esporta Hello nella parte superiore di hello di blade metriche o ricerca consente di trasferire le tabelle e grafici tooan foglio di calcolo Excel.

* [Dati di analisi](app-insights-analytics.md) offre un linguaggio avanzato di query per la telemetria che consente anche di esportare i risultati.
* Se si sta cercando troppo[esplorare i dati in Power BI](app-insights-export-power-bi.md), è possibile farlo senza utilizzare l'esportazione continua.
* Hello [API REST di accesso ai dati](https://dev.applicationinsights.io/) consente di accedere ai dati di telemetria a livello di codice.

Dopo l'esportazione continua copia toostorage i dati (in cui possibile abilitarlo per fino a quando si desidera), è ancora disponibile in Application Insights per hello consueta [periodo di memorizzazione](app-insights-data-retention-privacy.md).

## <a name="setup"></a> Creare un'esportazione continua
1. Nella risorsa di Application Insights per l'applicazione hello, aprire l'esportazione continua e scegliere **Aggiungi**:

    ![Scorrere verso il basso e fare clic su Esportazione continua](./media/app-insights-export-telemetry/01-export.png)

2. Scegliere i tipi di dati di telemetria hello desiderato tooexport.

3. Creare o selezionare un [account di archiviazione Azure](../storage/common/storage-introduction.md) in cui si desidera dati hello toostore.

    > [!Warning]
    > Per impostazione predefinita, il percorso di archiviazione hello verrà impostato toohello stessa area geografica della risorsa di Application Insights. Se si esegue l'archiviazione in un'area differente, è possibile che vengano applicati addebiti per il trasferimento.

    ![Fare clic su Aggiungi, Destinazione di esportazione, Account di archiviazione e quindi creare un nuovo archivio o scegliere un archivio esistente](./media/app-insights-export-telemetry/02-add.png)

4. Creare o selezionare un contenitore nell'archiviazione hello:

    ![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/create-container.png)

Dopo averla creata, l'esportazione viene avviata. Si ottengono solo i dati in arrivo dopo la creazione di esportazione hello.

Può esistere un ritardo di circa un'ora prima che i dati vengono visualizzati nel servizio di archiviazione hello.

### <a name="tooedit-continuous-export"></a>esportazione continua tooedit

Se si desidera che i tipi di evento hello toochange in un secondo momento, è sufficiente modificare esportazione hello:

![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>esportazione continua toostop

esportazione di hello toostop, fare clic su Disattiva. Quando si sceglie abilita nuovamente, esportazione hello verrà riavviato con nuovi dati. Si otterranno dati hello ricevuti nel portale di hello durante l'esportazione è stata disabilitata.

esportazione di hello toostop, l'eliminazione definitiva. Questa operazione non elimina i dati dalla risorsa di archiviazione.

### <a name="cant-add-or-change-an-export"></a>Non si riesce ad aggiungere o modificare un'esportazione?
* esportazioni tooadd o modifica, sono necessari i diritti di accesso proprietario, collaboratore o collaboratore di Application Insights. [Informazioni sui ruoli][roles].

## <a name="analyze"></a> Quali eventi si ottengono?
Hello dati esportati sono telemetria di hello non elaborati ricevuti dall'applicazione, ma è aggiungere dati di percorso che si calcolano dall'indirizzo IP del client hello.

Dati che sono stati eliminati da [campionamento](app-insights-sampling.md) non è incluso nei dati hello esportata.

Le altre metriche calcolate non sono incluse. Ad esempio, non esportazione medio utilizzo della CPU, ma si procederà all'esportazione di telemetria non elaborati di hello da cui viene calcolata la media hello.

Hello dati includono anche risultati hello di qualsiasi [test web disponibilità](app-insights-monitor-web-app-availability.md) che è stato impostato.

> [!NOTE]
> **Campionamento.** Se l'applicazione invia una grande quantità di dati, funzionalità di campionamento hello possono operare e inviare solo una frazione di telemetria hello generato. [Altre informazioni sul campionamento.](app-insights-sampling.md)
>
>

## <a name="get"></a>Controllare i dati di hello
È possibile esaminare archiviazione hello direttamente nel portale di hello. Fare clic su **Sfoglia**, selezionare l'account di archiviazione e quindi aprire i **Contenitori**.

tooinspect archiviazione di Azure in Visual Studio, aprire **vista**, **Cloud Explorer**. (Se non si dispone di tale comando di menu, è necessario tooinstall hello Azure SDK: hello aprire **nuovo progetto** finestra di dialogo espandere Visual c# del cloud e scegliere **ottenere Microsoft Azure SDK per .NET**.)

Quando si apre l'archivio BLOB, si noterà un contenitore con un set di file BLOB. URI di ogni file Hello derivato dal nome di risorsa di Application Insights, la chiave di strumentazione, tipo di dati di telemetria/data/ora. (nome della risorsa hello è tutti in lettere minuscole, e la chiave di strumentazione hello omette trattini).

![Controllare l'archivio di blob hello con uno strumento appropriato](./media/app-insights-export-telemetry/04-data.png)

hello data e ora siano UTC e quando è stato depositato telemetria hello nell'archivio di hello - tempo di hello non è stato generato. Pertanto, se si scrivono dati di code toodownload hello, è possibile spostarsi in modo lineare dati hello.

Di seguito è il formato di hello di hello percorso:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`è ora di creazione blob in hello interno gestione temporanea di archiviazione
* `blobDeliveryTimeUtc`è il momento di hello è copiato toohello esportazione destinazione archiviazione blob

## <a name="format"></a> Formato dati
* Ogni BLOB è un file di testo che contiene più righe separate da '\n'. Contiene dati di telemetria hello elaborati in un periodo di tempo di circa metà un minuto.
* Ogni riga rappresenta un punto dati di telemetria, ad esempio una richiesta o una visualizzazione di pagina.
* Ogni riga è un documento JSON non formattato. Se desidera toosit comincerà, aprirlo in Visual Studio e scegliere Modifica, avanzate, File di formato:

![Visualizza dati di telemetria hello con uno strumento appropriato](./media/app-insights-export-telemetry/06-json.png)

Gli intervalli di tempo sono espressi in tick, dove 10 000 tick = 1 ms. Ad esempio, questi valori vengono visualizzate un tempo pari a 1 ms toosend una richiesta da browser hello, 3 MS tooreceive e 1.8s tooprocess hello pagina nel browser hello:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>L'elaborazione dei dati hello
Su una scala di piccole dimensioni, è possibile scrivere i dati di alcuni toopull codice divide in due, leggerlo in un foglio di calcolo e così via. ad esempio:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

Per un esempio di codice più esaustivo, vedere l'articolo relativo all'[uso di un ruolo di lavoro][exportasa].

## <a name="delete"></a>Eliminare i vecchi dati
Si noti che è responsabile per la gestione della capacità di archiviazione e l'eliminazione dei dati precedente hello se necessario.

## <a name="if-you-regenerate-your-storage-key"></a>Se si rigenera la chiave di archiviazione...
Se si modifica l'archiviazione di chiavi tooyour hello, l'esportazione continua smetteranno di funzionare. Verrà visualizzata una notifica nell'account Azure.

Aprire il pannello di esportazione continua hello e modificare l'esportazione. Modifica hello esportare destinazione, ma lasciare hello stessa risorsa di archiviazione selezionato. Fare clic su OK tooconfirm.

![Modifica hello continua esportare, aprire e chiudere tre destinazione dell'esportazione.](./media/app-insights-export-telemetry/07-resetstore.png)

l'esportazione continua Hello verrà riavviato.

## <a name="export-samples"></a>Esempi di esportazione

* [Esportare tooSQL tramite flusso Analitica][exportasa]
* [Esempio di analisi di flusso 2](app-insights-export-stream-analytics.md)

In scale di dimensioni maggiori, prendere in considerazione [HDInsight](https://azure.microsoft.com/services/hdinsight/) -cluster Hadoop in cloud hello. HDInsight offre un'ampia gamma di tecnologie per la gestione e analisi dei dati di grandi dimensioni e, è possibile utilizzare dati tooprocess che sono stati esportati da Application Insights.

## <a name="q--a"></a>Domande e risposte
* *Si intende scaricare semplicemente un grafico.*  

    Questa operazione è consentita. Nella parte superiore di hello del Pannello di hello, fare clic su **Esporta dati**.
* *È stata impostata un'esportazione, ma non sono presenti dati nell'archivio personale.*

    Application Insights ricevuto eventuali dati di telemetria dall'app perché è impostare esportazione hello? Si riceveranno solo nuovi dati.
* *Tentato tooset backup un'esportazione, ma è stato negato l'accesso*

    Se l'organizzazione account hello è di proprietà, è necessario toobe un membro dei gruppi di collaboratori o i proprietari di hello.
* *È possibile esportare toomy retta locale proprio archivio?*

    No. Il motore di esportazione attualmente funziona solo con Archiviazione di Azure.  
* *C'è alcun limite di toohello di dati inseriti nell'archivio personale?*

    No. Si saranno mantenere il push dei dati fino a quando non si elimina l'esportazione di hello. Verrà interrotta se viene raggiunto i limiti di hello esterno per l'archiviazione blob, ma che è notevole. È attivo tooyou toocontrol si utilizza lo spazio di archiviazione.  
* *Il numero di BLOB è consigliabile vedere nel servizio di archiviazione hello*

  * Per ogni tipo di dati di tipo è tooexport selezionato, un nuovo blob viene creato ogni minuto (se sono disponibili dati).
  * Per le applicazioni con traffico elevato, inoltre, vengono allocate unità di partizione aggiuntive. In questo caso ogni unità crea un BLOB ogni minuto.
* *Non è hello toomy chiave archiviazione rigenerate o nome hello del contenitore hello modificato, ed esportazione hello non funziona.*

    Modificare l'esportazione di hello e aprire Pannello di destinazione di esportazione hello. Lasciare hello stessa risorsa di archiviazione selezionato in precedenza e fare clic su OK tooconfirm. L'esportazione verrà riavviata. Se è stata modifica hello all'interno di hello dopo alcuni giorni, dei dati andrà perso.
* *È possibile sospendere l'esportazione di hello?*

    Sì. Fare clic su Disabilita.

## <a name="code-samples"></a>Esempi di codice

* [Esempio di analisi di flusso](app-insights-export-stream-analytics.md)
* [Esportare tooSQL tramite flusso Analitica][exportasa]
* [Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
