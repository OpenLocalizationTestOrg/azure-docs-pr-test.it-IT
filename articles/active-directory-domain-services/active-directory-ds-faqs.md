---
title: aaaFAQs - servizi di dominio di Azure Active Directory | Documenti Microsoft
description: Domande frequenti su Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Servizi di dominio Azure Active Directory: domande frequenti
Questa pagina risponde alle domande frequenti su Azure Active Directory Domain Services hello. Controllarla costantemente per eventuali aggiornamenti.

### <a name="troubleshooting-guide"></a>Guida per la risoluzione dei problemi
Fare riferimento tooour [Troubleshooting guide](active-directory-ds-troubleshooting.md) per soluzioni toocommon problemi durante la configurazione o amministrazione dei servizi di dominio Active Directory di Azure.

### <a name="configuration"></a>Configurazione
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>È possibile creare più domini per una singola directory di Azure AD?
No. È possibile creare solo un singolo dominio gestito da Servizi di dominio Azure AD per una singola directory di Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>È possibile abilitare Active Directory Domain Services in una rete virtuale di Azure Resource Manager?
No. È possibile abilitare Azure AD Domain Services soltanto in una rete virtuale di Azure classica. È possibile connettersi hello rete virtuale classica tooa Gestione risorse rete virtuale usando toouse peering di rete virtuale il dominio in una rete virtuale di gestione delle risorse gestito.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>È possibile abilitare Azure AD Domain Services in una directory di Azure AD federata? Usare gli utenti tooauthenticate ADFS per l'accesso tooOffice 365. È possibile abilitare Azure AD Domain Services per questa directory?
No. Servizi di dominio Active Directory di Azure è necessario accedere toohello gli hash delle password di account utente, gli utenti tooauthenticate tramite NTLM o Kerberos. In una directory federativa, gli hash delle password non vengono archiviati nella directory di Azure AD hello. Azure AD Domain Services, di conseguenza, non funziona con questi tipi di directory di Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>È possibile rendere disponibile Servizi di dominio Azure AD in più reti virtuali all'interno della sottoscrizione?
servizio Hello stesso non supporta direttamente in questo scenario. Servizi di dominio Azure AD è disponibile in una sola rete virtuale alla volta. Tuttavia, è possibile configurare la connettività tra più reti virtuali tooexpose servizi di dominio Active Directory di Azure tooother reti virtuali. Questo articolo descrive come [connettere più reti virtuali in Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>È possibile abilitare Servizi di dominio Azure AD con PowerShell?
PowerShell e la distribuzione automatizzata di Servizi di dominio Azure AD non sono attualmente disponibili.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>È disponibile nel nuovo portale di Azure hello servizi di dominio Active Directory di Azure?
No. Servizi di dominio Active Directory di Azure possono essere configurati solo in hello [portale di Azure classico](https://manage.windowsazure.com). È previsto il supporto per hello tooextend [portale di Azure](https://portal.azure.com) in hello future.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>È possibile aggiungere controller tooan servizi di dominio Active Directory di Azure gestito dominio?
No. dominio Hello fornito da servizi di dominio Active Directory di Azure è un dominio gestito. Non è necessario tooprovision, configurare o gestire in altro modo il controller di dominio per questo dominio, queste attività vengono fornite come un servizio da Microsoft di gestione. Pertanto, è possibile aggiungere il controller di dominio aggiuntivi (lettura / scrittura o sola lettura) per il dominio gestito hello.

### <a name="administration-and-operations"></a>Amministrazione e gestione
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>È possibile collegare toohello controller di dominio per il dominio gestito tramite Desktop remoto?
No. Non si dispone delle autorizzazioni tooconnect toodomain controller hello gestito dominio tramite Desktop remoto. I membri del gruppo 'Administrators di controller di dominio di AAD' hello possono amministrare hello dominio gestiti tramite gli strumenti di amministrazione di Active Directory, ad esempio Active Directory amministrazione centro hello o PowerShell di Active Directory. Questi strumenti vengono installati tramite hello 'Server strumenti di amministrazione remota' funzionalità in un server Windows aggiunti a un dominio gestito toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Dopo aver abilitato Servizi di dominio Azure AD, Quale account utente utilizza toodomain aggiunta a un dominio toothis macchine?
I membri del gruppo amministrativo hello 'Administrators di controller di dominio di AAD' possono macchine aggiunta al dominio. Inoltre, i membri di questo gruppo vengono concesse toomachines accesso desktop remoto che sono stati toohello aggiunti a un dominio.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Dispone dei privilegi di amministratore di dominio per il dominio gestito di hello fornita da servizi di dominio Active Directory di Azure?
No. Non vengono concessi privilegi amministrativi nel dominio gestito hello. Privilegi sia ' amministratore di dominio ' e ' amministratore dell'organizzazione ' non sono disponibili per toouse all'interno di dominio hello. Amministratore di dominio esistente o gruppi di amministratori dell'organizzazione all'interno della directory di Azure AD anche non vengono concessi privilegi di amministratore di dominio o aziendale nel dominio hello.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>È possibile modificare l'appartenenza ai gruppi usando il protocollo LDAP o altri strumenti di amministrazione di AD nei domini gestiti?
No. Le appartenenze ai gruppi non possono essere modificate nei domini gestiti da Servizi di dominio Azure AD. Hello che stesso vale per gli attributi utente. È tuttavia possibile modificare le appartenenze ai gruppi o gli attributi utente in Azure AD o nel dominio locale. Tali modifiche vengono automaticamente sincronizzate tooAzure AD servizi di dominio.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Quanto tempo occorre per le modifiche si rende visibile toomy Azure Active directory toobe nel mio dominio gestito?
Le modifiche apportate nella directory di Azure AD con hello dell'interfaccia utente AD Azure o PowerShell sono sincronizzati tooyour di dominio gestiti. Questo processo di sincronizzazione viene eseguito in background di hello. Una volta completata la sincronizzazione iniziale monouso hello della directory, viene in genere richiede circa 20 minuti per le modifiche apportate in Azure AD toobe riflesse nel dominio gestito.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>È possibile estendere schema hello di hello dominio gestito fornito da servizi di dominio Active Directory di Azure?
No. schema di Hello è amministrato da Microsoft per il dominio gestito hello. Le estensioni dello schema non sono supportate da Servizi di dominio Azure Active Directory.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>È possibile modificare o aggiungere record DNS nel domino gestito?
Sì. I membri del gruppo di hello 'AAD DC Administrators' vengono concessi privilegi di amministratore DNS ', toomodify record DNS nel dominio gestito hello. In un computer in esecuzione Windows Server toohello aggiunti a un dominio gestito, toomanage DNS possono utilizzare console Gestore DNS hello. hello toouse console Gestore DNS, installare 'Gli strumenti Server DNS', che fa parte della funzionalità facoltativa di hello 'Strumenti amministrazione remota del Server' nel server di hello. Altre informazioni sulle [utilità di amministrazione, monitoraggio e risoluzione dei problemi DNS](https://technet.microsoft.com/library/cc753579.aspx) sono disponibili su TechNet.

### <a name="billing-and-availability"></a>Fatturazione e disponibilità
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Servizi di dominio Azure AD è a pagamento?
Sì. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>È disponibile una versione di valutazione gratuita per servizio hello?
Questo servizio è incluso nella versione di valutazione gratuita hello per Azure. È possibile iscriversi per una [valutazione gratuita di un mese di Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>È possibile ottenere Servizi di dominio Azure AD come parte di Enterprise Mobility Suite (EMS)? È necessario servizi di dominio toouse Azure AD di Azure AD Premium?
No. Azure Active Directory Domain Services è un servizio di Azure con pagamento in base al consumo e non fa parte di EMS. Servizi di dominio AD Azure può essere usato con tutte le edizioni di Azure AD (gratuito, Basic e Premium). La fatturazione avviene su base oraria, a seconda dell'uso.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Le aree di Azure è disponibile nel servizio di hello?
Fare riferimento toohello [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/) toosee pagina un elenco di hello aree di Azure in cui i servizi di dominio Active Directory di Azure è disponibili.
