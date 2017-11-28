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
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="ef321-104">Avvisi in tempo reale nella rete CDN di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ef321-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="ef321-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ef321-105">Overview</span></span>
<span data-ttu-id="ef321-106">Questo documento illustra gli avvisi in tempo reale nella rete CDN di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ef321-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="ef321-107">Questa funzionalità fornisce notifiche in tempo reale sulle prestazioni di hello degli endpoint hello nel profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="ef321-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="ef321-108">È possibile configurare avvisi HTTP o di posta elettronica in base a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ef321-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="ef321-109">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="ef321-109">Bandwidth</span></span>
* <span data-ttu-id="ef321-110">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="ef321-110">Status Codes</span></span>
* <span data-ttu-id="ef321-111">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="ef321-111">Cache Statuses</span></span>
* <span data-ttu-id="ef321-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="ef321-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="ef321-113">Creazione di un avviso in tempo reale</span><span class="sxs-lookup"><span data-stu-id="ef321-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="ef321-114">In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="ef321-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="ef321-116">Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ef321-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="ef321-118">viene visualizzato il portale di gestione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="ef321-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="ef321-119">Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **statistiche in tempo reale** riquadro a comparsa.</span><span class="sxs-lookup"><span data-stu-id="ef321-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="ef321-120">Fare clic su **Real-Time Alerts**(Avvisi in tempo reale).</span><span class="sxs-lookup"><span data-stu-id="ef321-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="ef321-122">viene visualizzato l'elenco di Hello delle configurazioni di avviso esistente (se presente).</span><span class="sxs-lookup"><span data-stu-id="ef321-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="ef321-123">Fare clic su hello **Aggiungi avviso** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ef321-123">Click hello **Add Alert** button.</span></span>
   
    ![Pulsante Add Alert (Aggiungi avviso)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="ef321-125">Verrà visualizzato un form per la creazione di un nuovo avviso.</span><span class="sxs-lookup"><span data-stu-id="ef321-125">A form for creating a new alert is displayed.</span></span>
   
    ![Form New Alert (Nuovo avviso)](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="ef321-127">Se si desidera toobe questo avviso è attivo quando fa clic su **salvare**, controllare hello **avviso abilitato** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="ef321-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="ef321-128">Immettere un nome descrittivo per l'avviso in hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="ef321-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="ef321-129">In hello **Media Type** elenco a discesa Seleziona **HTTP LOB**.</span><span class="sxs-lookup"><span data-stu-id="ef321-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo di supporto con LOB HTTP selezionato](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="ef321-131">È necessario selezionare **HTTP LOB** come hello **tipo di supporto**.</span><span class="sxs-lookup"><span data-stu-id="ef321-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="ef321-132">Hello altre opzioni non vengono utilizzati da **rete CDN di Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="ef321-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="ef321-133">Errore tooselect **HTTP LOB** genererà l'avviso toonever attivato.</span><span class="sxs-lookup"><span data-stu-id="ef321-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="ef321-134">Creare un **espressione** toomonitor selezionando un **metrica**, **operatore**, e **attivare valore**.</span><span class="sxs-lookup"><span data-stu-id="ef321-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="ef321-135">Per **metrica**, selezionare il tipo di hello della condizione che si desidera monitorare.</span><span class="sxs-lookup"><span data-stu-id="ef321-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="ef321-136">**Mbps di larghezza di banda** hello quantità dell'utilizzo della larghezza di banda in megabit al secondo.</span><span class="sxs-lookup"><span data-stu-id="ef321-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="ef321-137">**Totale connessioni** è il numero di hello di tooour di connessioni simultanee HTTP server edge.</span><span class="sxs-lookup"><span data-stu-id="ef321-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="ef321-138">Le definizioni di hello vari stati di cache e i codici di stato, vedere [codici di stato della Cache della rete CDN di Azure](https://msdn.microsoft.com/library/mt759237.aspx) e [codici di stato HTTP della rete CDN di Azure](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef321-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="ef321-139">**Operatore** è l'operatore matematico hello che stabilisce una relazione di hello tra metrica hello e il valore trigger hello.</span><span class="sxs-lookup"><span data-stu-id="ef321-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="ef321-140">**Attivare valore** valore di soglia hello che devono essere soddisfatte prima che verrà inviata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ef321-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="ef321-141">In hello di esempio seguente, espressione hello che ho creato indica che desidera toobe una notifica quando il numero di hello dei codici di stato 404 è maggiore di 25.</span><span class="sxs-lookup"><span data-stu-id="ef321-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Espressione di esempio di avviso in tempo reale](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="ef321-143">Per **intervallo**, immettere la frequenza con cui si desidera che espressione hello valutata.</span><span class="sxs-lookup"><span data-stu-id="ef321-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="ef321-144">In hello **notificare** elenco a discesa, selezionare questa opzione quando si desidera toobe una notifica quando hello espressione è true.</span><span class="sxs-lookup"><span data-stu-id="ef321-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="ef321-145">**Condizione di avvio** indica che verrà inviata una notifica quando hello specificato è rilevata condizione.</span><span class="sxs-lookup"><span data-stu-id="ef321-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="ef321-146">**Condizione di fine** indica che verrà inviata una notifica quando hello specificato condizione non viene più rilevata.</span><span class="sxs-lookup"><span data-stu-id="ef321-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="ef321-147">Questa notifica può essere attivata solo dopo che il sistema di monitoraggio di rete ha rilevato che hello specificato insufficiente.</span><span class="sxs-lookup"><span data-stu-id="ef321-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="ef321-148">**Continua** indica che verrà inviata una notifica ogni volta che hello sistema di monitoraggio rete rileva hello specificato condizione.</span><span class="sxs-lookup"><span data-stu-id="ef321-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="ef321-149">Tenere presente che solo controllo una volta per ogni intervallo per hello la condizione specificata, verrà di sistema di monitoraggio della rete hello.</span><span class="sxs-lookup"><span data-stu-id="ef321-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="ef321-150">**Condizione iniziale e finale** indica che verrà inviata una notifica, hello prima volta che hello condizione specificata è stata rilevata e nuovamente quando la condizione hello non viene più rilevata.</span><span class="sxs-lookup"><span data-stu-id="ef321-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="ef321-151">Se si desidera tooreceive notifiche tramite posta elettronica, controllare hello **cui inviare la notifica tramite posta elettronica** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="ef321-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Form per la notifica tramite posta elettronica](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="ef321-153">In hello **a** immettere l'indirizzo di posta elettronica hello in cui si desidera delle notifiche inviate.</span><span class="sxs-lookup"><span data-stu-id="ef321-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="ef321-154">Per **soggetto** e **corpo**, è possibile lasciare l'impostazione predefinita hello o è possibile personalizzare il messaggio hello utilizzando hello **le parole chiave disponibili** toodynamically elenco inserire i dati di avviso quando il messaggio Hello viene inviato.</span><span class="sxs-lookup"><span data-stu-id="ef321-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ef321-155">È possibile testare la notifica di posta elettronica hello facendo hello **una notifica di prova** pulsante, ma solo dopo la configurazione degli avvisi hello è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="ef321-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="ef321-156">Se si desidera toobe notifiche registrato i server web tooa, controllare hello **notifica mediante HTTP Post** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="ef321-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Form per la notifica tramite HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="ef321-158">In hello **Url** immettere l'URL di hello in cui si desidera messaggio hello HTTP inviato.</span><span class="sxs-lookup"><span data-stu-id="ef321-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="ef321-159">In hello **intestazioni** casella di testo immettere toobe intestazioni HTTP hello inviato nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="ef321-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="ef321-160">Per **corpo** è possibile personalizzare il messaggio hello utilizzando hello **le parole chiave disponibili** toodynamically elenco inserire i dati di avviso quando viene inviato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="ef321-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="ef321-161">**Intestazioni** e **corpo** predefinito tooan toohello simile payload XML riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ef321-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="ef321-162">È possibile testare hello notifica HTTP Post facendo hello **una notifica di prova** pulsante, ma solo dopo la configurazione degli avvisi hello è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="ef321-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="ef321-163">Fare clic su hello **salvare** pulsante toosave la configurazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="ef321-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="ef321-164">Se al passaggio 5 è stata selezionata l'opzione **Alert Enabled** (Avviso abilitato), ora l'avviso è attivo.</span><span class="sxs-lookup"><span data-stu-id="ef321-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef321-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef321-165">Next Steps</span></span>
* <span data-ttu-id="ef321-166">Vedere [Statistiche in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="ef321-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="ef321-167">Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="ef321-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="ef321-168">Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="ef321-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

