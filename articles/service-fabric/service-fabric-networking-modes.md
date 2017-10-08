---
title: "le modalità per servizi di Azure Service Fabric contenitore aaaConfigure | Documenti Microsoft"
description: "Informazioni su come toosetup hello diverse modalità di rete di Azure Service Fabric supporta."
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
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="1e1c0-103">Modalità di rete del contenitore di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1e1c0-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="1e1c0-104">Hello modalità di rete predefinite disponibili in Service Fabric hello cluster per i servizi contenitore è hello `nat` modalità di rete.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="1e1c0-105">Con hello `nat` modalità, con toohello di ascolto di più contenitori del servizio di rete stessa porta genera errori di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="1e1c0-106">Per l'esecuzione di diversi servizi in ascolto sulla stessa porta, Service Fabric supporta hello hello `open` modalità di rete (versione 5.7 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="1e1c0-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="1e1c0-107">Con hello `open` modalità di rete, ogni servizio contenitore ottiene un indirizzo IP assegnato dinamicamente internamente che consente più servizi toolisten toohello stessa porta.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="1e1c0-108">Pertanto, con un singolo tipo di servizio con un endpoint statico definito nel manifesto del servizio hello, nuovi servizi possono essere creati ed eliminati senza errori di distribuzione utilizzando hello `open` modalità di rete.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="1e1c0-109">Analogamente, è possibile utilizzare hello stesso `docker-compose.yml` file con mapping di porta statica per la creazione di più servizi.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="1e1c0-110">Utilizzando hello assegnato dinamicamente servizi toodiscover IP non è consigliabile poiché le modifiche all'indirizzo IP hello quando servizio hello riavvia o si sposta il nodo tooanother.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="1e1c0-111">Utilizzare solo hello **servizio Service Fabric denominazione** o hello **servizio DNS** per l'individuazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="1e1c0-112">È consentito solo un totale di 4096 indirizzi IP per ogni rete virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="1e1c0-113">Di conseguenza, hello somma hello numero di nodi e numero di hello contenitore di istanze del servizio (con `open` rete) non può superare i 4096 all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="1e1c0-114">Per tali scenari ad alta densità, hello `nat` è consigliata la modalità di rete.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="1e1c0-115">Configurazione della modalità di rete aperta</span><span class="sxs-lookup"><span data-stu-id="1e1c0-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="1e1c0-116">Impostare il modello di gestione risorse di Azure hello abilitando il servizio DNS e hello IP Provider in `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="1e1c0-117">Impostare la sezione hello rete profilo tooallow con più indirizzi toobe configurato in ogni nodo del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="1e1c0-118">Hello questo esempio viene impostata cinque indirizzi IP per ogni nodo (in questo modo è possibile avere cinque istanze di servizio in ascolto sulla porta toohello in ogni nodo) per un cluster di Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="1e1c0-119">Per i cluster Linux, un'ulteriore configurazione IP pubblica viene aggiunto tooallow di connettività in uscita.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="1e1c0-120">Hello frammento di codice seguente imposta cinque indirizzi IP per ogni nodo per un cluster Linux:</span><span class="sxs-lookup"><span data-stu-id="1e1c0-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="1e1c0-121">Per i cluster consente di configurare solo un gruppo Windows regola aprire la porta UDP 53/per la rete virtuale hello con hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="1e1c0-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="1e1c0-122">Priorità</span><span class="sxs-lookup"><span data-stu-id="1e1c0-122">Priority</span></span> |    <span data-ttu-id="1e1c0-123">Nome</span><span class="sxs-lookup"><span data-stu-id="1e1c0-123">Name</span></span>    |    <span data-ttu-id="1e1c0-124">Sorgente</span><span class="sxs-lookup"><span data-stu-id="1e1c0-124">Source</span></span>      |  <span data-ttu-id="1e1c0-125">Destination</span><span class="sxs-lookup"><span data-stu-id="1e1c0-125">Destination</span></span>   |   <span data-ttu-id="1e1c0-126">Service</span><span class="sxs-lookup"><span data-stu-id="1e1c0-126">Service</span></span>    | <span data-ttu-id="1e1c0-127">Azione</span><span class="sxs-lookup"><span data-stu-id="1e1c0-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="1e1c0-128">2000</span><span class="sxs-lookup"><span data-stu-id="1e1c0-128">2000</span></span> | <span data-ttu-id="1e1c0-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="1e1c0-129">Custom_Dns</span></span> | <span data-ttu-id="1e1c0-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1e1c0-130">VirtualNetwork</span></span> | <span data-ttu-id="1e1c0-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1e1c0-131">VirtualNetwork</span></span> | <span data-ttu-id="1e1c0-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="1e1c0-132">DNS (UDP/53)</span></span> | <span data-ttu-id="1e1c0-133">CONSENTI</span><span class="sxs-lookup"><span data-stu-id="1e1c0-133">Allow</span></span>  |


4. <span data-ttu-id="1e1c0-134">Specificare le modalità di rete hello nel manifesto dell'applicazione hello per ogni servizio `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="1e1c0-135">modalità Hello `open` comporta servizio hello ottenere un indirizzo IP dedicato.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="1e1c0-136">Se non è specificata una modalità, il valore predefinito toohello base `nat` modalità.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="1e1c0-137">Pertanto, nell'esempio di manifesto seguente hello `NodeContainerServicePackage1` e `NodeContainerServicePackage2` possibile ogni toohello ascolto stessa porta (entrambi i servizi sono in attesa sulla `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="1e1c0-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="1e1c0-138">È possibile combinare e abbinare diverse modalità di rete tra servizi all'interno di un'applicazione per un cluster di Windows.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="1e1c0-139">Pertanto, è possibile avere alcuni servizi sulla modalità `open` e alcuni sulla modalità di rete `nat`.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="1e1c0-140">Quando un servizio è configurato con `nat`, porta hello è in ascolto toomust essere univoco.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="1e1c0-141">La combinazione di modalità di rete per diversi servizi non è supportata nei cluster di Linux.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1e1c0-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e1c0-142">Next steps</span></span>
<span data-ttu-id="1e1c0-143">In questo articolo sono state fornite informazioni sulle modalità di rete offerte da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1e1c0-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="1e1c0-144">Modello di applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1e1c0-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="1e1c0-145">Risorse del manifesto del servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1e1c0-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="1e1c0-146">Distribuire un tooService di contenitore di Windows Fabric in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1e1c0-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="1e1c0-147">Distribuire un tooService contenitore Docker dell'infrastruttura in Linux</span><span class="sxs-lookup"><span data-stu-id="1e1c0-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
