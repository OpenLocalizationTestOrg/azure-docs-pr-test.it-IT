---
title: aaaOverview di controllo di accesso in archivio Data Lake | Documenti Microsoft
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
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="a00c9-103">Controllo di accesso in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a00c9-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="a00c9-104">Archivio Azure Data Lake implementa un modello di controllo di accesso che deriva da HDFS, che a sua volta deriva dal modello di controllo degli accessi di hello POSIX.</span><span class="sxs-lookup"><span data-stu-id="a00c9-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="a00c9-105">Questo articolo riepiloga le nozioni di base di hello del modello di controllo di accesso di hello per archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="a00c9-106">toolearn più sul modello di controllo degli accessi HDFS hello, vedere [HDFS autorizzazioni Guida](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="a00c9-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="a00c9-107">Elenchi di controllo di accesso per file e cartelle</span><span class="sxs-lookup"><span data-stu-id="a00c9-107">Access control lists on files and folders</span></span>

<span data-ttu-id="a00c9-108">Esistono due tipologie di elenchi di controllo di accesso (ACL): **ACL di accesso** e **ACL predefiniti**.</span><span class="sxs-lookup"><span data-stu-id="a00c9-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="a00c9-109">**Accesso ACL**: questi oggetti tooan di controllo accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="a00c9-110">Sia i file che le cartelle hanno ACL di accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="a00c9-111">**Gli ACL predefinito**: "Modello" degli ACL associato a una cartella che determinano hello accesso ACL per gli oggetti figlio che vengono creati in tale cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="a00c9-112">I file non hanno ACL predefiniti.</span><span class="sxs-lookup"><span data-stu-id="a00c9-112">Files do not have Default ACLs.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="a00c9-114">Sia gli ACL di accesso e gli ACL predefinito hanno hello stessa struttura.</span><span class="sxs-lookup"><span data-stu-id="a00c9-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="a00c9-116">Modifica hello ACL predefinito per un elemento padre non influisce sul hello accesso o ACL predefinito degli elementi figlio che esistono già.</span><span class="sxs-lookup"><span data-stu-id="a00c9-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="a00c9-117">Utenti e identità</span><span class="sxs-lookup"><span data-stu-id="a00c9-117">Users and identities</span></span>

<span data-ttu-id="a00c9-118">Ogni file e cartella ha autorizzazioni distinte per le entità seguenti:</span><span class="sxs-lookup"><span data-stu-id="a00c9-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="a00c9-119">utente del file hello proprietario Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-119">hello owning user of hello file</span></span>
* <span data-ttu-id="a00c9-120">gruppo proprietario Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-120">hello owning group</span></span>
* <span data-ttu-id="a00c9-121">Utenti non anonimi</span><span class="sxs-lookup"><span data-stu-id="a00c9-121">Named users</span></span>
* <span data-ttu-id="a00c9-122">Gruppi con nome</span><span class="sxs-lookup"><span data-stu-id="a00c9-122">Named groups</span></span>
* <span data-ttu-id="a00c9-123">Tutti gli altri utenti</span><span class="sxs-lookup"><span data-stu-id="a00c9-123">All other users</span></span>

<span data-ttu-id="a00c9-124">identità di Hello di utenti e gruppi sono le identità di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a00c9-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="a00c9-125">Se non specificato diversamente, un "user", nel contesto di hello dell'archivio Data Lake, è possibile uno: un utente di Azure Active Directory o un gruppo di sicurezza di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a00c9-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="a00c9-126">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a00c9-126">Permissions</span></span>

