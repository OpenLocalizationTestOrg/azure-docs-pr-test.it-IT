---
title: tipo aaaWhat dei sistemi di raccolta sono necessari per Azure RemoteApp? | Microsoft Docs
description: Informazioni sui tipi di hello delle raccolte disponibili con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Tipi di raccolte disponibili per Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp consente di condividere applicazioni e risorse con utenti su qualsiasi dispositivo. A tale scopo occorre la creazione di risorse e raccolte toohold hello App, e quindi si condividono tali raccolte con gli utenti. Esistono 2 diverse opzioni per le raccolte con opzioni differenti per la rete e l'autenticazione. Qual è quella appropriata per ogni esigenza?

Si analizzerà diverse considerazioni hello e scelte toomake tooget hello di frequente da una raccolta di Azure RemoteApp. 

## <a name="quick-differences-between-hello-collection-types"></a>Rapide differenze tra tipi di raccolta hello
|  | Cloud | Ibrido |
| --- | --- | --- |
| Usa una rete virtuale esistente |Sì |Sì |
| Richiede account connessi ad Active Directory (DirSync) |No |Sì |
| Richiede l'aggiunta al dominio |No |Sì |
| Richiede tooVNET accessibile controller di dominio |No |Sì |

## <a name="cloud-collections"></a>Raccolte nel cloud
* Toocreate rapido - raccolta hello è rapidamente il provisioning, vale a dire che le app toousers accedere più velocemente.
* Applicazioni proprie o condivisione delle applicazioni predefinite. È possibile utilizzare un'immagine personalizzata (creata da una macchina virtuale di Azure) o una delle immagini hello incluse con la sottoscrizione.
* Non è necessario tooconfigure una connessione tra la raccolta e il dominio locale.
* Ma è possibile utilizzare facoltativamente il proprio accesso tooprovide di rete virtuale di Azure nell'ambiente locale per l'autenticazione di Windows non toouse o di condivisione di dati in risorse di SQL Server (utilizzando l'autenticazione del database).

Come si crea una raccolta?

* Solo cloud? Crea con hello **creazione rapida** opzione nel portale di hello.
* Cloud + rete virtuale? Creare utilizzando hello **Create con una rete virtuale** opzione ma non si sceglie toojoin un dominio.

## <a name="hybrid-collections"></a>Raccolte ibride
* Fornire una rete locale tooon accesso completo + rete virtuale di Azure.
* Include l'accesso con aggiunta al dominio per applicazioni e dati. Le applicazioni remote possono eseguire l'autenticazione in Active Directory in locale e possono quindi accedere alle risorse nel dominio.
* Abilitare il monitoraggio e la gestione avanzati con soluzioni System Center e Criteri di gruppo di Windows esistenti (tramite un'immagine personalizzata creata in Windows Server 2012 R2)
* Supporto [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour la rete virtuale di Azure tra reti VIRTUALI locali.

Creare utilizzando hello **Create con una rete virtuale** opzione e scegliere toojoin un dominio.

## <a name="authentication-options"></a>Opzioni di autenticazione
Azure RemoteApp supporta sia account Microsoft che account Azure Active Directory, ma non tutte le raccolte supportano tutti i metodi. 

| Tipo di account |  | Cloud | Cloud + rete virtuale | Ibrido |
| --- | --- | --- | --- | --- |
| Account Microsoft | |Sì |Sì |No |
| Azure Active Directory (Azure AD) | | | | |
| Solo Azure AD |Sì |Sì |No | |
| AD Connect con sincronizzazione password |Sì |Sì |Sì | |
| AD Connect senza sincronizzazione password |Sì |Sì |No | |
| AD Connect con AD FS |Sì |Sì |Sì | |
| Provider di identità di terze parti supportati da Azure (come Ping) |Sì |Sì |Sì | |
| Autenticazione a più fattori | |Sì |Sì |Sì |

### <a name="cloud-and-cloud--vnet"></a>Cloud e Cloud + rete virtuale
Con le raccolte di cloud, è possibile utilizzare gli account Microsoft, gli account di Azure AD o una combinazione di due hello. Utilizzare gli account di hello che funzionano meglio per gli utenti.

Non sono previsti requisiti specifici per l'uso di account Microsoft. 

Se si desidera toouse account di Azure AD, è necessario verificare che il tenant di Azure AD corrisponda hello uno associati alla sottoscrizione toomake. Quando si crea la sottoscrizione di Azure RemoteApp, si utilizzava tenant di Azure AD di hello è automaticamente associato alla sottoscrizione. Qualsiasi utente di Azure AD assegnare autorizzazioni tooneeds toobe lo stesso tenant. Se necessario, è possibile [modificare tenant di Azure AD hello](remoteapp-changetenant.md) associati alla sottoscrizione.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Ibrido (o cloud + Azure AD + Active Directory)
L'uso di Azure AD insieme ad Active Directory in locale è un prerequisito per una raccolta ibrida. È necessario toouse AD Connect toointegrate hello due directory. Ma è alcune scelte per quanto riguarda toohow configuri AD Connect. 

Esistono due scenari per AD Connect, ovvero l'uso della sincronizzazione delle password o l'uso della federazione di Active Directory. Estrarre hello [informazioni di Active Directory Connect](../active-directory/active-directory-aadconnect.md) toofigure quale di questi è adatto per l'utente.

È inoltre possibile usare Azure AD e Active Directory con una raccolta nel cloud. Assicurarsi di che seguire hello stessi passaggi di impostazione.

Estrarre [Azure AD + requisiti di Active Directory per Azure RemoteApp](remoteapp-ad.md) per tooconfigure necessari passaggi di hello Azure AD e Active Directory.

## <a name="go-create-your-collection"></a>A questo punto è possibile procedere
OK, ritengo che è stato calcolato a questo punto, pertanto non c'è toodo a sinistra di una sola operazione - creare la prima raccolta di Azure RemoteApp.

[Creare una raccolta nel cloud](remoteapp-create-cloud-deployment.md) o [creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md).

