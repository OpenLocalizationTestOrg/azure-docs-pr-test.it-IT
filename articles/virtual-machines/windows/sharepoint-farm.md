---
title: server farm di SharePoint aaaCreate in Azure | Documenti Microsoft
description: Creare rapidamente una nuova farm di SharePoint 2013 o SharePoint 2016 in Azure utilizzando hello Azure marketplace portale.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Creare una server farm di SharePoint utilizzando hello Azure marketplace portale

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Farm SharePoint 2013
Con hello Microsoft Azure portale marketplace, è possibile creare rapidamente le farm di SharePoint Server 2013 preconfigurate. Ciò consente di risparmiare una notevole quantità di tempo in caso si necessiti di una farm di SharePoint di base o a disponibilità elevata per un ambiente di sviluppo e test o in caso si stia valutando l'opportunità di usare SharePoint Server 2013 come soluzione per la collaborazione all'interno dell'organizzazione.

> [!NOTE]
> Hello **Server Farm di SharePoint** elemento hello Azure Marketplace di hello portale di Azure è stato rimosso. È stata sostituita con hello **SharePoint 2013 non a disponibilità elevata Farm** e **Farm a disponibilità elevata di SharePoint 2013** elementi.
>
>

farm di SharePoint base Hello è costituita da tre macchine virtuali in questa configurazione.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

È possibile usare questa configurazione di farm per un'installazione semplificata per lo sviluppo di app SharePoint o per la prima valutazione di SharePoint 2013.

toocreate hello base () SharePoint farm a tre server:

1. Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)
2. Fare clic su **Distribuisci**.
3. In hello **SharePoint 2013 non a disponibilità elevata Farm** riquadro, fare clic su **crea**.
4. Specificare le impostazioni nei passaggi hello di hello **creare SharePoint 2013 non a disponibilità elevata Farm** riquadro e quindi fare clic su **crea**.

farm di SharePoint a disponibilità elevata Hello è costituito da nove macchine virtuali in questa configurazione.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

È possibile utilizzare questa farm configurazione tootest carichi più client elevati, disponibilità elevata del sito di SharePoint esterno hello e gruppi di disponibilità AlwaysOn di SQL Server per una farm di SharePoint. È anche possibile usare questa configurazione per lo sviluppo di app SharePoint in un ambiente a disponibilità elevata.

farm di SharePoint (nove server) a disponibilità elevata hello toocreate:

1. Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)
2. Fare clic su **Distribuisci**.
3. In hello **Farm a disponibilità elevata di SharePoint 2013** riquadro, fare clic su **crea**.
4. Specificare le impostazioni nei passaggi hello sette hello **creare a disponibilità elevata Farm di SharePoint 2013** riquadro e quindi fare clic su **crea**.

> [!NOTE]
> Non è possibile creare hello **SharePoint 2013 non a disponibilità elevata Farm** o **Farm a disponibilità elevata di SharePoint 2013** con una versione di valutazione gratuita di Azure.
>
>

Hello portale di Azure crea entrambi questi farm in una rete virtuale solo cloud con una presenza web con connessione Internet. È presente alcuna site-to-site VPN o ExpressRoute connessione back-tooyour organizzazione rete.

> [!NOTE]
> Quando si crea hello base o farm di SharePoint a disponibilità elevata utilizzando hello portale di Azure, è possibile specificare un gruppo di risorse esistente. toowork risolvere questa limitazione, creare queste aziende con Azure PowerShell. Per altre informazioni, vedere [Creare farm di sviluppo e di testing di SharePoint 2013 con Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Farm SharePoint 2016
Vedere [questo articolo](https://technet.microsoft.com/library/mt723354.aspx) per hello toobuild di istruzioni hello seguente a server singolo SharePoint Server 2016 farm.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>La gestione di farm di SharePoint hello
È possibile amministrare il server di hello di queste aziende tramite le connessioni Desktop remoto. Per ulteriori informazioni, vedere [accedere alla macchina virtuale toohello](quick-create-portal.md#connect-to-virtual-machine).

Dal sito di SharePoint di amministrazione centrale hello, è possibile configurare i siti, applicazioni di SharePoint e altre funzionalità. Per altre informazioni, vedere [Configurare SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Passaggi successivi
* Altre [configurazioni di SharePoint](https://technet.microsoft.com/library/dn635309.aspx) nei servizi dell'infrastruttura di Azure.
