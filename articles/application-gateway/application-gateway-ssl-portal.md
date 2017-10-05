---
title: Configurare l'offload SSL - Gateway applicazione di Azure - Portale di Azure | Documentazione Microsoft
description: Questa pagina contiene istruzioni per creare un gateway applicazione con offload SSL usando il portale
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="dea0c-103">Configurare un gateway applicazione per l'offload SSL con il portale</span><span class="sxs-lookup"><span data-stu-id="dea0c-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dea0c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dea0c-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="dea0c-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dea0c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="dea0c-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="dea0c-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="dea0c-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dea0c-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="dea0c-108">Il gateway applicazione di Azure può essere configurato per terminare la sessione Secure Sockets Layer (SSL) nel gateway ed evitare costose attività di decrittografia SSL nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="dea0c-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="dea0c-109">L'offload SSL semplifica anche la configurazione e la gestione del server front-end dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="dea0c-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="dea0c-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="dea0c-110">Scenario</span></span>

<span data-ttu-id="dea0c-111">Lo scenario seguente illustra la configurazione dell'offload SSL in un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="dea0c-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="dea0c-112">Lo scenario presuppone che sia già stata seguita la procedura per [creare un gateway applicazione](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dea0c-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dea0c-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="dea0c-113">Before you begin</span></span>

<span data-ttu-id="dea0c-114">Per configurare l'offload SSL con un gateway applicazione, è necessario un certificato,</span><span class="sxs-lookup"><span data-stu-id="dea0c-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="dea0c-115">che viene caricato nel gateway applicazione e viene usato per crittografare e decrittografare il traffico inviato tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="dea0c-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="dea0c-116">Il certificato deve essere in formato PFX (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="dea0c-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="dea0c-117">Questo formato di file consente l'esportazione della chiave privata necessaria al gateway applicazione per eseguire la crittografia e la decrittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="dea0c-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="dea0c-118">Aggiungere un listener HTTPS</span><span class="sxs-lookup"><span data-stu-id="dea0c-118">Add an HTTPS listener</span></span>

<span data-ttu-id="dea0c-119">Il listener HTTPS cerca il traffico in base alla relativa configurazione e consente di instradare il traffico ai pool back-end.</span><span class="sxs-lookup"><span data-stu-id="dea0c-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="dea0c-120">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="dea0c-120">Step 1</span></span>

<span data-ttu-id="dea0c-121">Passare al portale di Azure e selezionare un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="dea0c-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="dea0c-122">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="dea0c-122">Step 2</span></span>

<span data-ttu-id="dea0c-123">Fare clic su Listener e quindi sul pulsante Aggiungi per aggiungere un listener.</span><span class="sxs-lookup"><span data-stu-id="dea0c-123">Click Listeners and click the Add button to add a listener.</span></span>

![Pannello di panoramica del gateway applicazione][1]

### <a name="step-3"></a><span data-ttu-id="dea0c-125">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="dea0c-125">Step 3</span></span>

<span data-ttu-id="dea0c-126">Inserire le informazioni necessarie per il listener e caricare il certificato PFX. Al termine, fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="dea0c-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="dea0c-127">**Nome** : questo valore è un nome descrittivo del listener.</span><span class="sxs-lookup"><span data-stu-id="dea0c-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="dea0c-128">**Configurazione IP front-end** : questo valore è la configurazione IP front-end usata per il listener.</span><span class="sxs-lookup"><span data-stu-id="dea0c-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="dea0c-129">**Porta front-end (Nome/Porta)** : nome descrittivo della porta usata nel front-end del gateway applicazione e porta effettiva usata.</span><span class="sxs-lookup"><span data-stu-id="dea0c-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="dea0c-130">**Protocollo** : opzione che consente di determinare se usare HTTPS o HTTP per il front-end.</span><span class="sxs-lookup"><span data-stu-id="dea0c-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="dea0c-131">**Certificato (Nome/Password)** : se si usa l'offload SSL, per questa impostazione sono necessari un certificato PFX, un nome descrittivo e una password.</span><span class="sxs-lookup"><span data-stu-id="dea0c-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Pannello Aggiungi listener][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="dea0c-133">Creare una regola e associarla al listener</span><span class="sxs-lookup"><span data-stu-id="dea0c-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="dea0c-134">Ora che il listener è stato creato,</span><span class="sxs-lookup"><span data-stu-id="dea0c-134">The listener has now been created.</span></span> <span data-ttu-id="dea0c-135">è necessario creare una regola per gestire il traffico dal listener.</span><span class="sxs-lookup"><span data-stu-id="dea0c-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="dea0c-136">Le regole definiscono in che modo il traffico viene indirizzato ai pool back-end sulla base di varie impostazioni di configurazione, tra cui se viene usata l'affinità di sessione basata su cookie, nonché il protocollo, la porta e i probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="dea0c-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="dea0c-137">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="dea0c-137">Step 1</span></span>

<span data-ttu-id="dea0c-138">Fare clic su **Regole** nel gateway applicazione e quindi su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="dea0c-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![Pannello delle regole del gateway applicazione][3]

### <a name="step-2"></a><span data-ttu-id="dea0c-140">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="dea0c-140">Step 2</span></span>

<span data-ttu-id="dea0c-141">Nel pannello **Aggiungi regola di base** digitare il nome descrittivo della regola e scegliere il listener creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="dea0c-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="dea0c-142">Scegliere il pool back-end e l'impostazione HTTP appropriati e fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="dea0c-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![Finestra delle impostazioni HTTP][4]

<span data-ttu-id="dea0c-144">Le impostazioni vengono così salvate nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="dea0c-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="dea0c-145">Il processo di salvataggio di queste impostazioni può richiedere tempo e le impostazioni potrebbero non essere immediatamente visualizzabili tramite il portale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dea0c-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="dea0c-146">Al termine del salvataggio, il gateway applicazione gestisce la crittografia e la decrittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="dea0c-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="dea0c-147">Tutto il traffico tra il gateway applicazione e i server Web back-end verrà gestito su HTTP.</span><span class="sxs-lookup"><span data-stu-id="dea0c-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="dea0c-148">Tutte le comunicazioni verso il client, se avviate su HTTPS, verranno restituite al client crittografate.</span><span class="sxs-lookup"><span data-stu-id="dea0c-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dea0c-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dea0c-149">Next steps</span></span>

<span data-ttu-id="dea0c-150">Per informazioni su come configurare un probe di integrità personalizzato con un gateway applicazione di Azure, vedere [Creare un gateway applicazione con il portale](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dea0c-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
