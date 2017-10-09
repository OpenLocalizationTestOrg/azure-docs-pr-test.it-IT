---
title: "modalità di distribuzione (classico) Manager e gestione dei servizi di aaaResource | Documenti Microsoft"
description: Differenze di hello tra Gestione risorse e i modelli di distribuzione classica.
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Modelli di distribuzione di Azure
Hello piattaforma Azure è in fase di transizione.  Se si è tooAzure nuova o viene utilizzata per anni, è importante toounderstand alcune delle principali modifiche hello rendiamo piattaforma toohello durante tale transizione.

Tutte le risorse di Azure supportano uno o entrambi i modelli di distribuzione hello:

* **Gestione risorse:** si tratta di modello di distribuzione più recente di hello per le risorse di Azure. La maggior parte delle risorse più recenti supporta già questo modello di distribuzione, che in futuro sarà supportato da tutte le risorse.   
* **Classico:** questo modello è attualmente supportato dalla maggior parte delle risorse di Azure esistenti. Nuove risorse aggiunti tooAzure non supporta questo modello.

Hello documentazione ogni risorsa di Azure i modelli di servizio possibile creare con.

## <a name="why-does-this-matter"></a>Perché è importante?
È importante per hello seguenti motivi:

* funzionalità della piattaforma Azure Hello in uso sono diverse per questi due modelli.  Ad esempio, le risorse create utilizzando il modello di distribuzione di gestione risorse hello (o semplicemente Resource Manager) possono essere create con [modelli di gestione risorse di Azure](azure-resource-manager/resource-group-overview.md#template-deployment), mentre non le risorse create con modello di distribuzione classica hello.
* Hello funzionalità singole risorse di Azure o comportamenti possono essere diverso nei due modelli di hello o esiste solo in un modello o altri hello.  Ad esempio, bilanciamento del carico del traffico tra macchine virtuali create con modello di distribuzione classica hello è *implicita* perché le macchine virtuali sono membri di un servizio Cloud di Azure e carico viene automaticamente bilanciato tra virtuale macchine in un servizio cloud. Macchine virtuali create con Gestione risorse non sono membri di un servizio cloud e deve essere una risorsa distinta di bilanciamento del carico di Azure *in modo esplicito* creato bilanciare il traffico tooload tra più macchine virtuali.  
* Le modalità di creazione, configurazione e gestione delle risorse di Azure differiscono tra questi due modelli.
* Le risorse create usando un modello di distribuzione non possono necessariamente interagire con le risorse create usando un modello di distribuzione differente. Ad esempio, le macchine virtuali di Azure creato tramite un modello di distribuzione può essere solo tooAzure connesso reti virtuali create utilizzando hello stesso modello di distribuzione.    

Ciascuno dei modelli di distribuzione hello sottostante è un application programming interface (API) per ogni risorsa.  È presente un [API di gestione risorse](https://msdn.microsoft.com/library/azure/dn948464.aspx) per modello di distribuzione di gestione risorse di hello e una [servizio Gestione API](https://msdn.microsoft.com/library/azure/ee460799.aspx) per modello di distribuzione classica hello. Gli sviluppatori possono scrivere codice toointeract con queste API *direttamente*.  

I professionisti IT, tuttavia, in genere interagiscono con le API *indirettamente* tramite un portale con interfaccia grafico in un web browser, tramite Azure PowerShell cmdlet in un computer Windows o con hello Azure interfaccia della riga di comando (CLI) in entrambi un Computer Windows, OS X o Linux. Tutte e tre questi metodi indiretti utilizzati dal professionista IT hello interagiscono direttamente con le API di hello. Ciò significa che quando le nuove funzionalità sono state introdotta toohello Azure piattaforma o le risorse, è sempre disponibile direttamente attraverso hello API in primo luogo, con i metodi di hello indiretta sfruttare il supporto per hello nuove risorse e funzionalità dopo hello API viene reso disponibile.  

Hello nelle sezioni seguenti vengono illustrano le risorse di Azure vengono configurate mediante hello diversi modelli di distribuzione tramite i metodi di hello tre indiretta.

## <a name="portals"></a>Portali
Azure offre due portali:

* **[Portale di Azure](https://manage.windowsazure.com):** se si usa Azure da tempo si conosce già questo portale, È utilizzato toocreate e configurare le risorse di Azure meno recenti che supportano il modello di distribuzione classica hello. È possibile usarlo toocreate o configurare le risorse che supportano solo il gestore delle risorse. 
* **[Portale di anteprima di Azure](https://azure.microsoft.com/overview/preview-portal/):** se si usa una risorsa di Azure più recente è probabile che questo portale sia già stato usato. Può essere utilizzato toocreate e configurare alcune risorse di Azure. Che verrà infine in grado di toocreate e configurare tutte le risorse di Azure con esso. Per alcune risorse che supportano entrambi i modelli di distribuzione, questo portale può essere utilizzato toocreate e configurare una risorsa tramite un modello di distribuzione. 

Alcune risorse e le funzionalità possono essere solo create e configurate in un portale o hello altri. Alcune risorse o funzionalità non (ancora) è stato possibile creare o configurato in entrambi i portali e può essere configurata solo con PowerShell, hello CLI o entrambi. documentazione di Hello per ogni risorsa di Azure in dettaglio il metodo può essere creato con. 

## <a name="powershell"></a>PowerShell
Con [PowerShell](/powershell/azureps-cmdlets-docs) è possibile utilizzare un toocreate di script della riga di comando o dall'autore e configurare le risorse di Azure da un computer Windows.  Le singole risorse di Azure contengono [cmdlet di Resource Manager](/powershell/azure/overview), [cmdlet di Gestione dei servizi](/powershell/azure/overview?view=azuresmps-3.7.0) o entrambi.  Alcune risorse e le funzionalità possono essere create solo e/o configurato tramite PowerShell o hello CLI. A seconda risorsa hello, quando si usano i cmdlet PowerShell di gestione risorse è possibile due opzioni per la creazione e configurazione delle risorse di Azure:

* **Solo i cmdlet di PowerShell:** è possibile creare e configurare ogni risorsa di Azure singolarmente utilizzando i cmdlet di hello per ogni risorsa. È possibile eseguire questa operazione dalla riga di comando o includendo più comandi in uno script di PowerShell archiviabile e la cui versione può essere controllata.
* **I cmdlet di PowerShell con un modello di gestione risorse di Azure:** è possibile utilizzare PowerShell toocreate Azure risorse usando un modello di gestione risorse di Azure. È possibile salvare i modelli e controllarne la versione. Per ulteriori informazioni, leggere hello [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md) articolo. Esistono anche diversi [modelli di Guida introduttiva](https://azure.microsoft.com/documentation/templates/) per soluzioni comuni che è possibile scaricare e modificare.

## <a name="cli"></a>CLI
È possibile creare e configurare le risorse di Azure da computer Windows o OS X, Linux utilizzando hello CLI.  Hello lettura [installazione hello Azure CLI](cli-install-nodejs.md) hello tooinstall di articolo CLI sul sistema operativo scelto. Come PowerShell, sono disponibili diversi comandi che devono essere utilizzati a seconda se si creano risorse usando [Gestione risorse](xplat-cli-azure-resource-manager.md) o hello [classica (servizio di gestione)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) modelli di distribuzione.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni, vedere [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Comprendere come troppo[progettare modelli](best-practices-resource-manager-design-templates.md).

