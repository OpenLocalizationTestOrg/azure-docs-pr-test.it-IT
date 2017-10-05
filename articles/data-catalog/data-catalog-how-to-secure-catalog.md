---
title: Come proteggere l'accesso ad Azure Data Catalog | Microsoft Docs
description: Questo articolo descrive come proteggere il catalogo dati e gli asset corrispondenti.
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
ms.openlocfilehash: 9664a7bc8493b08c8e0797ac6f1b212079829833
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="ee9aa-103">Come proteggere l'accesso al catalogo dati e agli asset di dati</span><span class="sxs-lookup"><span data-stu-id="ee9aa-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee9aa-104">Questa funzionalità è disponibile solo nell'edizione Standard di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="ee9aa-105">Azure Data Catalog consente di specificare chi può accedere al catalogo dati e quali operazioni può eseguire sui metadati del catalogo (registrazione, annotazione, assunzione della proprietà del catalogo).</span><span class="sxs-lookup"><span data-stu-id="ee9aa-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="ee9aa-106">Utenti e autorizzazioni del catalogo</span><span class="sxs-lookup"><span data-stu-id="ee9aa-106">Catalog users and permissions</span></span>
<span data-ttu-id="ee9aa-107">Per assegnare a un utente o un gruppo l'accesso a un catalogo dati e impostare le autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="ee9aa-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="ee9aa-108">Nella [home page del catalogo dati](http://www.azuredatacatalog.com) fare clic su **Impostazioni** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![Catalogo dati - Impostazioni](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="ee9aa-110">Nella pagina delle impostazioni espandere la sezione **Utenti del catalogo**.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="ee9aa-111">![Utenti del catalogo - Aggiungi](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="ee9aa-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="ee9aa-112">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-112">Click **Add**.</span></span>
4. <span data-ttu-id="ee9aa-113">Immettere il **nome utente** completo o il nome del **gruppo di sicurezza** di Azure Active Directory (AAD) associato al catalogo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="ee9aa-114">Se si aggiungono più utenti o gruppi usare la virgola (',') come separatore.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="ee9aa-115">![Utenti del catalogo - Utenti o gruppi](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="ee9aa-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="ee9aa-116">Premere **INVIO** o **TAB** per uscire dalla casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="ee9aa-117">Verificare che tutte le autorizzazioni (**Annota**, **Registra** e **Diventa proprietario**) siano assegnate per impostazione predefinita a tali utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="ee9aa-118">In tal modo l'utente o il gruppo potrà [registrare asset di dati]( data-catalog-how-to-register.md), [annotare asset di dati]( data-catalog-how-to-annotate.md) e [diventare proprietario di asset di dati]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="ee9aa-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="ee9aa-119">![Utenti del catalogo - Autorizzazioni predefinite](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="ee9aa-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="ee9aa-120">Per assegnare a un utente o un gruppo solo l'accesso in lettura al catalogo, disattivare l'opzione **Annota** per l'utente o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="ee9aa-121">In questo modo l'utente o il gruppo non può aggiungere annotazioni agli asset di dati del catalogo, ma può visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="ee9aa-122">Per impedire a un utente o un gruppo di registrare asset di dati, disattivare l'opzione **Registra** per l'utente o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="ee9aa-123">Per impedire a un utente o un gruppo di diventare proprietario di un asset di dati, disattivare l'opzione **Diventa proprietario** per l'utente o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="ee9aa-124">Per eliminare un utente o un gruppo dagli utenti del catalogo, fare clic su **x** in corrispondenza dell'utente o del gruppo nella parte inferiore dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="ee9aa-125">![Utenti del catalogo - Elimina utente](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="ee9aa-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ee9aa-126">È consigliabile aggiungere gruppi di sicurezza come utenti del catalogo, anziché aggiungere direttamente singoli utenti e assegnare loro le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="ee9aa-127">Aggiungere quindi a ogni gruppo di sicurezza gli utenti che corrispondono ai ruoli e ai diritti di accesso al catalogo del gruppo.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="ee9aa-128">Considerazioni speciali</span><span class="sxs-lookup"><span data-stu-id="ee9aa-128">Special considerations</span></span>

- <span data-ttu-id="ee9aa-129">Le autorizzazioni assegnate ai gruppi di sicurezza sono cumulative.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="ee9aa-130">Si supponga ad esempio che un utente appartenga a due gruppi.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-130">Say, a user is in two groups.</span></span> <span data-ttu-id="ee9aa-131">Un gruppo ha l'autorizzazione di annotazione e l'altro gruppo non ha tale autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="ee9aa-132">L'utente avrà dell'autorizzazione di annotazione.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="ee9aa-133">Le autorizzazioni assegnate in modo esplicito a un utente eseguono l'override delle autorizzazioni assegnate ai gruppi a cui appartiene l'utente.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="ee9aa-134">Nell'esempio precedente, si supponga di aver aggiunto in modo esplicito l'utente agli utenti del catalogo e di non aver assegnato a tale utente l'autorizzazione di annotazione.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="ee9aa-135">L'utente non può aggiungere annotazioni agli asset di dati, anche se è membro di un gruppo che dispone dell'autorizzazione di annotazione.</span><span class="sxs-lookup"><span data-stu-id="ee9aa-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee9aa-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee9aa-136">Next steps</span></span>
- [<span data-ttu-id="ee9aa-137">Introduzione ad Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="ee9aa-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

