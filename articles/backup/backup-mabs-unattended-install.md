---
title: Installazione invisibile del server di Backup di Azure v2 | Microsoft Docs
description: "Usare uno script di PowerShell per installare in modo invisibile il server di Backup di Azure v2. Questo tipo di installazione è chiamato anche installazione automatica."
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="879b2-104">Eseguire un'installazione automatica del server di Backup di Azure v2</span><span class="sxs-lookup"><span data-stu-id="879b2-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="879b2-105">Informazioni su come eseguire un'installazione automatica del server di Backup di Azure v2.</span><span class="sxs-lookup"><span data-stu-id="879b2-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="879b2-106">Questi passaggi non sono applicabili se si installa il server di Backup di Azure v1.</span><span class="sxs-lookup"><span data-stu-id="879b2-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="879b2-107">Installare il server di backup v2</span><span class="sxs-lookup"><span data-stu-id="879b2-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="879b2-108">Nel server che ospita il server di Backup di Azure v2, creare un file di testo.</span><span class="sxs-lookup"><span data-stu-id="879b2-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="879b2-109">(è possibile creare il file nel Blocco note o in un altro editor di testo). Salvare il file con il nome MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="879b2-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="879b2-110">Incollare il codice seguente nel file MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="879b2-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="879b2-111">Sostituire il testo all'interno delle parentesi (\< \>) con i valori dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="879b2-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="879b2-112">Il testo seguente è un esempio:</span><span class="sxs-lookup"><span data-stu-id="879b2-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="879b2-113">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="879b2-113">Save the file.</span></span> <span data-ttu-id="879b2-114">Quindi, a un prompt con privilegi elevati nel server di installazione, immettere questo comando:</span><span class="sxs-lookup"><span data-stu-id="879b2-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="879b2-115">È possibile usare questi flag per l'installazione:</span><span class="sxs-lookup"><span data-stu-id="879b2-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="879b2-116">
**/f**: percorso del file .ini</span><span class="sxs-lookup"><span data-stu-id="879b2-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="879b2-117">
**/l**: percorso del log</span><span class="sxs-lookup"><span data-stu-id="879b2-117">
**/l**: Log path</span></span></br><span data-ttu-id="879b2-118">
**/i**: percorso di installazione</span><span class="sxs-lookup"><span data-stu-id="879b2-118">
**/i**: Installation path</span></span></br><span data-ttu-id="879b2-119">
**/x**: percorso di disinstallazione</span><span class="sxs-lookup"><span data-stu-id="879b2-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="879b2-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="879b2-120">Next steps</span></span>
<span data-ttu-id="879b2-121">Dopo aver installato il server di backup, leggere le informazioni su come preparare il server o iniziare a proteggere un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="879b2-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="879b2-122">Preparare i carichi di lavoro del server di backup</span><span class="sxs-lookup"><span data-stu-id="879b2-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="879b2-123">Usare il server di backup per eseguire il backup di un server VMware</span><span class="sxs-lookup"><span data-stu-id="879b2-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="879b2-124">Usare il server di backup per eseguire il backup di SQL Server</span><span class="sxs-lookup"><span data-stu-id="879b2-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="879b2-125">Aggiungere Modern Backup Storage al server di backup</span><span class="sxs-lookup"><span data-stu-id="879b2-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
