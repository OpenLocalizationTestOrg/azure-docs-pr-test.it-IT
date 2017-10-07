---
title: un IoT Hub mediante Azure CLI (az.py) aaaCreate | Documenti Microsoft
description: Come un hub IoT di Azure mediante toocreate hello multipiattaforma CLI di Azure 2.0 (az.py).
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Creazione di un hub IoT utilizzando hello Azure CLI 2.0

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduzione

È possibile utilizzare l'interfaccia CLI di Azure 2.0 (az.py) toocreate e gestire hub IoT di Azure a livello di codice. Questo articolo illustra come toouse hello toocreate CLI di Azure 2.0 (az.py) un hub IoT.

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* [CLI di Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) : hello CLI per hello classic e risorse Gestione modelli di distribuzione.
* Azure CLI 2.0 (az.py) - hello prossima generazione CLI per hello risorse Gestione modello di distribuzione come descritto in questo articolo.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Accedere all'account Azure e impostarlo

Accedi tooyour account Azure e selezionare la sottoscrizione.

1. Al prompt dei comandi di hello, eseguire hello [comando login][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Seguire tooauthenticate istruzioni hello utilizzando codice hello e Accedi tooyour account Azure tramite un web browser.

2. Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello associato con le credenziali dell'account di Azure. Utilizzare la seguente hello [toolist comando hello account Azure] [ lnk-az-account-command] disponibile per toouse è:
    
    ```azurecli
    az account list 
    ```

    Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT. È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Creare un hub IoT

Utilizzare hello Azure CLI toocreate un gruppo di risorse e quindi aggiungere un hub IoT.

1. Quando si crea un hub IoT, è necessario crearlo in un gruppo di risorse. Utilizzare un gruppo di risorse esistente oppure eseguire l'esempio hello [comando toocreate un gruppo di risorse][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > Hello precedente esempio Crea gruppo di risorse hello in hello percorso Stati Uniti occidentali. È possibile visualizzare un elenco di ubicazioni disponibili eseguendo il comando hello `az account list-locations -o table`.
    >
    >

2. Eseguire il seguente hello [comando toocreate un hub IoT] [ lnk-az-iot-command] nel gruppo di risorse, utilizzando un nome univoco globale per l'hub IoT:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> comando precedente Hello crea un hub IoT in hello S1 piano tariffario per il quale verrà addebitato. Per altre informazioni, vedere [Azure IoT Hub Prezzi][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Rimuovere un hub IoT

È possibile utilizzare anche hello Azure CLI[eliminare una singola risorsa][lnk-az-resource-command], ad esempio un hub IoT o elimina un gruppo di risorse e tutte le relative risorse, inclusi tutti gli hub IoT.

toodelete un hub IoT, eseguire hello comando seguente:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete un gruppo di risorse e tutte le relative risorse, hello esecuzione seguente comando:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Passaggi successivi
toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Utilizzo di hello toomanage portale Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
