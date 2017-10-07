---
title: registri aaaManage rete sicurezza gruppo flusso con il Watcher di rete di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come flusso del gruppo di sicurezza di rete toomanage accede Watcher di rete di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Gestire i registri del flusso di rete sicurezza gruppo nel portale di Azure hello

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Registri flusso gruppo di sicurezza rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete. Questi log di flusso sono scritti in formato JSON e contengono informazioni importanti, tra cui: 

- Flussi in ingresso e in uscita in base a ciascuna regola.
- scheda di rete che hello flusso Hello si applica a.
- 5 tuple informazioni sul flusso di hello (origine/destinazione IP, porta di origine/destinazione, protocol).
- Indica se il traffico è stato consentito o negato.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un'istanza del controllo di rete](network-watcher-create.md). scenario di Hello si presuppone inoltre che si dispone di un gruppo di risorse con una macchina virtuale valida.

## <a name="register-insights-provider"></a>Registrare il provider di Insight

Per il flusso di registrazione toowork hello correttamente, **Insights** provider deve essere registrato. provider di hello tooregister, hello take alla procedura seguente: 

1. Andare troppo**sottoscrizioni**, quindi selezionare hello sottoscrizione per cui si desidera tooenable flusso registri. 
2. In hello **sottoscrizione** pannello seleziona **i provider di risorse**. 
3. Esaminare hello elenco dei provider e verificare che hello **Insights** provider è registrato. In caso contrario selezionare **Registra**.

![Visualizzare i provider][providers]

## <a name="enable-flow-logs"></a>Abilitare i log di flusso

Questi passaggi vengono illustrati il processo di hello di abilitazione del flusso di log in un gruppo di sicurezza di rete.

### <a name="step-1"></a>Passaggio 1

Passare l'istanza di tooa Watcher di rete e quindi selezionare **NSG flusso registra**.

![Panoramica dei log di flusso][1]

### <a name="step-2"></a>Passaggio 2

Selezionare un gruppo di sicurezza di rete dall'elenco di hello.

![Panoramica dei log di flusso][2]

### <a name="step-3"></a>Passaggio 3 

In hello **delle impostazioni dei log flusso** pannello, impostare lo stato di hello troppo**su**e quindi configurare un account di archiviazione.  Al termine, fare clic su **OK**. Selezionare quindi **Salva**.

![Panoramica dei log di flusso][3]

## <a name="download-flow-logs"></a>Scaricare i log di flusso

I log di flusso vengono salvati in un account di archiviazione. Scaricare il tooview registri flusso li.

### <a name="step-1"></a>Passaggio 1

Selezionare i log di flusso, toodownload **è possibile scaricare i log di flusso dagli account di archiviazione configurato**. Questo passaggio consente di visualizzare account di archiviazione tooa in cui è possibile scegliere quali toodownload log.

![Impostazioni dei log di flusso][4]

### <a name="step-2"></a>Passaggio 2

Passare toohello account di archiviazione corretto. Selezionare quindi **Contenitori** > **insights-log-networksecuritygroupflowevent**.

![Impostazioni dei log di flusso][5]

### <a name="step-3"></a>Passaggio 3

Passare toohello del percorso del Registro di flusso hello, selezionarlo e quindi selezionare **scaricare**.

![Impostazioni dei log di flusso][6]

Per informazioni sulla struttura di hello del log di hello, visitare [Cenni preliminari sul registro del flusso di rete sicurezza gruppo](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
