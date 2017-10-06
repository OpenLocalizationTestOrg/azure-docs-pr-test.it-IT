---
title: "aaaGet avviato con scalabilità automatica in Azure | Documenti Microsoft"
description: Informazioni su come tooscale la risorsa in Azure.
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Introduzione alla scalabilità automatica in Azure
Questo articolo viene descritto come tooset backup delle impostazioni di scalabilità automatica per la risorsa nel portale di Microsoft Azure hello.

Azure scalabilità automatica di monitoraggio si applica solo set di scalabilità macchina toovirtual, servizi cloud, i piani di servizio App di Azure e gli ambienti del servizio App. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Individuare le impostazioni di scalabilità automatica hello nella sottoscrizione
È possibile individuare tutte le risorse di hello per cui è applicabile in Monitor di Azure. Utilizzare hello alla procedura seguente per una procedura dettagliata:

1. Aprire hello [portale di Azure.][1]
2. Fare clic sull'icona di monitoraggio di Azure di hello nel riquadro di sinistra hello.
  ![Aprire Monitoraggio di Azure][2]
3. Fare clic su **scalabilità automatica** tooview tutte le risorse di hello per la cui scalabilità automatica è applicabile, nonché il relativo stato corrente di scalabilità automatica.
  ![Individuazione della scalabilità automatica nel Monitoraggio di Azure][3]

È possibile utilizzare il riquadro di filtro hello in hello tooscope alto verso il basso hello elencano tooselect le risorse in un determinato gruppo di risorse, tipi di risorsa specifico o una risorsa specifica.

Per ogni risorsa, si trova il numero di istanze correnti di hello e stato scalabilità automatica hello. Hello stato scalabilità automatica può essere:

- **Non configurato**: non è stata ancora abilitata la scalabilità automatica per questa risorsa.
- **Configurato**: è stata abilitata la scalabilità automatica per questa risorsa.
- **Disattivato**: è stata disattivata la scalabilità automatica per questa risorsa.

## <a name="create-your-first-autoscale-setting"></a>Creare la prima impostazione di scalabilità automatica

Verrà ora passano attraverso un toocreate semplice procedura dettagliata la prima impostazione di scalabilità automatica.

1. Aprire hello **scalabilità automatica** pannello in Monitor di Azure e selezionare una risorsa che si desidera tooscale. (hello procedura seguente utilizza un piano di servizio App associato a un'app web. È possibile [creare la prima app Web ASP.NET in Azure in 5 minuti][4]).
2. Si noti che il numero di istanze correnti di hello è 1. Fare clic su **Abilita scalabilità automatica**.
  ![Impostazione di scalabilità per la nuova app Web][5]
3. Specificare un nome per la scala hello impostazione e quindi fare clic su **aggiungere una regola**. Notare le opzioni della regola scala hello aperti come un riquadro contesto sul lato destro hello. Per impostazione predefinita, consente di impostare l'istanza del conteggio di 1 se la percentuale di CPU della risorsa hello hello supera il 70% di hello opzione tooscale. Lasciare i valori predefiniti e fare clic su **Aggiungi**.
  ![Creare l'impostazione di scalabilità per un'app Web][6]
4. È stata così creata la prima regola di scalabilità. Si noti che hello UX consiglia di procedure consigliate e indica che ", è consigliabile toohave almeno una scala nella regola." toodo in modo:
  
    a. Fare clic su **Aggiungi regola**. 

    b. Impostare **operatore** troppo**minore**.

    c. Impostare **soglia** troppo**20**.

    d. Impostare **operazione** troppo**ridurre il numero da**.

   A questo punto si avrà un'impostazione di scalabilità che aumenta/riduce il numero di istanze in base all'utilizzo della CPU.
   ![Scalabilità in base alla CPU][8]
5. Fare clic su **Salva**.

Congratulazioni. Ora è stato creato correttamente il primo tooautoscale di impostazione di scala app web in base all'utilizzo della CPU.

> [!NOTE] 
> stessi passaggi Hello sono applicabili tooget avviato con una scala di macchina virtuale ruolo del servizio cloud o di set.

## <a name="other-considerations"></a>Altre considerazioni
### <a name="scale-based-on-a-schedule"></a>Scalare in base a una pianificazione
Inoltre tooscale basato sulla CPU, è possibile impostare la scala in modo diverso per specifici giorni della settimana hello.

1. Fare clic su **Aggiungi una condizione di scalabilità**.
2. Impostazione delle regole di modalità e hello scala hello è hello stesso come condizione predefinita hello.
3. Selezionare **ripetere giorni specifici** per la pianificazione di hello.
4. Selezionare i giorni hello e l'ora di inizio e fine hello per quando condizione scala hello deve essere applicato.

![Condizione di scalabilità in base alla pianificazione][9]
### <a name="scale-differently-on-specific-dates"></a>Impostare la scalabilità in modo diverso per date specifiche
Inoltre tooscale basato sulla CPU, è possibile impostare la scala in modo diverso per date specifiche.

1. Fare clic su **Aggiungi una condizione di scalabilità**.
2. Impostazione delle regole di modalità e hello scala hello è hello stesso come condizione predefinita hello.
3. Selezionare **specificare date di inizio e fine** per la pianificazione di hello.
4. Selezionare le date di inizio e fine hello e l'ora di inizio e fine hello per quando condizione scala hello deve essere applicato.

![Condizione di scalabilità in base alle date][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Visualizzare la cronologia di scala hello della risorsa
Ogni volta che la risorsa viene ridimensionata verso l'alto o verso il basso, viene registrato un evento nel registro attività hello. È possibile visualizzare cronologia scala hello della risorsa per hello nelle ultime 24 ore passando toohello **cronologia di esecuzione** scheda.

![Cronologia di esecuzione][11]

Se si desidera una cronologia completa di scala di hello tooview (per backup too90 giorni), selezionare **fare clic qui toosee ulteriori dettagli**. log attività Hello apre con pre-selezionata per la risorsa e una categoria di scalabilità automatica.

### <a name="view-hello-scale-definition-of-your-resource"></a>Definizione della vista hello scala della risorsa
Scalabilità automatica è una risorsa di Azure Resource Manager. È possibile visualizzare definizione scala hello in JSON passando toohello **JSON** scheda.

![Definizione del piano][12]

È possibile apportare modifiche direttamente in JSON, se necessario. Queste modifiche saranno applicate dopo averle salvate.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Disabilitare la scalabilità automatica e ridimensionare le istanze manualmente
Potrebbero esserci volte quando si desidera che l'impostazione di scala corrente toodisable e ridimensionare manualmente la risorsa.

Fare clic su hello **disabilitare la scalabilità automatica** pulsante nella parte superiore di hello.
![Disabilita scalabilità automatica][13]

> [!NOTE] 
> Questa opzione disabilita la configurazione. Tuttavia, è possibile tornare tooit dopo aver abilitato la scalabilità automatica nuovamente. 

È ora possibile impostare il numero di hello di istanze che si desidera tooscale toomanually.

![Impostare la scalabilità manuale][14]

È sempre possibile tornare tooAutoscale facendo **abilitare la scalabilità automatica** e quindi **salvare**.

## <a name="next-steps"></a>Passaggi successivi
- [Creare un avviso di Log attività toomonitor tutte le operazioni del motore di scalabilità automatica per la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Creare un avviso di Log attività toomonitor non riuscita. le operazioni di scala/scalabilità di scalabilità automatica per la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

