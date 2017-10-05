---
title: <span data-ttu-id="06c6f-101">Creare un modulo di integrazione di Automazione di Azure | Documentazione Microsoft</span><span class="sxs-lookup"><span data-stu-id="06c6f-101">Create an Azure Automation Integration Module | Microsoft Docs</span></span>
description: <span data-ttu-id="06c6f-102">Esercitazione che illustra la creazione, i test e un uso di esempio dei moduli di integrazione in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-102">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="06c6f-103">Moduli di integrazione di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="06c6f-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="06c6f-104">PowerShell è la tecnologia alla base di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="06c6f-105">Poiché Automazione di Azure è basato su PowerShell, i moduli di PowerShell sono essenziali per l'estendibilità di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="06c6f-106">Questo articolo illustra le specifiche dell'uso dei moduli di PowerShell, indicati come "moduli di integrazione", in Automazione di Azure e le procedure consigliate per creare moduli di PowerShell personalizzati destinati a fungere da moduli di integrazione in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="06c6f-107">Che cos'è un modulo di PowerShell</span><span class="sxs-lookup"><span data-stu-id="06c6f-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="06c6f-108">Un modulo di PowerShell è un gruppo di cmdlet di PowerShell, come **Get-Date** o **Copy-Item**, che può essere usato dalla console di PowerShell, da script, da flussi di lavoro, da runbook e da risorse di PowerShell DSC come WindowsFeature o File, che possono essere usate da configurazioni di PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="06c6f-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="06c6f-109">Tutte le funzionalità di PowerShell vengono esposte tramite cmdlet e risorse DSC e ogni risorsa DSC o cmdlet è supportato da un modulo di PowerShell, molti dei quali sono inclusi in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06c6f-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="06c6f-110">Ad esempio, il cmdlet **Get-Date** e il cmdlet **Copy-Item** e la risorsa Package DSC fanno parte rispettivamente dei moduli Microsoft.PowerShell.Utility, Microsoft.PowerShell.Management e PSDesiredStateConfiguration di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06c6f-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="06c6f-111">Tutti questi moduli sono inclusi in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06c6f-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="06c6f-112">Molti moduli di PowerShell, tuttavia, non sono inclusi in PowerShell e vengono invece distribuiti con prodotti proprietari o di terze parti come System Center 2012 Configuration Manager oppure dall'estesa community di PowerShell in posizioni come PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="06c6f-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="06c6f-113">I moduli sono utili perché semplificano attività complesse tramite funzionalità incapsulate.</span><span class="sxs-lookup"><span data-stu-id="06c6f-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="06c6f-114">Altre informazioni sui moduli di PowerShell sono disponibili in [MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="06c6f-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="06c6f-115">Che cos'è un modulo di integrazione di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="06c6f-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="06c6f-116">Un modulo di integrazione è simile a un modulo di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06c6f-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="06c6f-117">È semplicemente un modulo di PowerShell che contiene facoltativamente un file aggiuntivo di metadati che specifica il tipo di connessione di Automazione di Azure che deve essere usato con i cmdlet del modulo nei runbook.</span><span class="sxs-lookup"><span data-stu-id="06c6f-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="06c6f-118">Che sia presente o meno il file facoltativo, questi moduli di PowerShell possono essere importati in Automazione di Azure per rendere i cmdlet e le risorse DSC disponibili per l'uso rispettivamente in runbook e configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="06c6f-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="06c6f-119">In background Automazione di Azure archivia questi moduli e durante l'esecuzione del processo del runbook e del processo di compilazione DSC li carica nelle sandbox di Automazione di Azure in cui i runbook vengono eseguiti e le configurazioni DSC compilate.</span><span class="sxs-lookup"><span data-stu-id="06c6f-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="06c6f-120">Tutte le risorse DSC dei moduli vengono automaticamente inserite nel server pull di Automation DSC in modo che i computer che provano ad applicare le configurazioni DSC possano effettuarne il pull.</span><span class="sxs-lookup"><span data-stu-id="06c6f-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="06c6f-121">In Automazione di Azure sono inclusi per impostazione predefinita alcuni moduli di Azure PowerShell che possono essere usati per iniziare subito ad automatizzare la gestione di Azure, ma è possibile importare moduli di PowerShell per qualsiasi sistema, servizio o strumento con cui si vuole eseguire l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="06c6f-122">Alcuni moduli sono disponibili come "moduli globali" nel servizio di automazione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="06c6f-123">Questi moduli globali sono disponibili quando si crea un account di automazione e vengono talvolta aggiornati automaticamente nell'account di automazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06c6f-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="06c6f-124">Per evitare l'aggiornamento automatico è sempre possibile importare personalmente lo stesso modulo, che avrà la precedenza sulla versione del modulo globale messa a disposizione nel servizio.</span><span class="sxs-lookup"><span data-stu-id="06c6f-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="06c6f-125">Il formato di importazione del pacchetto di un modulo di integrazione è un file compresso con lo stesso nome del modulo ed estensione zip,</span><span class="sxs-lookup"><span data-stu-id="06c6f-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="06c6f-126">che contiene il modulo di Windows PowerShell e tutti i file di supporto, incluso un file manifesto (con estensione psd1) se previsto dal modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="06c6f-127">Se il modulo deve contenere un tipo di connessione di Automazione di Azure, deve contenere anche un file denominato `<ModuleName>-Automation.json` che specifica le proprietà del tipo di connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="06c6f-128">Questo file JSON, inserito nella cartella del modulo del file compresso con estensione zip, contiene i campi della "connessione" necessaria per connettersi al sistema o al servizio rappresentato dal modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="06c6f-129">In questo modo viene creato un tipo di connessione in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="06c6f-130">Usando questo file è possibile impostare i nomi, i tipi e l'eventuale crittografia e/o facoltatività dei campi per il tipo di connessione del modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="06c6f-131">Di seguito è riportato un modello nel formato di file json:</span><span class="sxs-lookup"><span data-stu-id="06c6f-131">The following is a template in the json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="06c6f-132">Per chi ha eseguito la distribuzione di Service Management Automation e la creazione di pacchetti di moduli di integrazione per runbook di automazione, dovrebbe avere un aspetto familiare.</span><span class="sxs-lookup"><span data-stu-id="06c6f-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="06c6f-133">Procedure consigliate per la creazione</span><span class="sxs-lookup"><span data-stu-id="06c6f-133">Authoring Best Practices</span></span>
<span data-ttu-id="06c6f-134">Anche se i moduli di integrazione sono essenzialmente moduli di PowerShell, per garantirne la massima usabilità in Automazione di Azure, durante la creazione di un modulo di PowerShell è consigliabile prendere in considerazione diversi aspetti.</span><span class="sxs-lookup"><span data-stu-id="06c6f-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="06c6f-135">Alcuni sono specifici di Automazione di Azure, mentre altri sono utili per garantire il corretto funzionamento dei moduli in Flusso di lavoro PowerShell indipendentemente dal fatto che si usi Automazione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="06c6f-136">Includere un riepilogo, una descrizione e un URI della Guida per ogni cmdlet del modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="06c6f-137">In PowerShell è possibile definire alcune informazioni della Guida per i cmdlet in modo che gli utenti possano visualizzare informazioni sul relativo uso con il cmdlet **Get-Help** .</span><span class="sxs-lookup"><span data-stu-id="06c6f-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="06c6f-138">Di seguito, ad esempio, è illustrato come definire un riepilogo e un URI della Guida per un modulo di PowerShell scritto in un file con estensione psm1.</span><span class="sxs-lookup"><span data-stu-id="06c6f-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="06c6f-139">Specificando queste informazioni, non solo la Guida verrà visualizzata usando il cmdlet **Get-Help** nella console di PowerShell, ma le funzionalità della Guida verranno esposte anche in Automazione di Azure,</span><span class="sxs-lookup"><span data-stu-id="06c6f-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="06c6f-140">ad esempio quando si inseriscono attività durante la creazione di runbook.</span><span class="sxs-lookup"><span data-stu-id="06c6f-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="06c6f-141">Facendo clic su "Visualizza Guida dettagliata", l'URI della Guida verrà aperto in un'altra scheda del Web browser usato per accedere ad Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="06c6f-142">![Guida dei moduli di integrazione](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="06c6f-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="06c6f-143">Se il modulo viene eseguito su un sistema remoto:</span><span class="sxs-lookup"><span data-stu-id="06c6f-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="06c6f-144">a.</span><span class="sxs-lookup"><span data-stu-id="06c6f-144">a.</span></span> <span data-ttu-id="06c6f-145">deve contenere un file di metadati del modulo di integrazione che definisce le informazioni necessarie per connettersi al sistema remoto, ovvero il tipo di connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="06c6f-146">b.</span><span class="sxs-lookup"><span data-stu-id="06c6f-146">b.</span></span> <span data-ttu-id="06c6f-147">Ogni cmdlet del modulo, inoltre, deve poter accettare un oggetto connessione (ovvero un'istanza del tipo di connessione) come parametro.</span><span class="sxs-lookup"><span data-stu-id="06c6f-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="06c6f-148">L'uso dei cmdlet del modulo in Automazione di Azure risulta più semplice se si consente che al cmdlet venga passato come parametro un oggetto con i campi del tipo di connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="06c6f-149">In questo modo, gli utenti non devono eseguire il mapping dei parametri dell'asset della connessione ai parametri del cmdlet corrispondenti ogni volta che chiamano un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06c6f-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="06c6f-150">In base all'esempio di runbook precedente, viene usato un asset di connessione Twilio denominato CorpTwilio per accedere a Twilio e restituire tutti i numeri di telefono nell'account.</span><span class="sxs-lookup"><span data-stu-id="06c6f-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="06c6f-151">Si noti il mapping dei campi della connessione ai parametri del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06c6f-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="06c6f-152">Un approccio più semplice ed efficiente consiste nel passare direttamente l'oggetto connessione al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06c6f-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="06c6f-153">È possibile abilitare un comportamento di questo tipo per i cmdlet consentendo loro di accettare direttamente un oggetto connessione come parametro, anziché soltanto i campi connessione per i parametri.</span><span class="sxs-lookup"><span data-stu-id="06c6f-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="06c6f-154">È in genere consigliabile che sia presente un set di parametri per ognuno, in modo che un utente che non usa Automazione di Azure possa chiamare i cmdlet senza costruire una tabella hash che funga da oggetto connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="06c6f-155">Il set di parametri **SpecifyConnectionFields** riportato di seguito viene usato per passare una alla volta le proprietà dei campi connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="06c6f-156">**UseConnectionObject** consente di passare direttamente la connessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="06c6f-157">Come si può notare, il cmdlet Send-TwilioSMS del [modulo Twilio di PowerShell](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) consente di usare entrambe le modalità:</span><span class="sxs-lookup"><span data-stu-id="06c6f-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="06c6f-158">Definire il tipo di output per tutti cmdlet del modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="06c6f-159">Definendo un tipo di output per un cmdlet, IntelliSense in fase di progettazione consente di determinare le proprietà di output del cmdlet da usare durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="06c6f-160">È particolarmente utile durante la creazione grafica di runbook di automazione, in cui la conoscenza in fase di progettazione è essenziale per facilitare l'esperienza dell'utente con il modulo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="06c6f-161">![Tipo di output di runbook grafici](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="06c6f-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="06c6f-162">Si ottiene così una funzionalità simile al "completamento automatico" dell'output di un cmdlet in PowerShell ISE, senza che sia necessario eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="06c6f-163">![PowerShell e IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="06c6f-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="06c6f-164">I cmdlet del modulo non devono accettare tipi di oggetto complessi per i parametri.</span><span class="sxs-lookup"><span data-stu-id="06c6f-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="06c6f-165">Flusso di lavoro PowerShell si differenzia da PowerShell perché archivia i tipi complessi in formato deserializzato.</span><span class="sxs-lookup"><span data-stu-id="06c6f-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="06c6f-166">I tipi primitivi vengono mantenuti come primitive, mentre i tipi complessi vengono convertiti nelle rispettive versioni deserializzate, che sono essenzialmente contenitori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="06c6f-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="06c6f-167">Se è stato usato il cmdlet **Get-Process** in un runbook o un flusso di lavoro di PowerShell, viene restituito un oggetto di tipo [Deserialized.System.Diagnostic.Process] anziché il tipo [System.Diagnostic.Process] previsto.</span><span class="sxs-lookup"><span data-stu-id="06c6f-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="06c6f-168">Questo tipo ha le stesse proprietà del tipo non deserializzato, ma nessun metodo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="06c6f-169">Se si cerca di passare questo valore come parametro a un cmdlet, che si aspetta un valore [System.Diagnostic.Process] per il parametro, viene visualizzato l'errore seguente: *Impossibile elaborare la trasformazione degli argomenti nel parametro 'process'. Errore: "Impossibile convertire il valore "System.Diagnostics.Process (CcmExec)" di tipo "Deserialized.System.Diagnostics.Process" nel tipo "System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="06c6f-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="06c6f-170">Ciò è dovuto alla mancata corrispondenza di tipo tra il tipo [System.Diagnostic.Process] previsto e il tipo [Deserialized.System.Diagnostic.Process] fornito.</span><span class="sxs-lookup"><span data-stu-id="06c6f-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="06c6f-171">Per evitare il problema, assicurarsi che i cmdlet del modulo non accettino tipi complessi per i parametri.</span><span class="sxs-lookup"><span data-stu-id="06c6f-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="06c6f-172">Di seguito è illustrato il modo errato di procedere.</span><span class="sxs-lookup"><span data-stu-id="06c6f-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="06c6f-173">Ecco invece il modo corretto, che consiste nell'accettare una primitiva che possa essere usata internamente dal cmdlet per recuperare l'oggetto complesso e usarlo.</span><span class="sxs-lookup"><span data-stu-id="06c6f-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="06c6f-174">Poiché i cmdlet vengono eseguiti nel contesto di PowerShell, non di Flusso di lavoro PowerShell, nel cmdlet $process diventa il tipo [System.Diagnostic.Process] corretto.</span><span class="sxs-lookup"><span data-stu-id="06c6f-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="06c6f-175">Gli asset di connessione dei runbook sono tabelle hash, ovvero un tipo complesso. Sembra però che queste tabelle hash possano essere passate perfettamente ai cmdlet per il parametro –Connection senza eccezione del cast.</span><span class="sxs-lookup"><span data-stu-id="06c6f-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="06c6f-176">Tecnicamente, il cast dal formato serializzato al formato deserializzato può essere eseguito correttamente per alcuni tipi di PowerShell, che possono quindi essere passati ai cmdlet per i parametri che accettano il tipo non deserializzato.</span><span class="sxs-lookup"><span data-stu-id="06c6f-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="06c6f-177">La tabella hash è uno di questi tipi.</span><span class="sxs-lookup"><span data-stu-id="06c6f-177">Hashtable is one of these.</span></span> <span data-ttu-id="06c6f-178">Anche i tipi definiti dall'autore del modulo possono essere implementati per poter essere deserializzati correttamente, ma sono necessari alcuni compromessi.</span><span class="sxs-lookup"><span data-stu-id="06c6f-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="06c6f-179">Per il tipo devono essere disponibili un costruttore predefinito e un PSTypeConverter e tutte le proprietà del tipo devono essere pubbliche.</span><span class="sxs-lookup"><span data-stu-id="06c6f-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="06c6f-180">I tipi già definiti che non sono di proprietà dell'autore del modulo, tuttavia, non possono essere in alcun modo "corretti" ed è per questo motivo che è consigliabile evitare completamente i tipi complessi per i parametri.</span><span class="sxs-lookup"><span data-stu-id="06c6f-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="06c6f-181">Suggerimento per la creazione di runbook: se per qualche motivo i cmdlet devono accettare un parametro di tipo complesso o si usa un modulo altrui che richiede un parametro di tipo complesso, la soluzione alternativa nei runbook Flusso di lavoro PowerShell e nei flussi di lavoro di PowerShell in PowerShell locale è eseguire il wrapping del cmdlet che genera il tipo complesso e del cmdlet che lo usa nella stessa attività InlineScript.</span><span class="sxs-lookup"><span data-stu-id="06c6f-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="06c6f-182">Poiché InlineScript esegue il contenuto come PowerShell anziché come Flusso di lavoro PowerShell, il cmdlet che genera il tipo complesso produrrà il tipo corretto e non il tipo complesso deserializzato.</span><span class="sxs-lookup"><span data-stu-id="06c6f-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="06c6f-183">Assicurarsi che tutti i cmdlet del modulo siano senza stato.</span><span class="sxs-lookup"><span data-stu-id="06c6f-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="06c6f-184">Flusso di lavoro PowerShell esegue tutti i cmdlet chiamati nel flusso di lavoro in una diversa sessione.</span><span class="sxs-lookup"><span data-stu-id="06c6f-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="06c6f-185">Di conseguenza, i cmdlet che dipendono dallo stato della sessione creato/modificato da altri cmdlet dello stesso modulo non funzioneranno nei runbook Flusso di lavoro PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06c6f-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="06c6f-186">Di seguito è riportato un esempio della soluzione da non adottare.</span><span class="sxs-lookup"><span data-stu-id="06c6f-186">Here is an example of what not to do.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="06c6f-187">Il modulo deve essere interamente contenuto in un pacchetto su cui è possibile eseguire Xcopy.</span><span class="sxs-lookup"><span data-stu-id="06c6f-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="06c6f-188">Poiché i moduli di Automazione di Azure vengono distribuiti nelle sandbox di Automazione quando devono essere eseguiti i runbook, devono funzionare in modo indipendente dall'host in cui vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="06c6f-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="06c6f-189">Dovrebbe quindi essere possibile comprimere il pacchetto del modulo e spostarlo in qualsiasi altro host con la stessa versione di PowerShell o una più recente ottenendo il normale funzionamento dopo l'importazione nell'ambiente PowerShell di tale host.</span><span class="sxs-lookup"><span data-stu-id="06c6f-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="06c6f-190">Perché ciò avvenga, il modulo non deve dipendere da file all'esterno della cartella del modulo (ovvero della cartella che viene compressa per l'importazione in Automazione di Azure) né da qualsiasi impostazione del Registro di sistema univoca di un host, come quelle definite dall'installazione di un prodotto.</span><span class="sxs-lookup"><span data-stu-id="06c6f-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="06c6f-191">Se questa procedura consigliata non viene seguita, il modulo non potrà essere usato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="06c6f-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="06c6f-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06c6f-192">Next steps</span></span>

* <span data-ttu-id="06c6f-193">Per iniziare a usare i runbook del flusso di lavoro PowerShell, vedere [Il primo runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="06c6f-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="06c6f-194">Per altre informazioni sulla creazione di moduli di PowerShell, vedere [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="06c6f-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

