---
title: aaaScale di un'app in Azure | Documenti Microsoft
description: "Informazioni su come tooscale di un'app in capacità tooadd di servizio App di Azure e funzionalità."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Aumentare le prestazioni di un'app in Azure
In questo articolo illustra come tooscale l'app in Azure App Service. Sono disponibili due flussi di lavoro per la scala di scalabilità, backup e la scalabilità orizzontale e in questo articolo illustra hello scala il flusso di lavoro.

* [Aumentare le prestazioni](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): è possibile ottenere più CPU, memoria, spazio su disco e altre funzionalità, ad esempio macchine virtuali dedicate, domini e certificati personalizzati, slot di staging, ridimensionamento automatico e altro ancora. È la scalabilità verticale modificando hello piano tariffario del piano di servizio App dell'app a cui appartiene.
* [Scalabilità orizzontale](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentare il numero di hello di istanze di macchine Virtuali che eseguono l'app.
  È possibile scalare orizzontalmente tooas molte istanze di 20, a seconda del livello di prezzo. [Gli ambienti del servizio app](../app-service/app-service-app-service-environments-readme.md) in **Premium** livello faranno ulteriormente aumentare le istanze di too50 conteggio di scalabilità orizzontale. Per altre informazioni sull'aumento del numero di istanze, vedere [Ridimensionare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md). Sono disponibili come il ridimensionamento automatico toouse, ovvero il numero di istanze tooscale automaticamente in base a regole predefinite e le pianificazioni di out.

scala impostazioni accettano solo secondi tooapply Hello e influiscono su tutte le app nel [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Non richiedono toochange è il codice o distribuire nuovamente l'applicazione.

Per informazioni sui prezzi hello e le funzionalità dei singoli piani di servizio App, vedere [dettagli prezzi del servizio App](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Prima di passare un piano di servizio App a hello **libero** livello, è necessario innanzitutto rimuovere hello [i limiti di spesa](https://azure.microsoft.com/pricing/spending-limits/) sul posto per la sottoscrizione di Azure. tooview o modificare le opzioni per la sottoscrizione di Microsoft Azure App Service, vedere [sottoscrizioni di Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Passare al piano tariffario superiore
1. Nel browser aprire hello [portale di Azure][portal].
2. Nel pannello dell'app fare clic su **Tutte le impostazioni** e quindi su **Aumenta prestazioni**.
   
    ![Passare tooscale backup dell'app di Azure.][ChooseWHP]
3. Scegliere il livello e quindi fare clic su **Seleziona**.
   
    Hello **notifiche** scheda lampeggia una verde **successo** al termine dell'operazione di hello.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Risorse correlate alla scalabilità
Se l'applicazione dipende da altri servizi, ad esempio database SQL o Archiviazione di Azure, è anche possibile aumentare le prestazioni di tali risorse in base alle esigenze. Queste risorse non vengono ridimensionate con il piano di servizio App hello e devono essere scalate separatamente.

1. In **Essentials**, fare clic su hello **gruppo di risorse** collegamento.
   
    ![Aumentare le prestazioni delle risorse correlate all'app di Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. In hello **riepilogo** fa parte di hello **gruppo di risorse** pannello, fare clic su una risorsa che si desidera tooscale. Hello seguente schermata mostra una risorsa del Database SQL e una risorsa di archiviazione di Azure.
   
    ![Passare tooresource gruppo blade tooscale backup dell'app di Azure](./media/web-sites-scale/ResourceGroup.png)
3. Per una risorsa del Database SQL, fare clic su **impostazioni** > **tariffario** hello tooscale piano tariffario.
   
    ![Applicare la scalabilità verticale hello Database di SQL back-end per l'app Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Per l'istanza di database SQL è anche possibile attivare la [replica geografica](../sql-database/sql-database-geo-replication-overview.md) .
   
    Per una risorsa di archiviazione di Azure, fare clic su **impostazioni** > **configurazione** tooscale le opzioni di archiviazione.
   
    ![Applicare la scalabilità verticale account di archiviazione di Azure hello usato dalla tua app di Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Informazioni sulle funzionalità per sviluppatori
A seconda di hello a livello di prezzo, hello orientate agli sviluppatori funzionalità seguenti sono disponibili:

### <a name="bitness"></a>Numero di bit
* Hello **base**, **Standard**, e **Premium** livelli supportano applicazioni a 32 e 64 bit.
* Hello **libero** e **Shared** piano livelli supportano solo applicazioni a 32 bit.

### <a name="debugger-support"></a>Supporto del debugger
* Supporto del debugger è disponibile per hello **libero**, **Shared**, e **base** modalità di una connessione per ogni piano di servizio App.
* Supporto del debugger è disponibile per hello **Standard** e **Premium** modalità di cinque connessioni simultanee per piano di servizio App.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Informazioni sulle altre funzionalità
* Per informazioni dettagliate su tutti i rimanenti funzionalità nel servizio App hello hello piani, inclusi i prezzi e le funzioni di utenti di interesse tooall (inclusi gli sviluppatori), vedere [dettagli prezzi del servizio App](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/) in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Passaggi successivi
* tooget introduttiva di Azure, vedere [versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Per informazioni sui prezzi, supporto e contratto di servizio, visitare hello seguenti collegamenti.
  
    [Dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Piani di supporto per Azure](https://azure.microsoft.com/support/plans/)
  
    [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/)
  
    [Dettagli prezzi - Database SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Dimensioni delle macchine virtuali e dei servizi cloud per Microsoft Azure][vmsizes]
  
    [Dettagli prezzi del servizio app](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Dettagli prezzi del servizio app - Connessioni SSL](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Per informazioni sulle procedure consigliate per Servizio app di Azure, inclusa la creazione di un'architettura scalabile e resiliente, vedere il post di blog relativo alle [procedure consigliate per le app Web del servizio app di Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Per i video sulla scalabilità delle app di servizio App, vedere hello seguenti risorse:
  
  * [Quando siti Web di Azure - con Stefan Schackow tooScale](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Scalabilità automatica per i siti Web di Azure, pianificata o in base alla CPU - con Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Che cosa accade durante il ridimensionamento dei siti Web di Azure - con Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
