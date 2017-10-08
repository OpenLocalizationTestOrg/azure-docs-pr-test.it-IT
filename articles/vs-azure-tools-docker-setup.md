---
title: un Host Docker con VirtualBox aaaConfigure | Documenti Microsoft
description: Istruzioni dettagliate tooconfigure Docker predefinito dell'istanza tramite Docker macchina e VirtualBox
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Configurare un Host Docker con VirtualBox
## <a name="overview"></a>Panoramica
Questo articolo consente di configurare un'istanza di Docker predefinita usando Docker Machine e VirtualBox. Se si usa hello [Docker per Windows beta](http://beta.docker.com/), questa configurazione non è necessaria.

## <a name="prerequisites"></a>Prerequisiti
Hello seguenti strumenti necessario toobe installato.

* [Docker Toolbox](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Configurazione del client di Docker hello con Windows PowerShell
un client di Docker, tooconfigure semplicemente aprire Windows PowerShell ed eseguire hello alla procedura seguente:

1. Creare un'istanza di host docker predefinita.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Verificare l'istanza predefinita di hello è configurato e in esecuzione. Verrà visualizzata un'istanza denominata `default' in esecuzione.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. Impostare il valore predefinito come host corrente hello e configurare la shell.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Visualizzare i contenitori di Docker active hello. elenco di Hello deve essere vuoto.
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> Ogni volta che si riavvia il computer di sviluppo, è necessario toorestart all'host docker locale.
> toodo hello, questo problema comando al prompt di comando seguente: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
