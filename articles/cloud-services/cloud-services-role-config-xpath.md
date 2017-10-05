---
title: Foglio informativo su XPath per la configurazione del ruolo di Servizi cloud | Documentazione Microsoft
description: "Varie impostazioni di XPath che è possibile usare nella configurazione del ruolo del servizio cloud per esporre le impostazioni come una variabile di ambiente."
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
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="61586-103">Esporre le impostazioni di configurazione del ruolo come una variabile di ambiente con XPath</span><span class="sxs-lookup"><span data-stu-id="61586-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="61586-104">Nel file di definizione del servzio del ruolo di lavoro o del ruolo Web del servizio cloud è possibile esporre i valori di configurazione di runtime come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="61586-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="61586-105">Sono supportati i valori XPath seguenti, che corrispondono ai valori di API.</span><span class="sxs-lookup"><span data-stu-id="61586-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="61586-106">Questi valori XPath sono disponibili anche tramite la libreria [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="61586-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="61586-107">App in esecuzione nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="61586-107">App running in emulator</span></span>
<span data-ttu-id="61586-108">Indica che l'app è in esecuzione nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="61586-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="61586-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-109">Type</span></span> | <span data-ttu-id="61586-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-111">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-111">XPath</span></span> |<span data-ttu-id="61586-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="61586-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="61586-113">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-113">Code</span></span> |<span data-ttu-id="61586-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="61586-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="61586-115">ID distribuzione</span><span class="sxs-lookup"><span data-stu-id="61586-115">Deployment ID</span></span>
<span data-ttu-id="61586-116">Recupera l'ID distribuzione per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="61586-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-117">Type</span></span> | <span data-ttu-id="61586-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-119">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-119">XPath</span></span> |<span data-ttu-id="61586-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="61586-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="61586-121">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-121">Code</span></span> |<span data-ttu-id="61586-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="61586-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="61586-123">ID ruolo</span><span class="sxs-lookup"><span data-stu-id="61586-123">Role ID</span></span>
<span data-ttu-id="61586-124">Recupera l'ID del ruolo corrente per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="61586-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-125">Type</span></span> | <span data-ttu-id="61586-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-127">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-127">XPath</span></span> |<span data-ttu-id="61586-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="61586-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="61586-129">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-129">Code</span></span> |<span data-ttu-id="61586-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="61586-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="61586-131">Aggiornamento dominio</span><span class="sxs-lookup"><span data-stu-id="61586-131">Update domain</span></span>
<span data-ttu-id="61586-132">Recupera il dominio di aggiornamento dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="61586-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-133">Type</span></span> | <span data-ttu-id="61586-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-135">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-135">XPath</span></span> |<span data-ttu-id="61586-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="61586-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="61586-137">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-137">Code</span></span> |<span data-ttu-id="61586-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="61586-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="61586-139">Dominio di errore</span><span class="sxs-lookup"><span data-stu-id="61586-139">Fault domain</span></span>
<span data-ttu-id="61586-140">Recupera il dominio di errore dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="61586-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-141">Type</span></span> | <span data-ttu-id="61586-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-143">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-143">XPath</span></span> |<span data-ttu-id="61586-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="61586-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="61586-145">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-145">Code</span></span> |<span data-ttu-id="61586-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="61586-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="61586-147">Nome del ruolo</span><span class="sxs-lookup"><span data-stu-id="61586-147">Role name</span></span>
<span data-ttu-id="61586-148">Recupera il nome del ruolo dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="61586-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-149">Type</span></span> | <span data-ttu-id="61586-150">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-151">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-151">XPath</span></span> |<span data-ttu-id="61586-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="61586-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="61586-153">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-153">Code</span></span> |<span data-ttu-id="61586-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="61586-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="61586-155">Impostazione di configurazione</span><span class="sxs-lookup"><span data-stu-id="61586-155">Config setting</span></span>
<span data-ttu-id="61586-156">Recupera il valore dell'impostazione di configurazione specificata.</span><span class="sxs-lookup"><span data-stu-id="61586-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="61586-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-157">Type</span></span> | <span data-ttu-id="61586-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-159">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-159">XPath</span></span> |<span data-ttu-id="61586-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="61586-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="61586-161">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-161">Code</span></span> |<span data-ttu-id="61586-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="61586-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="61586-163">Percorso di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="61586-163">Local storage path</span></span>
<span data-ttu-id="61586-164">Recupera il percorso di archiviazione locale per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="61586-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-165">Type</span></span> | <span data-ttu-id="61586-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-167">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-167">XPath</span></span> |<span data-ttu-id="61586-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="61586-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="61586-169">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-169">Code</span></span> |<span data-ttu-id="61586-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="61586-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="61586-171">Dimensioni di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="61586-171">Local storage size</span></span>
<span data-ttu-id="61586-172">Recupera le dimensioni di archiviazione locale per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="61586-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-173">Type</span></span> | <span data-ttu-id="61586-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-175">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-175">XPath</span></span> |<span data-ttu-id="61586-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="61586-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="61586-177">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-177">Code</span></span> |<span data-ttu-id="61586-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="61586-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="61586-179">Protocollo di endpoint</span><span class="sxs-lookup"><span data-stu-id="61586-179">Endpoint protocol</span></span>
<span data-ttu-id="61586-180">Recupera il protocollo di endpoint per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="61586-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-181">Type</span></span> | <span data-ttu-id="61586-182">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-183">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-183">XPath</span></span> |<span data-ttu-id="61586-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="61586-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="61586-185">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-185">Code</span></span> |<span data-ttu-id="61586-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="61586-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="61586-187">IP dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="61586-187">Endpoint IP</span></span>
<span data-ttu-id="61586-188">Ottiene l'indirizzo IP dell'endpoint specificato.</span><span class="sxs-lookup"><span data-stu-id="61586-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="61586-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-189">Type</span></span> | <span data-ttu-id="61586-190">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-191">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-191">XPath</span></span> |<span data-ttu-id="61586-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="61586-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="61586-193">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-193">Code</span></span> |<span data-ttu-id="61586-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="61586-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="61586-195">Porta dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="61586-195">Endpoint port</span></span>
<span data-ttu-id="61586-196">Recupera la porta dell'endpoint per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="61586-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="61586-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="61586-197">Type</span></span> | <span data-ttu-id="61586-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="61586-199">XPath</span><span class="sxs-lookup"><span data-stu-id="61586-199">XPath</span></span> |<span data-ttu-id="61586-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="61586-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="61586-201">Codice</span><span class="sxs-lookup"><span data-stu-id="61586-201">Code</span></span> |<span data-ttu-id="61586-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="61586-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="61586-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="61586-203">Example</span></span>
<span data-ttu-id="61586-204">Ecco un esempio di un ruolo di lavoro che crea un'attività di avvio con una variabile di ambiente denominata `TestIsEmulated` impostata sul valore [@emulated xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="61586-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="61586-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61586-205">Next steps</span></span>
<span data-ttu-id="61586-206">Altre informazioni sul file [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) .</span><span class="sxs-lookup"><span data-stu-id="61586-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="61586-207">Creare un pacchetto [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="61586-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="61586-208">Abilitare [Desktop remoto](cloud-services-role-enable-remote-desktop.md) per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="61586-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

