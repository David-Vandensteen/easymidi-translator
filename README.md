# easymidi-translator

## Overview

This library provides a way to translate MIDI (Musical Instrument Digital Interface) messages from one controller and channel to another.  
Is useful when you want to remap MIDI controls between different devices, allowing for customized MIDI signal routing.

## Features

- Remaps MIDI control change (CC) messages from one channel/controller to another.
- Supports translation of MIDI messages between different MIDI devices.
- Utilizes easymidi, a MIDI library for Node.js, to handle MIDI input and output.

## Install
```cmd
npm i git@github.com:David-Vandensteen/easymidi-translator.git#release/1.0.0
```

## Usage

1. Initialization: Create a new instance of Translator.
2. Define MIDI Inputs/Outputs:
   * Use fromEasymidiInput() to set the MIDI input source.
   * Use toEasymidiOutput() to set the MIDI output destination.
3. Define Channel Translation:
   * Use fromChannel() to specify the source channel.
   * Use toChannel() to specify the destination channel.
4. Define Controller Translation (optional):
   * Use fromController() to specify the source controller.
   * Use toController() to specify the destination controller.
5. Apply the Translation:
   * Call the apply() method to start translating MIDI messages.
   * If both controller translations are defined, the class listens for control change (cc) messages on the source channel/controller and sends them to the specified destination.
  
## Code example
```javascript
import { easymidi, Translator } from 'easymidi-translator';

// Create a new Translator instance
const midiTranslator = new Translator();

// Set the MIDI input and output
midiTranslator
  .fromEasymidiInput(new easymidi.Input('myMidiInputName'))
  .toEasymidiOutput(new easymidi.Output('myMidiOutputName'));

// Define the translation rules
midiTranslator
  .fromChannel(1)
  .toChannel(2)
  .fromController(10)
  .toController(20);

// Apply the translation
midiTranslator.apply();
```

## Important Notes
- Ensure that the MIDI devices you're working with are properly configured and connected.
- Assertions are used throughout the class to ensure correct input and output assignments. If an assertion fails, it indicates incorrect setup or usage.
- The apply() method is the final step to activate the translation. Ensure that all settings are correct before calling this method.
