---
title: " Gestire un server di configurazione in Azure Site Recovery | Microsoft Docs"
description: Questo articolo viene descritto come tooset e gestire un Server di configurazione.
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="e9016-103">Gestire un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="e9016-103">Manage a Configuration Server</span></span>

<span data-ttu-id="e9016-104">Configurazione Server funziona come un coordinatore tra servizi di ripristino del sito di hello e l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="e9016-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="e9016-105">Questo articolo descrive come è possibile impostare, configurare e gestire hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9016-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e9016-106">Prerequisites</span></span>
<span data-ttu-id="e9016-107">di seguito Hello sono hello minimo hardware, software e tooset necessarie di configurazione di rete di un Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e9016-108">[Pianificazione della capacità](site-recovery-capacity-planner.md) è tooensure un passaggio importante distribuire hello Server di configurazione con una configurazione adatta i requisiti di carico.</span><span class="sxs-lookup"><span data-stu-id="e9016-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="e9016-109">Per altre informazioni, vedere la sezione [Requisiti di dimensione per un server di configurazione](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="e9016-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="e9016-110">Download del software Server di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="e9016-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="e9016-111">Accedere toohello tooyour Azure portal e passare credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e9016-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="e9016-112">Sfoglia troppo**infrastruttura di Site Recovery** > **server di configurazione** (in VMware per la & macchine fisiche).</span><span class="sxs-lookup"><span data-stu-id="e9016-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Pagina di aggiunta server](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="e9016-114">Fare clic su hello **+ server** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e9016-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="e9016-115">In hello **Aggiungi Server** pagina, fare clic su chiave di registrazione hello toodownload pulsante Download hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="e9016-116">Questa chiave è necessaria durante hello del Server di configurazione installazione tooregister con il servizio di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e9016-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="e9016-117">Fare clic su hello **hello Download installazione unificata di Microsoft Azure Site Recovery** collegamento toodownload hello ultima versione di hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Pagina di download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="e9016-119">La versione più recente di hello del Server di configurazione può essere scaricata direttamente da [pagina di download di Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="e9016-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="e9016-120">Installazione e registrazione di un server di configurazione dall'interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="e9016-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="e9016-121">Installazione e registrazione di un server di configurazione dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="e9016-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="e9016-122">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="e9016-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="e9016-123">Argomenti della riga di comando del programma di installazione del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="e9016-124">Creare un file di credenziali di MySql</span><span class="sxs-lookup"><span data-stu-id="e9016-124">Create a MySql credentials file</span></span>
<span data-ttu-id="e9016-125">Il parametro MySQLCredsFilePath prende un file come input.</span><span class="sxs-lookup"><span data-stu-id="e9016-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e9016-126">Creare file hello utilizzando hello seguente formattare e passarlo come parametro di input MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="e9016-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="e9016-127">Creare un file di configurazione delle impostazioni del proxy</span><span class="sxs-lookup"><span data-stu-id="e9016-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="e9016-128">Il parametro ProxySettingsFilePath prende un file come input.</span><span class="sxs-lookup"><span data-stu-id="e9016-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e9016-129">Creare file hello utilizzando hello seguente formattare e passarlo come parametro di input ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="e9016-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="e9016-130">Modifica delle impostazioni del proxy per il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="e9016-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="e9016-131">Account di accesso tooyour Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e9016-132">Avviare cspsconfigtool.exe hello utilizzando il collegamento di hello nel.</span><span class="sxs-lookup"><span data-stu-id="e9016-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="e9016-133">Fare clic su hello **registrazione insieme credenziali** scheda.</span><span class="sxs-lookup"><span data-stu-id="e9016-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="e9016-134">Scaricare un nuovo file di registrazione dell'insieme di credenziali dal portale hello e fornirlo come input toohello strumento.</span><span class="sxs-lookup"><span data-stu-id="e9016-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="e9016-136">Fornire dettagli hello del nuovo Server Proxy e fare clic su hello **registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e9016-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="e9016-137">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="e9016-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="e9016-138">Eseguire hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="e9016-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="e9016-139">Se dispone di server di scalabilità orizzontale processo collegato toothis Server di configurazione, è necessario troppo[correggere le impostazioni del proxy hello in tutti i server di scalabilità orizzontale processo hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e9016-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="e9016-140">Registrare un Server di configurazione con hello stesso archivio di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e9016-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="e9016-141">Account di accesso tooyour Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="e9016-142">Avvia cspsconfigtool.exe hello utilizzando il collegamento di hello sul desktop.</span><span class="sxs-lookup"><span data-stu-id="e9016-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="e9016-143">Fare clic su hello **registrazione insieme credenziali** scheda.</span><span class="sxs-lookup"><span data-stu-id="e9016-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="e9016-144">Scaricare un nuovo file di registrazione dal portale hello e fornirlo come input toohello strumento.</span><span class="sxs-lookup"><span data-stu-id="e9016-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="e9016-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="e9016-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="e9016-146">Fornire i dettagli del Server Proxy hello e fare clic su hello **registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e9016-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="e9016-147">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="e9016-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="e9016-148">Eseguire hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="e9016-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="e9016-149">Se dispone di server di scalabilità orizzontale processo collegato toothis Server di configurazione, è necessario troppo[registrare nuovamente tutti i server di scalabilità orizzontale processo hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e9016-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="e9016-150">Registrazione di un server di configurazione con un insieme di credenziali di Servizi di ripristino diverso.</span><span class="sxs-lookup"><span data-stu-id="e9016-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="e9016-151">Account di accesso tooyour Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e9016-152">da un prompt dei comandi di amministratore, eseguire il comando di hello</span><span class="sxs-lookup"><span data-stu-id="e9016-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="e9016-153">Avviare cspsconfigtool.exe hello utilizzando il collegamento di hello nel.</span><span class="sxs-lookup"><span data-stu-id="e9016-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="e9016-154">Fare clic su hello **registrazione insieme credenziali** scheda.</span><span class="sxs-lookup"><span data-stu-id="e9016-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="e9016-155">Scaricare un nuovo file di registrazione dal portale hello e fornirlo come input toohello strumento.</span><span class="sxs-lookup"><span data-stu-id="e9016-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="e9016-157">Fornire i dettagli del Server Proxy hello e fare clic su hello **registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e9016-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="e9016-158">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="e9016-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="e9016-159">Eseguire hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="e9016-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="e9016-160">Rimozione delle autorizzazioni per un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="e9016-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="e9016-161">Verificare i seguenti hello prima di iniziare rimuovere il Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="e9016-162">Disabilitare la protezione di tutte le macchine virtuali in questo server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="e9016-163">Annullare l'associazione di tutti i criteri di replica dal Server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="e9016-164">Eliminare tutti gli host del server/vSphere vCenter toohello associato Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="e9016-165">Eliminare hello del Server di configurazione dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e9016-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="e9016-166">Nel portale di Azure, passare troppo**infrastruttura di Site Recovery** > **server di configurazione** dal menu di hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e9016-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="e9016-167">Fare clic su Server di configurazione che si desidera toodecommission hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="e9016-168">Nella pagina dettagli del Server di configurazione hello, fare clic sul pulsante Elimina hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="e9016-170">Fare clic su **Sì** tooconfirm l'eliminazione di hello del server di hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="e9016-171">Se si dispone di macchine virtuali, criteri di replica o vCenter server/vSphere host associato a questo Server di configurazione, è possibile eliminare il server di hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="e9016-172">Eliminare queste entità prima di provare l'insieme di credenziali toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="e9016-173">Disinstallare il software di Server di configurazione hello e le relative dipendenze</span><span class="sxs-lookup"><span data-stu-id="e9016-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="e9016-174">Se si prevede di nuovo tooreuse hello configurazione Server con Azure Site Recovery, quindi è possibile ignorare toostep 4 direttamente</span><span class="sxs-lookup"><span data-stu-id="e9016-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="e9016-175">Accedere come amministratore toohello Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="e9016-176">Scegliere Pannello di controllo > Programma > Disinstallare programmi</span><span class="sxs-lookup"><span data-stu-id="e9016-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="e9016-177">Disinstallare programmi hello in hello seguente sequenza:</span><span class="sxs-lookup"><span data-stu-id="e9016-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="e9016-178">Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e9016-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="e9016-179">Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="e9016-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="e9016-180">Provider di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9016-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="e9016-181">Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9016-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="e9016-182">Dipendenze del server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9016-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="e9016-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="e9016-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="e9016-184">Eseguire hello comando dal seguente e prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e9016-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="e9016-185">Rinnovare i certificati SSL (Server Secure Socket Layer) di configurazione</span><span class="sxs-lookup"><span data-stu-id="e9016-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="e9016-186">Hello del Server di configurazione è un server Web incorporato, che coordina le attività di hello di hello servizio di mobilità, i server di elaborazione e i server di destinazione Master connessi toohello Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="e9016-187">server Web del Server di configurazione Hello utilizza un tooauthenticate certificato SSL dei client.</span><span class="sxs-lookup"><span data-stu-id="e9016-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="e9016-188">Questo certificato ha una scadenza di tre anni e può essere rinnovato in qualsiasi momento usando hello seguente metodo:</span><span class="sxs-lookup"><span data-stu-id="e9016-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="e9016-189">La scadenza del certificato può avvenire solo nella versione 9.4.XXXX.X o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e9016-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="e9016-190">Aggiornare tutti i componenti di Azure Site Recovery hello (Server di configurazione, Server di elaborazione, Server di destinazione Master, servizio di mobilità) prima di iniziare del flusso di lavoro di hello rinnovare i certificati.</span><span class="sxs-lookup"><span data-stu-id="e9016-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="e9016-191">In hello portale di Azure, passare tooyour insieme di credenziali > infrastruttura di Site Recovery > Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9016-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="e9016-192">Fare clic su hello del Server di configurazione per il quale è necessario toorenew hello certificato SSL per.</span><span class="sxs-lookup"><span data-stu-id="e9016-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="e9016-193">In hello integrità del Server di configurazione, è possibile visualizzare la data di scadenza hello per hello certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="e9016-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="e9016-194">Rinnova certificato di hello facendo hello **rinnovare i certificati** azione, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="e9016-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="e9016-196">Avviso di scadenza del certificato SSL</span><span class="sxs-lookup"><span data-stu-id="e9016-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="e9016-197">Hello validità del certificato SSL per tutte le installazioni che si sono verificati prima di maggio 2016 è stata impostata tooone anno.</span><span class="sxs-lookup"><span data-stu-id="e9016-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="e9016-198">si è avviato visualizzare notifiche di scadenza certificato viene visualizzato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="e9016-199">Se il certificato SSL del Server di configurazione hello verrà tooexpire in hello due mesi successivi, il servizio di hello avvia la notifica agli utenti tramite il portale di Azure hello & posta elettronica (è necessario toobe sottoscritto tooAzure Site Recovery notifiche).</span><span class="sxs-lookup"><span data-stu-id="e9016-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="e9016-200">Iniziare a vedere un banner di notifica nella pagina delle risorse dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="e9016-202">Fare clic su hello banner tooget ulteriori informazioni sulla scadenza del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="e9016-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="e9016-204">Se al posto del pulsante **Renew Now** (Rinnova ora) viene visualizzato un pulsante **Upgrade Now** (Aggiorna ora).</span><span class="sxs-lookup"><span data-stu-id="e9016-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="e9016-205">Questo significa che sono disponibili alcuni componenti nell'ambiente che non sono ancora stato aggiornato too9.4.xxxx.x o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e9016-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="e9016-206">Requisiti di dimensione per un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="e9016-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="e9016-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e9016-207">**CPU**</span></span> | <span data-ttu-id="e9016-208">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="e9016-208">**Memory**</span></span> | <span data-ttu-id="e9016-209">**Dimensione disco cache**</span><span class="sxs-lookup"><span data-stu-id="e9016-209">**Cache disk size**</span></span> | <span data-ttu-id="e9016-210">**Frequenza di modifica dei dati**</span><span class="sxs-lookup"><span data-stu-id="e9016-210">**Data change rate**</span></span> | <span data-ttu-id="e9016-211">**Computer protetti**</span><span class="sxs-lookup"><span data-stu-id="e9016-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e9016-212">8 vCPU (2 socket * 4 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9016-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9016-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="e9016-213">16 GB</span></span> |<span data-ttu-id="e9016-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="e9016-214">300 GB</span></span> |<span data-ttu-id="e9016-215">500 GB o inferiore</span><span class="sxs-lookup"><span data-stu-id="e9016-215">500 GB or less</span></span> |<span data-ttu-id="e9016-216">Replicare meno di 100 computer.</span><span class="sxs-lookup"><span data-stu-id="e9016-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="e9016-217">12 vCPU (2 socket * 6 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9016-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9016-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="e9016-218">18 GB</span></span> |<span data-ttu-id="e9016-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="e9016-219">600 GB</span></span> |<span data-ttu-id="e9016-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="e9016-220">500 GB too1 TB</span></span> |<span data-ttu-id="e9016-221">Replicare tra 100 e 150 computer.</span><span class="sxs-lookup"><span data-stu-id="e9016-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="e9016-222">16 vCPU (2 socket * 8 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9016-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9016-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="e9016-223">32 GB</span></span> |<span data-ttu-id="e9016-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="e9016-224">1 TB</span></span> |<span data-ttu-id="e9016-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="e9016-225">1 TB too2 TB</span></span> |<span data-ttu-id="e9016-226">Replicare tra 150 e 200 computer.</span><span class="sxs-lookup"><span data-stu-id="e9016-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="e9016-227">Se la varianza dei dati giornaliera supera i 2 TB o tooreplicate si prevede più di 200 macchine virtuali, è consigliabile toodeploy processo aggiuntivo server tooload saldo hello il traffico di replica.</span><span class="sxs-lookup"><span data-stu-id="e9016-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="e9016-228">Altre informazioni su come server di toodeploy il processo di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="e9016-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="e9016-229">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="e9016-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
