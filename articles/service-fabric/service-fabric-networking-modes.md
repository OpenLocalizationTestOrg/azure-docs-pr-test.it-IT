---
title: "Configurare le modalità di rete per i servizi del contenitore di Azure Service Fabric | Microsoft Docs"
description: "Informazioni su come configurare le diverse modalità di rete supportate da Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f792f9604a5d6e62551ed92c1049d6e2b4216417
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="80cdd-103">Modalità di rete del contenitore di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="80cdd-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="80cdd-104">La modalità del servizio di rete predefinita offerta nel cluster di Service Fabric per i servizi del contenitore è la modalità di rete `nat`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-104">The default networking mode offered in the Service Fabric cluster for container services is the `nat` networking mode.</span></span> <span data-ttu-id="80cdd-105">Con la modalità di rete `nat`, la presenza di più di un servizio di contenitori in ascolto per gli stessi risultati di porta comporta errori di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="80cdd-105">With the `nat` networking mode, having more than one containers service listening to the same port results in deployment errors.</span></span> <span data-ttu-id="80cdd-106">Per eseguire diversi servizi in ascolto sulla stessa porta, Service Fabric supporta la modalità di rete `open` (versione 5.7 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="80cdd-106">For running several services that listen on the same port, Service Fabric supports the `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="80cdd-107">Con la modalità di rete `open`, ogni servizio del contenitore ottiene un indirizzo IP assegnato dinamicamente internamente, consentendo più servizi in ascolto sulla stessa porta.</span><span class="sxs-lookup"><span data-stu-id="80cdd-107">With the `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services to listen to the same port.</span></span>   

<span data-ttu-id="80cdd-108">Pertanto, con un singolo tipo di servizio con un endpoint statico definito nel manifesto del servizio, è possibile creare ed eliminare nuovi servizi senza errori di distribuzione tramite la modalità di rete `open`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-108">Thus, with a single service type with a static endpoint defined in the service manifest, new services may be created and deleted without deployment errors using the `open` networking mode.</span></span> <span data-ttu-id="80cdd-109">Analogamente, è possibile usare lo stesso file `docker-compose.yml` con il mapping delle porte statiche per la creazione di più servizi.</span><span class="sxs-lookup"><span data-stu-id="80cdd-109">Similarly, one can use the same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="80cdd-110">Usare l'IP assegnato dinamicamente per individuare i servizi non è consigliabile poiché l'indirizzo IP cambia quando il servizio viene riavviato o viene spostato in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="80cdd-110">Using the dynamically assigned IP to discover services is not advisable since the IP address changes when the service restarts or moves to another node.</span></span> <span data-ttu-id="80cdd-111">Usare solo **Service Fabric Naming Service** o il **servizio DNS** per l'individuazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="80cdd-111">Only use the **Service Fabric Naming Service**  or the **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="80cdd-112">È consentito solo un totale di 4096 indirizzi IP per ogni rete virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="80cdd-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="80cdd-113">Di conseguenza, la somma del numero di nodi e il numero di istanze del servizio contenitore (con rete `open`) non può superare i 4096 all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="80cdd-113">Thus, the sum of the number of nodes and the number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="80cdd-114">Per questi scenari ad alta densità, si consiglia la modalità di rete `nat`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-114">For such high-density scenarios, the `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="80cdd-115">Configurazione della modalità di rete aperta</span><span class="sxs-lookup"><span data-stu-id="80cdd-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="80cdd-116">Configurare il modello di Azure Resource Manager, abilitando il servizio DNS e il provider di IP in `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-116">Set up the Azure Resource Manager template by enabling DNS Service and the IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="80cdd-117">Configurare la sezione del profilo di rete per consentire la configurazione di più indirizzi IP in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="80cdd-117">Set up the network profile section to allow multiple IP addresses to be configured on each node of the cluster.</span></span> <span data-ttu-id="80cdd-118">Nell'esempio seguente si configurano cinque indirizzi IP per ogni nodo (pertanto è possibile avere cinque istanze del servizio in ascolto della porta su ogni nodo) per un cluster di Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="80cdd-118">The following example sets up five IP addresses per node (thus you can have five service instances listening to the port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="80cdd-119">Per i cluster di Linux, viene aggiunta un'altra configurazione dell'IP pubblico per consentire la connettività in uscita.</span><span class="sxs-lookup"><span data-stu-id="80cdd-119">For Linux clusters, an additional public IP configuration is added to allow outbound connectivity.</span></span> <span data-ttu-id="80cdd-120">Il frammento di codice seguente configura cinque indirizzi IP per ogni nodo per un cluster di Linux:</span><span class="sxs-lookup"><span data-stu-id="80cdd-120">The following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="80cdd-121">Solo per i cluster di Windows, configurare una regola del gruppo di sicurezza di rete aprendo la porta UDP/53 per la rete virtuale con i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="80cdd-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for the vNET with the following values:</span></span>

   | <span data-ttu-id="80cdd-122">Priorità</span><span class="sxs-lookup"><span data-stu-id="80cdd-122">Priority</span></span> |    <span data-ttu-id="80cdd-123">Nome</span><span class="sxs-lookup"><span data-stu-id="80cdd-123">Name</span></span>    |    <span data-ttu-id="80cdd-124">Sorgente</span><span class="sxs-lookup"><span data-stu-id="80cdd-124">Source</span></span>      |  <span data-ttu-id="80cdd-125">Destination</span><span class="sxs-lookup"><span data-stu-id="80cdd-125">Destination</span></span>   |   <span data-ttu-id="80cdd-126">Service</span><span class="sxs-lookup"><span data-stu-id="80cdd-126">Service</span></span>    | <span data-ttu-id="80cdd-127">Azione</span><span class="sxs-lookup"><span data-stu-id="80cdd-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="80cdd-128">2000</span><span class="sxs-lookup"><span data-stu-id="80cdd-128">2000</span></span> | <span data-ttu-id="80cdd-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="80cdd-129">Custom_Dns</span></span> | <span data-ttu-id="80cdd-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="80cdd-130">VirtualNetwork</span></span> | <span data-ttu-id="80cdd-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="80cdd-131">VirtualNetwork</span></span> | <span data-ttu-id="80cdd-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="80cdd-132">DNS (UDP/53)</span></span> | <span data-ttu-id="80cdd-133">CONSENTI</span><span class="sxs-lookup"><span data-stu-id="80cdd-133">Allow</span></span>  |


4. <span data-ttu-id="80cdd-134">Specificare la modalità di rete nel manifesto dell'app per ogni servizio `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-134">Specify the networking mode in the app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="80cdd-135">La modalità `open` consente al servizio di ottenere un indirizzo IP dedicato.</span><span class="sxs-lookup"><span data-stu-id="80cdd-135">The mode `open` results in the service getting a dedicated IP address.</span></span> <span data-ttu-id="80cdd-136">Se non si specifica una modalità, viene impostata la modalità predefinita di base `nat`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-136">If a mode isn't specified, it defaults to the basic `nat` mode.</span></span> <span data-ttu-id="80cdd-137">Pertanto, nell'esempio di manifesto seguente, `NodeContainerServicePackage1` e `NodeContainerServicePackage2` possono essere in ascolto sulla stessa porta (entrambi i servizi sono in ascolto su `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="80cdd-137">Thus, in the following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen to the same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="80cdd-138">È possibile combinare e abbinare diverse modalità di rete tra servizi all'interno di un'applicazione per un cluster di Windows.</span><span class="sxs-lookup"><span data-stu-id="80cdd-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="80cdd-139">Pertanto, è possibile avere alcuni servizi sulla modalità `open` e alcuni sulla modalità di rete `nat`.</span><span class="sxs-lookup"><span data-stu-id="80cdd-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="80cdd-140">Quando un servizio è configurato con `nat`, la porta su cui è in ascolto deve essere univoca.</span><span class="sxs-lookup"><span data-stu-id="80cdd-140">When a service is configured with `nat`, the port it is listening to must be unique.</span></span> <span data-ttu-id="80cdd-141">La combinazione di modalità di rete per diversi servizi non è supportata nei cluster di Linux.</span><span class="sxs-lookup"><span data-stu-id="80cdd-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="80cdd-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80cdd-142">Next steps</span></span>
<span data-ttu-id="80cdd-143">In questo articolo sono state fornite informazioni sulle modalità di rete offerte da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="80cdd-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="80cdd-144">Modello di applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="80cdd-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="80cdd-145">Risorse del manifesto del servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="80cdd-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="80cdd-146">Distribuire un contenitore Windows in Service Fabric su Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="80cdd-146">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="80cdd-147">Distribuire un contenitore Docker in Service Fabric su Linux</span><span class="sxs-lookup"><span data-stu-id="80cdd-147">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
