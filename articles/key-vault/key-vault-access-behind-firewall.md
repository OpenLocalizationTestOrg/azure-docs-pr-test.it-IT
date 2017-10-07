---
title: insieme di credenziali chiave di aaaAccess dietro un firewall | Documenti Microsoft
description: Informazioni su come tooaccess Azure chiave dell'insieme di credenziali da un'applicazione di un firewall
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Accedere a Insieme di credenziali delle chiavi di Azure protetto da firewall
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>D: nel applicazione client insieme di credenziali delle chiavi deve toobe dietro un firewall. Quali porte, gli host o degli indirizzi IP è necessario aprire tooenable accesso tooa chiave dell'insieme di credenziali?
tooaccess un insieme di credenziali chiave, l'applicazione client insieme di credenziali delle chiavi ha tooaccess più endpoint per varie funzionalità:

* Autenticazione tramite Azure Active Directory (Azure AD).
* Gestione di Insieme di credenziali delle chiavi di Azure, inclusa la creazione, la lettura, l'aggiornamento, l'eliminazione e l'impostazione dei criteri di accesso tramite Azure Resource Manager.
* L'accesso e la gestione degli oggetti (chiavi e segreti) archiviati nell'insieme di credenziali chiave stessa, passando hello endpoint specifico insieme di credenziali chiave (ad esempio, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Esistono alcune varianti a seconda della configurazione e dell'ambiente.   

## <a name="ports"></a>Porte
Passa tutti traffico tooa chiave dell'insieme di credenziali per tutte le tre funzioni (accesso piano autenticazione, la gestione e dati) su HTTPS: la porta 443. Verrà tuttavia generato occasionalmente traffico HTTP (porta 80) per CRL. I client che supportano OCSP non devono raggiungere CRL, ma possono in alcuni casi raggiungere [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Autenticazione
Le applicazioni client di chiave dell'insieme di credenziali necessario tooaccess gli endpoint di Azure Active Directory per l'autenticazione. endpoint Hello utilizzato dipende hello configurazione tenant di Azure AD, il tipo di hello di entità (entità utente o dell'entità servizio) e hello tipo di account, ad esempio, un account Microsoft o un lavoro o scuola account.  

| Tipo di entità | Endpoint:porta |
| --- | --- |
| Utente che usa un account Microsoft<br> (ad esempio, user@hotmail.com) |**Globale:**<br> login.microsoftonline.com:443<br><br> **Azure per la Cina:**<br> login.chinacloudapi.cn:443<br><br>**Azure per enti pubblici statunitensi:**<br> login-us.microsoftonline.com:443<br><br>**Azure per la Germania:**<br> login.microsoftonline.de:443<br><br> e <br>login.live.com:443 |
| Utente o entità servizio utilizzando un account aziendale o dell'istituto di istruzione con Azure Active Directory (ad esempio, user@contoso.com) |**Globale:**<br> login.microsoftonline.com:443<br><br> **Azure per la Cina:**<br> login.chinacloudapi.cn:443<br><br>**Azure per enti pubblici statunitensi:**<br> login-us.microsoftonline.com:443<br><br>**Azure per la Germania:**<br> login.microsoftonline.de:443 |
| Utente o entità servizio utilizzando un lavoro o account dell'istituto di istruzione, oltre a Active Directory Federation Services (ADFS) o altri endpoint federato (ad esempio, user@contoso.com) |Tutti gli endpoint per un account aziendale o dell'istituto di istruzione oltre ad AD FS o altri endpoint federati |

Esistono altri possibili scenari complessi. Fare riferimento troppo[flusso l'autenticazione di Azure Active Directory](/documentation/articles/active-directory-authentication-scenarios/), [integrazione di applicazioni con Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), e [protocolli di autenticazione di Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Per ulteriori informazioni.  

## <a name="key-vault-management"></a>Gestione dell'insieme di credenziali delle chiavi
Per la gestione di insieme di credenziali chiave (CRUD e l'impostazione di criteri di accesso), un'applicazione client insieme di credenziali chiave hello deve tooaccess un endpoint di gestione risorse di Azure.  

| Tipo di operazione | Endpoint:porta |
| --- | --- |
| Operazioni del piano di controllo dell'insieme di credenziali delle chiavi<br> tramite Azure Resource Manager |**Globale:**<br> management.azure.com:443<br><br> **Azure per la Cina:**<br> management.chinacloudapi.cn:443<br><br> **Azure per enti pubblici statunitensi:**<br> management.usgovcloudapi.net:443<br><br> **Azure per la Germania:**<br> management.microsoftazure.de:443 |
| API Graph di Azure Active Directory |**Globale:**<br> graph.windows.net:443<br><br> **Azure per la Cina:**<br> graph.chinacloudapi.cn:443<br><br> **Azure per enti pubblici statunitensi:**<br> graph.windows.net:443<br><br> **Azure per la Germania:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operazioni dell'insieme di credenziali delle chiavi
Per la gestione di oggetti (chiavi e segreti) insieme di credenziali chiave e le operazioni di crittografia, il client di insieme di credenziali chiave hello deve endpoint insieme di credenziali chiave di tooaccess hello. suffisso DNS di endpoint Hello varia a seconda della posizione di hello di credenziali delle chiavi. endpoint dell'insieme di credenziali chiave Hello è in formato hello *nome insieme di credenziali*. *suffisso dns di specifico area*, come descritto in hello nella tabella seguente.  

| Tipo di operazione | Endpoint:porta |
| --- | --- |
| Operazioni come crittografia sulle chiavi; creazione, lettura, aggiornamento ed eliminazione di chiavi e segreti; impostazione o definizione di tag e altri attributi per gli oggetti dell'insieme di credenziali delle chiavi (chiavi o segreti) |**Globale:**<br> &lt;nome-insiemecredenziali&gt;.vault.azure.net:443<br><br> **Azure per la Cina:**<br> &lt;nome-insiemecredenziali&gt;.vault.azure.cn:443<br><br> **Azure per enti pubblici statunitensi:**<br> &lt;nome-insiemecredenziali&gt;.vault.usgovcloudapi.net:443<br><br> **Azure per la Germania:**<br> &lt;nome-insiemecredenziali&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Intervalli di indirizzi IP
servizio insieme di credenziali chiave Hello Usa altre risorse di Azure come infrastruttura PaaS. È pertanto possibile tooprovide un specifico intervallo di indirizzi IP che insieme di credenziali chiave gli endpoint del servizio avrà in qualsiasi momento particolare. Se il firewall supporta solo gli intervalli di indirizzi IP, fare riferimento toohello [intervalli IP Data Center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653) documento. Per l'autenticazione e identità (Azure Active Directory), l'applicazione deve essere in grado di tooconnect toohello endpoint descritti in [gli indirizzi di autenticazione e identità](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Passaggi successivi
In caso di domande sull'insieme di credenziali chiave, visitare hello [forum di insieme di credenziali chiave di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

