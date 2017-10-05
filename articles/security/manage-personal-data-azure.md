---
title: Gestire i dati personali in Microsoft Azure | Microsoft Docs
description: Linee guida per correggere, aggiornare, eliminare ed esportare i dati personali in Azure Active Directory e nel database SQL di Azure
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
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="9e42e-103">Gestire i dati personali in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9e42e-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="9e42e-104">Questo articolo descrive le linee guida per correggere, aggiornare, eliminare ed esportare i dati personali in Azure Active Directory e nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e42e-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="9e42e-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="9e42e-105">Scenario</span></span>

<span data-ttu-id="9e42e-106">Una società con sede a Dublino offre pacchetti completi per matrimoni di fascia alta in Irlanda e in tutto il mondo per una clientela sia locale sia internazionale.</span><span class="sxs-lookup"><span data-stu-id="9e42e-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="9e42e-107">La società ha uffici, clienti, dipendenti e fornitori in tutto il mondo al fine di garantire un servizio completo nelle località che offre.</span><span class="sxs-lookup"><span data-stu-id="9e42e-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="9e42e-108">Tra i tanti servizi che gestisce, la società tiene traccia delle risposte agli inviti che includono preferenze e allergie alimentari.</span><span class="sxs-lookup"><span data-stu-id="9e42e-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="9e42e-109">Gli ospiti che partecipano ai matrimoni possono iscriversi a varie attività come una passeggiata a cavallo, un giro in barca e così via. Possono persino interagire reciprocamente in una pagina Web centrale nei mesi che precedono l'evento.</span><span class="sxs-lookup"><span data-stu-id="9e42e-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="9e42e-110">La società raccoglie i dati personali di dipendenti, fornitori, clienti e ospiti dei matrimoni.</span><span class="sxs-lookup"><span data-stu-id="9e42e-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="9e42e-111">A causa della natura internazionale della propria attività, la società deve osservare più livelli di normative.</span><span class="sxs-lookup"><span data-stu-id="9e42e-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="9e42e-112">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="9e42e-112">Problem statement</span></span>

- <span data-ttu-id="9e42e-113">Gli amministratori di dati devono essere in grado di correggere eventuali errori nei dati personali, modificare i dati e aggiornare quelli incompleti.</span><span class="sxs-lookup"><span data-stu-id="9e42e-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="9e42e-114">Necessità di amministratori di dati deve essere in grado di eliminare le informazioni personali alla richiesta di un oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="9e42e-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="9e42e-115">Devono poter esportare i dati e renderli disponibili su richiesta di un soggetto interessato in un formato comune e strutturato.</span><span class="sxs-lookup"><span data-stu-id="9e42e-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="9e42e-116">Obiettivi della società</span><span class="sxs-lookup"><span data-stu-id="9e42e-116">Company goals</span></span>

