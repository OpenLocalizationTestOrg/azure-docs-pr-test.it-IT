---
title: "linguaggio di ricerca più aaaAzure | Documenti Microsoft"
description: Ricerca di Azure supporta 56 lingue, grazie ai vantaggi offerti dagli analizzatori delle lingue della tecnologia Lucene e di elaborazione del linguaggio naturale di Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Creare un indice per i documenti in più lingue in Ricerca di Azure
> [!div class="op_single_selector"]
>
> * [Portale](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing hello potenza gli analizzatori del linguaggio è semplice come una proprietà di impostazione su un campo nella definizione dell'indice hello ricercabile. È ora possibile eseguire questo passaggio nel portale di hello.

Di seguito sono schermate di hello pannelli portale di Azure per la ricerca di Azure che consentono agli utenti toodefine uno schema di indice. Da questo pannello, gli utenti possono creare tutti i campi di hello e impostare proprietà analyzer hello per ognuno di essi.

> [!IMPORTANT]
> È possibile impostare solo un analizzatore di lingua durante la definizione di campo, ad esempio quando si crea un nuovo indice dall'hello messa a terra o quando si aggiunge un nuovo indice esistente tooan di campo. Assicurarsi di specificare completamente tutti gli attributi, inclusi analyzer hello, durante la creazione di campo hello. È non essere in grado di tooedit attributi hello o modificare il tipo di Analizzatore hello dopo aver salvato le modifiche.
>
>

## <a name="define-a-new-field-definition"></a>Definire una nuova definizione di campo
1. Accedi toohello [portale di Azure](https://portal.azure.com) e aprire hello blade di servizio del servizio di ricerca.
2. Fare clic su **Aggiungi indice** nel comando hello barra nella parte superiore di hello di hello servizio dashboard toostart un nuovo indice o aprire un tooset indice esistente in nuovi campi che si sta aggiungendo un analizzatore di indice esistente tooan.
3. viene visualizzato il pannello di campi Hello, contenente le opzioni per la definizione dello schema hello dell'indice di hello, incluso tab Analyzer hello utilizzato per la scelta di un analizzatore di lingua.
4. Nei campi, avviare una definizione di campo che fornisce un nome, scelta del tipo di dati hello e impostazione di attributi toomark hello campo come full-text ricercabili, recuperabile nei risultati della ricerca, può essere usati in strutture di navigazione di facet, ordinabile e così via.
5. Prima di proseguire campo successivo toohello aprire hello **Analyzer** scheda.

![][1]
*tooselect un analizzatore, fare clic su scheda Analyzer hello nel pannello campi hello*

## <a name="choose-an-analyzer"></a>Scegliere un analizzatore
1. La definizione di campo hello toofind di scorrimento.
2. Se non sono stati contrassegnati campo hello come disponibile per la ricerca, fare clic su hello casella di controllo ora toomark come **Searchable**.
3. Fare clic su elenco hello Analyzer area toodisplay hello di analizzatori disponibili.
4. Scegliere analyzer hello desiderato toouse.

![][2]
*Selezionare una delle analizzatori hello è supportato per ogni campo*

Per impostazione predefinita, tutti i campi ricercabili utilizzano hello [analizzatore Lucene Standard](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) che è indipendente dalla lingua. elenco completo di hello tooview di analizzatori di supportati, vedere [supporto della lingua nella ricerca di Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Una volta l'analizzatore di lingua hello è selezionata per un campo, verrà utilizzata con ogni richiesta di ricerca e indicizzazione per il campo. Quando una query viene eseguita in più campi usando gli analizzatori di diversi, hello query viene elaborata in modo indipendente dagli analizzatori di destra hello per ogni campo.

Molte applicazioni web e mobili servono gli utenti in tutto il mondo hello utilizzando diversi linguaggi. È possibile toodefine un indice per uno scenario simile mediante la creazione di un campo per ogni lingua supportata.

![][3]
*Definizione di indice con un campo di descrizione per ogni lingua supportata*

Se è noto linguaggio hello dell'agente di hello esecuzione di una query, una richiesta di ricerca può essere tooa con ambito di campo specifico utilizzando hello **searchFields** parametro di query. Hello nella query seguente verrà eseguita solo sul descrizione hello in polacco:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

È possibile eseguire query di indice dal portale hello utilizzando **Esplora ricerche** toopaste in un toohello simile a query illustrato in precedenza. Esplora ricerche è disponibile dalla barra dei comandi hello nel pannello service hello. Vedere [Query sull'indice ricerca di Azure nel portale di hello](search-explorer.md) per informazioni dettagliate.

In alcuni casi hello lingua dell'agente di hello esecuzione di una query non è noto, in cui hello case possono essere eseguite su tutti i campi contemporaneamente. Se necessario, è possibile definire delle preferenze per i risultati in una determinata lingua usando i [profili di punteggio](https://msdn.microsoft.com/library/azure/dn798928.aspx). Nel seguente esempio hello corrispondenze trovate nella descrizione hello in lingua inglese verranno considerato equivalente toomatches relativo superiore in polacco e il francese:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Se si è uno sviluppatore di .NET, si noti che è possibile configurare gli analizzatori del linguaggio mediante hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search). la versione più recente di Hello include il supporto per hello Microsoft gli analizzatori del linguaggio nonché.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
