---
title: 'Azure Active Directory Domain Services: creare o selezionare una rete virtuale | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="4e126-103">Creare o selezionare una rete virtuale per Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="4e126-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="4e126-104">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4e126-104">Before you begin</span></span>
<span data-ttu-id="4e126-105">Fare riferimento troppo[considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="4e126-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="4e126-106">Attività 2: Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4e126-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="4e126-107">attività di configurazione successiva Hello è toocreate una rete virtuale di Azure e una subnet all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="4e126-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="4e126-108">Abilitare Azure Active Directory Domain Services in questa subnet all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e126-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="4e126-109">Se si dispone di una rete virtuale esistente che si preferisce toouse, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4e126-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="4e126-110">Verificare che tale rete virtuale di Azure creare o scegliere toouse con Azure Active Directory Domain Services appartiene tooan area di Azure è supportato da Azure Active Directory Domain Services hello.</span><span class="sxs-lookup"><span data-stu-id="4e126-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="4e126-111">tooascertain hello aree di Azure in cui sono disponibili servizi di dominio di Azure Active Directory, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="4e126-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="4e126-112">Annotare il nome di hello di hello tooensure di rete virtuale selezionare la rete virtuale a destra di hello quando si abilita Azure Active Directory Domain Services in un passaggio di configurazione successive.</span><span class="sxs-lookup"><span data-stu-id="4e126-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="4e126-113">toocreate una rete virtuale di Azure in cui si desidera tooenable Azure Active Directory Domain Services, seguire queste istruzioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="4e126-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="4e126-114">Passare toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4e126-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4e126-115">Nel riquadro sinistro hello selezionare **reti**.</span><span class="sxs-lookup"><span data-stu-id="4e126-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="4e126-116">![Nodi di reti](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="4e126-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="4e126-117">Hello **reti virtuali** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="4e126-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="4e126-118">Nel riquadro delle attività hello nella parte inferiore di hello della finestra hello, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="4e126-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="4e126-120">Fare clic su **Servizi di rete**, quindi selezionare **Rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4e126-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Rete virtuale - creazione rapida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="4e126-122">Fare clic su una rete virtuale, toocreate **creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="4e126-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="4e126-123">Specificare un **nome** per la macchina di rete e provare a eseguire operazioni hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e126-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="4e126-124">È possibile scegliere tooconfigure **lo spazio degli indirizzi** o **numero massimo VM** per la rete.</span><span class="sxs-lookup"><span data-stu-id="4e126-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="4e126-125">È possibile lasciare hello **server DNS** impostando come **Nessuno** per ora.</span><span class="sxs-lookup"><span data-stu-id="4e126-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="4e126-126">È possibile aggiornare l'impostazione di hello dopo aver abilitato Servizi di dominio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4e126-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="4e126-127">In hello **percorso** elenco a discesa selezionare una regione di Azure supportata.</span><span class="sxs-lookup"><span data-stu-id="4e126-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="4e126-128">tooascertain hello aree di Azure in cui sono disponibili servizi di dominio di Azure Active Directory, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="4e126-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="4e126-129">toocreate la rete virtuale, fare clic su **creare una rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4e126-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Creare una rete virtuale per Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="4e126-131">Dopo aver creato una rete virtuale, selezionare il nome di rete virtuale hello hello e quindi fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="4e126-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Creare una subnet](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="4e126-133">In **spazi di indirizzi della rete virtuale**, fare clic su **aggiungere subnet**, quindi specificare una subnet con nome hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="4e126-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Creare una subnet per Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="4e126-135">toocreate hello subnet, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="4e126-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="4e126-136">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="4e126-136">Next step</span></span>
[<span data-ttu-id="4e126-137">Attività 3: Abilitare Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="4e126-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
