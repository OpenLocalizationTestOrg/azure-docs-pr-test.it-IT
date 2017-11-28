---
title: Impostazioni dei runbook | Documentazione Microsoft
description: Illustra le impostazioni di configurazione per un runbook in Automazione di Azure e come modificarle usando il portale di gestione di Azure e Windows PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="ad2b7-103">Impostazioni dei runbook</span><span class="sxs-lookup"><span data-stu-id="ad2b7-103">Runbook settings</span></span>
<span data-ttu-id="ad2b7-104">Ogni runbook in Automazione di Azure dispone di più impostazioni che consentono di identificarlo e di modificarne il comportamento di registrazione.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="ad2b7-105">Per ognuna di queste impostazioni, di seguito viene riportata una descrizione e vengono illustrate le procedure di modifica.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="ad2b7-106">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="ad2b7-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="ad2b7-107">Nome e descrizione</span><span class="sxs-lookup"><span data-stu-id="ad2b7-107">Name and description</span></span>
<span data-ttu-id="ad2b7-108">Non è possibile modificare il nome di un runbook dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="ad2b7-109">La descrizione è facoltativa e può contenere fino a 512 caratteri.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="ad2b7-110">Tag</span><span class="sxs-lookup"><span data-stu-id="ad2b7-110">Tags</span></span>
<span data-ttu-id="ad2b7-111">I tag consentono di assegnare parole e frasi distinte per facilitare l'identificazione di un runbook.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="ad2b7-112">Quando si invia un runbook alla [PowerShell Gallery](https://www.powershellgallery.com/), è possibile ad esempio specificare tag particolari per identificare le categorie in cui il runbook deve essere elencato.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="ad2b7-113">È possibile specificare più tag per un runbook separandole con le virgole.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="ad2b7-114">Registrazione</span><span class="sxs-lookup"><span data-stu-id="ad2b7-114">Logging</span></span>
<span data-ttu-id="ad2b7-115">Per impostazione predefinita, i record dettagliati e di avanzamento non vengono scritti nella cronologia processo.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="ad2b7-116">È possibile modificare le impostazioni per un determinato runbook per registrare questi record.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="ad2b7-117">Per altre informazioni su tali record, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ad2b7-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="ad2b7-118">Modifica delle impostazioni dei runbook</span><span class="sxs-lookup"><span data-stu-id="ad2b7-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="ad2b7-119">Modifica delle impostazioni dei runbook nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ad2b7-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="ad2b7-120">Per modificare le impostazioni di un runbook nel portale di Azure, usare il pannello **Impostazioni** corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="ad2b7-121">Nel portale di Azure selezionare **Automazione** e quindi fare clic sul nome di un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="ad2b7-122">Fare clic sulla scheda **Runbook** .</span><span class="sxs-lookup"><span data-stu-id="ad2b7-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="ad2b7-123">Fare clic sul nome di un runbook per aprire il pannello delle impostazioni corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="ad2b7-124">In tale pannello è possibile specificare o modificare i tag e la descrizione del runbook, configurare le impostazioni di traccia e registrazione e accedere agli strumenti di supporto per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="ad2b7-125">Modifica delle impostazioni dei runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad2b7-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="ad2b7-126">Per modificare le impostazioni di un runbook, è possibile usare il cmdlet [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad2b7-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="ad2b7-127">Se si intende specificare più tag, è possibile fornire una matrice o una singola stringa con valori delimitati da virgole per il parametro Tags.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="ad2b7-128">Per ottenere i tag correnti, usare [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad2b7-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="ad2b7-129">I comandi di esempio seguenti illustrano come impostare le proprietà di un runbook.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="ad2b7-130">Questo esempio aggiunge tre tag ai tag esistenti e specifica che vengano registrati i record dettagliati.</span><span class="sxs-lookup"><span data-stu-id="ad2b7-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="ad2b7-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad2b7-131">Next steps</span></span>
* <span data-ttu-id="ad2b7-132">Per informazioni su come creare e recuperare l'output e i messaggi di errore da runbook, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ad2b7-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="ad2b7-133">Per informazioni su come aggiungere un runbook già sviluppato dalla community o da un'altra origine o su come creare runbook propri, vedere [Creazione o importazione di un runbook](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="ad2b7-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

