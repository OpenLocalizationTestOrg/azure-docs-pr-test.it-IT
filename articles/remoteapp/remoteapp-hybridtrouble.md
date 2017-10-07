---
title: creazione di raccolte di RemoteApp ibrida aaaTroubleshoot | Documenti Microsoft
description: Informazioni su come errori di creazione raccolta ibrida tootroubleshoot RemoteApp
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="efb6b-103">Risoluzione dei problemi di creazione di raccolte ibride di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efb6b-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="efb6b-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="efb6b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="efb6b-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="efb6b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="efb6b-106">Una raccolta ibrida è ospitata in e archivia i dati in hello cloud di Azure, ma consente agli utenti accedere ai dati e le risorse memorizzate nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="efb6b-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="efb6b-107">Gli utenti possono accedere alle app effettuando l'accesso con le credenziali aziendali sincronizzate o federate con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efb6b-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="efb6b-108">È possibile distribuire una raccolta ibrida che utilizza una rete virtuale di Azure esistente oppure è possibile creare una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="efb6b-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="efb6b-109">Si consiglia di creare o utilizzare una subnet di rete virtuale con un intervallo CIDR sufficientemente ampio per la crescita prevista per RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb6b-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="efb6b-110">Se la raccolta non è stata ancora creata, </span><span class="sxs-lookup"><span data-stu-id="efb6b-110">Haven't created your collection yet?</span></span> <span data-ttu-id="efb6b-111">Vedere [creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md) per i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="efb6b-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="efb6b-112">Se si verificano problemi durante la creazione di raccolta, o se non funziona insieme hello modo hello si sospetta che deve, controllare hello le seguenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="efb6b-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="efb6b-113">L'immagine non è valida</span><span class="sxs-lookup"><span data-stu-id="efb6b-113">Your image is invalid</span></span>
<span data-ttu-id="efb6b-114">Se viene visualizzato un messaggio ad esempio, "GoldImageInvalid" quando si resta in attesa per Azure tooprovision la raccolta, significa che l'immagine modello non soddisfa hello [definito requisiti immagine](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="efb6b-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="efb6b-115">In tal caso, passare a leggere quelli [requisiti](remoteapp-imagereqs.md), correggere l'immagine e si tenta di toocreate nuovamente la raccolta.</span><span class="sxs-lookup"><span data-stu-id="efb6b-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="efb6b-116">Per la rete virtuale sono definiti gruppi di protezione di rete?</span><span class="sxs-lookup"><span data-stu-id="efb6b-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="efb6b-117">Se hai definiti nella subnet hello in uso per la raccolta di gruppi di sicurezza di rete, assicurarsi che questi [URL e le porte](remoteapp-ports.md) sono accessibili dall'interno della subnet.</span><span class="sxs-lookup"><span data-stu-id="efb6b-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="efb6b-118">È possibile aggiungere ulteriori rete sicurezza gruppi toohello le macchine virtuali distribuite da parte dell'utente in subnet hello per un controllo.</span><span class="sxs-lookup"><span data-stu-id="efb6b-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="efb6b-119">Si utilizzano propri server DNS?</span><span class="sxs-lookup"><span data-stu-id="efb6b-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="efb6b-120">Sono accessibili dalla subnet di rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="efb6b-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="efb6b-121">È possibile toomake hello che i server DNS in una rete virtuale sono sempre attivi e sempre in grado di tooresolve hello le macchine virtuali ospitate nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="efb6b-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="efb6b-122">Non usare Google DNS a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="efb6b-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="efb6b-123">Per le raccolte ibride è possibile utilizzare i propri server DNS.</span><span class="sxs-lookup"><span data-stu-id="efb6b-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="efb6b-124">È specificarli nello schema di configurazione di rete o tramite il portale di gestione di hello quando si crea la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="efb6b-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="efb6b-125">In ordine di hello sono specificati in una modalità di failover (come tooround anziché robin) vengono utilizzati i server DNS.</span><span class="sxs-lookup"><span data-stu-id="efb6b-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="efb6b-126">Consultare troppo[risoluzione dei nomi per le macchine virtuali e istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake che i server DNS siano correcly configurato.</span><span class="sxs-lookup"><span data-stu-id="efb6b-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="efb6b-127">Verificare che il server DNS hello per la raccolta di siano accessibili e disponibili su una subnet di rete virtuale hello specificato per questa raccolta.</span><span class="sxs-lookup"><span data-stu-id="efb6b-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="efb6b-128">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efb6b-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definire il DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="efb6b-130">Si sta utilizzando un controller di dominio di Active Directory nella raccolta?</span><span class="sxs-lookup"><span data-stu-id="efb6b-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="efb6b-131">Attualmente solo un dominio di Active Directory può essere associato a RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb6b-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="efb6b-132">raccolta ibrida Hello supporta solo gli account di Azure Active Directory che sono stati sincronizzati utilizzando lo strumento DirSync da una distribuzione di Windows Server Active Directory. in particolare, oppure è stata sincronizzata con l'opzione di sincronizzazione Password hello sincronizzati con federazione di Active Directory Federation Services (ADFS) configurata.</span><span class="sxs-lookup"><span data-stu-id="efb6b-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="efb6b-133">È necessario toocreate un dominio personalizzato corrispondente al suffisso di dominio UPN hello per il dominio locale e configurare l'integrazione di directory.</span><span class="sxs-lookup"><span data-stu-id="efb6b-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="efb6b-134">Per informazioni sulla pianificazione, vedere [Configurare Active Directory per RemoteApp di Azure](remoteapp-ad.md) .</span><span class="sxs-lookup"><span data-stu-id="efb6b-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="efb6b-135">Assicurarsi che i dettagli del dominio hello forniti siano validi e controller di dominio hello sia raggiungibile dalla macchina virtuale creata in subnet hello usata per Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="efb6b-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="efb6b-136">Assicurarsi inoltre che l'account del servizio hello le credenziali fornite hanno autorizzazioni tooadd computer toohello fornito dominio e che hello nome Active Directory fornito può essere risolto dal DNS specificato nella rete virtuale hello hello.</span><span class="sxs-lookup"><span data-stu-id="efb6b-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="efb6b-137">Quale nome di dominio è stato specificato quando è stata creata la raccolta?</span><span class="sxs-lookup"><span data-stu-id="efb6b-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="efb6b-138">nome di dominio Hello creati o aggiunti deve essere un nome di dominio interno (non il nome di dominio Azure AD) e deve essere in formato DNS risolvibile (contoso. Local).</span><span class="sxs-lookup"><span data-stu-id="efb6b-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="efb6b-139">Ad esempio, si dispone di un nome interno di Active Directory (contoso. Local) e un UPN di Active Directory (contoso.com) - è nome interno di hello toouse quando si crea la raccolta.</span><span class="sxs-lookup"><span data-stu-id="efb6b-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

