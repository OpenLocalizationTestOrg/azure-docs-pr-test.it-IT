---
title: aaaOverview di Azure Active Directory Domain Services | Documenti Microsoft
description: Panoramica dei Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Servizi di dominio Azure Active Directory
## <a name="overview"></a>Panoramica
Servizi di infrastruttura di Azure consentono di toodeploy un'ampia gamma di soluzioni di elaborazione in modo agile. Con macchine virtuali di Azure, è possibile distribuire quasi istantaneamente e si paga solo per minuto hello. Grazie al supporto per Windows, Linux, SQL Server, Oracle, IBM, SAP e BizTalk, è possibile distribuire qualsiasi carico di lavoro e qualunque linguaggio su quasi tutti i sistemi operativi. Questi vantaggi consentono toomigrate legacy applicazioni distribuite in locale tooAzure, toosave in spese operative.

Un aspetto essenziale di migrazione locale tooAzure applicazioni gestisce esigenze identità hello di queste applicazioni. Applicazioni basate su directory possono basati su LDAP per l'accesso in lettura o scrittura toohello directory aziendale o si basano sull'autenticazione integrata di Windows (autenticazione Kerberos o NTLM) tooauthenticate fine utenti. Le applicazioni line-of-business (LOB) in esecuzione in Windows Server vengono in genere distribuite in computer aggiunti a un dominio e quindi essere gestite in modo sicuro tramite Criteri di gruppo. too'lift MAIUSC ' cloud toohello di applicazioni locali, queste dipendenze sull'infrastruttura di identità aziendale hello necessario toobe risolto.

Gli amministratori spesso attivare tooone di hello seguenti soluzioni toosatisfy hello identità esigenze delle applicazioni distribuite in Azure:

* Distribuire una connessione VPN da sito a sito tra i carichi di lavoro in esecuzione in servizi di infrastruttura di Azure e hello directory aziendale locale.
* Estendere l'infrastruttura di dominio o foresta di Active Directory aziendale hello impostando i controller di dominio di replica utilizzando macchine virtuali di Azure.
* Distribuzione di un dominio autonomo in Azure tramite controller di dominio distribuiti come macchine virtuali di Azure.

Tutti questi approcci tuttavia prevedono costi elevati e un carico di lavoro amministrativo significativo. Gli amministratori sono controller di dominio richiesto toodeploy utilizzando macchine virtuali in Azure. È inoltre necessario toomanage, protetta, patch, monitoraggio, backup e risolvere i problemi relativi a queste macchine virtuali. l'affidabilità Hello toohello le connessioni VPN locale directory fa sì che i carichi di lavoro distribuiti in problemi di rete di Azure toobe tootransient vulnerabile o interruzioni del servizio. Queste interruzioni di rete determinano tempi di attività inferiori e affidabilità ridotta delle applicazioni.

È stato progettato tooprovide di servizi di dominio Active Directory di Azure un'alternativa più semplice.

## <a name="introducing-azure-ad-domain-services"></a>Introduzione a Servizi di dominio Azure AD
Servizi di dominio Azure Active Directory offre servizi di dominio gestiti, ad esempio aggiunta a un dominio, Criteri di gruppo, LDAP e autenticazione Kerberos/NTLM, completamente compatibili con Windows Server Active Directory. Si utilizzano questi servizi di dominio senza necessità di hello di si toodeploy, gestire e patch per i controller di dominio nel cloud hello. Servizi di dominio Active Directory di Azure si integra con tenant di Azure AD esistente, rendendo in tal modo possibile per gli utenti toolog utilizzando le credenziali aziendali. Inoltre, è possibile utilizzare i gruppi esistenti e tooresources di accesso toosecure gli account utente, garantendo un più uniforme 'accuratezza di spostamento e' di on-premise risorse tooAzure servizi di infrastruttura.

