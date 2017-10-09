---
title: aaaManage dati personali in Microsoft Azure | Documenti Microsoft
description: informazioni aggiuntive su come toocorrect, aggiornare, eliminare ed esportare dati personali in Azure Active Directory e Database SQL di Azure
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="071a3-103">Gestire i dati personali in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="071a3-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="071a3-104">Questo articolo fornisce informazioni aggiuntive su come toocorrect, aggiornare, eliminare ed esportare dati personali in Azure Active Directory e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="071a3-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="071a3-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="071a3-105">Scenario</span></span>

<span data-ttu-id="071a3-106">Una società di Dublin fornisce un punto vendita per matrimoni di destinazione di fascia alta in Irlanda e tutto il mondo hello per entrambi una base per i clienti locali e internazionali.</span><span class="sxs-lookup"><span data-stu-id="071a3-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="071a3-107">Hanno uffici, clienti, dipendenti e fornitori dislocati in località hello hello world toofully servizio che offrono.</span><span class="sxs-lookup"><span data-stu-id="071a3-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="071a3-108">Tra molti altri elementi, la società hello tiene traccia di inviate risposte che includono allergie food e le preferenze del.</span><span class="sxs-lookup"><span data-stu-id="071a3-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="071a3-109">Gli utenti guest matrimonio può registrare per varie attività, ad esempio riding, percorso di navigazione, emergenza si basa e così via e anche interagire tra loro in una pagina web centrale mesi hello conducono toohello evento.</span><span class="sxs-lookup"><span data-stu-id="071a3-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="071a3-110">società Hello raccoglie informazioni personali dai dipendenti, fornitori, clienti e utenti guest matrimonio.</span><span class="sxs-lookup"><span data-stu-id="071a3-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="071a3-111">A causa di hello natura internazionale hello hello azienda deve conformarsi a più livelli del regolamento.</span><span class="sxs-lookup"><span data-stu-id="071a3-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="071a3-112">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="071a3-112">Problem statement</span></span>

- <span data-ttu-id="071a3-113">Gli amministratori di dati devono essere toocorrect in grado di corrette personale informazioni e aggiornamento incomplete o la modifica delle informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="071a3-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="071a3-114">Necessità di amministratori di dati deve essere in grado di toodelete informazioni personali su richiesta hello di un oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="071a3-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="071a3-115">Gli amministratori di dati necessario tooexport dati e forniscono tooa soggetto di dati in un formato comune e strutturato sulla propria richiesta.</span><span class="sxs-lookup"><span data-stu-id="071a3-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="071a3-116">Obiettivi dell'azienda</span><span class="sxs-lookup"><span data-stu-id="071a3-116">Company goals</span></span>

