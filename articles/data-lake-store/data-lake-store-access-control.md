---
title: Panoramica del controllo di accesso in Data Lake Store | Documentazione Microsoft
description: Informazioni sul funzionamento del controllo di accesso in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="f3c90-103">Controllo di accesso in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3c90-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="f3c90-104">Azure Data Lake Store implementa un modello di controllo di accesso derivante da HDFS, che a sua volta deriva dal modello di controllo di accesso POSIX.</span><span class="sxs-lookup"><span data-stu-id="f3c90-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="f3c90-105">Questo articolo offre un riepilogo delle nozioni di base del modello di controllo di accesso per Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="f3c90-106">Per altre informazioni sul modello di controllo di accesso HDFS, vedere [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)(Guida alle autorizzazioni HDFS).</span><span class="sxs-lookup"><span data-stu-id="f3c90-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="f3c90-107">Elenchi di controllo di accesso per file e cartelle</span><span class="sxs-lookup"><span data-stu-id="f3c90-107">Access control lists on files and folders</span></span>

<span data-ttu-id="f3c90-108">Esistono due tipologie di elenchi di controllo di accesso (ACL): **ACL di accesso** e **ACL predefiniti**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="f3c90-109">**ACL di accesso**: questi elenchi controllano l'accesso a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="f3c90-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="f3c90-110">Sia i file che le cartelle hanno ACL di accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="f3c90-111">**ACL predefiniti**: "modello" di ACL associato a una cartella che determina gli ACL di accesso per tutti gli elementi figlio creati in tale cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="f3c90-112">I file non hanno ACL predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f3c90-112">Files do not have Default ACLs.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="f3c90-114">Sia gli ACL di accesso che gli ACL predefiniti presentano la stessa struttura.</span><span class="sxs-lookup"><span data-stu-id="f3c90-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="f3c90-116">La modifica dell'ACL predefinito per un elemento padre non influisce sull'ACL di accesso o sull'ACL predefinito degli elementi figlio già esistenti.</span><span class="sxs-lookup"><span data-stu-id="f3c90-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="f3c90-117">Utenti e identità</span><span class="sxs-lookup"><span data-stu-id="f3c90-117">Users and identities</span></span>

<span data-ttu-id="f3c90-118">Ogni file e cartella ha autorizzazioni distinte per le entità seguenti:</span><span class="sxs-lookup"><span data-stu-id="f3c90-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="f3c90-119">Utente proprietario del file</span><span class="sxs-lookup"><span data-stu-id="f3c90-119">The owning user of the file</span></span>
* <span data-ttu-id="f3c90-120">Gruppo proprietario</span><span class="sxs-lookup"><span data-stu-id="f3c90-120">The owning group</span></span>
* <span data-ttu-id="f3c90-121">Utenti non anonimi</span><span class="sxs-lookup"><span data-stu-id="f3c90-121">Named users</span></span>
* <span data-ttu-id="f3c90-122">Gruppi con nome</span><span class="sxs-lookup"><span data-stu-id="f3c90-122">Named groups</span></span>
* <span data-ttu-id="f3c90-123">Tutti gli altri utenti</span><span class="sxs-lookup"><span data-stu-id="f3c90-123">All other users</span></span>

<span data-ttu-id="f3c90-124">Le identità di utenti e gruppi sono identità di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3c90-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="f3c90-125">Se non viene specificato diversamente, quindi, nel contesto di Data Lake Store un "utente" può essere un utente di AD Azure o un gruppo di sicurezza di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3c90-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="f3c90-126">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="f3c90-126">Permissions</span></span>

