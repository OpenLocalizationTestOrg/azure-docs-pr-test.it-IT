---
title: hello aaaUsing pubblicare Azure applicazione guidata di Visual Studio | Documenti Microsoft
description: Informazioni su come tooconfigure hello varie impostazioni di Visual Studio pubblicazione Azure guidata applicazione hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Utilizzando Visual Studio pubblicazione Azure guidata applicazione hello
Dopo aver sviluppato un'applicazione web in Visual Studio, è possibile pubblicare tale tooan applicazione del servizio cloud di Azure tramite hello **pubblica l'applicazione Azure** procedura guidata. 

> [!NOTE]
> In questo argomento riguarda la distribuzione di servizi toocloud, non tooweb siti. Per informazioni sulla distribuzione di siti tooweb, vedere [come sito Web di Azure tooDeploy](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Accesso a procedura guidata pubblica l'applicazione Azure hello

È possibile accedere la procedura guidata pubblica l'applicazione Azure hello in due modi diversi a seconda del progetto di Visual Studio che è di tipo di hello.

**Se si dispone di un progetto servizio cloud di Azure:**

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **pubblica**.

**Se si dispone di un progetto applicazione Web non abilitato per Azure:**

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **convertire** > **convertire il progetto servizio Cloud tooAzure**. 

1. In **Esplora**, fare clic sul progetto Azure hello appena creato e scegliere dal menu di scelta rapida hello, **pubblica**.

## <a name="sign-in-page"></a>Pagina di accesso

![Pagina di accesso](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Account** - selezionare un account o **aggiungere un account** nell'elenco a discesa di hello account.

**Scegliere la propria sottoscrizione** -scegliere hello toouse di sottoscrizione per la distribuzione.
   
## <a name="settings-page---common-settings-tab"></a>Pagina Impostazioni - Scheda Impostazioni comuni   

![Impostazioni comuni](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Servizio cloud** -utilizzando l'elenco a discesa hello, selezionare un cloud esistente, oppure selezionare  **&lt;Crea nuovo >**e creare un servizio cloud. centro dati Hello Visualizza tra parentesi per ogni servizio cloud. È consigliabile che hello posizione del data center per essere hello servizio cloud hello stesso come posizione del data center hello per account di archiviazione hello (impostazioni avanzate).  

**Ambiente** - Selezionare **Produzione** o **Gestione temporanea**. Scegliere l'applicazione di ambiente di gestione temporanea se si desidera toodeploy hello in un ambiente di test. 

**Configurazione compilazione** - Selezionare **Debug** o **Rilascio**.

**Configurazione servizio** - Selezionare **Cloud** o **Locale**.
   
**Abilitare Desktop remoto per tutti i ruoli** -verificare che questa opzione se si desidera toobe tooremotely in grado di connettersi toohello servizio. Questa opzione viene usata principalmente per la risoluzione dei problemi. Quando si seleziona questa casella di controllo, hello **configurazione Desktop remoto** viene visualizzata la finestra di dialogo. Scegliere hello **impostazioni** configurazione hello toochange del collegamento.
   
**Abilita distribuzione Web per tutti i ruoli web** -selezionare questa opzione, la distribuzione di web tooenable per il servizio di hello. È necessario selezionare hello **Abilita Desktop remoto per tutti i ruoli** opzione toouse questa funzionalità. Per altre informazioni, vedere [[Pubblicazione di un servizio cloud di Azure con Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Pagina Impostazioni - Scheda Impostazioni avanzate

![Impostazioni avanzate](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Etichetta distribuzione** -accettare nome predefinito hello o immettere un nome di propria scelta. tooappend hello data toohello etichetta della distribuzione, lasciare hello casella di controllo. 
   
**Account di archiviazione** : selezionare questa opzione hello toouse account di archiviazione per la distribuzione, * *&lt;Crea nuovo > toocreate un account di archiviazione. centro dati Hello Visualizza tra parentesi per ogni account di archiviazione. È consigliabile che hello posizione del data center per essere hello account di archiviazione hello stesso come posizione del data center hello per il servizio cloud hello (impostazioni comuni).  
   
account di archiviazione Azure Hello Archivia pacchetto hello per la distribuzione dell'applicazione hello. Dopo aver distribuita l'applicazione hello, pacchetto hello viene rimosso dall'account di archiviazione hello.

**Eliminare la distribuzione in caso di errore** -selezionare la distribuzione di hello toohave opzione eliminata se vengono rilevati errori durante la pubblicazione. Deve essere deselezionata se si desidera toomaintain un indirizzo IP virtuale costante per il servizio cloud.

**Aggiornamento della distribuzione** -selezionare questa opzione se si desidera toodeploy solo i componenti aggiornati. Questo tipo di distribuzione risulta più rapida della distribuzione completa. Controllare se si desidera toomaintain un indirizzo IP virtuale costante per il servizio cloud. 

**Aggiornamento della distribuzione - impostazioni** -viene utilizzata questa finestra di dialogo toofurther specificare la modalità di hello ruoli toobe aggiornato. Se si sceglie **aggiornamento incrementale**, ogni istanza dell'applicazione viene aggiornata una dopo l'altra, in modo che un'applicazione hello è sempre disponibile. Se si sceglie **aggiornamento simultaneo**, tutte le istanze dell'applicazione vengono aggiornate in hello contemporaneamente. L'aggiornamento simultaneo è più veloce, ma il servizio potrebbe non essere disponibile durante il processo di aggiornamento hello. 

![Impostazioni di distribuzione](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Abilitare IntelliTrace** -specificare se si desidera tooenable IntelliTrace. Con IntelliTrace è possibile registrare informazioni di debug approfondite per un'istanza del ruolo quando è in esecuzione in Azure. Se è necessario a causa di hello toofind di un problema, è possibile utilizzare hello IntelliTrace registri toostep tramite il codice da Visual Studio come se fosse in esecuzione in Azure. Per altre informazioni sull'uso di IntelliTrace, vedere [Debug di un servizio cloud pubblicato con IntelliTrace e Visual Studio](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Abilitare la profilatura** -specificare se si desidera tooenable profilatura delle prestazioni. il profiler di Visual Studio Hello consente si tooget un'analisi approfondita degli aspetti computazionali di hello della modalità di esecuzione il servizio cloud. Per ulteriori informazioni sull'utilizzo del profiler di Visual Studio hello, vedere [Test delle prestazioni di hello di un servizio cloud di Azure](./vs-azure-tools-performance-profiling-cloud-services.md).

**Abilita Debugger remoto per tutti i ruoli** -specificare se si desidera tooenable il debug remoto. Per altre informazioni sul debug dei servizi cloud con Visual Studio, vedere [Debug di un servizio cloud o di una macchina virtuale di Azure in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Pagina Impostazioni di diagnostica

![Impostazioni di diagnostica](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

È possibile utilizzare diagnostica tootroubleshoot un servizio cloud di Azure (o macchina virtuale di Azure). Per informazioni sulla diagnostica, vedere [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Per informazioni su Application Insights, vedere [Informazioni su Azure Application Insights](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Pagina Riepilogo

![Riepilogo](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Profilo di destinazione** -è possibile scegliere un profilo di pubblicazione toocreate dalle impostazioni di hello che si sono scelto. È ad esempio possibile creare un profilo per un ambiente di test e un altro per l'ambiente di produzione. toosave questo profilo, scegliere hello **salvare** icona. Hello profilo hello creato e salvato nel progetto di Visual Studio hello. nome del profilo hello toomodify, aprire hello **profilo di destinazione** elenco e quindi scegliere **< Gestisci >**.
   
   > [!NOTE]
   > profilo di pubblicazione Hello viene visualizzato in Esplora soluzioni in Visual Studio e le impostazioni del profilo hello vengono scritte tooa file con estensione azurepubxml. Le impostazioni vengono salvate come attributi dei tag XML.
   > 
   > 

## <a name="publishing-your-application"></a>Pubblicazione dell'applicazione

Una volta configurato, tutte le impostazioni di hello per la distribuzione del progetto, selezionare **pubblica** nella parte inferiore di hello della finestra di dialogo hello. È possibile monitorare lo stato di processo hello in hello **Output** finestra in Visual Studio.

## <a name="next-steps"></a>Passaggi successivi
- [Eseguire la migrazione e pubblicare un servizio cloud di Azure da Visual Studio di tooan applicazione Web](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Informazioni su come servizio cloud toouse toopublish di Visual Studio di Azure](./vs-azure-tools-publishing-a-cloud-service.md)
- [Debug di un servizio cloud di Azure pubblicato con Visual Studio e IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Test delle prestazioni di hello di un servizio cloud di Azure](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 
- [Informazioni su Azure Application Insights](./application-insights/app-insights-overview.md)