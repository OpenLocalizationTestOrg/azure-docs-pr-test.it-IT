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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Come tooBuild un'applicazione Smooth Streaming Windows Store

Hello Smooth Streaming Client SDK per Windows 8 consente agli sviluppatori toobuild le applicazioni Windows Store in grado di riprodurre contenuto Smooth Streaming in tempo reale e su richiesta. Riproduzione di base toohello di Smooth Streaming di contenuto, hello SDK inoltre fornisce inoltre funzionalità avanzate come protezione Microsoft PlayReady, restrizione del livello di qualità, Live DVR, flusso audio di commutazione, in attesa per gli aggiornamenti di stato (ad esempio, le modifiche a livello di qualità ) e gli eventi di errore e così via. Per altre informazioni di funzionalità hello supportato, vedere hello [note sulla versione](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Per ulteriori informazioni, vedere [Player Framework per Windows 8](http://playerframework.codeplex.com/). 

In questa esercitazione vengono presentate quattro lezioni:

1. Creare un'applicazione Windows Store Smooth Streaming di base
2. Aggiungere un dispositivo di scorrimento tooControl hello supporti lo stato di avanzamento
3. Selezionare flussi Smooth Streaming
4. Selezionare tracce Smooth Streaming

## <a name="prerequisites"></a>Prerequisiti
* Windows 8 a 32 o 64 bit. È possibile scaricare la [versione di valutazione di Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) da MSDN.
* Visual Studio 2012 o Visual Studio Express 2012 (o versione successiva). È possibile ottenere una versione di valutazione di hello da [qui](http://www.microsoft.com/visualstudio/11/downloads).
* [Microsoft Smooth Streaming Client SDK per Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

soluzione Hello completato per ogni lezione può essere scaricato da esempi di codice per sviluppatori MSDN (raccolta codici): 

* [Lezione 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : semplice lettore multimediale Smooth Streaming per Windows 8 
* [Lezione 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : semplice lettore multimediale Smooth Streaming per Windows 8 con controllo per la barra del dispositivo di scorrimento 
* [Lezione 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : lettore multimediale Smooth Streaming per Windows 8 con selezione flusso  
* [Lezione 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907): lettore multimediale Smooth Streaming per Windows 8 con selezione traccia.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Lezione 1: Creare un'applicazione Windows Store Smooth Streaming di base

In questa lezione si creerà un'applicazione Windows Store con un controllo MediaElement tooplay Smooth Streaming del contenuto.  simile a un'applicazione Hello in esecuzione:

![Esempio di applicazione Windows Store Smooth Streaming][PlayerApplication]

Per ulteriori informazioni sullo sviluppo di app di Windows Store, vedere il sito relativo allo [sviluppo di app di Windows Store per Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). In questa lezione contiene hello seguire le procedure seguenti:

1. Creare un progetto Windows Store
2. Interfaccia utente di progettazione hello (XAML)
3. Modificare hello file code-behind
4. Compilare e testare un'applicazione hello

**toocreate un progetto Windows Store**

1. Eseguire Visual Studio 2012 o versione successiva.
2. Da hello **FILE** menu, fare clic su **New**, quindi fare clic su **progetto**.
3. Dalla finestra di dialogo Nuovo progetto hello, tipo o seleziona hello seguenti valori:

| Nome | Valore |
| --- | --- |
| Gruppo dei modelli di progetto |Installato/Modelli/Visual C#/Windows Store |
| Modello |Applicazione vuota (XAML) |
| Nome |SSPlayer |
| Percorso |C:\SSTutorials |
| Nome soluzione |SSPlayer |
| Crea directory per soluzione |(selezionata) |

1. Fare clic su **OK**.

**tooadd toohello un riferimento Smooth Streaming Client SDK**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **SSPlayer**, quindi scegliere **Aggiungi riferimento**.
2. Digitare o selezionare hello seguenti valori:

| Nome | Valore |
| --- | --- |
| Gruppo di riferimenti |Windows/Estensioni |
| riferimento |Selezionare Microsoft Smooth Streaming Client SDK per Windows 8 e Microsoft Visual C++ Runtime Package. |

1. Fare clic su **OK**. 

Dopo l'aggiunta di riferimenti hello, è necessario selezionare una piattaforma di destinazione hello (x64 o x86), aggiunta di riferimenti non funzionerà per la configurazione di piattaforma qualsiasi CPU.  In Esplora soluzioni verrà visualizzato un simbolo di avviso giallo per i riferimenti aggiunti.

**interfaccia utente di Windows Media player hello toodesign**

1. In Esplora soluzioni fare doppio clic su **MainPage. XAML** tooopen nella progettazione di hello visualizzare.
2. Individuare hello  **&lt;griglia&gt;**  e  **&lt;/Grid&gt;**  tag hello file XAML e codice di esempio hello Incolla tra i tag hello due:

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
   
   controllo MediaElement Hello è tooplayback utilizzato. controllo dispositivo di scorrimento Hello denominato sliderProgress verrà utilizzato in corso di hello prossima lezione toocontrol hello media.
3. Premere **CTRL + S** file hello toosave.

controllo MediaElement Hello non supporta Smooth Streaming del contenuto out-of-box. supporto di Smooth Streaming hello tooenable, è necessario registrare il gestore di hello Smooth Streaming-flusso di byte dall'estensione di file e il tipo MIME.  tooregister, metodo hello MediaExtensionManager.RegisterByteStremHandler dello spazio dei nomi Windows.Media hello.

In questo file XAML, sono associati ai controlli hello alcuni gestori di eventi.  Sarà quindi necessario definire tali gestori di eventi.

**toomodify hello file code-behind**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. All'inizio di hello del file hello, aggiungere hello istruzione using:
   
        using Windows.Media;
3. All'inizio di hello di hello **MainPage** classe, aggiungere hello dopo il membro di dati:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Alla fine hello hello **MainPage** costruttore, aggiungere hello due righe seguenti:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Alla fine hello hello **MainPage** classe, incollare hello seguente codice:
   
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

gestore dell'evento sliderProgress_PointerPressed Hello è definito qui.  Esistono altre opere toodo tooget lo stesso risultato, che verrà trattato in una lezione successiva di hello di questa esercitazione.
6. Premere **CTRL + S** file hello toosave.

Hello hello termine file code-behind è simile al seguente:

![Visualizzazione del codice dell'applicazione Windows Store Smooth Streaming in Visual Studio][CodeViewPic]

**applicazione hello toocompile e test**

1. Da hello **compilare** menu, fare clic su **Configuration Manager**.
2. Modifica **piattaforma soluzione attiva** toomatch la piattaforma di sviluppo.
3. Premere **F6** progetto hello toocompile. 
4. Premere **F5** toorun un'applicazione hello.
5. Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso. 
6. Fare clic su **Imposta origine**. Poiché **AutoPlay** è abilitata per impostazione predefinita, hello media deve essere eseguito automaticamente.  È possibile controllare il supporto di hello utilizzando hello **riprodurre**, **pausa** e **arrestare** pulsanti.  È possibile controllare il volume di supporti hello con dispositivo di scorrimento verticale hello.  Tuttavia hello dispositivo di scorrimento orizzontale per controllare lo stato di avanzamento di supporto non è completamente implementato ancora hello. 

La lezione 1 è stata completata.  In questa lezione, si utilizza un tooplayback controllo MediaElement contenuto Smooth Streaming.  Nella lezione successiva hello, si aggiungerà un dispositivo di scorrimento toocontrol hello lo stato di avanzamento di hello contenuto Smooth Streaming.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Lezione 2: Aggiungere un dispositivo di scorrimento tooControl hello supporti lo stato di avanzamento

Nella lezione 1, creato un'applicazione Windows Store con un tooplayback controllo MediaElement XAML Smooth Streaming di contenuti multimediali.  che include alcune funzionalità multimediali di base, come l'avvio, l'arresto e la sospensione della riproduzione.  In questa lezione si aggiungerà un'applicazione di toohello dispositivo di scorrimento della barra di controllo.

In questa esercitazione si utilizzerà una posizione di scorrimento timer tooupdate hello in base alla posizione corrente di hello di hello controllo MediaElement.  dispositivo di scorrimento Hello inizio e fine ora anche toobe necessario aggiornare in caso di contenuti live.  Questa può essere gestita meglio nell'evento di aggiornamento di hello origine adattivo.

Le origini multimediali sono oggetti che generano dati multimediali.  resolver di origine Hello accetta un URL, un flusso di byte e crea un'origine multimediale appropriato hello per il contenuto.  resolver di codice sorgente Hello è modalità standard di hello per le origini di hello applicazioni toocreate media. 

In questa lezione contiene hello seguire le procedure seguenti:

1. Registrare il gestore di Smooth Streaming hello 
2. Aggiungere gestori di eventi a livello di hello origine adattivo manager
3. Aggiungere gestori eventi a livello di origine adattivo hello
4. Aggiungere i gestori di eventi MediaElement
5. Aggiungere il codice relativo alla barra del dispositivo di scorrimento
6. Compilare e testare un'applicazione hello

**propertyset hello gestore e passare tooregister hello Smooth Streaming-flusso di byte**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. All'inizio di hello del file hello, aggiungere hello istruzione using:

        using Microsoft.Media.AdaptiveStreaming;
3. Inizio hello della classe MainPage hello, aggiungere hello membri dati seguenti:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Inside hello **MainPage** costruttore, aggiungere hello seguente codice dopo hello **questo. Inizializzare Components();**  riga e righe di codice di registrazione hello scritte nella lezione precedente hello:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Inside hello **MainPage** costruttore modificare via di hello tooadd metodi RegisterByteStreamHandler di hello due parametri:

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
6. Premere **CTRL + S** file hello toosave.

**gestore eventi a livello di tooadd hello origine adattivo manager**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. Inside hello **MainPage** classe, aggiungere hello dopo il membro di dati:
   
     private AdaptiveSource adaptiveSource = null;
3. Alla fine hello hello **MainPage** classe, aggiungere hello seguente gestore eventi:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Alla fine hello hello **MainPage** costruttore, aggiungere hello evento open origine adattivo toohello toosubscribe riga seguente:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Premere **CTRL + S** file hello toosave.

**gestori eventi a livello di origine adattivo tooadd**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. Inside hello **MainPage** classe, aggiungere hello dopo il membro di dati:
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. Alla fine hello hello **MainPage** classe, aggiungere hello gestori di eventi seguente:

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
4. Alla fine hello hello **mediaElement AdaptiveSourceOpened** metodo, aggiungere hello eventi toohello toosubscribe di codice seguente:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Premere **CTRL + S** file hello toosave.

Hello stessi eventi sono disponibili in adattivo gestione livello di origine, che può essere utilizzato per la gestione delle funzionalità comuni tooall elementi multimediali in app hello. Ogni elemento AdaptiveSource include i relativi eventi e tutti gli eventi AdaptiveSource vengono propagati in AdaptiveSourceManager.

**gestori di eventi tooadd elemento multimediale**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. Alla fine hello hello **MainPage** classe, aggiungere hello gestori di eventi seguente:

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
3. Alla fine hello hello **MainPage** costruttore, aggiungere hello eventi toohello toosubscript di codice seguente:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Premere **CTRL + S** file hello toosave.

**dispositivo di scorrimento tooadd correlato codice a barre**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. All'inizio di hello del file hello, aggiungere hello istruzione using:
      
        using Windows.UI.Core;
3. Inside hello **MainPage** classe, aggiungere hello membri dati seguenti:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Alla fine hello hello **MainPage** costruttore, aggiungere hello seguente codice:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Alla fine hello hello **MainPage** classe, aggiungere hello seguente codice:

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
>CoreDispatcher è usato toomake modifiche toohello dell'interfaccia utente del thread dal Thread dell'interfaccia utente non. In caso di colli di bottiglia nel thread del dispatcher, consentire allo sviluppatore dispatcher toouse fornito dall'elemento dell'interfaccia utente che ha intenzione di tooupdate.  ad esempio:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Alla fine hello hello **mediaElement_AdaptiveSourceStatusUpdated** metodo, aggiungere hello seguente codice:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Alla fine hello hello **MediaOpened** metodo, aggiungere hello seguente codice:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Premere **CTRL + S** file hello toosave.

**applicazione hello toocompile e test**

1. Premere **F6** progetto hello toocompile. 
2. Premere **F5** toorun un'applicazione hello.
3. Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso. 
4. Fare clic su **Imposta origine**. 
5. Barra di scorrimento hello di test.

La lezione 2 è stata completata.  In questa lezione è stato aggiunto un tooapplication dispositivo di scorrimento. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Lezione 3: Selezionare flussi Smooth Streaming
Smooth Streaming è contenuto in grado di supportare toostream con tracce audio in più lingue selezionabili per visualizzatori hello.  In questa lezione si abiliterà flussi tooselect visualizzatori. In questa lezione contiene hello seguire le procedure seguenti:

1. Modificare i file XAML hello
2. Modificare file behand del codice hello
3. Compilare e testare un'applicazione hello

**file XAML di hello toomodify**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.
2. Individuare &lt;Grid. RowDefinitions&gt;e modificare hello RowDefinitions in modo che il seguente aspetto:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Inside hello &lt;griglia&gt;&lt;/Grid&gt; tag, aggiungere hello di codice seguente toodefine un controllo listbox, in modo gli utenti possono visualizzare hello elenco di flussi disponibili e selezionare flussi:

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
4. Premere **CTRL + S** modifiche hello toosave.

**toomodify hello file code-behind**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. All'interno dello spazio dei nomi SSPlayer hello, aggiungere una nuova classe:
   
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
3. Inizio hello della classe MainPage hello, aggiungere hello definizioni di variabili seguenti:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. All'interno di hello classe MainPage, aggiungere hello area seguente:
   
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
5. Individuare il metodo mediaElement_ManifestReady hello, accodare hello seguente codice alla fine di hello della funzione hello:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Pertanto quando MediaElement manifesto è pronto, codice hello Ottiene un elenco di flussi disponibili hello e popola una casella di riepilogo dell'interfaccia utente di hello con elenco hello.
6. All'interno di hello classe MainPage, individuare i pulsanti dell'interfaccia utente di hello fare clic su area di eventi e quindi aggiungere hello seguente definizione di funzione:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**applicazione hello toocompile e test**

1. Premere **F6** progetto hello toocompile. 
2. Premere **F5** toorun un'applicazione hello.
3. Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso. 
4. Fare clic su **Imposta origine**. 
5. lingua predefinita Hello è audio_eng. Provare a tooswitch tra audio_eng e audio_es. Ogni volta che, si seleziona un nuovo flusso, è necessario fare clic su pulsante Submit hello.

La lezione 3 è stata completata.  In questa lezione, aggiungere i flussi toochoose funzionalità hello.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Lezione 4: Selezionare tracce Smooth Streaming
Una presentazione Smooth Streaming può contenere più file video codificati con livelli di qualità (velocità in bit) e risoluzioni diversi. In questa lezione si abiliterà utenti tooselect tracce. In questa lezione contiene hello seguire le procedure seguenti:

1. Modificare i file XAML hello
2. Modificare file behand del codice hello
3. Compilare e testare un'applicazione hello

**file XAML di hello toomodify**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza finestra di progettazione**.
2. Individuare hello &lt;griglia&gt; tag con nome hello **gridStreamAndBitrateSelection**, accodare hello seguente codice alla fine di hello del tag hello:
   
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
3. Premere **CTRL + S** toosave modifica

**toomodify hello file code-behind**

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **MainPage.xaml**, quindi scegliere **Visualizza codice**.
2. All'interno dello spazio dei nomi SSPlayer hello, aggiungere una nuova classe:
   
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
3. Inizio hello della classe MainPage hello, aggiungere hello definizioni di variabili seguenti:
   
        private List<Track> availableTracks;
4. All'interno di hello classe MainPage, aggiungere hello area seguente:
   
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
5. Individuare il metodo mediaElement_ManifestReady hello, accodare hello seguente codice alla fine di hello della funzione hello:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. All'interno di hello classe MainPage, individuare i pulsanti dell'interfaccia utente di hello fare clic su area di eventi e quindi aggiungere hello seguente definizione di funzione:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**applicazione hello toocompile e test**

1. Premere **F6** progetto hello toocompile. 
2. Premere **F5** toorun un'applicazione hello.
3. Nella parte superiore di hello di un'applicazione hello, è possibile utilizzare predefinito hello URL di Smooth Streaming o immetterne uno diverso. 
4. Fare clic su **Imposta origine**. 
5. Per impostazione predefinita, tutte le tracce di hello del flusso video hello sono selezionate. le modifiche apportate alla frequenza di bit tooexperiment hello, è possibile selezionare hello più bassa velocità in bit disponibili e quindi selezionare hello più alta velocità in bit disponibili. Dopo ogni modifica, è necessario fare clic su Invia.  È possibile visualizzare le modifiche della qualità video hello.

La lezione 4 è stata completata.  In questa lezione si aggiungere hello funzionalità toochoose tracce.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Altre risorse:
* [Come toobuild un'applicazione di Smooth Streaming Windows 8 JavaScript con le funzionalità avanzate](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Panoramica tecnica relativa a Smooth Streaming](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

