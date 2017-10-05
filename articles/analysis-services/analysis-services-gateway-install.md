---
title: Installare il gateway dati locale | Microsoft Docs
description: Informazioni su come installare e configurare un gateway dati locale.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="8b09d-103">Installare e configurare un gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="8b09d-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="8b09d-104">Quando uno o più server Azure Analysis Services nella stessa area si connettono a origini dati locali, è necessario un gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="8b09d-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="8b09d-105">Per altre informazioni sul gateway, vedere [Gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8b09d-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b09d-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b09d-106">Prerequisites</span></span>
<span data-ttu-id="8b09d-107">**Requisiti minimi:**</span><span class="sxs-lookup"><span data-stu-id="8b09d-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="8b09d-108">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="8b09d-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="8b09d-109">Versione a 64 bit di Windows 7 o Windows Server 2008 R2 (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="8b09d-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="8b09d-110">**Consigliato:**</span><span class="sxs-lookup"><span data-stu-id="8b09d-110">**Recommended:**</span></span>

* <span data-ttu-id="8b09d-111">8 CPU core</span><span class="sxs-lookup"><span data-stu-id="8b09d-111">8 Core CPU</span></span>
* <span data-ttu-id="8b09d-112">8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="8b09d-112">8 GB Memory</span></span>
* <span data-ttu-id="8b09d-113">Windows 2012 R2 versione a 64 bit (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="8b09d-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="8b09d-114">**Considerazioni importanti:**</span><span class="sxs-lookup"><span data-stu-id="8b09d-114">**Important considerations:**</span></span>

* <span data-ttu-id="8b09d-115">Durante l'installazione, quando si registra il gateway con Azure, viene selezionata l'area predefinita per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8b09d-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="8b09d-116">È possibile scegliere un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="8b09d-116">You can choose a different region.</span></span> <span data-ttu-id="8b09d-117">Se si dispone di server in più aree, è necessario installare un gateway per ogni area.</span><span class="sxs-lookup"><span data-stu-id="8b09d-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="8b09d-118">Il gateway non può essere installato in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="8b09d-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="8b09d-119">In un singolo computer può essere installato un solo gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="8b09d-120">Installare il gateway in un computer che rimane attivo e non passa alla modalità di sospensione.</span><span class="sxs-lookup"><span data-stu-id="8b09d-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="8b09d-121">Non installare il gateway in un computer connesso alla rete in modalità wireless.</span><span class="sxs-lookup"><span data-stu-id="8b09d-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="8b09d-122">È infatti possibile che si verifichi un calo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8b09d-122">Performance can be diminished.</span></span>


## <span data-ttu-id="8b09d-123"><a name="download"></a>Download</span><span class="sxs-lookup"><span data-stu-id="8b09d-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="8b09d-124">Scaricare il gateway</span><span class="sxs-lookup"><span data-stu-id="8b09d-124">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="8b09d-125"><a name="install"></a>Installare</span><span class="sxs-lookup"><span data-stu-id="8b09d-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="8b09d-126">Eseguire l'installazione.</span><span class="sxs-lookup"><span data-stu-id="8b09d-126">Run setup.</span></span>

2. <span data-ttu-id="8b09d-127">Selezionare un percorso, accettare le condizioni e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Percorso di installazione e condizioni di licenza](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="8b09d-129">Selezionare **Gateway dati locale (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="8b09d-130">Azure Analysis Services non supporta la modalità personale.</span><span class="sxs-lookup"><span data-stu-id="8b09d-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Scelta del tipo di gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="8b09d-132">Immettere un account per accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="8b09d-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="8b09d-133">L'account deve essere nell'istanza di Microsoft Azure Active Directory del tenant.</span><span class="sxs-lookup"><span data-stu-id="8b09d-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="8b09d-134">Questo account viene usato per l'amministratore del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-134">This account is used for the gateway administrator.</span></span> 

   ![Immissione di un account per accedere ad Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="8b09d-136">Se si accede con un account di dominio, questo verrà mappato all'account aziendale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b09d-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="8b09d-137">L'account aziendale verrà usato come amministratore del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="8b09d-138"><a name="register"></a>Registrare</span><span class="sxs-lookup"><span data-stu-id="8b09d-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="8b09d-139">Per creare una risorsa per il gateway in Azure, è necessario registrare l'istanza locale installata con il servizio cloud gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="8b09d-140">Selezionare l'opzione che **consente di registrare un nuovo gateway in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registra](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="8b09d-142">Digitare un nome e la chiave di ripristino per il gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="8b09d-143">Per impostazione predefinita, il gateway usa l'area predefinita della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8b09d-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="8b09d-144">Se è necessario selezionare un'area diversa, selezionare **Modifica area**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-144">If you need to select a different region, select **Change Region**.</span></span>

   ![Registra](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="8b09d-146"><a name="create-resource"></a>Creare una risorsa per il gateway di Azure</span><span class="sxs-lookup"><span data-stu-id="8b09d-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="8b09d-147">Dopo aver installato e registrato il gateway, è necessario creare una risorsa per il gateway nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b09d-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="8b09d-148">Accedere ad Azure con lo stesso account usato durante la registrazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="8b09d-149">Nel portale di Azure fare clic su **Crea un nuovo servizio** > **Integrazione aziendale**  > **Gateway dati locale** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Creazione di una risorsa per il gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="8b09d-151">In **Crea gateway di connessione**, immettere queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="8b09d-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="8b09d-152">**Nome**: inserire un nome per la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="8b09d-153">**Sottoscrizione**: selezionare la sottoscrizione di Azure da associare alla risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="8b09d-154">La presente sottoscrizione deve essere la medesima in cui si trovano i server.</span><span class="sxs-lookup"><span data-stu-id="8b09d-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="8b09d-155">La sottoscrizione predefinita si basa sull'account di Azure usato per accedere.</span><span class="sxs-lookup"><span data-stu-id="8b09d-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="8b09d-156">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="8b09d-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="8b09d-157">**Percorso**: selezionare l'area in cui è stato registrato il gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="8b09d-158">**Nome installazione**: se l'installazione del gateway non è già selezionata, selezionare il gateway registrato.</span><span class="sxs-lookup"><span data-stu-id="8b09d-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="8b09d-159">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="8b09d-160"><a name="connect-servers"></a>Connettere i server alla risorsa per il gateway</span><span class="sxs-lookup"><span data-stu-id="8b09d-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="8b09d-161">Nella panoramica del server Azure Analysis Services fare clic su **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Connessione del server al gateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="8b09d-163">In **Selezionare un gateway dati locale da connettere** selezionare la risorsa per il gateway e quindi fare clic su **Connetti gateway selezionato**.</span><span class="sxs-lookup"><span data-stu-id="8b09d-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Connessione del server alla risorsa per il gateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="8b09d-165">Se il gateway non viene visualizzato nell'elenco, probabilmente il server non si trova nella stessa area specificata durante la registrazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b09d-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="8b09d-166">È tutto.</span><span class="sxs-lookup"><span data-stu-id="8b09d-166">That's it.</span></span> <span data-ttu-id="8b09d-167">Se è necessario aprire le porte o risolvere eventuali problemi, vedere l'articolo su [Gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8b09d-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b09d-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b09d-168">Next steps</span></span>
* [<span data-ttu-id="8b09d-169">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8b09d-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="8b09d-170">Ottenere dati da Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8b09d-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
