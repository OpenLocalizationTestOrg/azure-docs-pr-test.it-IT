---
title: " Gestire un server di elaborazione con scalabilità orizzontale in Azure Site Recovery | Microsoft Docs"
description: "Questo articolo descrive come configurare e gestire un server di elaborazione con scalabilità orizzontale in Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="1ebe6-103">Gestire un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="1ebe6-104">Il server di elaborazione con scalabilità orizzontale funge da coordinatore per il trasferimento dei dati tra i servizi di Site Recovery e l'infrastruttura locale in uso.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="1ebe6-105">Questo articolo descrive come impostare, configurare e gestire i server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ebe6-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1ebe6-106">Prerequisites</span></span>
<span data-ttu-id="1ebe6-107">La tabella seguente elenca i requisiti minimi hardware, software e di rete richiesti per impostare un server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1ebe6-108">La [pianificazione della capacità](site-recovery-capacity-planner.md) è un passaggio importante per assicurarsi di distribuire un server di elaborazione con scalabilità orizzontale con una configurazione adatta ai requisiti di carico.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="1ebe6-109">Altre informazioni sulle [caratteristiche di scalabilità per un server di elaborazione con scalabilità orizzontale](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="1ebe6-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="1ebe6-110">Download del software per il server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="1ebe6-111">Accedere al portale di Azure e passare all'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="1ebe6-112">Passare a **Infrastruttura di Site Recovery** > **Server di configurazione**, in For VMware & Physical Machines (Computer VMware e fisici).</span><span class="sxs-lookup"><span data-stu-id="1ebe6-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="1ebe6-113">Selezionare il server di configurazione per eseguire il drill-down della relativa pagina delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="1ebe6-114">Fare clic sul pulsante **+ Server di elaborazione**.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="1ebe6-115">Nella pagina **Aggiungi server di elaborazione** selezionare l'opzione **Distribuire un server di elaborazione con scalabilità orizzontale in locale** dall'elenco a discesa **Scegliere dove distribuire il server di elaborazione**.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Pagina Aggiungi server](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="1ebe6-117">Fare clic sul collegamento per **scarica l'installazione unificata di Microsoft Azure Site Recovery** per ottenere la versione più recente per l'installazione del server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="1ebe6-118">La versione del server di elaborazione con scalabilità orizzontale deve essere uguale o inferiore rispetto alla versione del server di configurazione in esecuzione nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="1ebe6-119">Un modo semplice per garantire la compatibilità tra le versioni è l'uso degli stessi bit del programma di installazione usato per installare/aggiornare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="1ebe6-120">Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dall'interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="1ebe6-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="1ebe6-121">Se è necessario ridimensionare la distribuzione oltre 200 computer di origine oppure la varianza totale giornaliera è superiore a 2 TB, sono necessari server di elaborazione aggiuntivi per gestire il volume di traffico.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="1ebe6-122">Vedere [Dimensioni consigliate per il server di elaborazione](#size-recommendations-for-the-process-server) e quindi seguire queste istruzioni per configurare il server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="1ebe6-123">Dopo aver configurato il server è possibile eseguire la migrazione dei computer di origine per usarlo.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="1ebe6-124">Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="1ebe6-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="1ebe6-125">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="1ebe6-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="1ebe6-126">Argomenti della riga di comando del programma di installazione del server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="1ebe6-127">Creare un file di configurazione delle impostazioni del proxy</span><span class="sxs-lookup"><span data-stu-id="1ebe6-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="1ebe6-128">Il parametro ProxySettingsFilePath usa un file come input.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="1ebe6-129">Creare il file usando il formato seguente e passarlo come parametro ProxySettingsFilePath di input.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="1ebe6-130">Modifica delle impostazioni proxy per il server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="1ebe6-131">Accedere al server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="1ebe6-132">Aprire una finestra dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="1ebe6-133">Eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="1ebe6-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="1ebe6-134">Passare alla directory **%PROGRAMDATA%\ASR\Agent** ed eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="1ebe6-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="1ebe6-135">Nuova registrazione di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="1ebe6-136">Quindi aprire un prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="1ebe6-137">Passare alla directory **%PROGRAMDATA%\ASR\Agent** ed eseguire il comando</span><span class="sxs-lookup"><span data-stu-id="1ebe6-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="1ebe6-138">Aggiornamento di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="1ebe6-139">Rimozione di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="1ebe6-140">Assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="1ebe6-140">Ensure that:</span></span>
  - <span data-ttu-id="1ebe6-141">Lo stato della connessione del server di configurazione sia visualizzato come **connesso** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="1ebe6-142">Il server di elaborazione sia ancora in grado di comunicare con il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="1ebe6-143">Accedere al server di elaborazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="1ebe6-144">Scegliere Pannello di controllo > Programma > Disinstallare programmi</span><span class="sxs-lookup"><span data-stu-id="1ebe6-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="1ebe6-145">Disinstallare i programmi nella sequenza seguente:</span><span class="sxs-lookup"><span data-stu-id="1ebe6-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="1ebe6-146">Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1ebe6-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="1ebe6-147">Dipendenze del server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1ebe6-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="1ebe6-148">Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1ebe6-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="1ebe6-149">Possono essere necessari fino a 15 minuti affinché l'eliminazione del server di elaborazione sia visualizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="1ebe6-150">Se il server di elaborazione non è in grado di comunicare con il server di configurazione e quindi nel portale lo stato della connessione è Disconnesso, seguire questa procedura rimuoverlo dal server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="1ebe6-151">Annullamento della registrazione di un server di elaborazione con scalabilità orizzontale disconnesso da un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="1ebe6-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="1ebe6-152">Requisiti per il ridimensionamento di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="1ebe6-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="1ebe6-153">**Server di elaborazione aggiuntivo**</span><span class="sxs-lookup"><span data-stu-id="1ebe6-153">**Additional process server**</span></span> | <span data-ttu-id="1ebe6-154">**Dimensione disco cache**</span><span class="sxs-lookup"><span data-stu-id="1ebe6-154">**Cache disk size**</span></span> | <span data-ttu-id="1ebe6-155">**Frequenza di modifica dei dati**</span><span class="sxs-lookup"><span data-stu-id="1ebe6-155">**Data change rate**</span></span> | <span data-ttu-id="1ebe6-156">**Computer protetti**</span><span class="sxs-lookup"><span data-stu-id="1ebe6-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="1ebe6-157">4 vCPU (2 socket * 2 core a 2,5 GHz), 8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="1ebe6-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="1ebe6-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="1ebe6-158">300 GB</span></span> |<span data-ttu-id="1ebe6-159">250 GB o inferiore</span><span class="sxs-lookup"><span data-stu-id="1ebe6-159">250 GB or less</span></span> |<span data-ttu-id="1ebe6-160">Replicare un massimo di 85 computer.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="1ebe6-161">8 vCPU (2 socket * 4 core a 2,5 GHz), 12 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="1ebe6-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="1ebe6-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="1ebe6-162">600 GB</span></span> |<span data-ttu-id="1ebe6-163">Da 250 GB a 1 TB</span><span class="sxs-lookup"><span data-stu-id="1ebe6-163">250 GB to 1 TB</span></span> |<span data-ttu-id="1ebe6-164">Replicare tra 85 e 150 computer.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="1ebe6-165">12 vCPU (2 socket * 6 core a 2,5 GHz), 24 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="1ebe6-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="1ebe6-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="1ebe6-166">1 TB</span></span> |<span data-ttu-id="1ebe6-167">Da 1 TB a 2 TB</span><span class="sxs-lookup"><span data-stu-id="1ebe6-167">1 TB to 2 TB</span></span> |<span data-ttu-id="1ebe6-168">Replicare tra 150 e 225 computer.</span><span class="sxs-lookup"><span data-stu-id="1ebe6-168">Replicate between 150-225 machines.</span></span> |
