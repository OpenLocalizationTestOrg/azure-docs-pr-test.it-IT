---
title: aaaEnable Desktop remoto in un servizio Cloud di Azure | Documenti Microsoft
description: "La modalità di cloud di azure di tooconfigure connessioni desktop remoto tooallow all'applicazione di servizio"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="2a250-103">Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="2a250-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a250-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2a250-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="2a250-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="2a250-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="2a250-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a250-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="2a250-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a250-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="2a250-108">È possibile abilitare una connessione Desktop remoto nel ruolo durante lo sviluppo includendo i moduli di Desktop remoto hello nella definizione del servizio oppure è possibile scegliere tooenable Desktop remoto tramite hello estensione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2a250-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="2a250-109">Hello approccio consigliato è toouse hello Desktop remoto estensione come è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello senza tooredeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a250-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="2a250-110">Configurare Desktop remoto dal portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="2a250-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="2a250-111">portale di Azure classico Hello utilizza l'approccio di estensione di Desktop remoto di hello in cui è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="2a250-112">Hello **configura** pagina per il servizio cloud consente tooenable Desktop remoto, account di amministratore locale modifica hello usato tooconnect toohello le macchine virtuali, il certificato di hello usati nell'autenticazione e imposta hello Data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="2a250-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="2a250-113">Fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="2a250-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="2a250-114">Fare clic su hello **remoto** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Servizi cloud remoti](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="2a250-116">Tutte le istanze del ruolo verranno riavviate la prima volta che si abilita Desktop remoto e si fa clic su OK (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="2a250-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="2a250-117">tooprevent un riavvio, la password di hello hello certificato tooencrypt utilizzato deve essere installato nel ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="2a250-118">un riavvio, tooprevent [caricare un certificato per il servizio cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e restituirne toothis finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2a250-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="2a250-119">In **ruoli**selezionare ruolo hello desiderato tooupdate **tutti** per tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="2a250-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="2a250-120">Apportare le hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="2a250-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="2a250-121">Desktop remoto, seleziona hello tooenable **Abilita Desktop remoto** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="2a250-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="2a250-122">Desktop remoto, la casella di controllo crittografato hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="2a250-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="2a250-123">Creare un account toouse nelle connessioni Desktop remoto istanze del ruolo toohello.</span><span class="sxs-lookup"><span data-stu-id="2a250-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="2a250-124">Aggiornare la password di hello per l'account esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="2a250-125">Selezionare un toouse certificato caricato per l'autenticazione (caricamento hello certificato utilizzando **caricare** su hello **certificati** pagina) o creare un nuovo certificato.</span><span class="sxs-lookup"><span data-stu-id="2a250-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="2a250-126">Modificare la data di scadenza hello per la configurazione di Desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="2a250-127">Dopo aver completato gli aggiornamenti della configurazione, fare clic su **OK** (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="2a250-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="2a250-128">Accedere in remoto alle istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="2a250-128">Remote into role instances</span></span>
<span data-ttu-id="2a250-129">Dopo aver abilitato Desktop remoto per i ruoli di hello è possibile remota in un'istanza del ruolo tramite diversi strumenti.</span><span class="sxs-lookup"><span data-stu-id="2a250-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="2a250-130">istanza del ruolo tooa tooconnect dal portale di Azure classico hello:</span><span class="sxs-lookup"><span data-stu-id="2a250-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="2a250-131">Fare clic su **istanze** tooopen hello **istanze** pagina.</span><span class="sxs-lookup"><span data-stu-id="2a250-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="2a250-132">Selezionare un'istanza del ruolo per cui è configurato Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2a250-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="2a250-133">Fare clic su **Connetti**e seguire desktop hello tooopen istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="2a250-134">Fare clic su **aprire** e quindi **Connetti** toostart hello connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2a250-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="2a250-135">Utilizzare Visual Studio tooremote in un'istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="2a250-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="2a250-136">In Esplora server di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2a250-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="2a250-137">Espandere hello **Azure** > **servizi Cloud** > **[nome servizio cloud]** nodo.</span><span class="sxs-lookup"><span data-stu-id="2a250-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="2a250-138">Espandere **Gestione temporanea** o **Produzione**.</span><span class="sxs-lookup"><span data-stu-id="2a250-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="2a250-139">Espandere i singoli ruoli di hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="2a250-140">Fare doppio clic su una delle istanze del ruolo hello, fare clic su **connessione tramite Desktop remoto...** , quindi immettere nome utente hello e una password.</span><span class="sxs-lookup"><span data-stu-id="2a250-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Desktop remoto di Esplora server](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="2a250-142">Utilizzare PowerShell tooget hello RDP file</span><span class="sxs-lookup"><span data-stu-id="2a250-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="2a250-143">È possibile utilizzare hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) file RDP hello tooretrieve di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a250-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="2a250-144">È quindi possibile utilizzare il file RDP hello con servizio cloud di hello tooaccess connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2a250-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="2a250-145">A livello di codice, scaricare file RDP hello tramite hello API REST di gestione</span><span class="sxs-lookup"><span data-stu-id="2a250-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="2a250-146">È possibile utilizzare hello [scaricare il File RDP](https://msdn.microsoft.com/library/jj157183.aspx) file con estensione RDP hello toodownload operazione REST.</span><span class="sxs-lookup"><span data-stu-id="2a250-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="2a250-147">Desktop remoto nel file di definizione del servizio hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2a250-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="2a250-148">Questo metodo consente tooenable Desktop remoto per un'applicazione hello durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2a250-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="2a250-149">Questo approccio richiede password crittografate da archiviare nella configurazione del servizio file e qualsiasi configurazione di desktop remoto di aggiornamenti toohello richiederebbe una ridistribuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="2a250-150">Se si desidera tooavoid questi svantaggi, è necessario utilizzare l'estensione di desktop remoto hello basato approccio descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2a250-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="2a250-151">È possibile utilizzare Visual Studio troppo[abilitare una connessione desktop remoto](../vs-azure-tools-remote-desktop-roles.md) utilizzando l'approccio file di definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2a250-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="2a250-152">Hello riportato di seguito viene descritta la hello le modifiche necessarie toohello servizio modello file tooenable desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2a250-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="2a250-153">Visual Studio eseguirà automaticamente queste modifiche durante la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="2a250-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="2a250-154">Impostare la connessione di hello nel modello di servizio hello</span><span class="sxs-lookup"><span data-stu-id="2a250-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="2a250-155">Hello utilizzare **importazioni** hello tooimport elemento **RemoteAccess** modulo e hello **RemoteForwarder** modulo toohello [Servicedefinition](cloud-services-model-and-package.md#csdef) file.</span><span class="sxs-lookup"><span data-stu-id="2a250-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="2a250-156">Hello file di definizione del servizio deve essere simile toohello seguente esempio con hello `<Imports>` elemento aggiunto.</span><span class="sxs-lookup"><span data-stu-id="2a250-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="2a250-157">Hello [ServiceConfiguration. cscfg](cloud-services-model-and-package.md#cscfg) file deve essere simile toohello seguente esempio, si noti hello `<ConfigurationSettings>` e `<Certificates>` elementi.</span><span class="sxs-lookup"><span data-stu-id="2a250-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="2a250-158">Hello certificato specificato deve essere [caricato servizio cloud toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="2a250-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="2a250-159">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2a250-159">Additional Resources</span></span>
<span data-ttu-id="2a250-160">[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="2a250-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
