---
title: dati aaaCopy facilmente con copia guidata - Azure | Documenti Microsoft
description: Informazioni su come toouse hello dati toocopy Data Factory Copia guidata toosinks di origini dati supportate.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Copiare o spostare facilmente i dati con Copia guidata di Azure Data Factory
Hello Azure Data Factory Copia guidata è il processo di hello tooease l'inserimento di dati che è in genere un primo passaggio in uno scenario di integrazione di dati end-to-end. Se si utilizza Copia guidata di Azure Data Factory di hello, non è necessario toounderstand qualsiasi definizione JSON di pipeline, i set di dati e i servizi collegati. Tuttavia, dopo aver completato tutti i passaggi nella procedura guidata hello hello, hello guidata crea automaticamente una pipeline di dati toocopy dalla destinazione selezionata toohello di hello origine dati selezionata. Inoltre hello Copia guidata consente di dati di hello toovalidate il caricamento in fase di creazione, di hello che salva gran parte del tempo, soprattutto quando si sono l'inserimento di dati per hello prima volta dall'origine dati hello. hello toostart Copia guidata, fare clic su hello **copiare dati** riquadro hello home page della data factory.

![Copia guidata](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Una procedura guidata intuitiva per la copia dei dati
Questa procedura guidata consente di spostare tooeasily i dati da una vasta gamma di origini toodestinations in minuti. Dopo aver esaminato la procedura guidata hello, una pipeline con attività di copia viene creata automaticamente insieme a entità dipendenti di Data Factory (servizi collegati e i set di dati). Non sono ulteriori passaggi pipeline hello toocreate obbligatorio.   

![Selezionare l'origine dati](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Vedere [esercitazione guidata copia](data-factory-copy-data-wizard-tutorial.md) articolo per istruzioni dettagliate toocreate dati toocopy di pipeline di esempio da una tabella di Database SQL di Azure tooan blob di Azure. 
> 
> 

la procedura guidata Hello è progettato dati di grandi dimensioni presenti dall'inizio hello. È semplice ed efficiente tooauthor le pipeline di Data Factory che sposta centinaia di cartelle, file o tabelle utilizzando Creazione guidata copia dati hello. procedura guidata Hello supporta hello seguenti tre caratteristiche: anteprima automatica dei dati, l'acquisizione dello schema e mapping e filtraggio dei dati. 

## <a name="automatic-data-preview"></a>Anteprima automatica dei dati
procedura guidata copia Hello consente si tooreview dati hello hello selezionata parte origine dati per l'utente toovalidate se i dati in modo dettagliato hello hello destro dati che si desidera toocopy. Inoltre, se i dati di origine hello sono in un file di testo, procedura guidata copia hello analizza dello schema e i delimitatori di colonna e riga toolearn del file di testo hello automaticamente. 

![Impostazioni sul formato del file](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Acquisizione dello schema e mapping
schema di Hello di dati di input potrebbe non corrispondere schema hello dei dati di output in alcuni casi. In questo scenario, è necessario toomap colonne toocolumns dello schema di origine hello dallo schema di destinazione hello. 

procedura guidata copia Hello esegue automaticamente il mapping di colonne in toocolumns dello schema di origine hello nello schema di destinazione hello. È possibile sostituire i mapping di hello utilizzando elenchi a discesa hello (o) specificano se una colonna deve toobe ignorata durante la copia di dati hello.   

![Mapping dello schema](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtro dei dati
la procedura guidata Hello consente toofilter dati tooselect solo hello dati di origine che è l'archivio dati di destinazione/sink toohello toobe copiati. Filtro riduce volume hello hello dati toobe toohello copiato del sink dei dati, archiviano e pertanto migliora la velocità effettiva di hello dell'operazione di copia hello. Fornisce dati di toofilter un modo flessibile in un database relazionale utilizzando SQL query language (o) file in una cartella blob di Azure utilizzando [variabili e funzioni di Data Factory](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtro dei dati in un database
Nell'esempio hello query SQL hello utilizza hello `Text.Format` funzione e `WindowStart` variabile. 

![Espressione di convalida](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtro dei dati in una cartella BLOB di Azure
È possibile utilizzare variabili in dati toocopy percorso della cartella hello da una cartella in cui viene determinato in fase di esecuzione in base a [le variabili di sistema](data-factory-functions-variables.md#data-factory-system-variables). le variabili di Hello supportato sono: **{year}**, **{month}**, **{day}**, **{ora}**, **{minuto}**, e **{personalizzato}**. Esempio: inputfolder/{year}/{month}/{day}.

Si supponga di avere immesso le cartelle in hello seguente formato:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Fare clic su hello **Sfoglia** pulsante **File o cartella**, Sfoglia tooone di queste cartelle (ad esempio, 2016 -> 03 -> 01 -> 02), fare clic su **scegliere**. Dovrebbe essere `2016/03/01/02` nella casella di testo hello. Sostituire **2016** con **{year}**, **03** con **{month}**, **01** con **{day}** e **02** con **{hour}**, poi premere Tab. Dovrebbe essere formato hello tooselect di elenchi a discesa per questi quattro variabili:

![Uso di variabili di sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Come illustrato nella seguente schermata hello, è inoltre possibile utilizzare un **personalizzato** variabile e qualsiasi [supportate stringhe di formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). una cartella con tale struttura, utilizzare hello tooselect **Sfoglia** pulsante prima. Sostituire un valore con **{personalizzato}**e premere Tab toosee hello casella in cui è possibile digitare la stringa di formato hello.     

![Uso di variabili personalizzate](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Supporto per tipi di dati e di oggetti diversi
Tramite Copia guidata hello, è possibile spostare in modo efficiente centinaia di cartelle, file o tabelle.

![Selezionare le tabelle da cui toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Opzioni di pianificazione
Operazione di copia hello è possibile eseguire una sola volta o in una pianificazione (oraria, giornaliera, e così via). Entrambe le opzioni utilizzabili per breadth hello dei connettori hello in locale, cloud e copia desktop locale.

Un'operazione di copia occasionale consente lo spostamento dei dati da una destinazione tooa origine una sola volta. Si applica toodata di qualsiasi dimensione e qualsiasi formato supportato. copia di Hello pianificata consente toocopy dati in una ricorrenza prestabilita. È possibile utilizzare le impostazioni avanzate (ad esempio i tentativi, timeout e avvisi) tooconfigure hello pianificata copia.

![Proprietà di pianificazione](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione rapida dell'uso hello Data Factory Copia guidata toocreate una pipeline con attività di copia, vedere [esercitazione: creare una pipeline mediante Copia guidata hello](data-factory-copy-data-wizard-tutorial.md).

