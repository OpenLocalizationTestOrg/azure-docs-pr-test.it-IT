---
title: Utilizzo di Desktop remoto con i ruoli Azure | Documentazione Microsoft
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
ms.openlocfilehash: eab135d10c0d6df8ca72ac47d6804017a998a3d2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="26906-103">Utilizzo di Desktop remoto con i ruoli Azure</span><span class="sxs-lookup"><span data-stu-id="26906-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="26906-104">Usando Azure SDK e Servizi Desktop remoto, è possibile accedere ai ruoli di Azure e alle macchine virtuali ospitate da Azure.</span><span class="sxs-lookup"><span data-stu-id="26906-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="26906-105">In Visual Studio è possibile configurare Servizi Desktop remoto da un progetto del servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="26906-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="26906-106">Per abilitare Servizi Desktop remoto, è necessario creare un progetto di lavoro contenente uno o più ruoli e quindi pubblicarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="26906-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26906-107">Accedere a un ruolo di Azure solo per la risoluzione dei problemi o lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="26906-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="26906-108">Lo scopo di ogni macchina virtuale è eseguire un ruolo specifico nell'applicazione di Azure e non eseguire altre applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="26906-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span></span> <span data-ttu-id="26906-109">Se si vuole usare Azure per ospitare una macchina virtuale che è possibile usare per qualsiasi scopo, vedere Accesso alle macchine virtuali di Azure da Esplora server.</span><span class="sxs-lookup"><span data-stu-id="26906-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="26906-110">Per abilitare e usare Desktop remoto per un ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="26906-110">To enable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="26906-111">In Esplora soluzioni aprire il menu di scelta rapida per il progetto del servizio cloud e quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="26906-111">In Solution Explorer, open the shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="26906-112">Verrà visualizzata la procedura guidata **Pubblica l'applicazione Azure** .</span><span class="sxs-lookup"><span data-stu-id="26906-112">The **Publish Azure Application** wizard appears.</span></span>
   
    ![Comando per la pubblicazione di un progetto di servizio cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="26906-114">Nella parte inferiore della pagina **Impostazioni di pubblicazione di Microsoft Azure** della procedura guidata selezionare la casella di controllo **Abilita Desktop remoto per tutti i ruoli**.</span><span class="sxs-lookup"><span data-stu-id="26906-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="26906-115">Verrà visualizzata la finestra di dialogo **Configurazione Desktop remoto** .</span><span class="sxs-lookup"><span data-stu-id="26906-115">The **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="26906-116">Nella parte inferiore della finestra di dialogo **Configurazione Desktop remoto** scegliere il pulsante **Altre opzioni**.</span><span class="sxs-lookup"><span data-stu-id="26906-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span></span> 
   
    <span data-ttu-id="26906-117">Verrà visualizzato un elenco a discesa che consente di creare o scegliere un certificato in modo che sia possibile crittografare le informazioni sulle credenziali per la connessione tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="26906-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="26906-118">Nell'elenco a discesa scegliere **&lt;Crea>** o un certificato esistente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="26906-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span></span> 
   
    <span data-ttu-id="26906-119">Se si sceglie un certificato esistente, ignorare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="26906-119">If you choose an existing certificate, skip the following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26906-120">I certificati necessari per una connessione Desktop remoto sono diversi da quelli usati per altre operazioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="26906-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span></span> <span data-ttu-id="26906-121">Il certificato di accesso remoto deve avere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="26906-121">The remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="26906-122">Verrà visualizzata la finestra di dialogo **Crea certificato** .</span><span class="sxs-lookup"><span data-stu-id="26906-122">The **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="26906-123">Specificare un nome descrittivo per il nuovo certificato e quindi scegliere il pulsante **OK** .</span><span class="sxs-lookup"><span data-stu-id="26906-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span></span> <span data-ttu-id="26906-124">Il nuovo certificato verrà visualizzato nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="26906-124">The new certificate appears in the dropdown list box.</span></span>
   2. <span data-ttu-id="26906-125">Nella finestra di dialogo **Configurazione Desktop remoto** , specificare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="26906-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="26906-126">Non è possibile usare un account esistente.</span><span class="sxs-lookup"><span data-stu-id="26906-126">You can’t use an existing account.</span></span> <span data-ttu-id="26906-127">Non specificare l'amministratore come nome utente per il nuovo account.</span><span class="sxs-lookup"><span data-stu-id="26906-127">Don’t specify Administrator as the user name for the new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="26906-128">Se la password non soddisfa i requisiti di complessità necessari, accanto alla casella di testo della password viene visualizzata un'icona rossa.</span><span class="sxs-lookup"><span data-stu-id="26906-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span></span> <span data-ttu-id="26906-129">La password deve includere lettere maiuscole e minuscole, numeri o simboli.</span><span class="sxs-lookup"><span data-stu-id="26906-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="26906-130">Scegliere una data di scadenza dell'account, dopo la quale le connessioni Desktop remoto verranno bloccate.</span><span class="sxs-lookup"><span data-stu-id="26906-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="26906-131">Dopo aver fornito tutte le informazioni necessarie, scegliere il pulsante **OK** .</span><span class="sxs-lookup"><span data-stu-id="26906-131">After you've provided all the required information, choose the **OK** button.</span></span>
      
       <span data-ttu-id="26906-132">Verranno aggiunte diverse impostazioni che abilitano i servizi di accesso remoto ai file con estensione cscfg e csdef.</span><span class="sxs-lookup"><span data-stu-id="26906-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="26906-133">Nella procedura guidata **Impostazioni di pubblicazione Microsoft Azure** scegliere il pulsante **OK** quando si è pronti a pubblicare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="26906-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span></span>
   
    <span data-ttu-id="26906-134">Se non si è ancora pronti, premere il pulsante **Annulla** .</span><span class="sxs-lookup"><span data-stu-id="26906-134">If you're not ready to publish, choose the **Cancel** button.</span></span> <span data-ttu-id="26906-135">Le impostazioni di configurazione vengono salvate ed è possibile pubblicare il servizio cloud in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="26906-135">The configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="26906-136">Connettersi a un ruolo di Azure tramite Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="26906-136">Connect to an Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="26906-137">Dopo aver pubblicato il servizio cloud in Azure, è possibile usare Esplora Server per accedere alle macchine virtuali ospitate da Azure.</span><span class="sxs-lookup"><span data-stu-id="26906-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="26906-138">In Esplora server espandere il nodo **Azure** e quindi espandere il nodo di un servizio cloud e uno dei relativi ruoli per visualizzare un elenco di istanze.</span><span class="sxs-lookup"><span data-stu-id="26906-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>
2. <span data-ttu-id="26906-139">Aprire il menu di scelta rapida di un nodo dell'istanza e quindi scegliere **Connessione tramite desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="26906-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Connessione tramite Desktop remoto](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="26906-141">Immettere il nome utente e la password creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="26906-141">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="26906-142">L'accesso alla sessione remota è stato completato.</span><span class="sxs-lookup"><span data-stu-id="26906-142">You are now logged into your remote session.</span></span>