<span data-ttu-id="f3c90-127">Le autorizzazioni per un oggetto del file system sono **Lettura**, **Scrittura** ed **Esecuzione** e possono essere usate per file e cartelle come illustrato nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="f3c90-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="f3c90-128">File</span><span class="sxs-lookup"><span data-stu-id="f3c90-128">File</span></span>     |   <span data-ttu-id="f3c90-129">Cartella</span><span class="sxs-lookup"><span data-stu-id="f3c90-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="f3c90-130">**Lettura (R)**</span><span class="sxs-lookup"><span data-stu-id="f3c90-130">**Read (R)**</span></span> | <span data-ttu-id="f3c90-131">È possibile leggere il contenuto di un file</span><span class="sxs-lookup"><span data-stu-id="f3c90-131">Can read the contents of a file</span></span> | <span data-ttu-id="f3c90-132">Per elencare il contenuto della cartella sono necessarie le autorizzazioni di **Lettura** ed **Esecuzione**</span><span class="sxs-lookup"><span data-stu-id="f3c90-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="f3c90-133">**Scrittura (W)**</span><span class="sxs-lookup"><span data-stu-id="f3c90-133">**Write (W)**</span></span> | <span data-ttu-id="f3c90-134">È possibile scrivere o aggiungere in un file</span><span class="sxs-lookup"><span data-stu-id="f3c90-134">Can write or append to a file</span></span> | <span data-ttu-id="f3c90-135">Per creare elementi figlio in una cartella sono necessarie le autorizzazioni di **Scrittura** ed **Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="f3c90-136">**Esecuzione (X)**</span><span class="sxs-lookup"><span data-stu-id="f3c90-136">**Execute (X)**</span></span> | <span data-ttu-id="f3c90-137">Nessun valore nel contesto di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3c90-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="f3c90-138">È necessaria per attraversare gli elementi figlio di una cartella</span><span class="sxs-lookup"><span data-stu-id="f3c90-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="f3c90-139">Forme brevi per le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="f3c90-139">Short forms for permissions</span></span>

<span data-ttu-id="f3c90-140">La forma **RWX** viene usata per indicare **Lettura + Scrittura + Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="f3c90-141">Esiste una forma numerica ridotta in cui **Lettura=4**, **Scrittura=2** ed **Esecuzione=1** e la cui somma rappresenta le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="f3c90-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="f3c90-142">Di seguito sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="f3c90-142">Following are some examples.</span></span>

| <span data-ttu-id="f3c90-143">Forma numerica</span><span class="sxs-lookup"><span data-stu-id="f3c90-143">Numeric form</span></span> | <span data-ttu-id="f3c90-144">Forma breve</span><span class="sxs-lookup"><span data-stu-id="f3c90-144">Short form</span></span> |      <span data-ttu-id="f3c90-145">Significato</span><span class="sxs-lookup"><span data-stu-id="f3c90-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="f3c90-146">7</span><span class="sxs-lookup"><span data-stu-id="f3c90-146">7</span></span>            | <span data-ttu-id="f3c90-147">RWX</span><span class="sxs-lookup"><span data-stu-id="f3c90-147">RWX</span></span>        | <span data-ttu-id="f3c90-148">Lettura + Scrittura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="f3c90-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="f3c90-149">5</span><span class="sxs-lookup"><span data-stu-id="f3c90-149">5</span></span>            | <span data-ttu-id="f3c90-150">R-X</span><span class="sxs-lookup"><span data-stu-id="f3c90-150">R-X</span></span>        | <span data-ttu-id="f3c90-151">Lettura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="f3c90-151">Read + Execute</span></span>         |
| <span data-ttu-id="f3c90-152">4</span><span class="sxs-lookup"><span data-stu-id="f3c90-152">4</span></span>            | <span data-ttu-id="f3c90-153">R--</span><span class="sxs-lookup"><span data-stu-id="f3c90-153">R--</span></span>        | <span data-ttu-id="f3c90-154">Lettura</span><span class="sxs-lookup"><span data-stu-id="f3c90-154">Read</span></span>                   |
| <span data-ttu-id="f3c90-155">0</span><span class="sxs-lookup"><span data-stu-id="f3c90-155">0</span></span>            | ---        | <span data-ttu-id="f3c90-156">Nessuna autorizzazione</span><span class="sxs-lookup"><span data-stu-id="f3c90-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="f3c90-157">Non ereditarietà delle autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="f3c90-157">Permissions do not inherit</span></span>

