---
title: Gestire ruoli del database e utenti in Azure Analysis Services | Microsoft Docs
description: Informazioni su come gestire ruoli del database e utenti in un server Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="b3d4b-103">Gestire ruoli del database e utenti</span><span class="sxs-lookup"><span data-stu-id="b3d4b-103">Manage database roles and users</span></span>

<span data-ttu-id="b3d4b-104">A livello di database modello, tutti gli utenti devono appartenere a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="b3d4b-105">I ruoli definiscono gli utenti con determinate autorizzazioni per il database modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="b3d4b-106">Qualsiasi gruppo di sicurezza o utente aggiunto a un ruolo deve avere un account in un tenant di Azure AD nella stessa sottoscrizione del server.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="b3d4b-107">La modalità di definizione dei ruoli varia a seconda dello strumento in uso, ma l'effetto è lo stesso.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="b3d4b-108">Le autorizzazioni di ruoli includono:</span><span class="sxs-lookup"><span data-stu-id="b3d4b-108">Role permissions include:</span></span>
*  <span data-ttu-id="b3d4b-109">**Amministratore**: utenti che dispongono di autorizzazioni complete per il database.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="b3d4b-110">I ruoli del database con autorizzazioni di amministratore sono diversi dagli amministratori di server.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="b3d4b-111">**Elabora**: utenti che possono connettersi ed eseguire operazioni di elaborazione nel database e analizzare i dati del database modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="b3d4b-112">**Lettura**: utenti che possono usare un'applicazione client per connettersi e analizzare i dati del database modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="b3d4b-113">Quando si crea un progetto di modello tabulare, si creano ruoli e si aggiungono utenti o gruppi a questi ruoli usando Gestione ruoli in SSDT.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="b3d4b-114">Quando si esegue la distribuzione in un server, si usano SQL Server Management Studio (SSMS), [i cmdlet di PowerShell per Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx) o [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) per aggiungere o rimuovere ruoli e membri utente.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="b3d4b-115">Per aggiungere o gestire ruoli e utenti in SSDT</span><span class="sxs-lookup"><span data-stu-id="b3d4b-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="b3d4b-116">In SSDT > **Esplora modelli tabulari** fare clic con il pulsante destro del mouse su **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="b3d4b-117">In **Gestione ruoli** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="b3d4b-118">Digitare un nome per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="b3d4b-119">Per impostazione predefinita, il nome del ruolo predefinito è numerato in modo incrementale per ogni nuovo ruolo.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="b3d4b-120">È consigliabile digitare un nome che identifichi con precisione il tipo di membro, ad esempio responsabili finanze o esperti di risorse umane.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="b3d4b-121">Selezionare una delle seguenti autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="b3d4b-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="b3d4b-122">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b3d4b-122">Permission</span></span>|<span data-ttu-id="b3d4b-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b3d4b-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="b3d4b-124">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-124">**None**</span></span>|<span data-ttu-id="b3d4b-125">I membri non possono modificare lo schema del modello e non possono eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="b3d4b-126">**Lettura**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-126">**Read**</span></span>|<span data-ttu-id="b3d4b-127">I membri possono eseguire query su dati, in base ai filtri di riga, ma non possono modificare lo schema del modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="b3d4b-128">**Lettura ed elaborazione**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-128">**Read and Process**</span></span>|<span data-ttu-id="b3d4b-129">I membri possono eseguire query su dati in base ai filtri a livello di riga ed eseguire operazioni Elabora ed Elabora tutto, ma non possono modificare lo schema del modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="b3d4b-130">**Processo**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-130">**Process**</span></span>|<span data-ttu-id="b3d4b-131">I membri possono eseguire operazioni Elabora ed Elabora tutto.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="b3d4b-132">Non possono modificare lo schema del modello ed eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="b3d4b-133">**Amministratore**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-133">**Administrator**</span></span>|<span data-ttu-id="b3d4b-134">I membri possono modificare lo schema del modello ed eseguire query su tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="b3d4b-135">Se il ruolo che si sta creando dispone delle autorizzazioni Lettura o Lettura ed elaborazione, è possibile aggiungere filtri di riga usando una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="b3d4b-136">Fare clic sulla scheda **Filtri di riga**, quindi selezionare una tabella, quindi scegliere il campo **Filtro DAX** e quindi digitare una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="b3d4b-137">Fare clic su **Membri** > **Aggiungi esterno**.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="b3d4b-138">In **Aggiungi membro esterno** immettere gli utenti o i gruppi nel tenant di Azure AD dall'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="b3d4b-139">Dopo avere fatto clic su OK e avere chiuso Gestione ruoli, i ruoli e i membri del ruolo vengono visualizzati in Esplora modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Ruoli e utenti in Esplora modelli tabulari](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="b3d4b-141">Eseguire la distribuzione in un server di Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="b3d4b-142">Per aggiungere o gestire ruoli e utenti in SSMS</span><span class="sxs-lookup"><span data-stu-id="b3d4b-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="b3d4b-143">Per aggiungere ruoli e utenti a un database modello distribuito, è necessario connettersi al server come amministratore del server o già in un ruolo del database con autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="b3d4b-144">In Esplora oggetti fare clic con il pulsante destro del mouse su **Ruoli** > **Nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="b3d4b-145">In **Crea ruolo** immettere il nome di un ruolo e una descrizione.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="b3d4b-146">Selezionare un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-146">Select a permission.</span></span>
   |<span data-ttu-id="b3d4b-147">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b3d4b-147">Permission</span></span>|<span data-ttu-id="b3d4b-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b3d4b-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="b3d4b-149">**Controllo completo (amministratore)**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="b3d4b-150">I membri possono modificare lo schema del modello, eseguire operazioni di elaborazione e query su tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="b3d4b-151">**Elabora database**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-151">**Process database**</span></span>|<span data-ttu-id="b3d4b-152">I membri possono eseguire operazioni Elabora ed Elabora tutto.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="b3d4b-153">Non possono modificare lo schema del modello ed eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="b3d4b-154">**Lettura**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-154">**Read**</span></span>|<span data-ttu-id="b3d4b-155">I membri possono eseguire query su dati, in base ai filtri di riga, ma non possono modificare lo schema del modello.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="b3d4b-156">Fare clic su **Appartenenza**, quindi immettere un utente o un gruppo nel tenant di Azure AD dall'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Add user](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="b3d4b-158">Se il ruolo che si sta creando dispone dell'autorizzazione Lettura, è possibile aggiungere filtri di riga usando una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="b3d4b-159">Fare clic su **Filtri di riga**, selezionare una tabella e quindi digitare una formula DAX nel campo **Filtro DAX**.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="b3d4b-160">Per aggiungere ruoli e utenti usando uno script TMSL</span><span class="sxs-lookup"><span data-stu-id="b3d4b-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="b3d4b-161">È possibile eseguire uno script TMSL nella finestra XMLA in SSMS o usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="b3d4b-162">Usare il comando [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) e l'oggetto [Ruoli](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl).</span><span class="sxs-lookup"><span data-stu-id="b3d4b-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="b3d4b-163">**Script di esempio del linguaggio di scripting del modello tabulare**</span><span class="sxs-lookup"><span data-stu-id="b3d4b-163">**Sample TMSL script**</span></span>

<span data-ttu-id="b3d4b-164">In questo esempio, un gruppo e un utente esterno B2B vengono aggiunti al ruolo analista con autorizzazioni Lettura per il database SalesBI.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="b3d4b-165">Sia il gruppo che l'utente esterno devono trovarsi nello stesso tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="b3d4b-166">Per aggiungere ruoli e utenti usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3d4b-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="b3d4b-167">Il modulo [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) fornisce cmdlet di gestione database specifici dell'attività, oltre al cmdlet Invoke-ASCmd per utilizzo generico che accetta una query o uno script TMSL (Tabular Model Scripting Language).</span><span class="sxs-lookup"><span data-stu-id="b3d4b-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="b3d4b-168">I cmdlet seguenti vengono usati per la gestione di utenti e ruoli del database.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="b3d4b-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b3d4b-169">Cmdlet</span></span>|<span data-ttu-id="b3d4b-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b3d4b-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="b3d4b-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="b3d4b-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="b3d4b-172">Aggiunge un membro a un ruolo del database.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="b3d4b-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="b3d4b-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="b3d4b-174">Rimuove un membro da un ruolo del database.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="b3d4b-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="b3d4b-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="b3d4b-176">Esegue uno script TMSL.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="b3d4b-177">Filtri di riga</span><span class="sxs-lookup"><span data-stu-id="b3d4b-177">Row filters</span></span>  
<span data-ttu-id="b3d4b-178">I filtri di riga definiscono le righe di una tabella su cui i membri di uno specifico ruolo possono eseguire query.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="b3d4b-179">Vengono definiti per ogni tabella in un modello usando formule DAX.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="b3d4b-180">I filtri di riga possono essere definiti solo per i ruoli con le autorizzazioni Lettura e Lettura ed elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="b3d4b-181">Per impostazione predefinita, se non si definisce un filtro di riga per una determinata tabella, i membri possono eseguire query su tutte le righe della tabella a meno che non vengano applicati filtri incrociati da un'altra tabella.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="b3d4b-182">I filtri di riga richiedono una formula DAX, che deve restituire un valore TRUE/FALSE, per definire le righe su cui i membri del ruolo specifico possono eseguire query.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="b3d4b-183">Non è possibile eseguire query su righe non incluse nella formula DAX.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="b3d4b-184">Ad esempio, nel caso della tabella Customers con l'espressione di filtri di riga seguente, *=Customers [Country] = 'USA'*, i membri del ruolo Sales possono visualizzare solo i clienti negli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="b3d4b-185">I filtri di riga si applicano alle righe specificate e alle righe correlate.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="b3d4b-186">Quando una tabella contiene più relazioni, i filtri applicano la sicurezza per la relazione che è attiva.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="b3d4b-187">I filtri di riga vengono intersecati con altri filtri di riga definiti per le tabelle correlate, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b3d4b-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="b3d4b-188">Table</span><span class="sxs-lookup"><span data-stu-id="b3d4b-188">Table</span></span>|<span data-ttu-id="b3d4b-189">Espressione DAX</span><span class="sxs-lookup"><span data-stu-id="b3d4b-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="b3d4b-190">Region</span><span class="sxs-lookup"><span data-stu-id="b3d4b-190">Region</span></span>|<span data-ttu-id="b3d4b-191">=Region[Country]="USA"</span><span class="sxs-lookup"><span data-stu-id="b3d4b-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="b3d4b-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="b3d4b-192">ProductCategory</span></span>|<span data-ttu-id="b3d4b-193">=ProductCategory[Name]="Bicycles"</span><span class="sxs-lookup"><span data-stu-id="b3d4b-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="b3d4b-194">Transazioni</span><span class="sxs-lookup"><span data-stu-id="b3d4b-194">Transactions</span></span>|<span data-ttu-id="b3d4b-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="b3d4b-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="b3d4b-196">I membri possono eseguire query sulle righe di dati, in cui il cliente si trova negli Stati Uniti, la categoria del prodotto è biciclette e l'anno è il 2016.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="b3d4b-197">Gli utenti non possono eseguire query sulle transazioni all'esterno degli Stati Uniti, non relative alle biciclette o all'anno 2016, a meno che non siano membri di un altro ruolo che prevede queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="b3d4b-198">È possibile usare il filtro, *=FALSE()*, per negare l'accesso a tutte le righe di un'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="b3d4b-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3d4b-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3d4b-199">Next steps</span></span>
  <span data-ttu-id="b3d4b-200">[Gestire gli amministratori di server](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="b3d4b-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="b3d4b-201">Gestire Azure Analysis Services con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3d4b-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="b3d4b-202">Riferimento al Tabular Model Scripting Language (TMSL)</span><span class="sxs-lookup"><span data-stu-id="b3d4b-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

