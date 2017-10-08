---
title: aaaAzure Windows macchina virtuale DotNet Core esercitazione 1 | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a>Automazione delle distribuzioni di applicazioni tooWindows macchine virtuali

Questa serie di quattro articoli descrive in dettaglio la distribuzione e la configurazione di risorse e applicazioni di Azure mediante modelli di Azure Resource Manager. In questa serie, un modello di esempio viene distribuito e hello esaminata modello di distribuzione. obiettivo di Hello di questa serie è tooeducate relazione hello tra le risorse di Azure e tooprovide trasmette sull'esperienza di distribuzione di modelli di Azure Resource Manager completamente integrata. Questo documento presuppone un livello base di conoscenze relative ad Azure Resource Manager. Prima di iniziare questa esercitazione, acquisire familiarità con i concetti fondamentali di Azure Resource Manager.

## <a name="music-store-application"></a>Applicazione Music Store
esempio usato in questa serie Hello è .net application base simulando un negozio esperienza di acquisto. L'applicazione può essere distribuito tooeither un sistema virtuale Linux o Windows create per entrambe le distribuzioni di esempio. un'applicazione Hello include un'applicazione web e un database SQL. Prima di leggere gli articoli di hello in questa serie, distribuire l'applicazione hello utilizzando il pulsante di distribuzione hello presente in questa pagina. Quando è completamente distribuito, hello architettura applicazione / Azure è simile a hello seguente diagramma. 

è disponibile in questo caso, il modello di gestione risorse di archiviazione musica Hello [musica modello di Windows Store](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Applicazione Music Store](./media/dotnet-core-1-landing/music-store.png)

Ognuno di questi componenti, tra cui hello associare un modello JSON viene esaminato in hello seguenti quattro articoli.

* [**Architettura dell'applicazione** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : i componenti dell'applicazione, ad esempio siti web e database è necessario toobe ospitato nelle risorse del computer di Azure quali macchine virtuali e database SQL di Azure. Questo documento descrive come l'esigenza di calcolo di mapping, tooAzure risorse e la distribuzione di tali risorse con un modello di gestione risorse di Azure. 
* [**Accesso e protezione** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : durante l'hosting di applicazioni in Azure, è necessario tooconsider come avviene applicazione hello e come accedere ai componenti diversi dell'applicazione tra loro. Questo documento illustra in dettaglio fornendo e la protezione di internet accesso tooan accesso alle applicazioni e tra i componenti dell'applicazione.
* [**Disponibilità e scalabilità** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : disponibilità e scalabilità riferimento toohello toostay di possibilità di applicazioni in esecuzione durante i tempi di inattività dell'infrastruttura e hello possibilità tooscale richiesta applicazione toomeet di risorse di calcolo. Componenti di hello dettagli in questo documento è necessario toodeploy con bilanciamento del carico e delle applicazioni a disponibilità elevata.
* [**Distribuzione di applicazioni** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : quando è necessario considerare la distribuzione di applicazioni in macchine virtuali di Azure, il metodo hello per cui hello file binari dell'applicazione vengono installati nella macchina virtuale hello. Questo documento descrive come automatizzare l'installazione di applicazioni mediante le estensioni script personalizzate per le macchine virtuali di Azure.

obiettivo di Hello durante lo sviluppo di modelli di gestione risorse di Azure è la distribuzione di hello tooautomate dell'infrastruttura di Azure e installazione hello e configurazione di tutte le applicazioni ospitate in questa infrastruttura di Azure. Le informazioni riportate in questi articoli offrono un esempio di questa esperienza.

## <a name="deploy-hello-music-store-application"></a>Distribuire un'applicazione hello musica archivio
applicazione di archiviazione di file musicali Hello può essere distribuito tramite questo pulsante.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

modello di Azure Resource Manager Hello richiede hello seguente i valori dei parametri.

| Nome parametro | Description |
| --- | --- |
| ADMINUSERNAME |Nome utente amministratore viene utilizzata nella macchina virtuale hello e hello Database SQL di Azure. |
| ADMINPASSWORD |Password utilizzata nella macchina virtuale di Azure hello e il Database SQL. |
| NUMBEROFINSTANCES |numero di Hello di macchine virtuali toobe creato. Ognuno di tali applicazioni web, macchine virtuali host hello Negozio e tutto il traffico viene bilanciato tra loro. |
| PUBLICIPADDRESSDNSNAME |Nome DNS univoco globale associato all'indirizzo IP pubblico hello. |

Quando è stata completata la distribuzione dei modelli di hello, passare toohello l'indirizzo IP pubblico di usando qualsiasi browser internet. Hello .net Core musica sito verrà visualizzata.

## <a name="next-steps"></a>Passaggi successivi
<hr>

[Passaggio 1: Architettura delle applicazioni con i modelli di Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Passaggio 2: Accesso e sicurezza nei modelli di Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Passaggio 3: Disponibilità e scalabilità nei modelli di Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Passaggio 4: Distribuzione di applicazioni con i modelli di Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

