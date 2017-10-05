---
title: " Gestire un server di configurazione in Azure Site Recovery | Microsoft Docs"
description: L'articolo descrive come impostare e gestire un server di configurazione.
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="aa694-103">Gestire un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-103">Manage a Configuration Server</span></span>

<span data-ttu-id="aa694-104">Il server di configurazione funge da coordinatore tra i servizi di Site Recovery e l'infrastruttura locale in uso.</span><span class="sxs-lookup"><span data-stu-id="aa694-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="aa694-105">Questo articolo illustra come impostare, configurare e gestire il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa694-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa694-106">Prerequisites</span></span>
<span data-ttu-id="aa694-107">La tabella seguente elenca i requisiti minimi hardware, software e di rete richiesti per impostare un server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="aa694-108">La [pianificazione della capacità](site-recovery-capacity-planner.md) è un passaggio importante per assicurarsi di distribuire un server di configurazione con una configurazione adatta ai requisiti di carico.</span><span class="sxs-lookup"><span data-stu-id="aa694-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="aa694-109">Per altre informazioni, vedere la sezione [Requisiti di dimensione per un server di configurazione](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="aa694-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="aa694-110">Download del software del server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="aa694-111">Accedere al portale di Azure e passare all'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="aa694-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="aa694-112">Passare a **Infrastruttura di Site Recovery** > **Server di configurazione** (in For VMware & Physical Machines (Computer VMware e fisici)).</span><span class="sxs-lookup"><span data-stu-id="aa694-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Pagina di aggiunta server](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="aa694-114">Fare clic sul pulsante **+Servers** (+Server).</span><span class="sxs-lookup"><span data-stu-id="aa694-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="aa694-115">Nella pagina **Add Server** (Aggiungi server) fare clic sul pulsante Download (Scarica) per scaricare la chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="aa694-116">Questa chiave viene usata durante l'installazione del server di configurazione ai fini della registrazione con il servizio Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa694-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="aa694-117">Fare clic sul collegamento **Download the Microsoft Azure Site Recovery Unified Setup** (Scarica l'installazione unificata di Microsoft Azure Site Recovery) per scaricare la versione più recente del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Pagina di download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="aa694-119">La versione più recente del server di configurazione può essere scaricata direttamente dalla [pagina di download dell'Area download Microsoft](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="aa694-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="aa694-120">Installazione e registrazione di un server di configurazione dall'interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="aa694-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="aa694-121">Installazione e registrazione di un server di configurazione dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="aa694-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="aa694-122">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="aa694-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="aa694-123">Argomenti della riga di comando del programma di installazione del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="aa694-124">Creare un file di credenziali di MySql</span><span class="sxs-lookup"><span data-stu-id="aa694-124">Create a MySql credentials file</span></span>
<span data-ttu-id="aa694-125">Il parametro MySQLCredsFilePath prende un file come input.</span><span class="sxs-lookup"><span data-stu-id="aa694-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="aa694-126">Creare il file usando il formato seguente e passarlo come parametro MySQLCredsFilePath di input.</span><span class="sxs-lookup"><span data-stu-id="aa694-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="aa694-127">Creare un file di configurazione delle impostazioni del proxy</span><span class="sxs-lookup"><span data-stu-id="aa694-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="aa694-128">Il parametro ProxySettingsFilePath prende un file come input.</span><span class="sxs-lookup"><span data-stu-id="aa694-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="aa694-129">Creare il file usando il formato seguente e passarlo come parametro ProxySettingsFilePath di input.</span><span class="sxs-lookup"><span data-stu-id="aa694-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="aa694-130">Modifica delle impostazioni del proxy per il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="aa694-131">Accedere al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="aa694-132">Avviare il file cspsconfigtool.exe usando il relativo collegamento.</span><span class="sxs-lookup"><span data-stu-id="aa694-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="aa694-133">Fare clic sulla scheda **Vault Registration** (Registrazione dell'insieme di credenziali).</span><span class="sxs-lookup"><span data-stu-id="aa694-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="aa694-134">Scaricare un nuovo file di registrazione dell'insieme di credenziali dal portale e fornirlo come input allo strumento.</span><span class="sxs-lookup"><span data-stu-id="aa694-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="aa694-136">Specificare i dettagli del nuovo server proxy e fare clic sul pulsante **Register** (Registra).</span><span class="sxs-lookup"><span data-stu-id="aa694-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="aa694-137">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="aa694-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="aa694-138">Eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="aa694-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="aa694-139">Se sono presenti server di elaborazione con scalabilità orizzontale associati a questo server di configurazione, è necessario [correggere le impostazioni del proxy in tutti i server di elaborazione con scalabilità orizzontale](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa694-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="aa694-140">Registrare un server di configurazione con lo stesso insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="aa694-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="aa694-141">Accedere al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="aa694-142">Avviare il file cspsconfigtool.exe usando il relativo collegamento sul desktop.</span><span class="sxs-lookup"><span data-stu-id="aa694-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="aa694-143">Fare clic sulla scheda **Vault Registration** (Registrazione dell'insieme di credenziali).</span><span class="sxs-lookup"><span data-stu-id="aa694-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="aa694-144">Scaricare un nuovo file di registrazione dal portale e fornirlo come input allo strumento.</span><span class="sxs-lookup"><span data-stu-id="aa694-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="aa694-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="aa694-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="aa694-146">Specificare i dettagli del server proxy e fare clic sul pulsante **Register** (Registra).</span><span class="sxs-lookup"><span data-stu-id="aa694-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="aa694-147">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="aa694-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="aa694-148">Eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="aa694-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="aa694-149">Se sono presenti server di elaborazione con scalabilità orizzontale associati a questo server di configurazione, è necessario [registrare di nuovo tutti i server di elaborazione con scalabilità orizzontale](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa694-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="aa694-150">Registrazione di un server di configurazione con un insieme di credenziali di Servizi di ripristino diverso.</span><span class="sxs-lookup"><span data-stu-id="aa694-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="aa694-151">Accedere al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="aa694-152">Al prompt dei comandi dell'amministratore, eseguire il comando</span><span class="sxs-lookup"><span data-stu-id="aa694-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="aa694-153">Avviare il file cspsconfigtool.exe usando il relativo collegamento.</span><span class="sxs-lookup"><span data-stu-id="aa694-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="aa694-154">Fare clic sulla scheda **Vault Registration** (Registrazione dell'insieme di credenziali).</span><span class="sxs-lookup"><span data-stu-id="aa694-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="aa694-155">Scaricare un nuovo file di registrazione dal portale e fornirlo come input allo strumento.</span><span class="sxs-lookup"><span data-stu-id="aa694-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="aa694-157">Specificare i dettagli del server proxy e fare clic sul pulsante **Register** (Registra).</span><span class="sxs-lookup"><span data-stu-id="aa694-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="aa694-158">Aprire una finestra di prompt dei comandi di PowerShell per amministratore.</span><span class="sxs-lookup"><span data-stu-id="aa694-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="aa694-159">Eseguire il comando seguente</span><span class="sxs-lookup"><span data-stu-id="aa694-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="aa694-160">Rimozione delle autorizzazioni per un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="aa694-161">Prima di iniziare a rimuovere le autorizzazioni per il server di configurazione, assicurarsi di eseguire queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="aa694-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="aa694-162">Disabilitare la protezione di tutte le macchine virtuali in questo server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="aa694-163">Annullare l'associazione di tutti i criteri di replica dal server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="aa694-164">Eliminare tutti i server VCenter/host vSphere associati al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="aa694-165">Eliminare il server di configurazione dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="aa694-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="aa694-166">Nel portale di Azure passare a **Infrastruttura di Site Recovery** > **Server di configurazione** dal menu Insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="aa694-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="aa694-167">Fare clic sul server di configurazione per cui si desidera rimuovere le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="aa694-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="aa694-168">Nella pagina dei dettagli del server di configurazione fare clic sul pulsante Elimina.</span><span class="sxs-lookup"><span data-stu-id="aa694-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="aa694-170">Fare clic su **Sì** per confermare l'eliminazione del server.</span><span class="sxs-lookup"><span data-stu-id="aa694-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="aa694-171">Se il server di configurazione è associato a macchine virtuali, criteri di replica o server vCenter/host vSphere, non è possibile eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="aa694-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="aa694-172">Eliminare queste entità prima di provare a eliminare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="aa694-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="aa694-173">Disinstallare il software del server di configurazione e le relative dipendenze</span><span class="sxs-lookup"><span data-stu-id="aa694-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="aa694-174">Se si intende riutilizzare il server di configurazione con Azure Site Recovery, è possibile andare direttamente al passaggio 4</span><span class="sxs-lookup"><span data-stu-id="aa694-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="aa694-175">Accedere al server di configurazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="aa694-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="aa694-176">Scegliere Pannello di controllo > Programma > Disinstallare programmi</span><span class="sxs-lookup"><span data-stu-id="aa694-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="aa694-177">Disinstallare i programmi nella sequenza seguente:</span><span class="sxs-lookup"><span data-stu-id="aa694-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="aa694-178">Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aa694-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="aa694-179">Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="aa694-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="aa694-180">Provider di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa694-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="aa694-181">Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa694-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="aa694-182">Dipendenze del server di configurazione di Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa694-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="aa694-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="aa694-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="aa694-184">Al prompt dei comandi dell'amministratore, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="aa694-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="aa694-185">Rinnovare i certificati SSL (Server Secure Socket Layer) di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="aa694-186">Il server di configurazione include un server Web integrato che si occupa di orchestrare le attività del servizio Mobility, dei server di elaborazione e dei server di destinazione master connessi al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="aa694-187">Il server Web del server di configurazione usa un certificato SSL per l'autenticazione dei client.</span><span class="sxs-lookup"><span data-stu-id="aa694-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="aa694-188">Questo certificato ha una scadenza di tre anni e può essere rinnovato in qualsiasi momento usando il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="aa694-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="aa694-189">La scadenza del certificato può avvenire solo nella versione 9.4.XXXX.X o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="aa694-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="aa694-190">Aggiornare tutti i componenti di Azure Site Recovery (server di configurazione, server di elaborazione, server di destinazione master e servizio Mobility) prima di avviare il flusso di lavoro relativo al rinnovo dei certificati.</span><span class="sxs-lookup"><span data-stu-id="aa694-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="aa694-191">Nel portale di Azure passare a Insieme di credenziali > Infrastruttura di Site Recovery > Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa694-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="aa694-192">Fare clic sul server di configurazione per il quale è necessario rinnovare il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="aa694-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="aa694-193">Nell'ambito dell'integrità del server di configurazione, è possibile visualizzare la data di scadenza del certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="aa694-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="aa694-194">Rinnovare il certificato facendo clic sull'azione **Rinnova i certificati** come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="aa694-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="aa694-196">Avviso di scadenza del certificato SSL</span><span class="sxs-lookup"><span data-stu-id="aa694-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="aa694-197">La validità del certificato SSL per tutte le installazioni eseguite prima di maggio 2016 è stata impostata su un anno.</span><span class="sxs-lookup"><span data-stu-id="aa694-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="aa694-198">Nel portale di Azure hanno iniziato a comparire notifiche di scadenza certificato.</span><span class="sxs-lookup"><span data-stu-id="aa694-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="aa694-199">Due mesi prima che il certificato SSL del server di configurazione scada il servizio inizia ad avvertire gli utenti tramite il portale di Azure e la posta elettronica. Per ricevere questi avvisi è necessario sottoscrivere le notifiche di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa694-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="aa694-200">Si inizia a comparire un banner di notifica nella pagina delle risorse dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="aa694-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="aa694-202">Fare clic sul banner per visualizzare informazioni aggiuntive sulla scadenza del certificato.</span><span class="sxs-lookup"><span data-stu-id="aa694-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="aa694-204">Se al posto del pulsante **Renew Now** (Rinnova ora) viene visualizzato un pulsante **Upgrade Now** (Aggiorna ora).</span><span class="sxs-lookup"><span data-stu-id="aa694-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="aa694-205">Significa che esistono alcuni componenti nell'ambiente che non sono stati ancora aggiornati alla versione 9.4.xxxx.x o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="aa694-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="aa694-206">Requisiti di dimensione per un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa694-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="aa694-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="aa694-207">**CPU**</span></span> | <span data-ttu-id="aa694-208">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="aa694-208">**Memory**</span></span> | <span data-ttu-id="aa694-209">**Dimensione disco cache**</span><span class="sxs-lookup"><span data-stu-id="aa694-209">**Cache disk size**</span></span> | <span data-ttu-id="aa694-210">**Frequenza di modifica dei dati**</span><span class="sxs-lookup"><span data-stu-id="aa694-210">**Data change rate**</span></span> | <span data-ttu-id="aa694-211">**Computer protetti**</span><span class="sxs-lookup"><span data-stu-id="aa694-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="aa694-212">8 vCPU (2 socket * 4 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="aa694-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="aa694-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="aa694-213">16 GB</span></span> |<span data-ttu-id="aa694-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="aa694-214">300 GB</span></span> |<span data-ttu-id="aa694-215">500 GB o inferiore</span><span class="sxs-lookup"><span data-stu-id="aa694-215">500 GB or less</span></span> |<span data-ttu-id="aa694-216">Replicare meno di 100 computer.</span><span class="sxs-lookup"><span data-stu-id="aa694-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="aa694-217">12 vCPU (2 socket * 6 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="aa694-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="aa694-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="aa694-218">18 GB</span></span> |<span data-ttu-id="aa694-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="aa694-219">600 GB</span></span> |<span data-ttu-id="aa694-220">Da 500 GB a 1 TB</span><span class="sxs-lookup"><span data-stu-id="aa694-220">500 GB to 1 TB</span></span> |<span data-ttu-id="aa694-221">Replicare tra 100 e 150 computer.</span><span class="sxs-lookup"><span data-stu-id="aa694-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="aa694-222">16 vCPU (2 socket * 8 core a 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="aa694-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="aa694-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="aa694-223">32 GB</span></span> |<span data-ttu-id="aa694-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="aa694-224">1 TB</span></span> |<span data-ttu-id="aa694-225">Da 1 TB a 2 TB</span><span class="sxs-lookup"><span data-stu-id="aa694-225">1 TB to 2 TB</span></span> |<span data-ttu-id="aa694-226">Replicare tra 150 e 200 computer.</span><span class="sxs-lookup"><span data-stu-id="aa694-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="aa694-227">Se la varianza dei dati giornalieri supera 2 TB o si intende replicare più di 200 macchine virtuali, è consigliabile distribuire ulteriori server di elaborazione per bilanciare il traffico di replica.</span><span class="sxs-lookup"><span data-stu-id="aa694-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="aa694-228">Altre informazioni su come distribuire i server di elaborazione con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="aa694-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="aa694-229">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="aa694-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
