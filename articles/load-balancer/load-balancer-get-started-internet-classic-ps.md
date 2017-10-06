---
title: con una connessione Internet aaaCreate bilanciamento del carico - PowerShell di Azure classico | Documenti Microsoft
description: "Informazioni su come una connessione Internet toocreate bilanciamento del carico in modalità classica tramite PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Introduzione alla creazione del servizio di bilanciamento del carico Internet (classico) in PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure classico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servizi cloud di Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica. È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure. È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo. Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Configurazione del servizio di bilanciamento del carico con PowerShell

tooset di bilanciamento del carico tramite powershell, attenersi alla procedura hello:

1. Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.
2. Dopo aver creato una macchina virtuale, è possibile utilizzare i cmdlet di PowerShell tooadd una macchina virtuale di tooa del servizio di bilanciamento carico all'interno di hello stesso servizio cloud.

In hello esempio seguente si aggiungerà un set di bilanciamento del carico chiamato toocloud "webfarm" computer "mytestcloud" (o myctestcloud.cloudapp.net), aggiunta di endpoint hello per hello toovirtual bilanciamento di carico del servizio denominato "web1" e "web2". servizio di bilanciamento del carico Hello riceve il traffico di rete sulla porta 80 e bilancia il carico tra le macchine virtuali hello definite da hello endpoint locale (in questo caso porta 80) tramite TCP.

### <a name="step-1"></a>Passaggio 1

Creare un endpoint con carico bilanciato per web1"hello prima macchina virtuale"

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Passaggio 2

Creare un altro endpoint per hello secondo VM "web2" hello utilizzando stesso caricare il nome del set di bilanciamento del carico

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Rimuovere una macchina virtuale dal servizio di bilanciamento del carico

È possibile usare Remove-AzureEndpoint tooremove un endpoint della macchina virtuale dal servizio di bilanciamento del carico hello

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Passaggi successivi

È anche possibile [iniziare a creare un bilanciamento del carico interno](load-balancer-get-started-ilb-classic-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento del traffico di rete per un servizio di bilanciamento del carico specifico.

Se l'applicazione deve tookeep connessioni attive per i server di bilanciamento del carico, è possibile comprendere più su [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md). Quando si utilizza Bilanciamento carico di Azure, questo risulterà utile toolearn sul comportamento di connessione inattiva.
