---
title: 'Esercitazione su Azure Analysis Services - Lezione 11: Creare ruoli | Microsoft Docs'
description: Descrive come creare ruoli nel progetto per l'esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="cdfff-103">Lezione 11: Creare ruoli</span><span class="sxs-lookup"><span data-stu-id="cdfff-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="cdfff-104">In questa lezione verranno creati ruoli.</span><span class="sxs-lookup"><span data-stu-id="cdfff-104">In this lesson, you create roles.</span></span> <span data-ttu-id="cdfff-105">I ruoli consentono di proteggere i dati e gli oggetti del database del modello, limitando l'accesso solo agli utenti membri del ruolo.</span><span class="sxs-lookup"><span data-stu-id="cdfff-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="cdfff-106">Ogni ruolo è definito con una sola autorizzazione: Nessuna, Lettura, Lettura ed elaborazione, Elaborazione o Amministratore.</span><span class="sxs-lookup"><span data-stu-id="cdfff-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="cdfff-107">I ruoli possono essere definiti durante la creazione dei modelli tramite Gestione ruoli.</span><span class="sxs-lookup"><span data-stu-id="cdfff-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="cdfff-108">Dopo avere distribuito un modello, è possibile gestire i ruoli con SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="cdfff-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="cdfff-109">Per altre informazioni, vedere [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular) (Ruoli).</span><span class="sxs-lookup"><span data-stu-id="cdfff-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="cdfff-110">La creazione di ruoli non è necessaria per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cdfff-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="cdfff-111">Per impostazione predefinita, l'account con cui si esegue l'accesso ha i privilegi di Amministratore per il modello.</span><span class="sxs-lookup"><span data-stu-id="cdfff-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="cdfff-112">Per consentire anche ad altri utenti dell'organizzazione di esplorare il modello usando un client per la creazione di report, tuttavia, è necessario creare almeno un ruolo con autorizzazioni Lettura e aggiungere tali utenti come membri.</span><span class="sxs-lookup"><span data-stu-id="cdfff-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="cdfff-113">Vengono creati tre ruoli:</span><span class="sxs-lookup"><span data-stu-id="cdfff-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="cdfff-114">**Sales Manager** - Questo ruolo può includere gli utenti dell'organizzazione che si vuole dispongano dell'autorizzazione Lettura per tutti gli oggetti e i dati del modello.</span><span class="sxs-lookup"><span data-stu-id="cdfff-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="cdfff-115">**Sales Analyst US** - Questo ruolo può includere gli utenti dell'organizzazione che si vuole possano esplorare solo i dati relativi alle vendite negli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="cdfff-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="cdfff-116">Per questo ruolo si usa una formula DAX per definire un *filtro di riga*, che consente ai membri di visualizzare solo i dati per gli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="cdfff-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="cdfff-117">**Administrator** - Questo ruolo può includere gli utenti a cui si vuole concedere l'autorizzazione Amministratore, che consente l'accesso illimitato e concede le autorizzazioni per eseguire attività amministrative sul database del modello.</span><span class="sxs-lookup"><span data-stu-id="cdfff-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="cdfff-118">Dato che gli account utente e di gruppo di Windows nell'organizzazione sono univoci, è possibile aggiungere gli account dell'organizzazione ai membri.</span><span class="sxs-lookup"><span data-stu-id="cdfff-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="cdfff-119">Tuttavia, per questa esercitazione, è anche possibile non specificare i membri.</span><span class="sxs-lookup"><span data-stu-id="cdfff-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="cdfff-120">È possibile testare l'effetto di ogni ruolo in un secondo momento nella lezione 12: Analizzare in Excel.</span><span class="sxs-lookup"><span data-stu-id="cdfff-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="cdfff-121">Tempo previsto per il completamento della lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="cdfff-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="cdfff-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdfff-122">Prerequisites</span></span>  
<span data-ttu-id="cdfff-123">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="cdfff-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="cdfff-124">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 10: Creare partizioni](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="cdfff-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="cdfff-125">Creare ruoli</span><span class="sxs-lookup"><span data-stu-id="cdfff-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="cdfff-126">Per creare un ruolo utente Sales Manager</span><span class="sxs-lookup"><span data-stu-id="cdfff-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="cdfff-127">In Esplora modelli tabulari fare clic con il pulsante destro del mouse su **Ruoli** > **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="cdfff-128">In Gestione ruoli fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="cdfff-129">Fare clic sul nuovo ruolo e quindi nella colonna **Nome** rinominare il ruolo in **Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="cdfff-130">Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa e quindi selezionare l'autorizzazione **Lettura**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="cdfff-132">Facoltativo: fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cdfff-133">Nella finestra di dialogo **Seleziona utenti o gruppi** immettere gli utenti o i gruppi di Windows dell'organizzazione che si vuole includere nel ruolo.</span><span class="sxs-lookup"><span data-stu-id="cdfff-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="cdfff-134">Per creare un ruolo utente Sales Analyst US</span><span class="sxs-lookup"><span data-stu-id="cdfff-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="cdfff-135">In Gestione ruoli fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="cdfff-136">Rinominare il ruolo **Sales Analyst US**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="cdfff-137">Assegnare a questo ruolo l'autorizzazione **Lettura**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="cdfff-138">Fare clic sulla scheda Filtri di riga e quindi, solo per la per tabella **DimGeography**, digitare la formula seguente nella colonna Filtro DAX:</span><span class="sxs-lookup"><span data-stu-id="cdfff-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="cdfff-139">Una formula per il filtro di riga deve restituire un valore booleano (TRUE/FALSE).</span><span class="sxs-lookup"><span data-stu-id="cdfff-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="cdfff-140">Con questa formula si specifica che devono essere visibili per l'utente solo le righe con il valore "US" per Country Region Code.</span><span class="sxs-lookup"><span data-stu-id="cdfff-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="cdfff-142">Facoltativo: fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cdfff-143">Nella finestra di dialogo **Seleziona utenti o gruppi** immettere gli utenti o i gruppi di Windows dell'organizzazione che si vuole includere nel ruolo.</span><span class="sxs-lookup"><span data-stu-id="cdfff-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="cdfff-144">Per creare un ruolo utente Administrator</span><span class="sxs-lookup"><span data-stu-id="cdfff-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="cdfff-145">Fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="cdfff-146">Rinominare il ruolo **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="cdfff-147">Assegnare a questo ruolo l'autorizzazione **Amministratore**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="cdfff-148">Facoltativo: fare clic sulla scheda **Membri** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cdfff-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="cdfff-149">Nella finestra di dialogo **Seleziona utenti o gruppi** immettere gli utenti o i gruppi di Windows dell'organizzazione che si vuole includere nel ruolo.</span><span class="sxs-lookup"><span data-stu-id="cdfff-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="cdfff-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdfff-150">What's next?</span></span>
<span data-ttu-id="cdfff-151">[Lezione 12: Analizzare in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="cdfff-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
