---
title: 'Azure Active Directory Domain Services: Aggiornare le impostazioni DNS per hello rete virtuale di Azure | Documenti Microsoft'
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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="f852d-103">Abilitare Azure Active Directory Domain Services (anteprima)</span><span class="sxs-lookup"><span data-stu-id="f852d-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="f852d-104">Attività 4: aggiornare le impostazioni DNS per hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f852d-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="f852d-105">In hello precedenti attività di configurazione, si attiva Azure Active Directory Domain Services per la directory.</span><span class="sxs-lookup"><span data-stu-id="f852d-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="f852d-106">attività successiva Hello è tooensure che i computer in rete virtuale hello possono connettersi e utilizzare tali servizi.</span><span class="sxs-lookup"><span data-stu-id="f852d-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="f852d-107">In questo articolo, aggiornare le impostazioni del server DNS hello per il rete virtuale toopoint toohello due indirizzi IP in Azure Active Directory Domain Services è disponibile nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="f852d-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="f852d-108">tooupdate hello impostazioni del server DNS per la rete virtuale di hello in cui è stato abilitato Azure Active Directory Domain Services hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f852d-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="f852d-109">Hello **Panoramica** scheda Elenca un set di **necessari passaggi di configurazione** toobe eseguita dopo che il dominio gestito viene eseguito il provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="f852d-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="f852d-110">primo passaggio di configurazione Hello è **impostazioni del server DNS di aggiornamento per la rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="f852d-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - Scheda Panoramica al termine del provisioning](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="f852d-112">Quando il provisioning del dominio è stato completato, in questo riquadro vengono visualizzati due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="f852d-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="f852d-113">Ogni indirizzo IP rappresenta un controller di dominio per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="f852d-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="f852d-114">primo indirizzo IP hello toocopy indirizzo tooclipboard, fare clic su hello copia pulsante Avanti tooit.</span><span class="sxs-lookup"><span data-stu-id="f852d-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="f852d-115">Quindi fare clic su hello **server configurare DNS** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f852d-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="f852d-116">Incollare l'indirizzo IP prima hello hello **server DNS aggiungere** casella di testo in hello **server DNS** blade.</span><span class="sxs-lookup"><span data-stu-id="f852d-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="f852d-117">Scorrere orizzontalmente toohello toocopy hello secondo indirizzo IP a sinistra e incollarlo in hello **server DNS aggiungere** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f852d-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services - Aggiornamento di DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="f852d-119">Fare clic su **salvare** una volta completate i server DNS per la rete virtuale hello tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="f852d-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="f852d-120">Macchine virtuali nella rete hello ottenere solo le nuove impostazioni DNS di hello dopo un riavvio.</span><span class="sxs-lookup"><span data-stu-id="f852d-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="f852d-121">Se sono necessarie le impostazioni DNS di tooget hello aggiornato immediatamente, attivare un riavvio di un portale hello, PowerShell o hello CLI.</span><span class="sxs-lookup"><span data-stu-id="f852d-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="f852d-122">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f852d-122">Next step</span></span>
[<span data-ttu-id="f852d-123">Attività 5: abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory</span><span class="sxs-lookup"><span data-stu-id="f852d-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
