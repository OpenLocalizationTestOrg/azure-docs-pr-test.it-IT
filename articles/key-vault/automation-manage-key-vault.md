---
title: Gestire l'insieme di credenziali delle chiavi di Azure usando Automazione di Azure | Microsoft Docs
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire l'insieme di credenziali chiave di Azure."
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
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="715c7-103">Gestione dell'insieme di credenziali chiave usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="715c7-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="715c7-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione delle chiavi e dei segreti nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="715c7-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="715c7-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="715c7-105">What is Azure Automation?</span></span>
<span data-ttu-id="715c7-106">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi e la configurazione preferita per lo stato.</span><span class="sxs-lookup"><span data-stu-id="715c7-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="715c7-107">Usando Automazione di Azure, è possibile automatizzare attività manuali, ripetute, a esecuzione prolungata e soggette a errori per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="715c7-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="715c7-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="715c7-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="715c7-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="715c7-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="715c7-110">Il servizio consente di ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="715c7-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="715c7-111">In che modo è possibile gestire l'insieme di credenziali chiave di Azure con Automazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="715c7-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="715c7-112">L'insieme di credenziali delle chiavi può essere gestito in Automazione di Azure usando i [cmdlet per l'insieme di credenziali delle chiavi di AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e i [cmdlet per l'insieme di credenziali delle chiavi di Azure classico](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="715c7-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="715c7-113">Il modulo Azure per la gestione dell'insieme di credenziali delle chiavi classico è disponibile automaticamente in Automazione di Azure ed è possibile importare il [modulo per l'insieme di credenziali delle chiavi di AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in Automazione di Azure, in modo da poter eseguire molte delle attività di gestione dell'insieme di credenziali delle chiavi all'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="715c7-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="715c7-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="715c7-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="715c7-115">Con i cmdlet dell'insieme di credenziali delle chiavi di Azure è possibile eseguire, ad esempio, queste attività:</span><span class="sxs-lookup"><span data-stu-id="715c7-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="715c7-116">Creare e configurare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="715c7-116">Create and configure a key vault</span></span>
* <span data-ttu-id="715c7-117">Creare o importare una chiave</span><span class="sxs-lookup"><span data-stu-id="715c7-117">Create or import a key</span></span>
* <span data-ttu-id="715c7-118">Creare o aggiornare un segreto</span><span class="sxs-lookup"><span data-stu-id="715c7-118">Create or update a secret</span></span>
* <span data-ttu-id="715c7-119">Aggiornare gli attributi di una chiave</span><span class="sxs-lookup"><span data-stu-id="715c7-119">Update attributes of a key</span></span>
* <span data-ttu-id="715c7-120">Ottenere una chiave o un segreto</span><span class="sxs-lookup"><span data-stu-id="715c7-120">Get a key or secret</span></span>
* <span data-ttu-id="715c7-121">Eliminare una chiave o un segreto</span><span class="sxs-lookup"><span data-stu-id="715c7-121">Delete a key or secret</span></span>

<span data-ttu-id="715c7-122">Di seguito sono riportati alcuni esempi di uso di PowerShell per gestire l'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="715c7-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="715c7-123">Insieme di credenziali delle chiavi di Azure - Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="715c7-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="715c7-124">Installazione e configurazione di un insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="715c7-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="715c7-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="715c7-125">Next steps</span></span>
<span data-ttu-id="715c7-126">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e del modo in cui può essere usato per gestire l'insieme di credenziali chiave di Azure, usare i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="715c7-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="715c7-127">Vedere l' [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md)di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="715c7-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="715c7-128">Vedere gli [script di PowerShell dell'insieme di credenziali chiave di Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="715c7-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

