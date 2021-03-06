## Gibber ##

Gibber is a live coding environment for the web browser, using the Gibberish audio engine and the CodeMirror code editor.
It runs in Chrome, Firefox and nightly builds of Safari.

Below is a code sample. To test out Gibber, visit http://www.charlie-roberts.com/gibber

``` javascript
Gibber.setBPM(180);     // default = 120. You can also refer to Gibber as _g.

s = Sine(240, .25);     // Sine wave with freq 240, amp .5.

s.fx.add(               // create an fx chain for oscillator                   
    Clip(50),           // Soft-Clip Distortion
    Delay(_16)          // Delay with delay time set to 1/4 of a beat (1/16th note)
);

a = Arp("C2m7", _16, "updown", 3); // Arpeggiator: Cminor7 chord in 2nd octave, 16th notes, up then down, 3 octave range

d = Drums("x*o-x*o-", _8);

d.chain( Crush(6) );

d.pitch = 2;     // play drum sapmles at twice their normal pitch

s.mod("frequency", LFO(8, 4), "+");  // Vibrato - modulating frequency by +/- 4Hz 8 times per second
s.removeMod(0);

a.shuffle();        // randomize arpeggio
a.reset();          // reset arpeggio

Master.fx.add( Schizo(), Reverb() ); // Master FX are applied to summed signal of all generators
Master.removeFX(0);                  // remove first effect in chain. don't pass a argument to remove all fx.
```

Gibber also relies on Sink.js, audiofile.js, require.js and jQuery for functionality. Note that for drum samples to work the 
sample locations in drums.js must be changed.