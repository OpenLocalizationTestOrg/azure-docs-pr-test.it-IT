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
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Risoluzione dei problemi di creazione di raccolte ibride di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Una raccolta ibrida è ospitata nel cloud di Azure insieme ai dati ma consente agli utenti di accedere anche ai dati e alle risorse archiviati nella rete locale. Gli utenti possono accedere alle app effettuando l'accesso con le credenziali aziendali sincronizzate o federate con Azure Active Directory. È possibile distribuire una raccolta ibrida che utilizza una rete virtuale di Azure esistente oppure è possibile creare una nuova rete virtuale. Si consiglia di creare o utilizzare una subnet di rete virtuale con un intervallo CIDR sufficientemente ampio per la crescita prevista per RemoteApp di Azure.

Se la raccolta non è stata ancora creata,  vedere [Come creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md).

Se si verificano problemi durante la creazione della raccolta o se la raccolta non funziona come previsto, consultare le informazioni seguenti.

## <a name="your-image-is-invalid"></a>L'immagine non è valida
Se viene visualizzato un messaggio del tipo "GoldImageInvalid" quando si è in attesa di Azure per eseguire il provisioning per la raccolta, significa che l'immagine del modello non soddisfa i [requisiti definiti per l’immagine](remoteapp-imagereqs.md). Quindi, leggere quei [requisiti](remoteapp-imagereqs.md), correggere l'immagine e cercare di creare nuovamente la raccolta.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Per la rete virtuale sono definiti gruppi di protezione di rete?
Se sono stati definiti gruppi di sicurezza di rete nella subnet usata per la raccolta, assicurarsi che gli [URL e le porte](remoteapp-ports.md) siano accessibili dalla subnet.

È possibile aggiungere gruppi di protezione di rete aggiuntivi alle macchine virtuali distribuite nella subnet per un maggiore controllo.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Si utilizzano propri server DNS? Sono accessibili dalla subnet di rete virtuale?
> [!NOTE]
> È necessario verificare che i server DNS nella rete virtuale siano sempre attivi e sempre in grado di risolvere le macchine virtuali ospitate nella rete virtuale. Non usare Google DNS a questo scopo.
> 
> 

Per le raccolte ibride è possibile utilizzare i propri server DNS. Specificarli nello schema di configurazione di rete o tramite il portale di gestione quando si crea la rete virtuale. I server DNS vengono utilizzati nell'ordine in cui vengono specificati in modo failover (anziché round robin).  
Vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) per verificare che i server DNS siano configurati correttamente.

Verificare che i server DNS per la raccolta siano accessibili e disponibili dalla subnet di rete virtuale specificata per questa raccolta.

Ad esempio:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definire il DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Si sta utilizzando un controller di dominio di Active Directory nella raccolta?
Attualmente solo un dominio di Active Directory può essere associato a RemoteApp di Azure. La raccolta ibrida supporta solo gli account Azure Active Directory che sono stati sincronizzati mediante uno strumento come DirSync da una distribuzione di Windows Server Active Directory. In particolare, sincronizzati con l'opzione di sincronizzazione password oppure con la federazione di Active Directory Federation Services (ADFS) configurata. È necessario creare un dominio personalizzato che corrisponda al suffisso di dominio UPN per il dominio locale e impostare l'integrazione di directory.

Per informazioni sulla pianificazione, vedere [Configurare Active Directory per RemoteApp di Azure](remoteapp-ad.md) .

Assicurarsi che i dettagli del dominio forniti siano validi e che il controller di dominio sia raggiungibile dalla macchina virtuale creata nella subnet utilizzata per RemoteApp di Azure. Assicurarsi inoltre che le credenziali dell'account di servizio fornite dispongano delle autorizzazioni per aggiungere computer al dominio specificato e che il nome di Active Directory specificato posa essere risolto dal DNS fornito nella rete virtuale.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Quale nome di dominio è stato specificato quando è stata creata la raccolta?
Il nome di dominio creato o aggiunto deve essere un nome di dominio interno (non il nome di dominio Active Directory di Azure) e deve essere nel formato DNS risolvibile (contoso.local). Ad esempio, si dispone di un nome interno di Active Directory (contoso.local) e di un UPN di Directory Active (contoso.com): è necessario utilizzare il nome interno quando si crea la raccolta.

