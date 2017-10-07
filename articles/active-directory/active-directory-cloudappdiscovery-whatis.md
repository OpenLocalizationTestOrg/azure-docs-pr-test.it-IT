---
title: le applicazioni cloud a Cloud App Discovery non gestita di aaaFinding | Documenti Microsoft
description: Fornisce informazioni sulla ricerca e la gestione delle applicazioni con Cloud App Discovery, quali sono i vantaggi di hello e sul relativo funzionamento.
services: active-directory
keywords: cloud app discovery, gestione delle applicazioni
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Ricerca di applicazioni cloud non gestite con Cloud App Discovery
## <a name="overview"></a>Panoramica
Nelle aziende moderne i reparti IT spesso non sono a conoscenza di tutte le applicazioni cloud hello che i membri dell'organizzazione di utilizzare toodo il proprio lavoro. È facile toosee perché gli amministratori avranno preoccupazioni dati toocorporate di accesso non autorizzato, perdita di dati e altri rischi di protezione. A causa di questa mancanza di consapevolezza, la creazione di un piano per la gestione dei rischi per la sicurezza potrebbe sembrare complicata.

Cloud App Discovery è una funzionalità Premium di Azure Active Directory (AD) che consente applicazioni cloud toodiscover in uso da parte di persone hello all'interno dell'organizzazione.

**Cloud App Discovery consente di:**

* Trovare le applicazioni cloud hello in uso e misurarne dal numero di utenti, volume di traffico o un numero di applicazione toohello di richieste web.
* Identificare gli utenti di hello che usano un'applicazione.
* Esportare i dati per analisi offline.
* Portare le applicazioni sotto il controllo IT e abilitare la funzionalità Single Sign-On per la gestione degli utenti.

## <a name="how-it-works"></a>Funzionamento
1. Gli agenti di utilizzo dell'applicazione vengono installati nei computer dell'utente.
2. informazioni sull'utilizzo di applicazione Hello acquisite dagli agenti hello viene inviate tramite un servizio cloud app discovery di canale crittografato protetto toohello.
3. Hello servizio Cloud App Discovery valuta dati hello e genera i report.

![Diagramma di Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

tooget a usare Cloud App Discovery, vedere [Guida introduttiva a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Articoli correlati
* [Considerazioni sulla sicurezza e sulla privacy in Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Guida alla distribuzione di criteri di gruppo di Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Guida alla distribuzione di Cloud App Discovery System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Impostazioni del Registro di sistema di Cloud App Discovery per servizi proxy con porte personalizzate](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Log modifiche dell'agente di Cloud App Discovery ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Domande frequenti di Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

