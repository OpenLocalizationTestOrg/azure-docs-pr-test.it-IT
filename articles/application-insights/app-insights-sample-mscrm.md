---
title: aaaMicrosoft Dynamics CRM e Azure Application Insights | Documenti Microsoft
description: Ottenere i dati di telemetria da Microsoft Dynamics CRM Online tramite Application Insights. Procedura dettagliate relative a installazione, recupero dei dati, visualizzazione ed esportazione.
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Procedura dettagliata: Abilitazione della telemetria per Microsoft Dynamics CRM Online tramite Application Insights
In questo articolo illustra come i dati di telemetria tooget [Microsoft Dynamics CRM Online](https://www.dynamics.com/) utilizzando [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Verranno esaminati procedura completa di hello di aggiunta di Application Insights script tooyour applicazione, l'acquisizione di dati e visualizzazione dei dati.

> [!NOTE]
> [Selezionare la soluzione di esempio hello](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Aggiungere Application Insights toonew o istanza esistente di CRM Online
toomonitor l'applicazione, si aggiunge un'applicazione tooyour Application Insights SDK. Hello SDK invia dati di telemetria toohello [portale Application Insights](https://portal.azure.com), in cui è possibile utilizzare l'analisi potenti e strumenti di diagnostica o esportazione toostorage dati hello.

### <a name="create-an-application-insights-resource-in-azure"></a>Creare una risorsa di Application Insights in Azure
1. Ottenere un [account in Microsoft Azure](http://azure.com/pricing). 
2. Sign in hello [portale di Azure](https://portal.azure.com) e aggiungere una nuova risorsa di Application Insights. in cui i dati verranno elaborati e visualizzati.
   
    ![Clic su +, Servizi per gli sviluppatori, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Scegliere ASP.NET come tipo di applicazione hello.
3. Aprire una pagina della Guida introduttiva hello "monitoraggio e diagnosi lato client".
   
    ![Frammento di codice per l'inserimento nella pagina Web](./media/app-insights-sample-mscrm/03.png)

**Tenere aperto codici hello** mentre si hello il passaggio successivo in un'altra finestra del browser. È necessario codice hello presto. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Creare una risorsa Web JavaScript in Microsoft Dynamics CRM
1. Aprire l'istanza di CRM Online ed eseguire l'accesso con privilegi di amministratore.
2. Aprire Microsoft Dynamics CRM impostazioni, le personalizzazioni, Personalizza hello sistema
   
    ![Impostazioni di Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Impostazioni > Personalizzazioni](./media/app-insights-sample-mscrm/05.png)

    ![Personalizzare l'opzione di sistema hello](./media/app-insights-sample-mscrm/06.png)

1. Creare una risorsa JavaScript.
   
    ![Finestra di dialogo Nuova risorsa Web](./media/app-insights-sample-mscrm/07.png)
   
    Assegnare un nome, seleziona **Script (JScript)** e hello Apri editor di testo.
   
    ![Editor di testo hello aperto](./media/app-insights-sample-mscrm/08.png)
2. Copiare il codice hello da Application Insights. Durante la copia di rendere tooignore che tag di script. Fare riferimento alla schermata illustrata di seguito:
   
    ![Impostare la chiave di strumentazione](./media/app-insights-sample-mscrm/09.png)
   
    codice Hello include una chiave di strumentazione hello che identifica la risorsa di Application insights.
3. Fare clic su Salva e quindi su Pubblica.
   
    ![Fare clic su Salva e quindi su Pubblica](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Form strumentazione
1. In Microsoft CRM Online, aprire il form dell'Account hello
   
    ![Modulo account](./media/app-insights-sample-mscrm/11.png)
2. Aprire il form hello proprietà
   
    ![Proprietà del modulo](./media/app-insights-sample-mscrm/12.png)
3. Aggiungere hello risorsa web JavaScript che è stato creato
   
    ![Menu Aggiungi](./media/app-insights-sample-mscrm/13.png)
   
    ![Aggiungere una risorsa web hello](./media/app-insights-sample-mscrm/14.png)
4. Salvare e pubblicare le personalizzazioni dei form.

## <a name="metrics-captured"></a>Metriche acquisite
Ora impostati acquisizione della telemetria per form hello. Ogni volta che viene utilizzato, verranno inviati dati tooyour risorsa di Application Insights.

Di seguito sono esempi di dati hello che verrà visualizzato.

#### <a name="application-health"></a>Integrità dell'applicazione
![Tempo di caricamento pagina di esempio](./media/app-insights-sample-mscrm/15.png)

![Grafico delle visualizzazioni pagina di esempio](./media/app-insights-sample-mscrm/16.png)

Eccezioni del browser:

![Grafico delle eccezioni del browser](./media/app-insights-sample-mscrm/17.png)

Fare clic su hello grafico tooget dettaglio:

![Elenco delle eccezioni](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Utilizzo
![Utenti, sessioni e visualizzazioni pagine](./media/app-insights-sample-mscrm/19.png)

![Grafici della sessione](./media/app-insights-sample-mscrm/20.png)

![Versioni del browser](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Browser
![Scomposizione del tempo di caricamento della pagina](./media/app-insights-sample-mscrm/22.png)

![Conteggio delle sessioni in base alla versione del browser](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Georilevazione
![Conteggio delle sessioni in base al paese](./media/app-insights-sample-mscrm/24.png)

![Sessioni e utenti in base al paese](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Richieste visualizzazione pagina interna
![Riepilogo della visualizzazione pagina](./media/app-insights-sample-mscrm/26.png)

![Cercare negli eventi della visualizzazione pagina](./media/app-insights-sample-mscrm/27.png)

![Visualizzazioni pagina simili](./media/app-insights-sample-mscrm/28.png)

![Proprietà delle visualizzazioni di pagina](./media/app-insights-sample-mscrm/29.png)

![Pagine per sessione](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Codice di esempio
[Esaminare il codice di esempio hello](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
È possibile eseguire anche un'analisi più approfondita, se si [esportare hello dati tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Soluzione di esempio Microsoft Dynamics CRM
[Di seguito viene implementata in Microsoft Dynamics CRM soluzione di esempio hello](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Altre informazioni
* [Informazioni su Azure Application Insights](app-insights-overview.md)
* [Application Insights per pagine Web](app-insights-javascript.md)
* [Altri esempi e procedure dettagliate](app-insights-code-samples.md)
