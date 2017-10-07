---
title: Active Directory PoC Playbook ingredienti aaaAzure | Documenti Microsoft
description: "Esplorare e implementare rapidamente gli scenari di Gestione delle identità e degli accessi"
services: active-directory
keywords: azure active directory, playbook, modello di verifica, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Ingredienti del playbook dei modelli di verifica di Azure Active Directory 

## <a name="theme"></a>Tema
Azure AD fornisce soluzioni di identità e degli accessi in più aree in enterprise hello. Si classifica gli scenari di hello in hello seguenti aree: 

* [Molte app, una sola identità](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Aumentare la sicurezza](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Scalabilità self-service](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Definisce un tema tooframe hello che POC consente gli sforzi hello toofocus definita adatta alle esigenze agli obiettivi aziendali, che spesso sono trigger hello di interesse hello in un modello di prova in primo luogo hello. 

## <a name="environment"></a>Environment

È importante toodetermine i dettagli di hello dell'ambiente hello in cui si installerà hello PoC. In teoria è possibile creare su di esso dopo hello che POC viene completata. ambiente di destinazione Hello è essenziale e si deve trovare hello giusto equilibrio tra rendendo l'oggetto e reale come possibili e overhead di hello di vincoli o considerazioni aggiuntive. ambienti Hello per PoCs sono:
* **Produzione:** scenari hello verrà implementati nell'ambiente in tempo reale e già stati distribuiti servizi Cloud Microsoft (soluzione di produzione AD, Office 365, Azure AD/SSO tenant). 
* **Test accettazione utente / ambiente di sviluppo:** è disponibile un’infrastruttura di test (AD parallelo e potenziale tenant di Azure AD/soluzione SSO) con dati di test analoghi alla produzione. In genere, ambiente di test hello è condiviso tra più progetti in enterprise hello.

Nella maggior parte dei casi, gli scenari in questa guida sono additivi in natura. Di conseguenza, possano essere distribuiti nel tenant di produzione hello senza modificare gli utenti all'esterno di hello in ambiente di prova. In questo documento, verranno esclusi gli scenari che avrebbero un impatto globale a livello di tenant. In questi casi, è possibile tooconsider un ambiente non di produzione. 


## <a name="target-users"></a>Utenti di destinazione

È importante toodetermine hello riferimento impostato per gli utenti che verranno esercitare scenari hello, in particolar modo quando ambiente hello produzione o test. categorie di Hello degli utenti di destinazione di prova sono:
* **Utenti della fase pilota:** utenti reali nell'ambiente di hello che utilizzerà la soluzione hello con hello l'account utilizzato per la loro tooday giorno processo funzioni
* **Gli utenti di test:** account creati in hello ambiente di Test 

La maggior parte degli scenari contemplati in questa guida può essere usata dagli utenti pilota. In questo documento verranno escluse se necessario le considerazioni in merito agli utenti di destinazione.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]