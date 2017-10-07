---
title: crittografia disco aaaApply nel Centro protezione di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * applicare crittografia disco * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Applicare la crittografia del disco nel Centro sicurezza Azure
Il Centro sicurezza di Azure suggerisce di applicare la crittografia dischi se sono presenti dischi di VM Windows o Linux che non vengono crittografati con Crittografia dischi di Azure. Crittografia dischi consente di crittografare i dischi delle VM IaaS Windows e Linux.  La crittografia è consigliabile per hello del sistema operativo e i volumi di dati di una macchina virtuale.

Crittografia dei dischi utilizza standard di settore hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funzionalità di Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funzionalità di Linux. Queste funzionalità forniscono del sistema operativo e toohelp crittografia dati proteggere e salvaguardare i dati e soddisfare le protezione dell'organizzazione e impegni di conformità. Crittografia del disco è integrata con [insieme credenziali chiavi Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia disco hello nella sottoscrizione di insieme di credenziali chiave, assicurando che tutti i dati in dischi di macchina virtuale hello vengono crittografati a riposo nel [ Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Crittografia disco Azure è supportata in hello seguenti sistemi operativi server Windows, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2. Crittografia del disco è supportata in hello seguenti sistemi operativi Linux server - alla Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES).
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **applicare la crittografia del disco**.
2. In hello **applicare la crittografia del disco** pannello viene visualizzato un elenco di macchine virtuali per cui è consigliabile crittografia del disco.
3. Seguire toothese di crittografia hello istruzioni tooapply macchine virtuali.

![][1]

tooencrypt macchine virtuali di Azure che sono stati identificati dal Centro sicurezza PC come crittografia, è consigliabile hello alla procedura seguente:

* Installare e configurare Azure PowerShell. In questo modo toorun hello PowerShell i comandi necessari tooset backup hello prerequisiti necessari tooencrypt macchine virtuali di Azure.
* Ottenere ed eseguire script di PowerShell Azure prerequisiti di Azure disco crittografia hello.
* Crittografare le macchine virtuali.

[Crittografare una macchina virtuale di Azure](security-center-disk-encryption.md) illustra la procedura.  In questo argomento si presuppone il che uso Windows 10 come computer client hello da cui è possibile configurare crittografia del disco.

È possibile usare diversi approcci per le macchine virtuali di Azure. Se si è già esperti in materia di Azure PowerShell o l'interfaccia CLI di Azure, è preferibile approcci alternativi toouse. toolearn su questi altri approcci, vedere [crittografia del disco di Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Vedere anche
Questo documento ha illustrato come tooimplement hello Centro sicurezza PC indicazione "Applica crittografia del disco." toolearn ulteriori informazioni su crittografia del disco, vedere l'esempio hello:

* [Gestione di crittografia e la chiave insieme di credenziali chiave di Azure](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) - informazioni su come il disco toouse la gestione della crittografia per le macchine virtuali IaaS insieme credenziali chiavi Azure toohelp proteggere e salvaguardare i dati.
* [Crittografare una macchina virtuale di Azure](security-center-disk-encryption.md) (documento), informazioni su come tooencrypt macchine virtuali di Azure.
* [Crittografia disco Azure](../security/azure-security-disk-encryption.md) (documento), informazioni su come tooenable disco crittografia per Windows e le macchine virtuali Linux.

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure criteri di sicurezza.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
