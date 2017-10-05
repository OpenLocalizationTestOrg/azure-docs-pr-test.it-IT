---
title: 'Azure Active Directory Domain Services: abilitare Azure Active Directory Domain Services | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services tramite il portale di Azure classico
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="4e4c3-103">Abilitare Azure Active Directory Domain Services tramite il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="4e4c3-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="4e4c3-104">Attività 3: Abilitare Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="4e4c3-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="4e4c3-105">In questa attività si abiliterà Azure Active Directory Domain Services (Azure AD DS) per la directory seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e4c3-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="4e4c3-106">Passare al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4e4c3-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4e4c3-107">Selezionare il pulsante **Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="4e4c3-108">Selezionare il tenant (directory) di Azure Active Directory (Azure AD) per il quale si desidera abilitare Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="4e4c3-110">Nella pagina **anteprima directory** fare clic sulla scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="4e4c3-112">In **servizi di dominio**, modificare l'opzione **Abilita Servizi di dominio per la directory** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="4e4c3-113">Nella pagina verranno visualizzate altre opzioni di configurazione di Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Abilita servizi di dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="4e4c3-115">Quando si abilita Azure Active Directory Domain Services per il tenant, Azure AD genera e archivia gli hash delle credenziali Kerberos e NTLM necessari per l'autenticazione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="4e4c3-116">Specificare il **Nome di dominio DNS di Servizi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="4e4c3-117">Il nome di dominio predefinito della directory (con suffisso **.onmicrosoft.com**) viene selezionato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="4e4c3-118">Nell'elenco sono contenuti tutti i domini che sono stati configurati per la directory di Azure AD, inclusi i domini verificati e non verificati configurati nella scheda **Domini**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="4e4c3-119">È inoltre possibile immettere un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="4e4c3-120">In questo esempio, il nome di dominio personalizzato è *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="4e4c3-121">Il prefisso del nome del dominio specificato (ad esempio, *contoso100* nel nome di dominio *contoso100.com*) può contenere massimo 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="4e4c3-122">Non è possibile creare un dominio di Azure Active Directory Domain Services con un prefisso contenente più di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="4e4c3-123">Assicurarsi che il nome di dominio DNS scelto per il dominio gestito non esista già nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="4e4c3-124">In particolare, verificare se:</span><span class="sxs-lookup"><span data-stu-id="4e4c3-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="4e4c3-125">È già presente un dominio con lo stesso nome di dominio DNS nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="4e4c3-126">La rete virtuale selezionata ha una connessione VPN alla rete locale, dove è presente un dominio con lo stesso nome di dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="4e4c3-127">Esiste un servizio cloud con lo stesso nome della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="4e4c3-128">Selezionare una rete virtuale in cui si desidera la disponibilità di Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="4e4c3-129">Selezionare la rete virtuale e la subnet dedicata create nell'elenco a discesa **Connetti Servizi di dominio a questa rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="4e4c3-130">Tenere inoltre in considerazione quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4e4c3-130">Also consider the following:</span></span>

   * <span data-ttu-id="4e4c3-131">Assicurarsi che la rete virtuale specificata appartenga a un'area di Azure supportata da Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="4e4c3-132">Per conoscere le aree di Azure in cui è disponibile Azure Active Directory Domain Services, vedere i [servizi di Azure per area](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="4e4c3-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="4e4c3-133">Le reti virtuali appartenenti a un'area in cui Azure Active Directory Domain Services non è supportato non vengono visualizzate nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="4e4c3-134">Usare una subnet dedicata nella rete virtuale per Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="4e4c3-135">*Non* selezionare la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="4e4c3-136">Vedere le [considerazioni sulla rete](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="4e4c3-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="4e4c3-137">Analogamente, le reti virtuali create con Azure Resource Manager non vengono visualizzate nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="4e4c3-138">Le reti virtuali basate su Resource Manager attualmente non sono supportate da Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="4e4c3-139">Per abilitare Azure Active Directory Domain Services, fare clic su **Salva** nel riquadro attività nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="4e4c3-140">Quando si attiva Azure Active Directory Domain Services per la directory, la pagina mostra lo stato *In sospeso*.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Finestra Abilita Domain Services](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="4e4c3-142">Azure Active Directory Domain Services garantisce un'elevata disponibilità per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="4e4c3-143">Dopo avere abilitato Azure Active Directory Domain Services, vengono visualizzati uno alla volta gli indirizzi IP per cui è disponibile Domain Services nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="4e4c3-144">Il secondo indirizzo IP viene visualizzato poco dopo il primo, non appena il servizio abilita la disponibilità elevata per il dominio.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="4e4c3-145">Al termine della configurazione e attivazione della disponibilità elevata per il dominio, nella sezione **Servizi di dominio** della scheda **Configura** dovrebbero comparire due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="4e4c3-146">Dopo circa 20-30 minuti, il primo indirizzo IP in cui è disponibile Domain Services nella rete virtuale viene visualizzato nel campo **Indirizzo IP** nella pagina **Configura**.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![La finestra di Domain Service visualizza il primo indirizzo IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="4e4c3-148">Quando la disponibilità elevata è operativa per il dominio, nella pagina sono visualizzati due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="4e4c3-149">Il dominio gestito è disponibile nella rete virtuale selezionata a questi due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="4e4c3-150">Prendere nota degli indirizzi IP per poter aggiornare le impostazioni DNS per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="4e4c3-151">Questo passaggio consente alle macchine virtuali nella rete virtuale di connettersi al dominio per operazioni quali l'aggiunta al dominio.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![La finestra di Domain Services mostra entrambi gli IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="4e4c3-153">A seconda delle dimensioni del tenant di Azure AD (ad esempio, numero di utenti e gruppi), la sincronizzazione con il dominio gestito richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="4e4c3-154">Questo processo di sincronizzazione avviene in background.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="4e4c3-155">Per tenant di grandi dimensioni con decine di migliaia di oggetti, possono essere necessari anche un paio di giorni perché tutti gli utenti, le appartenenze ai gruppi e le credenziali siano sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="4e4c3-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="4e4c3-156">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="4e4c3-156">Next step</span></span>
[<span data-ttu-id="4e4c3-157">Attività 4: Aggiornare le impostazioni DNS per la rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4e4c3-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
