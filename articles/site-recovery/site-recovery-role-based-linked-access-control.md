---
title: aaaUsing toomanage di controllo di accesso basato sui ruoli Azure Site Recovery | Documenti Microsoft
description: In questo articolo viene descritto come tooapply e l'utilizzo in base al ruolo di controllo di accesso (RBAC) toomanage le distribuzioni di Azure Site Recovery
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Usare le distribuzioni di Azure Site Recovery toomanage di controllo di accesso basato sui ruoli

Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure. Usa tale controllo, è possibile separare le responsabilità all'interno del team e concedere solo accesso specifiche autorizzazioni toousers come i processi specifici tooperform necessari.

Azure Site Recovery fornisce i ruoli predefiniti 3 toocontrol operazioni di gestione di Site Recovery. Maggiori informazioni sui [ruoli predefiniti del Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md)

* [Sito di ripristino collaboratore](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -questo ruolo dispone di tutte le operazioni di Azure Site Recovery toomanage necessarie le autorizzazioni in un insieme di credenziali di servizi di ripristino. Un utente con questo ruolo, tuttavia, non è possibile creare o eliminare un insieme di credenziali di servizi di ripristino oppure assegnare gli utenti tooother diritti di accesso. Questo ruolo è più adatto per gli amministratori di ripristino di emergenza che possono attivare e gestire il ripristino di emergenza per le applicazioni o l'intera azienda, come casi di hello.
* [Operatore di ripristino sito](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -questo ruolo dispone di autorizzazioni tooexecute e gestione Failover e Failback operazioni. Un utente con questo ruolo non è possibile abilitare o disabilitare la replica, creare o eliminare gli insiemi di credenziali, registrare una nuova infrastruttura oppure assegnare gli utenti tooother diritti di accesso. Questo ruolo è ideale per un operatore di ripristino di emergenza che può eseguire il failover di macchine virtuali o applicazioni quando richiesto dai proprietari delle applicazioni e dagli amministratori IT in una situazione di emergenza effettiva o simulata, ad esempio per un'esercitazione sul ripristino di emergenza. Registra la risoluzione di emergenza hello, operatore hello ripristino di emergenza può proteggere nuovamente e failback hello macchine virtuali.
* [Sito di ripristino lettore](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -questo ruolo dispone di autorizzazioni tooview tutte le operazioni di gestione di Site Recovery. Questo ruolo è adatto a un dirigente di monitoraggio IT che possa monitorare lo stato corrente di hello di protezione e generare i ticket di supporto, se necessario.

Se si cerca toodefine dei ruoli personalizzati per un maggiore controllo, vedere come troppo[creare ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md) in Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Le autorizzazioni richieste tooEnable replica per nuove macchine virtuali
Quando una nuova macchina virtuale viene replicato tooAzure usando Azure Site Recovery, livelli di accesso dell'utente hello associato vengono convalidati tooensure che hello utente hello necessarie autorizzazioni toouse hello Azure risorse fornite tooSite ripristino.

replica tooenable per una nuova macchina virtuale, un utente è necessario quanto segue:
* Autorizzazione toocreate una macchina virtuale nel gruppo di risorse selezionato hello
* Autorizzazione toocreate una macchina virtuale nella rete virtuale selezionata hello
* Autorizzazione toowrite toohello selezionato di account di archiviazione

L'utente deve hello seguente replica toocomplete delle autorizzazioni di una nuova macchina virtuale.

> [!IMPORTANT]
>Verificare che le autorizzazioni rilevanti vengono aggiunti al modello di distribuzione hello (Gestione risorse / classico) utilizzato per la distribuzione di risorse.

| **Tipo di risorsa** | **Modello di distribuzione** | **Autorizzazione** |
| --- | --- | --- |
| Calcolo | Gestione risorse | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Classico | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Rete | Gestione risorse | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Classico | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Archiviazione | Gestione risorse | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Classico | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Gruppo di risorse | Gestione risorse | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

È consigliabile utilizzare hello 'Collaboratore alla macchina virtuale' e 'Classico collaboratore alla macchina virtuale' [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) per la distribuzione di gestione risorse e classica modelli rispettivamente.

## <a name="next-steps"></a>Passaggi successivi
* [Controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.
* Informazioni su come accedere a toomanage con:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Risoluzione dei problemi del controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-troubleshooting.md): suggerimenti per la risoluzione di problemi comuni.
