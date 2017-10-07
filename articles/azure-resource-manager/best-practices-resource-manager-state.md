---
title: aaaPass valori complessi tra modelli di Azure | Documenti Microsoft
description: Mostra consigliabile approcci per l'utilizzo di dati relativi allo stato tooshare oggetti complessi con i modelli di gestione risorse di Azure e collegato.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Condivisione dello stato tooand dai modelli di gestione risorse di Azure
Questo argomento illustra le procedure consigliate per la gestione e la condivisione dello stato all'interno dei modelli. Hello parametri e variabili illustrate in questo argomento sono riportati alcuni esempi di tipo hello degli oggetti è possibile definire tooconveniently organizzare i requisiti di distribuzione. Da questi esempi, è possibile implementare gli oggetti con valori di proprietà utili per l'ambiente.

Questo argomento fa parte di un white paper di dimensioni maggiori. scaricare hello tooread completo carta, [World classe Resource Manager modelli considerazioni e procedure consigliate di rivelati](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Uso di impostazioni di configurazione standard
Piuttosto che offrono un modello che fornisce la massima flessibilità e le variazioni innumerevoli, un modello comune è tooprovide una selezione di una configurazione conosciuta. In effetti, gli utenti possono selezionare taglie standard, come sandbox, small, medium e large. Altri esempi di taglie sono le offerte di prodotti, come Community Edition o Enterprise Edition. In altri casi, potrebbero essere configurazioni specifiche per i carichi di lavoro di una determinata tecnologia, ad esempio map reduce o no sql.

Con gli oggetti complessi, è possibile creare le variabili che contengono raccolte di dati, talvolta noti anche come "elenchi di proprietà" e utilizzare tale dichiarazione della risorsa di hello toodrive dati nel modello. Questo approccio fornisce configurazioni note ed efficienti di dimensioni variabili, preconfigurate per i clienti. Senza configurazioni note, gli utenti del modello di hello devono determinare dimensioni cluster autonomamente, fattore nei vincoli di risorse di piattaforma ed eseguire matematiche tooidentify hello risultante partizionamento dell'account di archiviazione e altre risorse (a causa delle dimensioni toocluster e limitazioni delle risorse). Inoltre toomaking una migliore esperienza per cliente hello, alcune configurazioni note sono toosupport più semplice e consentono di offrire un livello di densità.

Hello seguente esempio viene illustrato come le variabili di toodefine che contengono oggetti complessi per la rappresentazione di raccolte di dati. le raccolte di Hello definiscono i valori utilizzati per la dimensione della macchina virtuale, le impostazioni di rete, impostazioni del sistema operativo e disponibilità.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Si noti che hello **tshirtSize** variabile concatena magliette hello fornite tramite un parametro (**Small**, **Media**, **grande**) toohello testo **tshirtSize**. Utilizzare questa variabile di oggetto complesso associato hello tooretrieve variabile per tale magliette.

È quindi possibile fare riferimento a queste variabili in un secondo momento nel modello di hello. Hello possibilità tooreference denominato le variabili e le relative proprietà semplifica la sintassi dei modelli di hello e rende facile toounderstand contesto. Hello di esempio seguente definisce una risorsa toodeploy utilizzando oggetti hello illustrati in precedenza tooset valori. Ad esempio, hello dimensioni della macchina virtuale è impostato per il recupero del valore di hello per `variables('tshirtSize').vmSize` mentre il valore di hello per dimensioni del disco hello vengano recuperata dal `variables('tshirtSize').diskSize`. Inoltre, hello URI per un modello collegato viene impostato con il valore di hello per `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Passaggio di stato tooa modello
È possibile condividere lo stato in un modello tramite parametri forniti direttamente durante la distribuzione.

Hello seguenti tabella elenchi comunemente utilizzati parametri nei modelli.

| Nome | Valore | Descrizione |
| --- | --- | --- |
| location |Stringa da un elenco vincolato di aree di Azure |percorso di Hello in cui vengono distribuite le risorse di hello. |
| storageAccountNamePrefix |String |Nome DNS univoco per l'Account di archiviazione in cui vengono collocati i dischi della macchina virtuale di hello hello |
| domainName |String |Nome di dominio di hello accessibile pubblicamente jumpbox macchina virtuale in formato hello: **{domainName}. { percorso}.cloudapp.com** ad esempio: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |String |Nome utente per hello macchine virtuali |
| adminPassword |String |Password per hello macchine virtuali |
| tshirtSize |Stringa da un elenco vincolato di taglie offerte |Hello denominato tooprovision dimensioni unità di scala. Ad esempio, "Small", "Medium", "Large" |
| virtualNetworkName |String |Nome di rete virtuale hello hello consumer desidera toouse. |
| enableJumpbox |Stringa da un elenco vincolato (abilitato/disabilitato) |Parametro che identifica se tooenable un jumpbox per ambiente hello. Valori: "enabled", "disabled" |

Hello **tshirtSize** parametro usato nella sezione precedente hello è definito come:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Passare modelli toolinked stato
Quando ci si connette toolinked modelli, spesso utilizzare una combinazione di statico e generato le variabili.

### <a name="static-variables"></a>Variabili statiche
Variabili statiche sono spesso valori di base tooprovide utilizzato, ad esempio, gli URL vengono utilizzati in un modello.

Nel seguente estratto di codice modello hello `templateBaseUrl` specifica il percorso radice hello per modello hello in GitHub. riga successiva Hello compila una nuova variabile `sharedTemplateUrl` che concatena hello l'URL di base con nome noto di hello del modello di risorse condivise hello. Sotto tale riga, una variabile oggetto complesso è toostore usato un magliette, dove l'URL di base hello è concatenato toohello noto percorso del modello di configurazione e archiviati in hello `vmTemplate` proprietà.

Il vantaggio di Hello di questo approccio è che se il percorso di modello hello viene modificato, è necessario solo toochange variabile statica di hello in un'unica posizione, che viene passata in tutti i modelli di hello collegato.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Variabili generate
Nelle variabili toostatic aggiunta, vengono generate in modo dinamico diverse variabili. In questa sezione vengono illustrati alcuni dei tipi di variabili generate comuni hello.

#### <a name="tshirtsize"></a>tshirtSize
Si ha familiarità con questa variabile generata dagli esempi hello precedenti.

#### <a name="networksettings"></a>networkSettings
In un hello capacità, funzionalità o il modello di soluzione con ambito end-to-end, modelli collegati in genere creano risorse esistenti in una rete. Un approccio semplice è toouse le impostazioni di rete toostore un oggetto complesso e passarli toolinked modelli.

Di seguito è riportato un esempio di impostazioni di rete di comunicazione.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Le risorse create nei modelli collegati vengono spesso inserite in un set di disponibilità. Nel seguente esempio di hello, hello Nome set di disponibilità specificato e hello anche dominio di errore e aggiorna toouse conteggio di dominio.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Se è necessario più set di disponibilità (ad esempio, uno per i nodi principali) e un altro per i nodi di dati, è possibile utilizzare un nome come prefisso, specificare più set di disponibilità o di seguire il modello di hello illustrato in precedenza per la creazione di una variabile per una specifica magliette.

#### <a name="storagesettings"></a>storageSettings
I dettagli di archiviazione spesso vengono condivisi con i modelli collegati. Nell'esempio hello riportato di seguito, un *storageSettings* oggetto fornisce informazioni dettagliate su hello i nomi degli account e il contenitore di archiviazione.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Con i modelli collegati, potrebbe essere tipi di nodi toovarious le impostazioni del sistema operativo toopass tra tipi diversi di configurazione. Un oggetto complesso è un modo semplice toostore e condivisione di informazioni sul sistema operativo e lo rende anche più facile toosupport più sistemi operativi disponibili per la distribuzione.

Hello esempio seguente viene illustrato un oggetto per *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Una variabile generata, *machineSettings* è un oggetto complesso contenente una combinazione di variabili principali per la creazione di una nuova VM: variabili di Hello includono nome utente dell'amministratore e la password, un prefisso per i nomi di macchina virtuale hello e riferimento a un'immagine del sistema operativo.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Si noti che *osImageReference* recupera hello valori hello *osSettings* variabile definita nel modello principale hello. Pertanto, è possibile modificare facilmente hello del sistema operativo per una macchina virtuale, interamente o in base alle preferenze hello di un consumer di modello.

#### <a name="vmscripts"></a>vmScripts
Hello *vmScripts* oggetto contiene i dettagli sul toodownload script hello ed eseguire in un'istanza di macchina virtuale, inclusi i riferimenti esterni e interni. All'esterno di riferimenti includono infrastruttura hello.
I riferimenti interni includono configurazione e hello installato software installato.

Utilizzare hello *scriptsToDownload* hello toolist proprietà script toodownload toohello macchina virtuale. Inoltre, l'oggetto contiene argomenti della riga di toocommand riferimenti per i diversi tipi di azioni. Tali azioni includono l'esecuzione di installazione predefinita di hello per ogni singolo nodo, un'installazione che viene eseguito dopo che tutti i nodi vengono distribuiti e script aggiuntivi che possono essere specifico tooa modello specificato.

Questo esempio è tratto toodeploy un modello utilizzato MongoDB, che richiede un'analisi toodeliver la disponibilità elevata. Hello *arbiterNodeInstallCommand* è stato aggiunto troppo*vmScripts* analisi hello tooinstall.

sezione variabili Hello è riportate le variabili di hello che definiscono hello testo specifico tooexecute hello lo script con i valori appropriati di hello.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Restituzione dello stato da un modello
Non solo può passare i dati in un modello, è anche possibile chiamata modello di condivisione dati toohello indietro. In hello **restituisce** sezione di un modello collegato, è possibile specificare le coppie chiave/valore che possono essere utilizzate dal modello di origine hello.

Hello esempio seguente viene illustrato come toopass hello indirizzo IP privato generato in un modello collegato.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

Nel modello principale hello, è possibile utilizzare tali dati con hello la seguente sintassi:

    "[reference('master-node').outputs.masterip.value]"

È possibile utilizzare l'espressione seguente nella sezione di output di hello o la sezione relativa alle risorse hello del modello principale hello. È possibile utilizzare l'espressione hello nella sezione variabili hello perché si basa sullo stato del runtime di hello. tooreturn questo valore dal modello principale hello, usare:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Per un esempio di utilizzo hello restituisce una sezione di un modello collegato tooreturn di dischi di dati per una macchina virtuale, vedere [la creazione di più dischi dati per una macchina virtuale](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Definizione delle impostazioni di autenticazione per la macchina virtuale
È possibile utilizzare hello stesso modello illustrato in precedenza per la configurazione delle impostazioni toospecify hello impostazioni di autenticazione per una macchina virtuale. Creare un parametro per il passaggio in tipo di hello di autenticazione.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Aggiungere le variabili per i tipi di autenticazione diversi hello e una variabile toostore quale tipo viene usato per la distribuzione in base al valore di hello del parametro hello.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Quando si definisce una macchina virtuale hello, si imposta hello **osProfile** toohello variabile creata.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Passaggi successivi
* toolearn sulle sezioni hello hello del modello di, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md)
* le funzioni hello toosee disponibili all'interno di un modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md)
