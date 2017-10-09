---
title: impostazioni aaaRunbook | Documenti Microsoft
description: Vengono descritte le impostazioni di configurazione hello per un runbook in automazione di Azure e come toochange sia mediante hello portale di gestione di Azure e Windows PowerShell.
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="c09a2-103">Impostazioni dei runbook</span><span class="sxs-lookup"><span data-stu-id="c09a2-103">Runbook settings</span></span>
<span data-ttu-id="c09a2-104">Ogni runbook in automazione di Azure dispone di più impostazioni che consentono di toobe identificato e toochange relativo comportamento di registrazione.</span><span class="sxs-lookup"><span data-stu-id="c09a2-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="c09a2-105">Ognuna di queste impostazioni è descritta di seguito seguita da procedure su come toomodify li.</span><span class="sxs-lookup"><span data-stu-id="c09a2-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="c09a2-106">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="c09a2-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="c09a2-107">Nome e descrizione</span><span class="sxs-lookup"><span data-stu-id="c09a2-107">Name and description</span></span>
<span data-ttu-id="c09a2-108">È possibile modificare il nome di hello di un runbook dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c09a2-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="c09a2-109">Hello descrizione è facoltativo e può essere di too512 caratteri.</span><span class="sxs-lookup"><span data-stu-id="c09a2-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="c09a2-110">Tag</span><span class="sxs-lookup"><span data-stu-id="c09a2-110">Tags</span></span>
<span data-ttu-id="c09a2-111">Tag consentono il che identificazione di un runbook è tooassign parole e frasi toohelp.</span><span class="sxs-lookup"><span data-stu-id="c09a2-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="c09a2-112">Ad esempio, quando si invia un toohello runbook [PowerShell Gallery](https://www.powershellgallery.com/), si specifica tooidentify tag particolari quali categorie hello runbook dovrebbe essere elencato.</span><span class="sxs-lookup"><span data-stu-id="c09a2-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="c09a2-113">È possibile specificare più tag per un runbook separandole con le virgole.</span><span class="sxs-lookup"><span data-stu-id="c09a2-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="c09a2-114">Registrazione</span><span class="sxs-lookup"><span data-stu-id="c09a2-114">Logging</span></span>
<span data-ttu-id="c09a2-115">Per impostazione predefinita, i record dettagliati e di avanzamento non vengono scritte toojob cronologia.</span><span class="sxs-lookup"><span data-stu-id="c09a2-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="c09a2-116">È possibile modificare le impostazioni di hello per un determinato runbook di toolog questi record.</span><span class="sxs-lookup"><span data-stu-id="c09a2-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="c09a2-117">Per altre informazioni su tali record, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="c09a2-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="c09a2-118">Modifica delle impostazioni dei runbook</span><span class="sxs-lookup"><span data-stu-id="c09a2-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="c09a2-119">Modifica delle impostazioni di runbook con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c09a2-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="c09a2-120">È possibile modificare le impostazioni per un runbook nel portale di Azure hello da hello **impostazioni** pannello per il runbook hello.</span><span class="sxs-lookup"><span data-stu-id="c09a2-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="c09a2-121">Nel portale di Azure hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="c09a2-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="c09a2-122">Seleziona hello **runbook** scheda.</span><span class="sxs-lookup"><span data-stu-id="c09a2-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="c09a2-123">Fare clic sul nome di un runbook hello e si è il pannello impostazioni toohello diretto per hello runbook.</span><span class="sxs-lookup"><span data-stu-id="c09a2-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="c09a2-124">Da qui è possibile specificare o modificare i tag, hello descrizione del runbook, configura la registrazione e le impostazioni di traccia e toohelp di strumenti di supporto risolvere i problemi di accesso.</span><span class="sxs-lookup"><span data-stu-id="c09a2-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="c09a2-125">Modifica delle impostazioni dei runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c09a2-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="c09a2-126">È possibile utilizzare hello [Set AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) impostazioni hello toochange di cmdlet per un runbook.</span><span class="sxs-lookup"><span data-stu-id="c09a2-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="c09a2-127">Se si desidera toospecify più tag, è possibile fornire una matrice o una singola stringa con il parametro di tag toohello valori delimitati da virgole.</span><span class="sxs-lookup"><span data-stu-id="c09a2-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="c09a2-128">È possibile ottenere i tag corrente hello con hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="c09a2-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="c09a2-129">Hello comandi di esempio seguenti Mostra come tooset hello proprietà di un runbook.</span><span class="sxs-lookup"><span data-stu-id="c09a2-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="c09a2-130">In questo esempio aggiunge tre tag esistenti toohello tag e specifica che i record dettagliati devono essere registrati.</span><span class="sxs-lookup"><span data-stu-id="c09a2-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="c09a2-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c09a2-131">Next steps</span></span>
* <span data-ttu-id="c09a2-132">toolearn toocreate e recuperare messaggi di errore e di output dal runbook, vedere [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="c09a2-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="c09a2-133">vedere un runbook che è stato già sviluppato da hello community o altra origine o toocreate propri runbook tooadd toounderstand [la creazione o importazione di un Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="c09a2-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

