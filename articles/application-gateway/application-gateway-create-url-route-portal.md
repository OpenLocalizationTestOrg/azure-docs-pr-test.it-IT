---
title: Creare una regola basata sul percorso - Gateway applicazione di Azure - Portale di Azure | Microsoft Docs
description: Informazioni su come creare una regola basata sul percorso per un gateway applicazione tramite il portale
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a>Creare una regola basata sul percorso per un gateway applicazione usando il portale

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-url-route-cli.md)

Il routing basato sul percorso dell'URL consente di associare le route in base al percorso dell'URL della richiesta HTTP. Verifica se è disponibile una route per il pool back-end configurato per l'URL elencato nel gateway applicazione e invia il traffico di rete al pool back-end definito. In genere il routing basato su URL viene usato per le richieste di bilanciamento del carico per diversi tipi di contenuto tra vari pool di server back-end.

Il routing basato su URL introduce un nuovo tipo di regola per i gateway applicazione. Per il gateway applicazione sono disponibili due tipi di regole: di base e basate sul percorso. Il tipo di regola di base fornisce un servizio di tipo round robin per i pool back-end, mentre le regole basate sul percorso, oltre alla distribuzione round robin, tengono conto del modello di percorso dell'URL della richiesta per la scelta del pool back-end.

## <a name="scenario"></a>Scenario

Lo scenario seguente illustra la creazione di una regola basata sul percorso in un gateway applicazione esistente.
Lo scenario presuppone che sia già stata seguita la procedura per [creare un gateway applicazione](application-gateway-create-gateway-portal.md).

![route dell'URL][scenario]

## <a name="createrule"></a>Creare la regola basata sul percorso

Una regola basata sul percorso richiede un proprio listener. Prima di creare la regola, verificare di avere un listener disponibile all'uso.

### <a name="step-1"></a>Passaggio 1

Passare al [portale di Azure](http://portal.azure.com) e selezionare un gateway applicazione esistente. Fare clic su **Regole**

![Panoramica del gateway applicazione][1]

### <a name="step-2"></a>Passaggio 2

Fare clic sul pulsante **Basata sul percorso** per aggiungere una nuova regola di questo tipo.

### <a name="step-3"></a>Passaggio 3

Il pannello **Add path-based rule** (Aggiungi regola basata sul percorso) contiene due sezioni. La prima è la sezione in cui sono stati definiti il listener, il nome della regola e le impostazioni del percorso predefinito. Le impostazioni del percorso predefinite sono per le route che non rientrano nella route personalizzata basata sul percorso. La seconda sezione dl pannello **Add path-based rule** (Aggiungi regola basata sul percorso) viene usata per definire le regole stesse basate sul percorso.

**Basic Settings**

* **Nome**: nome descrittivo della regola accessibile nel portale.
* **Listener** : questo valore è il listener usato per la regola.
* **Default backend pool** (Pool back-end predefinito): questa impostazione definisce il back-end da usare per la regola predefinita.
* **Default HTTP settings** (Impostazioni HTTP predefinite ): questa impostazione definisce le impostazioni HTTP da usare per la regola predefinita.

**Regole basate sul percorso**

* **Nome**: questo valore è un nome descrittivo della regola basata sul percorso.
* **Percorsi** : questa impostazione definisce il percorso cercato dalla regola per l'inoltro del traffico.
* **Pool back-end** : questa impostazione definisce il back-end da usare per la regola.
* **Impostazione HTTP** : questa impostazione definisce le impostazioni HTTP da usare per la regola.

> [!IMPORTANT]
> Percorsi: elenco dei modelli di percorso usati per la corrispondenza. Ognuno deve iniziare con una barra / e l'unica posizione in cui è consentito il carattere "\*" è alla fine. Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.  

![Pannello Add path-based rule (Aggiungi regola basata sul percorso)][2]

L'aggiunta di una regola basata sul percorso a un gateway applicazione esistente è un processo semplice con il portale. Dopo aver creato una regola basata sul percorso, è possibile modificarla per aggiungere altre regole. 

![aggiunta di altre regole basate sul percorso][3]

Questo passaggio configura una route basata sul percorso. È importante comprendere che le richieste non vengono scritte di nuovo: quando arriva una richiesta, il gateway applicazione la controlla e quindi la regola di base sul modello di URL la invia al back-end appropriato.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come configurare l'offload SSL con un gateway applicazione di Azure, vedere [Configurare un gateway applicazione per l'offload SSL con il portale](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
