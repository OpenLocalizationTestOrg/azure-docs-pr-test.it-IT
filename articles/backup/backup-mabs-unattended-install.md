---
title: aaaSilent installazione del Server di Backup di Azure v2 | Documenti Microsoft
description: "Utilizzare un toosilently di script di PowerShell di installazione Server di Backup di Azure v2. Questo tipo di installazione è chiamato anche installazione automatica."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Eseguire un'installazione automatica del server di Backup di Azure v2

Informazioni su come toorun un'installazione automatica di Azure Backup Server v2. 

Questi passaggi non sono applicabili se si installa il server di Backup di Azure v1.

## <a name="install-backup-server-v2"></a>Installare il server di backup v2

1. Nel server di hello che ospita il Server di Backup di Azure v2, creare un file di testo. (È possibile creare file hello in blocco note o in un altro testo dell'editor.) Salvare il file hello MABSSetup.ini. 

2. Incollare hello seguente codice nel file MABSSetup.ini hello. Sostituire il testo hello parentesi hello (\< \>) con i valori dell'ambiente. Dopo il testo Hello è riportato un esempio:

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Salvare il file hello. Quindi, a un prompt con privilegi elevati nel server di installazione di hello, immettere questo comando:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

È possibile utilizzare questi flag per l'installazione di hello:</br>
**/f**: percorso del file .ini</br>
**/l**: percorso del log</br>
**/i**: percorso di installazione</br>
**/x**: percorso di disinstallazione</br>

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il Server di Backup, informazioni su come tooprepare del server, o iniziare a proteggere un carico di lavoro.

- [Preparare i carichi di lavoro del server di backup](backup-azure-microsoft-azure-backup.md)
- [Utilizzare tooback Server di Backup di un server VMware](backup-azure-backup-server-vmware.md)
- [Usare Backup Server tooback verticale di SQL Server](backup-azure-sql-mabs.md)
- [Aggiungere l'archiviazione dei Backup moderna tooBackup Server](backup-mabs-add-storage.md)