<span data-ttu-id="f3c90-158">Nel modello di tipo POSIX usato da Data Lake Store, le autorizzazioni per un elemento vengono archiviate nell'elemento stesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="f3c90-159">In altri termini, le autorizzazioni per un elemento non sono ereditabili dagli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="f3c90-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="f3c90-160">Scenari comuni correlati alle autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="f3c90-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="f3c90-161">Di seguito sono riportati alcuni scenari comuni che consentono di comprendere quali autorizzazioni sono necessarie per eseguire determinate operazioni su un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="f3c90-162">Autorizzazioni necessarie per la lettura di un file</span><span class="sxs-lookup"><span data-stu-id="f3c90-162">Permissions needed to read a file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="f3c90-164">Per il file da leggere, il chiamante deve avere autorizzazioni di **Lettura**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="f3c90-165">Per tutte le cartelle della struttura di cartelle contenenti il file, il chiamante deve avere autorizzazioni di **Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="f3c90-166">Autorizzazioni necessarie per l'aggiunta a un file</span><span class="sxs-lookup"><span data-stu-id="f3c90-166">Permissions needed to append to a file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="f3c90-168">Per il file a cui si intende eseguire l'aggiunta, il chiamante deve avere autorizzazioni di **Scrittura**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="f3c90-169">Per tutte le cartelle contenenti il file, il chiamante deve avere autorizzazioni di **Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="f3c90-170">Autorizzazioni necessarie per l'eliminazione di un file</span><span class="sxs-lookup"><span data-stu-id="f3c90-170">Permissions needed to delete a file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="f3c90-172">Per la cartella padre, il chiamante deve avere autorizzazioni di **Scrittura + Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="f3c90-173">Per tutte le altre cartelle nel percorso del file, il chiamante deve avere autorizzazioni di **Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="f3c90-174">Se vengono soddisfatte le due condizioni precedenti, non sono necessarie autorizzazioni di scrittura per il file per eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="f3c90-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="f3c90-175">Autorizzazioni necessarie per l'enumerazione di una cartella</span><span class="sxs-lookup"><span data-stu-id="f3c90-175">Permissions needed to enumerate a folder</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="f3c90-177">Per la cartella di cui si intende eseguire l'enumerazione, il chiamante deve avere autorizzazioni di **Lettura + Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="f3c90-178">Per tutte le cartelle predecessore, il chiamante deve avere autorizzazioni di **Esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="f3c90-179">Visualizzazione delle autorizzazioni nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f3c90-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="f3c90-180">Nel pannello **Esplora dati** dell'account Data Lake Store fare clic su **Accesso** per visualizzare gli ACL per un file o una cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="f3c90-181">Fare clic su **Accesso** per visualizzare gli ACL per la cartella **catalog** dell'account **mydatastore**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="f3c90-183">La sezione superiore di questo pannello mostra una panoramica delle autorizzazioni dell'utente,</span><span class="sxs-lookup"><span data-stu-id="f3c90-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="f3c90-184">che nello screenshot seguente si chiama Bob. A seguire vengono mostrate le autorizzazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="f3c90-185">Successivamente, nel pannello **Accesso** fare clic su **Visualizzazione semplice** per passare alla visualizzazione semplificata.</span><span class="sxs-lookup"><span data-stu-id="f3c90-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="f3c90-187">Fare clic su **Vista avanzata** per visualizzare la vista più avanzata, che mostra i concetti relativi ad ACL predefiniti, maschera e utente con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="f3c90-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="f3c90-189">Utente con privilegi avanzati</span><span class="sxs-lookup"><span data-stu-id="f3c90-189">The super-user</span></span>

<span data-ttu-id="f3c90-190">Un utente con privilegi avanzati ha diritti superiori rispetto a qualsiasi altro utente di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="f3c90-191">Un utente con privilegi avanzati:</span><span class="sxs-lookup"><span data-stu-id="f3c90-191">A super-user:</span></span>

* <span data-ttu-id="f3c90-192">Ha autorizzazioni RWX per **tutti** i file e le cartelle.</span><span class="sxs-lookup"><span data-stu-id="f3c90-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="f3c90-193">Può modificare le autorizzazioni per qualsiasi file o cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="f3c90-194">Può modificare l'utente o il gruppo proprietario di qualsiasi file o cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="f3c90-195">In Azure un account Data Lake Store include diversi ruoli di Azure, tra cui:</span><span class="sxs-lookup"><span data-stu-id="f3c90-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="f3c90-196">Proprietari</span><span class="sxs-lookup"><span data-stu-id="f3c90-196">Owners</span></span>
* <span data-ttu-id="f3c90-197">Collaboratori</span><span class="sxs-lookup"><span data-stu-id="f3c90-197">Contributors</span></span>
* <span data-ttu-id="f3c90-198">Lettori</span><span class="sxs-lookup"><span data-stu-id="f3c90-198">Readers</span></span>

