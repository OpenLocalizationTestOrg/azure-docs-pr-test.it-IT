---
title: Ottimizzare l'ambiente SQL Server con Log Analytics di Azure|Documentazione Microsoft
description: "Con Log Analytics di Azure è possibile usare la soluzione SQL Assessment per valutare i rischi e l'integrità degli ambienti SQL Server a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="5cdca-103">Ottimizzare l'ambiente SQL Server con la soluzione SQL Assessment in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5cdca-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![Simbolo di Valutazione SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="5cdca-105">È possibile usare la soluzione SQL Assessment per valutare i rischi e l'integrità degli ambienti server a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="5cdca-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="5cdca-106">Questo articolo consente di installare la soluzione in modo che si possano intraprendere azioni correttive per problemi potenziali.</span><span class="sxs-lookup"><span data-stu-id="5cdca-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="5cdca-107">La soluzione offre un elenco con priorità di raccomandazioni specifiche per l'infrastruttura distribuita dei server,</span><span class="sxs-lookup"><span data-stu-id="5cdca-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="5cdca-108">classificate in sei aree di interesse che consentono di comprendere rapidamente il rischio e agire in maniera appropriata.</span><span class="sxs-lookup"><span data-stu-id="5cdca-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="5cdca-109">Le raccomandazioni si basano sulla conoscenza e sull'esperienza acquisite dai tecnici Microsoft in base a migliaia di visite dei clienti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="5cdca-110">Ogni raccomandazione offre informazioni aggiuntive sui motivi per cui un problema può essere rilevante per l'utente e su come implementare le modifiche suggerite.</span><span class="sxs-lookup"><span data-stu-id="5cdca-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="5cdca-111">Si possono scegliere le aree di interesse più importanti per l'organizzazione e tenere traccia dello stato di avanzamento verso la realizzazione di un ambiente integro ed esente da rischi.</span><span class="sxs-lookup"><span data-stu-id="5cdca-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="5cdca-112">Dopo aver aggiunto la soluzione e completato una valutazione, nel dashboard **SQL Assessment** per l'infrastruttura nell'ambiente verranno visualizzate le informazioni di riepilogo per l'area di interesse.</span><span class="sxs-lookup"><span data-stu-id="5cdca-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="5cdca-113">Le sezioni seguenti descrivono come usare le informazioni visualizzate nel dashboard **SQL Assessment** , in cui sarà possibile intraprendere le azioni consigliate per l'infrastruttura dei server di SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![immagine del riquadro  SQL Assessment](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![Immagine del dashboard SQL Assessment ](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="5cdca-116">Installazione e configurazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="5cdca-116">Installing and configuring the solution</span></span>
<span data-ttu-id="5cdca-117">SQL Assessment è compatibile con le edizioni Standard, Developer ed Enterprise di tutte le versioni attualmente supportate di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5cdca-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="5cdca-118">Usare le informazioni seguenti per installare e configurare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="5cdca-119">Nei server in cui è installato SQL Server devono essere installati gli agenti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="5cdca-120">La soluzione SQL Assessment richiede l'installazione di una versione di .NET Framework 4 supportata in ogni computer che contiene un agente OMS.</span><span class="sxs-lookup"><span data-stu-id="5cdca-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="5cdca-121">Per installare la soluzione, l'utente deve essere amministratore o collaboratore della sottoscrizione di Azure se si usa il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdca-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="5cdca-122">L'utente deve anche essere membro del ruolo di amministratore o collaboratore dell'area di lavoro OMS nel portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="5cdca-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="5cdca-123">Quando si usa l'agente Operations Manager con SQL Assessment, è necessario usare un account RunAs di Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="5cdca-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="5cdca-124">Per altre informazioni, vedere di seguito [Account RunAs di Operations Manager per OMS](#operations-manager-run-as-accounts-for-oms) .</span><span class="sxs-lookup"><span data-stu-id="5cdca-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5cdca-125">L'agente MMA non supporta gli account RunAs di Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="5cdca-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="5cdca-126">Aggiungere la soluzione SQL Assessment all'area di lavoro OMS usando la procedura descritta nell'articolo [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5cdca-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="5cdca-127">Non è richiesta alcuna ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="5cdca-128">Dopo aver aggiunto la soluzione, il file AdvisorAssessment.exe viene aggiunto al server con agenti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="5cdca-129">I dati di configurazione vengono letti e quindi inviati al servizio OMS nel cloud per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="5cdca-130">Viene applicata la logica ai dati ricevuti, quindi questi ultimi vengono registrati nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="5cdca-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="5cdca-131">Informazioni dettagliate sulla raccolta dei dati di SQL Assessment</span><span class="sxs-lookup"><span data-stu-id="5cdca-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="5cdca-132">SQL Assessment raccoglie dati WMI, dati del Registro di sistema, dati sulle prestazioni e risultati delle visualizzazioni a gestione dinamica di SQL Server usando gli agenti abilitati.</span><span class="sxs-lookup"><span data-stu-id="5cdca-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="5cdca-133">La tabella seguente illustra i metodi di raccolta dati per gli agenti, se Operations Manager (SCOM) è obbligatorio e la frequenza con cui i dati vengono raccolti da un agente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="5cdca-134">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="5cdca-134">platform</span></span> | <span data-ttu-id="5cdca-135">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="5cdca-135">Direct Agent</span></span> | <span data-ttu-id="5cdca-136">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="5cdca-136">SCOM agent</span></span> | <span data-ttu-id="5cdca-137">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5cdca-137">Azure Storage</span></span> | <span data-ttu-id="5cdca-138">SCOM obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="5cdca-138">SCOM required?</span></span> | <span data-ttu-id="5cdca-139">Dati dell'agente SCOM inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="5cdca-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="5cdca-140">frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="5cdca-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5cdca-141">Windows</span><span class="sxs-lookup"><span data-stu-id="5cdca-141">Windows</span></span> | <span data-ttu-id="5cdca-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5cdca-142">&#8226;</span></span> | <span data-ttu-id="5cdca-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5cdca-143">&#8226;</span></span> |  |  | <span data-ttu-id="5cdca-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5cdca-144">&#8226;</span></span> |<span data-ttu-id="5cdca-145">7 giorni</span><span class="sxs-lookup"><span data-stu-id="5cdca-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="5cdca-146">Account RunAs di Operations Manager per OMS</span><span class="sxs-lookup"><span data-stu-id="5cdca-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="5cdca-147">Log Analytics in OMS usa l'agente e il gruppo di gestione di Operations Manager per raccogliere e inviare dati al servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="5cdca-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="5cdca-148">OMS si basa si Management Pack per i carichi di lavoro per offrire servizi a valore aggiunto.</span><span class="sxs-lookup"><span data-stu-id="5cdca-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="5cdca-149">Ogni carico di lavoro richiede privilegi specifici per eseguire i Management Pack in un contesto di sicurezza diverso, ad esempio un account di dominio.</span><span class="sxs-lookup"><span data-stu-id="5cdca-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="5cdca-150">È necessario fornire informazioni sulle credenziali configurando un account RunAs di Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="5cdca-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="5cdca-151">Usare le informazioni seguenti per impostare l'account RunAs di Operations Manager per SQL Assessment.</span><span class="sxs-lookup"><span data-stu-id="5cdca-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="5cdca-152">Impostare l'account RunAs per SQL Assessment</span><span class="sxs-lookup"><span data-stu-id="5cdca-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="5cdca-153">Se si usa già il Management Pack di SQL Server, è consigliabile usare l'account RunAs corrispondente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="5cdca-154">Per configurare l'account RunAs di SQL in Operations Console</span><span class="sxs-lookup"><span data-stu-id="5cdca-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="5cdca-155">Se si usa l'agente diretto OMS, anziché l'agente SCOM, il management pack viene sempre eseguito nel contesto di sicurezza dell'account di sistema locale.</span><span class="sxs-lookup"><span data-stu-id="5cdca-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="5cdca-156">Ignorare i passaggi seguenti da 1 a 5 ed eseguire l'esempio di T-SQL o PowerShell, specificando NT AUTHORITY\SYSTEM come nome utente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="5cdca-157">In Operations Manager aprire la console operatore e quindi fare clic su **Administration**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="5cdca-158">In **Esegui come configurazione**, fare clic su **Profili** e aprire **Profilo RunAs di OMS SQL Assessment**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="5cdca-159">Nella pagina **Esegui come account** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="5cdca-160">Selezionare un account RunAs Windows che contiene le credenziali necessarie per SQL Server oppure fare clic su **New** per crearne uno.</span><span class="sxs-lookup"><span data-stu-id="5cdca-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5cdca-161">Il tipo dell'account RunAs deve essere Windows.</span><span class="sxs-lookup"><span data-stu-id="5cdca-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="5cdca-162">L'account RunAs deve appartenere anche al gruppo Local Administrators in tutti i server Windows che ospitano istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5cdca-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="5cdca-163">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-163">Click **Save**.</span></span>
6. <span data-ttu-id="5cdca-164">Modificare ed eseguire il seguente esempio T-SQL in ciascuna istanza di SQL Server per concedere le autorizzazioni minime richieste dall'account RunAs per eseguire la valutazione SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="5cdca-165">Tuttavia, non è necessario farlo se l'account RunAs fa già parte del ruolo server sysadmin nelle istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5cdca-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="5cdca-166">Per configurare l'account RunAs di SQL con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cdca-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="5cdca-167">Aprire una finestra di PowerShell ed eseguire il seguente script dopo averlo aggiornato con le informazioni:</span><span class="sxs-lookup"><span data-stu-id="5cdca-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="5cdca-168">Informazioni sulla classificazione in ordine di priorità delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="5cdca-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="5cdca-169">A ogni raccomandazione generata viene assegnato un valore di ponderazione che identifica l'importanza relativa della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="5cdca-170">Vengono visualizzate solo le dieci raccomandazioni più importanti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="5cdca-171">Come vengono calcolate le ponderazioni</span><span class="sxs-lookup"><span data-stu-id="5cdca-171">How weights are calculated</span></span>
<span data-ttu-id="5cdca-172">Le ponderazioni sono valori aggregati che si basano su tre fattori chiave:</span><span class="sxs-lookup"><span data-stu-id="5cdca-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="5cdca-173">La *probabilità* che un problema identificato causi inconvenienti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="5cdca-174">Una probabilità più elevata equivale a un punteggio complessivamente maggiore per la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="5cdca-175">L' *impatto* del problema per l'organizzazione se causa effettivamente un problema.</span><span class="sxs-lookup"><span data-stu-id="5cdca-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="5cdca-176">Un impatto più elevato equivale a un punteggio complessivamente maggiore per la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="5cdca-177">Il *lavoro* richiesto per implementare la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="5cdca-178">Un lavoro richiesto più elevato equivale a un punteggio complessivamente inferiore per la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="5cdca-179">La ponderazione per ogni raccomandazione è espressa come percentuale del punteggio totale disponibile per ogni area di interesse.</span><span class="sxs-lookup"><span data-stu-id="5cdca-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="5cdca-180">Ad esempio, se una raccomandazione nell'area di interesse relativa a sicurezza e conformità ha un punteggio pari al 5%, l'implementazione della raccomandazione aumenterà del 5% il punteggio complessivo di quell'area.</span><span class="sxs-lookup"><span data-stu-id="5cdca-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="5cdca-181">Aree di interesse</span><span class="sxs-lookup"><span data-stu-id="5cdca-181">Focus areas</span></span>
<span data-ttu-id="5cdca-182">**Sicurezza e conformità** : quest'area di interesse descrive raccomandazioni relative alle potenziali minacce e violazioni della sicurezza, ai criteri aziendali e ai requisiti di conformità tecnici, legali e normativi.</span><span class="sxs-lookup"><span data-stu-id="5cdca-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="5cdca-183">**Disponibilità e continuità aziendale** : quest'area di interesse descrive raccomandazioni relative alla disponibilità del servizio, alla resilienza dell'infrastruttura e alla protezione aziendale.</span><span class="sxs-lookup"><span data-stu-id="5cdca-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="5cdca-184">**Prestazioni e scalabilità** : quest'area di interesse descrive raccomandazioni utili per favorire la crescita dell'infrastruttura IT dell'organizzazione, assicurando che l'ambiente IT soddisfi gli attuali requisiti in termini di prestazioni e possa rispondere alle mutevoli esigenze dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="5cdca-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="5cdca-185">**Aggiornamento, migrazione e distribuzione**: quest'area di interesse mostra le raccomandazioni utili per aggiornare, eseguire la migrazione e distribuire SQL Server nell'infrastruttura esistente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="5cdca-186">**Operazioni e monitoraggio**: quest'area di interesse mostra le raccomandazioni utili per semplificare le operazioni IT, implementare la manutenzione preventiva e ottimizzare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5cdca-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="5cdca-187">**Gestione modifiche e configurazione**: quest'area di interesse mostra le raccomandazioni utili per proteggere le operazioni quotidiane, assicurare che le modifiche non influiscano negativamente sull'infrastruttura, stabilire procedure di controllo delle modifiche e rilevare e monitorare le configurazioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="5cdca-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="5cdca-188">È consigliabile mirare a ottenere un punteggio del 100% in tutte le aree di interesse?</span><span class="sxs-lookup"><span data-stu-id="5cdca-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="5cdca-189">Non necessariamente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-189">Not necessarily.</span></span> <span data-ttu-id="5cdca-190">Le raccomandazioni si basano sulla conoscenza e sull'esperienza acquisite dai tecnici Microsoft attraverso migliaia di visite dei clienti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="5cdca-191">Non esistono tuttavia due infrastrutture di server uguali e raccomandazioni specifiche possono essere più o meno pertinenti per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="5cdca-192">Ad esempio, alcune raccomandazioni sulla sicurezza possono risultare meno pertinenti se le macchine virtuali non sono esposte a Internet.</span><span class="sxs-lookup"><span data-stu-id="5cdca-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="5cdca-193">Alcune raccomandazioni sulla disponibilità possono risultare meno pertinenti per i servizi che forniscono creazione di report e raccolta dei dati ad hoc a bassa priorità.</span><span class="sxs-lookup"><span data-stu-id="5cdca-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="5cdca-194">I problemi che possono essere importanti per un'azienda collaudata possono esserlo meno per una start-up.</span><span class="sxs-lookup"><span data-stu-id="5cdca-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="5cdca-195">È consigliabile identificare quali sono le proprie aree di interesse prioritarie e quindi osservare il cambiamento dei punteggi nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5cdca-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="5cdca-196">Ogni raccomandazione include informazioni aggiuntive sui motivi per cui potrebbe essere importante.</span><span class="sxs-lookup"><span data-stu-id="5cdca-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="5cdca-197">È consigliabile usare queste informazioni aggiuntive per valutare se l'implementazione della raccomandazione è appropriata, a seconda della natura dei servizi IT e delle esigenze aziendali dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="5cdca-198">Usare le raccomandazioni relative all'area di interesse della valutazione</span><span class="sxs-lookup"><span data-stu-id="5cdca-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="5cdca-199">Prima di poter usare una soluzione di valutazione in OMS, è necessario averla installata.</span><span class="sxs-lookup"><span data-stu-id="5cdca-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="5cdca-200">Per altre informazioni sull'installazione di soluzioni, vedere [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5cdca-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="5cdca-201">Dopo l'installazione, sarà possibile visualizzare il riepilogo delle raccomandazioni usando il riquadro SQL Assessment della pagina Overview in OMS.</span><span class="sxs-lookup"><span data-stu-id="5cdca-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="5cdca-202">Visualizzare il riepilogo delle valutazioni relative alla conformità per l'infrastruttura, quindi visualizzare le raccomandazioni nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="5cdca-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="5cdca-203">Per visualizzare le raccomandazioni per un'area di interesse e applicare un'azione correttiva</span><span class="sxs-lookup"><span data-stu-id="5cdca-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="5cdca-204">Nella pagina **Panoramica** fare clic sul riquadro **SQL Assessment**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="5cdca-205">Nella pagina **SQL Assessment** verificare le informazioni di riepilogo in uno dei pannelli dell'area di interesse, quindi fare clic su un'area specifica per visualizzare le raccomandazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="5cdca-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="5cdca-206">In una delle pagine relative alle aree di interesse è possibile visualizzare le raccomandazioni relative all'ambiente specifico, classificate in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="5cdca-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="5cdca-207">Fare clic su una raccomandazione in **Affected Objects** (Oggetti interessati) per visualizzare i dettagli relativi al motivo per cui è stata generata.</span><span class="sxs-lookup"><span data-stu-id="5cdca-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="5cdca-208">![immagine delle raccomandazioni di SQL Assessment](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="5cdca-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="5cdca-209">È possibile eseguire le azioni correttive suggerite in **Suggested Actions**(Azioni suggerite).</span><span class="sxs-lookup"><span data-stu-id="5cdca-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="5cdca-210">Dopo la risoluzione dell'elemento, le valutazioni successive indicheranno che le azioni consigliate sono state effettuate e il punteggio relativo alla conformità aumenterà.</span><span class="sxs-lookup"><span data-stu-id="5cdca-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="5cdca-211">Gli elementi corretti vengono visualizzati come **Passed Objects**.</span><span class="sxs-lookup"><span data-stu-id="5cdca-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="5cdca-212">Ignorare le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="5cdca-212">Ignore recommendations</span></span>
<span data-ttu-id="5cdca-213">Per ignorare delle raccomandazioni è possibile creare un file di testo che OMS userà per impedirne la visualizzazione nei risultati della valutazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="5cdca-214">Per identificare le raccomandazioni che verranno ignorate</span><span class="sxs-lookup"><span data-stu-id="5cdca-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="5cdca-215">Accedere all'area di lavoro e aprire Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="5cdca-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="5cdca-216">Usare la query seguente per elencare le raccomandazioni non riuscite per i computer nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="5cdca-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="5cdca-217">Ecco lo screenshot che mostra la query di ricerca nei log: ![raccomandazioni con esito negativo](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="5cdca-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="5cdca-218">Scegliere le raccomandazioni da ignorare.</span><span class="sxs-lookup"><span data-stu-id="5cdca-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="5cdca-219">Nella procedura successiva verranno usati i valori per ID raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="5cdca-220">Per creare e usare un file di testo IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="5cdca-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="5cdca-221">Creare un file denominato IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="5cdca-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="5cdca-222">Incollare o digitare ogni ID raccomandazione per ogni raccomandazione che OMS dovrà ignorare in una riga separata e quindi salvare e chiudere il file.</span><span class="sxs-lookup"><span data-stu-id="5cdca-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="5cdca-223">Inserire il file nella cartella seguente in ogni computer in cui si vuole che OMS ignori le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="5cdca-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="5cdca-224">Nei computer con Microsoft Monitoring Agent, connesso direttamente o tramite Operations Manager, *SystemDrive*:\Programmi\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="5cdca-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="5cdca-225">Nel server di gestione Operations Manager *SystemDrive*: \Programmi\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="5cdca-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="5cdca-226">Per verificare che le raccomandazioni vengano ignorate</span><span class="sxs-lookup"><span data-stu-id="5cdca-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="5cdca-227">Dopo la successiva esecuzione della valutazione pianificata, per impostazione predefinita ogni 7 giorni, le raccomandazioni specificate sono contrassegnate come ignorate e non verranno visualizzate nel dashboard di valutazione.</span><span class="sxs-lookup"><span data-stu-id="5cdca-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="5cdca-228">È possibile usare le query di Ricerca log seguenti per elencare tutte le raccomandazioni ignorate.</span><span class="sxs-lookup"><span data-stu-id="5cdca-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="5cdca-229">Se in seguito si decide che si vogliono vedere le raccomandazioni ignorate, rimuovere eventuali file IgnoreRecommendations.txt oppure rimuovere gli ID raccomandazione dagli stessi.</span><span class="sxs-lookup"><span data-stu-id="5cdca-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="5cdca-230">Domande frequenti sulla soluzione SQL Assessment</span><span class="sxs-lookup"><span data-stu-id="5cdca-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="5cdca-231">*Con che frequenza viene eseguita la valutazione?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="5cdca-232">La valutazione viene eseguita ogni 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="5cdca-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="5cdca-233">*È possibile configurare la frequenza di esecuzione della valutazione?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="5cdca-234">Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="5cdca-234">Not at this time.</span></span>

<span data-ttu-id="5cdca-235">*Se viene rilevato un altro server dopo l'aggiunta della soluzione SQL Assessment, il server verrà valutato?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="5cdca-236">Sì, a partire dal rilevamento verrà valutato ogni 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="5cdca-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="5cdca-237">*Se un server viene rimosso, quando sarà rimosso dalla valutazione?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="5cdca-238">Se un server non invia dati per 3 settimane, verrà rimosso.</span><span class="sxs-lookup"><span data-stu-id="5cdca-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="5cdca-239">*Qual è il nome del processo che esegue la raccolta di dati?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="5cdca-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="5cdca-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="5cdca-241">*Quanto tempo occorre per la raccolta di dati?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="5cdca-242">La raccolta di dati effettiva sul server richiede circa 1 ora.</span><span class="sxs-lookup"><span data-stu-id="5cdca-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="5cdca-243">È possibile che sia necessario più tempo nei server in cui è presente un numero elevato di istanze o database SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="5cdca-244">*Quali tipi di dati vengono raccolti?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="5cdca-245">Vengono raccolti i tipi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="5cdca-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="5cdca-246">WMI</span><span class="sxs-lookup"><span data-stu-id="5cdca-246">WMI</span></span>
  * <span data-ttu-id="5cdca-247">Registro</span><span class="sxs-lookup"><span data-stu-id="5cdca-247">Registry</span></span>
  * <span data-ttu-id="5cdca-248">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="5cdca-248">Performance counters</span></span>
  * <span data-ttu-id="5cdca-249">DMV (Dynamic Management View) di SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="5cdca-250">*È possibile definire l'orario per la raccolta di dati?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="5cdca-251">Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="5cdca-251">Not at this time.</span></span>

<span data-ttu-id="5cdca-252">*Perché è necessario configurare un account RunAs?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="5cdca-253">Per un server SQL vengono eseguite alcune SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="5cdca-254">Per permetterne l'esecuzione, è necessario usare un account RunAs con autorizzazioni di tipo VISUALIZZAZIONE STATO DEL SERVER per SQL.</span><span class="sxs-lookup"><span data-stu-id="5cdca-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="5cdca-255">Per eseguire query relative a WMI, sono inoltre necessarie credenziali di amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="5cdca-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="5cdca-256">*Perché vengono visualizzate solo le prime 10 raccomandazioni?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="5cdca-257">Invece di esaminare un lunghissimo elenco completo di attività, è consigliabile concentrare l'attenzione sulle raccomandazioni con priorità maggiore.</span><span class="sxs-lookup"><span data-stu-id="5cdca-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="5cdca-258">Dopo la verifica delle raccomandazioni principali, verranno rese disponibili raccomandazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="5cdca-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="5cdca-259">Se si preferisce visualizzare l'elenco dettagliato, usare la ricerca log di OMS per mostrare tutte le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="5cdca-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="5cdca-260">*È possibile ignorare una raccomandazione?*</span><span class="sxs-lookup"><span data-stu-id="5cdca-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="5cdca-261">Sì, vedere la sezione [Ignorare le raccomandazioni](#ignore-recommendations) sopra.</span><span class="sxs-lookup"><span data-stu-id="5cdca-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cdca-262">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5cdca-262">Next steps</span></span>
* <span data-ttu-id="5cdca-263">[Eseguire ricerche nei log](log-analytics-log-searches.md) per visualizzare raccomandazioni e dati dettagliati di SQL Assessment.</span><span class="sxs-lookup"><span data-stu-id="5cdca-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
