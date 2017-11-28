---
title: gateway dati locale di aaaInstall | Documenti Microsoft
description: Informazioni su come tooinstall e configurare un gateway dati locale.
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
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="34cc9-103">Installare e configurare un gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="34cc9-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="34cc9-104">Un gateway dati locale è obbligatorio quando hello di uno o più server Azure Analysis Services nella stessa area connettersi a origini dati locali tooon.</span><span class="sxs-lookup"><span data-stu-id="34cc9-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="34cc9-105">toolearn ulteriori informazioni sui gateway hello, vedere [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="34cc9-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34cc9-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="34cc9-106">Prerequisites</span></span>
<span data-ttu-id="34cc9-107">**Requisiti minimi:**</span><span class="sxs-lookup"><span data-stu-id="34cc9-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="34cc9-108">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="34cc9-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="34cc9-109">Versione a 64 bit di Windows 7 o Windows Server 2008 R2 (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="34cc9-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="34cc9-110">**Consigliato:**</span><span class="sxs-lookup"><span data-stu-id="34cc9-110">**Recommended:**</span></span>

* <span data-ttu-id="34cc9-111">8 CPU core</span><span class="sxs-lookup"><span data-stu-id="34cc9-111">8 Core CPU</span></span>
* <span data-ttu-id="34cc9-112">8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="34cc9-112">8 GB Memory</span></span>
* <span data-ttu-id="34cc9-113">Windows 2012 R2 versione a 64 bit (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="34cc9-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="34cc9-114">**Considerazioni importanti:**</span><span class="sxs-lookup"><span data-stu-id="34cc9-114">**Important considerations:**</span></span>

* <span data-ttu-id="34cc9-115">Durante l'installazione, quando si registra il gateway con Azure, è selezionata l'area predefinita hello per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="34cc9-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="34cc9-116">È possibile scegliere un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="34cc9-116">You can choose a different region.</span></span> <span data-ttu-id="34cc9-117">Se si dispone di server in più aree, è necessario installare un gateway per ogni area.</span><span class="sxs-lookup"><span data-stu-id="34cc9-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="34cc9-118">Impossibile installare il gateway Hello in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="34cc9-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="34cc9-119">In un singolo computer può essere installato un solo gateway.</span><span class="sxs-lookup"><span data-stu-id="34cc9-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="34cc9-120">Installare il gateway di hello in un computer che rimanga nel e non va toosleep.</span><span class="sxs-lookup"><span data-stu-id="34cc9-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="34cc9-121">Non installare il gateway hello in una rete di computer in modalità wireless connesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="34cc9-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="34cc9-122">È infatti possibile che si verifichi un calo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="34cc9-122">Performance can be diminished.</span></span>


## <span data-ttu-id="34cc9-123"><a name="download"></a>Scaricare</span><span class="sxs-lookup"><span data-stu-id="34cc9-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="34cc9-124">Scaricare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="34cc9-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="34cc9-125"><a name="install"></a>Installare</span><span class="sxs-lookup"><span data-stu-id="34cc9-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="34cc9-126">Eseguire l'installazione.</span><span class="sxs-lookup"><span data-stu-id="34cc9-126">Run setup.</span></span>

2. <span data-ttu-id="34cc9-127">Selezionare un percorso, accettare le condizioni di hello e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Percorso di installazione e condizioni di licenza](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="34cc9-129">Selezionare **Gateway dati locale (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="34cc9-130">Azure Analysis Services non supporta la modalità personale.</span><span class="sxs-lookup"><span data-stu-id="34cc9-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Scelta del tipo di gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="34cc9-132">Immettere un account toosign tooAzure.</span><span class="sxs-lookup"><span data-stu-id="34cc9-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="34cc9-133">Hello account deve essere del tenant Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="34cc9-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="34cc9-134">Questo account viene utilizzato per l'amministratore del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-134">This account is used for hello gateway administrator.</span></span> 

   ![Immettere un account toosign in tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="34cc9-136">Se si accede con un account di dominio, sarà eseguito il mapping di account aziendale tooyour in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34cc9-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="34cc9-137">Verrà utilizzato l'account aziendale come amministratore del gateway hello hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="34cc9-138"><a name="register"></a>Registrare</span><span class="sxs-lookup"><span data-stu-id="34cc9-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="34cc9-139">In ordine toocreate una risorsa per il gateway in Azure, è necessario registrare l'istanza locale di hello che è stato installato con il servizio Cloud Gateway hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="34cc9-140">Selezionare l'opzione **Consente di registrare un nuovo gateway in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registra](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="34cc9-142">Digitare un nome e la chiave di ripristino per il gateway.</span><span class="sxs-lookup"><span data-stu-id="34cc9-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="34cc9-143">Per impostazione predefinita, il gateway di hello utilizza area predefinita della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="34cc9-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="34cc9-144">Se è necessario tooselect un'area diversa, selezionare **area Modifica**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Registra](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="34cc9-146"><a name="create-resource"></a>Creare una risorsa per il gateway di Azure</span><span class="sxs-lookup"><span data-stu-id="34cc9-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="34cc9-147">Dopo aver installato e registrato il gateway, è necessario toocreate una risorsa di gateway nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="34cc9-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="34cc9-148">Accedi tooAzure con hello stesso account usato durante la registrazione gateway hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="34cc9-149">Nel portale di Azure fare clic su **Crea un nuovo servizio** > **Integrazione aziendale**  > **Gateway dati locale** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Creazione di una risorsa per il gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="34cc9-151">In **Crea gateway di connessione**, immettere queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="34cc9-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="34cc9-152">**Nome**: inserire un nome per la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="34cc9-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="34cc9-153">**Sottoscrizione**: selezionare hello tooassociate sottoscrizione di Azure alla risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="34cc9-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="34cc9-154">La sottoscrizione deve essere il server si trovano nella stessa sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="34cc9-155">sottoscrizione predefinita Hello è basata su account di Azure utilizzato toosign in hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="34cc9-156">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="34cc9-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="34cc9-157">**Percorso**: area hello selezionare il gateway è stato registrato.</span><span class="sxs-lookup"><span data-stu-id="34cc9-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="34cc9-158">**Nome di installazione**: se l'installazione del gateway non è già selezionata, selezionare hello registrato.</span><span class="sxs-lookup"><span data-stu-id="34cc9-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="34cc9-159">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="34cc9-160"><a name="connect-servers"></a>Connettere i server toohello gateway</span><span class="sxs-lookup"><span data-stu-id="34cc9-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="34cc9-161">Nella panoramica del server Azure Analysis Services fare clic su **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Connessione server toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="34cc9-163">In **Pick tooconnect un Gateway dati locale**, selezionare la risorsa del gateway e quindi fare clic su **gateway selezionato Connetti**.</span><span class="sxs-lookup"><span data-stu-id="34cc9-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Connettere toogateway server](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="34cc9-165">Se il gateway non compare nell'elenco di hello, il server è probabile che non nella stessa area come area hello è specificato durante la registrazione gateway hello hello.</span><span class="sxs-lookup"><span data-stu-id="34cc9-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="34cc9-166">È tutto.</span><span class="sxs-lookup"><span data-stu-id="34cc9-166">That's it.</span></span> <span data-ttu-id="34cc9-167">Se si necessita di porte tooopen o eseguire attività di risoluzione, essere certi toocheck out [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="34cc9-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34cc9-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34cc9-168">Next steps</span></span>
* [<span data-ttu-id="34cc9-169">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="34cc9-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="34cc9-170">Ottenere dati da Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="34cc9-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
