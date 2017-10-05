---
title: 'Azure Active Directory Domain Services: aggiornare le impostazioni DNS per la rete virtuale di Azure | Microsoft Docs'
description: Introduzione a Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="43499-103">Abilitare Azure Active Directory Domain Services (anteprima)</span><span class="sxs-lookup"><span data-stu-id="43499-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="43499-104">Attività 4: Aggiornare le impostazioni DNS per la rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="43499-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="43499-105">Nelle attività di configurazione precedenti è stata completata l'abilitazione di Azure Active Directory Domain Services per la directory.</span><span class="sxs-lookup"><span data-stu-id="43499-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="43499-106">L'attività successiva consiste nell'assicurarsi che i computer della rete virtuale possano connettersi a questi servizi e utilizzarli.</span><span class="sxs-lookup"><span data-stu-id="43499-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="43499-107">In questo articolo si aggiorneranno le impostazioni del server DNS per la rete virtuale in modo che puntino ai due indirizzi IP in cui è disponibile Azure Active Directory Domain Services nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="43499-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="43499-108">Per aggiornare l'impostazione del server DNS per la rete virtuale in cui è stato abilitato Azure Active Directory Domain Services, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="43499-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="43499-109">La scheda **Panoramica** elenca una **Procedura di configurazione necessaria** da eseguire dopo il provisioning completo del dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="43499-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="43499-110">Il primo passaggio di configurazione è **Aggiorna le impostazioni del server DNS per la rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="43499-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - Scheda Panoramica dopo il provisioning completo](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="43499-112">Quando il provisioning del dominio è stato completato, in questo riquadro vengono visualizzati due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="43499-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="43499-113">Ogni indirizzo IP rappresenta un controller di dominio per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="43499-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="43499-114">Per copiare il primo indirizzo IP negli Appunti, fare clic sul pulsante Copia accanto all'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="43499-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="43499-115">Fare quindi clic sul pulsante **Configura i server DNS**.</span><span class="sxs-lookup"><span data-stu-id="43499-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="43499-116">Incollare il primo indirizzo IP nella casella di testo **Aggiungi server DNS** nel pannello **Server DNS**.</span><span class="sxs-lookup"><span data-stu-id="43499-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="43499-117">Scorrere orizzontalmente verso sinistra per copiare il secondo indirizzo IP e incollarlo nella casella di testo **Aggiungi server DNS**.</span><span class="sxs-lookup"><span data-stu-id="43499-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Domain Services - Aggiornamento di DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="43499-119">Fare clic su **Salva** al termine dell'aggiornamento dei server DNS per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="43499-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="43499-120">Le macchine virtuali nella rete ottengono le nuove impostazioni DNS solo dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="43499-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="43499-121">Se è necessario ottenere subito le impostazioni DNS aggiornate, eseguire il riavvio dal portale, da PowerShell o dall'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="43499-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="43499-122">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="43499-122">Next step</span></span>
[<span data-ttu-id="43499-123">Attività 5: Abilitare la sincronizzazione password con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="43499-123">Task 5: enable password synchronization to Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
