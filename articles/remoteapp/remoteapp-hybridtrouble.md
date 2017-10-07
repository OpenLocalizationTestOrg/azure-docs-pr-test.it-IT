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
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Risoluzione dei problemi di creazione di raccolte ibride di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Una raccolta ibrida è ospitata in e archivia i dati in hello cloud di Azure, ma consente agli utenti accedere ai dati e le risorse memorizzate nella rete locale. Gli utenti possono accedere alle app effettuando l'accesso con le credenziali aziendali sincronizzate o federate con Azure Active Directory. È possibile distribuire una raccolta ibrida che utilizza una rete virtuale di Azure esistente oppure è possibile creare una nuova rete virtuale. Si consiglia di creare o utilizzare una subnet di rete virtuale con un intervallo CIDR sufficientemente ampio per la crescita prevista per RemoteApp di Azure.

Se la raccolta non è stata ancora creata,  Vedere [creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md) per i passaggi di hello.

Se si verificano problemi durante la creazione di raccolta, o se non funziona insieme hello modo hello si sospetta che deve, controllare hello le seguenti informazioni.

## <a name="your-image-is-invalid"></a>L'immagine non è valida
Se viene visualizzato un messaggio ad esempio, "GoldImageInvalid" quando si resta in attesa per Azure tooprovision la raccolta, significa che l'immagine modello non soddisfa hello [definito requisiti immagine](remoteapp-imagereqs.md). In tal caso, passare a leggere quelli [requisiti](remoteapp-imagereqs.md), correggere l'immagine e si tenta di toocreate nuovamente la raccolta.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Per la rete virtuale sono definiti gruppi di protezione di rete?
Se hai definiti nella subnet hello in uso per la raccolta di gruppi di sicurezza di rete, assicurarsi che questi [URL e le porte](remoteapp-ports.md) sono accessibili dall'interno della subnet.

È possibile aggiungere ulteriori rete sicurezza gruppi toohello le macchine virtuali distribuite da parte dell'utente in subnet hello per un controllo.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Si utilizzano propri server DNS? Sono accessibili dalla subnet di rete virtuale?
> [!NOTE]
> È possibile toomake hello che i server DNS in una rete virtuale sono sempre attivi e sempre in grado di tooresolve hello le macchine virtuali ospitate nella rete virtuale hello. Non usare Google DNS a questo scopo.
> 
> 

Per le raccolte ibride è possibile utilizzare i propri server DNS. È specificarli nello schema di configurazione di rete o tramite il portale di gestione di hello quando si crea la rete virtuale. In ordine di hello sono specificati in una modalità di failover (come tooround anziché robin) vengono utilizzati i server DNS.  
Consultare troppo[risoluzione dei nomi per le macchine virtuali e istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake che i server DNS siano correcly configurato.

Verificare che il server DNS hello per la raccolta di siano accessibili e disponibili su una subnet di rete virtuale hello specificato per questa raccolta.

ad esempio:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definire il DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Si sta utilizzando un controller di dominio di Active Directory nella raccolta?
Attualmente solo un dominio di Active Directory può essere associato a RemoteApp di Azure. raccolta ibrida Hello supporta solo gli account di Azure Active Directory che sono stati sincronizzati utilizzando lo strumento DirSync da una distribuzione di Windows Server Active Directory. in particolare, oppure è stata sincronizzata con l'opzione di sincronizzazione Password hello sincronizzati con federazione di Active Directory Federation Services (ADFS) configurata. È necessario toocreate un dominio personalizzato corrispondente al suffisso di dominio UPN hello per il dominio locale e configurare l'integrazione di directory.

Per informazioni sulla pianificazione, vedere [Configurare Active Directory per RemoteApp di Azure](remoteapp-ad.md) .

Assicurarsi che i dettagli del dominio hello forniti siano validi e controller di dominio hello sia raggiungibile dalla macchina virtuale creata in subnet hello usata per Azure RemoteApp hello. Assicurarsi inoltre che l'account del servizio hello le credenziali fornite hanno autorizzazioni tooadd computer toohello fornito dominio e che hello nome Active Directory fornito può essere risolto dal DNS specificato nella rete virtuale hello hello.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Quale nome di dominio è stato specificato quando è stata creata la raccolta?
nome di dominio Hello creati o aggiunti deve essere un nome di dominio interno (non il nome di dominio Azure AD) e deve essere in formato DNS risolvibile (contoso. Local). Ad esempio, si dispone di un nome interno di Active Directory (contoso. Local) e un UPN di Active Directory (contoso.com) - è nome interno di hello toouse quando si crea la raccolta.