La funzionalità Servizi di dominio Azure Active Directory funziona perfettamente a prescindere dal fatto che il tenant Azure AD sia di tipo solo cloud o sincronizzato con l'istanza di Active Directory locale.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Servizi di dominio Azure AD per le organizzazioni solo cloud
Un annuncio di Azure solo cloud tenant (spesso cui tooas ' gestito tenant') non dispone di un footprint di identità locale. In altre parole, gli account utente, le password e appartenenze a gruppi sono tutti i cloud toohello native -, creati e gestiti in Azure AD. Si supponga che Contoso sia un tenant Azure AD solo cloud. Come illustrato nella seguente figura hello, amministratore di Contoso ha configurato una rete virtuale in servizi di infrastruttura di Azure. I carichi di lavoro di server e applicazioni sono distribuiti in questa rete virtuale in macchine virtuali di Azure. Poiché Contoso è un tenant solo cloud, tutte le identità degli utenti, le relative credenziali e le appartenenze ai gruppi sono create e gestite in Azure.

![Panoramica di Servizi di dominio Azure AD](./media/active-directory-domain-services-overview/aadds-overview.png)

Contoso amministratore IT può abilitare i servizi di dominio Azure Active Directory per i tenant di Azure AD e scegliere toomake servizi di dominio disponibili in questa rete virtuale. Successivamente, servizi di dominio Active Directory di Azure esegue il provisioning di un dominio gestito e lo rende disponibile nella rete virtuale hello. Tutti gli account utente, le appartenenze ai gruppi e le credenziali utente disponibili nel tenant Azure AD di Contoso sono anche disponibili in questo dominio appena creato. Questa funzionalità consente agli utenti in hello organizzazione toosign toohello dominio utilizzando le credenziali aziendali, ad esempio, quando ci si connette in remoto toodomain appartenenti a un computer tramite Desktop remoto. Gli amministratori possono eseguire il provisioning di accesso tooresources nel dominio hello tramite appartenenze a gruppi esistenti. Applicazioni distribuite in macchine virtuali nella rete virtuale hello possono usare funzionalità quali l'aggiunta al dominio, LDAP lettura, LDAP bind, autenticazione NTLM e Kerberos e criteri di gruppo.

Di seguito sono riportati alcuni aspetti salienti di hello un dominio gestito che viene eseguito il provisioning da servizi di dominio Active Directory di Azure:

* Contoso amministratore IT non è necessario toomanage, patch o monitorare questo dominio o controller di dominio per il dominio gestito.
* Non sussiste alcuna replica toomanage AD necessario per questo dominio. Gli account utente, le appartenenze ai gruppi e le credenziali del tenant Azure AD di Contoso sono automaticamente disponibili all'interno del dominio gestito.
* Poiché il dominio hello è gestito da Azure AD servizi di dominio Contoso amministratore IT non dispone di privilegi di amministratore di dominio o l'amministratore dell'organizzazione in questo dominio.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Servizi di dominio Azure AD per le organizzazioni ibride
Le organizzazioni con un'infrastruttura IT ibrida utilizzano una combinazione di risorse cloud e risorse locali. Queste organizzazioni di sincronizzare le informazioni di identità dal loro tenant di Azure AD tootheir directory locale. Così come le organizzazioni ibrida toomigrate più di cloud toohello applicazioni on-premise, soprattutto directory compatibile con le applicazioni legacy, servizi di dominio Active Directory di Azure possono essere utile toothem.

Litware Corporation ha distribuito [Azure AD Connect](../active-directory/active-directory-aadconnect.md), informazioni sulle identità toosynchronize al proprio tenant di Azure AD tootheir directory locale. informazioni di identità Hello sono sincronizzate includono gli account utente, gli hash delle credenziali per l'autenticazione (sincronizzazione della password) e le appartenenze.

> [!NOTE]
> **La sincronizzazione delle password è obbligatoria per ibrida organizzazioni toouse servizi di dominio AD Azure**. Questo requisito è perché sono necessarie le credenziali degli utenti in hello gestito dominio forniti da servizi di dominio di Active Directory di Azure, tooauthenticate questi utenti tramite i metodi di autenticazione NTLM o Kerberos.
>
>