<span data-ttu-id="a00c9-127">le autorizzazioni di Hello su un oggetto file System sono **lettura**, **scrivere**, e **Execute**, e possono essere usati nei file e cartelle come illustrato nella seguente tabella hello:</span><span class="sxs-lookup"><span data-stu-id="a00c9-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="a00c9-128">File</span><span class="sxs-lookup"><span data-stu-id="a00c9-128">File</span></span>     |   <span data-ttu-id="a00c9-129">Cartella</span><span class="sxs-lookup"><span data-stu-id="a00c9-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="a00c9-130">**Lettura (R)**</span><span class="sxs-lookup"><span data-stu-id="a00c9-130">**Read (R)**</span></span> | <span data-ttu-id="a00c9-131">Grado di leggere il contenuto di hello di un file</span><span class="sxs-lookup"><span data-stu-id="a00c9-131">Can read hello contents of a file</span></span> | <span data-ttu-id="a00c9-132">Richiede **lettura** e **Execute** contenuto hello toolist della cartella hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="a00c9-133">**Scrittura (W)**</span><span class="sxs-lookup"><span data-stu-id="a00c9-133">**Write (W)**</span></span> | <span data-ttu-id="a00c9-134">Scrivere o aggiungere file tooa</span><span class="sxs-lookup"><span data-stu-id="a00c9-134">Can write or append tooa file</span></span> | <span data-ttu-id="a00c9-135">Richiede **scrivere** e **Execute** toocreate di elementi figlio in una cartella</span><span class="sxs-lookup"><span data-stu-id="a00c9-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="a00c9-136">**Esecuzione (X)**</span><span class="sxs-lookup"><span data-stu-id="a00c9-136">**Execute (X)**</span></span> | <span data-ttu-id="a00c9-137">Non significa che qualsiasi elemento nel contesto di hello dell'archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="a00c9-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="a00c9-138">Elementi figlio di hello tootraverse obbligatorio di una cartella</span><span class="sxs-lookup"><span data-stu-id="a00c9-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="a00c9-139">Forme brevi per le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a00c9-139">Short forms for permissions</span></span>

<span data-ttu-id="a00c9-140">**RWX** è usato tooindicate **lettura + scrivere ed eseguire**.</span><span class="sxs-lookup"><span data-stu-id="a00c9-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="a00c9-141">In cui è presente un formato numerico più ridotto **lettura = 4**, **scrivere = 2**, e **Execute = 1**, hello somma che rappresenta le autorizzazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="a00c9-142">Di seguito sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="a00c9-142">Following are some examples.</span></span>

| <span data-ttu-id="a00c9-143">Forma numerica</span><span class="sxs-lookup"><span data-stu-id="a00c9-143">Numeric form</span></span> | <span data-ttu-id="a00c9-144">Forma breve</span><span class="sxs-lookup"><span data-stu-id="a00c9-144">Short form</span></span> |      <span data-ttu-id="a00c9-145">Significato</span><span class="sxs-lookup"><span data-stu-id="a00c9-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="a00c9-146">7</span><span class="sxs-lookup"><span data-stu-id="a00c9-146">7</span></span>            | <span data-ttu-id="a00c9-147">RWX</span><span class="sxs-lookup"><span data-stu-id="a00c9-147">RWX</span></span>        | <span data-ttu-id="a00c9-148">Lettura + Scrittura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="a00c9-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="a00c9-149">5</span><span class="sxs-lookup"><span data-stu-id="a00c9-149">5</span></span>            | <span data-ttu-id="a00c9-150">R-X</span><span class="sxs-lookup"><span data-stu-id="a00c9-150">R-X</span></span>        | <span data-ttu-id="a00c9-151">Lettura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="a00c9-151">Read + Execute</span></span>         |
| <span data-ttu-id="a00c9-152">4</span><span class="sxs-lookup"><span data-stu-id="a00c9-152">4</span></span>            | <span data-ttu-id="a00c9-153">R--</span><span class="sxs-lookup"><span data-stu-id="a00c9-153">R--</span></span>        | <span data-ttu-id="a00c9-154">Lettura</span><span class="sxs-lookup"><span data-stu-id="a00c9-154">Read</span></span>                   |
| <span data-ttu-id="a00c9-155">0</span><span class="sxs-lookup"><span data-stu-id="a00c9-155">0</span></span>            | ---        | <span data-ttu-id="a00c9-156">Nessuna autorizzazione</span><span class="sxs-lookup"><span data-stu-id="a00c9-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="a00c9-157">Non ereditarietà delle autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a00c9-157">Permissions do not inherit</span></span>

