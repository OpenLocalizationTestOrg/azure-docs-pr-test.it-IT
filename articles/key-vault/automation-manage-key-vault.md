---
title: aaaManage insieme credenziali chiavi Azure utilizzando l'automazione di Azure | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage insieme credenziali chiavi Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="d93e5-103">Gestione dell'insieme di credenziali chiave usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d93e5-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="d93e5-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione delle chiavi e segreti nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="d93e5-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="d93e5-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d93e5-105">What is Azure Automation?</span></span>
<span data-ttu-id="d93e5-106">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi e la configurazione preferita per lo stato.</span><span class="sxs-lookup"><span data-stu-id="d93e5-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="d93e5-107">Attività manuali ripetute, con esecuzione prolungata e soggetta a errori utilizzando l'automazione di Azure, può essere automatizzata tooincrease affidabilità, efficienza e toovalue tempo per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="d93e5-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d93e5-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="d93e5-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="d93e5-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="d93e5-110">Liberare e ridurre i costi operativi IT e DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d93e5-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="d93e5-111">In che modo è possibile gestire l'insieme di credenziali chiave di Azure con Automazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="d93e5-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="d93e5-112">Insieme di credenziali chiave possono essere gestiti in automazione di Azure con hello [i cmdlet di Azure Resource Manager insieme di credenziali chiave](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [i cmdlet di Azure classico insieme di credenziali di chiave](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="d93e5-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="d93e5-113">Hello modulo Azure per gestire l'insieme di credenziali chiave classico è disponibile automaticamente in automazione di Azure ed è possibile importare hello [modulo di Azure Resource Manager KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in automazione di Azure, in modo che è possibile eseguire molte della gestione dell'insieme di credenziali chiave attività all'interno del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="d93e5-114">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="d93e5-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="d93e5-115">I cmdlet di hello insieme credenziali chiavi Azure è possibile eseguire queste attività tra gli altri:</span><span class="sxs-lookup"><span data-stu-id="d93e5-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="d93e5-116">Creare e configurare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d93e5-116">Create and configure a key vault</span></span>
* <span data-ttu-id="d93e5-117">Creare o importare una chiave</span><span class="sxs-lookup"><span data-stu-id="d93e5-117">Create or import a key</span></span>
* <span data-ttu-id="d93e5-118">Creare o aggiornare un segreto</span><span class="sxs-lookup"><span data-stu-id="d93e5-118">Create or update a secret</span></span>
* <span data-ttu-id="d93e5-119">Aggiornare gli attributi di una chiave</span><span class="sxs-lookup"><span data-stu-id="d93e5-119">Update attributes of a key</span></span>
* <span data-ttu-id="d93e5-120">Ottenere una chiave o un segreto</span><span class="sxs-lookup"><span data-stu-id="d93e5-120">Get a key or secret</span></span>
* <span data-ttu-id="d93e5-121">Eliminare una chiave o un segreto</span><span class="sxs-lookup"><span data-stu-id="d93e5-121">Delete a key or secret</span></span>

<span data-ttu-id="d93e5-122">Ecco alcuni esempi di utilizzo di PowerShell toomanage insieme di credenziali chiave:</span><span class="sxs-lookup"><span data-stu-id="d93e5-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="d93e5-123">Insieme di credenziali delle chiavi di Azure - Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="d93e5-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="d93e5-124">Installazione e configurazione di un insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d93e5-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="d93e5-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d93e5-125">Next steps</span></span>
<span data-ttu-id="d93e5-126">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage insieme di credenziali chiave di Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d93e5-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="d93e5-127">Vedere hello automazione di Azure [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="d93e5-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="d93e5-128">Vedere hello [insieme di credenziali chiave di Azure PowerShell script](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="d93e5-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

