---
title: Risoluzione dei problemi di creazione delle raccolte ibride di RemoteApp | Documentazione Microsoft
description: Informazioni su come risolvere i problemi relativi agli errori di creazione delle raccolte ibride di RemoteApp
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="937fb-103">Risoluzione dei problemi di creazione di raccolte ibride di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="937fb-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="937fb-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="937fb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="937fb-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="937fb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="937fb-106">Una raccolta ibrida è ospitata nel cloud di Azure insieme ai dati ma consente agli utenti di accedere anche ai dati e alle risorse archiviati nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="937fb-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="937fb-107">Gli utenti possono accedere alle app effettuando l'accesso con le credenziali aziendali sincronizzate o federate con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="937fb-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="937fb-108">È possibile distribuire una raccolta ibrida che utilizza una rete virtuale di Azure esistente oppure è possibile creare una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937fb-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="937fb-109">Si consiglia di creare o utilizzare una subnet di rete virtuale con un intervallo CIDR sufficientemente ampio per la crescita prevista per RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="937fb-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="937fb-110">Se la raccolta non è stata ancora creata, </span><span class="sxs-lookup"><span data-stu-id="937fb-110">Haven't created your collection yet?</span></span> <span data-ttu-id="937fb-111">vedere [Come creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="937fb-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="937fb-112">Se si verificano problemi durante la creazione della raccolta o se la raccolta non funziona come previsto, consultare le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="937fb-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="937fb-113">L'immagine non è valida</span><span class="sxs-lookup"><span data-stu-id="937fb-113">Your image is invalid</span></span>
<span data-ttu-id="937fb-114">Se viene visualizzato un messaggio del tipo "GoldImageInvalid" quando si è in attesa di Azure per eseguire il provisioning per la raccolta, significa che l'immagine del modello non soddisfa i [requisiti definiti per l’immagine](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="937fb-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="937fb-115">Quindi, leggere quei [requisiti](remoteapp-imagereqs.md), correggere l'immagine e cercare di creare nuovamente la raccolta.</span><span class="sxs-lookup"><span data-stu-id="937fb-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="937fb-116">Per la rete virtuale sono definiti gruppi di protezione di rete?</span><span class="sxs-lookup"><span data-stu-id="937fb-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="937fb-117">Se sono stati definiti gruppi di sicurezza di rete nella subnet usata per la raccolta, assicurarsi che gli [URL e le porte](remoteapp-ports.md) siano accessibili dalla subnet.</span><span class="sxs-lookup"><span data-stu-id="937fb-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="937fb-118">È possibile aggiungere gruppi di protezione di rete aggiuntivi alle macchine virtuali distribuite nella subnet per un maggiore controllo.</span><span class="sxs-lookup"><span data-stu-id="937fb-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="937fb-119">Si utilizzano propri server DNS?</span><span class="sxs-lookup"><span data-stu-id="937fb-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="937fb-120">Sono accessibili dalla subnet di rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="937fb-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="937fb-121">È necessario verificare che i server DNS nella rete virtuale siano sempre attivi e sempre in grado di risolvere le macchine virtuali ospitate nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937fb-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="937fb-122">Non usare Google DNS a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="937fb-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="937fb-123">Per le raccolte ibride è possibile utilizzare i propri server DNS.</span><span class="sxs-lookup"><span data-stu-id="937fb-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="937fb-124">Specificarli nello schema di configurazione di rete o tramite il portale di gestione quando si crea la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937fb-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="937fb-125">I server DNS vengono utilizzati nell'ordine in cui vengono specificati in modo failover (anziché round robin).</span><span class="sxs-lookup"><span data-stu-id="937fb-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="937fb-126">Vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) per verificare che i server DNS siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="937fb-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="937fb-127">Verificare che i server DNS per la raccolta siano accessibili e disponibili dalla subnet di rete virtuale specificata per questa raccolta.</span><span class="sxs-lookup"><span data-stu-id="937fb-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="937fb-128">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="937fb-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definire il DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="937fb-130">Si sta utilizzando un controller di dominio di Active Directory nella raccolta?</span><span class="sxs-lookup"><span data-stu-id="937fb-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="937fb-131">Attualmente solo un dominio di Active Directory può essere associato a RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="937fb-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="937fb-132">La raccolta ibrida supporta solo gli account Azure Active Directory che sono stati sincronizzati mediante uno strumento come DirSync da una distribuzione di Windows Server Active Directory. In particolare, sincronizzati con l'opzione di sincronizzazione password oppure con la federazione di Active Directory Federation Services (ADFS) configurata.</span><span class="sxs-lookup"><span data-stu-id="937fb-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="937fb-133">È necessario creare un dominio personalizzato che corrisponda al suffisso di dominio UPN per il dominio locale e impostare l'integrazione di directory.</span><span class="sxs-lookup"><span data-stu-id="937fb-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="937fb-134">Per informazioni sulla pianificazione, vedere [Configurare Active Directory per RemoteApp di Azure](remoteapp-ad.md) .</span><span class="sxs-lookup"><span data-stu-id="937fb-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="937fb-135">Assicurarsi che i dettagli del dominio forniti siano validi e che il controller di dominio sia raggiungibile dalla macchina virtuale creata nella subnet utilizzata per RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="937fb-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="937fb-136">Assicurarsi inoltre che le credenziali dell'account di servizio fornite dispongano delle autorizzazioni per aggiungere computer al dominio specificato e che il nome di Active Directory specificato posa essere risolto dal DNS fornito nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937fb-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="937fb-137">Quale nome di dominio è stato specificato quando è stata creata la raccolta?</span><span class="sxs-lookup"><span data-stu-id="937fb-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="937fb-138">Il nome di dominio creato o aggiunto deve essere un nome di dominio interno (non il nome di dominio Active Directory di Azure) e deve essere nel formato DNS risolvibile (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="937fb-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="937fb-139">Ad esempio, si dispone di un nome interno di Active Directory (contoso.local) e di un UPN di Directory Active (contoso.com): è necessario utilizzare il nome interno quando si crea la raccolta.</span><span class="sxs-lookup"><span data-stu-id="937fb-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

