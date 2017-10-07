---
title: Glossario di aaaAzure - dizionario di Azure | Documenti Microsoft
description: Utilizzare la terminologia di hello glossario di Azure toounderstand cloud hello piattaforma Azure. Questo breve dizionario di Azure include le definizioni dei termini comuni relativi al cloud usati in Azure.
keywords: Dizionario di Azure, terminologia cloud, glossario di Azure, definizioni terminologiche, termini del cloud
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Glossario di Microsoft Azure: un dizionario di terminologia cloud nella piattaforma Azure hello

Glossario di Microsoft Azure Hello è un dizionario breve della terminologia di cloud per hello piattaforma Azure. Vedere anche la pagina relativa alla

* [Microsoft Azure e Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) - Definizioni dei servizi di Azure e delle rispettive controparti AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Terminologia del cloud computing](https://azure.microsoft.com/overview/cloud-computing-dictionary/) - Terminologia generale relativa al cloud.

## <a name="account"></a>account
Un account che ha utilizzato tooaccess e gestione una sottoscrizione di Azure. Spesso è indicato un Azure account anche se un account può essere uno di questi tooas: il lavoro esistente, dell'istituto di istruzione, o personale account Microsoft, o un nome utente di Office 365 e una password. È inoltre possibile creare un account toomanage una sottoscrizione di Azure quando effettua l'iscrizione per hello [versione di valutazione gratuita](https://azure.microsoft.com).  
Vedere [iscriversi per una sottoscrizione di Azure con l'account Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) e [account, è possibile utilizzare toosign in](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>App per le API
Nome alternativo per [app del servizio app](#app-service-app).

## <a name="app-service-app"></a>app del servizio app
Hello risorse di calcolo che [Azure App Service](app-service/app-service-value-prop-what-is.md) fornisce per l'hosting di un [sito o applicazione web](app-service-web/app-service-web-overview.md), [web API](app-service-api/app-service-api-apps-why-best-platform.md), o [back-end dell'app mobile](app-service-mobile/app-service-mobile-value-prop.md). Le applicazioni di servizio App sono anche cui tooas *servizi App*, *le app web*, *App per le API*, e *App per dispositivi mobili*.

## <a name="availability-set"></a>set di disponibilità
Una raccolta di macchine virtuali che vengono gestiti insieme l'affidabilità e la ridondanza di applicazione tooprovide. utilizzo di Hello un set di disponibilità garantisce che durante un evento di manutenzione pianificato o sia disponibile almeno una macchina virtuale.  
Vedere [gestione hello disponibilità delle macchine virtuali Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gestione hello disponibilità delle macchine virtuali Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>modello di distribuzione classica di Azure
Uno dei due [modelli di distribuzione](resource-manager-deployment-model.md) utilizzato toodeploy risorse in Azure (nuovo modello di hello è Azure Resource Manager). Alcuni servizi di Azure supportano solo modello di distribuzione di gestione delle risorse hello, alcuni browser supportano solo il modello di distribuzione classica hello e alcuni browser supportano entrambi. documentazione di Hello per ogni servizio di Azure consente di specificare quali modelli supportano.

## <a name="cli"></a>interfaccia della riga di comando di Azure
Un'interfaccia della riga di comando che possono essere utilizzati toomanage servizi di Azure da Windows, macOS e Linux.  Alcuni servizi o le funzionalità del servizio possono essere gestite solo tramite PowerShell o hello CLI. Vedere [Interfaccia della riga di comando di Azure 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Toomanage un'interfaccia della riga di comando di servizi Azure tramite una riga di comando dai PC Windows. Alcuni servizi o le funzionalità del servizio possono essere gestite solo tramite PowerShell o hello CLI.
Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>modello di distribuzione Azure Resource Manager
Uno dei due [modelli di distribuzione](resource-manager-deployment-model.md) utilizzato toodeploy risorse in Microsoft Azure (altri hello è il modello di distribuzione classica hello). Alcuni servizi di Azure supportano solo modello di distribuzione di gestione delle risorse hello, alcuni browser supportano solo il modello di distribuzione classica hello e alcuni browser supportano entrambi. documentazione di Hello per ogni servizio di Azure consente di specificare quali modelli supportano.

## <a name="fault-domain"></a>dominio di errore
raccolta di macchine virtuali in un set di disponibilità che probabilmente non riesca a hello stesso Hello ora. Un esempio è un gruppo di macchine virtuali in un rack che condividono un'unità di alimentazione e un commutatore di rete comune. In Azure, hello di macchine virtuali in un set di disponibilità sono automaticamente separate in più domini di errore.  
Vedere [gestione hello disponibilità delle macchine virtuali Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [gestione hello disponibilità delle macchine virtuali Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>area geografica
Limite definito per la residenza dei dati che contiene in genere due o più aree. limiti di Hello sia all'interno o oltre i confini e sono influenzati dal regolamentazione fiscale. Ogni area geografica include almeno un'area. Asia Pacifico e Giappone sono esempi di aree geografiche. Chiamata anche *geografia*.  
Vedere [Aree di Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>replica geografica
processo di Hello di automaticamente la replica del contenuto, ad esempio BLOB, tabelle e code all'interno di una coppia internazionale.  
Vedere [Replica geografica attiva per il database SQL di Azure](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>immagine
Un file che include il numero di macchine virtuali del sistema operativo hello e configurazione di applicazioni che può essere utilizzati toocreate. In Azure sono disponibili due tipi di immagini: l'immagine della macchina virtuale e l'immagine del sistema operativo. Un'immagine di macchina virtuale include un sistema operativo e tutti i dischi collegati macchina virtuale tooa quando viene creato l'immagine di hello. L'immagine del sistema operativo contiene solo un sistema operativo generalizzato senza configurazioni del disco dati.  
Vedere [Naviga e selezionare le immagini di macchina virtuale Windows in Azure con PowerShell o hello CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>limiti
numero di Hello di risorse che possono essere creati o hello benchmark delle prestazioni che possono essere ottenuti. I limiti sono in genere associati a sottoscrizioni, servizi e offerte.  
Vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>bilanciamento del carico
Risorsa che distribuisce il traffico in ingresso nei computer di una rete. In Azure, un bilanciamento del carico distribuisce macchine toovirtual traffico definite in un set di bilanciamento del carico. Il servizio di [bilanciamento del carico](load-balancer/load-balancer-overview.md) può essere connesso a Internet oppure interno.  

## <a name="mobile-app"></a>app per dispositivi mobili
Nome alternativo per [app del servizio app](#app-service-app).

## <a name="offer"></a>offer
prezzi di Hello, crediti e termini correlati applicabili tooan sottoscrizione di Azure.  
Vedere hello [pagina dettagli dell'offerta di Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
portale web sicura Hello utilizzato toodeploy e gestire i servizi Azure.  Sono disponibili due portali: hello [portale di Azure](http://portal.azure.com/) hello e [portale classico](http://manage.windowsazure.com/). Alcuni servizi sono disponibili in entrambi i portali, mentre altri sono disponibili in uno solo o hello altri. Hello [grafico disponibilità portale Azure](https://azure.microsoft.com/features/azure-portal/availability/) elenchi quali servizi sono disponibili in del portale.

## <a name="region"></a>region
Area all'interno di un'area geografica che non supera i confini nazionali e include uno o più data center. Prezzi, regionali e tipi di offerta vengono esposte a livello di area hello. Un'area in genere è associata a un'altra area, che può essere backup tooseveral centinaia di miglia da subito. Le coppie di aree possono essere usate come meccanismo per il ripristino di emergenza e gli scenari a disponibilità elevata. Definito anche tooas *percorso*.  
Vedere [Aree di Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>resource
Elemento incluso nella soluzione Azure. Ogni servizio di Azure consente toodeploy diversi tipi di risorse, quali database o le macchine virtuali.   
Vedere [Panoramica di Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>gruppo di risorse
Contenitore in Resource Manager che include le risorse correlate di un'applicazione. gruppo di risorse Hello può includere tutte le risorse di hello per un'applicazione o solo le risorse che sono raggruppate logicamente. È possibile decidere come risorse tooallocate tooresource gruppi basati su cosa hello più utile per l'organizzazione.  
Vedere [Panoramica di Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>modello di Resource Manager
Un file JSON che definisce in modo dichiarativo di una o più risorse di Azure e che definisce le dipendenze tra hello distribuite le risorse. modello di Hello può essere utilizzato toodeploy hello risorse ripetutamente e in modo coerente.  
Vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>provider di risorse
Un servizio che fornisce risorse hello è possibile distribuire e gestire tramite Gestione risorse. Ogni provider di risorse offre operazioni per l'utilizzo di risorse hello che vengono distribuite. I provider di risorse è possibile accedere tramite il portale di Azure, hello Azure PowerShell e gli SDK di programmazione diversi.  
Vedere [Panoramica di Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>role
Un modo per controllare l'accesso che può essere assegnato toousers, gruppi e i servizi. I ruoli sono in grado di tooperform azioni, ad esempio creare, gestire e continuare a leggere le risorse di Azure.  
Vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>contratto di servizio
accordo Hello che descrive gli impegni di Microsoft per la connettività e tempi di attività. Ogni servizio di Azure ha un contratto di servizio specifico.  
Vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>firma di accesso condiviso
Una firma che consente una risorsa di tooa toogrant limitato l'accesso, senza esporre la chiave dell'account. Ad esempio, [di archiviazione di Azure Usa SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooobjects di accesso client toogrant come BLOB. [IoT Hub Usa SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) dati di telemetria toogrant dispositivi autorizzazione toosend.

## <a name="storage-account"></a>archiviazione di Azure
Un account che consente di accedere ai servizi di Azure Blob, coda, tabella e File toohello in archiviazione di Azure. nome account di archiviazione Hello definisce lo spazio dei nomi univoco hello per gli oggetti di dati di archiviazione di Azure.  
Vedere [Informazioni sugli account di archiviazione di Azure](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>sottoscrizione
Contratto di un cliente con Microsoft che consente loro tooobtain Azure servizi. prezzi di sottoscrizione Hello e termini correlati vengono gestite con offerta hello scelto per la sottoscrizione di hello.
Vedere [Contratto di Sottoscrizione Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/) e [Associare le sottoscrizioni di Azure ad Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>tag
Un termine di indicizzazione che consente di toocategorize risorse in base a requisiti tooyour per la gestione o di fatturazione. Quando si dispone di un insieme complesso di risorse, è possibile utilizzare tag toovisualize tali risorse in modo più utile di hello hello. Ad esempio possibile contrassegnare le risorse che svolgono un ruolo simile all'interno dell'organizzazione o appartengono toohello stesso reparto.  
Vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>dominio di aggiornamento
raccolta di macchine virtuali in un set di disponibilità che vengono aggiornati in hello Hello contemporaneamente. Macchine virtuali in hello nello stesso dominio di aggiornamento vengono riavviate insieme durante la manutenzione pianificata. Azure non riavvia mai più di un dominio di aggiornamento Definito anche tooas un dominio di aggiornamento.  
Vedere [gestione hello disponibilità delle macchine virtuali Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gestione hello disponibilità delle macchine virtuali Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>macchina virtuale
implementazione di Hello software di un computer fisico che esegue un sistema operativo. Più macchine virtuali è possibile eseguire contemporaneamente in hello stesso hardware. In Azure sono disponibili macchine virtuali di dimensioni diverse.  
Vedere [Documentazione delle macchine virtuali](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>estensione macchina virtuale
Una risorsa che implementa i comportamenti o funzionalità che consentono uno altri programmi di lavoro o fornire il possibilità hello per toointeract con un computer in esecuzione. Ad esempio, è Impossibile utilizzare hello accesso alla VM estensione tooreset o modificare i valori di accesso remoto in una macchina virtuale di Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Vedere [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>rete virtuale
Rete che offre la connettività tra le risorse di Azure e che è isolata da tutti gli altri tenant di Azure. [Gateway VPN di Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) consente di stabilire connessioni tra reti virtuali e [tra una rete virtuale e una rete locale](vpn-gateway/vpn-gateway-plan-design.md). È possibile controllare completamente i blocchi di indirizzi IP hello, impostazioni DNS, i criteri di sicurezza e le tabelle di route all'interno di una rete virtuale.  
Vedere [Panoramica di Rete virtuale](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>app Web
Nome alternativo per [app del servizio app](#app-service-app).

## <a name="see-also"></a>Vedere anche

* [Inizia a usare Azure](https://azure.microsoft.com/get-started/)
* [Centro risorse cloud](https://azure.microsoft.com/resources/)  
* [Azure per le applicazioni aziendali](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure nel data center](https://azure.microsoft.com/overview/business-apps-on-azure/)

