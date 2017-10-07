---
title: Factory di Azure Copia guidata aaaData | Documenti Microsoft
description: Informazioni su come toouse hello dati toocopy Data Factory Azure Copia guidata toosinks di origini dati supportate.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Copia guidata di Azure Data Factory
Hello Azure Data Factory Copia guidata semplifica il processo di hello l'inserimento di dati che è in genere un primo passaggio in uno scenario di integrazione di dati end-to-end. Se si utilizza Copia guidata di Azure Data Factory di hello, non è necessario toounderstand tutte le definizioni di JSON per i servizi collegati, set di dati e pipeline. procedura guidata di Hello crea automaticamente una pipeline di dati toocopy dalla destinazione selezionata toohello di hello origine dati selezionata. Inoltre, hello Copia guidata consente di dati di hello toovalidate il caricamento in fase di creazione di hello. Ciò consente di risparmiare tempo, soprattutto quando si sono l'inserimento di dati per hello prima volta dall'origine dati hello. hello toostart Copia guidata, fare clic su hello **copiare dati** riquadro hello home page della data factory.

![Copia guidata](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Pensata per i Big Data
Questa procedura guidata consente di spostare tooeasily i dati da una vasta gamma di origini toodestinations in minuti. Dopo la riconnessione guidata hello, una pipeline con attività di copia viene creata automaticamente, insieme a entità dipendenti di Data Factory (servizi collegati e set di dati). Non sono ulteriori passaggi pipeline hello toocreate obbligatorio.   

![Selezionare l'origine dati](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Per istruzioni dettagliate toocreate dati toocopy di pipeline di esempio da una tabella di Database SQL di Azure tooan blob di Azure, vedere hello [esercitazione guidata copia](data-factory-copy-data-wizard-tutorial.md).
>
>

la procedura guidata Hello è progettato dati di grandi dimensioni presenti dall'inizio di hello, con il supporto per diversi tipi di dati e oggetti. È possibile creare pipeline di Data Factory che spostano centinaia di cartelle, file o tabelle. procedura guidata di Hello supporta anteprima automatica dei dati, l'acquisizione dello schema e mapping e il filtro dei dati.

## <a name="automatic-data-preview"></a>Anteprima automatica dei dati
È possibile visualizzare in anteprima parte dei dati dall'origine dati selezionata hello in ordine toovalidate hello se dati hello sono toocopy. Inoltre, se i dati di origine hello sono in un file di testo, hello Copia guidata analizza la riga hello hello testo file toolearn e delimitatori di colonna e lo schema automaticamente.

![Impostazioni sul formato del file](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Acquisizione dello schema e mapping
schema di Hello di dati di input potrebbe non corrispondere schema hello dei dati di output in alcuni casi. In questo scenario, è necessario toomap colonne toocolumns dello schema di origine hello dallo schema di destinazione hello.

> [!TIP]
> Copia dei dati da SQL Server o Database SQL di Azure in Azure SQL Data Warehouse, se non esiste alcuna tabella hello nell'archivio di destinazione hello, Data Factory supporta quando dello schema dell'origine utilizzando la creazione della tabella automatica. Altre informazioni da [spostare tooand dati da Azure SQL Data Warehouse usando Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).
>

Utilizzare tooselect un elenco a discesa una colonna dalla colonna tooa toomap di hello origine dello schema nello schema di destinazione hello. Copia guidata Hello tenta toounderstand il modello per il mapping di colonna. Si applica hello stesso modello toohello rest delle colonne di hello, in modo che non è necessario tooselect colonne hello individualmente il mapping dello schema toocomplete hello. Se si preferisce, è possibile eseguire l'override di questi mapping utilizzando le colonne hello elenchi a discesa toomap hello uno alla volta. modello di Hello diventa più accurata di come si esegue il mapping di più colonne. Copia guidata Hello aggiorna continuamente il modello di hello e alla fine raggiunge hello destra di modello per la colonna hello mapping si desidera tooachieve.     

![Mapping dello schema](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtro dei dati
È possibile filtrare i dati tooselect solo hello dati di origine che deve toobe copiati toohello sink dati archivio. Filtro riduce volume hello hello dati toobe toohello copiato del sink dei dati, archiviano e pertanto migliora la velocità effettiva di hello dell'operazione di copia hello. Fornisce dati di toofilter un modo flessibile in un database relazionale utilizzando il linguaggio di query SQL hello o di file in una cartella blob di Azure mediante [variabili e funzioni di Data Factory](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtro dei dati in un database
Hello schermata riportata di seguito viene illustrata una query SQL utilizzando hello `Text.Format` funzione e `WindowStart` variabile.

![Espressione di convalida](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtro dei dati in una cartella BLOB di Azure
È possibile utilizzare variabili in dati toocopy percorso della cartella hello da una cartella in cui viene determinato in fase di esecuzione in base a [le variabili di sistema](data-factory-functions-variables.md#data-factory-system-variables). le variabili di Hello supportato sono: **{year}**, **{month}**, **{day}**, **{ora}**, **{minuto}**, e **{personalizzato}**. Ad esempio: inputfolder/{year}/{month}/{day}.

Si supponga di avere immesso le cartelle in hello seguente formato:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Fare clic su hello **Sfoglia** pulsante **File o cartella**, Sfoglia tooone di queste cartelle (ad esempio, 2016 -> 03 -> 01 -> 02), fare clic su **scegliere**. Dovrebbe essere `2016/03/01/02` nella casella di testo hello. A questo punto, sostituire **2016** con **{year}**, **03** con **{month}**, **01** con **{day}** , e **02** con **{ora}**e premere hello **scheda** chiave. Dovrebbe essere formato hello tooselect di elenchi a discesa per questi quattro variabili:

![Uso di variabili di sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Come illustrato nella seguente schermata hello, è inoltre possibile utilizzare un **personalizzato** variabile e qualsiasi [supportate stringhe di formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). una cartella con tale struttura, utilizzare hello tooselect **Sfoglia** pulsante prima. Sostituire un valore con **{personalizzato}**e premere hello **scheda** casella di testo hello toosee chiave in cui è possibile digitare la stringa di formato hello.     

![Uso di variabili personalizzate](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Opzioni di pianificazione
Operazione di copia hello è possibile eseguire una sola volta o in una pianificazione (oraria, giornaliera, e così via). Entrambi queste opzioni possono essere usati per breadth hello dei connettori hello in ambienti, tra cui on-premise, cloud e copia desktop locale.

Un'operazione di copia occasionale consente lo spostamento dei dati da una destinazione tooa origine una sola volta. Si applica toodata di qualsiasi dimensione e qualsiasi formato supportato. copia di Hello pianificata consente toocopy dati in una ricorrenza prestabilita. È possibile utilizzare le impostazioni avanzate (ad esempio i tentativi, timeout e avvisi) tooconfigure hello pianificata copia.

![Proprietà di pianificazione](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione rapida dell'uso hello Data Factory Copia guidata toocreate una pipeline con attività di copia, vedere [esercitazione: creare una pipeline mediante Copia guidata hello](data-factory-copy-data-wizard-tutorial.md).
