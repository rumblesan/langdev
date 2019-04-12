---
title: "Beginning Trax"
date: 2019-04-08T16:20:01+01:00
description: Outline for the development of the Trax environment
tags:
- trax
---

Trax is going to be a fairly minimal, live-coding language, initially just for creating acid bass lines.  Quickly after getting the initial version working I want to add drums and effects, but to begin with it's purely about the bass.

## Language

The language I have in mind is heavily influenced by Ixi lang, Tidal, and Gibber, with a simple example of what I'm after looking like this.

```
scale minor
tonic 60
octave -2

make synth1 tb303

play synth1 [1^ 4 1*2^\ 4 1\ 1 ~ ]
```

This is entirely likely to change in the future, but it should serve as a good starting point. The `scale` and `tonic` behaviour is pulled from Ixi lang, and realistically I think it will probably stay like this. At some point I expect `octave` to become a parameter specific to the instruments and synths, but this functionality will be OK for the moment.

Where Ixi creates agents with a name and can then change the instrument that agent uses, I prefer the idea of explicitly creating a named synthesizer and then manipulating it in a fashion similar to Gibber. Whether that continues to happen through using them as arguments to functions, or methods on the objects remains to be seen.

The part that I'm most wanting to explore is the pattern generation. In this example, the 303 instanced called `synth1` is given an explicit pattern to play.
The pattern has 7 events, with the default timing of an event corresponding to a 16th note. The `^` symbol means that we accent the note, the `\` means the note will slide into the next, the `*2` doubles the length, and the `~` is a rest. The numbers refer to the interval in the scale we defined, with respect to the tonic note.
So this pattern should be eight 16th notes in length. The first note is accented. The third note is twice as long as the others, accented and sliding into the fourth. The fifth note also slides into the sixth, and the pattern has a 16th note rest at the end.

## Architecture

Despite it being simple, there's going to be quite a few moving parts.

* A Parser
* An Interpreter
* A Sequencer/Scheduler
* A Synthesiser
* An Editor plug-in

The synthesiser engine will be written in SuperCollider, with the note information being sent to it over OSC. The parser, interpreter, and sequencer will all be written in JavaScript. The editor used will be Atom, because it's easy to build plug-ins for and it can run the JavaScript code internally.

Each of these will be the simplest thing it can be to get everything working.

Having just recently built a re-implementation of Ixi lang, I'm going to be using the same patterns of interaction between the components as well. The Interpreter will run code and return one or more `Actions`. The Atom plug-in will be responsible for turning these into either OSC messages sent to SuperCollider, or performing editor specific actions, such as highlighting text.

## Next Steps

The specifics of building these components are going to be on their own pages, which can all be found under the [Trax](/tags/trax) tag.

