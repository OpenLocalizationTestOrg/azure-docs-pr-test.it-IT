---
title: 'Esempio di IoT di Azure MyDriving: Avvio rapido | Documentazione Microsoft'
description: "Introduzione a un'applicazione che è una dimostrazione completa di come tooarchitect un sistema IoT utilizzando Microsoft Azure, tra cui flusso Analitica, Machine Learning e hub eventi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="39532-103">Sistema IoT MyDriving: Avvio rapido</span><span class="sxs-lookup"><span data-stu-id="39532-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="39532-104">MyDriving è un sistema che illustra hello progettazione e implementazione di una tipica [Internet of Things](iot-suite-overview.md) soluzione (IoT) che raccoglie i dati di telemetria dai dispositivi, elabora i dati nel cloud hello e si applica l'apprendimento tooprovide una risposta adattiva.</span><span class="sxs-lookup"><span data-stu-id="39532-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="39532-105">dimostrazione di Hello registra i dati sulle visite Auto, utilizzando i dati dal telefono cellulare e un adattatore che raccoglie informazioni dal sistema di controllo dell'automobile.</span><span class="sxs-lookup"><span data-stu-id="39532-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="39532-106">Usa questi commenti e suggerimenti di dati tooprovide al proprio approccio Guida gli utenti tooother di confronto.</span><span class="sxs-lookup"><span data-stu-id="39532-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="39532-107">Hello reale MyDriving mira tooget per iniziare a creare la propria soluzione IoT.</span><span class="sxs-lookup"><span data-stu-id="39532-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="39532-108">Ma prima di esso, possibile iniziare a usarlo con hello MyDriving app stessa, come un membro del team utente test.</span><span class="sxs-lookup"><span data-stu-id="39532-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="39532-109">Ciò offre un'esperienza di app hello e sistema hello dietro come un consumer, prima di addentrarsi nell'architettura di hello.</span><span class="sxs-lookup"><span data-stu-id="39532-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="39532-110">Introduce anche tooHockeyApp, un modo sporadico della gestione delle distribuzioni di alfa e beta hello degli utenti tootest app.</span><span class="sxs-lookup"><span data-stu-id="39532-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="39532-111">Utilizzare l'esperienza per dispositivi mobili hello</span><span class="sxs-lookup"><span data-stu-id="39532-111">Use hello mobile experience</span></span>
<span data-ttu-id="39532-112">Se si dispone di un dispositivo Android, iOS o Windows 10, è possibile utilizzare app MyDriving hello.</span><span class="sxs-lookup"><span data-stu-id="39532-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="39532-113">Installazione di Android e Windows 10 Mobile</span><span class="sxs-lookup"><span data-stu-id="39532-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="39532-114">Nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="39532-114">On your device:</span></span>

1. <span data-ttu-id="39532-115">Consentire le app di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="39532-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="39532-116">Android: in **Impostazioni**,  > **Sicurezza**, consentire le app da **Origini sconosciute**.</span><span class="sxs-lookup"><span data-stu-id="39532-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="39532-117">Windows 10: in **Impostazioni** > , **Aggiornamenti** > **Per gli sviluppatori**, impostare **Modalità sviluppatore**.</span><span class="sxs-lookup"><span data-stu-id="39532-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="39532-118">Unirsi al team di test beta mediante l'iscrizione o l'accesso a [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="39532-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="39532-119">HockeyApp rende facile toodistribute prime versioni di utenti tootest app.</span><span class="sxs-lookup"><span data-stu-id="39532-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="39532-120">Se si usa Windows 10, è possibile utilizzare browser Edge hello.</span><span class="sxs-lookup"><span data-stu-id="39532-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="39532-121">Se fosse un partecipante di compilazione 2016, accedi hello stesso posta elettronica dell'account Microsoft che è registrato per la conferenza hello, utilizzando uno dei pulsanti Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="39532-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="39532-122">L'iscrizione a HockeyApp è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="39532-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Schermata di accesso di HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="39532-124">Scaricare e installare l'applicazione hello da qui:</span><span class="sxs-lookup"><span data-stu-id="39532-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="39532-125">Android</span><span class="sxs-lookup"><span data-stu-id="39532-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="39532-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="39532-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="39532-127">Sono disponibili due elementi.</span><span class="sxs-lookup"><span data-stu-id="39532-127">There are two items.</span></span> <span data-ttu-id="39532-128">Installare il certificato di hello in **persone attendibili**.</span><span class="sxs-lookup"><span data-stu-id="39532-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="39532-129">Installare quindi l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="39532-129">Then install hello app.</span></span>

