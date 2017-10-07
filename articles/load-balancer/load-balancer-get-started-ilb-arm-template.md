---
title: aaaCreate un bilanciamento del carico interno - modello di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico utilizzando un modello di gestione risorse
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>Creare un servizio di bilanciamento del carico interno usando un modello

> [!div class="op_single_selector"]
> * [Portale di Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Distribuire il modello di hello utilizzando fare clic su toodeploy

modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra. toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.

## <a name="deploy-hello-template-by-using-powershell"></a>Distribuire il modello di hello tramite PowerShell

modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.

1. Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.
2. Scaricare disco locale tooyour hello parametri file.
3. Modificare il file hello e salvarlo.
4. Eseguire hello **New AzureRmResourceGroupDeployment** toocreate cmdlet un gruppo di risorse utilizzando hello modello.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
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

3. Aprire il file di parametro hello, selezionare il contenuto e salvarlo tooa file nel computer. Per questo esempio, sono stati salvati i file di parametri hello troppo*parameters.json*.
4. Eseguire hello **distribuzione gruppo di azure creare** toodeploy hello nuovo bilanciamento del carico interno utilizzando il modello di hello e parametro di comando file scaricato e modificato in precedenza. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

