---
title: aaaHow toosecure accesso tooAzure catalogo dati | Documenti Microsoft
description: In questo articolo viene illustrato come toosecure catalogo dati e i dati aziendali.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="be8a9-103">Modalità di accesso di asset di dati e di catalogo toodata toosecure</span><span class="sxs-lookup"><span data-stu-id="be8a9-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="be8a9-104">Questa funzionalità è disponibile solo nell'edizione standard di hello di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="be8a9-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="be8a9-105">Azure Data Catalog consente toospecify chi può accedere al catalogo dati hello e quali operazioni (registrare, annotare, diventare proprietario) possono eseguire sui metadati nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="be8a9-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="be8a9-106">Utenti e autorizzazioni del catalogo</span><span class="sxs-lookup"><span data-stu-id="be8a9-106">Catalog users and permissions</span></span>
<span data-ttu-id="be8a9-107">toogive un utente o un hello gruppo accedere catalogo dati tooa e impostare le autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="be8a9-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="be8a9-108">In hello [home page del catalogo dati](http://www.azuredatacatalog.com), fare clic su **impostazioni** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="be8a9-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![Catalogo dati - Impostazioni](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="be8a9-110">Nella pagina delle impostazioni di hello, espandere hello **utenti catalogo** sezione.</span><span class="sxs-lookup"><span data-stu-id="be8a9-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="be8a9-111">![Utenti del catalogo - Aggiungi](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="be8a9-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="be8a9-112">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="be8a9-112">Click **Add**.</span></span>
4. <span data-ttu-id="be8a9-113">Immettere hello completo **nome utente** o nome di hello **gruppo di sicurezza** in Azure Active Directory (AAD) associata a catalogo hello hello.</span><span class="sxs-lookup"><span data-stu-id="be8a9-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="be8a9-114">Se si aggiungono più utenti o gruppi usare la virgola (',') come separatore.</span><span class="sxs-lookup"><span data-stu-id="be8a9-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="be8a9-115">![Utenti del catalogo - Utenti o gruppi](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="be8a9-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="be8a9-116">Premere **invio** o **scheda** dalla casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="be8a9-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="be8a9-117">Verificare che tutte le autorizzazioni (**Annota**, **registrare**, e **Take Ownership**) assegnati toothese utenti o gruppi per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="be8a9-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="be8a9-118">Vale a dire hello utente o gruppo può [registrare asset di dati]( data-catalog-how-to-register.md), [annotare asset di dati]( data-catalog-how-to-annotate.md), e [diventare proprietario dell'asset di dati]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="be8a9-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="be8a9-119">![Utenti del catalogo - Autorizzazioni predefinite](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="be8a9-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="be8a9-120">toogive un utente o gruppo solo hello leggere catalogo toohello di accesso, cancellare hello **annotare** opzione per l'utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="be8a9-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="be8a9-121">Quando si esegue questa operazione, hello utente o gruppo non è possibile annotare asset di dati nel catalogo di hello ma possono visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="be8a9-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="be8a9-122">toodeny un utente o gruppo tramite la registrazione di asset di dati, cancellare hello **registrare** opzione per l'utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="be8a9-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="be8a9-123">un utente di assunzione di proprietà di un asset di dati crittografato hello toodeny **assumere la proprietà** opzione per l'utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="be8a9-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="be8a9-124">Fare clic su un utente/gruppo di utenti del catalogo, toodelete **x** per hello utente/gruppo nella parte inferiore di hello dell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="be8a9-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="be8a9-125">![Utenti del catalogo - Elimina utente](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="be8a9-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="be8a9-126">Si consiglia di aggiungere direttamente utenti toocatalog gruppi di sicurezza anziché l'aggiunta di utenti e assegnare le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="be8a9-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="be8a9-127">Quindi, aggiungere gruppi di sicurezza toohello gli utenti che corrispondono ai loro catalogo toohello diritti di accesso e i relativi ruoli.</span><span class="sxs-lookup"><span data-stu-id="be8a9-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="be8a9-128">Considerazioni speciali</span><span class="sxs-lookup"><span data-stu-id="be8a9-128">Special considerations</span></span>

- <span data-ttu-id="be8a9-129">le autorizzazioni di Hello assegnate toosecurity gruppi sono additive.</span><span class="sxs-lookup"><span data-stu-id="be8a9-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="be8a9-130">Si supponga ad esempio che un utente appartenga a due gruppi.</span><span class="sxs-lookup"><span data-stu-id="be8a9-130">Say, a user is in two groups.</span></span> <span data-ttu-id="be8a9-131">Un gruppo ha l'autorizzazione di annotazione e l'altro gruppo non ha tale autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="be8a9-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="be8a9-132">L'utente avrà dell'autorizzazione di annotazione.</span><span class="sxs-lookup"><span data-stu-id="be8a9-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="be8a9-133">assegnare le autorizzazioni di Hello in modo esplicito hello di override utente tooa le autorizzazioni assegnate toogroups toowhich hello utente appartiene.</span><span class="sxs-lookup"><span data-stu-id="be8a9-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="be8a9-134">Nell'esempio precedente hello, ad esempio, aggiunte in modo esplicito gli utenti di toocatalog utente hello e non si assegnano autorizzazioni annotare.</span><span class="sxs-lookup"><span data-stu-id="be8a9-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="be8a9-135">utente Hello non è possibile annotare asset di dati, anche se l'utente di hello è un membro di un gruppo che dispone di annotare le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="be8a9-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be8a9-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be8a9-136">Next steps</span></span>
- [<span data-ttu-id="be8a9-137">Introduzione ad Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="be8a9-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

