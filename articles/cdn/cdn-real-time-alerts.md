---
title: gli avvisi in tempo reale di CDN aaaAzure | Documenti Microsoft
description: Avvisi in tempo reale nella rete CDN di Microsoft Azure. Gli avvisi in tempo reale forniscono notifiche sulle prestazioni di hello degli endpoint hello nel profilo di rete CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Avvisi in tempo reale nella rete CDN di Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overview
Questo documento illustra gli avvisi in tempo reale nella rete CDN di Microsoft Azure. Questa funzionalità fornisce notifiche in tempo reale sulle prestazioni di hello degli endpoint hello nel profilo di rete CDN.  È possibile configurare avvisi HTTP o di posta elettronica in base a quanto segue:

* Larghezza di banda
* Codici di stato
* Stati della cache
* Connessioni

## <a name="creating-a-real-time-alert"></a>Creazione di un avviso in tempo reale
1. In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
3. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **statistiche in tempo reale** riquadro a comparsa.  Fare clic su **Real-Time Alerts**(Avvisi in tempo reale).
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    viene visualizzato l'elenco di Hello delle configurazioni di avviso esistente (se presente).
4. Fare clic su hello **Aggiungi avviso** pulsante.
   
    ![Pulsante Add Alert (Aggiungi avviso)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Verrà visualizzato un form per la creazione di un nuovo avviso.
   
    ![Form New Alert (Nuovo avviso)](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Se si desidera toobe questo avviso è attivo quando fa clic su **salvare**, controllare hello **avviso abilitato** casella di controllo.
6. Immettere un nome descrittivo per l'avviso in hello **nome** campo.
7. In hello **Media Type** elenco a discesa Seleziona **HTTP LOB**.
   
    ![Tipo di supporto con LOB HTTP selezionato](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > È necessario selezionare **HTTP LOB** come hello **tipo di supporto**.  Hello altre opzioni non vengono utilizzati da **rete CDN di Azure da Verizon**.  Errore tooselect **HTTP LOB** genererà l'avviso toonever attivato.
   > 
   > 
8. Creare un **espressione** toomonitor selezionando un **metrica**, **operatore**, e **attivare valore**.
   
   * Per **metrica**, selezionare il tipo di hello della condizione che si desidera monitorare.  **Mbps di larghezza di banda** hello quantità dell'utilizzo della larghezza di banda in megabit al secondo.  **Totale connessioni** è il numero di hello di tooour di connessioni simultanee HTTP server edge.  Le definizioni di hello vari stati di cache e i codici di stato, vedere [codici di stato della Cache della rete CDN di Azure](https://msdn.microsoft.com/library/mt759237.aspx) e [codici di stato HTTP della rete CDN di Azure](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Operatore** è l'operatore matematico hello che stabilisce una relazione di hello tra metrica hello e il valore trigger hello.
   * **Attivare valore** valore di soglia hello che devono essere soddisfatte prima che verrà inviata una notifica.
     
     In hello di esempio seguente, espressione hello che ho creato indica che desidera toobe una notifica quando il numero di hello dei codici di stato 404 è maggiore di 25.
     
     ![Espressione di esempio di avviso in tempo reale](./media/cdn-real-time-alerts/cdn-expression.png)
9. Per **intervallo**, immettere la frequenza con cui si desidera che espressione hello valutata.
10. In hello **notificare** elenco a discesa, selezionare questa opzione quando si desidera toobe una notifica quando hello espressione è true.
    
    * **Condizione di avvio** indica che verrà inviata una notifica quando hello specificato è rilevata condizione.
    * **Condizione di fine** indica che verrà inviata una notifica quando hello specificato condizione non viene più rilevata. Questa notifica può essere attivata solo dopo che il sistema di monitoraggio di rete ha rilevato che hello specificato insufficiente.
    * **Continua** indica che verrà inviata una notifica ogni volta che hello sistema di monitoraggio rete rileva hello specificato condizione. Tenere presente che solo controllo una volta per ogni intervallo per hello la condizione specificata, verrà di sistema di monitoraggio della rete hello.
    * **Condizione iniziale e finale** indica che verrà inviata una notifica, hello prima volta che hello condizione specificata è stata rilevata e nuovamente quando la condizione hello non viene più rilevata.
11. Se si desidera tooreceive notifiche tramite posta elettronica, controllare hello **cui inviare la notifica tramite posta elettronica** casella di controllo.  
    
    ![Form per la notifica tramite posta elettronica](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    In hello **a** immettere l'indirizzo di posta elettronica hello in cui si desidera delle notifiche inviate. Per **soggetto** e **corpo**, è possibile lasciare l'impostazione predefinita hello o è possibile personalizzare il messaggio hello utilizzando hello **le parole chiave disponibili** toodynamically elenco inserire i dati di avviso quando il messaggio Hello viene inviato.
    
    > [!NOTE]
    > È possibile testare la notifica di posta elettronica hello facendo hello **una notifica di prova** pulsante, ma solo dopo la configurazione degli avvisi hello è stato salvato.
    > 
    > 
12. Se si desidera toobe notifiche registrato i server web tooa, controllare hello **notifica mediante HTTP Post** casella di controllo.
    
    ![Form per la notifica tramite HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    In hello **Url** immettere l'URL di hello in cui si desidera messaggio hello HTTP inviato. In hello **intestazioni** casella di testo immettere toobe intestazioni HTTP hello inviato nella richiesta di hello.  Per **corpo** è possibile personalizzare il messaggio hello utilizzando hello **le parole chiave disponibili** toodynamically elenco inserire i dati di avviso quando viene inviato il messaggio hello.  **Intestazioni** e **corpo** predefinito tooan toohello simile payload XML riportato di seguito.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > È possibile testare hello notifica HTTP Post facendo hello **una notifica di prova** pulsante, ma solo dopo la configurazione degli avvisi hello è stato salvato.
    > 
    > 
13. Fare clic su hello **salvare** pulsante toosave la configurazione dell'avviso.  Se al passaggio 5 è stata selezionata l'opzione **Alert Enabled** (Avviso abilitato), ora l'avviso è attivo.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [Statistiche in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-stats.md)
* Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)
* Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)

