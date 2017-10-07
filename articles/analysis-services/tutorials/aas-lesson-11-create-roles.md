---
<span data-ttu-id="f99b2-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 11: creare ruoli | Descrizione di "Microsoft Docs: viene descritto come ruoli toocreate hello progetto tutorial Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f99b2-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="f99b2-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="f99b2-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="f99b2-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="f99b2-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="f99b2-104">Lezione 11: Creare ruoli</span><span class="sxs-lookup"><span data-stu-id="f99b2-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f99b2-105">In questa lezione verranno creati ruoli.</span><span class="sxs-lookup"><span data-stu-id="f99b2-105">In this lesson, you create roles.</span></span> <span data-ttu-id="f99b2-106">I ruoli garantiscono protezione dati e oggetti di database modello, limitando l'accesso tooonly gli utenti che sono membri del ruolo.</span><span class="sxs-lookup"><span data-stu-id="f99b2-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="f99b2-107">Ogni ruolo è definito con una sola autorizzazione: Nessuna, Lettura, Lettura ed elaborazione, Elaborazione o Amministratore.</span><span class="sxs-lookup"><span data-stu-id="f99b2-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="f99b2-108">I ruoli possono essere definiti durante la creazione dei modelli tramite Gestione ruoli.</span><span class="sxs-lookup"><span data-stu-id="f99b2-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="f99b2-109">Dopo avere distribuito un modello, è possibile gestire i ruoli con SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="f99b2-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="f99b2-110">vedere, più toolearn [ruoli](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="f99b2-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="f99b2-111">Creazione di ruoli è toocomplete non necessari in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f99b2-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="f99b2-112">Per impostazione predefinita, si è connessi con account di hello privilegi di amministratore nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="f99b2-113">Tuttavia, per altri utenti nella toobrowse organizzazione utilizzando uno strumento client, è necessario creare almeno un ruolo lettura autorizzazioni e aggiungere tali utenti come membri.</span><span class="sxs-lookup"><span data-stu-id="f99b2-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="f99b2-114">Vengono creati tre ruoli:</span><span class="sxs-lookup"><span data-stu-id="f99b2-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="f99b2-115">**Responsabile vendite** : questo ruolo può includere gli utenti dell'organizzazione per cui si desidera toohave lettura autorizzazione tooall modello a oggetti e dati.</span><span class="sxs-lookup"><span data-stu-id="f99b2-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="f99b2-116">**Sales Analyst US** : questo ruolo può includere gli utenti dell'organizzazione per cui si desidera solo i dati in grado di toobrowse toobe toosales in Italia hello correlati.</span><span class="sxs-lookup"><span data-stu-id="f99b2-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="f99b2-117">Per questo ruolo, utilizzare un toodefine formula DAX un *filtro di riga*, che limita i membri toobrowse solo i dati per hello Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="f99b2-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="f99b2-118">**Amministratore** : questo ruolo può includere gli utenti per cui si desidera toohave amministratore le autorizzazioni, che consente accesso illimitato e autorizzazioni tooperform le attività amministrative sul database modello hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="f99b2-119">Poiché gli account utente e gruppo di Windows nell'organizzazione sono univoci, è possibile aggiungere l'account da toomembers l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f99b2-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="f99b2-120">Tuttavia, per questa esercitazione, è possibile inoltre omettere i membri di hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="f99b2-121">Testare l'effetto di hello di ogni ruolo in un secondo momento nella lezione 12: analizza in Excel.</span><span class="sxs-lookup"><span data-stu-id="f99b2-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="f99b2-122">Stimato toocomplete ora questa lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="f99b2-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f99b2-123">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f99b2-123">Prerequisites</span></span>  
<span data-ttu-id="f99b2-124">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="f99b2-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f99b2-125">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 10: creare partizioni](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="f99b2-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="f99b2-126">Creare ruoli</span><span class="sxs-lookup"><span data-stu-id="f99b2-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="f99b2-127">un ruolo utente Sales Manager toocreate</span><span class="sxs-lookup"><span data-stu-id="f99b2-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="f99b2-128">In Esplora modelli tabulari fare clic con il pulsante destro del mouse su **Ruoli** > **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="f99b2-129">In Gestione ruoli fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="f99b2-130">Fare clic su nuovo ruolo hello e quindi in hello **nome** colonna, rinominare il ruolo di hello troppo**Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="f99b2-131">In hello **autorizzazioni** colonna, fare clic su elenco a discesa hello e quindi selezionare hello **lettura** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f99b2-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="f99b2-133">Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="f99b2-134">In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="f99b2-135">un ruolo utente Sales Analyst US toocreate</span><span class="sxs-lookup"><span data-stu-id="f99b2-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="f99b2-136">In Gestione ruoli fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="f99b2-137">Rinominare il ruolo di hello troppo**Sales Analyst US**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="f99b2-138">Assegnare a questo ruolo l'autorizzazione **Lettura**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="f99b2-139">Fare clic sulla scheda filtri di riga hello e quindi per hello **DimGeography** tabella solo nella colonna filtro DAX hello hello di tipo formula seguente:</span><span class="sxs-lookup"><span data-stu-id="f99b2-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="f99b2-140">Formula di filtro di riga di un valore booleano (TRUE/FALSE) tooa deve essere risolto.</span><span class="sxs-lookup"><span data-stu-id="f99b2-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="f99b2-141">Con questa formula, si specifica che solo le righe con valore Country Region Code hello "US" sono visibili toohello utente.</span><span class="sxs-lookup"><span data-stu-id="f99b2-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="f99b2-143">Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="f99b2-144">In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="f99b2-145">toocreate un ruolo utente amministratore</span><span class="sxs-lookup"><span data-stu-id="f99b2-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="f99b2-146">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="f99b2-147">Rinominare il ruolo di hello troppo**amministratore**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="f99b2-148">Assegnare a questo ruolo l'autorizzazione **Amministratore**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="f99b2-149">Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f99b2-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="f99b2-150">In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="f99b2-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="f99b2-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f99b2-151">What's next?</span></span>
<span data-ttu-id="f99b2-152">[Lezione 12: Analizzare in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="f99b2-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
