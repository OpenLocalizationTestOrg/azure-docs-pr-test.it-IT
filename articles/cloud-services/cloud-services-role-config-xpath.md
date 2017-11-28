---
title: il foglio informativo XPath di aaaCloud ruolo Servizi file config | Documenti Microsoft
description: "Hello varie impostazioni di XPath, che è possibile utilizzare nelle impostazioni del cloud servizio ruolo configurazione tooexpose hello come una variabile di ambiente."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="bf45c-103">Esporre le impostazioni di configurazione del ruolo come una variabile di ambiente con XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="bf45c-104">Lavoro del servizio cloud di hello o file di definizione del servizio di ruolo web, è possibile esporre i valori di configurazione di runtime come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="bf45c-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="bf45c-105">Hello valori XPath seguenti è supportato (che corrispondono a valori tooAPI).</span><span class="sxs-lookup"><span data-stu-id="bf45c-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="bf45c-106">Questi valori XPath sono disponibili anche tramite hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) libreria.</span><span class="sxs-lookup"><span data-stu-id="bf45c-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="bf45c-107">App in esecuzione nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="bf45c-107">App running in emulator</span></span>
<span data-ttu-id="bf45c-108">Indica che app hello è in esecuzione nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="bf45c-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-109">Type</span></span> | <span data-ttu-id="bf45c-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-111">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-111">XPath</span></span> |<span data-ttu-id="bf45c-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="bf45c-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="bf45c-113">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-113">Code</span></span> |<span data-ttu-id="bf45c-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="bf45c-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="bf45c-115">ID distribuzione</span><span class="sxs-lookup"><span data-stu-id="bf45c-115">Deployment ID</span></span>
<span data-ttu-id="bf45c-116">Recupera l'ID distribuzione hello per istanza hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="bf45c-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-117">Type</span></span> | <span data-ttu-id="bf45c-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-119">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-119">XPath</span></span> |<span data-ttu-id="bf45c-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="bf45c-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="bf45c-121">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-121">Code</span></span> |<span data-ttu-id="bf45c-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="bf45c-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="bf45c-123">ID ruolo</span><span class="sxs-lookup"><span data-stu-id="bf45c-123">Role ID</span></span>
<span data-ttu-id="bf45c-124">Recupera l'ID del ruolo per l'istanza di hello corrente hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="bf45c-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-125">Type</span></span> | <span data-ttu-id="bf45c-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-127">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-127">XPath</span></span> |<span data-ttu-id="bf45c-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="bf45c-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="bf45c-129">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-129">Code</span></span> |<span data-ttu-id="bf45c-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="bf45c-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="bf45c-131">Aggiornamento dominio</span><span class="sxs-lookup"><span data-stu-id="bf45c-131">Update domain</span></span>
<span data-ttu-id="bf45c-132">Recupera il dominio di aggiornamento hello dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="bf45c-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-133">Type</span></span> | <span data-ttu-id="bf45c-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-135">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-135">XPath</span></span> |<span data-ttu-id="bf45c-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="bf45c-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="bf45c-137">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-137">Code</span></span> |<span data-ttu-id="bf45c-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="bf45c-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="bf45c-139">Dominio di errore</span><span class="sxs-lookup"><span data-stu-id="bf45c-139">Fault domain</span></span>
<span data-ttu-id="bf45c-140">Recupera il dominio di errore hello dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="bf45c-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-141">Type</span></span> | <span data-ttu-id="bf45c-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-143">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-143">XPath</span></span> |<span data-ttu-id="bf45c-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="bf45c-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="bf45c-145">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-145">Code</span></span> |<span data-ttu-id="bf45c-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="bf45c-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="bf45c-147">Nome del ruolo</span><span class="sxs-lookup"><span data-stu-id="bf45c-147">Role name</span></span>
<span data-ttu-id="bf45c-148">Recupera il nome del ruolo hello di istanze di hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="bf45c-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-149">Type</span></span> | <span data-ttu-id="bf45c-150">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-151">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-151">XPath</span></span> |<span data-ttu-id="bf45c-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="bf45c-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="bf45c-153">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-153">Code</span></span> |<span data-ttu-id="bf45c-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="bf45c-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="bf45c-155">Impostazione di configurazione</span><span class="sxs-lookup"><span data-stu-id="bf45c-155">Config setting</span></span>
<span data-ttu-id="bf45c-156">Impostazione di configurazione specificato il valore hello recupera hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="bf45c-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-157">Type</span></span> | <span data-ttu-id="bf45c-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-159">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-159">XPath</span></span> |<span data-ttu-id="bf45c-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="bf45c-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="bf45c-161">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-161">Code</span></span> |<span data-ttu-id="bf45c-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="bf45c-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="bf45c-163">Percorso di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="bf45c-163">Local storage path</span></span>
<span data-ttu-id="bf45c-164">Recupera il percorso di archiviazione locale hello per istanza hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="bf45c-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-165">Type</span></span> | <span data-ttu-id="bf45c-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-167">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-167">XPath</span></span> |<span data-ttu-id="bf45c-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="bf45c-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="bf45c-169">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-169">Code</span></span> |<span data-ttu-id="bf45c-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="bf45c-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="bf45c-171">Dimensioni di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="bf45c-171">Local storage size</span></span>
<span data-ttu-id="bf45c-172">Recupera la dimensione hello di archiviazione locale di hello per istanza hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="bf45c-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-173">Type</span></span> | <span data-ttu-id="bf45c-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-175">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-175">XPath</span></span> |<span data-ttu-id="bf45c-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="bf45c-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="bf45c-177">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-177">Code</span></span> |<span data-ttu-id="bf45c-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="bf45c-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="bf45c-179">Protocollo di endpoint</span><span class="sxs-lookup"><span data-stu-id="bf45c-179">Endpoint protocol</span></span>
<span data-ttu-id="bf45c-180">Recupera il protocollo di endpoint hello per istanza hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="bf45c-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-181">Type</span></span> | <span data-ttu-id="bf45c-182">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-183">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-183">XPath</span></span> |<span data-ttu-id="bf45c-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="bf45c-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="bf45c-185">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-185">Code</span></span> |<span data-ttu-id="bf45c-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="bf45c-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="bf45c-187">IP dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="bf45c-187">Endpoint IP</span></span>
<span data-ttu-id="bf45c-188">Ottiene hello specificato l'indirizzo IP dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="bf45c-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="bf45c-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-189">Type</span></span> | <span data-ttu-id="bf45c-190">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-191">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-191">XPath</span></span> |<span data-ttu-id="bf45c-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="bf45c-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="bf45c-193">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-193">Code</span></span> |<span data-ttu-id="bf45c-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="bf45c-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="bf45c-195">Porta dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="bf45c-195">Endpoint port</span></span>
<span data-ttu-id="bf45c-196">Recupera una porta dell'endpoint per l'istanza di hello hello.</span><span class="sxs-lookup"><span data-stu-id="bf45c-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="bf45c-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="bf45c-197">Type</span></span> | <span data-ttu-id="bf45c-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="bf45c-199">XPath</span><span class="sxs-lookup"><span data-stu-id="bf45c-199">XPath</span></span> |<span data-ttu-id="bf45c-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="bf45c-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="bf45c-201">Codice</span><span class="sxs-lookup"><span data-stu-id="bf45c-201">Code</span></span> |<span data-ttu-id="bf45c-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="bf45c-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="bf45c-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="bf45c-203">Example</span></span>
<span data-ttu-id="bf45c-204">Di seguito è riportato un esempio di un ruolo di lavoro che crea un'attività di avvio con una variabile di ambiente denominata `TestIsEmulated` impostare toohello [ @emulated valore xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="bf45c-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="bf45c-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf45c-205">Next steps</span></span>
<span data-ttu-id="bf45c-206">Altre informazioni su hello [ServiceConfiguration. cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span><span class="sxs-lookup"><span data-stu-id="bf45c-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="bf45c-207">Creare un pacchetto [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="bf45c-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="bf45c-208">Abilitare [Desktop remoto](cloud-services-role-enable-remote-desktop.md) per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="bf45c-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

