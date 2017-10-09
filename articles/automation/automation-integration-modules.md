---
title: aaaCreate un modulo di integrazione di automazione di Azure | Documenti Microsoft
description: Esercitazione che illustra utilizzare hello di esempio, test e la creazione di moduli di integrazione in automazione di Azure.
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
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="6670a-103">Moduli di integrazione di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6670a-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="6670a-104">PowerShell è una tecnologia fondamentale di hello dietro l'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="6670a-105">Poiché automazione di Azure è basata su PowerShell, i moduli di PowerShell sono toohello chiave estendibilità di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="6670a-106">In questo articolo è guiderà specifiche hello dell'uso di automazione di Azure di moduli di PowerShell, cui tooas "Moduli di integrazione" e procedure consigliate per la creazione di propri toomake moduli di PowerShell che funzionano come moduli di integrazione all'interno di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="6670a-107">Che cos'è un modulo di PowerShell</span><span class="sxs-lookup"><span data-stu-id="6670a-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="6670a-108">Un modulo di PowerShell è un gruppo di cmdlet di PowerShell come **Get-Date** o **Copy-Item**, che può essere utilizzato dalla console di PowerShell hello, script, flussi di lavoro, runbook e le risorse DSC PowerShell come WindowsFeature o File, che può essere utilizzato dalle configurazioni di PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="6670a-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="6670a-109">Le funzionalità di hello di PowerShell viene esposta tramite i cmdlet e le risorse DSC e tutte le risorse/DSC cmdlet sono supportata da un modulo di PowerShell, molti dei quali forniti con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6670a-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="6670a-110">Ad esempio, hello **Get-Date** cmdlet fa parte del modulo di PowerShell Utility, hello e **Copy-Item** cmdlet fa parte del modulo PowerShell Microsoft hello e risorsa Package DSC Hello fa parte del modulo PSDesiredStateConfiguration PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="6670a-111">Tutti questi moduli sono inclusi in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6670a-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="6670a-112">Tuttavia, molti moduli di PowerShell non fanno parte di PowerShell e vengono invece distribuiti con i prodotti prima o di terze parti come System Center 2012 Configuration Manager o da una grande community PowerShell hello in luoghi come PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="6670a-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="6670a-113">i moduli di Hello sono utili perché rendono più semplice tramite la funzionalità incapsulata attività complesse.</span><span class="sxs-lookup"><span data-stu-id="6670a-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="6670a-114">Altre informazioni sui moduli di PowerShell sono disponibili in [MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6670a-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="6670a-115">Che cos'è un modulo di integrazione di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6670a-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="6670a-116">Un modulo di integrazione è simile a un modulo di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6670a-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="6670a-117">Il relativo semplicemente un modulo di PowerShell che contiene facoltativamente un file aggiuntivo - un file di metadati che specifica un toobe di tipo di connessione di automazione di Azure utilizzati con i cmdlet del modulo hello nei runbook.</span><span class="sxs-lookup"><span data-stu-id="6670a-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="6670a-118">Facoltativo del file oppure No, questi moduli possono essere importati in automazione di Azure toomake dei cmdlet disponibili per utilizzano all'interno di runbook e le relative risorse DSC disponibili per l'utilizzo all'interno delle configurazioni DSC di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6670a-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="6670a-119">Background hello, automazione di Azure archivia questi moduli e al processo del runbook e tempo di esecuzione processo di compilazione DSC, li carica in sandbox di automazione di Azure hello in cui vengono eseguiti i runbook e vengono compilate le configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="6670a-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="6670a-120">Le risorse DSC nei moduli vengono inserite automaticamente anche nel server di pull DSC di automazione di hello, in modo che è possibile effettuare il pull da macchine tentando tooapply le configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="6670a-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="6670a-121">Forniti un numero di moduli di PowerShell di Azure predefinito hello in automazione di Azure per toouse è pertanto possibile iniziare subito l'automazione di gestione di Azure, ma è possibile importare i moduli di PowerShell per qualsiasi sistema, servizio o lo strumento desiderato toointegrate con.</span><span class="sxs-lookup"><span data-stu-id="6670a-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="6670a-122">Alcuni moduli vengono forniti come "moduli globali" nel servizio di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="6670a-123">Questi moduli globali sono disponibili tooyou quando si crea un account di automazione, e viene aggiornato in alcuni casi che li automaticamente inserisce tooyour account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6670a-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="6670a-124">Se si vuole impedire toobe auto-aggiornato, è possibile importare sempre hello stesso modulo manualmente e che avrà la precedenza sulla versione del modulo globale hello del modulo forniti nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="6670a-125">formato di Hello in cui importare un pacchetto di modulo di integrazione è un file compresso con hello stesso nome modulo hello e l'estensione. zip.</span><span class="sxs-lookup"><span data-stu-id="6670a-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="6670a-126">Contiene il modulo di Windows PowerShell hello e qualsiasi file di supporto, tra cui un file manifesto (psd1) se nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="6670a-127">Se il modulo hello deve contenere un tipo di connessione di automazione di Azure, deve contenere anche un file con nome hello `<ModuleName>-Automation.json` che specifica le proprietà di tipo connessione hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="6670a-128">Questo è un file json inserito in una cartella del file zip del modulo hello e contiene i campi di hello di "connessione" che è necessario tooconnect toohello sistema o modulo hello servizio rappresenta.</span><span class="sxs-lookup"><span data-stu-id="6670a-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="6670a-129">In questo modo viene creato un tipo di connessione in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="6670a-130">Uso di questo file è possibile impostare i nomi dei campi hello, tipi, e se i campi di hello devono essere crittografati e / o facoltativi, per il tipo di connessione hello del modulo hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="6670a-131">di seguito Hello è un modello in formato json hello:</span><span class="sxs-lookup"><span data-stu-id="6670a-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="6670a-132">Se è stato distribuito Service Management Automation e creare pacchetti di moduli di integrazione per i runbook di automazione, dovrebbe essere tooyou molto familiare.</span><span class="sxs-lookup"><span data-stu-id="6670a-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="6670a-133">Procedure consigliate per la creazione</span><span class="sxs-lookup"><span data-stu-id="6670a-133">Authoring Best Practices</span></span>
<span data-ttu-id="6670a-134">Anche se i moduli di integrazione sono essenzialmente i moduli di PowerShell, sia ancora disponibile una serie di operazioni, è consigliabile durante la creazione di un modulo di PowerShell, toomake è più utilizzabile in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="6670a-135">Alcune di queste sono automazione di Azure specifico e alcuni di essi sono utili toomake solo i moduli funzionano correttamente in flusso di lavoro PowerShell, indipendentemente dal fatto se si utilizza l'automazione.</span><span class="sxs-lookup"><span data-stu-id="6670a-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="6670a-136">Include un riepilogo, descrizione e l'URI della Guida per ogni cmdlet nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="6670a-137">In PowerShell, è possibile definire alcune informazioni della Guida per la Guida dei cmdlet tooallow hello utente tooreceive per utilizzarli con hello **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6670a-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="6670a-138">Di seguito, ad esempio, è illustrato come definire un riepilogo e un URI della Guida per un modulo di PowerShell scritto in un file con estensione psm1.</span><span class="sxs-lookup"><span data-stu-id="6670a-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="6670a-139">Fornire queste informazioni non visualizzerà soltanto i questa Guida utilizzando hello **Get-Help** hello di cmdlet nella console di PowerShell, perché verrà inoltre esporre questa funzionalità della Guida di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="6670a-140">ad esempio quando si inseriscono attività durante la creazione di runbook.</span><span class="sxs-lookup"><span data-stu-id="6670a-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="6670a-141">Fare clic su "Visualizza Guida dettagliata" verrà URI della Guida hello aperto in un'altra scheda di hello web browser in uso tooaccess automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="6670a-142">![Guida dei moduli di integrazione](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="6670a-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="6670a-143">Se il modulo hello viene eseguito in un sistema remoto,</span><span class="sxs-lookup"><span data-stu-id="6670a-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="6670a-144">a.</span><span class="sxs-lookup"><span data-stu-id="6670a-144">a.</span></span> <span data-ttu-id="6670a-145">Deve contenere un file di metadati di modulo di integrazione che definisce hello informazioni necessarie tooconnect toothat sistema remoto, ovvero il tipo di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="6670a-146">b.</span><span class="sxs-lookup"><span data-stu-id="6670a-146">b.</span></span> <span data-ttu-id="6670a-147">Ogni cmdlet nel modulo hello deve essere in grado di tootake in un oggetto di connessione (un'istanza di quel tipo di connessione) come parametro.</span><span class="sxs-lookup"><span data-stu-id="6670a-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="6670a-148">I cmdlet nel modulo hello diventano più facile toouse in automazione di Azure se si consente di passare un oggetto con i campi di hello hello del tipo di connessione come parametro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6670a-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="6670a-149">Questo consente agli utenti non dispone di parametri di toomap dei parametri corrispondenti del cmdlet di hello connessione asset toohello ogni volta che si chiama un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6670a-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="6670a-150">In base a hello runbook di esempio precedente, utilizza un asset di connessione di Twilio denominato CorpTwilio tooaccess Twilio e restituire tutti i numeri di telefono hello in account hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="6670a-151">Si noti la modalità è mapping dei campi di hello hello parametri di connessione toohello del cmdlet hello?</span><span class="sxs-lookup"><span data-stu-id="6670a-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="6670a-152">Tooapproach un modo più semplice e più direttamente questo sta passando hello connessione oggetto toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="6670a-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="6670a-153">È possibile abilitare il comportamento simile al seguente per i cmdlet, consentendo loro tooaccept un oggetto di connessione direttamente come parametro, anziché solo i campi di connessione per i parametri.</span><span class="sxs-lookup"><span data-stu-id="6670a-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="6670a-154">In genere è opportuno un set di parametri per ognuno, in modo che un utente non utilizzando l'automazione di Azure è possibile chiamare il cmdlet senza creare una tabella hash tooact come oggetto di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="6670a-155">Set di parametri **SpecifyConnectionFields** di seguito è toopass usate le proprietà di campo connessione hello uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="6670a-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="6670a-156">**UseConnectionObject** consente di passare hello direttamente tramite connessione.</span><span class="sxs-lookup"><span data-stu-id="6670a-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="6670a-157">Come si può notare, hello trasmissione TwilioSMS cmdlet in hello [modulo PowerShell di Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) consente di passare in entrambi i casi:</span><span class="sxs-lookup"><span data-stu-id="6670a-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="6670a-158">Definire il tipo di output per tutti i cmdlet nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="6670a-159">Per un cmdlet consente di IntelliSense in fase di progettazione si definisce un tipo di output è determinare hello toohelp restituire proprietà del cmdlet hello, per l'utilizzo durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="6670a-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="6670a-160">È particolarmente utile durante l'automazione runbook grafici per la modifica, in cui knowledge fase di progettazione è l'esperienza utente semplice tooan chiave con il modulo.</span><span class="sxs-lookup"><span data-stu-id="6670a-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="6670a-161">![Tipo di output di runbook grafici](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="6670a-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="6670a-162">Questa operazione è simile toohello "con tipo" funzionalità di un cmdlet di output in PowerShell ISE senza toorun.</span><span class="sxs-lookup"><span data-stu-id="6670a-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="6670a-163">![PowerShell e IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="6670a-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="6670a-164">I cmdlet nel modulo hello è possibile utilizzare i tipi di oggetto complesso per i parametri.</span><span class="sxs-lookup"><span data-stu-id="6670a-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="6670a-165">Flusso di lavoro PowerShell si differenzia da PowerShell perché archivia i tipi complessi in formato deserializzato.</span><span class="sxs-lookup"><span data-stu-id="6670a-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="6670a-166">Tipi primitivi verranno mantenuta come primitivi, ma i tipi complessi sono versioni tootheir convertito deserializzato, che sono essenzialmente elenchi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="6670a-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="6670a-167">Ad esempio, se è stato utilizzato hello **Get-Process** cmdlet in un runbook, o un flusso di lavoro di PowerShell per questo scopo, potrebbe restituire un oggetto di tipo [Deserialized.System.Diagnostic.Process], non hello [previsto Tipo Diagnostic].</span><span class="sxs-lookup"><span data-stu-id="6670a-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="6670a-168">Questo tipo dispone di tutte hello stesse proprietà come hello non deserializzato tipo, ma nessuno dei metodi di hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="6670a-169">Se si tenta toopass questo valore come parametro tooa cmdlet, i cmdlet di hello in cui è previsto un valore di [Diagnostic] per questo parametro, viene visualizzato il seguente errore hello: *non è in grado di elaborare trasformazione argomento sul parametro 'process' . Errore: "non è possibile convertire il valore di"Diagnostics (CcmExec)"hello di tipo"Deserialized.System.Diagnostics.Process"tootype"Diagnostics".*</span><span class="sxs-lookup"><span data-stu-id="6670a-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="6670a-170">In questo modo è che un tipo non corrispondente tra hello previsto tipo [Diagnostic] e [Deserialized.System.Diagnostic.Process] tipo specificato di hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="6670a-171">Hello questo problema consiste tooensure hello cmdlet del modulo non accettano i tipi complessi per i parametri.</span><span class="sxs-lookup"><span data-stu-id="6670a-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="6670a-172">Ecco toodo modo errato hello è.</span><span class="sxs-lookup"><span data-stu-id="6670a-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="6670a-173">Di seguito è hello destro, in una primitiva che può essere usata internamente dal cmdlet hello toograb hello oggetto complesso e utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="6670a-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="6670a-174">Poiché i cmdlet eseguiti nel contesto di hello di PowerShell, non flusso di lavoro PowerShell, all'interno di cmdlet hello $process diventa hello corretto [Diagnostic] tipo.</span><span class="sxs-lookup"><span data-stu-id="6670a-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="6670a-175">Gli asset di connessione nel runbook sono tabelle hash, che sono un tipo complesso, e ancora queste tabelle hash sembra toobe in grado di toobe passato nel cmdlet per loro – parametro di connessione, perfettamente con alcuna eccezione di cast.</span><span class="sxs-lookup"><span data-stu-id="6670a-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="6670a-176">Tecnicamente, alcuni tipi di PowerShell sono in grado di toocast correttamente dal modulo tootheir deserializzato formato serializzato e pertanto possono essere passati in cmdlet per i parametri che accetta il tipo non è stato deserializzato hello.</span><span class="sxs-lookup"><span data-stu-id="6670a-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="6670a-177">La tabella hash è uno di questi tipi.</span><span class="sxs-lookup"><span data-stu-id="6670a-177">Hashtable is one of these.</span></span> <span data-ttu-id="6670a-178">È possibile che toobe di tipi definiti dell'autore del modulo implementata in modo che correttamente può deserializzare nonché, ma esistono alcune tooconsider compromessi.</span><span class="sxs-lookup"><span data-stu-id="6670a-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="6670a-179">Hello toohave esigenze di tipo un costruttore predefinito, dispone di tutte le proprietà pubblici e avere un PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="6670a-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="6670a-180">Tuttavia, per i tipi già definiti dall'autore del modulo che hello non proprietari, è non troppo "correggerli", pertanto hello tipi complessi di raccomandazione tooavoid per i parametri tutti insieme.</span><span class="sxs-lookup"><span data-stu-id="6670a-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="6670a-181">Creazione di runbook Suggerimento: se per qualche motivo il cmdlet necessario tootake un complesso il parametro di tipo, o se si utilizza un altro modulo che richiede un parametro di tipo complesso, con la soluzione alternativa hello nei runbook del flusso di lavoro di PowerShell e flussi di lavoro di PowerShell in locale PowerShell, è toowrap hello cmdlet che genera l'errore di tipo complesso hello e cmdlet hello che utilizza il tipo complesso di hello in hello stessa attività InlineScript.</span><span class="sxs-lookup"><span data-stu-id="6670a-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="6670a-182">Poiché InlineScript viene eseguito il relativo contenuto come PowerShell anziché flusso di lavoro PowerShell, cmdlet hello la generazione di tipo complesso hello produrrebbe tale tipo corretto, non hello deserializzata il tipo complesso.</span><span class="sxs-lookup"><span data-stu-id="6670a-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="6670a-183">Verificare tutti i cmdlet nel modulo hello senza stato.</span><span class="sxs-lookup"><span data-stu-id="6670a-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="6670a-184">Flusso di lavoro PowerShell viene eseguito ogni cmdlet denominato nel flusso di lavoro hello in un'altra sessione.</span><span class="sxs-lookup"><span data-stu-id="6670a-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="6670a-185">Ciò significa che i cmdlet che variano a seconda dello stato della sessione creato / modificato da altri cmdlet di hello stesso modulo non funzionerà nei runbook del flusso di lavoro di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6670a-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="6670a-186">Di seguito è riportato un esempio di ciò che non toodo.</span><span class="sxs-lookup"><span data-stu-id="6670a-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="6670a-187">modulo Hello deve essere completamente contenuto in un pacchetto in grado di Xcopy.</span><span class="sxs-lookup"><span data-stu-id="6670a-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="6670a-188">Poiché i moduli di automazione di Azure sono distribuite toohello automazione sandbox quando runbook necessario tooexecute, è necessario che toowork indipendentemente dall'host hello in che vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="6670a-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="6670a-189">Ciò significa che è necessario essere in grado di tooZip pacchetto modulo hello, spostarlo tooany altri host con hello uguale o più recente versione di PowerShell e fare in modo funzionano normalmente durante l'importazione in ambiente di PowerShell di tale host.</span><span class="sxs-lookup"><span data-stu-id="6670a-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="6670a-190">Affinché tale toohappen, hello modulo deve non dipendono da tutti i file all'esterno di hello modulo (cartella hello che ottiene compressi quando si importano in automazione di Azure) o in una sola impostazione del Registro di sistema univoco in un host, ad esempio quelle impostate hello installare di un prodotto.</span><span class="sxs-lookup"><span data-stu-id="6670a-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="6670a-191">Se non è seguita questa procedura consigliata, modulo hello non sarà utilizzabile in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6670a-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6670a-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6670a-192">Next steps</span></span>

* <span data-ttu-id="6670a-193">tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="6670a-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="6670a-194">toolearn informazioni sulla creazione di moduli di PowerShell, vedere [la scrittura di un modulo Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="6670a-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

