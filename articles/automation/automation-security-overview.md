---
title: tooauthentication aaaIntro in automazione di Azure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di sicurezza di automazione e hello diversi metodi di autenticazione disponibili per gli account di automazione in automazione di Azure.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: sicurezza in Automazione, proteggere Automazione; autenticazione in Automazione
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Introduzione tooauthentication in automazione di Azure  
Automazione di Azure consente attività tooautomate sulle risorse in Azure, in locale, nonché con altri provider di cloud come Amazon Web Services (AWS).  Affinché un tooperform runbook le azioni richieste, deve disporre delle autorizzazioni toosecurely accedere hello alle risorse con diritti minimi di hello necessari all'interno di sottoscrizione hello.

In questo articolo illustra hello vari scenari di autenticazione supportati da automazione di Azure e Mostra la modalità di avvio tooget basato sull'ambiente hello o ambienti è necessario toomanage.  

## <a name="automation-account-overview"></a>Panoramica dell'account di Automazione
Quando si avvia automazione di Azure per hello prima volta, è necessario creare almeno un account di automazione. Gli account di automazione consentono di tooisolate le risorse di automazione (runbook, risorse, configurazioni) da hello le risorse contenute in altri account di automazione. È possibile utilizzare le risorse tooseparate gli account di automazione in ambienti logici distinti. Ad esempio, è possibile usare un account per lo sviluppo, uno per la produzione e un altro per l'ambiente locale.  Un account di Automazione di Azure è diverso dagli account Microsoft creati nella sottoscrizione di Azure.

risorse di automazione Hello per ogni account di automazione sono associate a una singola regione di Azure, ma gli account di automazione è possono gestire tutte le risorse di hello nella sottoscrizione. Hello motivo principale toocreate gli account di automazione in aree diverse sarebbe se si dispone di criteri che richiedono dati e risorse toobe tooa isolato area specifica di un.

> [!NOTE]
> Gli account di automazione e che contengono le risorse di hello vengono creati nel portale di Azure hello, non è possibile accedere in hello portale di Azure classico. Se si desidera toomanage questi account o le proprie risorse con Windows PowerShell, è necessario utilizzare i moduli di gestione risorse di Azure hello.
>

Tutte le attività hello eseguite sulle risorse usando Gestione risorse di Azure e i cmdlet di Azure hello in automazione di Azure deve autenticare tooAzure utilizzando l'autenticazione basata su credenziali identità aziendale di Azure Active Directory.  L'autenticazione basata su certificato era hello metodo di autenticazione originale con la modalità di gestione dei servizi Azure, ma era toosetup complicata.  Autenticazione tooAzure con l'utente di Azure Active Directory è stata back introdotte nel 2014 toonot solo semplificare hello processo tooconfigure un account di autenticazione, ma anche supporto hello possibilità toonon interattivo autenticare tooAzure con un unico account utente che funziona correttamente con Gestione risorse di Azure e le risorse classiche.   

Attualmente, quando si crea un nuovo account di automazione in hello portale di Azure, viene creato automaticamente:

* Account RunAs che crea una nuova entità servizio in Azure Active Directory, un certificato e assegna hello collaboratore basata sui ruoli access control (RBAC), che saranno utilizzate le risorse di gestione risorse toomanage utilizzo dei runbook.
* Classico account RunAs caricando un certificato di gestione, che potrà essere toomanage utilizzato Gestione servizi di Azure o le risorse classiche utilizzo dei runbook.  

Controllo di accesso basato sui ruoli è disponibile con Gestione risorse di Azure toogrant è consentito l'account utente di Azure AD tooan azioni e account RunAs e l'autenticazione di tale entità servizio.  Leggere [controllo di accesso basato sui ruoli nell'articolo di automazione di Azure](automation-role-based-access-control.md) per ulteriori informazioni toohelp sviluppato il modello di gestione delle autorizzazioni di automazione.  

I runbook in esecuzione in un Runbook Worker ibrido nel Data Center o in servizi in AWS di elaborazione non è possibile utilizzare hello stesso metodo che viene in genere utilizzata per i runbook tooAzure risorse di autenticazione.  In questo modo tali risorse sono in esecuzione all'esterno di Azure e di conseguenza, può richiedere le proprie credenziali di sicurezza definite in automazione tooauthenticate tooresources che avranno accesso a livello locale.  

## <a name="authentication-methods"></a>Metodi di autenticazione
Hello nella tabella seguente sono riepilogati hello diversi metodi di autenticazione per ogni ambiente supportato da automazione di Azure e hello articolo che descrive la modalità autenticazione toosetup per i runbook.

| Metodo | Environment | Articolo |
| --- | --- | --- |
| Account utente di Azure AD |Gestione risorse di Azure e Gestione servizi di Azure |[Autenticare runbook con un account utente di Azure AD](automation-create-aduser-account.md) |
| Account RunAs di Azure |Gestione risorse di Azure |[Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md) |
| Account RunAs classico di Azure |Azure Service Management |[Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md) |
| Autenticazione di Windows |Data Center locale |[Autenticare runbook per ruoli di lavoro ibridi per runbook](automation-hybrid-runbook-worker.md) |
| Credenziali AWS |Amazon Web Services |[Autenticare runbook con Amazon Web Services (AWS)](automation-config-aws-account.md) |
