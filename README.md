# Touchdesigner Audioreact love (EN)

**On how to generative audio-reactive visuals with TouchDesigner.**

Inspired by tutorials from [Bileam Tschepe](https://www.youtube.com/@elekktronaut) and [PPPANIK](https://www.youtube.com/@pppanik2040).

## Audio-reactive setup

We can open a sound file with an `Audio File In` CHOP, or listen to the sound from the mic of your computer with an `Audio Device In` CHOP.

If we want to listen to music from Youtube or Spotify or whatever, we need to install another software that will allow us to create a virtual audio cable in the computer, so the sound can go in TouchDesigner instead of out of the speakers.

## Spectre sonore en visuel

 There is a thousand ways to generate visuals with sound. My favorite way at the moment it to do it with the frequencies spectrum.

So after the `Audio Device In` CHOP, link an `Audio Spectrum` CHOP outputting in a `Chop to` TOP.

 ![screen de Touch](./images/screen6.png)

We can play with the parameters in the `Audio Spectrum`, to boost high frequencies for example, or add audio parameters CHOPs before, but I don't do it.

In the `Chop to` TOP, choose "RG" as Data Format. 
The two channels from left and right become red and green values.

So we have a strip of 1 pixel where the frequencies appear in red or green depending of the stereo pan, or in yellow by additive mixing.
The intensity of the color depends of the height of the strip on the frequency on the spectrum.

To transform this strip of colors in an full-sized image, we create a `Constant` TOP with a black background, and we give it a resolution of 1080*1920.

We create a `Composite` TOP in output of the `Constant` TOP, and we add the `CHOP to` TOP to the `Composite`.

 ![screen de Touch](./images/screen7.png)

We therefore have a full-sized image wih the frequencies in colors depending of the stereo, that we can then modify and improve.

 ![screen de Touch](./images/gif1.gif)
 *The piano part in the intro of "Tout Le Monde" of Neniu*

 ![screen de Touch](./images/gif2.gif)
 *The beginning of "I'm Not In Love" of 10cc, where we see the bass in yellow on the left.*

 ![screen de Touch](./images/gif3.gif)
 *The moment where the sound is moving in the stereo panning in "Ridin" of Cordon, where we can see the frequencies going from green to red to green.*

 ## Analyse audio dans Touchdesigner

 TouchDesigner a un node dédié à l'analyse audio, mais la qualité de l'analyse varie énormément en fonction des sons.

 ![screen de Touch](./images/gif4.gif)
*"Doudou" de Aya Nakamura* 

Dans le dossier "Tools" de la Palette, on récupère le node `audioAnalysis`.
![screen de Config audio et MIDI](./images/screen9.png)

blablbla tous les paramètres
![screen de Config audio et MIDI](./images/screen10.png)

blabla les sorties
![screen de Config audio et MIDI](./images/screen11.png)

### Virtual audio cable audio in mac OS
I personally use [BlackHole](https://existential.audio/blackhole/) with Mac.

Open the application `Audio and MIDI configuration` in the Application > Utilitaires folder.

![screen de Config audio et MIDI](./images/screen1.png)

In the app, click on `Create a multiple output`.

![screen de Config audio et MIDI](./images/screen2.png)

Check "BlackHole (2ch)".

![screen de Config audio et MIDI](./images/screen3.png)

In TouchDesigner, create an `Audio Device In` CHOP and select "BlackHole (2ch)" as Device.

![screen de Config audio et MIDI](./images/screen4.png)

Create an `Audio Device Out` CHOP in output, and select "Built-In Output" as Device, so the sound goes out of the sound output of the coomputer.

![screen de Config audio et MIDI](./images/screen5.png)

The sound from the computer goes in BlackHole, then in TouchDesigner from BlackHole, and then in the sound output (speakers or headphones) : sound > BlackHole > TouchDesigner > sound output.

The best way is to put the sound at the maximum on the source (Spotify, etc) and lower it after in the `Audio Device Out` CHOP.

We could also check "Built In Output" in the multiple output in the Audio and MIDI config app, so the sound output in BlackHole and in the sound output from the computer so it would go : sound > BlackHole > TouchDesigner + sound > sound output.
But as TouchDesigner sometimes looses FPS, I want the music to stay synchro with my visual even when it slows down.

![schema](./images/schemaEN.png)

 ### Virtual audio cable in windows

Same way but with [Virtual Audio Cable](https://vb-audio.com/Cable/), Elekktronaut did a tutorial video rencently : ["Internal Audio to TouchDesigner"](https://www.elekktronaut.com/tutorials/internal-audio-to-touchdesigner).


## To go further

- The [intro to Touchdesigner](https://github.com/LucieMrc/IntroTD) (EN).

- The tuto [Feedback loop in TD](https://github.com/LucieMrc/TD_feedback_love_EN) (EN).s