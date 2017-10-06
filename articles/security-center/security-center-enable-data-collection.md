---
title: raccolta di dati aaaEnable in Centro sicurezza di Azure | Documenti Microsoft
description: " Informazioni su come raccolta di dati tooenable in Centro sicurezza di Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Abilitare la raccolta dati nel Centro sicurezza di Azure

> [!NOTE]
> A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. vedere, più toolearn [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md). informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>
>

Centro sicurezza PC raccoglie i dati da tooassess le macchine virtuali (VM) lo stato di protezione, fornire consigli sulla sicurezza e ricevere un avviso toothreats. Quando si accede a Centro sicurezza PC, è necessario hello opzione tooenable la raccolta dei dati per tutte le macchine virtuali nella sottoscrizione. Se la raccolta dei dati non è abilitata, il Centro sicurezza PC consiglia di attivare la raccolta dei dati nei criteri di sicurezza hello per la sottoscrizione.

Quando è abilitata la raccolta dei dati, è supportato Centro sicurezza PC disposizioni hello Microsoft Monitoring Agent in tutte le macchine virtuali di Azure e quelli nuovi creati. esegue l'analisi Hello Microsoft Monitoring Agent per diverse configurazioni di sicurezza. Inoltre, sistema operativo hello genera eventi del registro eventi. Esempi di tali dati sono: tipo e versione del sistema operativo, log del sistema operativo (registri eventi di Windows), processi in esecuzione, nome computer, indirizzi IP, utente connesso e ID tenant. Microsoft Monitoring Agent Hello legge le configurazioni e voci del registro eventi e copia hello dati tooyour dell'area di lavoro per l'analisi. Microsoft Monitoring Agent Hello copia area tooyour file dump di arresto anomalo del sistema.

Se si utilizza livello gratuito di hello del Centro sicurezza PC, è possibile disabilitare la raccolta dei dati dalle macchine virtuali disattivando la raccolta dei dati nei criteri di sicurezza hello. La disabilitazione della raccolta dati consente di limitare le valutazioni relative alla sicurezza per le macchine virtuali. vedere, più toolearn [la disabilitazione della raccolta dati](#disabling-data-collection). Gli snapshot dei dischi delle macchine virtuali e la raccolta di elementi resteranno abilitati anche se la raccolta dati è stata disabilitata. Raccolta dati è obbligatorio per le sottoscrizioni nel livello Standard di hello del Centro sicurezza PC.

> [!NOTE]
> Per altre informazioni vedere i [piani tariffari](security-center-pricing.md) gratuito e standard del Centro sicurezza.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questo argomento non costituisce una guida dettagliata.
>
>

1. In hello **indicazioni** pannello seleziona **Abilita raccolta dati per le sottoscrizioni**.  Verrà visualizzata hello **attivare la raccolta di dati** blade.
   ![Pannello Raccomandazioni][2]
2. In hello **attivare la raccolta di dati** pannello, selezionare la sottoscrizione. Hello **criteri di sicurezza** apre pannello per la sottoscrizione.
3. In hello **criteri di sicurezza** pannello seleziona **su** in **la raccolta dei dati** tooautomatically raccogliere i log. Accensione di hello disposizioni di raccolta dati il monitoraggio di estensione su tutti correnti e nuovi supportate macchine virtuali nella sottoscrizione hello.
4. Selezionare **Salva**.
5. Selezionare **OK**.

## <a name="disabling-data-collection"></a>Disabilitazione della raccolta dati
Se si utilizza livello gratuito di hello del Centro sicurezza PC, è possibile disabilitare la raccolta dei dati dalle macchine virtuali in qualsiasi momento disattivando la raccolta dei dati nei criteri di sicurezza hello. Raccolta dati è obbligatorio per le sottoscrizioni nel livello Standard di hello del Centro sicurezza PC.

1. Restituire toohello **Centro sicurezza PC** pannello e seleziona hello **criteri** riquadro. Verrà visualizzata hello **sicurezza criteri: consente di definire criteri per ogni sottoscrizione** blade.
   ![Riquadro Criteri selezionare hello][5]
2. In hello **sicurezza criteri: consente di definire criteri per ogni sottoscrizione** blade, sottoscrizione selezionare hello che si desidera toodisable la raccolta dei dati.
3. Hello **criteri di sicurezza** apre pannello per la sottoscrizione.  Selezionare **No** in Raccolta di dati.
4. Selezionare **salvare** nella barra multifunzione superiore hello.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "Abilita la raccolta dati." toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
- [Sicurezza dei dati nel Centro sicurezza di Azure](security-center-data-security.md): informazioni sulla gestione e la protezione dei dati nel Centro sicurezza.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
