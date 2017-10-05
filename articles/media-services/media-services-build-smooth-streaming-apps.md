---
title: Esercitazione per l'app Smooth Streaming di Windows Store | Microsoft Docs
description: Informazioni su come usare Servizi multimediali di Azure per creare un'applicazione Windows Store C# con un controllo XML MediaElement per riprodurre contenuto Smooth Streaming.
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="aba70-103">Come creare un'applicazione Windows Store Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="aba70-104">Smooth Streaming Client SDK per Windows 8 consente agli sviluppatori di creare app di Windows Store in grado di riprodurre contenuto Smooth Streaming in diretta e su richiesta.</span><span class="sxs-lookup"><span data-stu-id="aba70-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="aba70-105">Oltre a fornire le funzionalità di riproduzione di base del contenuto Smooth Streaming, l'SDK offre inoltre funzionalità avanzate, ad esempio protezione Microsoft PlayReady, limitazione del livello di qualità, DVR in diretta, commutazione del flusso audio, ascolto per aggiornamenti di stato (ad esempio variazioni del livello di qualità) ed eventi di errore, e così via.</span><span class="sxs-lookup"><span data-stu-id="aba70-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="aba70-106">Per altre informazioni sulle funzionalità supportate, vedere le [note sulla versione](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="aba70-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="aba70-107">Per ulteriori informazioni, vedere [Player Framework per Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="aba70-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="aba70-108">In questa esercitazione vengono presentate quattro lezioni:</span><span class="sxs-lookup"><span data-stu-id="aba70-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="aba70-109">Creare un'applicazione Windows Store Smooth Streaming di base</span><span class="sxs-lookup"><span data-stu-id="aba70-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="aba70-110">Aggiungere una barra del dispositivo scorrimento per controllare l'avanzamento del file multimediale</span><span class="sxs-lookup"><span data-stu-id="aba70-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="aba70-111">Selezionare flussi Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="aba70-112">Selezionare tracce Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aba70-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aba70-113">Prerequisites</span></span>
* <span data-ttu-id="aba70-114">Windows 8 a 32 o 64 bit.</span><span class="sxs-lookup"><span data-stu-id="aba70-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="aba70-115">È possibile scaricare la [versione di valutazione di Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) da MSDN.</span><span class="sxs-lookup"><span data-stu-id="aba70-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="aba70-116">Visual Studio 2012 o Visual Studio Express 2012 (o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="aba70-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="aba70-117">Per scaricare la versione di valutazione, fare clic [qui](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="aba70-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="aba70-118">[Microsoft Smooth Streaming Client SDK per Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="aba70-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="aba70-119">La soluzione completata per ogni lezione può essere scaricata dagli esempi di esempi di codice per sviluppatori in MSDN.</span><span class="sxs-lookup"><span data-stu-id="aba70-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="aba70-120">[Lezione 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : semplice lettore multimediale Smooth Streaming per Windows 8</span><span class="sxs-lookup"><span data-stu-id="aba70-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="aba70-121">[Lezione 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : semplice lettore multimediale Smooth Streaming per Windows 8 con controllo per la barra del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="aba70-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="aba70-122">[Lezione 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : lettore multimediale Smooth Streaming per Windows 8 con selezione flusso</span><span class="sxs-lookup"><span data-stu-id="aba70-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="aba70-123">[Lezione 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907): lettore multimediale Smooth Streaming per Windows 8 con selezione traccia.</span><span class="sxs-lookup"><span data-stu-id="aba70-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="aba70-124">Lezione 1: Creare un'applicazione Windows Store Smooth Streaming di base</span><span class="sxs-lookup"><span data-stu-id="aba70-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="aba70-125">In questa lezione verrà creata un'applicazione Windows Store con un controllo MediaElement per riprodurre contenuto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="aba70-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="aba70-126">L'applicazione in esecuzione avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-126">The running application looks like:</span></span>

![Esempio di applicazione Windows Store Smooth Streaming][PlayerApplication]

<span data-ttu-id="aba70-128">Per ulteriori informazioni sullo sviluppo di app di Windows Store, vedere il sito relativo allo [sviluppo di app di Windows Store per Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="aba70-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="aba70-129">In questa lezione sono incluse le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="aba70-130">Creare un progetto Windows Store</span><span class="sxs-lookup"><span data-stu-id="aba70-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="aba70-131">Progettare l'interfaccia utente (XAML)</span><span class="sxs-lookup"><span data-stu-id="aba70-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="aba70-132">Modificare il file code-behind</span><span class="sxs-lookup"><span data-stu-id="aba70-132">Modify the code behind file</span></span>
4. <span data-ttu-id="aba70-133">Compilare ed eseguire il test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="aba70-133">Compile and test the application</span></span>

<span data-ttu-id="aba70-134">**Per creare un progetto Windows Store**</span><span class="sxs-lookup"><span data-stu-id="aba70-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="aba70-135">Eseguire Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="aba70-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="aba70-136">Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="aba70-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="aba70-137">Nella finestra di dialogo Nuovo progetto digitare o selezionare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="aba70-138">Nome</span><span class="sxs-lookup"><span data-stu-id="aba70-138">Name</span></span> | <span data-ttu-id="aba70-139">Valore</span><span class="sxs-lookup"><span data-stu-id="aba70-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="aba70-140">Gruppo dei modelli di progetto</span><span class="sxs-lookup"><span data-stu-id="aba70-140">Template group</span></span> |<span data-ttu-id="aba70-141">Installato/Modelli/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="aba70-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="aba70-142">Modello</span><span class="sxs-lookup"><span data-stu-id="aba70-142">Template</span></span> |<span data-ttu-id="aba70-143">Applicazione vuota (XAML)</span><span class="sxs-lookup"><span data-stu-id="aba70-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="aba70-144">Nome</span><span class="sxs-lookup"><span data-stu-id="aba70-144">Name</span></span> |<span data-ttu-id="aba70-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="aba70-145">SSPlayer</span></span> |
| <span data-ttu-id="aba70-146">Percorso</span><span class="sxs-lookup"><span data-stu-id="aba70-146">Location</span></span> |<span data-ttu-id="aba70-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="aba70-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="aba70-148">Nome soluzione</span><span class="sxs-lookup"><span data-stu-id="aba70-148">Solution Name</span></span> |<span data-ttu-id="aba70-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="aba70-149">SSPlayer</span></span> |
| <span data-ttu-id="aba70-150">Crea directory per soluzione</span><span class="sxs-lookup"><span data-stu-id="aba70-150">Create directory for solution</span></span> |<span data-ttu-id="aba70-151">(selezionata)</span><span class="sxs-lookup"><span data-stu-id="aba70-151">(selected)</span></span> |

1. <span data-ttu-id="aba70-152">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="aba70-152">Click **OK**.</span></span>

<span data-ttu-id="aba70-153">**Per aggiungere un riferimento a Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="aba70-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="aba70-154">In Esplora soluzioni fare clic con il pulsante destro del mouse su **SSPlayer**, quindi scegliere **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="aba70-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="aba70-155">Digitare o selezionare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-155">Type or select the following values:</span></span>

| <span data-ttu-id="aba70-156">Nome</span><span class="sxs-lookup"><span data-stu-id="aba70-156">Name</span></span> | <span data-ttu-id="aba70-157">Valore</span><span class="sxs-lookup"><span data-stu-id="aba70-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="aba70-158">Gruppo di riferimenti</span><span class="sxs-lookup"><span data-stu-id="aba70-158">Reference group</span></span> |<span data-ttu-id="aba70-159">Windows/Estensioni</span><span class="sxs-lookup"><span data-stu-id="aba70-159">Windows/Extensions</span></span> |
| <span data-ttu-id="aba70-160">riferimento</span><span class="sxs-lookup"><span data-stu-id="aba70-160">Reference</span></span> |<span data-ttu-id="aba70-161">Selezionare Microsoft Smooth Streaming Client SDK per Windows 8 e Microsoft Visual C++ Runtime Package.</span><span class="sxs-lookup"><span data-stu-id="aba70-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="aba70-162">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="aba70-162">Click **OK**.</span></span> 

<span data-ttu-id="aba70-163">Dopo avere aggiunto i riferimenti, è necessario selezionare la piattaforma di destinazione (x64 o x86). L'aggiunta di riferimenti non funzionerà per la configurazione di piattaforma Qualsiasi CPU.</span><span class="sxs-lookup"><span data-stu-id="aba70-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="aba70-164">In Esplora soluzioni verrà visualizzato un simbolo di avviso giallo per i riferimenti aggiunti.</span><span class="sxs-lookup"><span data-stu-id="aba70-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="aba70-165">**Per progettare l'interfaccia utente del lettore**</span><span class="sxs-lookup"><span data-stu-id="aba70-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="aba70-166">In Esplora soluzioni fare doppio clic su **MainPage.xaml** per aprirlo in visualizzazione Progettazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="aba70-167">Individuare i tag **&lt;Grid&gt;** e **&lt;/Grid>&gt;** nel file XAML e incollare il codice seguente tra i due tag:</span><span class="sxs-lookup"><span data-stu-id="aba70-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="aba70-168">Il controllo MediaElement viene utilizzato per riprodurre i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="aba70-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="aba70-169">Nella lezione successiva verrà utilizzato il controllo del dispositivo di scorrimento denominato sliderProgress per controllare l'avanzamento del file multimediale.</span><span class="sxs-lookup"><span data-stu-id="aba70-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="aba70-170">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-171">Il controllo MediaElement non supporta il contenuto Smooth Streaming per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="aba70-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="aba70-172">Per abilitare il supporto Smooth Streaming, è necessario registrare il gestore del flusso di byte in base all'estensione del nome file e al tipo MIME.</span><span class="sxs-lookup"><span data-stu-id="aba70-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="aba70-173">Per effettuare la registrazione è necessario usare il metodo MediaExtensionManager.RegisterByteStremHandler dello spazio dei nomi Windows.Media.</span><span class="sxs-lookup"><span data-stu-id="aba70-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="aba70-174">Nel file XAML alcuni gestori di eventi sono associati ai controlli.</span><span class="sxs-lookup"><span data-stu-id="aba70-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="aba70-175">Sarà quindi necessario definire tali gestori di eventi.</span><span class="sxs-lookup"><span data-stu-id="aba70-175">You must define those event handlers.</span></span>

<span data-ttu-id="aba70-176">**Per modificare il file code-behind**</span><span class="sxs-lookup"><span data-stu-id="aba70-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="aba70-177">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-178">Aggiungere l'istruzione using seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="aba70-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="aba70-179">All'inizio della classe **MainPage** aggiungere il membro dati seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="aba70-180">Alla fine del costruttore **MainPage** aggiungere le due righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="aba70-181">Alla fine della classe **MainPage** incollare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="aba70-182">Il gestore di eventi sliderProgress_PointerPressed viene definito qui.</span><span class="sxs-lookup"><span data-stu-id="aba70-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="aba70-183">Per renderlo funzionante, è tuttavia necessario eseguire ulteriori attività che verranno illustrate nella lezione successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="aba70-184">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-185">Il file code-behind finito avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-185">The finished the code behind file shall look like this:</span></span>

![Visualizzazione del codice dell'applicazione Windows Store Smooth Streaming in Visual Studio][CodeViewPic]

<span data-ttu-id="aba70-187">**Per compilare e testare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="aba70-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="aba70-188">Nel menu **GENERA** scegliere **Gestione configurazione**.</span><span class="sxs-lookup"><span data-stu-id="aba70-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="aba70-189">Modificare **Piattaforma soluzione attiva** in base alla piattaforma di sviluppo in uso.</span><span class="sxs-lookup"><span data-stu-id="aba70-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="aba70-190">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aba70-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="aba70-191">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="aba70-192">Nella parte superiore dell'applicazione, è possibile utilizzare l'URL di Smooth Streaming predefinito o immetterne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="aba70-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="aba70-193">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="aba70-193">Click **Set Source**.</span></span> <span data-ttu-id="aba70-194">Poiché l'opzione **Riproduzione automatica** è abilitata per impostazione predefinita, il file multimediale verrà riprodotto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aba70-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="aba70-195">È possibile controllare i file multimediali usando i pulsanti di **riproduzione**, **pausa** e **arresto**.</span><span class="sxs-lookup"><span data-stu-id="aba70-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="aba70-196">È possibile controllare il volume del contenuto multimediale tramite il dispositivo di scorrimento verticale.</span><span class="sxs-lookup"><span data-stu-id="aba70-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="aba70-197">Il dispositivo di scorrimento orizzontale per il controllo dell'avanzamento del file multimediale non è tuttavia ancora implementato.</span><span class="sxs-lookup"><span data-stu-id="aba70-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="aba70-198">La lezione 1 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aba70-198">You have completed lesson1.</span></span>  <span data-ttu-id="aba70-199">In questa lezione è stato utilizzato un controllo MediaElement per riprodurre contenuto multimediale Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="aba70-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="aba70-200">Nella lezione successiva verrà aggiunto un dispositivo di scorrimento per controllare l'avanzamento del contenuto multimediale Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="aba70-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="aba70-201">Lezione 2: Aggiungere una barra del dispositivo di scorrimento per controllare l'avanzamento del file multimediale</span><span class="sxs-lookup"><span data-stu-id="aba70-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="aba70-202">Nella lezione 1 è stata creata un'applicazione Windows Store con un controllo XAML MediaElement per riprodurre contenuto multimediale Smooth Streaming,</span><span class="sxs-lookup"><span data-stu-id="aba70-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="aba70-203">che include alcune funzionalità multimediali di base, come l'avvio, l'arresto e la sospensione della riproduzione.</span><span class="sxs-lookup"><span data-stu-id="aba70-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="aba70-204">In questa lezione verrà aggiunto un controllo per la barra del dispositivo di scorrimento all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="aba70-205">In questa esercitazione verrà utilizzato un timer per l'aggiornamento della posizione del dispositivo di scorrimento in base alla posizione corrente del controllo MediaElement.</span><span class="sxs-lookup"><span data-stu-id="aba70-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="aba70-206">Sarà inoltre necessario aggiornare l'ora di inizio e di fine del dispositivo di scorrimento in caso di contenuto in diretta.</span><span class="sxs-lookup"><span data-stu-id="aba70-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="aba70-207">È possibile gestire questo scenario nell'evento di aggiornamento dell'origine adattiva.</span><span class="sxs-lookup"><span data-stu-id="aba70-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="aba70-208">Le origini multimediali sono oggetti che generano dati multimediali.</span><span class="sxs-lookup"><span data-stu-id="aba70-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="aba70-209">Il resolver dell'origine accetta un URL o un flusso di byte e crea l'origine multimediale appropriata per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="aba70-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="aba70-210">Il resolver dell'origine rappresenta il modo standard per la creazione di origini multimediali da parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="aba70-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="aba70-211">In questa lezione sono incluse le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="aba70-212">Registrare il gestore Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="aba70-213">Aggiungere i gestori di eventi a livello di gestione dell'origine adattiva</span><span class="sxs-lookup"><span data-stu-id="aba70-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="aba70-214">Aggiungere i gestori di eventi a livello di origine adattiva</span><span class="sxs-lookup"><span data-stu-id="aba70-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="aba70-215">Aggiungere i gestori di eventi MediaElement</span><span class="sxs-lookup"><span data-stu-id="aba70-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="aba70-216">Aggiungere il codice relativo alla barra del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="aba70-216">Add slider bar related code</span></span>
6. <span data-ttu-id="aba70-217">Compilare ed eseguire il test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="aba70-217">Compile and test the application</span></span>

<span data-ttu-id="aba70-218">**Per registrare il gestore del flusso di byte Smooth Streaming e passare propertySet**</span><span class="sxs-lookup"><span data-stu-id="aba70-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="aba70-219">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-220">Aggiungere l'istruzione using seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="aba70-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="aba70-221">All'inizio della classe MainPage aggiungere i membri dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="aba70-222">Nel costruttore **MainPage** aggiungere il codice seguente dopo la riga **this.Initialize Components();** e le righe di codice per la registrazione scritte nella lezione precedente:</span><span class="sxs-lookup"><span data-stu-id="aba70-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="aba70-223">Nel costruttore **MainPage** modificare i due metodi RegisterByteStreamHandler per aggiungere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="aba70-224">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-225">**Per aggiungere il gestore eventi a livello di gestione dell'origine adattiva**</span><span class="sxs-lookup"><span data-stu-id="aba70-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="aba70-226">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-227">All'interno della classe **MainPage** aggiungere il membro dati seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="aba70-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="aba70-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="aba70-229">Alla fine della classe **MainPage** aggiungere il gestore di eventi seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="aba70-230">Alla fine del costruttore **MainPage** aggiungere la riga seguente per effettuare la sottoscrizione all'evento di apertura dell'origine adattiva:</span><span class="sxs-lookup"><span data-stu-id="aba70-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="aba70-231">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-232">**Per aggiungere i gestori eventi a livello di origine adattiva**</span><span class="sxs-lookup"><span data-stu-id="aba70-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="aba70-233">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-234">All'interno della classe **MainPage** aggiungere il membro dati seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="aba70-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="aba70-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="aba70-236">Alla fine della classe **MainPage** aggiungere i gestori di eventi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="aba70-237">Alla fine del metodo **mediaElement AdaptiveSourceOpened** aggiungere il codice seguente per eseguire la sottoscrizione agli eventi:</span><span class="sxs-lookup"><span data-stu-id="aba70-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="aba70-238">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-239">Gli stessi eventi sono inoltre disponibili a livello di gestione dell'origine adattiva e possono essere utilizzati per gestire le funzionalità comuni a tutti gli elementi multimediali nell'app.</span><span class="sxs-lookup"><span data-stu-id="aba70-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="aba70-240">Ogni elemento AdaptiveSource include i relativi eventi e tutti gli eventi AdaptiveSource vengono propagati in AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="aba70-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="aba70-241">**Per aggiungere i gestori eventi MediaElement**</span><span class="sxs-lookup"><span data-stu-id="aba70-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="aba70-242">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-243">Alla fine della classe **MainPage** aggiungere i gestori di eventi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="aba70-244">Alla fine del costruttore **MainPage** aggiungere il codice seguente per eseguire la sottoscrizione agli eventi:</span><span class="sxs-lookup"><span data-stu-id="aba70-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="aba70-245">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-246">**Per aggiungere il codice relativo alla barra del dispositivo di scorrimento**</span><span class="sxs-lookup"><span data-stu-id="aba70-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="aba70-247">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-248">Aggiungere l'istruzione using seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="aba70-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="aba70-249">All'interno della classe **MainPage** aggiungere i membri dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="aba70-250">Alla fine del costruttore **MainPage** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="aba70-251">Alla fine della classe **MainPage** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="aba70-252">Per apportare modifiche al thread dell'interfaccia utente da un thread non di interfaccia utente viene usato CoreDispatcher.</span><span class="sxs-lookup"><span data-stu-id="aba70-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="aba70-253">In caso di colli di bottiglia nel thread del dispatcher, gli sviluppatori possono scegliere di usare il dispatcher fornito dall'elemento dell'interfaccia utente che intendono aggiornare.</span><span class="sxs-lookup"><span data-stu-id="aba70-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="aba70-254">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="aba70-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="aba70-255">Alla fine del metodo **mediaElement_AdaptiveSourceStatusUpdated** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="aba70-256">Alla fine del metodo **MediaOpened** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="aba70-257">Premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="aba70-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="aba70-258">**Per compilare e testare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="aba70-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="aba70-259">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aba70-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="aba70-260">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="aba70-261">Nella parte superiore dell'applicazione, è possibile utilizzare l'URL di Smooth Streaming predefinito o immetterne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="aba70-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="aba70-262">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="aba70-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="aba70-263">Eseguire il test della barra del dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="aba70-263">Test the slider bar.</span></span>

<span data-ttu-id="aba70-264">La lezione 2 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aba70-264">You have completed lesson 2.</span></span>  <span data-ttu-id="aba70-265">In questa lezione è stato aggiunto un dispositivo di scorrimento all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="aba70-266">Lezione 3: Selezionare flussi Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="aba70-267">Smooth Streaming consente di trasmettere contenuto in streaming con tracce audio in più lingue selezionabili dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="aba70-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="aba70-268">In questa lezione verrà illustrato come abilitare gli utenti per la selezione dei flussi.</span><span class="sxs-lookup"><span data-stu-id="aba70-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="aba70-269">In questa lezione sono incluse le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="aba70-270">Modificare il file XAML</span><span class="sxs-lookup"><span data-stu-id="aba70-270">Modify the XAML file</span></span>
2. <span data-ttu-id="aba70-271">Modificare il file code-behind</span><span class="sxs-lookup"><span data-stu-id="aba70-271">Modify the code behand file</span></span>
3. <span data-ttu-id="aba70-272">Compilare ed eseguire il test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="aba70-272">Compile and test the application</span></span>

<span data-ttu-id="aba70-273">**Per modificare il file XAML**</span><span class="sxs-lookup"><span data-stu-id="aba70-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="aba70-274">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.</span><span class="sxs-lookup"><span data-stu-id="aba70-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="aba70-275">Individuare &lt;Grid.RowDefinitions&gt; e modificare gli elementi RowDefinitions affinché presentino un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="aba70-276">All'interno dei tag &lt;Grid&gt;&lt;/Grid&gt; aggiungere il codice seguente per definire un controllo casella di riepilogo, in modo da consentire agli utenti di visualizzare l'elenco dei flussi disponibili e selezionare quello desiderato:</span><span class="sxs-lookup"><span data-stu-id="aba70-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="aba70-277">Premere **CTRL+S** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="aba70-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="aba70-278">**Per modificare il file code-behind**</span><span class="sxs-lookup"><span data-stu-id="aba70-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="aba70-279">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-280">All'interno dello spazio dei nomi SSPlayer, aggiungere una nuova classe:</span><span class="sxs-lookup"><span data-stu-id="aba70-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="aba70-281">All'inizio della classe MainPage aggiungere le seguenti definizioni di variabili:</span><span class="sxs-lookup"><span data-stu-id="aba70-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="aba70-282">All'interno della classe MainPage aggiungere l'area seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="aba70-283">Individuare il metodo mediaElement_ManifestReady e aggiungere il codice seguente alla fine della funzione:</span><span class="sxs-lookup"><span data-stu-id="aba70-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="aba70-284">Quando il manifesto di MediaElement è pronto, il codice recupera un elenco dei flussi disponibili e popola la casella di riepilogo dell'interfaccia utente con l'elenco.</span><span class="sxs-lookup"><span data-stu-id="aba70-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="aba70-285">All'interno della classe MainPage, individuare l'area degli eventi clic dei pulsanti dell'interfaccia utente e aggiungere la seguente definizione di funzione:</span><span class="sxs-lookup"><span data-stu-id="aba70-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="aba70-286">**Per compilare e testare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="aba70-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="aba70-287">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aba70-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="aba70-288">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="aba70-289">Nella parte superiore dell'applicazione, è possibile utilizzare l'URL di Smooth Streaming predefinito o immetterne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="aba70-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="aba70-290">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="aba70-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="aba70-291">La lingua predefinita è audio_eng.</span><span class="sxs-lookup"><span data-stu-id="aba70-291">The default language is audio_eng.</span></span> <span data-ttu-id="aba70-292">Provare a passare da audio_eng ad audio_es e viceversa.</span><span class="sxs-lookup"><span data-stu-id="aba70-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="aba70-293">Ogni volta che si seleziona un nuovo flusso, è necessario fare clic sul pulsante Invia.</span><span class="sxs-lookup"><span data-stu-id="aba70-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="aba70-294">La lezione 3 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aba70-294">You have completed lesson 3.</span></span>  <span data-ttu-id="aba70-295">In questa lezione è stata aggiunta la funzionalità per la selezione dei flussi.</span><span class="sxs-lookup"><span data-stu-id="aba70-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="aba70-296">Lezione 4: Selezionare tracce Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="aba70-297">Una presentazione Smooth Streaming può contenere più file video codificati con livelli di qualità (velocità in bit) e risoluzioni diversi.</span><span class="sxs-lookup"><span data-stu-id="aba70-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="aba70-298">In questa lezione verrà illustrato come abilitare gli utenti per la selezione delle tracce.</span><span class="sxs-lookup"><span data-stu-id="aba70-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="aba70-299">In questa lezione sono incluse le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba70-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="aba70-300">Modificare il file XAML</span><span class="sxs-lookup"><span data-stu-id="aba70-300">Modify the XAML file</span></span>
2. <span data-ttu-id="aba70-301">Modificare il file code-behind</span><span class="sxs-lookup"><span data-stu-id="aba70-301">Modify the code behand file</span></span>
3. <span data-ttu-id="aba70-302">Compilare ed eseguire il test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="aba70-302">Compile and test the application</span></span>

<span data-ttu-id="aba70-303">**Per modificare il file XAML**</span><span class="sxs-lookup"><span data-stu-id="aba70-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="aba70-304">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.</span><span class="sxs-lookup"><span data-stu-id="aba70-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="aba70-305">Individuare il tag &lt;Grid&gt; con il nome **gridStreamAndBitrateSelection** e aggiungere il codice seguente alla fine del tag:</span><span class="sxs-lookup"><span data-stu-id="aba70-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="aba70-306">Premere **CTRL+S** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="aba70-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="aba70-307">**Per modificare il file code-behind**</span><span class="sxs-lookup"><span data-stu-id="aba70-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="aba70-308">In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.</span><span class="sxs-lookup"><span data-stu-id="aba70-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="aba70-309">All'interno dello spazio dei nomi SSPlayer, aggiungere una nuova classe:</span><span class="sxs-lookup"><span data-stu-id="aba70-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="aba70-310">All'inizio della classe MainPage aggiungere le seguenti definizioni di variabili:</span><span class="sxs-lookup"><span data-stu-id="aba70-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="aba70-311">All'interno della classe MainPage aggiungere l'area seguente:</span><span class="sxs-lookup"><span data-stu-id="aba70-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="aba70-312">Individuare il metodo mediaElement_ManifestReady e aggiungere il codice seguente alla fine della funzione:</span><span class="sxs-lookup"><span data-stu-id="aba70-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="aba70-313">All'interno della classe MainPage, individuare l'area degli eventi clic dei pulsanti dell'interfaccia utente e aggiungere la seguente definizione di funzione:</span><span class="sxs-lookup"><span data-stu-id="aba70-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="aba70-314">**Per compilare e testare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="aba70-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="aba70-315">Premere **F6** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="aba70-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="aba70-316">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aba70-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="aba70-317">Nella parte superiore dell'applicazione, è possibile utilizzare l'URL di Smooth Streaming predefinito o immetterne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="aba70-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="aba70-318">Fare clic su **Imposta origine**.</span><span class="sxs-lookup"><span data-stu-id="aba70-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="aba70-319">Per impostazione predefinita, tutte le tracce del flusso video sono selezionate.</span><span class="sxs-lookup"><span data-stu-id="aba70-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="aba70-320">Per sperimentare le diverse velocità in bit, è possibile selezionare la velocità in bit più bassa e quella più alta tra quelle disponibili.</span><span class="sxs-lookup"><span data-stu-id="aba70-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="aba70-321">Dopo ogni modifica, è necessario fare clic su Invia.</span><span class="sxs-lookup"><span data-stu-id="aba70-321">You must click Submit after each change.</span></span>  <span data-ttu-id="aba70-322">Sarà quindi possibile visualizzare le modifiche alla qualità del video.</span><span class="sxs-lookup"><span data-stu-id="aba70-322">You can see the video quality changes.</span></span>

<span data-ttu-id="aba70-323">La lezione 4 è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aba70-323">You have completed lesson 4.</span></span>  <span data-ttu-id="aba70-324">In questa lezione è stata aggiunta la funzionalità per la selezione delle tracce.</span><span class="sxs-lookup"><span data-stu-id="aba70-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="aba70-325">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="aba70-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aba70-326">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="aba70-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="aba70-327">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="aba70-327">Other Resources:</span></span>
* [<span data-ttu-id="aba70-328">Come creare un'applicazione Smooth Streaming per Windows 8 in JavaScript con funzionalità avanzate</span><span class="sxs-lookup"><span data-stu-id="aba70-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="aba70-329">Panoramica tecnica relativa a Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="aba70-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

