---
title: bilanciamento del carico con una connessione Internet aaaCreate - modello di Azure | Documenti Microsoft
description: Informazioni su come una connessione Internet toocreate bilanciamento del carico in Gestione risorse di un modello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Creazione di un servizio di bilanciamento del carico Internet mediante l'uso di un modello

> [!div class="op_single_selector"]
> * [Portale](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico utilizzando il modello di distribuzione classica](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Distribuire il modello di hello utilizzando fare clic su toodeploy

modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra. toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](http://go.microsoft.com/fwlink/?LinkId=544801), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.

## <a name="deploy-hello-template-by-using-powershell"></a>Distribuire il modello di hello tramite PowerShell

modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.

1. Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.
2. Eseguire hello **New AzureRmResourceGroupDeployment** toocreate cmdlet un gruppo di risorse utilizzando hello modello.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Distribuire il modello di hello utilizzando hello CLI di Azure

modello di hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.

    ```azurecli
    azure config mode arm
    ```

    Ecco l'output di hello previsto per comando hello sopra indicato:

        info:    New mode is arm

3. Dal browser, passare troppo[hello modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copiare il contenuto di hello del file json hello e incollare in un nuovo file nel computer. Per questo scenario, si sarebbero copiando i valori hello sotto tooa file denominato **c:\lb\azuredeploy.parameters.json**.
4. Eseguire hello **distribuzione gruppo di azure creare** cmdlet toodeploy hello nuovo bilanciamento del carico utilizzando il modello di hello e parametro file scaricato e modificato in precedenza. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
