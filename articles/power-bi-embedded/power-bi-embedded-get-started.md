---
title: Introduzione a Microsoft Power BI Embedded aaaGet
description: Power BI Embedded, aggiungere report di Power BI interattivi nell'applicazione di Business Intelligence
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Introduzione a Microsoft Power BI Embedded

**Power BI Embedded** è un servizio di Azure che tooadd agli sviluppatori di applicazioni consente report interattivi di Power BI nelle proprie applicazioni. **Power BI Embedded** funziona con le applicazioni esistenti, senza la necessità di riprogettazione o modificare utenti modo hello Accedi.

Risorse per **Microsoft Power BI Embedded** viene effettuato il provisioning tramite hello [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx). In questo caso, risorse hello viene effettuato il provisioning sono una **raccolta dell'area di lavoro di Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Creare una raccolta di aree di lavoro

Oggetto **dell'area di lavoro raccolta** è una risorsa di Azure di livello superiore di hello e un contenitore per il contenuto di hello che verrà incorporato nell'applicazione. Una **Raccolta di aree di lavoro** può essere creata in due modi:

* Manualmente tramite il portale di Azure hello
* Livello di programmazione tramite hello API Manager(ARM) risorse di Azure

Si analizzerà hello passaggi toobuild un **dell'area di lavoro raccolta** utilizzando hello portale di Azure.

1. Aprire il **portale di Azure**ed eseguire l'accesso: [http://portal.azure.com](http://portal.azure.com).
2. Fare clic su **+ nuovo** nel riquadro superiore hello.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. In **Dati e analisi** fare clic su **Power BI Embedded**.
4. In hello **dell'area di lavoro Raccolta pannello**, immettere le informazioni necessarie hello. Per **Prezzi**, vedere [Prezzi di Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Fare clic su **Crea**.

Hello **dell'area di lavoro raccolta** richiederà qualche minuto tooprovision. Al termine, verrà visualizzato toohello **dell'area di lavoro Raccolta pannello**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Hello **pannello creazione** contiene informazioni hello necessarie toocall hello API che creano aree di lavoro e distribuire contenuto toothem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Visualizzare le chiavi di accesso dell'API Power BI

Uno dei principali tipi di informazioni necessarie toocall hello API REST di Power BI hello sono hello **chiavi di accesso**. Questi vengono utilizzati toogenerate hello **token app** che vengono utilizzati tooauthenticate le richieste API. tooview il **chiavi di accesso**, fare clic su **chiavi di accesso** su hello **pannello impostazioni**. Per altre informazioni sui **token delle app**, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Come si noterà, sono disponibili due chiavi.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Copiarle e archiviarle in modo sicuro nell'applicazione. È molto importante considerare queste chiavi come si farebbe con una password, perché verrà forniscono accesso tooall hello contenuto il **dell'area di lavoro insieme**.

Anche se sono disponibili due chiavi, è necessaria una sola chiave alla volta. seconda chiave Hello viene fornito e quindi è possibile rigenerare periodicamente le chiavi senza interrompere il servizio di accesso toohello.

Dopo aver creato un'istanza di Power BI per l'applicazione e le **chiavi di accesso**, è possibile importare un report nell'app in uso. Prima viene illustrato come tooimport un report, nella sezione successiva hello descrive la creazione tooembed set di dati e i report di Power BI in un'app.

## <a name="working-with-workspaces"></a>Utilizzo di aree di lavoro

Dopo aver creato la raccolta dell'area di lavoro, sarà necessario toocreate un'area di lavoro che conterrà i report e set di dati. toocreate un'area di lavoro, sarà necessario hello toouse [API REST di area di lavoro Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Creare tooembed set di dati e i report di Power BI in un'app con Power BI Desktop

Ora che è stata creata un'istanza di Power BI per l'applicazione e ha **chiavi di accesso**, saranno necessari il set di dati di toocreate hello Power BI e report che si desidera tooembed. I set di dati e i report possono essere creati con **Power BI Desktop**. È possibile scaricare [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662). In alternativa, iniziare tooquickly, è possibile scaricare hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> altre informazioni su come toolearn toouse **Power BI Desktop**, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Con **Power BI Desktop**, tooyour origine dei dati si connette tramite l'importazione di una copia dei dati di hello in **Power BI Desktop** o la connessione diretta toohello dati di origine utilizzando **DirectQuery**.

Di seguito sono differenze nell'utilizzo hello **importazione** e **DirectQuery**.

| Importa | DirectQuery |
| --- | --- |
| Tabelle, colonne, *e dati* vengono importati o copiati in **Power BI Desktop**. Mentre si lavora con visualizzazioni, **Power BI Desktop** una copia dei dati hello una query. toosee eventuali modifiche di dati sottostante toohello durante l'esecuzione, è necessario aggiornare o importare, nuovamente un dataset corrente non completato. |Solo *tabelle e colonne* vengono importate o copiate in **Power BI Desktop**. Mentre si lavora con visualizzazioni, **Power BI Desktop** query hello origine dati sottostante, ovvero sempre si visualizzano i dati correnti. |

Per ulteriori informazioni sull'origine dei dati tooa connessione, vedere [origine dati di connessione tooa](power-bi-embedded-connect-datasource.md).

Dopo aver salvato il lavoro in **Power BI Desktop**viene creato un file PBIX. Questo file contiene il report. Inoltre, se si importa hello dati PBIX contiene hello set di dati completo, o se si utilizza **DirectQuery**, hello PBIX contiene uno schema di set di dati. Distribuire a livello di codice hello PBIX nell'area di lavoro utilizzando hello [API Power BI Importa](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** dispone di altre API toochange hello server e database che il set di dati fa riferimento il set di tooand una credenziale dell'account del servizio che hello set di dati utilizzerà tooconnect tooyour database. Vedere [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (POST di SetAllConnections) e [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (PATCH dell'origine dati del gateway).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Creare set di dati e report di Power BI usando le API

### <a name="datsets"></a>Set di dati

È possibile creare set di dati in Power BI Embedded utilizzando hello API REST. ed effettuare poi il push dei dati nel set di dati. In questo modo toowork con i dati senza necessità di hello di Power BI Desktop. Per altre informazioni, vedere [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Pubblica set di dati).

### <a name="reports"></a>Report

È possibile creare un report da un set di dati direttamente in un'applicazione con hello API JavaScript. Per altre informazioni, vedere [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded).

## <a name="see-also"></a>Vedere anche

[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Incorporare un report)  
[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded)
[Save reports](power-bi-embedded-save-reports.md) (Salvare report)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

