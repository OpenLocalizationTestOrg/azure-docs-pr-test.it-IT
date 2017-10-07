---
title: esercitazione di BI aaaPower per il connettore Azure Cosmos DB | Documenti Microsoft
description: Utilizzare questo tooimport esercitazione JSON di Power BI, creare report dettagliati e visualizzare i dati usando il connettore di Azure Cosmos DB e Power BI hello.
keywords: esercitazione Power BI, visualizzare dati, connettore Power BI
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Esercitazione di Power BI per Azure Cosmos DB: visualizzare i dati usando il connettore di Power BI hello
[PowerBI.com](https://powerbi.microsoft.com/) è un servizio online in cui è possibile creare e condividere i dashboard e report con i dati importanti tooyou sono all'organizzazione.  Power BI Desktop è una dedicata strumento che consente di creazione tooretrieve i dati del report da diverse origini dati, merge e trasformare i dati di hello, creare visualizzazioni e report potenti e pubblicare i report di hello tooPower BI.  Con la versione più recente di hello di Power BI Desktop, è ora possibile connettersi tooyour DB Cosmos account tramite il connettore DB Cosmos hello per Power BI.   

In questa esercitazione, Power BI analizzerà hello passaggi tooconnect tooa DB Cosmos account in Power BI Desktop, esplorare tooa raccolta in cui i dati di hello tooextract utilizzando hello Navigator, trasforma i dati JSON in formato tabulare, tramite Query di Power BI Desktop Editor, compilare e pubblicare un report tooPowerBI.com.

Dopo aver completato questa esercitazione Power BI, sarà in grado di tooanswer hello seguenti domande:  

* Come è possibile creare report con i dati di Cosmos DB tramite Power BI Desktop?
* Come è possibile collegare l'account Cosmos DB tooa in Power BI Desktop?
* Come è possibile recuperare dati da una raccolta di Power BI Desktop?
* Come è possibile trasformare dati JSON annidati in Power BI Desktop?
* Come è possibile pubblicare e condividere i report personalizzati in PowerBI.com?

> [!NOTE]
> connettore di Power BI Hello per Azure Cosmos DB connette tooPower BI Desktop per l'estrazione e trasformazione dei dati. I report creati in Power BI Desktop possono quindi essere tooPowerBI.com pubblicato. Non è possibile estrarre e trasformare direttamente in PowerBI.com dati di Azure Cosmos DB. 

## <a name="prerequisites"></a>Prerequisiti
Prima di seguire le istruzioni di hello in questa esercitazione Power BI, verificare di disporre di accesso toohello seguenti risorse:

* [più recente di Power BI Desktop Hello](https://powerbi.microsoft.com/desktop).
* Account di accesso tooour demo o dati nell'account di database Cosmos.
  * account demo Hello viene popolata con dati volcano hello illustrati in questa esercitazione. Questo account demo non è associato ad alcun contratto di servizio e viene usato esclusivamente a scopo dimostrativo.  Microsoft si riserva hello toomake destra modifiche toothis demo account inclusi a titolo esemplificativo, terminazione hello account, modificare la chiave hello, limitare l'accesso, la modifica di eliminare i dati di hello, in qualsiasi momento senza preavviso o motivo.
    * URL: https://analytics.documents.azure.com
    * Chiave di sola lettura: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * In alternativa, toocreate il proprio account, vedere [creare un account di database Azure Cosmos DB tramite il portale di Azure hello](https://azure.microsoft.com/documentation/articles/create-account/). Quindi, tooget esempio volcano dati simili toowhat utilizzati in questa esercitazione (ma non contengono blocchi di hello GeoJSON), vedere hello [sito NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) e quindi importare i dati di hello utilizzando hello [la migrazione dei dati di Azure Cosmos DB strumento](import-data.md).

tooshare i report in PowerBI.com, è necessario disporre di un account in PowerBI.com.  toolearn ulteriori informazioni su Power BI per gratuita e Power BI Pro, visitare [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Attività iniziali
In questa esercitazione, si supponga che sei un geologist Studio vulcani tutto il mondo hello.  Hello volcano vengono memorizzati in un account DB Cosmos e documenti JSON hello simile hello successivo documento di esempio.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Si desidera tooretrieve hello volcano dati hello Cosmos DB account e visualizzare i dati in un report di Power BI interattivo come hello seguito relazione.

![Completando l'esercitazione di Power BI con connettore di Power BI hello, sarà in grado di toovisualize dati con report di Power BI Desktop volcano hello](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Pronto toogive it a riprovare? Di seguito sono riportati i requisiti iniziali.

1. Eseguire Power BI Desktop sulla workstation.
2. Dopo l'avvio di Power BI Desktop viene visualizzata una schermata *iniziale* .
   
    ![Schermata iniziale di Power BI Desktop - Connettore Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. È possibile **recupera dati**, vedere **origini recenti**, o **aprire altri report** direttamente da hello *iniziale* dello schermo.  Fare clic su hello X nella schermata di hello tooclose di hello angolo superiore destro. Hello **Report** di Power BI Desktop viene visualizzato.
   
    ![Visualizzazione report di Power BI Desktop - Connettore Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Seleziona hello **Home** della barra multifunzione, quindi fare clic su **recupera dati**.  Hello **recupera dati** finestra.
5. Fare clic su **Azure**, selezionare **Microsoft Azure DocumentDB (Beta)**, quindi fare clic su **Connetti**. 

    ![Recupero di dati in Power BI Desktop - Connettore Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. In hello **anteprima connettore** pagina, fare clic su **continua**. Hello **DocumentDB di Microsoft Azure Connect** verrà visualizzata la finestra.
7. Specificare hello Cosmos DB account URL dell'endpoint come dati hello tooretrieve, come illustrato di seguito e quindi fare clic su **OK**. toouse il proprio account, è possibile recuperare l'URL da hello URI casella hello hello  **[chiavi](manage-account.md#keys)**  blade di hello portale di Azure. hello toouse demo account, immettere `https://analytics.documents.azure.com` per hello URL. 
   
    Omette istruzione SQL, nome della raccolta e nome del database hello come questi campi sono facoltativi.  Al contrario, si utilizzerà hello Navigator tooselect hello Database e la raccolta tooidentify da cui provengono i dati di hello.
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: finestra di connessione desktop](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Se ci si connette a endpoint toothis per hello prima volta, richiesto per la chiave dell'account hello. Per il proprio account, recuperare la chiave hello hello **chiave primaria** casella hello  **[le chiavi di sola lettura](manage-account.md#keys)**  blade di hello portale di Azure. Per l'account demo hello, chiave hello è `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Immettere la chiave appropriata hello e quindi fare clic su **Connetti**.
   
    È consigliabile utilizzare hello chiave di sola lettura durante la creazione di report.  Ciò impedirà un'esposizione non necessaria dei rischi di sicurezza toopotential hello chiave master. chiave di sola lettura Hello è disponibile da hello [chiavi](manage-account.md#keys) blade di hello portale di Azure o è possibile utilizzare hello demo account fornite in precedenza.
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: chiave dell'account](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Se viene visualizzato un messaggio di errore "database specificato hello non trovata." vedere i passaggi in questa soluzione alternativa hello [problema di Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Quando l'account di hello è connesso, hello **Navigator** verranno visualizzati.  Hello **Navigator** verrà visualizzato un elenco dei database con account hello.
10. Fare clic ed espandere il database di hello in hello dati per report hello proverrà dal, se si utilizza l'account demo hello, selezionare **volcanodb**.   
11. A questo punto, selezionare una raccolta che verranno recuperati i dati di hello da. Se si utilizza l'account demo hello, selezionare **volcano1**.
    
    riquadro di anteprima Hello Mostra un elenco di **Record** elementi.  In Power BI un documento viene rappresentato come tipo di **Record** . In modo analogo, anche un blocco JSON annidato in un documento è un **Record**.
    
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: finestra di spostamento](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Fare clic su **modifica** toolaunch hello, Editor di Query in una nuova dati hello tootransform di finestra.

## <a name="flattening-and-transforming-json-documents"></a>Rendere flat e trasformare i documenti JSON
1. Passare finestra Editor di Query di Power BI toohello dove hello **documento** colonna nel riquadro centrale hello.
   ![Editor di Query di Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Fare clic sul pulsante di espansione hello in hello a destra di hello **documento** intestazione di colonna.  verrà visualizzato il menu di scelta rapida Hello con un elenco di campi.  Selezionare i campi hello è necessario per il report, ad esempio, nome Volcano, paese, area, percorso, l'elevazione dei privilegi, tipo, lo stato e ultimo eruzione conoscere e quindi fare clic su **OK**.
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: espandere i documenti](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. riquadro centrale Hello visualizzerà un'anteprima del risultato hello con hello campi selezionati.
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: appiattire i risultati](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. In questo esempio, hello proprietà Location è un blocco di GeoJSON in un documento.  Come si può vedere, la località è rappresentata come tipo di **Record** in Power BI Desktop.  
5. Fare clic su expander hello in hello a destra dell'intestazione di colonna percorso hello.  verrà visualizzato il menu di scelta rapida Hello con campi di tipo e le coordinate.  Consente di selezionare il campo di coordinate hello e fare clic su **OK**.
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: record della posizione](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Hello riquadro centrale Mostra ora una colonna di coordinate di **elenco** tipo.  Come mostrato all'inizio di hello di esercitazione hello, hello i dati GeoJSON in questa esercitazione è di tipo Point con valori di latitudine e longitudine registrati nella matrice di coordinate hello.
   
    elemento di Hello coordinate [0] rappresenta longitudine mentre coordinate [1] indica la latitudine.
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: elenco di coordinate](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Matrice di coordinate tooflatten hello, si creerà un **colonna personalizzata** chiamato LatLong.  Seleziona hello **Aggiungi colonna** della barra multifunzione e fare clic su **Aggiungi colonna personalizzata**.  Hello **Aggiungi colonna personalizzata** finestra.
8. Specificare un nome per la nuova colonna hello, ad esempio LatLong.
9. E quindi specificare una formula personalizzata di hello per la nuova colonna hello.  Per questo esempio, verranno concatenati i valori di latitudine e longitudine hello separati da una virgola, come illustrato di seguito utilizzando hello formula seguente: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Fare clic su **OK**.
   
    Per altre informazioni su Data Analysis Expressions (DAX), incluse le funzioni DAX, vedere [Nozioni di base su DAX in Power BI Designer](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: Aggiungi colonna personalizzata](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. A questo punto, riquadro centrale hello visualizzerà hello nuova colonna LatLong popolato con hello latitudine e i valori di longitudine separati da una virgola.
    
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: colonna LatLong personalizzata](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Se si riceve un errore nella colonna nuovo hello, assicurarsi che i passaggi di hello applicato in impostazioni di Query corrispondano hello seguente illustrazione:
    
    ![I passaggi applicati devono essere Origine, Navigazione, Documento espanso, Documento posizione espanso, Aggiunto personalizzato](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Se i passaggi sono diversi, eliminare hello passaggi aggiuntivi e tentare nuovamente di aggiungere la colonna personalizzata hello. 
11. A questo punto, è stato completato dati hello conversione in formato tabulare.  È possibile sfruttare tutte le funzionalità di hello disponibili in hello Editor di Query tooshape e trasformare i dati nel database Cosmos.  Se si utilizza l'esempio hello, modificare il tipo di dati hello l'elevazione dei privilegi troppo**numero intero** modificando hello **tipo di dati** su hello **Home** della barra multifunzione.
    
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: Cambia tipo di colonna](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Fare clic su **chiudere e applicare** modello di dati toosave hello.
    
    ![Esercitazione su Power BI per il connettore Azure Cosmos DB per Power BI: Chiudi e applica](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Compilare report hello
Visualizzazione di Power BI Desktop Report è in cui è possibile avviare la creazione di report toovisualize dati.  È possibile creare report trascinando e rilasciando i campi in hello **Report** area di disegno.

![Visualizzazione report di Power BI Desktop - Connettore Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

In visualizzazione Report hello, è necessario trovare:

1. Hello **campi** riquadro, si tratta in cui verrà visualizzato un elenco dei modelli di dati con campi, è possibile utilizzare per i report.
2. Hello **visualizzazioni** riquadro. Un report può contenere una o più visualizzazioni.  Selezionare i tipi visual hello adattamento esigenze da hello **visualizzazioni** riquadro.
3. Hello **Report** area di disegno, si tratta in cui gli oggetti visivi hello verrà compilato per il report.
4. Hello **Report** pagina. È possibile aggiungere più pagine del report in Power BI Desktop.

esempio Hello illustrati i passaggi di base di hello di creazione di un report di visualizzazione mappa interattivo semplice.

1. Per questo esempio, si creerà una vista mappa che mostra hello posizione di ogni volcano.  In hello **visualizzazioni** riquadro, fare clic su hello mappa tipo di oggetto visivo come evidenziato nella schermata di hello precedente.  Dovrebbe essere hello mappa tipo di oggetto visivo disegnata su hello **Report** area di disegno.  Hello **visualizzazione** riquadro deve visualizzare anche un set di proprietà correlate toohello tipo di oggetto visivo della mappa.
2. A questo punto, trascinare i campi LatLong hello da hello **campi** riquadro toohello **percorso** proprietà **visualizzazioni** riquadro.
3. Successivamente, trascinare e rilasciare hello Volcano nome campo toohello **legenda** proprietà.  
4. Quindi, trascinare e rilasciare hello elevazione campo toohello **dimensioni** proprietà.  
5. Dovrebbe essere hello mappa che illustra un set di bolle che indica la posizione di hello di ogni volcano con dimensioni di hello di bolla hello correlazione toohello l'elevazione dei privilegi di volcano hello visual.
6. È stato così creato un report di base.  Per personalizzare ulteriormente report hello aggiungendo altre visualizzazioni.  In questo caso, un interattivo report Volcano tipo sezionamento toomake hello è stato aggiunto.  
   
    ![Schermata di report di Power BI Desktop finale di hello al completamento dell'esercitazione di Power BI hello per Azure Cosmos DB](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Pubblicare e condividere il report
tooshare report, è necessario disporre di un account in PowerBI.com.

1. In hello Power BI Desktop, fare clic su hello **Home** della barra multifunzione.
2. Fare clic su **Pubblica**.  Sarà richiesto tooenter hello utente nome e una password per l'account PowerBI.com.
3. Una volta credenziali hello sono stata autenticata, report hello è pubblicato tooyour destinazione selezionata.
4. Fare clic su **Open 'PowerBITutorial.pbix' in Power BI** toosee e condividere il report in PowerBI.com.
   
    ![Pubblicazione tooPower successo BI! Aprire Esercitazione in Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Creare un dashboard in Power BI
Ora che si dispone di un report, è possibile condividerlo in PowerBI.com

Quando si pubblica il report da Power BI Desktop tooPowerBI.com, viene generato un **Report** e **Dataset** nel tenant di PowerBI.com. Ad esempio, dopo che è stato pubblicato un report denominato **PowerBITutorial** tooPowerBI.com, vedrai PowerBITutorial entrambi hello **report** e **set di dati** sezioni in PowerBI.com.

   ![Schermata di hello nuovi Report e set di dati in PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate un dashboard condivisibile, fare clic su hello **Aggiungi pagina dinamica** pulsante report PowerBI.com.

   ![Schermata di hello nuovi Report e set di dati in PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Quindi seguire le istruzioni hello [aggiungere un riquadro da un report](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate un nuovo dashboard. 

È inoltre possibile eseguire le modifiche ad hoc tooreport prima di creare un dashboard. Tuttavia, è consigliabile utilizzare le modifiche di Power BI Desktop tooperform hello e ripubblicare hello tooPowerBI.com di report.

## <a name="refresh-data-in-powerbicom"></a>Aggiornare i dati in PowerBI.com
Esistono due modi toorefresh dati ad hoc e pianificati.

Per un aggiornamento ad hoc, è sufficiente fare clic su eclipses hello (…) da hello **Dataset**, ad esempio PowerBITutorial. A questo punto viene visualizzato un elenco di azioni, tra cui **Aggiorna adesso**. Fare clic su **Aggiorna ora** dati hello toorefresh.

![Schermata di Aggiorna adesso in PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Per un aggiornamento pianificato, hello seguente.

1. Fare clic su **Pianifica aggiornamento** nell'elenco di azioni hello. 

    ![Schermata di hello pianificazione dell'aggiornamento in PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. In hello **impostazioni** espandere **le credenziali dell'origine dati**. 
3. Fare clic su **Modifica credenziali**. 
   
    popup Configura Hello viene visualizzato. 
4. Immettere hello tooconnect chiave toohello DB Cosmos account per set di dati, quindi fare clic su **Accedi**. 
5. Espandere **Pianifica aggiornamento** e impostare la pianificazione di hello toorefresh hello set di dati. 
6. Fare clic su **applica** e avere impostato l'aggiornamento pianificato hello.

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni su Power BI, vedere [Introduzione a Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn ulteriori informazioni su Cosmos DB, vedere hello [pagina di destinazione di documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

