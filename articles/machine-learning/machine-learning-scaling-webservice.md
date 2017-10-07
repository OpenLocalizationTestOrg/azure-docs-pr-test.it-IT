---
title: concorrenza tooincrease aaaHow di un servizio web Azure Machine Learning | Documenti Microsoft
description: Informazioni su come concorrenza tooincrease un Azure Machine Learning servizio web tramite l'aggiunta di altri endpoint.
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure machine learning, servizi Web, messa in funzione, scalabilità, endpoint, concorrenza"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Ridimensionamento di un servizio Web di Azure Machine Learning con l'aggiunta di altri endpoint
> [!NOTE]
> Questo argomento vengono descritte le tecniche applicabile tooa **classico** servizio Web di Machine Learning. 
> 
> 

Per impostazione predefinita, ogni servizio Web pubblicato toosupport configurato 20 richieste simultanee e può essere a un massimo di 200 richieste simultanee. Hello portale di Azure classico offre un modo tooset questo valore, Azure Machine Learning consente di ottimizzare automaticamente hello impostazione tooprovide hello migliori prestazioni per il servizio web e hello portale valore viene ignorato. 

Se si prevede di API hello toocall con un carico superiore al valore Max Concurrent Calls 200 supporterà, è necessario creare più endpoint in hello stesso servizio Web. È quindi possibile distribuire casualmente il carico tra tutti gli endpoint.

Hello il ridimensionamento di un servizio Web è un'attività comune. Tooscale alcuni motivi sono toosupport più di 200 richieste simultanee, aumentare la disponibilità tramite più endpoint o fornire endpoint separati per il servizio web hello. È possibile aumentare la scalabilità hello aggiungendo altri endpoint per hello stesso servizio Web tramite [portale di Azure classico](https://manage.windowsazure.com/) o hello [servizio Web di Azure Machine Learning](https://services.azureml.net/) portale.

Per altre informazioni sull'aggiunta di nuovi endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md).

Tenere presente che può essere negativo se non si chiama hello API con una frequenza elevata di conseguenza utilizzando un numero elevato di concorrenza. Se si inserisce un carico relativamente ridotto in un'API configurata per un carico elevato, è possibile visualizzare i timeout sporadici e/o picchi di latenza hello.

Hello che sincrone API vengono in genere utilizzate in situazioni in cui si desidera una bassa latenza. Latenza qui implica tempo hello necessario per l'API di hello toocomplete una richiesta e non viene tenuto in considerazione i ritardi di rete. Si supponga di avere un'API con una latenza di 50 ms. toofully utilizzare la capacità disponibile hello con livello di velocità elevata e Max Concurrent Calls = 20, è necessario toocall questa API 20 * 1000 / = 400 50 volte al secondo. Questa estensione ulteriormente, un numero massimo di chiamate simultanee pari a 200 consente si toocall hello API 4000 volte al secondo, presupponendo una latenza di 50 ms.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
