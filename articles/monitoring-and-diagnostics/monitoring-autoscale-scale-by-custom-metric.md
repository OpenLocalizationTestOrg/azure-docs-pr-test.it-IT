---
title: "aaaGet avviata con scalabilità automatica da metrica personalizzata in Azure | Documenti Microsoft"
description: Informazioni su come tooscale la risorsa in base alla metrica personalizzata in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Introduzione alla scalabilità automatica in base a una metrica personalizzata in Azure
Questo articolo viene descritto come tooscale la risorsa da una metrica personalizzata nel portale di Azure.

Azure ridimensionamento automatico di monitoraggio si applica solo tooVirtual set di scalabilità macchina (VMSS), servizi cloud, piani di servizio app e gli ambienti del servizio app. 

# <a name="lets-get-started"></a>Introduzione
In questo articolo si presuppone che l'utente abbia un'app Web con Application Insights configurato. Se non è già stato fatto, è possibile [configurare Application Insights per il sito Web ASP.NET][1].

- Aprire il [portale di Azure][2]
- Fare clic sull'icona di monitoraggio di Azure nel riquadro di spostamento sinistro hello.
  ![Avviare Monitoraggio di Azure][3]
- Fare clic su impostazioni tooview tutte le risorse di hello per cui automaticamente la scala è applicabile, e il relativo stato corrente di scalabilità automatica di scalabilità automatica ![individuare il ridimensionamento automatico in monitor di Azure][4]
- Aprire Pannello 'Autoscale' in Monitoraggio di Azure e selezionare una risorsa che si desidera tooscale
> Nota: procedura hello utilizza un piano di servizio app associato a un'app web che ha configurati informazioni di app.
- Nel Pannello di impostazione hello scala per la risorsa hello, si noti che il numero di istanze correnti di hello è 1. Fare clic su 'Abilita scalabilità automatica'.
  ![Impostazione di scalabilità per la nuova app Web][5]
- Fornire un nome per l'impostazione di scala di hello e hello fare clic su "Aggiungi una regola di". Si noti hello regola le opzioni della scala che viene visualizzata come riquadro contesto sul lato destro di hello. Per impostazione predefinita, imposta l'istanza 1 conteggio se hello CPU percetage della risorsa hello è superiore al 70% di hello opzione tooscale. Origine della metrica hello modifica nella parte superiore di hello troppo "Application Insights", selezionare hello risorse insights app nell'elenco a discesa 'Resource' hello e metrica personalizzata di hello quindi in base in cui si desidera tooscale.
  ![Ridimensionare in base a una metrica personalizzata][6]
- Passaggio di toohello simile precedente, aggiungere una regola di scala che scalabilità e ridurre il numero di scala hello di 1 se la metrica personalizzata hello è inferiore alla soglia.
  ![Scalabilità in base alla CPU][7]
- Impostare i limiti dell'istanza hello. Ad esempio, se si desidera tooscale tra 2 e 5 istanze a seconda delle fluttuazioni metrica personalizzata hello, impostare 'minimo' troppo '2', 'massimo' troppo '5' e 'default' troppo '2'
> Nota: nel caso in cui si verifica un problema durante la lettura delle metriche delle risorse hello e capacità corrente hello è di sotto di capacità predefinita hello, quindi la disponibilità di hello tooensure della risorsa di hello, scalabilità automatica verranno scalabilità toohello predefinita. Se la capacità corrente hello è superiore alla capacità predefinita, la scalabilità automatica non verranno scalare.
- Fare clic su 'Salva'

A questo punto È ora la scala, l'impostazione di app web in base a una metrica personalizzata tooauto scala creato correttamente.

> Nota: hello stessi passaggi sono applicabili tooget avviato con un ruolo del servizio VMSS o cloud.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
