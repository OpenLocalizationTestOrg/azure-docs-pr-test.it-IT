---
title: aaaGet avviato con gli hub di notifica di Azure utilizzando Baidu | Documenti Microsoft
description: "In questa esercitazione, è illustrato come toouse gli hub di notifica di Azure toopush notifiche tooAndroid i dispositivi con Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="44b54-103">Introduzione ad Hub di notifica tramite Baidu</span><span class="sxs-lookup"><span data-stu-id="44b54-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="44b54-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="44b54-104">Overview</span></span>
<span data-ttu-id="44b54-105">Push cloud Baidu è un servizio cloud cinese, che è possibile utilizzare i dispositivi toomobile di notifiche push toosend.</span><span class="sxs-lookup"><span data-stu-id="44b54-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="44b54-106">Questo servizio è utile in Cina, in cui il recapito delle notifiche push tooAndroid è complesso a causa di presenza di hello di diverse app Store e di push dei servizi, inoltre toohello disponibilità dei dispositivi Android che non sono in genere connessi tooGCM (Google Il cloud di messaggistica).</span><span class="sxs-lookup"><span data-stu-id="44b54-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44b54-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="44b54-107">Prerequisites</span></span>
<span data-ttu-id="44b54-108">Questa esercitazione richiede:</span><span class="sxs-lookup"><span data-stu-id="44b54-108">This tutorial requires:</span></span>

