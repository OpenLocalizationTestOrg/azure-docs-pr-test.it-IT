---
title: -Gateway applicazione Azure - portale di Azure di offload SSL aaaConfigure | Documenti Microsoft
description: Questa pagina fornisce un gateway applicazione con SSL offload tramite il portale di hello toocreate di istruzioni
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="80fb2-103">Configurare un gateway applicazione per l'offload SSL tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="80fb2-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="80fb2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="80fb2-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="80fb2-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80fb2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="80fb2-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="80fb2-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="80fb2-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="80fb2-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="80fb2-108">Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="80fb2-109">Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="80fb2-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="80fb2-110">Scenario</span></span>

<span data-ttu-id="80fb2-111">Hello segue scenario passa attraverso la configurazione di offload SSL su un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="80fb2-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="80fb2-112">Hello scenario si presuppone che siano state già seguite passaggi hello troppo[creare un Gateway applicazione](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80fb2-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="80fb2-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="80fb2-113">Before you begin</span></span>

<span data-ttu-id="80fb2-114">offload SSL di tooconfigure con un gateway applicazione, è necessario un certificato.</span><span class="sxs-lookup"><span data-stu-id="80fb2-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="80fb2-115">Questo certificato viene caricato nel gateway applicazione hello e usato tooencrypt e decrittografia il traffico hello inviato tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="80fb2-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="80fb2-116">certificato Hello deve toobe nel formato di scambio di informazioni personali (pfx).</span><span class="sxs-lookup"><span data-stu-id="80fb2-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="80fb2-117">Questo formato di file consente di hello privata toobe chiave esportato richiesto dal hello applicazione gateway tooperform hello crittografia e decrittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="80fb2-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="80fb2-118">Aggiungere un listener HTTPS</span><span class="sxs-lookup"><span data-stu-id="80fb2-118">Add an HTTPS listener</span></span>

<span data-ttu-id="80fb2-119">listener HTTPS Hello Cerca il traffico in base alla relativa configurazione e consente di pool back-end di route hello traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="80fb2-120">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="80fb2-120">Step 1</span></span>

<span data-ttu-id="80fb2-121">Passare toohello portale di Azure e selezionare un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="80fb2-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="80fb2-122">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="80fb2-122">Step 2</span></span>

<span data-ttu-id="80fb2-123">Selezionare i listener hello Aggiungi pulsante tooadd un listener.</span><span class="sxs-lookup"><span data-stu-id="80fb2-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![Pannello di panoramica del gateway applicazione][1]

### <a name="step-3"></a><span data-ttu-id="80fb2-125">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="80fb2-125">Step 3</span></span>

<span data-ttu-id="80fb2-126">Compilare le informazioni necessarie per il listener hello hello e caricamento hello certificato PFX, al termine, fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="80fb2-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="80fb2-127">**Nome** -questo valore è un nome descrittivo del listener hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="80fb2-128">**Configurazione IP Frontend** -questo valore è una configurazione IP front-end del hello che viene utilizzato per il listener hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="80fb2-129">**Porta front-end (nome/porta)** -un nome descrittivo per la porta hello utilizzata nel front-end di hello di gateway applicazione hello e hello effettivo della porta utilizzata.</span><span class="sxs-lookup"><span data-stu-id="80fb2-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="80fb2-130">**Protocollo** -toodetermine un commutatore se viene utilizzato https o http per front-end hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="80fb2-131">**Certificato (Nome/Password)** : se si usa l'offload SSL, per questa impostazione sono necessari un certificato PFX, un nome descrittivo e una password.</span><span class="sxs-lookup"><span data-stu-id="80fb2-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Pannello Aggiungi listener][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="80fb2-133">Creare una regola e associarlo toohello listener</span><span class="sxs-lookup"><span data-stu-id="80fb2-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="80fb2-134">listener Hello è stata creata.</span><span class="sxs-lookup"><span data-stu-id="80fb2-134">hello listener has now been created.</span></span> <span data-ttu-id="80fb2-135">È ora toocreate un traffico di hello toohandle regola dal listener hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="80fb2-136">Le regole definiscono come il traffico è indirizzato toohello pool di back-end in base a più impostazioni di configurazione, ad esempio se viene utilizzato l'affinità di sessione basato su cookie, protocollo, porta e probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="80fb2-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="80fb2-137">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="80fb2-137">Step 1</span></span>

<span data-ttu-id="80fb2-138">Fare clic su hello **regole** di gateway applicazione hello, quindi fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="80fb2-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![Pannello delle regole del gateway applicazione][3]

### <a name="step-2"></a><span data-ttu-id="80fb2-140">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="80fb2-140">Step 2</span></span>

<span data-ttu-id="80fb2-141">In hello **Aggiungi regola di base** pannello digitare hello nome descrittivo per la regola hello e scegliere listener hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="80fb2-142">Scegliere il pool di back-end appropriata hello e http impostazione e fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="80fb2-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![Finestra delle impostazioni HTTP][4]

<span data-ttu-id="80fb2-144">gateway applicazione toohello verranno salvate le impostazioni di Hello.</span><span class="sxs-lookup"><span data-stu-id="80fb2-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="80fb2-145">Hello Salva processo per queste impostazioni potrebbe richiedere qualche minuto prima che vengano tooview disponibili tramite il portale di hello o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80fb2-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="80fb2-146">Gateway applicazione hello dopo il salvataggio gestisce hello crittografia e decrittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="80fb2-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="80fb2-147">Tutto il traffico tra server di hello back-end web e di gateway applicazione hello verrà gestito tramite http.</span><span class="sxs-lookup"><span data-stu-id="80fb2-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="80fb2-148">Verrà restituito client toohello crittografata qualsiasi client toohello indietro comunicazione se avviata tramite https.</span><span class="sxs-lookup"><span data-stu-id="80fb2-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80fb2-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80fb2-149">Next steps</span></span>

<span data-ttu-id="80fb2-150">toolearn come probe tooconfigure dello stato personalizzato con Gateway applicazione Azure, vedere [per creare un probe di integrità personalizzato](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80fb2-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
