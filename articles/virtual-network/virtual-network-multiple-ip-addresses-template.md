---
title: gli indirizzi IP aaaMultiple per macchine virtuali di Azure - modello | Documenti Microsoft
description: "Informazioni su come tooassign più gli indirizzi IP macchina virtuale tooa utilizzando un modello di gestione risorse di Azure."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Assegnare più indirizzi IP macchine toovirtual utilizzando un modello di gestione risorse di Azure

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

In questo articolo viene illustrato come una macchina virtuale (VM) durante la distribuzione Azure Resource Manager hello toocreate modello utilizzando un modello di gestione risorse. Impossibile assegnare indirizzi IP pubblici e privati toohello stessa scheda di rete quando si distribuisce una macchina virtuale tramite il modello di distribuzione classica hello. ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Descrizione modello

Distribuzione di un modello consente tooquickly e creare in modo coerente le risorse di Azure con i valori di configurazione diverso. Hello lettura [procedura dettagliata di modello di gestione risorse](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo se non si ha familiarità con i modelli di gestione risorse di Azure. Hello [distribuire una macchina virtuale con più indirizzi IP](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) modello viene utilizzato in questo articolo.

<a name="resources"></a>La distribuzione del modello hello crea hello seguenti risorse:

|Risorsa|Nome|Descrizione|
|---|---|---|
|Interfaccia di rete|*myNic1*|configurazioni IP tre Hello descritte nella sezione di hello scenario di questo articolo vengono create e assegnate toothis scheda di rete.|
|Risorsa indirizzo IP pubblico|ne vengono creati 2: *myPublicIP* e *myPublicIP2*|Queste risorse vengono assegnate indirizzi IP pubblici statici e vengono assegnate toohello *IPConfig 1* e *IPConfig 2* le configurazioni IP descritte nello scenario di hello.|
|VM|*myVM1*|Macchina virtuale Standard DS3.|
|Rete virtuale|*myVNet1*|Rete virtuale con una subnet denominata *mySubnet*.|
|Account di archiviazione|Distribuzione toohello univoco|Account di archiviazione.|

<a name="parameters"></a>Quando si distribuisce il modello di hello, è necessario specificare i valori per hello seguenti parametri:

|Nome|Descrizione|
|---|---|
|adminUsername|Nome utente amministratore. nome utente Hello deve essere conformi alle [requisiti di nome utente di Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Password di amministratore password hello devono essere conformi alle [requisiti delle password di Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|Nome DNS per PublicIPAddressName1. nome DNS Hello risolverà tooone di indirizzi IP pubblici hello assegnato toohello macchina virtuale. Hello nome deve essere univoco all'interno di hello Azure regione (località) è creare hello macchina virtuale in.|
|dnsLabelPrefix1|Nome DNS per PublicIPAddressName2. nome DNS Hello risolverà tooone di indirizzi IP pubblici hello assegnato toohello macchina virtuale. Hello nome deve essere univoco all'interno di hello Azure regione (località) è creare hello macchina virtuale in.|
|OSVersion|versione di Windows/Linux Hello per hello macchina virtuale. sistema operativo Hello è un'immagine completamente con patch di hello la versione di Windows/Linux selezionato.|
|imagePublisher|Hello Windows/Linux immagine server di pubblicazione per hello selezionare macchina virtuale.|
|imageOffer|immagine di Windows/Linux Hello per hello seleziona macchina virtuale.|

Ognuna delle risorse di hello distribuite dal modello hello è configurata con varie impostazioni predefinite. È possibile visualizzare queste impostazioni mediante uno dei seguenti metodi hello:

- **Modello di visualizzazione hello in GitHub:** se si ha familiarità con i modelli, è possibile visualizzare le impostazioni di hello all'interno di hello [modello](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Visualizzare le impostazioni di hello dopo la distribuzione:** se non si ha familiarità con i modelli, è possibile distribuire il modello di hello tramite i passaggi in uno dei seguenti sezioni hello e quindi visualizzare le impostazioni di hello dopo la distribuzione.

È possibile utilizzare hello portale di Azure, PowerShell o hello Azure interfaccia della riga di comando (CLI) toodeploy hello modello. Tutti i metodi di producano hello stesso risultato. modello hello toodeploy, hello completato i passaggi in uno dei hello le sezioni seguenti:

## <a name="deploy-using-hello-azure-portal"></a>Distribuire mediante hello portale di Azure

modello di hello toodeploy utilizzando hello portale di Azure completo hello seguendo i passaggi:

1. Modificare il modello di hello, se necessario. Consente di distribuire il modello di Hello risorse hello e le impostazioni elencate nella hello [risorse](#resources) sezione di questo articolo. toolearn ulteriori informazioni sui modelli e in che modo tooauthor usarle, vedere l'articolo hello [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)articolo.
2. Distribuire il modello di hello con uno dei seguenti metodi hello:
    - **Modello di hello selezionare nel portale di hello:** hello completato i passaggi in hello [distribuire le risorse da un modello personalizzato](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) articolo. Scegliere il modello di pre-esistente hello denominato *101-vm-più-ipconfig*.
    - **Direttamente:** fare clic su hello seguente modello di pulsante tooopen hello direttamente nel portale di hello:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Indipendentemente dal metodo hello desiderato, è necessario toosupply valori per hello [parametri](#parameters) elencate in precedenza in questo articolo. Dopo aver distribuito hello VM, connettersi toohello macchina virtuale e aggiungere hello privata IP indirizzi toohello del sistema operativo è stato distribuito completando hello passaggi hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

## <a name="deploy-using-powershell"></a>Distribuire tramite PowerShell

modello di hello toodeploy tramite PowerShell, hello completo alla procedura seguente:

1. Modello di distribuzione hello completando i passaggi hello hello [distribuire un modello con PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) articolo. Hello descritti più opzioni per la distribuzione di un modello. Se si sceglie toodeploy utilizzando hello `-TemplateUri parameter`, hello URI per questo modello è *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Se si sceglie toodeploy utilizzando hello `-TemplateFile` parametro copia hello contenuto di hello [file modello](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) da GitHub in un nuovo file nel computer. Modificare il contenuto del modello hello, se opportuno. Consente di distribuire il modello di Hello risorse hello e le impostazioni elencate nella hello [risorse](#resources) sezione di questo articolo. toolearn ulteriori informazioni sui modelli e in che modo tooauthor usarle, vedere l'articolo hello [modelli Authoring Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)articolo.

    Indipendentemente dall'opzione hello scegliere modello hello toodeploy con, è necessario fornire valori per i valori di parametro hello elencati nella hello [parametri](#parameters) sezione di questo articolo. Se si sceglie di parametri di toosupply utilizzando un file dei parametri, copiare il contenuto di hello di hello [file dei parametri](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) da GitHub in un nuovo file nel computer in uso. Modificare i valori hello nel file hello. Utilizza il file hello creato come valore di hello per hello `-TemplateParameterFile` parametro.

    toodetermine i valori validi per i parametri imageOffer hello OSVersion e ImagePublisher, hello completo di passaggi di hello [Naviga e l'articolo di immagini di macchina virtuale di Windows seleziona](../virtual-machines/windows/cli-ps-findimage.md) articolo.

    >[!TIP]
    >Se non si è certi se un dnslabelprefix è disponibile, immettere hello `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind comando out. Se è disponibile, il comando hello restituirà `True`.

2. Dopo aver distribuito hello VM, connettersi toohello macchina virtuale e aggiungere hello privata IP indirizzi toohello del sistema operativo è stato distribuito completando hello passaggi hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

## <a name="deploy-using-hello-azure-cli"></a>Distribuire mediante hello CLI di Azure

modello di hello toodeploy utilizzando hello Azure CLI 1.0, hello completo alla procedura seguente:

1. Modello di distribuzione hello completando i passaggi hello hello [distribuire un modello con hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) articolo. Hello descritti più opzioni per la distribuzione modello hello. Se si sceglie toodeploy utilizzando hello `--template-uri` (-f), hello URI per questo modello è *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Se si sceglie toodeploy utilizzando hello `--template-file` (-f) parametro copia hello contenuto di hello [file modello](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) da GitHub in un nuovo file nel computer. Modificare il contenuto del modello hello, se opportuno. Consente di distribuire il modello di Hello risorse hello e le impostazioni elencate nella hello [risorse](#resources) sezione di questo articolo. toolearn ulteriori informazioni sui modelli e in che modo tooauthor usarle, vedere l'articolo hello [modelli Authoring Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)articolo.

    Indipendentemente dall'opzione hello scegliere modello hello toodeploy con, è necessario fornire valori per i valori di parametro hello elencati nella hello [parametri](#parameters) sezione di questo articolo. Se si sceglie di parametri di toosupply utilizzando un file dei parametri, copiare il contenuto di hello di hello [file dei parametri](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) da GitHub in un nuovo file nel computer in uso. Modificare i valori hello nel file hello. Utilizza il file hello creato come valore di hello per hello `--parameters-file` (-e) parametro.

    toodetermine i valori validi per i parametri imageOffer hello OSVersion e ImagePublisher, hello completo di passaggi di hello [Naviga e l'articolo di immagini di macchina virtuale di Windows seleziona](../virtual-machines/windows/cli-ps-findimage.md) articolo.

2. Dopo aver distribuito hello VM, connettersi toohello macchina virtuale e aggiungere hello privata IP indirizzi toohello del sistema operativo è stato distribuito completando hello passaggi hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
