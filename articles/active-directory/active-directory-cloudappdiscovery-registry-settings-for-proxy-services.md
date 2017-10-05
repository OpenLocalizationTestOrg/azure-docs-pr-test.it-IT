---
title: Impostazioni del Registro di sistema di Cloud App Discovery per i servizi proxy | Documentazione Microsoft
description: Questo argomento illustra tutti i passaggi da eseguire per impostare la porta necessaria sui computer che eseguono l'agente Cloud App Discovery.
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="a9e29-103">Impostazioni del Registro di sistema di Cloud App Discovery per i servizi proxy</span><span class="sxs-lookup"><span data-stu-id="a9e29-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="a9e29-104">Per impostazione predefinita, l'agente Cloud App Discovery è configurato solo per l'uso delle porte 80 o 443.</span><span class="sxs-lookup"><span data-stu-id="a9e29-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="a9e29-105">Se si prevede di installare Cloud App Discovery in un ambiente con un server proxy che usa una porta personalizzata (non la 80 né la 443), è necessario configurare gli agenti per l'uso di questa porta.</span><span class="sxs-lookup"><span data-stu-id="a9e29-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="a9e29-106">La configurazione si basa su una chiave del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="a9e29-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="a9e29-107">Questo argomento illustra tutti i passaggi da eseguire per impostare la porta necessaria sui computer che eseguono l'agente Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="a9e29-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="a9e29-108">**Per modificare la porta usata dal computer che esegue l'agente Cloud App Discovery, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a9e29-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="a9e29-109">Avviare l'Editor del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="a9e29-109">Start the registry editor.</span></span> <br> ![Esegui](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="a9e29-111">Passare alla chiave seguente del Registro di sistema oppure crearla: </span><span class="sxs-lookup"><span data-stu-id="a9e29-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="a9e29-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="a9e29-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="a9e29-113">Creare un nuovo valore **multistringa** denominato **Ports**.</span><span class="sxs-lookup"><span data-stu-id="a9e29-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="a9e29-114">![Nuovo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="a9e29-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="a9e29-115">Per aprire la finestra di dialogo **Modifica multistringhe** , fare doppio clic sul valore Ports.</span><span class="sxs-lookup"><span data-stu-id="a9e29-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="a9e29-116">Nella casella di testo Dati valore digitare i valori seguenti e aggiungere tutte le porte personalizzate usate dall'organizzazione: </span><span class="sxs-lookup"><span data-stu-id="a9e29-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="a9e29-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="a9e29-117">
   **80**</span></span> <br><span data-ttu-id="a9e29-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="a9e29-118">
   **8080**</span></span> <br><span data-ttu-id="a9e29-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="a9e29-119">
   **8118**</span></span> <br><span data-ttu-id="a9e29-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="a9e29-120">
   **8888**</span></span> <br><span data-ttu-id="a9e29-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="a9e29-121">
   **81**</span></span> <br><span data-ttu-id="a9e29-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="a9e29-122">
   **12080**</span></span> <br><span data-ttu-id="a9e29-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="a9e29-123">
**6999**</span></span> <br><span data-ttu-id="a9e29-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="a9e29-124">
**30606**</span></span> <br><span data-ttu-id="a9e29-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="a9e29-125">
**31595**</span></span> <br><span data-ttu-id="a9e29-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="a9e29-126">
**4080**</span></span> <br><span data-ttu-id="a9e29-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="a9e29-127">
**443**</span></span> <br><span data-ttu-id="a9e29-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="a9e29-128">
**1110**</span></span> <br><br><span data-ttu-id="a9e29-129">
![Modifica multistringhe](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="a9e29-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="a9e29-130">Fare clic su **OK** per chiudere la finestra di dialogo **Modifica multistringhe**.</span><span class="sxs-lookup"><span data-stu-id="a9e29-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="a9e29-131">**Risorse aggiuntive**</span><span class="sxs-lookup"><span data-stu-id="a9e29-131">**Additional Resources**</span></span>

* [<span data-ttu-id="a9e29-132">Come individuare app cloud non autorizzate usate nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="a9e29-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