<span data-ttu-id="f3c90-199">Tutti i membri del ruolo **Proprietari** per un account Data Lake Store sono automaticamente superuser per tale account.</span><span class="sxs-lookup"><span data-stu-id="f3c90-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="f3c90-200">Per altre informazioni, vedere l'articolo relativo al [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f3c90-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="f3c90-201">Se si vuole creare un ruolo Controllo degli accessi in base al ruolo personalizzato con autorizzazioni di utente avanzato, è necessario avere le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f3c90-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="f3c90-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="f3c90-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="f3c90-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="f3c90-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="f3c90-204">Utente proprietario</span><span class="sxs-lookup"><span data-stu-id="f3c90-204">The owning user</span></span>

<span data-ttu-id="f3c90-205">L'utente che ha creato l'elemento ne è automaticamente l'utente proprietario.</span><span class="sxs-lookup"><span data-stu-id="f3c90-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="f3c90-206">Un utente proprietario può:</span><span class="sxs-lookup"><span data-stu-id="f3c90-206">An owning user can:</span></span>

* <span data-ttu-id="f3c90-207">Modificare le autorizzazioni di un file di sua proprietà.</span><span class="sxs-lookup"><span data-stu-id="f3c90-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="f3c90-208">Modificare il gruppo proprietario di un file di sua proprietà, a condizione che l'utente proprietario sia anche membro del gruppo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f3c90-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="f3c90-209">L'utente proprietario *non può* modificare l'utente proprietario di un altro file.</span><span class="sxs-lookup"><span data-stu-id="f3c90-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="f3c90-210">Solo i superuser possono modificare l'utente proprietario di un file o una cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="f3c90-211">Gruppo proprietario</span><span class="sxs-lookup"><span data-stu-id="f3c90-211">The owning group</span></span>

<span data-ttu-id="f3c90-212">Negli ACL POSIX ogni utente è associato a un "gruppo primario".</span><span class="sxs-lookup"><span data-stu-id="f3c90-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="f3c90-213">L'utente "alice", ad esempio, può appartenere al gruppo "finanza".</span><span class="sxs-lookup"><span data-stu-id="f3c90-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="f3c90-214">Alice può anche appartenere a più gruppi, ma uno solo è sempre designato come il suo gruppo primario.</span><span class="sxs-lookup"><span data-stu-id="f3c90-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="f3c90-215">Quando Alice crea un file in POSIX, come gruppo proprietario del file viene impostato il gruppo primario di Alice, in questo caso "finanza".</span><span class="sxs-lookup"><span data-stu-id="f3c90-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="f3c90-216">Quando viene creato un nuovo elemento del file system, Data Lake Store assegna un valore al gruppo proprietario.</span><span class="sxs-lookup"><span data-stu-id="f3c90-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="f3c90-217">**Caso 1**: cartella radice "/".</span><span class="sxs-lookup"><span data-stu-id="f3c90-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="f3c90-218">Questa cartella viene creata al momento della creazione di un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="f3c90-219">In questo caso il gruppo proprietario viene impostato sull'utente che ha creato l'account.</span><span class="sxs-lookup"><span data-stu-id="f3c90-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="f3c90-220">**Caso 2**: tutti gli altri casi. Quando viene creato un nuovo elemento, il gruppo proprietario viene copiato dalla cartella padre.</span><span class="sxs-lookup"><span data-stu-id="f3c90-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="f3c90-221">Il gruppo proprietario può essere modificato da:</span><span class="sxs-lookup"><span data-stu-id="f3c90-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="f3c90-222">Qualsiasi utente con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="f3c90-222">Any super-users.</span></span>
* <span data-ttu-id="f3c90-223">Utente proprietario, se è anche membro del gruppo di destinazione</span><span class="sxs-lookup"><span data-stu-id="f3c90-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="f3c90-224">Algoritmo di controllo dell'accesso</span><span class="sxs-lookup"><span data-stu-id="f3c90-224">Access check algorithm</span></span>

