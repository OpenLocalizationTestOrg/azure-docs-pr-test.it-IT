---
title: " Gestire un server di elaborazione con scalabilità orizzontale in Azure Site Recovery | Microsoft Docs"
description: "Questo articolo viene descritto come tooset configurare e gestire un Server di elaborazione di scalabilità orizzontale in Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="d5c86-103">Gestire un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="d5c86-104">Server di scalabilità orizzontale processo agisce come un coordinatore per il trasferimento di dati tra servizi di ripristino del sito di hello e l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="d5c86-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="d5c86-105">Questo articolo descrive come impostare, configurare e gestire i server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d5c86-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5c86-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5c86-106">Prerequisites</span></span>
<span data-ttu-id="d5c86-107">di seguito Hello sono hello consigliato tooset necessarie di configurazione di rete di un Server di scalabilità orizzontale processo hardware e software.</span><span class="sxs-lookup"><span data-stu-id="d5c86-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d5c86-108">[Pianificazione della capacità](site-recovery-capacity-planner.md) è tooensure un passaggio importante distribuire hello processo Server di scalabilità orizzontale con una configurazione adatta i requisiti di carico.</span><span class="sxs-lookup"><span data-stu-id="d5c86-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="d5c86-109">Altre informazioni sulle [caratteristiche di scalabilità per un server di elaborazione con scalabilità orizzontale](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="d5c86-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="d5c86-110">Download del software Server di scalabilità orizzontale processo hello</span><span class="sxs-lookup"><span data-stu-id="d5c86-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="d5c86-111">Accedere toohello tooyour Azure portal e passare credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d5c86-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="d5c86-112">Sfoglia troppo**infrastruttura di Site Recovery** > **server di configurazione** (in VMware per la & macchine fisiche).</span><span class="sxs-lookup"><span data-stu-id="d5c86-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="d5c86-113">Selezionare il toodrill di server di configurazione verso il basso nella pagina dei dettagli del server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d5c86-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="d5c86-114">Fare clic su hello **+ Server di elaborazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d5c86-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="d5c86-115">In hello **server di elaborazione aggiungere** selezionare **distribuzione una scalabilità orizzontale di un processo Server on-premise** opzione hello **specificare dove toodeploy il server di elaborazione** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="d5c86-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Pagina di aggiunta server](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="d5c86-117">Fare clic su hello **hello Download installazione unificata di Microsoft Azure Site Recovery** collegamento toodownload hello più recente di installazione di Server di elaborazione hello scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d5c86-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="d5c86-118">Hello la versione del Server di scalabilità orizzontale processo deve essere uguale tooor inferiore alla versione di hello del Server di configurazione in esecuzione nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d5c86-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="d5c86-119">Compatibilità di versione tooensure un modo semplice è toouse hello stessi bit di installazione che è utilizzato recentemente tooinstall/aggiornare il Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5c86-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="d5c86-120">Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dall'interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="d5c86-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="d5c86-121">Se hai tooscale orizzontalmente la distribuzione oltre 200 macchine di origine, oppure un totale giornaliero di varianza del tasso di più di 2 TB, è necessario volume di traffico hello toohandle server processo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="d5c86-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="d5c86-122">Controllare hello [consigli per i server di elaborazione di dimensioni](#size-recommendations-for-the-process-server), quindi seguire queste istruzioni tooset dei server di elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="d5c86-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="d5c86-123">Dopo aver configurato il server di hello, eseguire la migrazione toouse macchine di origine è.</span><span class="sxs-lookup"><span data-stu-id="d5c86-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="d5c86-124">Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="d5c86-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="d5c86-125">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="d5c86-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="d5c86-126">Argomenti della riga di comando del programma di installazione del server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d5c86-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="d5c86-127">Creare un file di configurazione delle impostazioni del proxy</span><span class="sxs-lookup"><span data-stu-id="d5c86-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="d5c86-128">Il parametro ProxySettingsFilePath prende un file come input.</span><span class="sxs-lookup"><span data-stu-id="d5c86-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="d5c86-129">Creare file utilizzando hello seguente formattare e passarlo come parametro di input ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="d5c86-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="d5c86-130">Modifica delle impostazioni proxy per il server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="d5c86-131">Accedere al server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d5c86-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="d5c86-132">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5c86-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="d5c86-133">Eseguire hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="d5c86-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="d5c86-134">Quindi cerca nella directory toohello **%PROGRAMDATA%\ASR\Agent** e hello esecuzione comando seguente</span><span class="sxs-lookup"><span data-stu-id="d5c86-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="d5c86-135">Nuova registrazione di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="d5c86-136">Quindi aprire un prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5c86-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="d5c86-137">Sfogliare la directory toohello **%PROGRAMDATA%\ASR\Agent** ed eseguire il comando hello</span><span class="sxs-lookup"><span data-stu-id="d5c86-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="d5c86-138">Aggiornamento di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="d5c86-139">Rimozione di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="d5c86-140">Assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="d5c86-140">Ensure that:</span></span>
  - <span data-ttu-id="d5c86-141">Mostra lo stato della connessione del Server di configurazione come **connesso** in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5c86-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="d5c86-142">Server di elaborazione è comunque possibile toocommunicate con il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d5c86-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="d5c86-143">Accedere come amministratore server di elaborazione toohello</span><span class="sxs-lookup"><span data-stu-id="d5c86-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="d5c86-144">Scegliere Pannello di controllo > Programma > Disinstallare programmi</span><span class="sxs-lookup"><span data-stu-id="d5c86-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="d5c86-145">Disinstallare i programmi di hello in sequenza hello fornito seguente:</span><span class="sxs-lookup"><span data-stu-id="d5c86-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="d5c86-146">Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d5c86-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="d5c86-147">Dipendenze del server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d5c86-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="d5c86-148">Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d5c86-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="d5c86-149">Può richiedere fino too15 minuti per tooreflect l'eliminazione di Server di elaborazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c86-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="d5c86-150">Se il server di elaborazione di hello è Impossibile toocommunicate con hello del Server di configurazione (stato di connessione nel portale è disconnesso), è necessario toofollow hello seguendo i passaggi toopurge da hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5c86-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="d5c86-151">Annullamento della registrazione di un server di elaborazione con scalabilità orizzontale disconnesso da un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="d5c86-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="d5c86-152">Requisiti per il ridimensionamento di un server di elaborazione con scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="d5c86-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="d5c86-153">**Server di elaborazione aggiuntivo**</span><span class="sxs-lookup"><span data-stu-id="d5c86-153">**Additional process server**</span></span> | <span data-ttu-id="d5c86-154">**Dimensione disco cache**</span><span class="sxs-lookup"><span data-stu-id="d5c86-154">**Cache disk size**</span></span> | <span data-ttu-id="d5c86-155">**Frequenza di modifica dei dati**</span><span class="sxs-lookup"><span data-stu-id="d5c86-155">**Data change rate**</span></span> | <span data-ttu-id="d5c86-156">**Computer protetti**</span><span class="sxs-lookup"><span data-stu-id="d5c86-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="d5c86-157">4 vCPU (2 socket * 2 core a 2,5 GHz), 8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="d5c86-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="d5c86-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="d5c86-158">300 GB</span></span> |<span data-ttu-id="d5c86-159">250 GB o inferiore</span><span class="sxs-lookup"><span data-stu-id="d5c86-159">250 GB or less</span></span> |<span data-ttu-id="d5c86-160">Replicare un massimo di 85 computer.</span><span class="sxs-lookup"><span data-stu-id="d5c86-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="d5c86-161">8 vCPU (2 socket * 4 core a 2,5 GHz), 12 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="d5c86-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="d5c86-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="d5c86-162">600 GB</span></span> |<span data-ttu-id="d5c86-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="d5c86-163">250 GB too1 TB</span></span> |<span data-ttu-id="d5c86-164">Replicare tra 85 e 150 computer.</span><span class="sxs-lookup"><span data-stu-id="d5c86-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="d5c86-165">12 vCPU (2 socket * 6 core a 2,5 GHz), 24 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="d5c86-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="d5c86-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="d5c86-166">1 TB</span></span> |<span data-ttu-id="d5c86-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="d5c86-167">1 TB too2 TB</span></span> |<span data-ttu-id="d5c86-168">Replicare tra 150 e 225 computer.</span><span class="sxs-lookup"><span data-stu-id="d5c86-168">Replicate between 150-225 machines.</span></span> |
