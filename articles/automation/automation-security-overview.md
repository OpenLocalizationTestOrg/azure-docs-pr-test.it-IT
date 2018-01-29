---
title: Introduzione all'autenticazione in Automazione di Azure | Microsoft Docs
description: Questo articolo offre una panoramica della sicurezza in Automazione e dei diversi metodi di autenticazione disponibili per gli account di Automazione in Automazione di Azure.
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: tysonn
keywords: sicurezza in Automazione, proteggere Automazione; autenticazione in Automazione
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 99882c1ff7517beec2ca827c63620f773d7d07c3
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="introduction-to-authentication-in-azure-automation"></a>Introduzione all'autenticazione in Automazione di Azure  
Automazione di Azure consente di automatizzare le attività sulle risorse in Azure, in locale e con altri provider di servizi cloud, ad esempio Amazon Web Services (AWS).  Un runbook, per eseguire le azioni obbligatorie, deve avere le autorizzazioni per accedere in modo sicuro alle risorse con i diritti minimi necessari nella sottoscrizione.

Questo articolo illustra i diversi scenari di autenticazione supportati da Automazione di Azure e spiega come iniziare partendo da uno o più ambienti che è necessario gestire.  

## <a name="automation-account-overview"></a>Panoramica dell'account di Automazione
Al primo avvio di Automazione di Azure sarà necessario creare almeno un account di Automazione. Gli account di Automazione consentono di isolare le risorse di Automazione (runbook, asset, configurazioni) dalle risorse contenute in altri account di Automazione. È possibile usare gli account di Automazione per separare le risorse in ambienti logici distinti. Ad esempio, è possibile usare un account per lo sviluppo, uno per la produzione e un altro per l'ambiente locale.  Un account di Automazione di Azure è diverso dagli account Microsoft creati nella sottoscrizione di Azure.

Le risorse di Automazione per ogni account di Automazione sono associate a una singola area di Azure, ma gli account di Automazione possono gestire tutte le risorse nella sottoscrizione. Il motivo principale per cui creare gli account di Automazione in aree diverse è la presenza di criteri che richiedono dati e risorse per essere isolati in un'area specifica.

Tutte le attività eseguite sulle risorse con Azure Resource Manager e i cmdlet di Azure in Automazione di Azure devono eseguire l'autenticazione in Azure con l'autenticazione basata su credenziali dell'identità dell'organizzazione di Azure Active Directory.  L'autenticazione basata su certificati è il metodo di autenticazione originale con le risorse classiche di Azure, ma è complessa da configurare.  L'autenticazione in Azure con un utente di Azure AD è stata reintrodotta nel 2014 non solo per semplificare il processo di configurazione di un account di autenticazione, ma anche per offrire la possibilità di eseguire l'autenticazione in Azure in modo non interattivo con un solo account utente che funzionasse con risorse sia classiche che di Azure Resource Manager.   

Attualmente, quando si crea un nuovo account di Automazione nel portale di Azure viene creato automaticamente quanto segue:

* Account RunAs che crea una nuova entità servizio in Azure Active Directory e un certificato e assegna il ruolo Collaboratore per il controllo degli accessi in base al ruolo, usato per gestire le risorse di Resource Manager con i runbook.
* Account RunAs classico, caricando un certificato di gestione che viene usato per gestire le risorse classiche di Azure con i runbook.  

Il controllo degli accessi in base al ruolo è disponibile con Azure Resource Manager per l'esecuzione di azioni consentite con un account utente di Azure AD e per l'autenticazione di tale entità servizio.  Per altre informazioni utili per sviluppare il modello per la gestione delle autorizzazioni di Automazione, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).  

I runbook eseguiti in un ruolo di lavoro ibrido per runbook nel data center o in servizi di calcolo in AWS non possono usare lo stesso metodo usato per i runbook che si autenticano per le risorse di Azure.  Il motivo è che queste risorse vengono eseguite all'esterno di Azure e di conseguenza devono usare le proprie credenziali di sicurezza definite in Automazione per autenticare le risorse cui accedono in locale.  

## <a name="authentication-methods"></a>Metodi di autenticazione
La tabella seguente riepiloga i diversi metodi di autenticazione per ogni ambiente supportato da Automazione di Azure e l'articolo che descrive come configurare l'autenticazione per i runbook.

| Metodo | Ambiente | Articolo |
| --- | --- | --- |
| Account utente di Azure AD |Azure Resource Manager e ambiente Azure classico |[Autenticare runbook con un account utente di Azure AD](automation-create-aduser-account.md) |
| Account RunAs di Azure |Gestione risorse di Azure |[Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md) |
| Account RunAs classico di Azure |Ambiente Azure classico |[Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md) |
| Autenticazione di Windows |Data Center locale |[Autenticare runbook per ruoli di lavoro ibridi per runbook](automation-hybrid-runbook-worker.md) |
| Credenziali AWS |Amazon Web Services |[Autenticare runbook con Amazon Web Services (AWS)](automation-config-aws-account.md) |
