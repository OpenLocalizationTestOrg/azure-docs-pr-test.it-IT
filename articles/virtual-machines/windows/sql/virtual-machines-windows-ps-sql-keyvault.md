---
title: aaaIntegrate insieme di credenziali di chiave con SQL Server in macchine virtuali di Windows in Azure (gestione delle risorse) | Documenti Microsoft
description: Informazioni su come tooautomate hello configurazione di crittografia di SQL Server per l'utilizzo con l'insieme di credenziali chiave di Azure. In questo argomento viene illustrato come toouse integrazione dell'insieme di credenziali chiave di Azure con le macchine virtuali di SQL Server creato con Gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestione risorse](virtual-machines-windows-ps-sql-keyvault.md)
> * [Classico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Panoramica
Esistono più funzionalità di crittografia di SQL Server, ad esempio [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [crittografia a livello di colonna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) e [crittografia di backup](https://msdn.microsoft.com/library/dn449489.aspx). I moduli di crittografia occorre toomanage e archiviano le chiavi di crittografia hello che è utilizzare per la crittografia. Hello servizio insieme di credenziali chiave di Azure (insieme) è progettata tooimprove hello sicurezza e la gestione di queste chiavi in una posizione sicura e altamente disponibile. Hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) consente di SQL Server toouse queste chiavi dall'insieme di credenziali chiave di Azure.

Se si esegue SQL Server locale dei computer, vi sono [è possibile attenersi alla procedura tooaccess insieme credenziali chiavi Azure dal computer di SQL Server on-premise](https://msdn.microsoft.com/library/dn198405.aspx). Ma per SQL Server in macchine virtuali di Azure, è possibile risparmiare tempo utilizzando hello *integrazione dell'insieme di credenziali chiave di Azure* funzionalità.

Quando questa funzionalità è abilitata, automaticamente installa hello connettore SQL Server, configura hello EKM provider tooaccess insieme credenziali chiavi Azure e crea hello credenziali tooallow si tooaccess l'insieme di credenziali. Se è stato esaminato passaggi hello hello indicato in precedenza documentazione locale, è possibile vedere che questa funzionalità consente di automatizzare i passaggi 2 e 3. Hello è comunque necessario toodo manualmente è chiavi e l'insieme di credenziali chiave hello toocreate. Da qui, hello intero il programma di installazione della VM SQL è automatizzato. Quando questa funzionalità viene completato il programma di installazione, è possibile eseguire toobegin istruzioni T-SQL la crittografia del database o backup in modo analogo.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Abilitazione e configurazione dell'integrazione di AKV
È possibile abilitare l'integrazione di AKV durante il provisioning oppure configurarlo per VM esistenti.

### <a name="new-vms"></a>Nuove VM
Se si esegue il provisioning di una nuova macchina virtuale con Gestione risorse di SQL Server, hello portale di Azure fornisce un tooenable passaggio integrazione insieme credenziali chiavi Azure. Hello insieme credenziali chiavi Azure funzionalità è disponibile solo per hello Enterprise, Developer ed Evaluation Edition di SQL Server.

![Integrazione dell'insieme di credenziali delle chiavi di Azure per SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Per una procedura dettagliata di provisioning, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VM esistenti
Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server. Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.

![Integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello sezione integrazione automatizzata insieme di credenziali chiave.

![Configurare l'integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.

> [!NOTE]
> È inoltre possibile configurare l'integrazione di AKV mediante un modello. Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'integrazione dell'insieme di credenziali delle chiavi di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