<span data-ttu-id="a00c9-158">Nel modello di tipo POSIX hello utilizzato dall'archivio Data Lake, autorizzazioni per un elemento vengono archiviate in elemento hello stesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="a00c9-159">In altre parole, le autorizzazioni per un elemento non possono essere ereditate dagli elementi padre hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="a00c9-160">Toopermissions correlati a scenari comuni</span><span class="sxs-lookup"><span data-stu-id="a00c9-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="a00c9-161">Di seguito sono alcune toohelp scenari comuni comprendere quali autorizzazioni sono necessarie tooperform determinate operazioni in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="a00c9-162">Autorizzazioni necessarie tooread un file</span><span class="sxs-lookup"><span data-stu-id="a00c9-162">Permissions needed tooread a file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="a00c9-164">Per leggere toobe di file di hello, hello chiamante esigenze **lettura** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="a00c9-165">Per tutti hello cartelle nella struttura di cartelle hello che contengono file hello, hello chiamante esigenze **Execute** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="a00c9-166">Autorizzazioni necessarie tooappend tooa file</span><span class="sxs-lookup"><span data-stu-id="a00c9-166">Permissions needed tooappend tooa file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="a00c9-168">Per toobe file hello accodati a, hello chiamante esigenze **scrivere** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="a00c9-169">Per tutti hello cartelle contenenti file hello, hello chiamante esigenze **Execute** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="a00c9-170">Autorizzazioni necessarie toodelete un file</span><span class="sxs-lookup"><span data-stu-id="a00c9-170">Permissions needed toodelete a file</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="a00c9-172">Cartella padre hello, hello chiamante esigenze **scrittura eseguire** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="a00c9-173">Per tutti hello altre cartelle nel percorso del file hello, hello chiamante esigenze **Execute** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="a00c9-174">Scrivere le autorizzazioni per file hello non sono necessari toodelete purché hello precedente due condizioni sono true.</span><span class="sxs-lookup"><span data-stu-id="a00c9-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="a00c9-175">Autorizzazioni necessarie tooenumerate una cartella</span><span class="sxs-lookup"><span data-stu-id="a00c9-175">Permissions needed tooenumerate a folder</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="a00c9-177">Per tooenumerate cartella hello, hello chiamante esigenze **lettura + Execute** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="a00c9-178">Per tutti hello cartelle predecessore, hello chiamante esigenze **Execute** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="a00c9-179">Autorizzazioni di visualizzazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="a00c9-180">Da hello **Esplora dati** fare clic su Pannello di hello account archivio Data Lake, **accesso** toosee hello ACL per un file o una cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="a00c9-181">Fare clic su **accesso** toosee hello ACL per hello **catalogo** cartella hello **mydatastore** account.</span><span class="sxs-lookup"><span data-stu-id="a00c9-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="a00c9-183">In questo pannello, nella sezione superiore hello Mostra una panoramica delle autorizzazioni hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="a00c9-184">(Nella schermata hello utente hello è Bob). Successivamente, vengono visualizzate le autorizzazioni di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="a00c9-185">Dopo che da hello **accesso** pannello, fare clic su **vista semplice** toosee hello visualizzazione più semplice.</span><span class="sxs-lookup"><span data-stu-id="a00c9-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="a00c9-187">Fare clic su **vista avanzata** toosee hello più avanzate, visualizzazione in cui vengono visualizzati i concetti di hello di ACL predefinito, la maschera e utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="a00c9-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="a00c9-189">utente avanzato Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-189">hello super-user</span></span>

<span data-ttu-id="a00c9-190">Un utente avanzato è hello la maggior parte dei diritti di tutti gli utenti di hello hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="a00c9-191">Un utente con privilegi avanzati:</span><span class="sxs-lookup"><span data-stu-id="a00c9-191">A super-user:</span></span>

* <span data-ttu-id="a00c9-192">Disponga delle autorizzazioni di RWX troppo**tutti** file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="a00c9-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="a00c9-193">Può modificare le autorizzazioni di hello su qualsiasi file o cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="a00c9-194">Cambiare hello utente proprietario o l'appartenenza a gruppo di qualsiasi file o cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="a00c9-195">In Azure un account Data Lake Store include diversi ruoli di Azure, tra cui:</span><span class="sxs-lookup"><span data-stu-id="a00c9-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="a00c9-196">Proprietari</span><span class="sxs-lookup"><span data-stu-id="a00c9-196">Owners</span></span>
* <span data-ttu-id="a00c9-197">Collaboratori</span><span class="sxs-lookup"><span data-stu-id="a00c9-197">Contributors</span></span>
* <span data-ttu-id="a00c9-198">Lettori</span><span class="sxs-lookup"><span data-stu-id="a00c9-198">Readers</span></span>

