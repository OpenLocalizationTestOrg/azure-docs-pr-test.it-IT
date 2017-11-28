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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="9ecca-104">Eseguire un'installazione automatica del server di Backup di Azure v2</span><span class="sxs-lookup"><span data-stu-id="9ecca-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="9ecca-105">Informazioni su come toorun un'installazione automatica di Azure Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="9ecca-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="9ecca-106">Questi passaggi non sono applicabili se si installa il server di Backup di Azure v1.</span><span class="sxs-lookup"><span data-stu-id="9ecca-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="9ecca-107">Installare il server di backup v2</span><span class="sxs-lookup"><span data-stu-id="9ecca-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="9ecca-108">Nel server di hello che ospita il Server di Backup di Azure v2, creare un file di testo.</span><span class="sxs-lookup"><span data-stu-id="9ecca-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="9ecca-109">(È possibile creare file hello in blocco note o in un altro testo dell'editor.) Salvare il file hello MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="9ecca-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="9ecca-110">Incollare hello seguente codice nel file MABSSetup.ini hello.</span><span class="sxs-lookup"><span data-stu-id="9ecca-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="9ecca-111">Sostituire il testo hello parentesi hello (\< \>) con i valori dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9ecca-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="9ecca-112">Dopo il testo Hello è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="9ecca-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="9ecca-113">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="9ecca-113">Save hello file.</span></span> <span data-ttu-id="9ecca-114">Quindi, a un prompt con privilegi elevati nel server di installazione di hello, immettere questo comando:</span><span class="sxs-lookup"><span data-stu-id="9ecca-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="9ecca-115">È possibile utilizzare questi flag per l'installazione di hello:</span><span class="sxs-lookup"><span data-stu-id="9ecca-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="9ecca-116">
**/f**: percorso del file .ini</span><span class="sxs-lookup"><span data-stu-id="9ecca-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="9ecca-117">
**/l**: percorso del log</span><span class="sxs-lookup"><span data-stu-id="9ecca-117">
**/l**: Log path</span></span></br><span data-ttu-id="9ecca-118">
**/i**: percorso di installazione</span><span class="sxs-lookup"><span data-stu-id="9ecca-118">
**/i**: Installation path</span></span></br><span data-ttu-id="9ecca-119">
**/x**: percorso di disinstallazione</span><span class="sxs-lookup"><span data-stu-id="9ecca-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="9ecca-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ecca-120">Next steps</span></span>
<span data-ttu-id="9ecca-121">Dopo aver installato il Server di Backup, informazioni su come tooprepare del server, o iniziare a proteggere un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9ecca-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="9ecca-122">Preparare i carichi di lavoro del server di backup</span><span class="sxs-lookup"><span data-stu-id="9ecca-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="9ecca-123">Utilizzare tooback Server di Backup di un server VMware</span><span class="sxs-lookup"><span data-stu-id="9ecca-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="9ecca-124">Usare Backup Server tooback verticale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="9ecca-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="9ecca-125">Aggiungere l'archiviazione dei Backup moderna tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="9ecca-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
