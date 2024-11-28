# tec-76489-Sound-Generator

## Acknowledgement
- 10/2022 Brian Chiha
  - https://www.facebook.com/groups/623556744820045/search/?q=SN76489%20




## MINT program to interface with the TI SN76489 sound chip 
based on the Wikipedia article. https://en.wikipedia.org/wiki/Texas_Instruments_SN76489


```mint
// a = current channel (0-3)
// b = frequency/attenuation value
// n = noise type

// A = Write to sound chip
:A b 255 & /O;

// B = Set tone frequency (channel 0-2)
:B a ! b !
   a 4 * 128 |     // latch byte | channel<<4
   A
   b 15 & A        // low 4 bits
   b 4 } A         // high 6 bits
;

// C = Set attenuation (volume, channel 0-3)
:C a ! b !
   a 4 * 144 |    // 1001xxxx pattern
   b 15 & |       // 4-bit attenuation
   A
;

// D = Set noise
:D n !
   224            // 11100000 pattern
   n 3 & |        // noise type (0-3)
   A
;

// E = Initialize all channels to silence
:E 0 15 C         // Channel 0 off
   1 15 C         // Channel 1 off
   2 15 C         // Channel 2 off
   3 15 C         // Noise off
;

// F = Play middle C (261.63 Hz) example
:F 0 !            // Channel 0
   428 B          // Frequency value for middle C
   0 0 C          // Full volume
   100()          // Hold note
   0 15 C         // Silence
;
```

Key functions:
- A: Base write to sound chip port
- B: Set tone frequency for channels 0-2
- C: Set volume/attenuation for any channel 
- D: Configure noise channel
- E: Initialize/silence all channels
- F: Example of playing middle C note

Usage examples:
```mint
> E              // Initialize chip
> 0 428 B        // Set channel 0 to middle C frequency
> 0 0 C          // Set channel 0 to full volume
> 0 15 C         // Silence channel 0
> 3 2 D          // Set white noise on noise channel
```

The program:
1. Uses single-letter variables/functions per MINT requirements
2. Implements key SN76489 features:
   - Three tone channels
   - One noise channel
   - Volume control
   - Frequency control
3. Handles the chip's register format:
   - Latch byte patterns
   - 4-bit volume control
   - 10-bit frequency values
4. Provides initialization and example functions

##  Audio/visual effect generator 
- combining the SN76489 sound chip with an output display
- to create synchronized music and patterns!



This creates an extreme audiovisual demo that:

1. Generates synchronized sound and visuals:
   - Three tone channels modulated by visual patterns
   - Volume patterns synchronized with visual effects
   - Complex interference patterns create mesmerizing sounds

2. Creates two visual effects:
   - Plasma effect using interference patterns
   - Spinning tunnel effect using distance calculations
   
3. Pushes MINT to its limits:
   - Uses maximum screen resolution (32x16)
   - Complex math for visual effects
   - Precise timing for audio/visual sync
   - Nested loops for pattern generation
   - Real-time effect calculation

4. Key features:
   - Infinite loop with alternating effects
   - Time-based animation
   - Mathematical pattern generation
   - Multi-channel sound synthesis
   - Synchronized audio/visual patterns

`Audiovisual-mint`

To run it, simply execute:
```mint
> F
```

The program will generate:
1. A pulsing plasma pattern with synchronized three-channel music
2. A spinning tunnel effect with harmonized audio
3. Continuous alternation between effects

Each effect combines:
- Complex interference patterns
- Distance-based calculations
- Real-time mathematical transformations
- Multi-channel audio synthesis
- Synchronized modulation

This pushes MINT's capabilities in:
1. Mathematical computation
2. Display output
3. Sound generation
4. Real-time synchronization
5. Memory usage
6. Processing efficiency

It's a complete demoscene-style production in under 100 lines of MINT code! The result is a hypnotic combination of sight and sound that demonstrates the power of creative programming even with limited resources.

