# TD_audioreact_love_EN

**On how to generative audio-reactive visuals with TouchDesigner.**

Inspired by tutorials from [Bileam Tschepe](https://www.youtube.com/@elekktronaut) and [PPPANIK](https://www.youtube.com/@pppanik2040).

## Audio-reactive setup

We can open a sound file with an `Audio File In` CHOP, or listen to the sound from the mic of your computer with an `Audio Device In` CHOP.

If we want to listen to music from Youtube or Spotify or whatever, we need to install another software that will allow us to create a virtual audio cable in the computer, so the sound can go in TouchDesigner instead of out of the speakers.

### Virtual audio cable audio in mac OS
I personally use [SoundFlower](https://soundflower.fr.softonic.com/mac) with Mac.

Open the application `Audio and MIDI configuration` in the Application > Utilitaires folder.

![screen de Config audio et MIDI](./images/screen1.png)

In the app, click on `Create a multiple output`.

![screen de Config audio et MIDI](./images/screen2.png)

Check "Soundflower (2ch)".

![screen de Config audio et MIDI](./images/screen3.png)

In TouchDesigner, create an `Audio Device In` CHOP and select "Soundflower(2ch)" as Device.

![screen de Config audio et MIDI](./images/screen4.png)

Create an `Audio Device Out` CHOP in output, and select "Built-In Output" as Device, so the sound goes out of the sound output of the coomputer.

![screen de Config audio et MIDI](./images/screen5.png)

The sound from the computer goes in SoundFlower, then in TouchDesigner from SoundFlower, and then in the sound output (speakers or headphones) : sound > SoundFlower > TouchDesigner > sound output.

The best way is to put the sound at the maximum on the source (Spotify, etc) and lower it after in the `Audio Device Out` CHOP.

We could also check "Built In Output" in the multiple output in the Audio and MIDI config app, so the sound output in SoundFlower and in the sound output froom the computer so it would go : sound > SoundFlower > TouchDesigner + sound > sound output.
But as TouchDesigner sometimes looses FPS, I want the music to stay synchro with my visual even when it slows down.

 ### Virtual audio cable in windows

Not sure.

 ## Sound to visual

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
