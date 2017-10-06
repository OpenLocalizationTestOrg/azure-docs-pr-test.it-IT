---
title: "aaaWhat è l'insieme di credenziali chiave di Azure? | Microsoft Docs"
description: L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud. Con l'insieme di credenziali chiave di Azure i clienti possono crittografare chiavi e segreti (ad esempio, chiavi di autenticazione, chiavi dell'account di archiviazione, chiavi di crittografia dati, file PFX e password) usando chiavi protette da moduli di protezione hardware (HSM).
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Cos'è l'insieme di credenziali chiave di Azure?
L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree. Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduzione
L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud. Con l'insieme di credenziali delle chiavi è possibile crittografare chiavi e segreti (ad esempio, chiavi di autenticazione, chiavi dell'account di archiviazione, chiavi di crittografia dati, file PFX e password) usando chiavi protette da moduli di protezione hardware (HSM). Per una maggiore sicurezza, è possibile importare o generare le chiavi in moduli di protezione hardware. Se si sceglie questa operazione, i processi di Microsoft a toodo le chiavi di FIPS 140-2 livello 2 convalidati moduli di protezione hardware (hardware e firmware).  

Insieme di credenziali chiave semplifica il processo di gestione delle chiavi hello e consente il controllo toomaintain di chiavi per l'accesso e crittografare i dati. Gli sviluppatori possono creare chiavi per lo sviluppo e test in minuti e quindi migrare le chiavi tooproduction. Gli amministratori della sicurezza possono concedere e revocare tookeys di autorizzazione, in base alle esigenze.

Hello utilizzare toobetter nella tabella seguente è comprendere come insieme di credenziali chiave consente di esigenze di hello toomeet di sviluppatori e amministratori della sicurezza.

| Ruolo | Presentazione del problema | Soluzione offerta dall'insieme di credenziali chiave di Azure |
| --- | --- | --- |
| Sviluppatore di un'applicazione Azure |"Voglio toowrite un'applicazione per Azure che usa chiavi per la firma e crittografia, ma si desidera toobe queste chiavi esterne da un'applicazione in modo che la soluzione hello è adatta per un'applicazione geograficamente distribuita. <br/><br/>Inoltre, è toobe queste chiavi e segreti protetto, senza la necessità di codice hello toowrite per me. Inoltre, è toobe queste chiavi e segreti semplice per me toouse da applicazioni, con prestazioni ottimali." |√ Le chiavi vengono archiviate in un insieme di credenziali e richiamate dall'URI quando è necessario.<br/><br/> √ Le chiavi vengono protette da Azure con algoritmi standard del settore, lunghezze delle chiavi e moduli di protezione hardware.<br/><br/> √ Chiavi vengono elaborate in moduli di protezione hardware che si trovano in hello stesso Data Center di Azure come applicazioni hello. Ciò fornisce maggiore affidabilità e la latenza ridotta rispetto a quella se le chiavi di hello risiedono in un percorso separato, ad esempio in locale. |
| Sviluppatore di software come un servizio (SaaS) |"Non si desidera la responsabilità di hello responsabilità o potenziale per i segreti e tutte le chiavi tenant dei clienti. <br/><br/>Desidera tooown clienti hello e gestiscono le relative chiavi in modo che è possibile concentrarsi sull'esecuzione di operazioni ottimale, che fornisce funzionalità di software di base hello". |√ I clienti possono importare le loro chiavi in Azure e gestirle. Quando un'applicazione SaaS deve tooperform le operazioni di crittografia tramite chiavi dei clienti, insieme di credenziali chiave effettua queste operazioni per conto di un'applicazione hello. un'applicazione Hello non consente di visualizzare le chiavi dei clienti hello. |
| Responsabile della sicurezza |"Si desidera tooknow le applicazioni conformi con i moduli HSM FIPS 140-2 livello 2 per la gestione delle chiavi protetta. <br/><br/>Si desidera che l'organizzazione sia nel controllo del ciclo di vita chiave hello toomake e monitorare l'utilizzo della chiave. <br/><br/>E anche se si usa più servizi di Azure e risorse, si desidero che le chiavi di hello toomanage da un'unica posizione in Azure". |√ I moduli di protezione hardware hanno la certificazione FIPS 140-2 livello 2.<br/><br/>√ L'insieme di credenziali delle chiavi è progettato in modo che Microsoft non possa vedere o estrarre le chiavi.<br/><br/>√ Registrazione quasi in tempo reale dell'utilizzo delle chiavi.<br/><br/>Insieme di credenziali hello √ offre un'unica interfaccia, indipendentemente dal quanti gli insiemi di credenziali è in Azure, le aree sono, supporto e le applicazioni li utilizzano. |

Chiunque abbia una sottoscrizione di Azure può creare e usare insiemi di credenziali delle chiavi. Anche se l'insieme di credenziali chiave è un vantaggio per sviluppatori e amministratori della sicurezza, può essere implementato e gestito dall'amministratore di un'organizzazione che gestisce altri servizi di Azure per un'organizzazione. L'amministratore sarebbe ad esempio, accedere con una sottoscrizione di Azure, creare un insieme di credenziali per l'organizzazione hello in tasti toostore e quindi essere responsabile per le attività operative, ad esempio:

* Creare o importare una chiave o un segreto
* Revocare o eliminare una chiave o un segreto
* Autorizzare utenti o applicazioni tooaccess hello chiave dell'insieme di credenziali, in modo da poter quindi gestire o usare le chiavi e segreti
* Configurare l'utilizzo delle chiavi (ad esempio, la firma o la crittografia)
* Monitorare l'utilizzo delle chiavi

L'amministratore potrebbe quindi fornire agli sviluppatori con URI toocall dalle rispettive applicazioni e fornire loro amministratore della sicurezza con le informazioni di registrazione dell'utilizzo chiave. 

   ![Panoramica dell'insieme di credenziali chiave di Azure][1]

Gli sviluppatori possono anche gestire hello le chiavi direttamente, utilizzando le API. Per ulteriori informazioni, vedere [hello Guida per gli sviluppatori di insieme di credenziali chiave](key-vault-developers-guide.md).

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione introduttiva per gli amministratori, vedere [Introduzione all'insieme di credenziali chiave di Azure](key-vault-get-started.md).

Per altre informazioni sulla registrazione dell'utilizzo per l'insieme di credenziali delle chiavi, vedere [Registrazione dell'insieme di credenziali delle chiavi di Azure](key-vault-logging.md).

Per altre informazioni sull'uso di chiavi e segreti con l'insieme di credenziali delle chiavi di Azure, vedere [About Keys, Secrets, and Certificates](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx) (Informazioni su chiavi, segreti e certificati).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
