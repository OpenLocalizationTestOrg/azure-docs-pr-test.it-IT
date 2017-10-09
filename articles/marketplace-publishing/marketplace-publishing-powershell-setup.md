---
title: aaaSet di PowerShell toocreate una macchina virtuale per hello Marketplace | Documenti Microsoft
description: Le istruzioni per configurare Azure PowerShell e utilizzarlo come un'opzione facoltativa elabora toocreate VM immagini toodeploy, flusso e vendono su, hello Azure Marketplace
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Configurare Azure PowerShell toocreate un'offerta per hello Azure Marketplace
Per informazioni dettagliate su come tooset di PowerShell in Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Un approccio semplice è toouse hello certificato, che scarica e Importa il certificato è necessario per l'autenticazione. hello tooobtain necessari certificati, utilizzare hello **Get-AzurePublishSettingsFile** cmdlet. Quando richiesto, salvare file hello. certificato di hello tooimport in una sessione di PowerShell, usare hello **Import-AzurePublishSettingsFile** cmdlet.

tooconfigure e archivio hello Microsoft Azure sottoscrizione impostazioni comuni per la sessione di PowerShell hello, utilizzare hello **Set-AzureSubscription** e **Select-AzureSubscription** cmdlet:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

comando primo Hello associa un account di archiviazione predefinito sottoscrizione hello (necessario per alcune operazioni di provisioning di macchine Virtuali).  in secondo luogo Hello rende sottoscrizione hello hello quella corrente (riconosciuto da altri cmdlet).

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)
* [Creazione di un'immagine di macchina virtuale per hello Marketplace](marketplace-publishing-vm-image-creation.md)

