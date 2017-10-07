---
title: ruoli e utenti in Azure Analysis Services del database aaaManage | Documenti Microsoft
description: Informazioni su come toomanage database ruoli e utenti in un server Analysis Services in Azure.
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="31e7e-103">Gestire ruoli del database e utenti</span><span class="sxs-lookup"><span data-stu-id="31e7e-103">Manage database roles and users</span></span>

<span data-ttu-id="31e7e-104">A livello di database modello hello, tutti gli utenti devono appartenere tooa ruolo.</span><span class="sxs-lookup"><span data-stu-id="31e7e-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="31e7e-105">I ruoli definiscono gli utenti con determinate autorizzazioni per database modello hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="31e7e-106">Qualsiasi utente o gruppo di protezione aggiunta tooa ruolo deve includere un account in un tenant di Azure AD in hello stessa sottoscrizione server hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="31e7e-107">Come definire i ruoli è diverso a seconda dello strumento hello che è utilizzato, ma è hello effetto hello stesso.</span><span class="sxs-lookup"><span data-stu-id="31e7e-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="31e7e-108">Le autorizzazioni di ruoli includono:</span><span class="sxs-lookup"><span data-stu-id="31e7e-108">Role permissions include:</span></span>
*  <span data-ttu-id="31e7e-109">**Amministratore** -gli utenti hanno le autorizzazioni complete per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="31e7e-110">I ruoli del database con autorizzazioni di amministratore sono diversi dagli amministratori di server.</span><span class="sxs-lookup"><span data-stu-id="31e7e-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="31e7e-111">**Processo** -gli utenti possono connettersi tooand eseguire operazioni di elaborazione nel database di hello e analizzare i dati del database modello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="31e7e-112">**Lettura** -gli utenti possono usare un client applicazione tooconnect tooand analizzare i dati del database modello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="31e7e-113">Quando si crea un progetto di modello tabulare, creare i ruoli e aggiungere utenti o gruppi di ruoli toothose tramite Gestione ruoli in SSDT.</span><span class="sxs-lookup"><span data-stu-id="31e7e-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="31e7e-114">Quando è distribuito tooa server, utilizzare SQL Server Management Studio, [i cmdlet di PowerShell per Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), o [linguaggio di Scripting del modello tabulare](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) o rimuovere ruoli e membri di un utente.</span><span class="sxs-lookup"><span data-stu-id="31e7e-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="31e7e-115">tooadd o gestire ruoli e utenti in SSDT</span><span class="sxs-lookup"><span data-stu-id="31e7e-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="31e7e-116">In SSDT > **Esplora modelli tabulari** fare clic con il pulsante destro del mouse su **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="31e7e-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="31e7e-117">In **Gestione ruoli** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="31e7e-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="31e7e-118">Digitare un nome per il ruolo di hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="31e7e-119">Per impostazione predefinita, il nome di hello del ruolo predefinito di hello è numerato in modo incrementale per ogni nuovo ruolo.</span><span class="sxs-lookup"><span data-stu-id="31e7e-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="31e7e-120">È consigliabile che si digita un nome che identifichi il tipo membro hello, ad esempio responsabili finanze o esperti di risorse umane.</span><span class="sxs-lookup"><span data-stu-id="31e7e-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="31e7e-121">Selezionare una di queste autorizzazioni hello:</span><span class="sxs-lookup"><span data-stu-id="31e7e-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="31e7e-122">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="31e7e-122">Permission</span></span>|<span data-ttu-id="31e7e-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31e7e-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="31e7e-124">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="31e7e-124">**None**</span></span>|<span data-ttu-id="31e7e-125">I membri non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="31e7e-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="31e7e-126">**Lettura**</span><span class="sxs-lookup"><span data-stu-id="31e7e-126">**Read**</span></span>|<span data-ttu-id="31e7e-127">I membri possono eseguire query dati (in base ai filtri di riga), ma non è possibile modificare lo schema del modello hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="31e7e-128">**Lettura ed elaborazione**</span><span class="sxs-lookup"><span data-stu-id="31e7e-128">**Read and Process**</span></span>|<span data-ttu-id="31e7e-129">I membri possono eseguire una query dei dati (in base ai filtri a livello di riga) e l'esecuzione di operazioni elabora ed elabora tutto, ma non è possibile modificare lo schema del modello hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="31e7e-130">**Processo**</span><span class="sxs-lookup"><span data-stu-id="31e7e-130">**Process**</span></span>|<span data-ttu-id="31e7e-131">I membri possono eseguire operazioni Elabora ed Elabora tutto.</span><span class="sxs-lookup"><span data-stu-id="31e7e-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="31e7e-132">Non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="31e7e-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="31e7e-133">**Amministratore**</span><span class="sxs-lookup"><span data-stu-id="31e7e-133">**Administrator**</span></span>|<span data-ttu-id="31e7e-134">I membri possono modificare lo schema del modello hello e tutti i dati di query.</span><span class="sxs-lookup"><span data-stu-id="31e7e-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="31e7e-135">Se il ruolo di hello sono creazione è di lettura o autorizzazione di lettura ed elaborazione, è possibile aggiungere filtri di riga tramite una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="31e7e-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="31e7e-136">Fare clic su hello **i filtri di riga** scheda, quindi selezionare una tabella, quindi fare clic su hello **filtro DAX** campo e quindi digitare una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="31e7e-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="31e7e-137">Fare clic su **Membri** > **Aggiungi esterno**.</span><span class="sxs-lookup"><span data-stu-id="31e7e-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="31e7e-138">In **Aggiungi membro esterno** immettere gli utenti o i gruppi nel tenant di Azure AD dall'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="31e7e-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="31e7e-139">Dopo avere fatto clic su OK e avere chiuso Gestione ruoli, i ruoli e i membri del ruolo vengono visualizzati in Esplora modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="31e7e-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Ruoli e utenti in Esplora modelli tabulari](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="31e7e-141">Distribuire il server Azure Analysis Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="31e7e-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="31e7e-142">tooadd o gestire ruoli e utenti in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="31e7e-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="31e7e-143">tooadd ruoli e utenti tooa distribuita database modello, è necessario essere connessi toohello server come un amministratore del Server o già in un ruolo del database con autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="31e7e-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="31e7e-144">In Esplora oggetti fare clic con il pulsante destro del mouse su **Ruoli** > **Nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="31e7e-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="31e7e-145">In **Crea ruolo** immettere il nome di un ruolo e una descrizione.</span><span class="sxs-lookup"><span data-stu-id="31e7e-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="31e7e-146">Selezionare un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="31e7e-146">Select a permission.</span></span>
   |<span data-ttu-id="31e7e-147">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="31e7e-147">Permission</span></span>|<span data-ttu-id="31e7e-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31e7e-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="31e7e-149">**Controllo completo (amministratore)**</span><span class="sxs-lookup"><span data-stu-id="31e7e-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="31e7e-150">I membri possono modificare schema del modello hello, elaborare ed eseguire query su tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="31e7e-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="31e7e-151">**Elabora database**</span><span class="sxs-lookup"><span data-stu-id="31e7e-151">**Process database**</span></span>|<span data-ttu-id="31e7e-152">I membri possono eseguire operazioni Elabora ed Elabora tutto.</span><span class="sxs-lookup"><span data-stu-id="31e7e-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="31e7e-153">Non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="31e7e-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="31e7e-154">**Lettura**</span><span class="sxs-lookup"><span data-stu-id="31e7e-154">**Read**</span></span>|<span data-ttu-id="31e7e-155">I membri possono eseguire query dati (in base ai filtri di riga), ma non è possibile modificare lo schema del modello hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="31e7e-156">Fare clic su **Appartenenza**, quindi immettere un utente o un gruppo nel tenant di Azure AD dall'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="31e7e-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Add user](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="31e7e-158">Se il ruolo di hello che si sta creando dispone dell'autorizzazione di lettura, è possibile aggiungere filtri di riga tramite una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="31e7e-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="31e7e-159">Fare clic su **i filtri di riga**, selezionare una tabella e quindi digitare una formula DAX in hello **filtro DAX** campo.</span><span class="sxs-lookup"><span data-stu-id="31e7e-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="31e7e-160">tooadd ruoli e utenti usando uno script TMSL</span><span class="sxs-lookup"><span data-stu-id="31e7e-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="31e7e-161">È possibile eseguire uno script TMSL nella finestra XMLA di hello in SQL Server Management Studio o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31e7e-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="31e7e-162">Hello utilizzare [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) comando e hello [ruoli](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) oggetto.</span><span class="sxs-lookup"><span data-stu-id="31e7e-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="31e7e-163">**Script di esempio del linguaggio di scripting del modello tabulare**</span><span class="sxs-lookup"><span data-stu-id="31e7e-163">**Sample TMSL script**</span></span>

<span data-ttu-id="31e7e-164">In questo esempio, un utente esterno B2B e un gruppo vengono aggiunti ruolo analista toohello con autorizzazioni di lettura per il database SalesBI hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="31e7e-165">Entrambi hello utente esterno e gruppo deve trovarsi nello stesso tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31e7e-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
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

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="31e7e-166">tooadd ruoli e utenti tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="31e7e-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="31e7e-167">Hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) modulo fornisce database specifici di attività Gestione cmdlet e hello generiche cmdlet Invoke-ASCmd che accetta un query Tabular Model Scripting Language (TMSL) o uno script.</span><span class="sxs-lookup"><span data-stu-id="31e7e-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="31e7e-168">Hello seguendo i cmdlet utilizzato per gestire utenti e ruoli del database.</span><span class="sxs-lookup"><span data-stu-id="31e7e-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="31e7e-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="31e7e-169">Cmdlet</span></span>|<span data-ttu-id="31e7e-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31e7e-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="31e7e-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="31e7e-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="31e7e-172">Aggiungere un ruolo del database membro tooa.</span><span class="sxs-lookup"><span data-stu-id="31e7e-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="31e7e-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="31e7e-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="31e7e-174">Rimuove un membro da un ruolo del database.</span><span class="sxs-lookup"><span data-stu-id="31e7e-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="31e7e-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="31e7e-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="31e7e-176">Esegue uno script TMSL.</span><span class="sxs-lookup"><span data-stu-id="31e7e-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="31e7e-177">Filtri di riga</span><span class="sxs-lookup"><span data-stu-id="31e7e-177">Row filters</span></span>  
<span data-ttu-id="31e7e-178">I filtri di riga definiscono le righe di una tabella su cui i membri di uno specifico ruolo possono eseguire query.</span><span class="sxs-lookup"><span data-stu-id="31e7e-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="31e7e-179">Vengono definiti per ogni tabella in un modello usando formule DAX.</span><span class="sxs-lookup"><span data-stu-id="31e7e-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="31e7e-180">I filtri di riga possono essere definiti solo per i ruoli con le autorizzazioni Lettura e Lettura ed elaborazione.</span><span class="sxs-lookup"><span data-stu-id="31e7e-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="31e7e-181">Per impostazione predefinita, se un filtro di riga non è definito per una determinata tabella, i membri possono eseguire una query tutte le righe nella tabella hello a meno che non applicato il filtro incrociato da un'altra tabella.</span><span class="sxs-lookup"><span data-stu-id="31e7e-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="31e7e-182">I filtri di riga richiedono una formula DAX, che deve restituire tooa valore TRUE o FALSE, le righe di hello toodefine che i membri di tale particolare ruolo possono eseguire query.</span><span class="sxs-lookup"><span data-stu-id="31e7e-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="31e7e-183">Impossibile recuperare le righe non incluse nella formula DAX hello.</span><span class="sxs-lookup"><span data-stu-id="31e7e-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="31e7e-184">Ad esempio, hello tabella Customers con hello espressione i filtri di riga, seguente *= clienti [Paese] = 'USA'*, i membri del ruolo Sales hello è possono visualizzare solo i clienti in hello USA.</span><span class="sxs-lookup"><span data-stu-id="31e7e-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="31e7e-185">I filtri di riga applicano toohello specificato righe e le righe correlate.</span><span class="sxs-lookup"><span data-stu-id="31e7e-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="31e7e-186">Quando una tabella dispone di più relazioni, filtri si applicano la protezione per relazione hello che è attiva.</span><span class="sxs-lookup"><span data-stu-id="31e7e-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="31e7e-187">I filtri di riga vengono intersecati con altri filtri di riga definiti per le tabelle correlate, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="31e7e-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="31e7e-188">Table</span><span class="sxs-lookup"><span data-stu-id="31e7e-188">Table</span></span>|<span data-ttu-id="31e7e-189">Espressione DAX</span><span class="sxs-lookup"><span data-stu-id="31e7e-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="31e7e-190">Region</span><span class="sxs-lookup"><span data-stu-id="31e7e-190">Region</span></span>|<span data-ttu-id="31e7e-191">=Region[Country]="USA"</span><span class="sxs-lookup"><span data-stu-id="31e7e-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="31e7e-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="31e7e-192">ProductCategory</span></span>|<span data-ttu-id="31e7e-193">=ProductCategory[Name]="Bicycles"</span><span class="sxs-lookup"><span data-stu-id="31e7e-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="31e7e-194">Transazioni</span><span class="sxs-lookup"><span data-stu-id="31e7e-194">Transactions</span></span>|<span data-ttu-id="31e7e-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="31e7e-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="31e7e-196">effetto Hello è i membri possono eseguire una query le righe di dati in cui hello cliente si trova negli Stati Uniti hello, categoria di prodotto hello è quella delle biciclette e anno hello è 2016.</span><span class="sxs-lookup"><span data-stu-id="31e7e-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="31e7e-197">Gli utenti non è possibile eseguire una query transazioni di fuori di Stati Uniti hello, transazioni che non sono biciclette o le transazioni non 2016 a meno che non sono membri di un altro ruolo che garantisce tali autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="31e7e-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="31e7e-198">È possibile utilizzare il filtro di hello, *=FALSE()*, righe di tooall toodeny accesso per un'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="31e7e-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e7e-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31e7e-199">Next steps</span></span>
  <span data-ttu-id="31e7e-200">[Gestire gli amministratori di server](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="31e7e-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="31e7e-201">Gestire Azure Analysis Services con PowerShell</span><span class="sxs-lookup"><span data-stu-id="31e7e-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="31e7e-202">Riferimento al Tabular Model Scripting Language (TMSL)</span><span class="sxs-lookup"><span data-stu-id="31e7e-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

