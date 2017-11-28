---
title: le impostazioni del Registro di sistema di individuazione di App per servizi Proxy aaaCloud | Documenti Microsoft
description: "obiettivo Hello di questo argomento è tooprovide si con hello i passaggi necessari per necessario tooperform tooset hello necessario porta hello i computer agente Cloud App Discovery hello."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="6a23b-103">Impostazioni del Registro di sistema di Cloud App Discovery per i servizi proxy</span><span class="sxs-lookup"><span data-stu-id="6a23b-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="6a23b-104">Per impostazione predefinita, l'agente Cloud App Discovery hello è toouse configurato solo hello porte 80 o 443.</span><span class="sxs-lookup"><span data-stu-id="6a23b-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="6a23b-105">Se prevede di installare Cloud App Discovery in un ambiente con un server proxy che utilizza una porta personalizzata (80 né 443), è necessario tooconfigure il toouse agenti questa porta.</span><span class="sxs-lookup"><span data-stu-id="6a23b-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="6a23b-106">configurazione di Hello è basata su una chiave del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="6a23b-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="6a23b-107">obiettivo Hello di questo argomento è tooprovide si con hello i passaggi necessari per necessario tooperform tooset hello necessario porta hello i computer agente Cloud App Discovery hello.</span><span class="sxs-lookup"><span data-stu-id="6a23b-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="6a23b-108">**porta hello toomodify utilizzata dal computer hello esecuzione agente Cloud App Discovery hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a23b-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a23b-109">Avviare l'editor del Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="6a23b-109">Start hello registry editor.</span></span> <br> ![Esegui](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="6a23b-111">Passare tooor creare hello seguente chiave del Registro di sistema:</span><span class="sxs-lookup"><span data-stu-id="6a23b-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="6a23b-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="6a23b-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="6a23b-113">Creare un nuovo valore **multistringa** denominato **Ports**.</span><span class="sxs-lookup"><span data-stu-id="6a23b-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="6a23b-114">![Nuovo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="6a23b-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="6a23b-115">hello tooopen **Modifica multistringhe** finestra di dialogo, fare doppio clic sul valore porte hello.</span><span class="sxs-lookup"><span data-stu-id="6a23b-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="6a23b-116">Nella casella dati valore hello digitare i seguenti valori hello e aggiungere tutte le porte personalizzate che vengono utilizzate dall'organizzazione:</span><span class="sxs-lookup"><span data-stu-id="6a23b-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="6a23b-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="6a23b-117">
   **80**</span></span> <br><span data-ttu-id="6a23b-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="6a23b-118">
   **8080**</span></span> <br><span data-ttu-id="6a23b-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="6a23b-119">
   **8118**</span></span> <br><span data-ttu-id="6a23b-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="6a23b-120">
   **8888**</span></span> <br><span data-ttu-id="6a23b-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="6a23b-121">
   **81**</span></span> <br><span data-ttu-id="6a23b-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="6a23b-122">
   **12080**</span></span> <br><span data-ttu-id="6a23b-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="6a23b-123">
**6999**</span></span> <br><span data-ttu-id="6a23b-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="6a23b-124">
**30606**</span></span> <br><span data-ttu-id="6a23b-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="6a23b-125">
**31595**</span></span> <br><span data-ttu-id="6a23b-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="6a23b-126">
**4080**</span></span> <br><span data-ttu-id="6a23b-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="6a23b-127">
**443**</span></span> <br><span data-ttu-id="6a23b-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="6a23b-128">
**1110**</span></span> <br><br><span data-ttu-id="6a23b-129">
![Modifica multistringhe](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="6a23b-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="6a23b-130">Fare clic su **OK** tooclose hello **Modifica multistringhe** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6a23b-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="6a23b-131">**Risorse aggiuntive**</span><span class="sxs-lookup"><span data-stu-id="6a23b-131">**Additional Resources**</span></span>

* [<span data-ttu-id="6a23b-132">Come individuare app cloud non autorizzate usate nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="6a23b-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

