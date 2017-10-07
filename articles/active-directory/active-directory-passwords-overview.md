---
title: Panoramica di reimpostazione della password self-service aaaAzure AD | Documenti Microsoft
description: "Cosa può fare la Reimpostazione self-service delle password in Azure AD per l'organizzazione?"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Reimpostazione della password self-service di Azure AD per hello professionisti IT

"Self-service" è un buzzword generati intorno all'interno di numerosi reparti IT in hello world con significati diversi. mercato Hello viene sovraccaricato di prodotti che consentono di gruppi locali toomanage, password o i profili utente dal cloud hello o in locale.

La Reimpostazione self-service delle password (SSPR) di Azure Active Directory (Azure AD) imposta se stessa a distanza con facilità di uso e distribuzione. La Reimpostazione self-service delle password di Azure AD combina un set di funzionalità che:

* Consenti il toomanage agli utenti la propria password
  * Da qualsiasi dispositivo
  * In qualsiasi posizione
  * In qualsiasi momento
* Mantiene la conformità con i criteri che si definiscono in qualità di amministratore

Se si è pronti, è possibile iniziare a usare la SSPR di Azure AD usando la nostra [guida introduttiva di avvio rapido](active-directory-passwords-getting-started.md) e vedere come gli utenti reimpostano rapidamente le proprie password.

## <a name="what-is-possible"></a>Cosa è possibile

* **Modifica della password self-service** consente agli utenti finali o agli amministratori toochange le proprie password senza l'assistenza dell'amministratore
* **Sblocco dell'account self-service** consente toounlock gli utenti finali i propri account senza l'assistenza dell'amministratore
* **Reimpostazione della password self-service** consente agli utenti finali o agli amministratori tooreset le proprie password automaticamente senza l'assistenza dell'amministratore. La reimpostazione delle password self-service è disponibile solo in Azure AD Premium o Basic - [Edizioni di Azure Active Directory](active-directory-editions.md).
* **La reimpostazione della password avviata dall'amministratore** consente un tooreset amministratore password dell'utente finale o un altro amministratore all'interno di hello [portale di Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* I **rapporti sulle attività di gestione delle password** forniscono agli amministratori informazioni dettagliate sulle attività di reimpostazione delle password e di registrazione che si verificano all'interno dell'organizzazione - [Report di gestione](active-directory-passwords-reporting.md)
* **Writeback delle password** consente la gestione delle password locali dal cloud hello in modo che precede di hello tutti gli scenari possono essere eseguiti da o per conto di hello, federati o utenti con password sincronizzate. Per il writeback delle password è necessaria una licenza di [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Perché scegliere la Reimpostazione self-service della password di Azure AD

* **Ridurre i costi** : poiché il supporto tecnico e la reimpostazione delle password assistita rappresentano in genere il 20% della spesa IT di un'organizzazione
* **Migliorare l'esperienza utente finale** e **ridurre i volumi di help desk** , assegnando a fine utenti hello power tooresolve i propri problemi relativi alla password in una sola volta senza la chiamata a un supporto tecnico o l'apertura di una richiesta di supporto.
* **Mobilità dell'unità** poiché gli utenti possono reimpostare le password da qualsiasi posizione.

## <a name="azure-ad-self-service-password-reset-availability"></a>Disponibilità della Reimpostazione self-service della password di Azure AD

La Reimpostazione self-service delle password di Azure AD è disponibile in tre livelli a seconda della sottoscrizione.

* **Azure AD Free** - Gli amministratori di reti solo cloud possono reimpostare la password personale
* **Azure AD Basic** o una **Sottoscrizione di Office365 a pagamento** - Gli amministratori e gli utenti di reti solo cloud possono reimpostare la password personale
* **Azure AD Premium** - qualsiasi utente o amministratore, inclusi gli utenti di reti solo cloud, federati o sincronizzati tramite password, può reimpostare la password personale. Password locali richiedono toobe di writeback delle password abilitata.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>La reimpostazione della password self-service di Azure AD, una somma di parti di hello

Self-service la reimpostazione della password in Azure AD è costituita da hello seguenti componenti:

* **Portale di configurazione di gestione di password** dove è possibile controllare le opzioni per la gestione delle password nel tenant tramite hello portale di Azure
* **Portale di registrazione della reimpostazione delle password** dove gli utenti possono eseguire la registrazione automatica per la reimpostazione della password
* **Portale di reimpostazione della password** in cui gli utenti possono reimpostare la password utilizzando sfide hello definite dall'amministratore di hello e hello risposte gli utenti hanno fornito.
* **Portale di modifica della password dell'utente** dove gli utenti possono modificare la propria password immettendo la vecchia password e fornendone una nuova
* **Report di gestione password** i report in cui gli amministratori possono visualizzare e analizzare l'attività di password per i tenant nel portale di Azure hello
* **Password writeback tooon locale con Azure AD Connect** consente si tooenable gestione locale, federato, o gli utenti dal cloud hello di sincronizzazione della password

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Prezzi, contratto di servizio, aggiornamenti e guida di orientamento di Azure AD

Ulteriori informazioni su questi argomenti sono disponibili nel seguente pagine hello

* [**Dettagli sui prezzi di Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Prezzi di Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Contratti di servizio di Azure**](https://azure.microsoft.com/support/legal/sla/)
* [**Contratto di servizio per Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Aggiornamenti di Azure**](https://azure.microsoft.com/updates/)
* [**Guida di orientamento di Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

