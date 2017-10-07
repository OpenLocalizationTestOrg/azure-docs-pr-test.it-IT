---
title: Gestire i backup con il controllo degli accessi in base al ruol | Documentazione Microsoft
description: Utilizzare le operazioni di gestione di controllo di accesso basato sui ruoli toomanage accesso toobackup nell'insieme di credenziali di servizi di ripristino.
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Utilizzare i punti di ripristino di Backup di Azure toomanage Role-Based Access Control
Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure. Usa tale controllo, è possibile separare i compiti all'interno del team e concedere solo quantità di hello di accesso toousers necessarie tooperform i processi.

> [!IMPORTANT]
> Ruoli predefiniti forniti dal Backup di Azure sono tooactions limitate che possono essere eseguite nel portale di Azure o i cmdlet di PowerShell insieme di credenziali di servizi di ripristino. Non rientrano sotto il controllo di questi ruoli le azioni eseguite nell'interfaccia utente client di Azure Backup Agent, nell'interfaccia utente di System Center Data Protection Manager o nell'interfaccia utente del server di Backup di Azure.

Backup di Azure fornisce le operazioni di gestione dei backup di toocontrol 3 ruoli predefiniti. Maggiori informazioni sui [ruoli predefiniti del Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md)

* [Eseguire il backup collaboratore](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -questo ruolo dispone di tutte le autorizzazioni toocreate e gestire il backup, ad eccezione di creazione dell'insieme di credenziali di servizi di ripristino e fornendo accesso tooothers. Si immagini questo ruolo come amministratore della gestione di backup autorizzato a eseguire ogni operazione in tale ambito.
* [Operatore di backup](../active-directory/role-based-access-built-in-roles.md#backup-operator) -questo ruolo dispone di autorizzazioni tooeverything tranne un collaboratore alla rimozione di backup e la gestione dei criteri di backup. Questo ruolo è toocontributor equivalente, ma non può eseguire operazioni distruttive quali Interrompi backup con i dati di eliminare o rimuovere la registrazione di risorse locali.
* [Eseguire il backup lettore](../active-directory/role-based-access-built-in-roles.md#backup-reader) -questo ruolo dispone di autorizzazioni tooview tutte le operazioni di gestione dei backup. Si supponga questo toobe ruolo una persona di monitoraggio.

Se si cerca toodefine dei ruoli personalizzati per un maggiore controllo, vedere come troppo[creare ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md) in RBAC di Azure.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Mapping di azioni di gestione toobackup ruoli predefiniti del Backup
Nella tabella seguente Hello acquisisce le azioni di gestione Backup hello e ruolo RBAC minimo corrispondente necessario tooperform tale operazione.

| Operazione di gestione | Ruolo RBAC minimo richiesto |
| --- | --- |
| Creare un insieme di credenziali di Servizi di ripristino | Collaboratore per il gruppo di risorse dell'insieme di credenziali |
| Abilitare il backup di VM di Azure | Operatore di backup per l'insieme di credenziali, collaboratore Macchina virtuale in VM |
| Backup su richiesta della VM | Operatore di backup |
| Ripristino della VM | Operatore di backup, collaboratore di gruppo di risorse in cui le reti virtuali e macchina virtuale verranno tooget distribuito |
| Ripristinare dischi e singoli file dal backup delle VM | Operatore di backup |
| Creare criteri di backup per il backup di VM di Azure | Collaboratore di backup |
| Modificare criteri di backup per il backup di VM di Azure | Collaboratore di backup |
| Eliminare criteri di backup per il backup di VM di Azure | Collaboratore di backup |
| Interrompere il backup (con o senza conservazione dei dati) in operazioni di backup di VM | Collaboratore di backup |
| Registrare Windows Server/client/SCDPM locale o server di Backup di Azure | Operatore di backup |
| Eliminare Windows Server/client/SCDPM locale o server di Backup di Azure registrato | Collaboratore di backup |

## <a name="next-steps"></a>Passaggi successivi
* [Controllo di accesso basato su ruoli](../active-directory/role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.
* Informazioni su come accedere a toomanage con:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Risoluzione dei problemi del controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-troubleshooting.md): suggerimenti per la risoluzione di problemi comuni.
