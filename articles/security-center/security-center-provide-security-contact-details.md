---
title: dettagli di contatto sicurezza aaaProvide nel Centro protezione di Azure | Documenti Microsoft
description: Questo documento viene illustrato come protezione tooprovide contattare i dettagli nel Centro protezione di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Specificare i dettagli dei contatti di sicurezza nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglierà di specificare i dettagli dei contatti di sicurezza per la sottoscrizione di Azure, se non è già stato fatto. Queste informazioni verranno utilizzate da Microsoft toocontact se hello Microsoft Security Response Center (MSRC) rileva che i dati sui clienti eseguiti da una parte non autorizzata o illegale. MSRC esegue un monitoraggio seleziona sicurezza di rete di Azure hello e dell'infrastruttura e riceve threat intelligence ed evitare eventuali abusi reclamo di terze parti.

Verrà inviata una notifica di posta elettronica hello prima giornaliero occorrenza di un avviso e solo per gli avvisi di livello di gravità elevato. Le preferenze di posta elettronica possono essere configurate solo per i criteri della sottoscrizione. I gruppi di risorse all'interno di una sottoscrizione ereditano queste impostazioni.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **fornire dettagli di contatto sicurezza**.
   ![Specificare contatti per la sicurezza][1]
2. Verrà aperto il pannello hello **fornire dettagli di contatto sicurezza**. Selezionare le informazioni di contatto tooprovide sottoscrizione di Azure di hello in.
   ![Specificare i dettagli dei contatti di sicurezza][2]
3. Viene visualizzato un altro pannello **Specificare i dettagli dei contatti di sicurezza** .

   * Immettere l'indirizzo di posta elettronica di contatto di hello sicurezza o gli indirizzi separati da virgole. Non è una limitazione del numero di indirizzi di posta elettronica che è possibile immettere toohello.
   * Immettere un numero di telefono internazionale per il contatto di sicurezza.
   * messaggi di posta elettronica tooreceive sugli avvisi di livello di gravità elevato, attivare l'opzione hello **invia messaggi di posta elettronica relative agli avvisi**.
   * In hello future, si avrà a disposizione i proprietari di toosubscription notifiche tramite posta elettronica toosend opzione hello. Attualmente questa opzione non è disponibile.
   * Selezionare **OK** sicurezza hello tooapply sottoscrizione tooyour informazioni di contatto.

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
