---
title: modelli aaaNetworking per Azure Service Fabric | Documenti Microsoft
description: "Descrive i modelli di rete comuni per l'infrastruttura di servizio e come toocreate un cluster con funzionalità di rete di Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Modelli di rete di Service Fabric
È possibile integrare il cluster di Azure Service Fabric con altre funzionalità di rete di Azure. In questo articolo viene illustrata la modalità toocreate cluster hello tale uso seguenti caratteristiche:

- [Rete virtuale o subnet esistente](#existingvnet)
- [Indirizzo IP pubblico statico](#staticpublicip)
- [Bilanciamento del carico esclusivamente interno](#internallb)
- [Bilanciamento del carico interno ed esterno](#internalexternallb)

Service Fabric viene eseguito in un set di scalabilità di macchine virtuali standard. In un cluster di Service Fabric si possono usare tutte le funzionalità che è possibile usare in un set di scalabilità di macchine virtuali. Nelle sezioni di rete Hello dei modelli di Azure Resource Manager hello per set di scalabilità di macchine virtuali e Service Fabric sono identiche. Dopo aver distribuito tooan rete virtuale esistente, è facile tooincorporate altre funzionalità, come Azure ExpressRoute, Gateway VPN di Azure, un gruppo di sicurezza di rete e peering di rete virtuale di rete.

Service Fabric si distingue dalle altre funzionalità di rete per un solo aspetto. Hello [portale di Azure](https://portal.azure.com) internamente utilizza hello Service Fabric risorsa toocall tooa cluster tooget informazioni sul provider sui nodi e le applicazioni. provider di risorse di Service Fabric Hello richiede l'accesso in ingresso accessibile pubblicamente toohello HTTP gateway (porta 19080, per impostazione predefinita) nell'endpoint di gestione di hello. [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) utilizza hello toomanage endpoint di gestione del cluster. provider di risorse di Service Fabric Hello utilizza anche queste informazioni di tooquery porta sul cluster, toodisplay in hello portale di Azure. 

Se la porta 19080 non è accessibile dal provider di risorse di Service Fabric hello, ad esempio un messaggio *non trovati nodi* viene visualizzato nel portale di hello e l'elenco di nodo e un'applicazione viene visualizzata vuota. Se si desidera toosee il cluster in hello portale di Azure, servizio di bilanciamento del carico deve esporre un indirizzo IP pubblico e il gruppo di sicurezza di rete deve consentire il traffico in ingresso porta 19080. Se il programma di installazione non soddisfa questi requisiti, hello portale di Azure non vengono visualizzati lo stato di hello del cluster.

## <a name="templates"></a>Modelli

Tutti i modelli di Service Fabric si trovano in [un unico file scaricabile](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Dovrebbe essere in grado di toodeploy modelli hello come-utilizzando i seguenti comandi PowerShell hello. Se si sta distribuendo hello modello di rete virtuale di Azure esistente o hello statico pubblico IP template, leggere prima hello [Initial setup](#initialsetup) sezione di questo articolo.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Configurazione iniziale

### <a name="existing-virtual-network"></a>Rete virtuale esistente

Nell'esempio seguente di hello, iniziare con una rete virtuale esistente denominata ExistingRG-vnet, in hello **ExistingRG** gruppo di risorse. subnet Hello è denominato default. Queste risorse predefiniti vengono create quando si utilizza hello toocreate portale Azure una standard macchina virtuale (VM). È possibile creare la rete virtuale hello e subnet senza hello VM di creazione, ma l'obiettivo principale di aggiunta di una rete virtuale esistente cluster tooan hello è tooother di connettività di rete tooprovide macchine virtuali. Creazione hello VM fornisce un buon esempio di come una rete virtuale esistente in genere viene utilizzata. Se il cluster di Service Fabric utilizza solo un bilanciamento del carico interno, senza un indirizzo IP pubblico, è possibile utilizzare hello macchina virtuale e il relativo indirizzo IP pubblico come sicuro *passare casella*.

### <a name="static-public-ip-address"></a>Indirizzo IP pubblico statico

In genere, un indirizzo IP pubblico statico è una risorsa dedicata che è gestita separatamente dal hello per le VM di cui è assegnato. Si è effettuato il provisioning in un gruppo di risorse di rete dedicata (come tooin anziché hello Service Fabric gruppo di risorse cluster stesso). Creare un indirizzo IP pubblico statico denominato staticIP1 in hello stesso gruppo di risorse ExistingRG, hello portale di Azure o tramite PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Modello di Service Fabric

Negli esempi di hello in questo articolo, utilizziamo template.json Service Fabric hello. È possibile utilizzare hello standard portale toodownload hello il modello procedura guidata dal portale hello prima di creare un cluster. È inoltre possibile utilizzare uno dei modelli di hello in hello [raccolta di modelli](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), ad esempio hello [cluster di Service Fabric cinque](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Rete virtuale o subnet esistente

1. Modificare nome toohello del parametro hello subnet di una subnet esistente hello e quindi aggiungere due nuovi parametri tooreference hello rete virtuale esistente:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Hello modifica `vnetID` rete virtuale di variabile toopoint toohello esistente:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Rimuovere `Microsoft.Network/virtualNetworks` dalle risorse in modo che Azure non crei una nuova rete virtuale:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Commento di rete virtuale di hello dall'hello `dependsOn` attributo di `Microsoft.Compute/virtualMachineScaleSets`, pertanto non dipendono dalla creazione di una nuova rete virtuale:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Distribuire il modello di hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Dopo la distribuzione, è necessario includere la rete virtuale le macchine virtuali del set di scalabilità di nuovo hello. tipo di nodo set di scalabilità di Hello macchina virtuale deve visualizzare subnet e la rete virtuale esistente di hello. È anche possibile usare Remote Desktop Protocol (RDP) tooaccess hello macchina virtuale che era già in una rete virtuale hello e impostare la scala di nuovo hello tooping su macchine virtuali:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Per un altro esempio, vedere [uno che non sia tooService specifico dell'infrastruttura](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Indirizzo IP pubblico statico

1. Aggiungere parametri per nome hello di hello esistente al gruppo di risorse IP statico, nome e il nome di dominio completo (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Rimuovere hello `dnsName` parametro. l'indirizzo IP statico hello già dispone di uno.

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Aggiungere un variabile tooreference hello indirizzo IP statico esistente:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Commento di indirizzo IP hello hello `dependsOn` attributo di `Microsoft.Network/loadBalancers`, pertanto non dipendono dalla creazione di un nuovo indirizzo IP:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. In hello `Microsoft.Network/loadBalancers` risorsa, hello modifica `publicIPAddress` elemento `frontendIPConfigurations` tooreference hello indirizzo IP statico esistente anziché uno appena creato:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. In hello `Microsoft.ServiceFabric/clusters` risorse, modifica `managementEndpoint` toohello FQDN DNS dell'indirizzo IP statico hello. Se si utilizza un cluster protetto, assicurarsi di modificare *http://* troppo*https://*. (Si noti che questo passaggio si applica solo i cluster di infrastruttura tooService. Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Distribuire il modello di hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Dopo la distribuzione, è possibile notare che il servizio di bilanciamento del carico associato toohello pubblica indirizzo IP statico da hello altro gruppo di risorse. endpoint di connessione client di Service Fabric Hello e [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello punto endpoint FQDN DNS dell'indirizzo IP statico hello.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Bilanciamento del carico esclusivamente interno

Questo scenario sostituisce bilanciamento del carico esterno hello nel modello di Service Fabric hello predefinito con un bilanciamento del carico interno. Per influisce hello portale di Azure e per provider di risorse di Service Fabric hello, vedere la precedente sezione hello.

1. Rimuovere hello `dnsName` parametro. Non è necessario.

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Facoltativamente, se si usa un metodo di allocazione statica è possibile aggiungere un parametro per l'indirizzo IP statico. Se si utilizza un metodo di allocazione dinamica, non è necessario toodo questo passaggio.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Rimuovere l'indirizzo IP hello `dependsOn` attributo di `Microsoft.Network/loadBalancers`, pertanto non dipendono dalla creazione di un nuovo indirizzo IP. Aggiungere la rete virtuale hello `dependsOn` attributo perché il servizio di bilanciamento del carico hello ora dipende dalla subnet hello dalla rete virtuale hello:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Modifica del bilanciamento carico di hello `frontendIPConfigurations` impostazione dall'utilizzo di un `publicIPAddress`, toousing una subnet e `privateIPAddress`. `privateIPAddress` usa un indirizzo IP interno statico predefinito. toouse un indirizzo IP dinamico, rimuovere hello `privateIPAddress` elemento e quindi modificare `privateIPAllocationMethod` troppo**dinamica**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. In hello `Microsoft.ServiceFabric/clusters` risorse, modifica `managementEndpoint` indirizzo di bilanciamento del carico interno toohello toopoint. Se si utilizza un cluster protetto, assicurarsi di modificare *http://* troppo*https://*. (Si noti che questo passaggio si applica solo i cluster di infrastruttura tooService. Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Distribuire il modello di hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Dopo la distribuzione, il servizio di bilanciamento del carico Usa indirizzo IP hello 10.0.0.250 statico privato. Se si dispone di un altro computer nella stessa rete virtuale, è possibile passare toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint. Si noti che si connette tooone dei nodi di hello bilanciamento del carico hello.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Bilanciamento del carico interno ed esterno

In questo scenario, iniziare con bilanciamento del carico esterno a nodo singolo tipo esistente hello e aggiungere un servizio di bilanciamento del carico interno per hello stesso tipo di nodo. Un pool di indirizzi back-end tooa porta back-end collegata può essere assegnato solo tooa singolo bilanciamento del carico. Scegliere a quale servizio di bilanciamento del carico assegnare le porte dell'applicazione e a quale assegnare gli endpoint di gestione (porte 19000 e 19080). Se si inserisce l'endpoint di gestione di hello su servizio di bilanciamento del carico interno hello, tenere hello presente risorsa Service Fabric restrizioni provider in precedenza in hello articolo. Nell'esempio hello che utilizziamo, gli endpoint di gestione di hello rimangono sul servizio di bilanciamento del carico esterno hello. Inoltre aggiungere una porta di porta 80 dell'applicazione e posizionalo nel servizio di bilanciamento del carico interno hello.

In un cluster di tipo di nodo due, un tipo di nodo è nel servizio di bilanciamento del carico esterno hello. Hello altro tipo di nodo è nel servizio di bilanciamento del carico interno hello. toouse un cluster di tipo di nodo due, in hello creare portale del tipo di nodo due modello (incluso in due servizi di bilanciamento del carico), passare hello secondo carico bilanciamento tooan bilanciamento del carico interno. Per ulteriori informazioni, vedere hello [bilanciamento del carico solo per uso interno](#internallb) sezione.

1. Aggiungi parametro di indirizzo IP del servizio di bilanciamento carico di interno statico hello. (Per le note correlate toousing un indirizzo IP dinamico, vedere le sezioni precedenti di questo articolo).

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Aggiungere un parametro della porta 80 dell'applicazione.

3. tooadd versioni interne di hello esistente rete variabili, copiare e incollare i controlli e aggiungere "-Int" nome toohello:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Se si avvia con modello generato portale hello che utilizza la porta 80 dell'applicazione, modello di portale predefinito hello aggiunge AppPort1 (porta 80) nel servizio di bilanciamento del carico esterno hello. In questo caso, rimuovere AppPort1 dal servizio di bilanciamento del carico esterno hello `loadBalancingRules` probe e, pertanto è possibile aggiungere il servizio di bilanciamento del carico interno toohello:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Aggiungere una seconda risorsa `Microsoft.Network/loadBalancers`. Ottenere un risultato simile bilanciamento del carico interno toohello creato in hello [bilanciamento del carico solo per uso interno](#internallb) sezione, ma Usa hello "-Int" caricare le variabili di sistema di bilanciamento e implementa solo hello applicazione la porta 80. Verranno rimossi anche `inboundNatPools`, gli endpoint RDP tookeep nel servizio di bilanciamento del carico pubblico hello. Se si desidera RDP nel servizio di bilanciamento del carico interno hello, spostare `inboundNatPools` da hello toothis bilanciamento di carico esterno interno il bilanciamento del carico:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. In `networkProfile` per hello `Microsoft.Compute/virtualMachineScaleSets` risorse, aggiungere il pool di indirizzi back-end interno hello:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Distribuire il modello di hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Dopo la distribuzione, è possibile visualizzare due servizi di bilanciamento del carico nel gruppo di risorse hello. Se si seleziona servizi di bilanciamento del carico hello, è possibile visualizzare l'indirizzo IP pubblico hello e indirizzo IP pubblico di gestione endpoint (porte 19000 e 19080) assegnato toohello. È inoltre possibile visualizzare hello statico interno IP applicazione e l'indirizzo endpoint (porta 80) assegnato toohello interno il bilanciamento del carico. Entrambi di caricamento Usa bilanciamento del carico scalabilità della macchina virtuale stessa hello impostare pool back-end.

## <a name="next-steps"></a>Passaggi successivi
[Creare un cluster](service-fabric-cluster-creation-via-arm.md)