<span data-ttu-id="f3c90-225">La figura seguente rappresenta l'algoritmo di controllo dell'accesso per gli account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Algoritmo per gli ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="f3c90-227">Proprietà mask e "autorizzazioni valide"</span><span class="sxs-lookup"><span data-stu-id="f3c90-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="f3c90-228">La **maschera** è un valore RWX usato per limitare l'accesso per **utenti non anonimi**, **gruppo proprietario** e **gruppi con nome** durante l'esecuzione dell'algoritmo di controllo dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="f3c90-229">Di seguito sono descritti i concetti chiave relativi a mask.</span><span class="sxs-lookup"><span data-stu-id="f3c90-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="f3c90-230">La maschera crea autorizzazioni valide.</span><span class="sxs-lookup"><span data-stu-id="f3c90-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="f3c90-231">Vale a dire che modifica le autorizzazioni al momento del controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="f3c90-232">La maschera può essere modificata direttamente dal proprietario del file e da qualsiasi utente con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="f3c90-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="f3c90-233">La maschera può rimuovere autorizzazioni per creare l'autorizzazione valida,</span><span class="sxs-lookup"><span data-stu-id="f3c90-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="f3c90-234">ma *non può* aggiungere autorizzazioni all'autorizzazione valida.</span><span class="sxs-lookup"><span data-stu-id="f3c90-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="f3c90-235">Verranno ora esaminati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="f3c90-235">Let's look at some examples.</span></span> <span data-ttu-id="f3c90-236">Nell'esempio seguente la maschera è impostata su **RWX** e non rimuove quindi alcuna autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f3c90-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="f3c90-237">Le autorizzazioni valide per l'utente non anonimo, il gruppo proprietario e il gruppo con nome non vengono modificate durante il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="f3c90-239">Nell'esempio seguente la maschera è impostata su **R-X**.</span><span class="sxs-lookup"><span data-stu-id="f3c90-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="f3c90-240">Ciò significa che **disabilita l'autorizzazione di scrittura** per l'**utente non anonimo**, il **gruppo proprietario** e il **gruppo con nome** al momento del controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="f3c90-242">Per riferimento, di seguito è illustrata la visualizzazione nel portale di Azure della maschera per un file o una cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="f3c90-244">Per un nuovo account Data Lake Store, l'impostazione predefinita della maschera per l'ACL di accesso e l'ACL predefinito della cartella radice ("/") è RWX.</span><span class="sxs-lookup"><span data-stu-id="f3c90-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="f3c90-245">Autorizzazioni per nuovi file e cartelle</span><span class="sxs-lookup"><span data-stu-id="f3c90-245">Permissions on new files and folders</span></span>