<span data-ttu-id="a00c9-199">Tutti gli utenti hello **proprietari** ruolo per un account archivio Data Lake è automaticamente un utente avanzato per l'account.</span><span class="sxs-lookup"><span data-stu-id="a00c9-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="a00c9-200">vedere, più toolearn [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a00c9-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="a00c9-201">Se si desidera toocreate un ruolo di controllo di accesso basato sui ruoli (RBAC) personalizzato che dispone delle autorizzazioni utente avanzato, è necessario hello toohave queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="a00c9-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="a00c9-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="a00c9-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="a00c9-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="a00c9-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="a00c9-204">utente proprietario Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-204">hello owning user</span></span>

<span data-ttu-id="a00c9-205">utente di Hello che ha creato l'elemento hello è automaticamente hello utente dell'elemento hello proprietario.</span><span class="sxs-lookup"><span data-stu-id="a00c9-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="a00c9-206">Un utente proprietario può:</span><span class="sxs-lookup"><span data-stu-id="a00c9-206">An owning user can:</span></span>

* <span data-ttu-id="a00c9-207">Modificare le autorizzazioni di hello di un file di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a00c9-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="a00c9-208">Modificare l'appartenenza gruppo di un file di proprietà, come utente proprietario hello è anche un membro del gruppo di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="a00c9-209">utente proprietario Hello *Impossibile* modificare hello proprietario l'utente di un altro file di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a00c9-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="a00c9-210">Solo gli utenti Super modificabili hello proprietario l'utente di un file o cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="a00c9-211">gruppo proprietario Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-211">hello owning group</span></span>

<span data-ttu-id="a00c9-212">Hello ACL POSIX, ogni utente è associata a un "gruppo primario".</span><span class="sxs-lookup"><span data-stu-id="a00c9-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="a00c9-213">Ad esempio, l'utente "alice" potrebbe appartenere gruppo "finance" toohello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="a00c9-214">Alice potrebbe appartenere anche toomultiple gruppi, ma un gruppo viene sempre definito come suo gruppo primario.</span><span class="sxs-lookup"><span data-stu-id="a00c9-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="a00c9-215">In POSIX, quando Alice crea un file, hello appartenenza gruppo di file è tooher gruppo primario, ovvero in questo caso "finance".</span><span class="sxs-lookup"><span data-stu-id="a00c9-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="a00c9-216">Quando viene creato un nuovo elemento filesystem, archivio Data Lake assegna un valore toohello proprietario gruppo.</span><span class="sxs-lookup"><span data-stu-id="a00c9-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="a00c9-217">**Caso 1**: cartella radice hello "/".</span><span class="sxs-lookup"><span data-stu-id="a00c9-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="a00c9-218">Questa cartella viene creata al momento della creazione di un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a00c9-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="a00c9-219">In questo caso, hello appartenenza gruppo toohello utente che ha creato l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="a00c9-220">**Caso 2** (tutti gli altri casi): quando viene creato un nuovo elemento, gruppo proprietario hello viene copiato dalla cartella padre hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="a00c9-221">gruppo proprietario Hello può essere modificato da:</span><span class="sxs-lookup"><span data-stu-id="a00c9-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="a00c9-222">Qualsiasi utente con privilegi avanzati.</span><span class="sxs-lookup"><span data-stu-id="a00c9-222">Any super-users.</span></span>
* <span data-ttu-id="a00c9-223">Hello proprietario l'utente, se l'utente proprietario hello è anche un membro del gruppo di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="a00c9-224">Algoritmo di controllo dell'accesso</span><span class="sxs-lookup"><span data-stu-id="a00c9-224">Access check algorithm</span></span>