- <span data-ttu-id="071a3-117">I dati personali errati di clienti, ospiti, dipendenti e fornitori devono essere corretti e aggiornati in Azure Active Directory e nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="071a3-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="071a3-118">Informazioni personali dell'utente devono essere eliminate in Azure Active Directory e Database SQL di Azure su richiesta hello di un oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="071a3-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="071a3-119">Dati personali devono essere esportati in un formato comune e strutturato su richiesta hello di un oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="071a3-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="071a3-120">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="071a3-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="071a3-121">Azure Active Directory: rettificare/correggere i dati personali errati o incompleti e cancellare/eliminare i profili utente/dati personali</span><span class="sxs-lookup"><span data-stu-id="071a3-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="071a3-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) è un servizio Microsoft per la gestione delle identità e delle directory multi-tenant, basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="071a3-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="071a3-123">È possibile correggere, aggiornare o eliminare i profili utente di clienti e dipendenti e le informazioni utente lavoro che contengono dati personali, ad esempio nome, il titolo di lavoro, indirizzo o il numero di telefono, un utente nel [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) ambiente utilizzando hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="071a3-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="071a3-124">È necessario accedere con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="071a3-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="071a3-125">Come si correggono o si aggiornano le informazioni del profilo e di lavoro degli utenti in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="071a3-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="071a3-126">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="071a3-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="071a3-127">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="071a3-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![supporto/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="071a3-129">In hello **utenti e gruppi** pannello seleziona **utenti**.</span><span class="sxs-lookup"><span data-stu-id="071a3-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="071a3-131">In hello **utenti e gruppi di utenti -** pannello selezionare un utente dall'elenco di hello, quindi, nel Pannello di hello per l'utente selezionato hello, **profilo** tooview hello informazioni del profilo utente che deve toobe corretto o aggiornati.</span><span class="sxs-lookup"><span data-stu-id="071a3-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="071a3-133">Correggere o aggiornare le informazioni di hello e quindi nella barra dei comandi di hello, selezionare **salvare.**</span><span class="sxs-lookup"><span data-stu-id="071a3-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="071a3-134">Nel Pannello di hello per l'utente selezionato hello, selezionare **Info lavoro** informazioni sul lavoro tooview utente che deve toobe corretto o è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="071a3-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="071a3-136">Correggere o aggiornare le informazioni lavoro hello e quindi nella barra dei comandi di hello, selezionare **salvare.**</span><span class="sxs-lookup"><span data-stu-id="071a3-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="071a3-137">Come si elimina un profilo utente in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="071a3-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="071a3-138">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="071a3-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="071a3-139">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="071a3-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="071a3-140">In hello **utenti e gruppi** pannello seleziona **utenti**.</span><span class="sxs-lookup"><span data-stu-id="071a3-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="071a3-142">In hello **utenti e gruppi di utenti -** pannello, selezionare un utente dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="071a3-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="071a3-144">Nel Pannello di hello per l'utente selezionato hello, selezionare **Panoramica**, quindi nella barra dei comandi di hello, selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="071a3-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="071a3-145">Database SQL: rettificare/correggere i dati personali errati o incompleti, cancellare/eliminare di dati personali ed esportare i dati personali</span><span class="sxs-lookup"><span data-stu-id="071a3-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="071a3-146">Il [database SQL di Microsoft Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) è un database che consente agli sviluppatori di compilare e gestire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="071a3-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="071a3-147">I dati personali possono essere aggiornati nel [database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando le query SQL standard e possono anche essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="071a3-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="071a3-148">Inoltre, è possibile esportare i dati personali da Database SQL tramite una vasta gamma di metodi, incluso hello importazione Server SQL Azure e l'esportazione guidata in un'ampia gamma di formati, tra cui un file BACPAC.</span><span class="sxs-lookup"><span data-stu-id="071a3-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="071a3-149">Come si correggono, aggiornano o cancellano i dati personali nel database SQL?</span><span class="sxs-lookup"><span data-stu-id="071a3-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="071a3-150">toolearn come toocorrect o aggiornamento dati personali in Database SQL, visitare hello [aggiornamento (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [aggiornare testo](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [aggiornare con l'espressione di tabella comune](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), o [ Aggiornamento del testo scrivere](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentazione.</span><span class="sxs-lookup"><span data-stu-id="071a3-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="071a3-151">toolearn come toodelete dati personali in Database SQL, visitare hello [eliminare (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentazione.</span><span class="sxs-lookup"><span data-stu-id="071a3-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="071a3-152">Come esportare file BACPAC di tooa dati personali in Database SQL?</span><span class="sxs-lookup"><span data-stu-id="071a3-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="071a3-153">Un file BACPAC include i metadati e dati del Database SQL hello e un file zip con estensione BACPAC.</span><span class="sxs-lookup"><span data-stu-id="071a3-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="071a3-154">Questa operazione può essere eseguita utilizzando hello [portale di Azure](https://portal.azure.com/), hello SQLPackage utilità della riga di comando, SQL Server Management Studio (SSMS) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="071a3-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="071a3-155">toolearn come file BACPAC tooa di tooexport dati, visitare hello [esportare un file BACPAC di SQL Azure database tooa](https://docs.microsoft.com/azure/sql-database/sql-database-export) pagina, che include istruzioni dettagliate per ogni metodo elencate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="071a3-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="071a3-156">Come esportare i dati personali da Database SQL con SQL Server Import hello / esportazione guidata?</span><span class="sxs-lookup"><span data-stu-id="071a3-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="071a3-157">Questa procedura guidata consente di copiare i dati da una destinazione tooa di origine.</span><span class="sxs-lookup"><span data-stu-id="071a3-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="071a3-158">Per una procedura guidata toohello introduzione, incluso come tooget, le informazioni sulle autorizzazioni e informazioni tooget con lo strumento di hello, visitare hello [importazione e l'esportazione di dati con SQL Server Import hello / esportazione guidata](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) pagina web.</span><span class="sxs-lookup"><span data-stu-id="071a3-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="071a3-159">Per una panoramica dei passaggi della procedura guidata hello, visitare hello [passaggi hello SQL Server di importazione / esportazione guidata](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) pagina web.</span><span class="sxs-lookup"><span data-stu-id="071a3-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="071a3-160">Passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="071a3-160">Next Steps:</span></span>

[<span data-ttu-id="071a3-161">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="071a3-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="071a3-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="071a3-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

