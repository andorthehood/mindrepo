---
title: Janko MIDI controller with accelerometer velocity
created: 2024-02-19
updated: 2025-11-23
tags: [electronics, midi, janko, idea]
status: draft
summary: Idea for a Janko-layout MIDI controller using keyboard switches and accelerometer-based velocity sensing similar to GarageBand on iPad.
---

# Context
This is an idea for a compact MIDI controller that uses a Janko keyboard layout, keyboard switches, and an accelerometer to estimate key velocity in a way similar to how GarageBand on iPad uses the tablet accelerometer for velocity.

# Content
- Use a Janko key layout to pack more notes into a small physical width and make transposition and scale patterns easier.
- Use mechanical keyboard switches (for example, MX-style switches) as the on/off sensors for each key.
- Build a key matrix that scans all switches with a microcontroller that can present itself as a USB MIDI device.
- Add an accelerometer to the controller so that fast downward motion during a key press increases MIDI velocity, and light, slow motion produces lower velocity.
- Consider either:
  - Mounting the accelerometer rigidly to the whole controller and using the entire device motion as the input, or
  - Mounting accelerometers per key group or per hand area if higher spatial resolution is needed.
- Sample the accelerometer at a high enough rate to capture the motion around the time a key is pressed, and compute velocity from the recent acceleration history.
- Use a ring buffer in firmware to store the last few tens of acceleration samples so that when a key press is detected you can compute velocity from both pre-press and around-press motion.
  - Typical algorithm: on a key transition from UP to DOWN, inspect the ring buffer window from about -10 ms to +10 ms around the event, take the maximum absolute acceleration magnitude in that window, and map it to a MIDI velocity value from 1 to 127.
- Use filtering (for example, a low-pass filter) to remove noise and high-frequency jitter from the accelerometer data.

# Rejected ideas

## True velocity-sensitive mechanical keyboard switches
- Normal mechanical keyboard switches are binary, so they do not provide natural velocity information.
- Analog mechanical switches (for example, Hall effect or optical) exist, but:
  - They are harder to source as bare switches.
  - They usually need a custom PCB and matching sensors.
  - They add a lot of electrical and mechanical complexity.
  - They are not practical for early prototyping.

Verdict: Too complicated and not worth the extra effort for this MIDI controller, especially because the keys do not need full typing-quality mechanics.

## Dual-switch piano-style velocity system
- Use two switches at different heights on each key and measure the time between the two switch events to estimate key travel speed and map it to velocity.
- This approach requires very precise mechanical tolerances and consistent switch travel across all keys.
- Getting reliable timing differences across a full key range (for example, 60–80 keys) is difficult and sensitive to manufacturing variation.
- The extra hardware adds bulk and makes the Janko-style keybed deeper and heavier.

Verdict: Technically possible but mechanically painful and not elegant for this project.

## Per-key analog sensors (Hall effect, optical, FSR, inductive)
- Use one analog sensor per key (for example, Hall effect, optical, force-sensing resistor, or inductive) to measure key position or force continuously and derive velocity from the signal.
- A full keyboard with 60–80 keys would need 60–80 sensors, which means a lot of wiring or an expensive custom PCB.
- Reading that many analog channels needs many ADC inputs or multiplexing, which increases complexity.
- Each sensor would need calibration and ongoing drift handling, which is hard to manage.
- The enclosure and keybed design must make space for all these sensors and keep alignment stable.
- Scanning many analog channels puts a heavier load on the microcontroller compared with a simple switch matrix.

Verdict: Too much hardware and complexity for a lightweight controller.

## Springs under the enclosure
- Mount the entire enclosure on springs so that pressing keys makes the whole box move, increasing the accelerometer signal.
- Springs introduce oscillation, which can cause double triggers or ringing in the accelerometer signal.
- It is hard to control damping well enough to get a clean, single impulse per key press.
- The moving enclosure makes the keyboard feel unstable and less pleasant to play.
- Extra stabilization or mechanical complexity would be needed to make it usable.

Verdict: Rubber bumpers or a firm base are better, because they allow small movement without long oscillation.