<span data-ttu-id="a00c9-225">Hello nella figura riportata di seguito rappresenta l'algoritmo di controllo di accesso di hello per gli account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algoritmo per gli ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="a00c9-227">maschera di Hello e "autorizzazioni"</span><span class="sxs-lookup"><span data-stu-id="a00c9-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="a00c9-228">Hello **mask** è un RWX valore che rappresenta l'accesso toolimit utilizzati per **denominato utenti**, hello **proprietario gruppo**, e **gruppi denominati** quando si è algoritmo di controllo di accesso hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a00c9-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="a00c9-229">Ecco i concetti chiave hello per mask hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="a00c9-230">maschera di Hello crea "autorizzazioni".</span><span class="sxs-lookup"><span data-stu-id="a00c9-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="a00c9-231">Vale a dire, di modificare le autorizzazioni di hello in fase di hello di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="a00c9-232">maschera di Hello può essere modificato direttamente dal proprietario del file hello e a qualsiasi utente super.</span><span class="sxs-lookup"><span data-stu-id="a00c9-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="a00c9-233">maschera Hello è possibile rimuovere le autorizzazioni toocreate hello effettivo di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="a00c9-234">maschera di Hello *Impossibile* aggiungere autorizzazioni toohello effettivo di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="a00c9-235">Verranno ora esaminati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="a00c9-235">Let's look at some examples.</span></span> <span data-ttu-id="a00c9-236">Nell'esempio seguente di hello, mask hello è troppo**RWX**, che indica che la maschera hello non rimuovere tutte le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="a00c9-237">le autorizzazioni valide di Hello per hello denominato utente, denominato gruppo e appartenenza gruppo non vengono modificate durante il controllo di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="a00c9-239">Nell'esempio seguente di hello, mask hello è troppo**R-X**.</span><span class="sxs-lookup"><span data-stu-id="a00c9-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="a00c9-240">Ciò significa che **disattiva le autorizzazioni di scrittura hello** per **denominato utente**, **proprietario gruppo**, e **gruppo denominato** in fase di hello di accesso controllo.</span><span class="sxs-lookup"><span data-stu-id="a00c9-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="a00c9-242">Per riferimento, ecco maschera hello per un file o una cartella in cui è presente hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a00c9-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="a00c9-244">Per un nuovo account archivio Data Lake, hello mask per hello accesso ACL predefinita della radice hello ("/") per impostazione predefinita cartella tooRWX.</span><span class="sxs-lookup"><span data-stu-id="a00c9-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="a00c9-245">Autorizzazioni per nuovi file e cartelle</span><span class="sxs-lookup"><span data-stu-id="a00c9-245">Permissions on new files and folders</span></span>

<span data-ttu-id="a00c9-246">Quando in una cartella esistente, viene creato un nuovo file o una cartella, hello ACL predefinita nella cartella padre hello determina:</span><span class="sxs-lookup"><span data-stu-id="a00c9-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="a00c9-247">ACL predefinito e ACL di accesso di una cartella figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="a00c9-248">ACL di accesso di un file figlio (i file non hanno un ACL predefinito).</span><span class="sxs-lookup"><span data-stu-id="a00c9-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="a00c9-249">Hello accesso di una cartella o file figlio</span><span class="sxs-lookup"><span data-stu-id="a00c9-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="a00c9-250">Quando viene creata una cartella o un file figlio, viene copiato ACL predefinito dell'elemento padre di hello come hello accesso ACL del file figlio hello o della cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="a00c9-251">Inoltre, se **altri** utente disponga delle autorizzazioni di RWX nell'ACL predefinito dell'elemento padre di hello, viene rimosso dalla finestra di accesso dell'elemento figlio di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="a00c9-253">Nella maggior parte degli scenari, le informazioni precedenti relative hello vengono che tutti necessarie tooknow sulla determinazione di accesso dell'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="a00c9-254">Tuttavia, se si ha familiarità con i sistemi POSIX e dettagliate desidera toounderstand come viene ottenuta questa trasformazione, vedere la sezione hello [ruolo dell'Umask creazione hello accesso ACL per i nuovi file e cartelle](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a00c9-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="a00c9-255">ACL predefinito di una cartella figlio</span><span class="sxs-lookup"><span data-stu-id="a00c9-255">A child folder's Default ACL</span></span>