- <span data-ttu-id="9e42e-117">I dati personali errati di clienti, ospiti, dipendenti e fornitori devono essere corretti e aggiornati in Azure Active Directory e nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e42e-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="9e42e-118">I dati personali devono essere eliminati in Azure Active Directory e nel database SQL di Azure su richiesta di un interessato.</span><span class="sxs-lookup"><span data-stu-id="9e42e-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="9e42e-119">I dati personali devono essere esportati su richiesta di un interessato in un formato comune e strutturato.</span><span class="sxs-lookup"><span data-stu-id="9e42e-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="9e42e-120">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="9e42e-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="9e42e-121">Azure Active Directory: rettificare/correggere i dati personali errati o incompleti e cancellare/eliminare i profili utente/dati personali</span><span class="sxs-lookup"><span data-stu-id="9e42e-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="9e42e-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) è un servizio Microsoft per la gestione delle identità e delle directory multi-tenant, basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="9e42e-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="9e42e-123">È possibile correggere, aggiornare o eliminare i profili utente dei clienti e dei dipendenti e le informazioni di lavoro dell'utente che contengono dati personali, ad esempio il nome, il titolo di lavoro, l'indirizzo o il numero di telefono, nell'ambiente [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) tramite il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9e42e-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="9e42e-124">È necessario accedere con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="9e42e-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="9e42e-125">Come si correggono o si aggiornano le informazioni del profilo e di lavoro degli utenti in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e42e-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="9e42e-126">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="9e42e-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="9e42e-127">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![supporto/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="9e42e-129">Nel pannello **Utenti e gruppi** selezionare **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="9e42e-131">Nel pannello **Utenti e gruppi - Utenti** selezionare un utente nell'elenco, quindi nel pannello dell'utente selezionato scegliere **Profilo** per visualizzare le informazioni del profilo utente che devono essere corrette o aggiornate.</span><span class="sxs-lookup"><span data-stu-id="9e42e-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="9e42e-133">Correggere o aggiornare le informazioni e quindi selezionare **Salva** nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9e42e-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="9e42e-134">Nel pannello dell'utente selezionato, selezionare **Informazioni lavoro** per visualizzare le informazioni di lavoro dell'utente che devono essere corrette o aggiornate.</span><span class="sxs-lookup"><span data-stu-id="9e42e-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="9e42e-136">Correggere o aggiornare le informazioni di lavoro e quindi nella barra dei comandi selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="9e42e-137">Come si elimina un profilo utente in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e42e-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="9e42e-138">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="9e42e-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="9e42e-139">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="9e42e-140">Nel pannello **Utenti e gruppi** selezionare **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="9e42e-142">Nel pannello **Utenti e gruppi - Utenti** selezionare un utente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="9e42e-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="9e42e-144">Nel pannello dell'utente selezionare **Panoramica**, quindi nella barra dei comandi selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="9e42e-145">Database SQL: rettificare/correggere i dati personali errati o incompleti, cancellare/eliminare di dati personali ed esportare i dati personali</span><span class="sxs-lookup"><span data-stu-id="9e42e-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="9e42e-146">Il [database SQL di Microsoft Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) è un database che consente agli sviluppatori di compilare e gestire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9e42e-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="9e42e-147">I dati personali possono essere aggiornati nel [database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando le query SQL standard e possono anche essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="9e42e-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="9e42e-148">È inoltre possibile esportarli dal database SQL usando vari modi, tra cui Importazione/Esportazione guidata Server SQL di Azure, e un'ampia gamma di formati, incluso un file con estensione BACPAC.</span><span class="sxs-lookup"><span data-stu-id="9e42e-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="9e42e-149">Come si correggono, aggiornano o cancellano i dati personali nel database SQL?</span><span class="sxs-lookup"><span data-stu-id="9e42e-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="9e42e-150">Per informazioni su come correggere o aggiornare i dati personali nel database SQL, consultare al documentazione relativa a [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql) o [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="9e42e-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="9e42e-151">Per informazioni su come eliminare i dati personali nel database SQL, consultare la documentazione relativa a [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="9e42e-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="9e42e-152">Come si esportano i dati personali verso un file BACPAC nel database SQL?</span><span class="sxs-lookup"><span data-stu-id="9e42e-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="9e42e-153">Un file BACPAC include i dati e i metadati del database SQL ed un file compresso con estensione BACPAC.</span><span class="sxs-lookup"><span data-stu-id="9e42e-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="9e42e-154">Questa operazione può essere eseguita usando il [portale di Azure](https://portal.azure.com/), l'utilità della riga di comando SQLPackage, SQL Server Management Studio (SSMS) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e42e-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="9e42e-155">Per informazioni su come esportare i dati in un file BACPAC, visitare la pagina [Esportare un database SQL di Azure in un file BACPAC](https://docs.microsoft.com/azure/sql-database/sql-database-export), che include le istruzioni dettagliate per seguire i modi elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9e42e-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="9e42e-156">Come si esportano i dati personali dal database SQL con Importazione/Esportazione guidata SQL Server?</span><span class="sxs-lookup"><span data-stu-id="9e42e-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="9e42e-157">Questa procedura guidata consente di copiare i dati da un'origine a una destinazione.</span><span class="sxs-lookup"><span data-stu-id="9e42e-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="9e42e-158">Per un'introduzione alla procedura guidata, incluse le istruzioni per visualizzarla, le informazioni sulle autorizzazioni e le istruzioni su come ottenere assistenza per questo strumento, visitare la pagina Web [Importare ed esportare dati con l'Importazione/Esportazione guidata SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="9e42e-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="9e42e-159">Per una panoramica dei passaggi della procedura guidata, visitare la pagina Web [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) (Passaggi di Importazione/Esportazione guidata SQL Server).</span><span class="sxs-lookup"><span data-stu-id="9e42e-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e42e-160">Passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="9e42e-160">Next Steps:</span></span>

[<span data-ttu-id="9e42e-161">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9e42e-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="9e42e-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e42e-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

