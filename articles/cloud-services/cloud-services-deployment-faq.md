---
title: problemi di aaaDeployment per domande frequenti sui servizi Cloud di Microsoft Azure | Documenti Microsoft
description: Questo articolo vengono elencati hello domande frequenti sulla distribuzione per servizi Cloud di Microsoft Azure.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemi di distribuzione per Servizi cloud di Azure: domande frequenti

Questo articolo include le domande frequenti relative ai problemi di distribuzione per [Servizi cloud di Microsoft Azure](https://azure.microsoft.com/services/cloud-services). È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Perché la distribuzione un toohello servizio cloud slot di staging talvolta non riuscire con un errore di allocazione della risorsa se è già presente una distribuzione esistente nello slot di produzione hello?
Se un servizio cloud dispone di una distribuzione in uno slot, hello intero servizio cloud è bloccato tooa specifico cluster. Ciò significa che se una distribuzione già esiste nello slot di produzione hello, una nuova distribuzione di gestione temporanea può essere allocata solo in hello stesso cluster come slot di produzione hello.

Errori di allocazione si verificano quando il cluster hello in cui si trova il servizio cloud non sufficiente fisica toosatisfy risorse di calcolo della richiesta di distribuzione.

Per informazioni su come mitigare gli errori di allocazione, vedere [Errore di allocazione dei servizi cloud: Soluzioni](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Perché il ridimensionamento di una distribuzione dei servizi cloud causa a volte un errore di allocazione?
Quando viene distribuito un servizio cloud, viene in genere aggiunti tooa specifico cluster. Ciò significa che la scalabilità verticale/out a un cloud esistente servizio deve allocare nuove istanze di hello dello stesso cluster. Se il cluster hello sta per raggiungere la capacità o hello desiderate VM/tipo di dimensione non è disponibile, hello richiesta potrebbe non riuscire.

Per informazioni su come mitigare gli errori di allocazione, vedere [Errore di allocazione dei servizi cloud: Soluzioni](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Perché la distribuzione di un servizio cloud in un gruppo di affinità causa a volte un errore di allocazione?
Un nuovo servizio cloud vuoto tooan di distribuzione può essere allocato dall'infrastruttura di hello in un cluster in tale area, a meno che il servizio di cloud hello è il gruppo di affinità tooan bloccati. Le distribuzioni toohello verrà ritentato stesso gruppo di affinità hello dello stesso cluster. Se il cluster hello è quasi capacità, la richiesta hello potrebbe non riuscire.

Per informazioni su come mitigare gli errori di allocazione, vedere [Errore di allocazione dei servizi cloud: Soluzioni](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Motivo per cui la modifica delle dimensioni della macchina virtuale o l'aggiunta di un nuova macchina virtuale tooan servizio cloud esistente talvolta comporta un errore di allocazione?
cluster di Hello in un Data Center possono avere diverse configurazioni di tipi di computer (ad esempio, una serie, serie Av2, serie D, Dv2 serie, serie G, serie H e così via). Ma non tutti i cluster hello necessariamente tutti i tipi di hello di macchine virtuali. Ad esempio, se si tenta di tooadd una serie D servizio cloud VM tooa in cui è già stata distribuita in un cluster di una sola serie, si verificheranno un errore di allocazione. Questo si verifica anche se si tenta di dimensioni toochange VM SKU (ad esempio, il passaggio da una serie di tooa D serie A).

Per informazioni su come mitigare gli errori di allocazione, vedere [Errore di allocazione dei servizi cloud: Soluzioni](cloud-services-allocation-failures.md#solutions).

dimensioni hello toocheck disponibili nella propria area geografica, vedere [Microsoft Azure: i prodotti disponibili per area](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Perché viene la distribuzione di un cloud servizio fail talvolta scadenza toolimits/quote o vincoli di sottoscrizione o del servizio?
Distribuzione di un servizio cloud potrebbe non riuscire se le risorse hello toobe obbligatorio allocata superano predefinito hello o quota massima consentita per il servizio a livello di area o Data Center hello. Per altre informazioni, vedere [Limiti relativi a Servizi cloud](../azure-subscription-service-limits.md#cloud-services-limits).

È anche possibile tenere traccia di hello corrente/quota di utilizzo per la sottoscrizione nel portale di hello: portale di Azure = > sottoscrizioni = > \<appropriati sottoscrizione > = > "Utilizzo + quota".

Informazioni relative all'uso/consumo di risorse possono anche essere recuperate tramite hello le API di fatturazione di Azure. Vedere [API di utilizzo delle risorse di Azure (anteprima)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Come è possibile modificare dimensioni hello di un servizio cloud distribuito macchina virtuale senza ridistribuirla?
È possibile modificare le dimensioni VM hello di un servizio cloud distribuito senza ridistribuirla. Hello dimensioni della macchina virtuale viene compilata in hello CSDEF, che può essere aggiornata solo con una ridistribuzione.

Per ulteriori informazioni, vedere [come un servizio cloud tooupdate](cloud-services-update-azure-service.md).

 