![Servizi di dominio Azure AD per Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hello precedente viene illustrato come le organizzazioni con una configurazione ibrida infrastruttura IT, ad esempio Litware Corporation, possono utilizzare servizi di dominio Active Directory di Azure. I carichi di lavoro di server e applicazioni di Litware che richiedono i servizi di dominio sono distribuiti in una rete virtuale nei servizi di infrastruttura di Azure. Del Litware amministratore IT può abilitare i servizi di dominio Azure Active Directory per i tenant di Azure AD e scegliere toomake un dominio gestito disponibile in questa rete virtuale. Poiché Litware è un'organizzazione con un'infrastruttura IT ibrido, le credenziali, gruppi e account utente vengono sincronizzati tootheir AD Azure tenant dalla directory locale. Questa funzionalità consente agli utenti toosign toohello dominio utilizzando le credenziali aziendali, ad esempio, durante la connessione remota toomachines aggiunti a un dominio toohello tramite Desktop remoto. Gli amministratori possono eseguire il provisioning di accesso tooresources nel dominio hello tramite appartenenze a gruppi esistenti. Applicazioni distribuite in macchine virtuali nella rete virtuale hello possono usare funzionalità quali l'aggiunta al dominio, LDAP lettura, LDAP bind, autenticazione NTLM e Kerberos e criteri di gruppo.

Di seguito sono riportati alcuni aspetti salienti di hello un dominio gestito che viene eseguito il provisioning da servizi di dominio Active Directory di Azure:

* dominio gestito Hello è autonomo. Non si tratta di un'estensione del dominio locale di Litware.
* Del Litware amministratore IT non è necessario toomanage, patch o controller di dominio di monitoraggio per questo dominio gestito.
* Non è presente alcun dominio di toothis replica toomanage AD necessità. Account utente, appartenenza al gruppo e le credenziali dalla directory locale di Litware sono sincronizzati tooAzure Active Directory tramite Azure AD Connect. Questi account utente, l'appartenenza al gruppo e le credenziali sono automaticamente disponibili nel dominio gestito hello.
* Perché il dominio hello è gestito dal dominio servizi di Azure AD, Litware amministratore IT non dispone di privilegi di amministratore di dominio o l'amministratore dell'organizzazione in questo dominio.

## <a name="benefits"></a>Vantaggi
Con i servizi di dominio Active Directory di Azure, è possibile utilizzare hello seguenti vantaggi:

* **Semplice** : È in grado di soddisfare esigenze di hello identità delle macchine virtuali distribuiti servizi di infrastruttura tooAzure con pochi semplici clic. Non è necessario toodeploy e gestire l'infrastruttura di identità in Azure o il programma di installazione connettività tooyour indietro identità infrastruttura locale.
* **Integrazione** : Servizi di dominio Azure AD è strettamente integrato con il tenant Azure AD. È ora possibile utilizzare Azure AD di una directory aziendale integrato basato su cloud che si occupa delle esigenze toohello tradizionali applicazioni compatibili con directory sia le applicazioni moderne.
* **Compatibile** : servizi di dominio Azure Active Directory si basa su un'infrastruttura di livello aziendale si basa sulla collaudata di hello di Windows Server Active Directory. Di conseguenza, le applicazioni possono dipendere da un più alto livello di compatibilità con le funzionalità di Windows Server Active Directory. Non tutte le funzionalità disponibili in Windows Server Active Directory sono attualmente disponibili in Servizi di dominio Azure AD. Tuttavia, le funzionalità disponibili sono compatibili con funzionalità Windows Server Active Directory corrispondenti hello che affidarsi nell'infrastruttura locale. Hello LDAP, Kerberos, NTLM, criteri di gruppo e dominio funzioni join costituiscono un'offerta avanzata che è stata testata e perfezionata su varie versioni di Windows Server.
* **Economica** – con servizi di dominio AD Azure, è possibile evitare l'onere di gestione e infrastruttura hello associata alla gestione delle identità infrastruttura toosupport directory compatibile con le applicazioni tradizionali. È possibile spostare questi tooAzure applicazioni, servizi di infrastruttura e trarre vantaggio da un maggiore risparmio in spese operative.
