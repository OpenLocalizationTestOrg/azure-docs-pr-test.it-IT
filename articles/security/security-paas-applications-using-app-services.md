---
title: aaaSecuring PaaS web e applicazioni per dispositivi mobili usando i servizi di App di Azure | Documenti Microsoft
description: " Informazioni sulle procedure consigliate della sicurezza di Servizi app di Azure per la protezione delle applicazioni Web PaaS e delle applicazioni per dispositivi mobili. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Protezione delle applicazioni Web PaaS e delle applicazioni per dispositivi mobili mediante i Servizi app di Azure

In questo articolo viene illustrato un insieme di procedure consigliate dei [Servizi App di Azure](https://azure.microsoft.com/services/app-service/) per la protezione delle applicazioni Web PaaS e delle applicazioni per dispositivi mobili. Queste procedure consigliate derivano dall'esperienza acquisita con Azure e l'esperienza dei clienti hello come manualmente.

## <a name="azure-app-services"></a>Servizi app di Azure
[Servizi App Azure](../app-service/app-service-value-prop-what-is.md) è un'offerta PaaS che consente di creare App web e dispositivi mobili per qualsiasi piattaforma o dispositivo e connettersi toodata ovunque e in locale o cloud hello. Servizi App include web hello e funzionalità per dispositivi mobili che sono state recapitate in precedenza separatamente come siti Web di Azure e servizi mobili di Azure. Include anche nuove funzionalità per l'automazione dei processi aziendali e l'hosting di API cloud. Come un unico servizio integrato, servizi App offre una vasta gamma di funzionalità scenari tooweb, mobili e l'integrazione.

toolearn, vedere Cenni preliminari su [App per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md) e [App Web](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Procedure consigliate

Quando si utilizza Servizi app, seguire queste procedure consigliate:

- [Eseguire l'autenticazione tramite Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). Servizi app fornisce un servizio OAuth 2.0 per il provider di identità. OAuth 2.0 è incentrato sulla semplicità di sviluppo client fornendo i flussi di autorizzazione specifici per le applicazioni Web, applicazioni desktop e telefoni cellulari. Azure AD Usa OAuth 2.0 tooenable si tooauthorize accesso toomobile e le applicazioni web.
- Limitare l'accesso in base alle tooknow necessità hello e i principi di sicurezza con privilegi minimi. Limitare l'accesso è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati. Controllo di accesso basato sui ruoli (RBAC) può essere utilizzato tooassign autorizzazioni toousers, gruppi e applicazioni in un determinato ambito. vedere toolearn più sulla concessione dell'accesso tooapplications, [Introduzione alla gestione di accesso](../active-directory/role-based-access-control-what-is.md).
- Proteggere le chiavi. Non importa quanto è valida la sicurezza impostata se si perdono le chiavi di sottoscrizione. L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud. Con l'insieme di credenziali delle chiavi è possibile crittografare chiavi e segreti (ad esempio, chiavi di autenticazione, chiavi dell'account di archiviazione, chiavi di crittografia dati, file PFX e password) usando chiavi protette da moduli di protezione hardware (HSM). Per una maggiore sicurezza, è possibile importare o generare le chiavi in moduli di protezione hardware. Vedere [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md) toolearn altre. È inoltre possibile utilizzare insieme di credenziali chiave toomanage i certificati TLS con rinnovo automatico.
- Limitare gli indirizzi IP di origine in ingresso. [Ambiente del servizio app](../app-service-web/app-service-app-service-environment-intro.md) dispone di una funzionalità di integrazione di rete virtuale che consente di limitare gli indirizzi origine IP di origine in ingresso tramite gruppi di sicurezza di rete (NSG). Se non si ha familiarità con le reti virtuali di Azure (Vnet), questa è una funzionalità che consente di tooplace molte delle risorse di Azure in una rete instradabile su internet non che è possibile controllare l'accesso a. vedere, più toolearn [integrare l'app con una rete virtuale di Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha introdotto tooa insieme di servizi App le procedure consigliate per proteggere il PaaS web e applicazioni per dispositivi mobili. toolearn più sulla protezione di distribuzioni PaaS, vedere:

- [Protezione delle distribuzioni PaaS](security-paas-deployments.md)
- [Protezione di applicazioni Web PaaS Eeb e di applicazioni per dispositivi mobili utilizzando il database SQL Azure e SQL Data Warehouse](security-paas-applications-using-sql.md)