<span data-ttu-id="a00c9-256">Creazione di una cartella figlio in una cartella padre, ACL predefinito della cartella padre hello è copiate come ACL predefinito della cartella di toohello figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="a00c9-258">Argomenti avanzati per informazioni dettagliate sugli ACL in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a00c9-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="a00c9-259">Di seguito sono toohelp alcuni argomenti avanzati che è comprendere il modo in cui vengono determinati gli ACL per le cartelle o file di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="a00c9-260">Ruolo dell'umask creazione hello accesso ACL per i nuovi file e cartelle</span><span class="sxs-lookup"><span data-stu-id="a00c9-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="a00c9-261">In un sistema compatibile POSIX, concetto generale hello è tale umask è un valore di bit 9 alla cartella padre hello utilizzati autorizzazione hello tootransform per **utente proprietario**, **proprietario gruppo**, e  **altri** su hello accesso di una cartella o un nuovo file figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="a00c9-262">bit Hello di un umask identificare quali tooturn bit accesso ACL dell'elemento figlio di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="a00c9-263">In questo modo viene utilizzato tooselectively impedire la propagazione di hello delle autorizzazioni per **utente proprietario**, **proprietario gruppo**, e **altri**.</span><span class="sxs-lookup"><span data-stu-id="a00c9-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="a00c9-264">In un sistema di HDFS umask hello in genere è un'opzione di configurazione in tutto il sito che viene controllata dagli amministratori.</span><span class="sxs-lookup"><span data-stu-id="a00c9-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="a00c9-265">Data Lake Store usa una proprietà **umask a livello di account** non modificabile.</span><span class="sxs-lookup"><span data-stu-id="a00c9-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="a00c9-266">annullare il mascheramento Hello hello illustrato nella tabella seguente per archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="a00c9-267">Gruppo utenti</span><span class="sxs-lookup"><span data-stu-id="a00c9-267">User group</span></span>  | <span data-ttu-id="a00c9-268">Impostazione</span><span class="sxs-lookup"><span data-stu-id="a00c9-268">Setting</span></span> | <span data-ttu-id="a00c9-269">Effetto sull'ACL di accesso di un nuovo elemento figlio</span><span class="sxs-lookup"><span data-stu-id="a00c9-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="a00c9-270">utente proprietario</span><span class="sxs-lookup"><span data-stu-id="a00c9-270">Owning user</span></span> | ---     | <span data-ttu-id="a00c9-271">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="a00c9-271">No effect</span></span>                             |
| <span data-ttu-id="a00c9-272">gruppo proprietario</span><span class="sxs-lookup"><span data-stu-id="a00c9-272">Owning group</span></span>| ---     | <span data-ttu-id="a00c9-273">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="a00c9-273">No effect</span></span>                             |
| <span data-ttu-id="a00c9-274">altri</span><span class="sxs-lookup"><span data-stu-id="a00c9-274">Other</span></span>       | <span data-ttu-id="a00c9-275">RWX</span><span class="sxs-lookup"><span data-stu-id="a00c9-275">RWX</span></span>     | <span data-ttu-id="a00c9-276">Rimuovere Lettura + Scrittura + Esecuzione</span><span class="sxs-lookup"><span data-stu-id="a00c9-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="a00c9-277">Hello nella figura seguente viene illustrata questa umask in azione.</span><span class="sxs-lookup"><span data-stu-id="a00c9-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="a00c9-278">effetto Hello è tooremove **lettura + scrivere ed eseguire** per **altri** utente.</span><span class="sxs-lookup"><span data-stu-id="a00c9-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="a00c9-279">Poiché umask hello non specificava bits per **utente proprietario** e **proprietario gruppo**, tali autorizzazioni non vengono trasformate.</span><span class="sxs-lookup"><span data-stu-id="a00c9-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="a00c9-281">bit permanenti Hello</span><span class="sxs-lookup"><span data-stu-id="a00c9-281">hello sticky bit</span></span>

