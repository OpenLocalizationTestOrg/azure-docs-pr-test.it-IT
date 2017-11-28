---
title: Desktop remoto con i ruoli Azure aaaUsing | Documenti Microsoft
description: Utilizzo di Desktop remoto con i ruoli Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="95a64-103">Utilizzo di Desktop remoto con i ruoli Azure</span><span class="sxs-lookup"><span data-stu-id="95a64-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="95a64-104">Tramite hello Azure SDK e Servizi Desktop remoto, è possibile accedere a ruoli di Azure e macchine virtuali ospitate da Azure.</span><span class="sxs-lookup"><span data-stu-id="95a64-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="95a64-105">In Visual Studio è possibile configurare Servizi Desktop remoto da un progetto del servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="95a64-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="95a64-106">tooenable di Servizi Desktop remoto, è necessario creare un progetto che contiene uno o più ruoli di lavoro e quindi pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="95a64-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a64-107">Accedere a un ruolo di Azure solo per la risoluzione dei problemi o lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="95a64-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="95a64-108">Salve a scopo di ogni macchina virtuale è un ruolo specifico nell'applicazione Azure, non toorun toorun altre applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="95a64-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="95a64-109">Se si desidera toouse toohost Azure una macchina virtuale che è possibile utilizzare per qualsiasi scopo, vedere l'accesso a macchine virtuali di Azure da Esplora Server.</span><span class="sxs-lookup"><span data-stu-id="95a64-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="95a64-110">tooenable e utilizzare Desktop remoto per un ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="95a64-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="95a64-111">In Esplora soluzioni, aprire il menu di scelta rapida hello per il progetto servizio cloud e quindi scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="95a64-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="95a64-112">Hello **pubblica l'applicazione Azure** procedura guidata viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="95a64-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Comando per la pubblicazione di un progetto di servizio cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="95a64-114">Nella parte inferiore di hello del **impostazioni di pubblicazione di Microsoft Azure** pagina della procedura guidata hello, seleziona hello **Abilita Desktop remoto** per la casella di controllo di tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="95a64-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="95a64-115">Hello **configurazione Desktop remoto** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="95a64-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="95a64-116">Nella parte inferiore di hello di hello **configurazione Desktop remoto** finestra di dialogo scegliere hello **altre opzioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95a64-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="95a64-117">Verrà visualizzato un elenco a discesa che consente di creare o scegliere un certificato in modo che sia possibile crittografare le informazioni sulle credenziali per la connessione tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="95a64-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="95a64-118">Nell'elenco a discesa hello scegliere  **&lt;Crea >**, o sceglierne uno esistente dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="95a64-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="95a64-119">Se si sceglie un certificato esistente, ignorare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="95a64-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95a64-120">i certificati di Hello necessari per una connessione desktop remoto sono diversi da quelli di hello utilizzato per altre operazioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="95a64-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="95a64-121">certificato di accesso remoto di Hello deve avere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="95a64-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="95a64-122">Hello **Create Certificate** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="95a64-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="95a64-123">Specificare un nome descrittivo per il nuovo certificato di hello e quindi scegliere hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95a64-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="95a64-124">Hello nuovo certificato viene visualizzato nella casella di riepilogo a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="95a64-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="95a64-125">In hello **configurazione Desktop remoto** finestra di dialogo, fornire un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="95a64-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="95a64-126">Non è possibile usare un account esistente.</span><span class="sxs-lookup"><span data-stu-id="95a64-126">You can’t use an existing account.</span></span> <span data-ttu-id="95a64-127">Non specificare l'amministratore come nome utente hello per il nuovo account di hello.</span><span class="sxs-lookup"><span data-stu-id="95a64-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="95a64-128">Se la password di hello non soddisfa i requisiti di complessità hello, casella di testo password toohello successiva un'icona rossa.</span><span class="sxs-lookup"><span data-stu-id="95a64-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="95a64-129">la password di Hello debba includere lettere maiuscole, lettere minuscole e i numeri o simboli.</span><span class="sxs-lookup"><span data-stu-id="95a64-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="95a64-130">Scegliere una data di scadenza account hello e dopo che le connessioni desktop remoto verranno bloccate.</span><span class="sxs-lookup"><span data-stu-id="95a64-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="95a64-131">Dopo aver fornito tutti hello le informazioni necessarie, scegliere hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95a64-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="95a64-132">Diverse impostazioni che abilitano i servizi di accesso remoto vengono aggiunti i file con estensione cscfg e csdef toohello.</span><span class="sxs-lookup"><span data-stu-id="95a64-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="95a64-133">In hello **impostazioni di pubblicazione di Microsoft Azure** procedura guidata, scegliere hello **OK** quando si è pronti a toopublish il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="95a64-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="95a64-134">Se non si è pronti toopublish, scegliere hello **Annulla** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95a64-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="95a64-135">salvataggio delle impostazioni di configurazione Hello ed è possibile pubblicare il servizio cloud in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="95a64-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="95a64-136">Connettersi tooan ruolo Azure tramite Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="95a64-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="95a64-137">Dopo aver pubblicato il servizio cloud in Azure, è possibile utilizzare toolog Esplora Server in macchine virtuali hello ospitata da Azure.</span><span class="sxs-lookup"><span data-stu-id="95a64-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="95a64-138">In Esplora Server espandere hello **Azure** nodo, quindi espandere il nodo hello di un servizio cloud e uno dei relativi toodisplay ruoli un elenco di istanze.</span><span class="sxs-lookup"><span data-stu-id="95a64-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="95a64-139">Aprire il menu di scelta rapida hello per un nodo dell'istanza e quindi scegliere **connessione tramite Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="95a64-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Connessione tramite Desktop remoto](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="95a64-141">Immettere nome utente hello e la password creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="95a64-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="95a64-142">L'accesso alla sessione remota è stato completato.</span><span class="sxs-lookup"><span data-stu-id="95a64-142">You are now logged into your remote session.</span></span>

