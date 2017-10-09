<!--author=alkohli last changed:02/22/16-->

#### <a name="tooattach-hello-sas-cables"></a>cavi SAS hello tooattach
1. Identificare hello primario e l'enclosure EBOD hello. enclosure Hello due possono essere identificate analizzando il retro. Hello seguente immagine per istruzioni, vedere. 
   
    ![Vista posteriore dell’enclosure principale e dell’enclosure EBOD](./media/storsimple-sas-cable-8600/HCSBackplaneofprimaryandEBODenclosure.png)
   
    **Vista posteriore dell’enclosure principale e dell’enclosure EBOD**
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Enclosure principale |
   | 2 |Chassis EBOD |
2. Individuare i numeri di serie hello hello primario e l'enclosure EBOD hello. adesivo con il numero di serie Hello viene apposta toohello sporgenza posteriore di ciascuno chassis. numeri di serie Hello devono essere identici in entrambe le enclosure. [Contattare il supporto Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) immediatamente se hello numeri di serie non corrispondono. Vedere la seguente figura i numeri di serie hello toolocate hello.
   
    ![Vista posteriore dell’enclosure con la posizione del numero di serie](./media/storsimple-sas-cable-8600/HCSRearviewofenclosureindicatinglocationofserialnumbersticker.png)
   
    **Posizione dell'etichetta del numero di serie**
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Sporgenza dello chassis hello |
3. Utilizzare hello fornito hello tooconnect tramite cavi SAS enclosure principale toohello di enclosure EBOD, come indicato di seguito:
   
   1. Identificare hello quattro porte SAS sulle enclosure principale hello ed EBOD hello. porte SAS Hello sono contrassegnate come EBOD sull'enclosure principale hello e corrispondono A tooport sull'enclosure EBOD hello, come illustrato nella figura di cablaggio SAS hello, di seguito.
   2. Hello utilizzare fornito SAS cavi tooconnect hello EBOD porta tooport A.
   3. Hello porta EBOD sul controller 0 deve essere connesso toohello porta A sul controller 0 EBOD. Hello porta EBOD sul controller 1 deve essere connesso toohello porta A sul controller 1 EBOD. Hello seguente illustrazione per istruzioni, vedere. 
      
      ![Cablaggio SAS per il dispositivo](./media/storsimple-sas-cable-8600/HCSSAScablingforyourdevice.png)
      
      **Cablaggio SAS**
      
      | Etichetta | Descrizione |
      |:--- |:--- |
      | A |Enclosure principale |
      | B |Chassis EBOD |
      | 1 |Controller 0 |
      | 2 |Controller 1 |
      | 3 |Controller 0 EBOD |
      | 4 |Controller 1 EBOD |
      | 5, 6 |Porte SAS sull'enclosure principale (contrassegnate con la dicitura EBOD) |
      | 7, 8 |Porte SAS sull'enclosure EBOD (Porta A) |