<span data-ttu-id="a00c9-282">bit permanenti Hello è una funzionalità più avanzata di un file System POSIX.</span><span class="sxs-lookup"><span data-stu-id="a00c9-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="a00c9-283">Nel contesto di hello dell'archivio Data Lake, è improbabile che bit permanenti hello saranno necessari.</span><span class="sxs-lookup"><span data-stu-id="a00c9-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="a00c9-284">Hello nella tabella seguente viene illustrato il funzionamento di bit permanenti hello in archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="a00c9-285">Gruppo utenti</span><span class="sxs-lookup"><span data-stu-id="a00c9-285">User group</span></span>         | <span data-ttu-id="a00c9-286">File</span><span class="sxs-lookup"><span data-stu-id="a00c9-286">File</span></span>    | <span data-ttu-id="a00c9-287">Cartella</span><span class="sxs-lookup"><span data-stu-id="a00c9-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="a00c9-288">Sticky bit **OFF**</span><span class="sxs-lookup"><span data-stu-id="a00c9-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="a00c9-289">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="a00c9-289">No effect</span></span>   | <span data-ttu-id="a00c9-290">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="a00c9-290">No effect.</span></span>           |
| <span data-ttu-id="a00c9-291">Sticky bit **ON**</span><span class="sxs-lookup"><span data-stu-id="a00c9-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="a00c9-292">Nessun effetto</span><span class="sxs-lookup"><span data-stu-id="a00c9-292">No effect</span></span>   | <span data-ttu-id="a00c9-293">Impedisce a chiunque tranne **utenti super** hello e **utente proprietario** di un elemento figlio da eliminazione o ridenominazione di tale elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="a00c9-294">bit permanenti Hello non è visualizzata nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="a00c9-295">Domande frequenti sugli ACL in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a00c9-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="a00c9-296">Di seguito sono riportate alcune domande frequenti sugli ACL in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a00c9-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="a00c9-297">È necessario il supporto per gli elenchi ACL tooenable?</span><span class="sxs-lookup"><span data-stu-id="a00c9-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="a00c9-298">No.</span><span class="sxs-lookup"><span data-stu-id="a00c9-298">No.</span></span> <span data-ttu-id="a00c9-299">Il controllo di accesso tramite ACL è sempre attivo per un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a00c9-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="a00c9-300">Quali autorizzazioni sono necessarie toorecursively Elimina la cartella e il relativo contenuto?</span><span class="sxs-lookup"><span data-stu-id="a00c9-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="a00c9-301">cartella padre Hello deve avere **scrittura eseguire** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="a00c9-302">Hello toobe cartella eliminata, e ogni cartella all'interno di esso, è necessario **lettura + scrivere ed eseguire** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a00c9-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="a00c9-303">Non è necessario scrivere le autorizzazioni toodelete file nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="a00c9-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="a00c9-304">Inoltre, hello cartella radice "/" può **mai** da eliminare.</span><span class="sxs-lookup"><span data-stu-id="a00c9-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="a00c9-305">Chi è proprietario di hello di un file o cartella?</span><span class="sxs-lookup"><span data-stu-id="a00c9-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="a00c9-306">creatore Hello di un file o cartella diventa il proprietario di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="a00c9-307">Il gruppo a cui è impostato come proprietario del gruppo di file o cartelle al momento della creazione di hello?</span><span class="sxs-lookup"><span data-stu-id="a00c9-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="a00c9-308">gruppo proprietario Hello viene copiato dal proprietario della cartella padre hello quali hello nuovo file o cartella viene creato in gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="a00c9-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="a00c9-309">Sto hello proprietario l'utente di un file ma non si dispone delle autorizzazioni RWX hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="a00c9-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="a00c9-310">Cosa devo fare?</span><span class="sxs-lookup"><span data-stu-id="a00c9-310">What do I do?</span></span>

