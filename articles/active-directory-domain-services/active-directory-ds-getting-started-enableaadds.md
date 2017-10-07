---
title: 'Azure Active Directory Domain Services: abilitare Azure Active Directory Domain Services | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
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
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="343de-103">Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="343de-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="343de-104">Attività 3: Abilitare Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="343de-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="343de-105">In questa attività, abilitare Servizi di dominio Active Directory Azure (Azure AD DS) per la directory effettuando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="343de-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="343de-106">Passare toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="343de-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="343de-107">Nel riquadro sinistro hello selezionare hello **Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="343de-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="343de-108">Selezionare tenant di Azure Active Directory (Azure AD) hello (directory) per il quale si desidera tooenable Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343de-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="343de-110">In hello **directory anteprima** pagina, fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="343de-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="343de-112">In **servizi di dominio**, modificare hello **Abilita servizi di dominio per questa directory** opzione troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="343de-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="343de-113">Ulteriori opzioni di configurazione di Azure Active Directory Domain Services visualizzati nella pagina di hello.</span><span class="sxs-lookup"><span data-stu-id="343de-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Abilita servizi di dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="343de-115">Quando si abilita Azure Active Directory Domain Services per il tenant, Azure AD genera e archivia hello Kerberos e NTLM degli hash delle credenziali necessarie per l'autenticazione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="343de-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="343de-116">Specificare hello **nome di dominio DNS di servizi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="343de-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="343de-117">nome di dominio Hello predefinito della directory hello (con un **. c o m** suffisso) è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="343de-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="343de-118">Hello elenco contiene tutti i domini che sono stati configurati per la directory di Azure AD, inclusi sia verificato e non verificati domini configurati nel hello **domini** scheda.</span><span class="sxs-lookup"><span data-stu-id="343de-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="343de-119">È inoltre possibile immettere un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="343de-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="343de-120">In questo esempio, è il nome di dominio personalizzato hello *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="343de-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="343de-121">prefisso Hello del nome del dominio specificato (ad esempio, *contoso100* in hello *contoso100.com* nome di dominio) deve contenere meno di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="343de-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="343de-122">Non è possibile creare un dominio di Azure Active Directory Domain Services con un prefisso contenente più di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="343de-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="343de-123">Verificare il nome di dominio DNS hello che scelto per hello gestito dominio non esiste già nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="343de-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="343de-124">In particolare, controllare se toosee:</span><span class="sxs-lookup"><span data-stu-id="343de-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="343de-125">Si dispone già di un dominio con hello stesso nome di dominio DNS nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="343de-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="343de-126">rete virtuale selezionata Hello ha una connessione VPN alla rete locale e si dispone di un dominio con hello stesso nome di dominio DNS nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="343de-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="343de-127">È un servizio cloud esistente con lo stesso nome nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="343de-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="343de-128">Selezionare una rete virtuale in cui si desidera toobe di Azure Active Directory Domain Services disponibili.</span><span class="sxs-lookup"><span data-stu-id="343de-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="343de-129">Selezionare la rete virtuale hello e una subnet dedicata creata in hello **toothis di rete virtuale di servizi di dominio Connetti** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="343de-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="343de-130">Considerare anche l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="343de-130">Also consider hello following:</span></span>

   * <span data-ttu-id="343de-131">Verificare che tale rete virtuale hello specificato appartiene tooan area di Azure supportati da servizi di dominio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343de-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="343de-132">tooascertain hello aree di Azure in cui servizi di dominio di Azure Active Directory è disponibili, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="343de-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="343de-133">Reti virtuali appartenenti tooa area in cui i servizi di dominio di Azure Active Directory non è supportato non vengono visualizzati nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="343de-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="343de-134">Utilizzare una subnet dedicata all'interno di rete virtuale hello per servizi di dominio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343de-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="343de-135">Eseguire *non* selezionare hello subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="343de-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="343de-136">Vedere le [considerazioni sulla rete](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="343de-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="343de-137">Analogamente, le reti virtuali che sono state create usando Gestione risorse di Azure non vengono visualizzati nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="343de-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="343de-138">Le reti virtuali basate su Resource Manager attualmente non sono supportate da Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="343de-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="343de-139">Fare clic su tooenable Azure Active Directory Domain Services, nel riquadro attività hello nella parte inferiore di hello della pagina hello **salvare**.</span><span class="sxs-lookup"><span data-stu-id="343de-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="343de-140">Servizi di dominio di Azure Active Directory è abilitato per la directory, pagina hello Visualizza lo stato di *in sospeso*.</span><span class="sxs-lookup"><span data-stu-id="343de-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Finestra Abilita Domain Services](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="343de-142">Azure Active Directory Domain Services garantisce un'elevata disponibilità per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="343de-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="343de-143">Dopo aver abilitato Servizi di dominio di Azure Active Directory, gli indirizzi IP di hello del dominio sono disponibili nella rete virtuale hello servizi sono visualizzati uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="343de-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="343de-144">secondo indirizzo IP di Hello viene visualizzato in primo luogo, poco dopo hello appena servizio hello consente una disponibilità elevata per il dominio.</span><span class="sxs-lookup"><span data-stu-id="343de-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="343de-145">Quando è configurata la disponibilità elevata e attivo per il dominio, vengono visualizzati due indirizzi IP in hello **servizi di dominio** sezione di hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="343de-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="343de-146">Dopo circa 20 minuti too30, hello primo indirizzo IP del dominio servizi disponibili nella rete virtuale in hello **indirizzo IP** campo hello **configura** pagina.</span><span class="sxs-lookup"><span data-stu-id="343de-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![La finestra di Domain Service visualizza il primo indirizzo IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="343de-148">Quando la disponibilità elevata è operativa per il dominio, i due indirizzi IP vengono visualizzati nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="343de-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="343de-149">Il dominio gestito è disponibile nella rete virtuale selezionata a questi due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="343de-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="343de-150">Si noti due indirizzi IP di hello in modo che sia possibile aggiornare le impostazioni DNS hello per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="343de-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="343de-151">In questo modo consente alle macchine virtuali nel dominio di hello rete virtuale tooconnect toohello per operazioni quali aggiunta al dominio.</span><span class="sxs-lookup"><span data-stu-id="343de-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![La finestra di Domain Services mostra entrambi gli IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="343de-153">A seconda delle dimensioni di hello del tenant di Azure AD (ad esempio, numero hello di utenti o gruppi), dominio di sincronizzazione tooyour gestito richiede un certo tempo.</span><span class="sxs-lookup"><span data-stu-id="343de-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="343de-154">Questo processo di sincronizzazione viene eseguita in background hello.</span><span class="sxs-lookup"><span data-stu-id="343de-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="343de-155">Per i tenant con decine di migliaia di oggetti di grandi dimensioni, potrebbe richiedere un o due giorni per tutti gli utenti, appartenenze a gruppi e credenziali toobe sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="343de-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="343de-156">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="343de-156">Next step</span></span>
[<span data-ttu-id="343de-157">Attività 4: aggiornare le impostazioni DNS di hello per hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="343de-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