<span data-ttu-id="f3c90-246">Quando si crea un nuovo file o una nuova cartella in una cartella esistente, l'ACL predefinito per la cartella padre determina quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f3c90-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="f3c90-247">ACL predefinito e ACL di accesso di una cartella figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="f3c90-248">ACL di accesso di un file figlio (i file non hanno un ACL predefinito).</span><span class="sxs-lookup"><span data-stu-id="f3c90-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="f3c90-249">ACL di accesso di una cartella o un file figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="f3c90-250">Quando si crea una cartella o un file figlio, l'ACL predefinito dell'elemento padre viene copiato come ACL di accesso della cartella o del file figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="f3c90-251">Se **altri** utenti hanno autorizzazioni RWX nell'ACL predefinito dell'elemento padre, vengono rimosse dall'ACL di accesso dell'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="f3c90-253">Nella maggior parte degli scenari le informazioni sopra riportate sono sufficienti a illustrare il modo in cui viene determinato l'ACL di accesso di un elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="f3c90-254">Se si ha familiarità con i sistemi POSIX e si vuole comprendere in modo approfondito come viene ottenuta questa trasformazione, vedere la sezione [Ruolo di umask nella creazione dell'ACL di accesso per nuovi file e cartelle](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f3c90-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="f3c90-255">ACL predefinito di una cartella figlio</span><span class="sxs-lookup"><span data-stu-id="f3c90-255">A child folder's Default ACL</span></span>

<span data-ttu-id="f3c90-256">Quando viene creata una cartella figlio in una cartella padre, l'ACL predefinito della cartella padre viene copiato, così com'è, nell'ACL predefinito della cartella figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="f3c90-258">Argomenti avanzati per informazioni dettagliate sugli ACL in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3c90-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="f3c90-259">Di seguito sono riportati alcuni argomenti avanzati utili per comprendere il modo in cui vengono determinati gli ACL per i file e le cartelle di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="f3c90-260">Ruolo di umask nella creazione dell'ACL di accesso per nuovi file e cartelle</span><span class="sxs-lookup"><span data-stu-id="f3c90-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="f3c90-261">In un sistema compatibile con POSIX, il concetto generale è che umask è un valore a 9 bit relativo alla cartella padre che viene usato per trasformare l'autorizzazione per l'**utente proprietario**, il **gruppo proprietario** e gli **altri** utenti nell'ACL di accesso di una nuova cartella o un nuovo file figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="f3c90-262">I bit di umask identificano i bit da disattivare nell'ACL di accesso dell'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="f3c90-263">L'opzione umask viene così usata per impedire in modo selettivo la propagazione delle autorizzazioni per l'**utente proprietario**, il **gruppo proprietario** e gli **altri** utenti.</span><span class="sxs-lookup"><span data-stu-id="f3c90-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="f3c90-264">In un sistema HDFS umask è in genere un'opzione di configurazione a livello di sito controllata dagli amministratori.</span><span class="sxs-lookup"><span data-stu-id="f3c90-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="f3c90-265">Data Lake Store usa una proprietà **umask a livello di account** non modificabile.</span><span class="sxs-lookup"><span data-stu-id="f3c90-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="f3c90-266">La tabella seguente illustra l'opzione umask per Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="f3c90-267">Gruppo utenti</span><span class="sxs-lookup"><span data-stu-id="f3c90-267">User group</span></span>  | <span data-ttu-id="f3c90-268">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f3c90-268">Setting</span></span> | <span data-ttu-id="f3c90-269">Effetto sull'ACL di accesso di un nuovo elemento figlio</span><span class="sxs-lookup"><span data-stu-id="f3c90-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="f3c90-270">utente proprietario</span><span class="sxs-lookup"><span data-stu-id="f3c90-270">Owning user</span></span> | ---     | <span data-ttu-id="f3c90-271">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="f3c90-271">No effect</span></span>                             |
| <span data-ttu-id="f3c90-272">gruppo proprietario</span><span class="sxs-lookup"><span data-stu-id="f3c90-272">Owning group</span></span>| ---     | <span data-ttu-id="f3c90-273">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="f3c90-273">No effect</span></span>                             |
| <span data-ttu-id="f3c90-274">altri</span><span class="sxs-lookup"><span data-stu-id="f3c90-274">Other</span></span>       | <span data-ttu-id="f3c90-275">RWX</span><span class="sxs-lookup"><span data-stu-id="f3c90-275">RWX</span></span>     | <span data-ttu-id="f3c90-276">Rimuovere Lettura + Scrittura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="f3c90-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="f3c90-277">La figura seguente illustra il funzionamento di questa proprietà umask.</span><span class="sxs-lookup"><span data-stu-id="f3c90-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="f3c90-278">L'effetto in definitiva è la rimozione dell'autorizzazione **Lettura + Scrittura + Esecuzione** per gli **altri** utenti.</span><span class="sxs-lookup"><span data-stu-id="f3c90-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="f3c90-279">Dato che in umask non sono specificati bit per l'**utente proprietario** e il **gruppo proprietario**, tali autorizzazioni non vengono trasformate.</span><span class="sxs-lookup"><span data-stu-id="f3c90-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="f3c90-281">Sticky bit</span><span class="sxs-lookup"><span data-stu-id="f3c90-281">The sticky bit</span></span>

<span data-ttu-id="f3c90-282">Lo sticky bit è una funzionalità più avanzata di un file system POSIX.</span><span class="sxs-lookup"><span data-stu-id="f3c90-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="f3c90-283">Nel contesto di Data Lake Store, è improbabile che lo sticky bit sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f3c90-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="f3c90-284">La tabella seguente descrive il funzionamento dello sticky bit in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="f3c90-285">Gruppo utenti</span><span class="sxs-lookup"><span data-stu-id="f3c90-285">User group</span></span>         | <span data-ttu-id="f3c90-286">File</span><span class="sxs-lookup"><span data-stu-id="f3c90-286">File</span></span>    | <span data-ttu-id="f3c90-287">Cartella</span><span class="sxs-lookup"><span data-stu-id="f3c90-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="f3c90-288">Sticky bit **OFF**</span><span class="sxs-lookup"><span data-stu-id="f3c90-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="f3c90-289">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="f3c90-289">No effect</span></span>   | <span data-ttu-id="f3c90-290">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="f3c90-290">No effect.</span></span>           |
| <span data-ttu-id="f3c90-291">Sticky bit **ON**</span><span class="sxs-lookup"><span data-stu-id="f3c90-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="f3c90-292">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="f3c90-292">No effect</span></span>   | <span data-ttu-id="f3c90-293">Impedisce a chiunque tranne agli **utenti con privilegi avanzati** e all'**utente proprietario** di un elemento figlio di eliminare o rinominare l'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="f3c90-294">Lo sticky bit non viene visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3c90-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="f3c90-295">Domande frequenti sugli ACL in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3c90-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="f3c90-296">Di seguito sono riportate alcune domande frequenti sugli ACL in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="f3c90-297">È necessario abilitare il supporto per gli ACL?</span><span class="sxs-lookup"><span data-stu-id="f3c90-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="f3c90-298">No.</span><span class="sxs-lookup"><span data-stu-id="f3c90-298">No.</span></span> <span data-ttu-id="f3c90-299">Il controllo di accesso tramite ACL è sempre attivo per un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="f3c90-300">Quali autorizzazioni sono necessarie per eliminare in modo ricorsivo una cartella e il relativo contenuto?</span><span class="sxs-lookup"><span data-stu-id="f3c90-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="f3c90-301">Sono necessarie autorizzazioni di **Scrittura + Esecuzione** per la cartella padre.</span><span class="sxs-lookup"><span data-stu-id="f3c90-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="f3c90-302">Sono necessarie autorizzazioni di **Lettura + Scrittura + Esecuzione** per la cartella da eliminare e per ogni cartella al suo interno.</span><span class="sxs-lookup"><span data-stu-id="f3c90-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="f3c90-303">Non sono necessarie autorizzazioni di Scrittura per eliminare i file nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="f3c90-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="f3c90-304">La cartella radice "/" non può **mai** essere eliminata.</span><span class="sxs-lookup"><span data-stu-id="f3c90-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="f3c90-305">Chi è il proprietario di un file o una cartella?</span><span class="sxs-lookup"><span data-stu-id="f3c90-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="f3c90-306">Il creatore di un file o una cartella ne diventa il proprietario.</span><span class="sxs-lookup"><span data-stu-id="f3c90-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="f3c90-307">Quale gruppo viene impostato come gruppo proprietario di un file o una cartella al momento della creazione?</span><span class="sxs-lookup"><span data-stu-id="f3c90-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="f3c90-308">Il gruppo proprietario viene copiato da quello della cartella padre in cui si crea il nuovo file o la nuova cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="f3c90-309">Se l'utente proprietario di un file non ha le autorizzazioni RWX di cui ha bisogno,</span><span class="sxs-lookup"><span data-stu-id="f3c90-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="f3c90-310">che cosa occorre fare?</span><span class="sxs-lookup"><span data-stu-id="f3c90-310">What do I do?</span></span>

<span data-ttu-id="f3c90-311">L'utente proprietario può modificare le autorizzazioni del file in modo da assegnarsi tutte le autorizzazioni RWX necessarie.</span><span class="sxs-lookup"><span data-stu-id="f3c90-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="f3c90-312">La visualizzazione degli ACL nel portale di Azure mostra i nomi utente, mentre tramite le API vengono visualizzati i GUID. Per quale motivo?</span><span class="sxs-lookup"><span data-stu-id="f3c90-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="f3c90-313">Le voci negli ACL vengono archiviate come GUID che corrispondono agli utenti in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3c90-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="f3c90-314">Le API restituiscono i GUID così come sono.</span><span class="sxs-lookup"><span data-stu-id="f3c90-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="f3c90-315">Il portale di Azure tenta di semplificare l'uso degli ACL traducendo i GUID in nomi descrittivi, quando è possibile.</span><span class="sxs-lookup"><span data-stu-id="f3c90-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="f3c90-316">Perché a volte negli ACL vengono visualizzati i GUID quando si usa il portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="f3c90-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="f3c90-317">Il GUID viene visualizzato quando l'utente non esiste più in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3c90-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="f3c90-318">In genere ciò si verifica se l'utente non fa più parte dell'azienda o l'account è stato eliminato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3c90-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="f3c90-319">Data Lake Store supporta l'ereditarietà degli ACL?</span><span class="sxs-lookup"><span data-stu-id="f3c90-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="f3c90-320">No.</span><span class="sxs-lookup"><span data-stu-id="f3c90-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="f3c90-321">Qual è la differenza tra mask e umask?</span><span class="sxs-lookup"><span data-stu-id="f3c90-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="f3c90-322">mask</span><span class="sxs-lookup"><span data-stu-id="f3c90-322">mask</span></span> | <span data-ttu-id="f3c90-323">umask</span><span class="sxs-lookup"><span data-stu-id="f3c90-323">umask</span></span>|
|------|------|
| <span data-ttu-id="f3c90-324">La proprietà **mask** è disponibile per ogni file e cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="f3c90-325">**umask** è una proprietà dell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3c90-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="f3c90-326">Di conseguenza, in Data Lake Store esiste un unico valore umask.</span><span class="sxs-lookup"><span data-stu-id="f3c90-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="f3c90-327">La proprietà mask per un file o una cartella può essere modificata dall'utente proprietario, dal gruppo proprietario di un file o da un superuser.</span><span class="sxs-lookup"><span data-stu-id="f3c90-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="f3c90-328">La proprietà umask non può essere modificata da alcun utente, inclusi gli utenti con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="f3c90-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="f3c90-329">È un valore costante non modificabile.</span><span class="sxs-lookup"><span data-stu-id="f3c90-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="f3c90-330">La proprietà mask viene usata durante l'algoritmo di controllo dell'accesso in fase di esecuzione per determinare se un utente ha il diritto di eseguire un'operazione su un file o una cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="f3c90-331">Il ruolo di mask è creare "autorizzazioni valide" al momento del controllo dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="f3c90-332">L'opzione umask non viene usata durante il controllo dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="f3c90-333">Viene usata per determinare l'ACL di accesso dei nuovi elementi figlio di una cartella.</span><span class="sxs-lookup"><span data-stu-id="f3c90-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="f3c90-334">La proprietà mask è un valore RWX a 3 bit applicato a un utente non anonimo, a un gruppo con nome e all'utente proprietario al momento del controllo dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="f3c90-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="f3c90-335">Umask è un valore a 9 bit applicato all'utente proprietario, al gruppo proprietario e agli **altri** utenti di un nuovo elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="f3c90-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="f3c90-336">Dove è possibile reperire altre informazioni sul modello di controllo di accesso POSIX?</span><span class="sxs-lookup"><span data-stu-id="f3c90-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="f3c90-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Elenchi di controllo di accesso POSIX in Linux)</span><span class="sxs-lookup"><span data-stu-id="f3c90-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="f3c90-338">[HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Guida alle autorizzazioni HDFS)</span><span class="sxs-lookup"><span data-stu-id="f3c90-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="f3c90-339">Domande frequenti su POSIX</span><span class="sxs-lookup"><span data-stu-id="f3c90-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="f3c90-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="f3c90-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="f3c90-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="f3c90-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="f3c90-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="f3c90-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="f3c90-343">ACL POSIX in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f3c90-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* <span data-ttu-id="f3c90-344">[ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: uso di elenchi di controllo di accesso in Linux)</span><span class="sxs-lookup"><span data-stu-id="f3c90-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="f3c90-345">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f3c90-345">See also</span></span>

* [<span data-ttu-id="f3c90-346">Panoramica dell’Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="f3c90-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