<span data-ttu-id="a00c9-311">utente proprietario Hello possibile modificarle hello toogive file hello stessi eventuali autorizzazioni RWX che necessarie.</span><span class="sxs-lookup"><span data-stu-id="a00c9-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="a00c9-312">Quando si visualizzano gli ACL nel portale di Azure hello vedo nomi utente, ma tramite le API, viene visualizzato GUID, è possibile?</span><span class="sxs-lookup"><span data-stu-id="a00c9-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="a00c9-313">Voci ACL hello vengono archiviate come GUID corrispondenti toousers in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a00c9-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="a00c9-314">Hello API restituiscono hello GUID come è.</span><span class="sxs-lookup"><span data-stu-id="a00c9-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="a00c9-315">Hello portale di Azure tenta toomake ACL più facile toouse dalla conversione hello GUID in nomi descrittivi, quando possibile.</span><span class="sxs-lookup"><span data-stu-id="a00c9-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="a00c9-316">Perché viene talvolta visualizzato GUID hello ACL durante l'utilizzo di hello portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="a00c9-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="a00c9-317">Un GUID viene visualizzato quando l'utente hello non esiste in più di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a00c9-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="a00c9-318">In genere ciò si verifica quando l'utente hello ha lasciato l'azienda di hello o il proprio account è stato eliminato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a00c9-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="a00c9-319">Data Lake Store supporta l'ereditarietà degli ACL?</span><span class="sxs-lookup"><span data-stu-id="a00c9-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="a00c9-320">No.</span><span class="sxs-lookup"><span data-stu-id="a00c9-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="a00c9-321">Qual è la differenza hello tra maschera e umask?</span><span class="sxs-lookup"><span data-stu-id="a00c9-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="a00c9-322">mask</span><span class="sxs-lookup"><span data-stu-id="a00c9-322">mask</span></span> | <span data-ttu-id="a00c9-323">umask</span><span class="sxs-lookup"><span data-stu-id="a00c9-323">umask</span></span>|
|------|------|
| <span data-ttu-id="a00c9-324">Hello **mask** proprietà è disponibile in tutti i file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="a00c9-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="a00c9-325">Hello **umask** è una proprietà di hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="a00c9-326">Pertanto, è solo un singolo umask hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a00c9-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="a00c9-327">proprietà mask Hello in un file o cartella può essere modificata da hello proprietario l'utente o gruppo di un file o un utente avanzato di proprietario.</span><span class="sxs-lookup"><span data-stu-id="a00c9-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="a00c9-328">proprietà umask Hello non può essere modificato da alcun utente, anche un utente avanzato.</span><span class="sxs-lookup"><span data-stu-id="a00c9-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="a00c9-329">È un valore costante non modificabile.</span><span class="sxs-lookup"><span data-stu-id="a00c9-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="a00c9-330">proprietà mask Hello viene utilizzato durante l'algoritmo di controllo di accesso di hello in fase di esecuzione toodetermine se un utente ha tooperform destra hello operazione su un file o cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="a00c9-331">ruolo di Hello della maschera hello è toocreate "autorizzazioni" in fase di hello di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="a00c9-332">umask Hello non viene usato affatto durante il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="a00c9-333">umask Hello è usato toodetermine hello accesso ACL di nuovi elementi figlio di una cartella.</span><span class="sxs-lookup"><span data-stu-id="a00c9-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="a00c9-334">maschera di Hello è un valore di 3 bit RWX che applica toonamed utente, gruppo e utente proprietario in fase di hello di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="a00c9-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="a00c9-335">umask Hello è un valore di bit 9 che applica toohello proprietario l'utente, proprietario, gruppo e **altri** di un nuovo elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="a00c9-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="a00c9-336">Dove è possibile reperire altre informazioni sul modello di controllo di accesso POSIX?</span><span class="sxs-lookup"><span data-stu-id="a00c9-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="a00c9-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Elenchi di controllo di accesso POSIX in Linux)</span><span class="sxs-lookup"><span data-stu-id="a00c9-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="a00c9-338">[HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Guida alle autorizzazioni HDFS)</span><span class="sxs-lookup"><span data-stu-id="a00c9-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="a00c9-339">Domande frequenti su POSIX</span><span class="sxs-lookup"><span data-stu-id="a00c9-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="a00c9-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="a00c9-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="a00c9-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="a00c9-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="a00c9-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="a00c9-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="a00c9-343">ACL POSIX in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a00c9-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* <span data-ttu-id="a00c9-344">[ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: uso di elenchi di controllo di accesso in Linux)</span><span class="sxs-lookup"><span data-stu-id="a00c9-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="a00c9-345">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a00c9-345">See also</span></span>

* [<span data-ttu-id="a00c9-346">Panoramica dell’Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="a00c9-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
