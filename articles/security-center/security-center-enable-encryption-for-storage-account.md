---
title: crittografia aaaEnable account di archiviazione nel Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * abilitare la crittografia per Azure Storage Account * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Abilitare la crittografia per l'account di archiviazione nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia all'utente di abilitare la crittografia del servizio di archiviazione di Azure per i dati inattivi.

Crittografia del servizio di archiviazione (SSE) funziona la crittografia dei dati di hello quando viene scritta tooAzure archiviazione e la decrittografia dei dati di hello prima del recupero.  SSE è attualmente disponibile solo per hello servizio Blob di Azure e può essere utilizzato per i BLOB in blocchi, BLOB di pagine e BLOB di aggiunta.  vedere, più toolearn [la crittografia del servizio di archiviazione per i dati inattivi](../storage/common/storage-service-encryption.md).


> [!Note]
> Dopo avere attivato la crittografia, vengono crittografati solo i nuovi dati. Qualsiasi BLOB esistente nell'account di archiviazione non viene crittografato. tooencrypt BLOB esistenti, vedere hello [domande frequenti di crittografia del servizio di archiviazione](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

La crittografia del servizio di archiviazione è supportata solo negli account di archiviazione di Gestione risorse. Gli account di archiviazione classici non sono attualmente supportati. hello toounderstand classico e modelli di distribuzione di gestione delle risorse, vedere [modelli di distribuzione Azure](../azure-classic-rm.md).

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questo argomento non costituisce una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **abilitare la crittografia per l'Account di archiviazione Azure**.
   ![Abilita la crittografia per l'account di archiviazione][1]
2. Hello **abilitare la crittografia di archiviazione** apre blade. Questo pannello sono elencati gli account di archiviazione di Azure hello in cui la crittografia di archiviazione è disabilitata. In questo esempio selezioniamo **storageacct1**.
   ![Abilita la crittografia di archiviazione][2]
3. Hello **crittografia** pannello **storageacct1** apre. Selezionare **Enabled**.
   ![Pannello di crittografia][3]
4. Selezionare **Salva**.

A questo punto è stata abilitata la crittografia di archiviazione per **storageacct1**.


## <a name="see-also"></a>Vedere anche
Questo documento ha illustrato come tooimplement hello Centro sicurezza PC indicazione "Abilita la crittografia per Account di archiviazione Azure." toolearn ulteriori informazioni su Azure la crittografia del servizio di archiviazione, vedere l'esempio hello:

* [Crittografia del servizio di archiviazione di Azure per dati inattivi](../storage/common/storage-service-encryption.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
