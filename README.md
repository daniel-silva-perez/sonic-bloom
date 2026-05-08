# Sonic Bloom — Real-Time Audio Visualizer

## Concept
An generative art visualizer that transforms audio into living, breathing particle ecosystems. 
Bass creates gravitational explosions. Mids sculpt flowing currents. Treble paints fine starlight threads.
Every session is unique — seeded by the audio fingerprint itself.

## Tech Stack
- Vanilla JS + Canvas 2D API (no deps, runs anywhere)
- Web Audio API (AudioContext, AnalyserNode, getUserMedia)
- Phase Vocoder for pitch shifting (stretching demo)
- File drag-drop + mic input

## Audio Pipeline
1. Source: microphone (`getUserMedia`) or file (`FileReader` → `decodeAudioData`)
2. `AudioContext.createMediaElementSource()` or `createMediaStreamSource()`
3. `AnalyserNode` (fftSize: 2048 or 4096 for detail)
4. Frequency data → particle physics engine
5. Canvas render loop at 60fps

## Particle System
- 512-1024 particles max (performance budget)
- Each particle: {x, y, vx, vy, hue, size, life, freqBand}
- Frequency bands mapped to particle behavior:
  - Sub-bass (20-60Hz): explosive radial force, large particles
  - Bass (60-250Hz): gravitational pull/ripple
  - Low-mid (250-500Hz): swirling vortices
  - Mid (500-2kHz): flowing streams
  - High-mid (2-6kHz): delicate sparks
  - Treble (6-20kHz): starfield threads

## Color
- Frequency → HSL hue (0=red, 120=green, 240=blue, wraps)
- Energy (RMS amplitude) → saturation + lightness pulse
- Background: deep black with subtle trail fade (fillRect alpha ~0.05)

## Effects
- Bloom: multiple layered canvases with `filter: blur` + additive blend
- Trails: semi-transparent background clear (not full clear)
- Glow: particles with `shadowBlur` proportional to energy
- Centrifuge: bass hits spin the whole field
- Waveform ribbon: draws the raw waveform as a 3D-looking ribbon at bottom

## UI
- Full-viewport canvas, no chrome
- Top-right: minimal controls (mic/file toggle, color mode, intensity slider)
- Bottom: tiny waveform strip
- Click anywhere to spawn burst of particles
- Double-click to toggle controls visibility
- ESC to reset

## Presets
- "Ocean": blue-dominant, smooth, flowing
- "Fire": red-orange, explosive, energetic  
- "Aurora": green-purple, ethereal, wave-like
- "Stardust": white-blue, delicate, sparse
