---
title: aaaTechnical prerequisiti per la creazione di un'immagine di macchina virtuale per hello Azure Marketplace | Documenti Microsoft
description: Comprendere i requisiti di hello per la creazione e distribuzione di un toohello immagine di macchina virtuale Azure Marketplace per altri utenti toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Prerequisiti di tecnici per la creazione di un'immagine di macchina virtuale per hello Azure Marketplace
Processo hello accuratamente prima di iniziare leggere e comprendere dove e perché viene eseguita ogni passaggio. Per quanto possibile, è necessario preparare le informazioni della società e altri dati, scaricare gli strumenti necessari, e/o creare componenti tecnici prima di iniziare il processo di creazione offerta hello. Questi elementi dovrebbero risultare chiari dalla lettura di questo articolo.  

## <a name="download-needed-tools--applications"></a>Scaricare gli strumenti e le applicazioni necessari
È necessario avere hello pronti prima di iniziare il processo di hello gli elementi seguenti:

* A seconda del sistema operativo di destinazione, installare hello [cmdlet di Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) o [strumento dell'interfaccia della riga di comando Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) da hello [download di Azure](https://azure.microsoft.com/downloads/) pagina.
* Installare lo strumento di esplorazione dell'archiviazione di Azure da CodePlex.
* Scaricare e installare lo strumento di Test di certificazione hello per Azure Certified:
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). È necessario uno strumento di certificazione hello toorun computer basati su Windows. Se non si dispone di un computer basato su Windows è disponibile, è possibile eseguire lo strumento hello in Azure usando una macchina virtuale basata su Windows.

## <a name="platforms-supported"></a>Piattaforme supportate
È possibile sviluppare macchine virtuali basate su Azure in Windows o Linux. Alcuni elementi di hello processo, ad esempio la creazione di un compatibili con Azure disco rigido virtuale (VHD), utilizzare diversi strumenti e passaggi a seconda del sistema operativo in uso di pubblicazione:  

* Se si utilizza Linux, fare riferimento a toohello di sezione "Creare un disco rigido virtuale di Azure compatibile (basati su Linux)" di hello [Guida alla pubblicazione immagine di macchina virtuale](marketplace-publishing-vm-image-creation.md).
* Se si utilizza Windows, fare riferimento a toohello di sezione "Creare un disco rigido virtuale di Azure compatibile (basato su Windows)" di hello [Guida alla pubblicazione immagine di macchina virtuale](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> È necessario accedere a computer basati su Windows tooa per:
> 
> * Eseguire lo strumento di convalida certificazione hello.
> * Creare l'URL di firma di accesso hello disco rigido virtuale condiviso per hello invio certificazione disco rigido virtuale.
> 
> 

## <a name="develop-your-vhd"></a>Sviluppare il disco rigido virtuale
È possibile sviluppare i dischi rigidi virtuali di Azure in locale o cloud hello:

* Lo sviluppo basato sul cloud implica che tutte le operazioni di sviluppo vengono eseguite in modalità remota su un disco rigido virtuale residente in Azure.
* Lo sviluppo in locale richiede il download di un disco rigido virtuale e il relativo sviluppo tramite l'infrastruttura locale. Sebbene questa operazione sia possibile, non è consigliabile. Si noti che lo sviluppo per Windows o SQL locale richiede è codici di licenza toohave hello rilevanti in locale. Non è possibile includere o installare SQL Server dopo aver creato una VM. È anche necessario basare l'offerta in un'immagine SQL approvata da hello portale di Azure. Se si decide di toodevelop locale, è necessario eseguire alcuni passaggi in modo diverso da se si sviluppa in cloud hello. È possibile trovare le informazioni appropriate in [Creare un'immagine di VM in locale](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
