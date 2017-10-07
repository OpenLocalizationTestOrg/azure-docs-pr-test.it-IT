---
title: un percorso basato su aaaCreate regola - Gateway applicazione Azure - portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate una regola basata sul percorso per un gateway applicazione utilizzando hello portale
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Creare una regola basata sul percorso per un gateway applicazione tramite il portale di hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-url-route-cli.md)

Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello della richiesta Http. Controlla se è presente un pool di back-end tooa route configurato per l'URL di hello elencato nel Gateway applicazione hello e invia toohello il traffico di rete hello è definito il pool back-end. Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.

Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola. Per il gateway applicazione sono disponibili due tipi di regole: di base e basate sul percorso. Hello il tipo di regola di base, fornisce il servizio di round robin per hello back-end pool durante il percorso basato su regole inoltre distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end appropriata hello.

## <a name="scenario"></a>Scenario

Hello nello scenario seguente passa attraverso la creazione di una regola basata sul percorso in un gateway applicazione esistente.
Hello scenario si presuppone che siano state già seguite passaggi hello troppo[creare un Gateway applicazione](application-gateway-create-gateway-portal.md).

![route dell'URL][scenario]

## <a name="createrule"></a>Crea regola di percorso basato su hello

Una regola di percorso richiede il proprio listener, prima di creare la regola hello essere tooverify che si dispone di un toouse listener disponibili.

### <a name="step-1"></a>Passaggio 1

Passare toohello [portale di Azure](http://portal.azure.com) e selezionare un gateway applicazione esistente. Fare clic su **Regole**

![Panoramica del gateway applicazione][1]

### <a name="step-2"></a>Passaggio 2

Fare clic su **basato sul percorso** pulsante tooadd una nuova regola percorso.

### <a name="step-3"></a>Passaggio 3

Hello **Aggiungi regola di percorso basato su** blade dispone di due sezioni. Hello prima sezione è in cui è definito listener hello, il nome di hello della regola hello e le impostazioni del percorso predefinito hello. impostazioni del percorso predefinito Hello sono per le route che non rientrano hello basato sul percorso della route personalizzato. seconda sezione di hello Hello **Aggiungi regola di percorso basato su** blade viene usata per definire le regole basate sul percorso hello personalmente.

**Basic Settings**

* **Nome** -questo valore è una regola di toohello nome descrittivo che sia accessibile nel portale di hello.
* **Listener** -questo valore è listener hello utilizzato per la regola di hello.
* **Predefinito pool back-end** -questa impostazione è hello definisce hello toobe di back-end utilizzato per la regola predefinita hello
* **Impostazioni HTTP predefinite** -questa impostazione è hello definisce hello HTTP impostazioni toobe utilizzato per la regola predefinita hello.

**Regole basate sul percorso**

* **Nome** -questo valore è una regola basata su toopath nome descrittivo.
* **Percorsi** -questa impostazione definisce hello percorso hello regola Cerca per l'inoltro del traffico
* **Pool back-end** -questa impostazione è hello definisce hello toobe di back-end utilizzato per la regola hello
* **Le impostazioni HTTP** -questa impostazione è hello definisce hello HTTP impostazioni toobe utilizzato per la regola hello.

> [!IMPORTANT]
> Percorsi: elenco hello di toomatch modelli percorso. Ogni deve iniziare con / e hello solo un "\*" è consentita al fine di hello. Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.  

![Pannello Add path-based rule (Aggiungi regola basata sul percorso)][2]

Aggiunta di una regola basata sul percorso di tooan gateway applicazione esistente è un processo semplice tramite il portale di hello. Dopo aver creata una regola di percorso, può essere modificato tooadd altre regole. 

![aggiunta di altre regole basate sul percorso][3]

Questo passaggio configura una route basata sul percorso. È importante toounderstand che le richieste vengono riscritti non, come le richieste provengano in gateway applicazione controlla richiesta hello e basic hello url modello invia hello richiesta toohello appropriata back-end.

## <a name="next-steps"></a>Passaggi successivi

toolearn tooconfigure offload SSL con Gateway applicazione Azure, vedere [configurare Offload SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
