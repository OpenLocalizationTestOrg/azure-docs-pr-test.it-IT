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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="47319-103">Aggiornare le impostazioni DNS per hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="47319-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="47319-104">Attività 4: Aggiornare le impostazioni DNS per hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="47319-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="47319-105">In hello precedenti attività di configurazione, si attiva Azure Active Directory Domain Services per la directory.</span><span class="sxs-lookup"><span data-stu-id="47319-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="47319-106">attività successiva Hello è tooensure che i computer in rete virtuale hello possono connettersi e utilizzare tali servizi.</span><span class="sxs-lookup"><span data-stu-id="47319-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="47319-107">In questo articolo, aggiornare le impostazioni del server DNS hello per il rete virtuale toopoint toohello due indirizzi IP in Azure Active Directory Domain Services è disponibile nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="47319-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="47319-108">Dopo aver abilitato Azure Active Directory Domain Services per la directory di hello, annotare gli indirizzi IP hello per Azure Active Directory Domain Services visualizzate in hello **configura** della directory.</span><span class="sxs-lookup"><span data-stu-id="47319-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="47319-109">tooupdate hello impostazioni del server DNS per la rete virtuale di hello in cui è stato abilitato Azure Active Directory Domain Services hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47319-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="47319-110">Passare toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47319-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="47319-111">Nel riquadro sinistro hello selezionare **reti**.</span><span class="sxs-lookup"><span data-stu-id="47319-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="47319-112">Hello **reti** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="47319-112">hello **Networks** window opens.</span></span>

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="47319-114">In hello **reti virtuali** scheda, rete virtuale di hello select in cui è abilitato Azure Active Directory Domain Services tooview le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="47319-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="47319-115">Fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="47319-115">Click hello **Configure** tab.</span></span>

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="47319-117">In hello **server DNS** immettere entrambi indirizzi IP hello che sono stati visualizzati in hello **servizi di dominio** sezione hello **configura** della directory.</span><span class="sxs-lookup"><span data-stu-id="47319-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="47319-118">Fare clic su impostazioni del server DNS hello toosave per la rete virtuale, nel riquadro attività hello nella parte inferiore di hello della finestra hello **salvare**.</span><span class="sxs-lookup"><span data-stu-id="47319-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Aggiornare le impostazioni del server per la rete virtuale hello hello DNS](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="47319-120">Macchine virtuali nella rete hello ottenere solo le nuove impostazioni DNS di hello dopo un riavvio.</span><span class="sxs-lookup"><span data-stu-id="47319-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="47319-121">Se sono necessarie le impostazioni DNS di tooget hello aggiornato immediatamente, attivare un riavvio di un portale hello, PowerShell o hello CLI.</span><span class="sxs-lookup"><span data-stu-id="47319-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="47319-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47319-122">Next steps</span></span>
<span data-ttu-id="47319-123">Attività 5: [abilitare tooAzure di sincronizzazione password servizi di dominio Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="47319-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
