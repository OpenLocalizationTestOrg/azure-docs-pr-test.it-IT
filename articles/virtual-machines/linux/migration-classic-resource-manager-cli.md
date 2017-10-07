---
title: macchine virtuali di aaaMigrate tooResource Manager utilizzando l'interfaccia CLI di Azure | Documenti Microsoft
description: Questo articolo descrive migrazione supportata dalla piattaforma hello delle risorse da Gestione risorse di tooAzure classico mediante Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Eseguire la migrazione di risorse IaaS da tooAzure classico Resource Manager tramite l'interfaccia CLI di Azure
Queste procedure illustrano di funzionamento dei comandi toomigrate infrastruttura come un servizio (IaaS) alle risorse dal modello di distribuzione Azure Resource Manager hello distribuzione classica modello toohello toouse Azure interfaccia della riga di comando (CLI). articolo Hello richiede hello [CLI di Azure](../../cli-install-nodejs.md).

> [!NOTE]
> Tutte le operazioni descritte di seguito hello sono idempotenti. Se si dispone di un problema diverso da una funzionalità non supportata o un errore di configurazione, è consigliabile che si riprova hello preparare, interrompere o l'operazione di commit. piattaforma Hello quindi tenterà nuovamente l'azione hello.
> 
> 

<br>
Ecco un ordine di hello tooidentify diagramma di flusso in cui è necessario passaggi toobe eseguite durante un processo di migrazione

![Schermata che illustra i passaggi della migrazione hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Passaggio 1: Preparare la migrazione
Ecco alcune procedure consigliate che è consigliabile quando si valutano la migrazione di risorse IaaS da tooResource classico Manager:

* Leggere hello [elenco di configurazioni non supportate o funzionalità](../windows/migration-classic-resource-manager-overview.md). Se si dispone di macchine virtuali che utilizzano le configurazioni non supportate o funzionalità, è consigliabile attendere hello configurazione delle funzionalità supporto toobe annunciato. In alternativa, è possibile rimuovere tale funzionalità o esce da tale migrazione tooenable configurazione se adatto alle proprie esigenze.
* Se si sono state automatizzate script da distribuire l'infrastruttura e le applicazioni oggi, provare a toocreate una configurazione di test simile utilizzando gli script per la migrazione. In alternativa, è possibile impostare gli ambienti di esempio di tramite hello portale di Azure.

> [!IMPORTANT]
> Gateway applicazione non sono attualmente supportati per la migrazione da tooResource classico Manager. toomigrate una rete virtuale classica con un gateway di applicazione, rimuovere gateway hello prima dell'esecuzione di una rete di hello toomove operazione Prepare. Dopo aver completato la migrazione di hello, riconnettersi gateway hello in Gestione risorse di Azure. 
>
>Gateway ExpressRoute connessione tooExpressRoute circuiti in un'altra sottoscrizione non è possibile eseguire la migrazione automaticamente. In questi casi, è possibile rimuovere gateway ExpressRoute hello, la migrazione della rete virtuale hello e ricreare il gateway di hello. Vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../../expressroute/expressroute-migration-classic-resource-manager.md) per ulteriori informazioni.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Passaggio 2: Impostare la sottoscrizione e registrare il provider di hello
Per gli scenari di migrazione, è necessario tooset dell'ambiente per entrambi classico e Gestione risorse. [Installare l'interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) e [selezionare la sottoscrizione](../../xplat-cli-connect.md).

Account di accesso tooyour.

    azure login

Selezionare hello sottoscrizione di Azure utilizzando hello comando seguente.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> La registrazione è una volta in passaggio ma è necessario toobe eseguita una volta prima di procedere alla migrazione. Verrà visualizzato hello seguente messaggio di errore senza registrazione 
> 
> *BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione) 
> 
> 

