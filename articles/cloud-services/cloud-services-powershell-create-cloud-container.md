---
title: un contenitore del servizio cloud con PowerShell aaaCreate | Documenti Microsoft
description: Questo articolo spiega come toocreate un cloud servizio contenitore con PowerShell. contenitore Hello ospita i ruoli web e di lavoro.
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Utilizzare un toocreate di comando di PowerShell di Azure un contenitore del servizio cloud vuoto
Questo articolo spiega come tooquickly creare un contenitore di servizi Cloud utilizzando i cmdlet PowerShell di Azure. Eseguire le operazioni di hello seguenti:

1. Installare i cmdlet di Microsoft Azure PowerShell hello da hello [Scarica Azure PowerShell](http://aka.ms/webpi-azps) pagina.
2. Aprire il prompt dei comandi di PowerShell hello.
3. Hello utilizzare [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.

   > [!NOTE]
   > Per ulteriori istruzioni sull'installazione di cmdlet di Azure PowerShell hello e connessione tooyour sottoscrizione di Azure, vedere troppo[come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Hello utilizzare **New-AzureService** toocreate cmdlet un contenitore di servizi cloud di Azure vuoto.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Eseguire questo cmdlet hello tooinvoke di esempio:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Per ulteriori informazioni sulla creazione del servizio cloud di Azure hello, eseguire:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Passaggi successivi
* hello toomanage distribuzione del servizio cloud, vedere toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandi. È possibile anche fare riferimento troppo[come servizi cloud tooconfigure](cloud-services-how-to-configure.md) per ulteriori informazioni.
* toopublish il servizio cloud tooAzure del progetto, fare riferimento toohello **PublishCloudService.ps1** nell'esempio di codice da [la distribuzione continua per il servizio cloud in Azure](cloud-services-dotnet-continuous-delivery.md).
