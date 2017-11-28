---
title: Esercitazione di Streaming Windows Store App aaaSmooth | Documenti Microsoft
description: Informazioni su come toouse toocreate di servizi multimediali di Azure un'applicazione Windows Store c# con un MediaElement XML controllare tooplayback Smooth Streaming del contenuto.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="1d2bc-103">Come tooBuild un'applicazione Smooth Streaming Windows Store</span><span class="sxs-lookup"><span data-stu-id="1d2bc-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="1d2bc-104">Hello Smooth Streaming Client SDK per Windows 8 consente agli sviluppatori toobuild le applicazioni Windows Store in grado di riprodurre contenuto Smooth Streaming in tempo reale e su richiesta.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="1d2bc-105">Riproduzione di base toohello di Smooth Streaming di contenuto, hello SDK inoltre fornisce inoltre funzionalità avanzate come protezione Microsoft PlayReady, restrizione del livello di qualità, Live DVR, flusso audio di commutazione, in attesa per gli aggiornamenti di stato (ad esempio, le modifiche a livello di qualità ) e gli eventi di errore e così via.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="1d2bc-106">Per altre informazioni di funzionalità hello supportato, vedere hello [note sulla versione](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="1d2bc-107">Per ulteriori informazioni, vedere [Player Framework per Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="1d2bc-108">In questa esercitazione vengono presentate quattro lezioni:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="1d2bc-109">Creare un'applicazione Windows Store Smooth Streaming di base</span><span class="sxs-lookup"><span data-stu-id="1d2bc-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="1d2bc-110">Aggiungere un dispositivo di scorrimento tooControl hello supporti lo stato di avanzamento</span><span class="sxs-lookup"><span data-stu-id="1d2bc-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="1d2bc-111">Selezionare flussi Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="1d2bc-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="1d2bc-112">Selezionare tracce Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="1d2bc-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d2bc-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d2bc-113">Prerequisites</span></span>
* <span data-ttu-id="1d2bc-114">Windows 8 a 32 o 64 bit.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="1d2bc-115">È possibile scaricare la [versione di valutazione di Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) da MSDN.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="1d2bc-116">Visual Studio 2012 o Visual Studio Express 2012 (o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="1d2bc-117">È possibile ottenere una versione di valutazione di hello da [qui](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="1d2bc-118">[Microsoft Smooth Streaming Client SDK per Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="1d2bc-119">soluzione Hello completato per ogni lezione può essere scaricato da esempi di codice per sviluppatori MSDN (raccolta codici):</span><span class="sxs-lookup"><span data-stu-id="1d2bc-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="1d2bc-120">[Lezione 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : semplice lettore multimediale Smooth Streaming per Windows 8</span><span class="sxs-lookup"><span data-stu-id="1d2bc-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="1d2bc-121">[Lezione 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : semplice lettore multimediale Smooth Streaming per Windows 8 con controllo per la barra del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="1d2bc-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="1d2bc-122">[Lezione 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : lettore multimediale Smooth Streaming per Windows 8 con selezione flusso</span><span class="sxs-lookup"><span data-stu-id="1d2bc-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="1d2bc-123">[Lezione 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907): lettore multimediale Smooth Streaming per Windows 8 con selezione traccia.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="1d2bc-124">Lezione 1: Creare un'applicazione Windows Store Smooth Streaming di base</span><span class="sxs-lookup"><span data-stu-id="1d2bc-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="1d2bc-125">In questa lezione si creerà un'applicazione Windows Store con un controllo MediaElement tooplay Smooth Streaming del contenuto.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="1d2bc-126">simile a un'applicazione Hello in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-126">hello running application looks like:</span></span>

![Esempio di applicazione Windows Store Smooth Streaming][PlayerApplication]

<span data-ttu-id="1d2bc-128">Per ulteriori informazioni sullo sviluppo di app di Windows Store, vedere il sito relativo allo [sviluppo di app di Windows Store per Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d2bc-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="1d2bc-129">In questa lezione contiene hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="1d2bc-130">Creare un progetto Windows Store</span><span class="sxs-lookup"><span data-stu-id="1d2bc-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="1d2bc-131">Interfaccia utente di progettazione hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="1d2bc-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="1d2bc-132">Modificare hello file code-behind</span><span class="sxs-lookup"><span data-stu-id="1d2bc-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="1d2bc-133">Compilare e testare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-133">Compile and test hello application</span></span>

<span data-ttu-id="1d2bc-134">**toocreate un progetto Windows Store**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="1d2bc-135">Eseguire Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="1d2bc-136">Da hello **FILE** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="1d2bc-137">Dalla finestra di dialogo Nuovo progetto hello, tipo o seleziona hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="1d2bc-138">Nome</span><span class="sxs-lookup"><span data-stu-id="1d2bc-138">Name</span></span> | <span data-ttu-id="1d2bc-139">Valore</span><span class="sxs-lookup"><span data-stu-id="1d2bc-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2bc-140">Gruppo dei modelli di progetto</span><span class="sxs-lookup"><span data-stu-id="1d2bc-140">Template group</span></span> |<span data-ttu-id="1d2bc-141">Installato/Modelli/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="1d2bc-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="1d2bc-142">Modello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-142">Template</span></span> |<span data-ttu-id="1d2bc-143">Applicazione vuota (XAML)</span><span class="sxs-lookup"><span data-stu-id="1d2bc-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="1d2bc-144">Nome</span><span class="sxs-lookup"><span data-stu-id="1d2bc-144">Name</span></span> |<span data-ttu-id="1d2bc-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="1d2bc-145">SSPlayer</span></span> |
| <span data-ttu-id="1d2bc-146">Percorso</span><span class="sxs-lookup"><span data-stu-id="1d2bc-146">Location</span></span> |<span data-ttu-id="1d2bc-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="1d2bc-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="1d2bc-148">Nome soluzione</span><span class="sxs-lookup"><span data-stu-id="1d2bc-148">Solution Name</span></span> |<span data-ttu-id="1d2bc-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="1d2bc-149">SSPlayer</span></span> |
| <span data-ttu-id="1d2bc-150">Crea directory per soluzione</span><span class="sxs-lookup"><span data-stu-id="1d2bc-150">Create directory for solution</span></span> |<span data-ttu-id="1d2bc-151">(selezionata)</span><span class="sxs-lookup"><span data-stu-id="1d2bc-151">(selected)</span></span> |

1. <span data-ttu-id="1d2bc-152">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-152">Click **OK**.</span></span>

<span data-ttu-id="1d2bc-153">**tooadd toohello un riferimento Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="1d2bc-154">In Esplora soluzioni fare clic con il pulsante destro del mouse su **SSPlayer**, quindi scegliere **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="1d2bc-155">Digitare o selezionare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-155">Type or select hello following values:</span></span>

| <span data-ttu-id="1d2bc-156">Nome</span><span class="sxs-lookup"><span data-stu-id="1d2bc-156">Name</span></span> | <span data-ttu-id="1d2bc-157">Valore</span><span class="sxs-lookup"><span data-stu-id="1d2bc-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2bc-158">Gruppo di riferimenti</span><span class="sxs-lookup"><span data-stu-id="1d2bc-158">Reference group</span></span> |<span data-ttu-id="1d2bc-159">Windows/Estensioni</span><span class="sxs-lookup"><span data-stu-id="1d2bc-159">Windows/Extensions</span></span> |
| <span data-ttu-id="1d2bc-160">riferimento</span><span class="sxs-lookup"><span data-stu-id="1d2bc-160">Reference</span></span> |<span data-ttu-id="1d2bc-161">Selezionare Microsoft Smooth Streaming Client SDK per Windows 8 e Microsoft Visual C++ Runtime Package.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="1d2bc-162">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-162">Click **OK**.</span></span> 

<span data-ttu-id="1d2bc-163">Dopo l'aggiunta di riferimenti hello, è necessario selezionare una piattaforma di destinazione hello (x64 o x86), aggiunta di riferimenti non funzionerà per la configurazione di piattaforma qualsiasi CPU.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="1d2bc-164">In Esplora soluzioni verrà visualizzato un simbolo di avviso giallo per i riferimenti aggiunti.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="1d2bc-165">**interfaccia utente di Windows Media player hello toodesign**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="1d2bc-166">In Esplora soluzioni fare doppio clic su **MainPage. XAML** tooopen nella progettazione di hello visualizzare.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="1d2bc-167">Individuare hello  **&lt;griglia&gt;**  e  **&lt;/Grid&gt;**  tag hello file XAML e codice di esempio hello Incolla tra i tag hello due:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="1d2bc-168">controllo MediaElement Hello è tooplayback utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="1d2bc-169">controllo dispositivo di scorrimento Hello denominato sliderProgress verrà utilizzato in corso di hello prossima lezione toocontrol hello media.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="1d2bc-170">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-171">controllo MediaElement Hello non supporta Smooth Streaming del contenuto out-of-box.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="1d2bc-172">supporto di Smooth Streaming hello tooenable, è necessario registrare il gestore di hello Smooth Streaming-flusso di byte dall'estensione di file e il tipo MIME.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="1d2bc-173">tooregister, metodo hello MediaExtensionManager.RegisterByteStremHandler dello spazio dei nomi Windows.Media hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="1d2bc-174">In questo file XAML, sono associati ai controlli hello alcuni gestori di eventi.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="1d2bc-175">Sarà quindi necessario definire tali gestori di eventi.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-175">You must define those event handlers.</span></span>

<span data-ttu-id="1d2bc-176">**toomodify hello file code-behind**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="1d2bc-177">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-178">All'inizio di hello del file hello, aggiungere hello istruzione using:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="1d2bc-179">All'inizio di hello di hello **MainPage** classe, aggiungere hello dopo il membro di dati:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="1d2bc-180">Alla fine hello hello **MainPage** costruttore, aggiungere hello due righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="1d2bc-181">Alla fine hello hello **MainPage** classe, incollare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="1d2bc-182">gestore dell'evento sliderProgress_PointerPressed Hello è definito qui.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="1d2bc-183">Esistono altre opere toodo tooget lo stesso risultato, che verrà trattato in una lezione successiva di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="1d2bc-184">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-185">Hello hello termine file code-behind è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-185">hello finished hello code behind file shall look like this:</span></span>

![Visualizzazione del codice dell'applicazione Windows Store Smooth Streaming in Visual Studio][CodeViewPic]

<span data-ttu-id="1d2bc-187">**applicazione hello toocompile e test**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="1d2bc-188">Da hello **compilare** menu, fare clic su **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="1d2bc-189">Modifica **piattaforma soluzione attiva** toomatch la piattaforma di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="1d2bc-190">Premere **F6** progetto hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="1d2bc-191">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="1d2bc-192">Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="1d2bc-193">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-193">Click **Set Source**.</span></span> <span data-ttu-id="1d2bc-194">Poiché **AutoPlay** è abilitata per impostazione predefinita, hello media deve essere eseguito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="1d2bc-195">È possibile controllare il supporto di hello utilizzando hello **riprodurre**, **pausa** e **arrestare** pulsanti.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="1d2bc-196">È possibile controllare il volume di supporti hello con dispositivo di scorrimento verticale hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="1d2bc-197">Tuttavia hello dispositivo di scorrimento orizzontale per controllare lo stato di avanzamento di supporto non è completamente implementato ancora hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="1d2bc-198">La lezione 1 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-198">You have completed lesson1.</span></span>  <span data-ttu-id="1d2bc-199">In questa lezione, si utilizza un tooplayback controllo MediaElement contenuto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="1d2bc-200">Nella lezione successiva hello, si aggiungerà un dispositivo di scorrimento toocontrol hello lo stato di avanzamento di hello contenuto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="1d2bc-201">Lezione 2: Aggiungere un dispositivo di scorrimento tooControl hello supporti lo stato di avanzamento</span><span class="sxs-lookup"><span data-stu-id="1d2bc-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="1d2bc-202">Nella lezione 1, creato un'applicazione Windows Store con un tooplayback controllo MediaElement XAML Smooth Streaming di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="1d2bc-203">che include alcune funzionalità multimediali di base, come l'avvio, l'arresto e la sospensione della riproduzione.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="1d2bc-204">In questa lezione si aggiungerà un'applicazione di toohello dispositivo di scorrimento della barra di controllo.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="1d2bc-205">In questa esercitazione si utilizzerà una posizione di scorrimento timer tooupdate hello in base alla posizione corrente di hello di hello controllo MediaElement.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="1d2bc-206">dispositivo di scorrimento Hello inizio e fine ora anche toobe necessario aggiornare in caso di contenuti live.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="1d2bc-207">Questa può essere gestita meglio nell'evento di aggiornamento di hello origine adattivo.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="1d2bc-208">Le origini multimediali sono oggetti che generano dati multimediali.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="1d2bc-209">resolver di origine Hello accetta un URL, un flusso di byte e crea un'origine multimediale appropriato hello per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="1d2bc-210">resolver di codice sorgente Hello è modalità standard di hello per le origini di hello applicazioni toocreate media.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="1d2bc-211">In questa lezione contiene hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="1d2bc-212">Registrare il gestore di Smooth Streaming hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="1d2bc-213">Aggiungere gestori di eventi a livello di hello origine adattivo manager</span><span class="sxs-lookup"><span data-stu-id="1d2bc-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="1d2bc-214">Aggiungere gestori eventi a livello di origine adattivo hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="1d2bc-215">Aggiungere i gestori di eventi MediaElement</span><span class="sxs-lookup"><span data-stu-id="1d2bc-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="1d2bc-216">Aggiungere il codice relativo alla barra del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="1d2bc-216">Add slider bar related code</span></span>
6. <span data-ttu-id="1d2bc-217">Compilare e testare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-217">Compile and test hello application</span></span>

<span data-ttu-id="1d2bc-218">**propertyset hello gestore e passare tooregister hello Smooth Streaming-flusso di byte**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="1d2bc-219">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-220">All'inizio di hello del file hello, aggiungere hello istruzione using:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="1d2bc-221">Inizio hello della classe MainPage hello, aggiungere hello membri dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="1d2bc-222">Inside hello **MainPage** costruttore, aggiungere hello seguente codice dopo hello **questo. Inizializzare Components();**  riga e righe di codice di registrazione hello scritte nella lezione precedente hello:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="1d2bc-223">Inside hello **MainPage** costruttore modificare via di hello tooadd metodi RegisterByteStreamHandler di hello due parametri:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="1d2bc-224">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-225">**gestore eventi a livello di tooadd hello origine adattivo manager**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="1d2bc-226">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-227">Inside hello **MainPage** classe, aggiungere hello dopo il membro di dati:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="1d2bc-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="1d2bc-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="1d2bc-229">Alla fine hello hello **MainPage** classe, aggiungere hello seguente gestore eventi:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="1d2bc-230">Alla fine hello hello **MainPage** costruttore, aggiungere hello evento open origine adattivo toohello toosubscribe riga seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="1d2bc-231">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-232">**gestori eventi a livello di origine adattivo tooadd**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="1d2bc-233">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-234">Inside hello **MainPage** classe, aggiungere hello dopo il membro di dati:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="1d2bc-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="1d2bc-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="1d2bc-236">Alla fine hello hello **MainPage** classe, aggiungere hello gestori di eventi seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="1d2bc-237">Alla fine hello hello **mediaElement AdaptiveSourceOpened** metodo, aggiungere hello eventi toohello toosubscribe di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="1d2bc-238">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-239">Hello stessi eventi sono disponibili in adattivo gestione livello di origine, che può essere utilizzato per la gestione delle funzionalità comuni tooall elementi multimediali in app hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="1d2bc-240">Ogni elemento AdaptiveSource include i relativi eventi e tutti gli eventi AdaptiveSource vengono propagati in AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="1d2bc-241">**gestori di eventi tooadd elemento multimediale**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="1d2bc-242">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-243">Alla fine hello hello **MainPage** classe, aggiungere hello gestori di eventi seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="1d2bc-244">Alla fine hello hello **MainPage** costruttore, aggiungere hello eventi toohello toosubscript di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="1d2bc-245">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-246">**dispositivo di scorrimento tooadd correlato codice a barre**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="1d2bc-247">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-248">All'inizio di hello del file hello, aggiungere hello istruzione using:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="1d2bc-249">Inside hello **MainPage** classe, aggiungere hello membri dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="1d2bc-250">Alla fine hello hello **MainPage** costruttore, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="1d2bc-251">Alla fine hello hello **MainPage** classe, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="1d2bc-252">CoreDispatcher è usato toomake modifiche toohello dell'interfaccia utente del thread dal Thread dell'interfaccia utente non.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="1d2bc-253">In caso di colli di bottiglia nel thread del dispatcher, consentire allo sviluppatore dispatcher toouse fornito dall'elemento dell'interfaccia utente che ha intenzione di tooupdate.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="1d2bc-254">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="1d2bc-255">Alla fine hello hello **mediaElement_AdaptiveSourceStatusUpdated** metodo, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="1d2bc-256">Alla fine hello hello **MediaOpened** metodo, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="1d2bc-257">Premere **CTRL + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="1d2bc-258">**applicazione hello toocompile e test**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="1d2bc-259">Premere **F6** progetto hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="1d2bc-260">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="1d2bc-261">Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="1d2bc-262">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="1d2bc-263">Barra di scorrimento hello di test.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-263">Test hello slider bar.</span></span>

<span data-ttu-id="1d2bc-264">La lezione 2 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-264">You have completed lesson 2.</span></span>  <span data-ttu-id="1d2bc-265">In questa lezione è stato aggiunto un tooapplication dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="1d2bc-266">Lezione 3: Selezionare flussi Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="1d2bc-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="1d2bc-267">Smooth Streaming è contenuto in grado di supportare toostream con tracce audio in più lingue selezionabili per visualizzatori hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="1d2bc-268">In questa lezione si abiliterà flussi tooselect visualizzatori.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="1d2bc-269">In questa lezione contiene hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="1d2bc-270">Modificare i file XAML hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="1d2bc-271">Modificare file behand del codice hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="1d2bc-272">Compilare e testare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-272">Compile and test hello application</span></span>

<span data-ttu-id="1d2bc-273">**file XAML di hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="1d2bc-274">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="1d2bc-275">Individuare &lt;Grid. RowDefinitions&gt;e modificare hello RowDefinitions in modo che il seguente aspetto:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="1d2bc-276">Inside hello &lt;griglia&gt;&lt;/Grid&gt; tag, aggiungere hello di codice seguente toodefine un controllo listbox, in modo gli utenti possono visualizzare hello elenco di flussi disponibili e selezionare flussi:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. <span data-ttu-id="1d2bc-277">Premere **CTRL + S** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="1d2bc-278">**toomodify hello file code-behind**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="1d2bc-279">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-280">All'interno dello spazio dei nomi SSPlayer hello, aggiungere una nuova classe:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="1d2bc-281">Inizio hello della classe MainPage hello, aggiungere hello definizioni di variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="1d2bc-282">All'interno di hello classe MainPage, aggiungere hello area seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-282">Inside hello MainPage class, add hello following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="1d2bc-283">Individuare il metodo mediaElement_ManifestReady hello, accodare hello seguente codice alla fine di hello della funzione hello:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="1d2bc-284">Pertanto quando MediaElement manifesto è pronto, codice hello Ottiene un elenco di flussi disponibili hello e popola una casella di riepilogo dell'interfaccia utente di hello con elenco hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="1d2bc-285">All'interno di hello classe MainPage, individuare i pulsanti dell'interfaccia utente di hello fare clic su area di eventi e quindi aggiungere hello seguente definizione di funzione:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="1d2bc-286">**applicazione hello toocompile e test**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="1d2bc-287">Premere **F6** progetto hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="1d2bc-288">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="1d2bc-289">Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="1d2bc-290">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="1d2bc-291">lingua predefinita Hello è audio_eng.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-291">hello default language is audio_eng.</span></span> <span data-ttu-id="1d2bc-292">Provare a tooswitch tra audio_eng e audio_es.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="1d2bc-293">Ogni volta che, si seleziona un nuovo flusso, è necessario fare clic su pulsante Submit hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="1d2bc-294">La lezione 3 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-294">You have completed lesson 3.</span></span>  <span data-ttu-id="1d2bc-295">In questa lezione, aggiungere i flussi toochoose funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="1d2bc-296">Lezione 4: Selezionare tracce Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="1d2bc-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="1d2bc-297">Una presentazione Smooth Streaming può contenere più file video codificati con livelli di qualità (velocità in bit) e risoluzioni diversi.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="1d2bc-298">In questa lezione si abiliterà utenti tooselect tracce.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="1d2bc-299">In questa lezione contiene hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="1d2bc-300">Modificare i file XAML hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="1d2bc-301">Modificare file behand del codice hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="1d2bc-302">Compilare e testare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1d2bc-302">Compile and test hello application</span></span>

<span data-ttu-id="1d2bc-303">**file XAML di hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="1d2bc-304">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="1d2bc-305">Individuare hello &lt;griglia&gt; tag con nome hello **gridStreamAndBitrateSelection**, accodare hello seguente codice alla fine di hello del tag hello:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. <span data-ttu-id="1d2bc-306">Premere **CTRL + S** toosave modifica</span><span class="sxs-lookup"><span data-stu-id="1d2bc-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="1d2bc-307">**toomodify hello file code-behind**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="1d2bc-308">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="1d2bc-309">All'interno dello spazio dei nomi SSPlayer hello, aggiungere una nuova classe:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="1d2bc-310">Inizio hello della classe MainPage hello, aggiungere hello definizioni di variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="1d2bc-311">All'interno di hello classe MainPage, aggiungere hello area seguente:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-311">Inside hello MainPage class, add hello following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="1d2bc-312">Individuare il metodo mediaElement_ManifestReady hello, accodare hello seguente codice alla fine di hello della funzione hello:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="1d2bc-313">All'interno di hello classe MainPage, individuare i pulsanti dell'interfaccia utente di hello fare clic su area di eventi e quindi aggiungere hello seguente definizione di funzione:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="1d2bc-314">**applicazione hello toocompile e test**</span><span class="sxs-lookup"><span data-stu-id="1d2bc-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="1d2bc-315">Premere **F6** progetto hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="1d2bc-316">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="1d2bc-317">Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="1d2bc-318">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="1d2bc-319">Per impostazione predefinita, tutte le tracce di hello del flusso video hello sono selezionate.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="1d2bc-320">le modifiche apportate alla frequenza di bit tooexperiment hello, è possibile selezionare hello più bassa velocità in bit disponibili e quindi selezionare hello più alta velocità in bit disponibili.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="1d2bc-321">Dopo ogni modifica, è necessario fare clic su Invia.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-321">You must click Submit after each change.</span></span>  <span data-ttu-id="1d2bc-322">È possibile visualizzare le modifiche della qualità video hello.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="1d2bc-323">La lezione 4 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-323">You have completed lesson 4.</span></span>  <span data-ttu-id="1d2bc-324">In questa lezione si aggiungere hello funzionalità toochoose tracce.</span><span class="sxs-lookup"><span data-stu-id="1d2bc-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1d2bc-325">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1d2bc-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1d2bc-326">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1d2bc-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="1d2bc-327">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="1d2bc-327">Other Resources:</span></span>
* [<span data-ttu-id="1d2bc-328">Come toobuild un'applicazione di Smooth Streaming Windows 8 JavaScript con le funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="1d2bc-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="1d2bc-329">Panoramica tecnica relativa a Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="1d2bc-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