Registrare con provider di risorse di migrazione hello utilizzando hello comando seguente. Si noti che in alcuni casi si verifica il timeout del comando. Tuttavia, la registrazione di hello sarà ha esito positivo.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Attendere cinque minuti per hello toofinish di registrazione. È possibile controllare stato hello dell'approvazione hello utilizzando hello comando seguente. Assicurarsi che RegistrationState sia `Registered` prima di procedere.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Passare ora toohello CLI `asm` modalità.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Passaggio 3: Assicurarsi di disporre di core a sufficienza macchina virtuale di gestione risorse di Azure in hello area della distribuzione corrente o rete virtuale di Azure
Per questo passaggio è necessario tooswitch troppo`arm` modalità. Eseguire questa operazione con hello comando seguente.

```
azure config mode arm
```

È possibile utilizzare hello seguente CLI comando toocheck hello quantità corrente di core che nel gestore di risorse di Azure. toolearn più sulle quote di core, vedere [limiti e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Dopo aver verificato questo passaggio, è possibile passare nuovamente troppo`asm` modalità.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Passaggio 4: Opzione 1 - Eseguire la migrazione delle macchine virtuali a un servizio cloud
Ottenere un elenco di servizi cloud tramite hello comando seguente, quindi selezione hello cloud servizio che si desidera toomigrate hello. Si noti che se hello macchine virtuali nel servizio cloud hello si trovano in una rete virtuale o se hanno ruoli web/di lavoro, si otterrà un messaggio di errore.

    azure service list

Eseguire hello dopo il nome di comando tooget hello distribuzione per il servizio cloud hello dall'output di hello dettagliato. Nella maggior parte dei casi, il nome di distribuzione hello è hello uguale al nome del servizio cloud hello.

    azure service show <serviceName> -vv

In primo luogo, verificare se è possibile eseguire la migrazione del servizio cloud hello utilizzando hello seguenti comandi:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Preparare le macchine virtuali hello nel servizio cloud hello per la migrazione. Si dispone di due opzioni toochoose da.

Se si desidera toomigrate hello macchine virtuali tooa piattaforma rete virtuale creata, utilizzare hello comando seguente.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Se si desidera tooan toomigrate rete virtuale nel modello di distribuzione di gestione risorse di hello esistente, utilizzare hello comando seguente.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Dopo la preparazione hello operazione ha esito positivo, è possibile esaminare hello output dettagliato tooget hello lo stato di migrazione di macchine virtuali hello e verificare che siano in hello `Prepared` stato.

    azure vm show <vmName> -vv

Controllare la configurazione di hello hello preparata risorse con CLI o hello portale di Azure. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.

    azure service deployment abort-migration <serviceName> <deploymentName>

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Passaggio 4: Opzione 2 - Eseguire la migrazione delle macchine virtuali a una rete virtuale
Selezione hello rete virtuale che si desidera toomigrate. Si noti che se la rete virtuale hello contiene ruoli web/di lavoro o macchine virtuali con configurazioni non supportate, si riceverà un messaggio di errore di convalida.

Ottenere tutte le reti virtuali hello nella sottoscrizione hello utilizzando hello comando seguente.

    azure network vnet list

output di Hello sarà simile al seguente:

![Schermata della riga di comando hello con il nome di rete virtuale intera hello evidenziato.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

In hello sopra riportato, hello **virtualNetworkName** è l'intero nome hello **"Gruppo classicubuntu16 classicubuntu16"**.

In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale di hello utilizzando hello comando seguente:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Preparare rete virtuale di hello di propria scelta per la migrazione utilizzando hello comando seguente.

    azure network vnet prepare-migration <virtualNetworkName>

Controllare la configurazione di hello hello preparata macchine virtuali con CLI o hello portale di Azure. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.

    azure network vnet abort-migration <virtualNetworkName>

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Passaggio 5: Eseguire la migrazione di un account di archiviazione
Dopo avere utilizzato la migrazione di macchine virtuali hello, è consigliabile che si esegue la migrazione di account di archiviazione hello.

Preparare account di archiviazione hello per la migrazione tramite hello comando seguente

    azure storage account prepare-migration <storageAccountName>

Controllare la configurazione di hello hello preparata con CLI o hello Azure portale account di archiviazione. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.

    azure storage account abort-migration <storageAccountName>

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utilizzare le risorse IaaS toomigrate PowerShell da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rivedere gli errori di migrazione più comuni](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
