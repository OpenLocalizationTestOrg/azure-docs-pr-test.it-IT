---
title: Le differenze e le considerazioni per le macchine virtuali nello Stack di Azure | Documenti Microsoft
description: Informazioni sulle considerazioni e le differenze quando si lavora con le macchine virtuali nello Stack di Azure.
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 6613946D-114C-441A-9F74-38E35DF0A7D7
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2018
ms.author: brenduns
ms.openlocfilehash: 6eafa2a5058ef1309cbf50be069ea1bb12f7e5b9
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Considerazioni per le macchine virtuali in Azure Stack

*Si applica a: Azure Stack integrate di sistemi Azure Stack Development Kit*

Macchine virtuali sono un su richiesta, le risorse di elaborazione scalabili offerti dallo Stack di Azure. Quando si usano macchine virtuali, è necessario comprendere che non esistono differenze tra le funzionalità disponibili in Azure e Azure Stack. In questo articolo viene fornita una panoramica delle considerazioni univoche per le macchine virtuali e delle relative funzionalità nello Stack di Azure. Per ulteriori informazioni sulle differenze generali tra Stack di Azure e Azure, vedere il [considerazioni chiave](azure-stack-considerations.md) articolo.

## <a name="cheat-sheet-virtual-machine-differences"></a>Schede di riferimento rapido: macchina virtuale differenze

| Funzionalità | Azure (globale) | Azure Stack |
| --- | --- | --- |
| Immagini di macchine virtuali | Azure Marketplace contiene le immagini che è possibile utilizzare per creare una macchina virtuale. Vedere il [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) pagina per visualizzare l'elenco delle immagini che sono disponibili in Azure Marketplace. | Per impostazione predefinita, sono non sono presenti immagini disponibili in marketplace dello Stack di Azure. L'amministratore del cloud di Azure Stack deve pubblicare o scaricare immagini marketplace Azure Stack prima che gli utenti possono usare tali. |
| Dimensioni delle macchine virtuali | Azure supporta un'ampia gamma di dimensioni per le macchine virtuali. Per conoscere le dimensioni disponibili e le opzioni, vedere il [dimensioni delle macchine virtuali di Windows](../../virtual-machines/virtual-machines-windows-sizes.md) e [dimensioni delle macchine virtuali Linux](../../virtual-machines/linux/sizes.md) argomenti. | Stack di Azure supporta un subset di dimensioni delle macchine virtuali che sono disponibili in Azure. Per visualizzare l'elenco dei formati supportati, vedere il [dimensioni delle macchine virtuali](#virtual-machine-sizes) sezione di questo articolo. |
| Quote macchina virtuale | [I limiti di quota](../../azure-subscription-service-limits.md#service-specific-limits) impostati da Microsoft | L'amministratore del cloud di Azure Stack deve assegnare quote prima di macchine virtuali che offrono agli utenti. |
| Estensioni macchina virtuale |Azure supporta un'ampia gamma di estensioni di macchina virtuale. Per ulteriori informazioni sulle estensioni disponibili, consultare il [estensioni delle macchine virtuali e le funzionalità](../../virtual-machines/windows/extensions-features.md) articolo.| Stack di Azure supporta un subset di estensioni che sono disponibili in Azure e dell'estensione hanno versioni specifiche. L'amministratore del cloud di Azure Stack possa scegliere le estensioni da messe a disposizione per i propri utenti. Per visualizzare l'elenco di estensioni supportate, consultare il [estensioni delle macchine virtuali](#virtual-machine-extensions) sezione di questo articolo. |
| Rete della macchina virtuale | Indirizzi IP pubblici assegnati alle macchine virtuali tenant sono accessibili tramite Internet.<br><br><br>Macchine virtuali di Azure è un nome DNS predefinito | Indirizzi IP pubblici assegnati a una macchina virtuale tenant sono accessibili solo l'ambiente Azure Stack Development Kit. Un utente deve avere accesso al Kit di sviluppo dello Stack di Azure tramite [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) per connettersi a una macchina virtuale che viene creata nello Stack di Azure.<br><br>Macchine virtuali create all'interno di un'istanza specifica di Stack di Azure è un nome DNS in base al valore configurato dall'amministratore del cloud. |
| Archiviazione della macchina virtuale | Supporta [dischi gestiti.](../../virtual-machines/windows/managed-disks-overview.md) | Dischi gestiti non sono ancora supportati nello Stack di Azure. |
| Versioni dell'API | Azure offre sempre le versioni più recenti di API per tutte le funzionalità di macchina virtuale. | Stack di Azure supporta versioni specifiche di API e servizi di Azure specifici per questi servizi. Per visualizzare l'elenco delle versioni API supportate, consultare il [versioni API](#api-versions) sezione di questo articolo. |
|Set di disponibilità della macchina virtuale|Più domini di errore (2 o 3 regione)<br>Più domini di aggiornamento<br>Supporto disco gestito|Dominio di errore singolo<br>Dominio di aggiornamento singolo<br>Nessun supporto per dischi gestiti|
|set di scalabilità di macchine virtuali|Scalabilità automatica è supportata|Scalabilità automatica non è supportato.<br>Aggiungere più istanze di una scala impostata utilizzando il portale, i modelli di gestione risorse o PowerShell.

## <a name="virtual-machine-sizes"></a>Dimensioni delle macchine virtuali

Stack di Azure supporta le dimensioni seguenti:

| type | Dimensione | Intervallo di dimensioni supportate |
| --- | --- | --- |
|Scopo generico |Basic A|A0 - A4|
|Scopo generico |A standard|A0-A7|
|Scopo generico |Serie D|D1 - D4|
|Scopo generico |Serie Dv2|D1_v2 - D5_v2|
|Scopo generico |Serie DS|DS1 - DS4|
|Scopo generico |Serie DSv2|DS1_v2 - DS5_v2|
|Ottimizzate per la memoria|Serie DS|DS11 - DS14|
|Ottimizzate per la memoria |Serie DSv2|DS11_v2 - DS14_v2|

Dimensioni delle macchine virtuali e le relative quantità di risorse associati sono coerenti tra Stack di Azure e Azure. Ad esempio, questa coerenza include la quantità di memoria, numero di core e la dimensione o numero di dischi dati che possono essere creati. Prestazioni delle stesse dimensioni di macchina virtuale nello Stack di Azure dipendono tuttavia le caratteristiche di un particolare ambiente dello Stack di Azure sottostante.

## <a name="virtual-machine-extensions"></a>Estensioni macchina virtuale

 Lo Stack di Azure supporta le seguenti versioni di estensione di macchina virtuale:

![Estensioni di VM](media/azure-stack-vm-considerations/vm-extensions.png)

Utilizzare lo script di PowerShell seguente per ottenere l'elenco di estensioni di macchine virtuali che sono disponibili nell'ambiente dello Stack di Azure:

```powershell
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize
```

## <a name="api-versions"></a>Versioni dell'API

Funzionalità delle macchine virtuali nello Stack di Azure supporta le versioni API seguenti:

![Tipi di risorsa di macchina virtuale](media/azure-stack-vm-considerations/vm-resoource-types.png)

Per ottenere le versioni di API per la funzionalità delle macchine virtuali che sono disponibili nell'ambiente dello Stack di Azure, è possibile utilizzare lo script di PowerShell seguente:

```powershell
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
L'elenco dei tipi di risorse supportati e le versioni dell'API può variare se l'operatore cloud Aggiorna ambiente dello Stack di Azure a una versione più recente.

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale Windows con PowerShell nello Stack di Azure](azure-stack-quick-create-vm-windows-powershell.md)