* <span data-ttu-id="44b54-109">Android SDK (si presuppone che si usa Eclipse), che è possibile scaricare da hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sito Android</a></span><span class="sxs-lookup"><span data-stu-id="44b54-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="44b54-110">[Mobile Services Android SDK]</span><span class="sxs-lookup"><span data-stu-id="44b54-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="44b54-111">[Baidu Push Android SDK]</span><span class="sxs-lookup"><span data-stu-id="44b54-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="44b54-112">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="44b54-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="44b54-113">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="44b54-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="44b54-114">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="44b54-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="44b54-115">Creare un account Baidu</span><span class="sxs-lookup"><span data-stu-id="44b54-115">Create a Baidu account</span></span>
<span data-ttu-id="44b54-116">toouse Baidu, è necessario disporre di un account Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="44b54-117">Se si dispone già di uno, accedi toohello [Baidu portale] e ignorare il passaggio successivo toohello.</span><span class="sxs-lookup"><span data-stu-id="44b54-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="44b54-118">In caso contrario, vedere hello attenendosi alle istruzioni su come toocreate un account Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="44b54-119">Passare toohello [Baidu portale] e fare clic su hello**登录**(**accesso**) collegamento.</span><span class="sxs-lookup"><span data-stu-id="44b54-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="44b54-120">Fare clic su**立即注册**processo di registrazione account toostart hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="44b54-121">Immettere i dettagli necessario hello, telefono o posta elettronica indirizzo e la password e verifica del codice, fare clic su **iscrizione**.</span><span class="sxs-lookup"><span data-stu-id="44b54-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="44b54-122">Si riceverà un indirizzo di posta elettronica toohello di posta elettronica immesso con un collegamento di tooactivate account Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="44b54-123">Accedi tooyour account di posta elettronica, posta elettronica di attivazione Baidu hello scegliere hello attivazione collegamento tooactivate account Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="44b54-124">Dopo aver creato un account Baidu attivato, accedi toohello [Baidu portale].</span><span class="sxs-lookup"><span data-stu-id="44b54-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="44b54-125">Registrarsi come sviluppatore Baidu</span><span class="sxs-lookup"><span data-stu-id="44b54-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="44b54-126">Dopo aver eseguito l'accesso in toohello [Baidu portale], fare clic su**更多 >>** (**più**).</span><span class="sxs-lookup"><span data-stu-id="44b54-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="44b54-127">Scorrere verso il basso hello**站长与开发者服务 (Webmaster e servizi per sviluppatori)** sezione e fare clic su**百度开放云平台**(**Baidu aprire piattaforma cloud**).</span><span class="sxs-lookup"><span data-stu-id="44b54-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="44b54-128">Nella pagina successiva di hello, fare clic su**开发者服务**(**servizi per sviluppatori**) nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="44b54-129">Nella pagina successiva di hello, fare clic su**注册开发者**(**gli sviluppatori registrati**) dal menu di hello nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="44b54-130">Immettere il nome, una descrizione e un numero di cellulare per ricevere un messaggio di testo di verifica e quindi fare clic su **送验证码** (**Invia codice di verifica**).</span><span class="sxs-lookup"><span data-stu-id="44b54-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="44b54-131">Per i numeri di telefono internazionale, è necessario codice paese di hello tooenclose tra parentesi.</span><span class="sxs-lookup"><span data-stu-id="44b54-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="44b54-132">Per un numero degli Stati Uniti, usare ad esempio **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="44b54-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="44b54-133">Dovrebbe venire visualizzato un messaggio di testo con un numero di verifica, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="44b54-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="44b54-134">Immettere il numero di verifica hello dal messaggio hello in**验证码**(**codice di conferma**).</span><span class="sxs-lookup"><span data-stu-id="44b54-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="44b54-135">Infine, completare la registrazione per sviluppatori di hello accettazione hello Baidu contratto e facendo clic su**提交**(**Invia**).</span><span class="sxs-lookup"><span data-stu-id="44b54-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="44b54-136">Verrà visualizzato hello dopo il corretto completamento della registrazione:</span><span class="sxs-lookup"><span data-stu-id="44b54-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="44b54-137">Creare un progetto di Baidu cloud push</span><span class="sxs-lookup"><span data-stu-id="44b54-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="44b54-138">Quando si crea un progetto di Baidu cloud push, si ricevono l'ID dell'app, la chiave API e la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="44b54-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="44b54-139">Dopo aver eseguito l'accesso in toohello [Baidu portale], fare clic su**更多 >>** (**più**).</span><span class="sxs-lookup"><span data-stu-id="44b54-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="44b54-140">Scorrere verso il basso hello**站长与开发者服务**(**Webmaster e servizi per sviluppatori**) sezione e fare clic su**百度开放云平台**(**Baidu aprire piattaforma cloud**).</span><span class="sxs-lookup"><span data-stu-id="44b54-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="44b54-141">Nella pagina successiva di hello, fare clic su**开发者服务**(**servizi per sviluppatori**) nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="44b54-142">Nella pagina successiva di hello, fare clic su**云推送**(**Push Cloud**) da hello**云服务**(**servizi Cloud**) sezione.</span><span class="sxs-lookup"><span data-stu-id="44b54-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="44b54-143">Una volta registrati gli sviluppatori, vedere**管理控制台**(**Console di gestione**) nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="44b54-144">Fare clic su **开发者服务管理** (**Gestione dei servizi per sviluppatori**).</span><span class="sxs-lookup"><span data-stu-id="44b54-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="44b54-145">Nella pagina successiva di hello, fare clic su**创建工程**(**Crea progetto**).</span><span class="sxs-lookup"><span data-stu-id="44b54-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="44b54-146">Immettere un nome di applicazione e fare clic su **创建** (**Crea**).</span><span class="sxs-lookup"><span data-stu-id="44b54-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="44b54-147">Al termine della creazione di un progetto push cloud Baidu viene visualizzata una pagina con l'**AppID**, la **chiave API** e la **chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="44b54-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="44b54-148">Prendere nota della chiave API hello e una chiave privata, che verrà utilizzato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="44b54-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="44b54-149">Configurare il progetto hello per le notifiche push facendo**云推送**(**Push Cloud**) nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="44b54-150">Nella pagina successiva di hello, fare clic su hello**推送设置**(**Push impostazioni**) pulsante.</span><span class="sxs-lookup"><span data-stu-id="44b54-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="44b54-151">Nella pagina di configurazione hello, aggiungere il nome del pacchetto hello che verrà utilizzato nel progetto Android in hello**应用包名**(**pacchetto di applicazione**), campo e quindi fare clic su**保存设置**( **Salvare**).</span><span class="sxs-lookup"><span data-stu-id="44b54-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="44b54-152">Vedrai hello**保存成功!** (**Salvataggio completato**).</span><span class="sxs-lookup"><span data-stu-id="44b54-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="44b54-153">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="44b54-153">Configure your notification hub</span></span>
1. <span data-ttu-id="44b54-154">Accedi toohello [portale di Azure classico], quindi fare clic su **+ nuovo** in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="44b54-155">Fare clic su **Servizi app**, **Bus di servizio**, **Hub di notifica** e infine su **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="44b54-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="44b54-156">Specificare un nome per il **Hub di notifica**selezionare hello **area** hello e **Namespace** questo hub di notifica in cui verrà creato e quindi fare clic su  **Creare un nuovo Hub di notifica**.</span><span class="sxs-lookup"><span data-stu-id="44b54-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="44b54-157">Fare clic su spazio dei nomi hello in cui è stato creato l'hub di notifica e quindi fare clic su **gli hub di notifica** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="44b54-158">Hub di notifica selezionare hello è creato e quindi fare clic su **configura** menu principale di hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="44b54-159">Scorrere verso il basso toohello **le impostazioni di notifica baidu** sezione e immettere la chiave API hello e una chiave privata che è stato ottenuto da console Baidu hello in precedenza per il progetto di push cloud Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="44b54-160">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="44b54-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="44b54-161">Fare clic su hello **Dashboard** scheda nella parte superiore di hello hub di notifica hello e quindi fare clic su **Visualizza stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="44b54-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="44b54-162">Prendere nota di hello **DefaultListenSharedAccessSignature** e **DefaultFullSharedAccessSignature** da hello **accedere alle informazioni di connessione** finestra.</span><span class="sxs-lookup"><span data-stu-id="44b54-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="44b54-163">Connettere l'hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="44b54-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="44b54-164">Nel plug-in Eclipse ADT creare un nuovo progetto Android selezionando **File** > **New (Nuovo)**  > **Android Application Project (Progetto applicazione Android)** .</span><span class="sxs-lookup"><span data-stu-id="44b54-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="44b54-165">Immettere un **nome applicazione** e assicurarsi che hello **minimo richiesto SDK** versione è stata impostata troppo**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="44b54-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="44b54-166">Fare clic su **Avanti** e continuare seguendo la procedura guidata hello finché hello **creare attività** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="44b54-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="44b54-167">Assicurarsi che **attività vuota** sia selezionata, infine selezionare **fine** toocreate una nuova applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="44b54-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="44b54-168">Verificare che tale hello **destinazione di compilazione progetto** sia impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="44b54-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="44b54-169">Scaricare il file di notifica-hub-0.4.jar hello da hello **file** scheda di hello [notifica-hub-Android-SDK in Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="44b54-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="44b54-170">Aggiungere toohello file hello **librerie** cartella del progetto Eclipse e aggiornamento hello *librerie* cartella.</span><span class="sxs-lookup"><span data-stu-id="44b54-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="44b54-171">Scaricare e decomprimere hello [Baidu Push Android SDK]aprire hello **librerie** cartella, quindi hello copia **pushservice x.y.z** jar file e hello **armeabi**  &  **mips** cartelle hello **librerie** cartella dell'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="44b54-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="44b54-172">Aprire hello **AndroidManifest.xml** file di Android di progetto e aggiungere hello le autorizzazioni richieste da hello SDK Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="44b54-173">Aggiungere hello **android: name** proprietà tooyour **applicazione** elemento **AndroidManifest.xml**, sostituendo *yourprojectname* (per esempio **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="44b54-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="44b54-174">Verificare che il nome del progetto corrisponda hello uno configurato nella console di hello Baidu.</span><span class="sxs-lookup"><span data-stu-id="44b54-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="44b54-175">Aggiungere hello seguente configurazione all'interno dell'elemento applicazione hello dopo hello **. MainActivity** elemento activity, sostituendo *yourprojectname* (ad esempio, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="44b54-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="44b54-176">Aggiungere una nuova classe denominata **ConfigurationSettings.java** toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="44b54-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="44b54-177">Aggiungere hello tooit di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="44b54-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="44b54-178">Impostare il valore di hello di **API_KEY** con cosa recuperati dal progetto di cloud Baidu hello in precedenza, **NotificationHubName** con il nome di hub di notifica dal portale di Azure classico hello e  **NotificationHubConnectionString** con DefaultListenSharedAccessSignature da hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="44b54-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="44b54-179">Aggiungere una nuova classe denominata **DemoApplication.java**e aggiungere hello tooit di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="44b54-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="44b54-180">Aggiungere un'altra nuova classe denominata **MyPushMessageReceiver.java**e aggiungere hello tooit di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="44b54-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="44b54-181">Classe hello che gestisce hello notifiche push che vengono ricevute dal server di push Baidu hello è.</span><span class="sxs-lookup"><span data-stu-id="44b54-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="44b54-182">Aprire **Mainactivity**e aggiungere hello seguente toohello **onCreate** metodo:</span><span class="sxs-lookup"><span data-stu-id="44b54-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="44b54-183">Aprire hello seguendo le istruzioni import nella parte superiore di hello:</span><span class="sxs-lookup"><span data-stu-id="44b54-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="44b54-184">Inviare notifiche tooyour app</span><span class="sxs-lookup"><span data-stu-id="44b54-184">Send notifications tooyour app</span></span>
<span data-ttu-id="44b54-185">È possibile verificare rapidamente la ricezione di notifiche nell'app mediante l'invio di notifiche in hello [portale di Azure](https://portal.azure.com/) utilizzando hello **inviare** pulsante hub di notifica hello, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="44b54-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="44b54-186">Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile.</span><span class="sxs-lookup"><span data-stu-id="44b54-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="44b54-187">Se una libreria non è disponibile per il back-end, è possibile utilizzare l'API REST hello toosend direttamente i messaggi di notifica.</span><span class="sxs-lookup"><span data-stu-id="44b54-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="44b54-188">In questa esercitazione è la semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="44b54-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="44b54-189">Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="44b54-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="44b54-190">Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:</span><span class="sxs-lookup"><span data-stu-id="44b54-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="44b54-191">**Interfaccia REST**: È possibile supportare la notifica su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="44b54-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="44b54-192">**Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="44b54-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="44b54-193">**Node.js**: [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="44b54-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="44b54-194">**App per dispositivi mobili**: per un esempio di come toosend notifiche da un back-end dell'App Mobile di servizio App di Azure che è integrato con hub di notifica, vedere [app mobile tooyour le notifiche push Aggiungi](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="44b54-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="44b54-195">**Java o PHP**: per un esempio di come le notifiche toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="44b54-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="44b54-196">(Facoltativo) Inviare notifiche da un'app console .NET</span><span class="sxs-lookup"><span data-stu-id="44b54-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="44b54-197">In questa sezione verrà illustrato come inviare notifiche con un'app console .NET.</span><span class="sxs-lookup"><span data-stu-id="44b54-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="44b54-198">Creare una nuova applicazione console in Visual C#:</span><span class="sxs-lookup"><span data-stu-id="44b54-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="44b54-199">Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44b54-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="44b54-200">Questa istruzione consente di aggiungere un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="44b54-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="44b54-201">File hello aprire **Program.cs** e aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="44b54-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="44b54-202">Nel `Program` classe, aggiungere al metodo hello e sostituire *DefaultFullSharedAccessSignatureSASConnectionString* e *NotificationHubName* con i valori hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="44b54-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="44b54-203">Aggiungere hello righe in seguito il **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="44b54-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="44b54-204">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="44b54-204">Test your app</span></span>
<span data-ttu-id="44b54-205">connettere questa app con un telefono effettivi solo tootest hello computer tooyour phone tramite un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="44b54-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="44b54-206">Questa azione Carica l'app nel telefono hello associata.</span><span class="sxs-lookup"><span data-stu-id="44b54-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="44b54-207">Fare clic su questa applicazione con l'emulatore di Windows hello, barra degli strumenti hello Eclipse superiore, tootest **eseguire**e quindi selezionare l'app: avvio dell'emulatore hello, caricamenti, e viene eseguito hello app.</span><span class="sxs-lookup"><span data-stu-id="44b54-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="44b54-208">app Hello recupera hello 'userId' e 'ID canale' dal servizio di notifica Baidu Push hello e lo registra con hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="44b54-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="44b54-209">toosend una notifica di prova, è possibile utilizzare una scheda debug hello di hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="44b54-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="44b54-210">Se è stata compilata un'applicazione console .NET hello per Visual Studio, premi semplicemente tasto F5 hello in un'applicazione hello toorun Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44b54-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="44b54-211">un'applicazione Hello invia una notifica che viene visualizzato nell'area di notifica superiore hello nell'emulatore o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44b54-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[portale di Azure classico]: https://manage.windowsazure.com/
[Baidu portale]: http://www.baidu.com/
