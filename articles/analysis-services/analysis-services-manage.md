---
title: Gestire Azure Analysis Services | Documentazione Microsoft
description: Informazioni su come gestire un server di Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="0adda-103">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0adda-103">Manage Analysis Services</span></span>
<span data-ttu-id="0adda-104">Dopo aver creato un server Analysis Services in Azure, potrà essere necessario eseguire alcune attività di amministrazione e gestione immediatamente o dopo un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="0adda-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="0adda-105">Ad esempio, eseguire l'elaborazione per i dati di aggiornamento, controllare quali utenti possono accedere ai modelli nel server o monitorare l'integrità del server.</span><span class="sxs-lookup"><span data-stu-id="0adda-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="0adda-106">Alcune attività di gestione possono essere eseguite solo nel portale di Azure, altre in SQL Server Management Studio (SSMS) e altre ancora possono essere eseguite in entrambi gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="0adda-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="0adda-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0adda-107">Azure portal</span></span>
<span data-ttu-id="0adda-108">Nel [portale di Azure](http://portal.azure.com/) è possibile creare ed eliminare i server, monitorare le risorse del server, modificare le dimensioni e gestire chi ha accesso ai server.</span><span class="sxs-lookup"><span data-stu-id="0adda-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="0adda-109">Se si verificano problemi, è inoltre possibile inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="0adda-109">If you're having some problems, you can also submit a support request.</span></span>

![Ottenere il nome del server in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="0adda-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0adda-111">SQL Server Management Studio</span></span>
<span data-ttu-id="0adda-112">La connessione al server in Azure è un'attività analoga alla connessione a un'istanza del server all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0adda-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="0adda-113">Da SSMS, è possibile eseguire molte delle attività, ad esempio elaborare i dati o creare uno script di elaborazione, gestire i ruoli e usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0adda-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="0adda-115">Scaricare e installare SSMS</span><span class="sxs-lookup"><span data-stu-id="0adda-115">Download and install SSMS</span></span>
<span data-ttu-id="0adda-116">Per ottenere tutte le funzionalità più recenti e un'esperienza ottimale quando ci si connette al server di Azure Analysis Services, assicurarsi di usare la versione più recente di SSMS.</span><span class="sxs-lookup"><span data-stu-id="0adda-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="0adda-117">[Scaricare SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="0adda-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="0adda-118">Per connettersi con SSMS</span><span class="sxs-lookup"><span data-stu-id="0adda-118">To connect with SSMS</span></span>
 <span data-ttu-id="0adda-119">Quando si usa SSMS, prima di connettersi al server la prima volta assicurarsi che il nome utente è incluso nel gruppo di amministratori di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="0adda-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="0adda-120">Per altre informazioni, vedere la sezione [Amministratori del server](#server-administrators) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="0adda-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="0adda-121">Prima di connettersi, è necessario ottenere il nome del server.</span><span class="sxs-lookup"><span data-stu-id="0adda-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="0adda-122">In **portale di Azure** > server > **Panoramica** > **Nome server** copiare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="0adda-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="0adda-124">In SSMS > **Esplora oggetti** fare clic su **Connetti** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="0adda-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="0adda-125">Nella finestra di dialogo **Connetti al server** incollare il nome del server e quindi in **Autenticazione** scegliere uno dei tipi di autenticazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="0adda-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="0adda-126">**Autenticazione di Windows** per usare le credenziali di dominio\nome utente e password di Windows.</span><span class="sxs-lookup"><span data-stu-id="0adda-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="0adda-127">**Autenticazione della password Active Directory** per usare un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="0adda-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="0adda-128">Ad esempio, per la connessione da un computer non incluso nel dominio.</span><span class="sxs-lookup"><span data-stu-id="0adda-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="0adda-129">**Autenticazione universale di Active Directory** per usare [l'autenticazione non interattiva o multi-factor](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0adda-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Connessione in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="0adda-131">Amministratori del server e utenti del database</span><span class="sxs-lookup"><span data-stu-id="0adda-131">Server administrators and database users</span></span>
<span data-ttu-id="0adda-132">In Azure Analysis Services ci sono due tipi di utenti, gli amministratori del server e gli utenti del database.</span><span class="sxs-lookup"><span data-stu-id="0adda-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="0adda-133">Entrambi i tipi di utenti devono essere in Azure Active Directory ed essere specificati dal nome UPN o dall'indirizzo di posta elettronica dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0adda-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="0adda-134">Per altre informazioni, vedere [Autenticazione e autorizzazioni utente](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="0adda-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="0adda-135">Risoluzione dei problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="0adda-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="0adda-136">Quando ci si connette tramite SSMS, se si riscontra un problema, potrebbe essere necessario cancellare la cache di accesso.</span><span class="sxs-lookup"><span data-stu-id="0adda-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="0adda-137">Non viene memorizzato nulla nella cache su disco. Per cancellare la cache, chiudere e riavviare il processo di connessione.</span><span class="sxs-lookup"><span data-stu-id="0adda-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0adda-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0adda-138">Next steps</span></span>
<span data-ttu-id="0adda-139">Se non è mai stato distribuito un modello tabulare nel nuovo server, questo è il momento migliore.</span><span class="sxs-lookup"><span data-stu-id="0adda-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="0adda-140">Per altre informazioni, vedere [Distribuire in Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0adda-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="0adda-141">Se un modello è stato distribuito nel server, si è pronti per connettersi a tale server tramite un client o un browser.</span><span class="sxs-lookup"><span data-stu-id="0adda-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="0adda-142">Per altre informazioni, vedere [Get data from Azure Analysis Services server](analysis-services-connect.md) (Ottenere dati dal server Azure Analysis Services).</span><span class="sxs-lookup"><span data-stu-id="0adda-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

