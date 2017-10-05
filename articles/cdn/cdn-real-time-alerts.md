---
title: Avvisi in tempo reale nella rete CDN di Azure | Documentazione Microsoft
description: Avvisi in tempo reale nella rete CDN di Microsoft Azure. Gli avvisi in tempo reale forniscono notifiche sulle prestazioni degli endpoint nel profilo della rete CDN.
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
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="2b343-104">Avvisi in tempo reale nella rete CDN di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2b343-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="2b343-105">Overview</span><span class="sxs-lookup"><span data-stu-id="2b343-105">Overview</span></span>
<span data-ttu-id="2b343-106">Questo documento illustra gli avvisi in tempo reale nella rete CDN di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b343-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="2b343-107">Questa funzionalità fornisce notifiche in tempo reale sulle prestazioni degli endpoint nel profilo della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="2b343-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="2b343-108">È possibile configurare avvisi HTTP o di posta elettronica in base a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2b343-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="2b343-109">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="2b343-109">Bandwidth</span></span>
* <span data-ttu-id="2b343-110">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="2b343-110">Status Codes</span></span>
* <span data-ttu-id="2b343-111">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="2b343-111">Cache Statuses</span></span>
* <span data-ttu-id="2b343-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="2b343-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="2b343-113">Creazione di un avviso in tempo reale</span><span class="sxs-lookup"><span data-stu-id="2b343-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="2b343-114">Nel [portale di Azure](https://portal.azure.com)passare al profilo della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="2b343-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="2b343-116">Dal pannello del profilo della rete CDN fare clic sul pulsante **Gestisci** .</span><span class="sxs-lookup"><span data-stu-id="2b343-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="2b343-118">Si aprirà il portale di gestione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="2b343-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="2b343-119">Passare il puntatore sulla scheda **Analytics** (Analisi) e quindi sul riquadro a comparsa **Real-Time Stats** (Statistiche in tempo reale).</span><span class="sxs-lookup"><span data-stu-id="2b343-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="2b343-120">Fare clic su **Real-Time Alerts**(Avvisi in tempo reale).</span><span class="sxs-lookup"><span data-stu-id="2b343-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="2b343-122">Verrà visualizzato l'elenco delle configurazioni di avviso esistenti (se presenti).</span><span class="sxs-lookup"><span data-stu-id="2b343-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="2b343-123">Fare clic sul pulsante **Add Alert** (Aggiungi avviso).</span><span class="sxs-lookup"><span data-stu-id="2b343-123">Click the **Add Alert** button.</span></span>
   
    ![Pulsante Add Alert (Aggiungi avviso)](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="2b343-125">Verrà visualizzato un form per la creazione di un nuovo avviso.</span><span class="sxs-lookup"><span data-stu-id="2b343-125">A form for creating a new alert is displayed.</span></span>
   
    ![Form New Alert (Nuovo avviso)](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="2b343-127">Per attivare l'avviso quando si fa clic su **Save** (Salva), selezionare la casella di controllo **Alert Enabled** (Avviso abilitato).</span><span class="sxs-lookup"><span data-stu-id="2b343-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="2b343-128">Immettere un nome descrittivo nel campo **Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="2b343-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="2b343-129">Nell'elenco a discesa **Media Type** (Tipo di supporto) selezionare **HTTP Large Object** (LOB HTTP).</span><span class="sxs-lookup"><span data-stu-id="2b343-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Tipo di supporto con LOB HTTP selezionato](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="2b343-131">È necessario selezionare **HTTP Large Object** (LOB HTTP) come **Media Type** (Tipo di supporto).</span><span class="sxs-lookup"><span data-stu-id="2b343-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="2b343-132">Le altre opzioni non vengono usate dalla **rete CDN di Azure di Verizon**.</span><span class="sxs-lookup"><span data-stu-id="2b343-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="2b343-133">Se non si seleziona **HTTP Large Object** (LOB HTTP), l'avviso non verrà mai attivato.</span><span class="sxs-lookup"><span data-stu-id="2b343-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="2b343-134">Per **Expression** (Espressione), creare un'espressione da monitorare selezionando valori per **Metric** (Metrica), **Operator** (Operatore) e **Trigger value** (Valore trigger).</span><span class="sxs-lookup"><span data-stu-id="2b343-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="2b343-135">Per **Metric**(Metrica), selezionare il tipo di condizione che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="2b343-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="2b343-136">**Bandwidth Mbps** (Mbps larghezza di banda) è la quantità di larghezza di banda utilizzata, misurata in megabit al secondo.</span><span class="sxs-lookup"><span data-stu-id="2b343-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="2b343-137">**Total Connections** (Connessioni totali) è il numero di connessioni HTTP simultanee ai server perimetrali.</span><span class="sxs-lookup"><span data-stu-id="2b343-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="2b343-138">Per informazioni sulle definizioni dei vari stati della cache e dei codici di stato, vedere [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Codici di stato della cache della rete CDN di Azure) e [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Codici di stato HTTP della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="2b343-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="2b343-139">**Operator** (Operatore) è l'operatore matematico che stabilisce la relazione tra la metrica e il valore trigger.</span><span class="sxs-lookup"><span data-stu-id="2b343-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="2b343-140">**Trigger Value** (Valore trigger) è il valore soglia da soddisfare perché venga inviata una notifica.</span><span class="sxs-lookup"><span data-stu-id="2b343-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="2b343-141">Nell'esempio seguente l'espressione creata indica che si vuole ricevere una notifica quando il numero di codici di stato 404 è maggiore di 25.</span><span class="sxs-lookup"><span data-stu-id="2b343-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Espressione di esempio di avviso in tempo reale](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="2b343-143">Per **Interval**(Intervallo), immettere la frequenza con cui l'espressione deve essere valutata.</span><span class="sxs-lookup"><span data-stu-id="2b343-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="2b343-144">Nell'elenco a discesa **Notify on** (Notifica per) selezionare per cosa si vuole ricevere una notifica quando l'espressione è true.</span><span class="sxs-lookup"><span data-stu-id="2b343-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="2b343-145">**Condition Start** (Inizio condizione) indica che verrà inviata una notifica la prima volta che viene rilevata la condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="2b343-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="2b343-146">**Condition End** (Fine condizione) indica che verrà inviata una notifica quando la condizione specificata non viene più rilevata.</span><span class="sxs-lookup"><span data-stu-id="2b343-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="2b343-147">Questa notifica può essere attivata solo dopo che il sistema di monitoraggio della rete ha rilevato che si è verificata la condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="2b343-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="2b343-148">**Continuous** (Continuo) indica che verrà inviata una notifica ogni volta che il sistema di monitoraggio della rete rileva la condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="2b343-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="2b343-149">Tenere presente che il sistema di monitoraggio della rete cerca la condizione specificata solo una volta per ogni intervallo.</span><span class="sxs-lookup"><span data-stu-id="2b343-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="2b343-150">**Condition Start and End** (Inizio e fine condizione) indica che verrà inviata una notifica la prima volta che viene rilevata la condizione specificata e ancora una volta quando la condizione non viene più rilevata.</span><span class="sxs-lookup"><span data-stu-id="2b343-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="2b343-151">Per ricevere le notifiche tramite posta elettronica, selezionare la casella di controllo **Notify by Email** (Notifica tramite posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="2b343-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Form per la notifica tramite posta elettronica](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="2b343-153">Nel campo **To** (A) immettere l'indirizzo di posta elettronica a cui devono essere inviate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="2b343-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="2b343-154">Per **Subject** (Oggetto) e **Body** (Corpo) è possibile lasciare i valori predefiniti oppure personalizzare il messaggio usando l'elenco **Available keywords** (Parole chiave disponibili) per inserire in modo dinamico i dati dell'avviso quando il messaggio viene inviato.</span><span class="sxs-lookup"><span data-stu-id="2b343-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2b343-155">Per testare la notifica tramite posta elettronica è possibile fare clic sul pulsante **Test Notification** (Notifica di prova), ma solo dopo aver salvato la configurazione degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="2b343-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="2b343-156">Per pubblicare le notifiche in un server Web, selezionare la casella di controllo **Notify by HTTP Post** (Notifica tramite HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="2b343-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Form per la notifica tramite HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="2b343-158">Nel campo **Url** immettere l'URL in cui deve essere pubblicato il messaggio HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b343-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="2b343-159">Nella casella di testo **Headers** (Intestazioni) immettere le intestazioni HTTP da inviare nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="2b343-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="2b343-160">Per **Body** (Corpo), è possibile personalizzare il messaggio usando l'elenco **Available keywords** (Parole chiave disponibili) per inserire in modo dinamico i dati dell'avviso quando il messaggio viene inviato.</span><span class="sxs-lookup"><span data-stu-id="2b343-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="2b343-161">L'impostazione predefinita per **Headers** (Intestazioni) e **Body** (Corpo) è un payload XML simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="2b343-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="2b343-162">Per testare la notifica tramite HTTP Post è possibile fare clic sul pulsante **Test Notification** (Notifica di prova), ma solo dopo aver salvato la configurazione degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="2b343-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="2b343-163">Fare clic sul pulsante **Save** (Salva) per salvare la configurazione degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="2b343-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="2b343-164">Se al passaggio 5 è stata selezionata l'opzione **Alert Enabled** (Avviso abilitato), ora l'avviso è attivo.</span><span class="sxs-lookup"><span data-stu-id="2b343-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b343-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b343-165">Next Steps</span></span>
* <span data-ttu-id="2b343-166">Vedere [Statistiche in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="2b343-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="2b343-167">Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="2b343-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="2b343-168">Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="2b343-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

