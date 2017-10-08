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
# <a name="service-fabric-container-networking-modes"></a>Modalità di rete del contenitore di Service Fabric

Hello modalità di rete predefinite disponibili in Service Fabric hello cluster per i servizi contenitore è hello `nat` modalità di rete. Con hello `nat` modalità, con toohello di ascolto di più contenitori del servizio di rete stessa porta genera errori di distribuzione. Per l'esecuzione di diversi servizi in ascolto sulla stessa porta, Service Fabric supporta hello hello `open` modalità di rete (versione 5.7 o versioni successive). Con hello `open` modalità di rete, ogni servizio contenitore ottiene un indirizzo IP assegnato dinamicamente internamente che consente più servizi toolisten toohello stessa porta.   

Pertanto, con un singolo tipo di servizio con un endpoint statico definito nel manifesto del servizio hello, nuovi servizi possono essere creati ed eliminati senza errori di distribuzione utilizzando hello `open` modalità di rete. Analogamente, è possibile utilizzare hello stesso `docker-compose.yml` file con mapping di porta statica per la creazione di più servizi.

Utilizzando hello assegnato dinamicamente servizi toodiscover IP non è consigliabile poiché le modifiche all'indirizzo IP hello quando servizio hello riavvia o si sposta il nodo tooanother. Utilizzare solo hello **servizio Service Fabric denominazione** o hello **servizio DNS** per l'individuazione del servizio. 


> [!WARNING]
> È consentito solo un totale di 4096 indirizzi IP per ogni rete virtuale in Azure. Di conseguenza, hello somma hello numero di nodi e numero di hello contenitore di istanze del servizio (con `open` rete) non può superare i 4096 all'interno di una rete virtuale. Per tali scenari ad alta densità, hello `nat` è consigliata la modalità di rete.
>

## <a name="setting-up-open-networking-mode"></a>Configurazione della modalità di rete aperta

1. Impostare il modello di gestione risorse di Azure hello abilitando il servizio DNS e hello IP Provider in `fabricSettings`. 

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

2. Impostare la sezione hello rete profilo tooallow con più indirizzi toobe configurato in ogni nodo del cluster di hello. Hello questo esempio viene impostata cinque indirizzi IP per ogni nodo (in questo modo è possibile avere cinque istanze di servizio in ascolto sulla porta toohello in ogni nodo) per un cluster di Windows Service Fabric.

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

    Per i cluster Linux, un'ulteriore configurazione IP pubblica viene aggiunto tooallow di connettività in uscita. Hello frammento di codice seguente imposta cinque indirizzi IP per ogni nodo per un cluster Linux:

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

3. Per i cluster consente di configurare solo un gruppo Windows regola aprire la porta UDP 53/per la rete virtuale hello con hello seguenti valori:

   | Priorità |    Nome    |    Sorgente      |  Destination   |   Service    | Azione |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | CONSENTI  |


4. Specificare le modalità di rete hello nel manifesto dell'applicazione hello per ogni servizio `<NetworkConfig NetworkType="open">`.  modalità Hello `open` comporta servizio hello ottenere un indirizzo IP dedicato. Se non è specificata una modalità, il valore predefinito toohello base `nat` modalità. Pertanto, nell'esempio di manifesto seguente hello `NodeContainerServicePackage1` e `NodeContainerServicePackage2` possibile ogni toohello ascolto stessa porta (entrambi i servizi sono in attesa sulla `Endpoint1`).

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
È possibile combinare e abbinare diverse modalità di rete tra servizi all'interno di un'applicazione per un cluster di Windows. Pertanto, è possibile avere alcuni servizi sulla modalità `open` e alcuni sulla modalità di rete `nat`. Quando un servizio è configurato con `nat`, porta hello è in ascolto toomust essere univoco. La combinazione di modalità di rete per diversi servizi non è supportata nei cluster di Linux. 


## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono state fornite informazioni sulle modalità di rete offerte da Service Fabric.  

* [Modello di applicazione di Service Fabric](service-fabric-application-model.md)
* [Risorse del manifesto del servizio di Service Fabric](service-fabric-application-model.md)
* [Distribuire un tooService di contenitore di Windows Fabric in Windows Server 2016](service-fabric-get-started-containers.md)
* [Distribuire un tooService contenitore Docker dell'infrastruttura in Linux](service-fabric-get-started-containers-linux.md)
