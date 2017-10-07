---
title: Azure Analysis Services aaaManage | Documenti Microsoft
description: Informazioni su come toomanage un Analysis Services server in Azure.
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
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="146c6-103">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="146c6-103">Manage Analysis Services</span></span>
<span data-ttu-id="146c6-104">Dopo aver creato un server Analysis Services in Azure, vi possono essere alcune attività di gestione e amministrazione è necessario tooperform immediatamente o verso il basso un po' hello strada.</span><span class="sxs-lookup"><span data-stu-id="146c6-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="146c6-105">Ad esempio, eseguire l'elaborazione dei dati di aggiornamento toohello, controllare chi può accedere ai modelli di hello del server o monitorare l'integrità del server.</span><span class="sxs-lookup"><span data-stu-id="146c6-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="146c6-106">Alcune attività di gestione possono essere eseguite solo nel portale di Azure, altre in SQL Server Management Studio (SSMS) e altre ancora possono essere eseguite in entrambi gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="146c6-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="146c6-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="146c6-107">Azure portal</span></span>
<span data-ttu-id="146c6-108">[Portale di Azure](http://portal.azure.com/) è in cui è possibile creare ed eliminare i server, monitoraggio delle risorse di server, modificare dimensioni e gestire chi ha accesso tooyour server.</span><span class="sxs-lookup"><span data-stu-id="146c6-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="146c6-109">Se si verificano problemi, è inoltre possibile inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="146c6-109">If you're having some problems, you can also submit a support request.</span></span>

![Ottenere il nome del server in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="146c6-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="146c6-111">SQL Server Management Studio</span></span>
<span data-ttu-id="146c6-112">Connessione server tooyour in Azure è simile a connessione tooa istanza del server dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="146c6-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="146c6-113">Da SQL Server Management Studio, è possibile eseguire molte delle hello stessa attività, ad esempio l'elaborazione dei dati o creare uno script di elaborazione, la gestione dei ruoli e utilizzare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="146c6-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="146c6-115">Scaricare e installare SSMS</span><span class="sxs-lookup"><span data-stu-id="146c6-115">Download and install SSMS</span></span>
<span data-ttu-id="146c6-116">tooget tutti hello funzionalità più recenti e più esperienza di hello quando ci si connette il server di Azure Analysis Services tooyour, assicurarsi che si utilizza una versione più recente di hello di SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="146c6-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="146c6-117">[Scaricare SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="146c6-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="146c6-118">tooconnect con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="146c6-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="146c6-119">Quando si utilizza SQL Server Management Studio, prima della connessione messaggi hello del server tooyour prima volta, assicurarsi che il nome utente è incluso nel gruppo di amministratori di Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="146c6-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="146c6-120">vedere, più toolearn [gli amministratori del Server](#server-administrators) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="146c6-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="146c6-121">Prima di connettersi, è necessario il nome di server hello tooget.</span><span class="sxs-lookup"><span data-stu-id="146c6-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="146c6-122">In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server hello copia.</span><span class="sxs-lookup"><span data-stu-id="146c6-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="146c6-124">In SSMS > **Esplora oggetti** fare clic su **Connetti** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="146c6-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="146c6-125">In hello **connettersi tooServer** nella finestra di dialogo Incolla in nome server hello, quindi in **autenticazione**, scegliere uno dei seguenti tipi di autenticazione hello:</span><span class="sxs-lookup"><span data-stu-id="146c6-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="146c6-126">**L'autenticazione di Windows** toouse le credenziali di dominio omeutente e la password di Windows.</span><span class="sxs-lookup"><span data-stu-id="146c6-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="146c6-127">**L'autenticazione di Password di Active Directory** toouse un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="146c6-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="146c6-128">Ad esempio, per la connessione da un computer non incluso nel dominio.</span><span class="sxs-lookup"><span data-stu-id="146c6-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="146c6-129">**Autenticazione universale di Active Directory** toouse [interattivo o multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="146c6-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Connessione in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="146c6-131">Amministratori del server e utenti del database</span><span class="sxs-lookup"><span data-stu-id="146c6-131">Server administrators and database users</span></span>
<span data-ttu-id="146c6-132">In Azure Analysis Services ci sono due tipi di utenti, gli amministratori del server e gli utenti del database.</span><span class="sxs-lookup"><span data-stu-id="146c6-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="146c6-133">Entrambi i tipi di utenti devono essere in Azure Active Directory ed essere specificati dal nome UPN o dall'indirizzo di posta elettronica dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="146c6-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="146c6-134">vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="146c6-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="146c6-135">Risoluzione dei problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="146c6-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="146c6-136">Quando ci si connette tramite SSMS, se si verificano problemi, potrebbe essere necessario cache di account di accesso tooclear hello.</span><span class="sxs-lookup"><span data-stu-id="146c6-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="146c6-137">Non è toodisc memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="146c6-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="146c6-138">cache hello tooclear, chiudere e riavviare hello connettere processo.</span><span class="sxs-lookup"><span data-stu-id="146c6-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="146c6-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="146c6-139">Next steps</span></span>
<span data-ttu-id="146c6-140">Se è già stato ancora distribuito un nuovo server tooyour di modello tabulare, ora è il momento opportuno.</span><span class="sxs-lookup"><span data-stu-id="146c6-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="146c6-141">vedere, più toolearn [distribuire tooAzure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="146c6-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="146c6-142">Se è già distribuito un server tooyour modello, si è pronti tooconnect tooit utilizzando un client o browser.</span><span class="sxs-lookup"><span data-stu-id="146c6-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="146c6-143">vedere, più toolearn [ottenere dati dal server Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="146c6-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

