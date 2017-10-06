---
title: aaaMonitor Azure Cosmos DB richieste e archiviazione | Documenti Microsoft
description: Informazioni su come toomonitor account del database Cosmos Azure per la metrica di utilizzo, ad esempio di utilizzo dell'archiviazione e le metriche delle prestazioni, ad esempio le richieste e di errori del server.
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Monitorare le richieste, l'utilizzo e le risorse di archiviazione di Azure Cosmos DB
È possibile monitorare gli account di Azure Cosmos DB in hello [portale di Azure](https://portal.azure.com/). Per ogni account Azure Cosmos DB sono disponibili metriche delle prestazioni, quali le richieste e gli errori del server, e metriche di utilizzo, ad esempio l'utilizzo di risorse di archiviazione.

Nel pannello Account hello, nuovo pannello metriche di hello, o in Monitor di Azure, è possibile esaminare le metriche.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Metriche delle prestazioni di visualizzazione nel pannello metriche hello
1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **più servizi**, scorrere troppo**database**, fare clic su **Azure Cosmos DB**, quindi fare clic su nome hello di hello Account di Azure DB Cosmos per cui si desidera tooview le metriche delle prestazioni.
2. Nel menu risorse hello in **monitoraggio**, fare clic su **metriche**.

Apre il pannello di metriche Hello ed è possibile selezionare tooreview raccolta hello. È possibile esaminare le metriche di disponibilità, le richieste, velocità effettiva e archiviazione e confrontarli toohello Azure Cosmos DB SLA.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Visualizzare le metriche delle prestazioni utilizzando Monitoraggio di Azure
1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **monitoraggio** su hello Jumpbar.
2. Scegliere dal menu risorse hello **metriche**.
3. In hello **Monitor - metriche** finestra hello **gruppo di risorse** dal menu a discesa, gruppo di risorse selezionare hello associato hello Azure Cosmos DB account che si desidera toomonitor. 
4. In hello **risorse** dal menu a discesa, selezionare hello database account toomonitor.
5. Nell'elenco di hello di **le metriche disponibili**, selezionare toodisplay metriche hello. Utilizzare hello CTRL pulsante toomulti-select. 

    Le metriche vengono visualizzate in hello **tracciare** finestra. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Metriche delle prestazioni di visualizzazione nel pannello account hello
1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **più servizi**, scorrere troppo**database**, fare clic su **Azure Cosmos DB**, quindi fare clic su nome hello di hello Account di Azure DB Cosmos per cui si desidera tooview le metriche delle prestazioni.
2. Hello **monitoraggio** ottica Visualizza hello seguenti sezioni per impostazione predefinita:
   
   * Totale richieste per hello giorno corrente.
   * Spazio di archiviazione usato.
   
   Se viene visualizzata la tabella **non sono disponibili dati** e si ritiene che vi sono dati nel database, vedere hello [Troubleshooting](#troubleshooting) sezione.
   
   ![Cattura di schermata dell'obiettivo di monitoraggio hello che mostra le richieste di hello e l'utilizzo di archiviazione hello](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Facendo clic su hello **richieste** o **Quota di utilizzo** riquadro apre dettagliate **metrica** blade.
4. Hello **metrica** pannello mostra i dettagli sulle metriche di hello è stato selezionato.  In hello parte superiore del pannello hello è un grafico di richieste nel grafico ogni ora e che è nella tabella sono riportati i valori di aggregazione per le richieste limitate e totale.  Hello blade metriche anche Mostra hello elenco di avvisi che sono stati toohello definita, filtrato metriche che vengono visualizzati nel pannello metriche corrente hello (in questo modo, se si dispone di un numero di avvisi, visualizzare solo quelle pertinenti presentate hello).   
   
   ![Schermata del Pannello di metrica hello che include limitate richieste](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Personalizzare le visualizzazioni di metriche delle prestazioni nel portale di hello
1. le metriche di hello toocustomize che consentono di visualizzare in un grafico specifico, fare clic su tooopen grafico hello in hello **metrica** blade e quindi fare clic su **Modifica grafico**.  
   ![Cattura di schermata dei controlli di blade metriche hello, con Modifica grafico evidenziato](./media/monitor-accounts/madocdb3.png)
2. In hello **Modifica grafico** pannello esistono opzioni toomodify hello metriche che consentono di visualizzare nel grafico hello, nonché l'intervallo di tempo.  
   ![Cattura di schermata del Pannello di modifica grafico hello](./media/monitor-accounts/madocdb4.png)
3. metriche di hello toochange visualizzate nella parte hello, è sufficiente selezionare o deselezionare le metriche delle prestazioni disponibili hello e quindi fare clic su **OK** nella parte inferiore di hello del pannello hello.  
4. hello toochange intervallo di tempo, scegliere un intervallo diverso (ad esempio, **personalizzato**), quindi fare clic su **OK** nella parte inferiore di hello del pannello hello.  
   
   ![Cattura di schermata della parte di intervallo di tempo hello che Mostra pannello di modifica grafico hello come tooenter un intervallo di tempo personalizzato](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Creare grafici side-by-side nel portale di hello
Hello portale di Azure consente di grafici di metriche di toocreate side-by-side.  

1. In primo luogo, fare clic sul grafico hello toocopy desiderati e selezionare **Personalizza**.
   
   ![Cattura di schermata del grafico delle richieste totali hello con l'opzione Personalizza hello evidenziato](./media/monitor-accounts/madocdb6.png)
2. Fare clic su **Clone** hello parte hello toocopy di menu e quindi fare clic su **eseguite di personalizzazione**.
   
   ![Schermata immagine del grafico di hello Totale richieste con hello Clone e fatto le opzioni di personalizzazione evidenziate](./media/monitor-accounts/madocdb7.png)  

È ora possono gestire questa parte come qualsiasi altra parte metrica personalizzazione intervallo metriche e l'ora visualizzata nella parte hello, hello.  In questo modo, è possibile visualizzare due metriche grafico side-by-side in hello contemporaneamente.  
    ![Cattura di schermata del grafico delle richieste totali hello e hello nuove richieste totale oltre il grafico ora](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Impostazione di avvisi nel portale di hello
1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **più servizi**, fare clic su **Azure Cosmos DB**, quindi fare clic su hello nome dell'account di Azure Cosmos DB hello per il quale si desidera toosetup avvisi di metrica di prestazioni.
2. Scegliere dal menu risorse hello **le regole di avviso** pannello regole di avviso di hello tooopen.  
   ![Cattura di schermata di hello avviso regole parte selezionata](./media/monitor-accounts/madocdb10.5.png)
3. In hello **regole di avviso** pannello, fare clic su **Aggiungi avviso**.  
   ![Schermata del pannello regole di avviso hello, con pulsante Aggiungi avviso di hello evidenziato](./media/monitor-accounts/madocdb11.png)
4. In hello **aggiungere una regola di avviso** pannello, specificare:
   
   * nome Hello della regola di avviso hello che si sta impostando.
   * Descrizione della nuova regola di avviso hello.
   * metrica di Hello per regola di avviso hello.
   * condizione Hello, soglia e periodo che determinano quando avviso hello attiva. Ad esempio, un errore del server numero maggiore di 5 su hello ultimi 15 minuti.
   * Se coadministrators e amministratore del servizio hello vengono inviati tramite posta elettronica quando viene generato un avviso di hello.
   * Indirizzi di posta elettronica aggiuntivi per le notifiche degli avvisi.  
     ![Cattura di schermata di hello aggiunta un pannello della regola di avviso](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Monitorare Azure Cosmos DB a livello di codice
Hello metriche sui livelli di account disponibili nel portale di hello, ad esempio di utilizzo dell'archiviazione di account e delle richieste totali, non sono disponibili tramite hello APIs DocumentDB. Tuttavia, è possibile recuperare i dati di utilizzo a livello di raccolta hello utilizzando hello APIs DocumentDB. dati di livello di raccolta tooretrieve hello seguenti:

* hello toouse API REST, [eseguire un'operazione GET sull'insieme di hello](https://msdn.microsoft.com/library/mt489073.aspx). informazioni sulla quota e l'utilizzo di Hello per raccolta di hello viene restituiti nelle intestazioni di x-ms-resource-quota e x-ms-resource-usage hello in risposta hello.
* hello toouse .NET SDK, usare hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) metodo, che restituisce un [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) che contiene un numero di proprietà di utilizzo, ad esempio  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**e altro ancora.

tooaccess altre metriche, utilizzare hello [monitoraggio Azure SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights). Le definizioni delle metriche disponibili possono essere recuperate chiamando:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Query tooretrieve singole metriche utilizzare hello seguente formato:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Per ulteriori informazioni, vedere [il recupero delle metriche delle risorse tramite l'API REST di Azure Monitor hello](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Si noti che il nuovo nome di Azure Insights è Monitoraggio di Azure.  Questo post di blog fa riferimento a nome precedente toohello.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se il monitoraggio riquadri di visualizzazione hello **non sono disponibili dati** messaggio ed è recente effettuato richieste o dati toohello database aggiunto, è possibile modificare l'utilizzo recente hello tooreflect riquadro hello.

### <a name="edit-a-tile-toorefresh-current-data"></a>Modificare i dati correnti toorefresh riquadro
1. le metriche di hello toocustomize che consentono di visualizzare in una determinata parte, fare clic su hello di hello grafico tooopen **metrica** blade e quindi fare clic su **Modifica grafico**.  
   ![Cattura di schermata dei controlli di blade metriche hello, con Modifica grafico evidenziato](./media/monitor-accounts/madocdb3.png)
2. In hello **Modifica grafico** pannello in hello **intervallo di tempo** fare clic su **passati ora**, quindi fare clic su **OK**.  
   ![Cattura di schermata del Pannello di modifica grafico hello con ora precedente selezionato](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Il riquadro verrà aggiornato con i dati e l'uso correnti.  
   ![Cattura di schermata della hello aggiornato totale richieste oltre il riquadro ora](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Passaggi successivi
toolearn più sulla pianificazione della capacità di Azure Cosmos DB, vedere hello [Calcolatrice di pianificazione della capacità di Azure Cosmos DB](https://www.documentdb.com/capacityplanner).

