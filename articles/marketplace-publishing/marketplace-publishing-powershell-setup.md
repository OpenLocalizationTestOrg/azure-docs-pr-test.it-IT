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
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="2063f-103">Configurare Azure PowerShell toocreate un'offerta per hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2063f-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="2063f-104">Per informazioni dettagliate su come tooset di PowerShell in Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2063f-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2063f-105">Un approccio semplice è toouse hello certificato, che scarica e Importa il certificato è necessario per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2063f-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="2063f-106">hello tooobtain necessari certificati, utilizzare hello **Get-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2063f-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="2063f-107">Quando richiesto, salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="2063f-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="2063f-108">certificato di hello tooimport in una sessione di PowerShell, usare hello **Import-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2063f-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="2063f-109">tooconfigure e archivio hello Microsoft Azure sottoscrizione impostazioni comuni per la sessione di PowerShell hello, utilizzare hello **Set-AzureSubscription** e **Select-AzureSubscription** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2063f-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="2063f-110">comando primo Hello associa un account di archiviazione predefinito sottoscrizione hello (necessario per alcune operazioni di provisioning di macchine Virtuali).</span><span class="sxs-lookup"><span data-stu-id="2063f-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="2063f-111">in secondo luogo Hello rende sottoscrizione hello hello quella corrente (riconosciuto da altri cmdlet).</span><span class="sxs-lookup"><span data-stu-id="2063f-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="2063f-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2063f-112">See also</span></span>
* [<span data-ttu-id="2063f-113">Guida introduttiva: come toopublish un toohello offerta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2063f-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="2063f-114">Creazione di un'immagine di macchina virtuale per hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="2063f-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