<span data-ttu-id="39532-130">*Eventuali problemi di avvio applicazione hello in Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="39532-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="39532-131">Il telefono potrebbe non essere aggiornato alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="39532-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="39532-132">Assicurarsi di aver ottenuto gli aggiornamenti più recenti di hello, o installare:</span><span class="sxs-lookup"><span data-stu-id="39532-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="39532-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="39532-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="39532-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="39532-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="39532-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="39532-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="39532-136">Installazione di iOS</span><span class="sxs-lookup"><span data-stu-id="39532-136">iOS installation</span></span>
<span data-ttu-id="39532-137">Se si è partecipato compilazione 2016, scaricare l'applicazione hello come membro del team di test in HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="39532-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="39532-138">Nel dispositivo iOS accedere troppo[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="39532-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="39532-139">Utilizzare uno dei pulsanti di accesso Microsoft hello e Accedi con hello stesso posta elettronica dell'account Microsoft che è stato registrato con conferenza hello.</span><span class="sxs-lookup"><span data-stu-id="39532-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="39532-140">(Non usare i campi di posta elettronica e password hello).</span><span class="sxs-lookup"><span data-stu-id="39532-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Schermata di accesso di HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="39532-142">Nel dashboard HockeyApp hello, selezionare MyDriving e scaricarlo.</span><span class="sxs-lookup"><span data-stu-id="39532-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="39532-143">Autorizzare versione beta di hello da HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="39532-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="39532-144">a.</span><span class="sxs-lookup"><span data-stu-id="39532-144">a.</span></span> <span data-ttu-id="39532-145">Andare troppo**impostazioni** > **generale** > **profili e la gestione dei dispositivi.**</span><span class="sxs-lookup"><span data-stu-id="39532-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="39532-146">b.</span><span class="sxs-lookup"><span data-stu-id="39532-146">b.</span></span> <span data-ttu-id="39532-147">Trust hello **Bit stadio GmbH** certificato.</span><span class="sxs-lookup"><span data-stu-id="39532-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="39532-148">Se non viene risolto compilazione 2016, è possibile compilare e distribuire app hello manualmente:</span><span class="sxs-lookup"><span data-stu-id="39532-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="39532-149">Scaricare codice hello [da GitHub].</span><span class="sxs-lookup"><span data-stu-id="39532-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="39532-150">Compilare e distribuire l'app [con Xamarin].</span><span class="sxs-lookup"><span data-stu-id="39532-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="39532-151">Informazioni su altre in hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="39532-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="39532-152">Ottenere un adattatore OBD (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="39532-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="39532-153">Questo aspetto è parte di hello che rende questa un reale sistema Internet of Things!</span><span class="sxs-lookup"><span data-stu-id="39532-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="39532-154">È possibile utilizzare l'applicazione hello senza uno, ma è più divertente reali hello e non sono costosi.</span><span class="sxs-lookup"><span data-stu-id="39532-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="39532-155">Sistemi diagnostici (OBD) sono una funzionalità hello di un'automobile che hello garage utilizza tootune backup Auto e diagnosticare rumori dispari e spie.</span><span class="sxs-lookup"><span data-stu-id="39532-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="39532-156">A meno che la macchina è di grande antichità, sono disponibili un socket in un punto qualsiasi in cabine hello, in genere dietro flap in dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="39532-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="39532-157">Con connettore di destra hello, è possibile ottenere le metriche delle prestazioni del motore di hello e apportare alcune modifiche.</span><span class="sxs-lookup"><span data-stu-id="39532-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="39532-158">È possibile acquistare un connettore OBD economici da posizioni di solito hello.</span><span class="sxs-lookup"><span data-stu-id="39532-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="39532-159">Si connette tramite Bluetooth o Wi-Fi app tooan sul telefono.</span><span class="sxs-lookup"><span data-stu-id="39532-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="39532-160">In questo caso, verrà tooconnect cloud toohello Auto.</span><span class="sxs-lookup"><span data-stu-id="39532-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="39532-161">connessione diretta di Hello da hello OBD è tooyour telefono, ma l'app funziona come un relè.</span><span class="sxs-lookup"><span data-stu-id="39532-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="39532-162">Dati di telemetria dell'automobile viene inviato retta toohello MyDriving IoT hub, in cui è elaborato toolog i viaggi e valutare il proprio stile di Guida.</span><span class="sxs-lookup"><span data-stu-id="39532-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="39532-163">un dispositivo OBD tooconnect:</span><span class="sxs-lookup"><span data-stu-id="39532-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="39532-164">Verificare che il veicolo abbia una presa OBD.</span><span class="sxs-lookup"><span data-stu-id="39532-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="39532-165">Ottenere un adattatore OBD:</span><span class="sxs-lookup"><span data-stu-id="39532-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="39532-166">Se si usa un telefono Android o Windows, è necessario un adattatore OBD II abilitato per Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="39532-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="39532-167">In questo caso, è stato usato [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="39532-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="39532-168">Se si usa un telefono iOS, è necessario un adattatore OBD abilitato per Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="39532-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="39532-169">In questo caso, è stato usato [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span><span class="sxs-lookup"><span data-stu-id="39532-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="39532-170">Seguire le istruzioni di hello forniti con il tooconnect adapter OBD è tooyour phone.</span><span class="sxs-lookup"><span data-stu-id="39532-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="39532-171">Tenere presente hello segue:</span><span class="sxs-lookup"><span data-stu-id="39532-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="39532-172">Una scheda Bluetooth deve essere abbinata a telefono hello hello **impostazioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="39532-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="39532-173">Un adapter Wi-Fi deve avere un indirizzo in 192.168.xxx.xxx intervallo hello.</span><span class="sxs-lookup"><span data-stu-id="39532-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="39532-174">Se si hanno diverse automobili, è possibile usare un adattatore distinto per ogni macchina (per un massimo di 3).</span><span class="sxs-lookup"><span data-stu-id="39532-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="39532-175">Se non si dispone di un adapter OBD, hello app invierà ancora percorso e dati sulla velocità dal nuovo toohello di ricevitore GPS del telefono hello terminano e verranno richiesto se si desidera un OBD toosimulate.</span><span class="sxs-lookup"><span data-stu-id="39532-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="39532-176">È possibile trovare informazioni sull'utilizzo di dati dalla scheda OBD hello app hello e sulle opzioni per creare il proprio dispositivo OBD nella sezione 2.1, "Dispositivi IoT" in hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="39532-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="39532-177">Utilizzare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="39532-177">Use hello app</span></span>
<span data-ttu-id="39532-178">Avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="39532-178">Start hello app.</span></span> <span data-ttu-id="39532-179">È presente un iniziale toowalk Guida introduttiva illustra il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="39532-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="39532-180">Tenere traccia dei viaggi.</span><span class="sxs-lookup"><span data-stu-id="39532-180">Track your trips</span></span>
<span data-ttu-id="39532-181">Toccare hello pulsante record (big cerchio rosso in basso hello hello) toostart un andata e ritorno e nuovamente tooend.</span><span class="sxs-lookup"><span data-stu-id="39532-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Illustrazione del pulsante di hello record di rilevamento di andata e ritorno](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="39532-183">Ogni volta che si avvia un andata e ritorno, se è presente alcun dispositivo OBD, verrà chiesto se si desidera che il simulatore di hello toouse.</span><span class="sxs-lookup"><span data-stu-id="39532-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="39532-184">Alla fine hello un andata e ritorno, toccare hello stop e sarà visualizzato un riepilogo.</span><span class="sxs-lookup"><span data-stu-id="39532-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Esempio di riepilogo di un viaggio](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="39532-186">Esaminare i viaggi</span><span class="sxs-lookup"><span data-stu-id="39532-186">Review your trips</span></span>
![Esempio di una viaggio precedente](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="39532-188">Esaminare il profilo</span><span class="sxs-lookup"><span data-stu-id="39532-188">Review your profile</span></span>
![Esempio di un profilo dello stile di guida](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="39532-190">Inviateci i commenti e suggerimenti sul test</span><span class="sxs-lookup"><span data-stu-id="39532-190">Send us your test feedback</span></span>
<span data-ttu-id="39532-191">Perché abbiamo creato MyDriving toohelp iniziare subito a usare i propri sistemi IoT, si desidera certamente toohear da parte dell'utente, sulle modalità di funzionamento.</span><span class="sxs-lookup"><span data-stu-id="39532-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="39532-192">Indicare se:</span><span class="sxs-lookup"><span data-stu-id="39532-192">Let us know if:</span></span>

* <span data-ttu-id="39532-193">Si sono riscontrate difficoltà o problematiche.</span><span class="sxs-lookup"><span data-stu-id="39532-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="39532-194">C'è un punto di estensione che potrebbe renderlo scenario tooyour più adatto.</span><span class="sxs-lookup"><span data-stu-id="39532-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="39532-195">Trovare un tooaccomplish modo più efficiente determinate esigenze.</span><span class="sxs-lookup"><span data-stu-id="39532-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="39532-196">Si hanno altri suggerimenti per migliorare MyDriving o questa documentazione.</span><span class="sxs-lookup"><span data-stu-id="39532-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="39532-197">All'interno di hello MyDriving app, è possibile utilizzare il meccanismo di feedback hello incorporato HockeyApp: in iOS e Android, è sufficiente specificare il telefono un agitazione oppure utilizzare hello **Feedback** comando di menu.</span><span class="sxs-lookup"><span data-stu-id="39532-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="39532-198">In questo modo viene applicato automaticamente uno screenshot in modo che il destinatario sappia di cosa si sta parlando.</span><span class="sxs-lookup"><span data-stu-id="39532-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="39532-199">E se sono presenti eventuali ingrato arresti anomali del sistema, HockeyApp raccoglie tootell i registri di arresto anomalo del sistema hello ci su di essi.</span><span class="sxs-lookup"><span data-stu-id="39532-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="39532-200">È inoltre possibile assegnare i commenti e suggerimenti tramite hello [portale HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="39532-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="39532-201">È anche possibile registrare un [problema in GitHub] o lasciare un commento qui di seguito (versione en-us).</span><span class="sxs-lookup"><span data-stu-id="39532-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="39532-202">Saremo lieti toohearing da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="39532-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="39532-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39532-203">Next steps</span></span>
* <span data-ttu-id="39532-204">Esplorare hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs) toounderstand come è stato progettato e costruito hello intero sistema MyDriving.</span><span class="sxs-lookup"><span data-stu-id="39532-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="39532-205">[Creare e distribuire un sistema personalizzato](iot-solution-build-system.md) con gli script di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39532-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="39532-206">Hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs) anche in modo semplificato le aree in cui ti hello la maggior parte delle personalizzazioni.</span><span class="sxs-lookup"><span data-stu-id="39532-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[da GitHub]: https://github.com/Azure-Samples/MyDriving
[con Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[portale HockeyApp]: https://rink.hockeyapp.org
[problema in GitHub]: https://github.com/Azure-Samples/MyDriving/issues
