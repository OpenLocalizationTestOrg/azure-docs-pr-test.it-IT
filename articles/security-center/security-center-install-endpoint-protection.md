---
title: aaaInstall Endpoint Protection in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * installare Endpoint Protection * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Installare Endpoint Protection nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia di installare Endpoint Protection nelle macchine virtuali di Azure se non è già abilitato. Questa indicazione si applica solo tooWindows macchine virtuali.

> [!NOTE]
> Questo esempio di distribuzione usa Microsoft Antimalware. Vedere [Integrazione di partner nel Centro sicurezza di Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) per un elenco di partner integrati con il Centro sicurezza.  
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questo argomento non costituisce una guida dettagliata.
>
>

1. In hello **indicazioni** pannello seleziona **installa Endpoint Protection**.
   ![Selezionare Installa Endpoint Protection][1]
2. Hello **installa Endpoint Protection** pannello verrà aperto un elenco di macchine virtuali senza la protezione di endpoint. Selezionare una delle hello elenco hello macchine virtuali che si vuole che tooinstall endpoint protection in e fare clic su **installare nelle macchine virtuali**.
   ![Selezionare le macchine virtuali tooinstall Endpoint Protection in][2]
3. Hello **selezionare Endpoint Protection** pannello apre tooallow si tooselect hello endpoint protection soluzione desiderata toouse. In questo esempio viene selezionato **Microsoft Antimalware**.
   ![Seleziona Endpoint Protection][3]
4. Ulteriori informazioni sulla soluzione di protezione endpoint hello viene visualizzate. Selezionare **Crea**.
   ![Creare una soluzione antimalware][4]
5. Immettere le impostazioni di configurazione necessarie hello hello **Aggiungi estensione** blade e quindi selezionare **OK**. toolearn informazioni sulle impostazioni di configurazione hello, vedere [predefiniti e personalizzati Antimalware configurazione](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) è ora attivo in hello selezionate le macchine virtuali.

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Installa Endpoint Protection". toolearn ulteriori informazioni su attivazione di Microsoft Antimalware in Azure, vedere hello seguente documento:

* [Microsoft Antimalware per servizi Cloud e macchine virtuali](../security/azure-security-antimalware.md) -informazioni su come toodeploy Microsoft Antimalware.

toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti documenti:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure criteri di sicurezza.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
