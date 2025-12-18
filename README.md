# Terminal Velocity

**Terminal Velocity** is a hyper-performance, native music sequencer that reimagines the traditional "Piano Roll" as a cascading "Matrix Rain" data stream.

Built entirely in **Rust**, it bypasses the browser and OS bloat to leverage the GPU for massive particle systems and the CPU for sub-millisecond audio latency. It is designed for electronic musicians and visualists who require precision, speed, and immersive aesthetics.

## ⚡ Concept

In **Play Mode**, the sequencer is a generative art installation. MIDI notes fall like code in a terminal.
In **Edit Mode**, the rain freezes. The falling glyphs become editable data nodes, allowing you to manipulate Note, Velocity, CC, and Duration directly within the data stream.

## 🚀 Tech Stack (The "Bare Metal" Approach)

This project rejects web technologies (DOM, GC, JavaScript) in favor of a pure systems-level architecture to ensure zero visual stutter and rock-solid timing.

* **Core Language:** [Rust](https://www.rust-lang.org/) (Memory safety without Garbage Collection).
* **Graphics Engine:** [WGPU](https://wgpu.rs/) (WebGPU Native).
* Runs on **Vulkan** (Windows/Linux), **Metal** (macOS), or **DX12**.
* Uses **Compute Shaders** to handle particle physics on the GPU, leaving the CPU free for audio.


* **Audio Backend:** [cpal](https://github.com/RustAudio/cpal).
* Low-level access to the audio device (DAC).
* Runs on a dedicated high-priority thread to prevent blocking.


* **UI Layer:** [egui](https://github.com/emilk/egui).
* Immediate Mode GUI written in Rust.
* No DOM, no HTML. The UI is rendered as a texture within the game loop (60Hz+).


* **Architecture:** [Bevy ECS](https://bevyengine.org/) (Entity Component System).
* Data-oriented design allows processing 10,000+ falling notes simultaneously with minimal CPU cache misses.



## 🎛 Features

* **Vertical Sequencer Flow:** Time flows from top to bottom.
* **Matrix Rain Visualization:** Each MIDI event is a glowing character glyph.
* **Live Editing:** Modify the "code" (notes) while the sequence runs.
* **Multi-Channel Support:** Unlimited tracks/layers defined by X-axis position.
* **MIDI Out / OSC:** Drives external hardware synths or DAW VSTs.
* **Procedural Visuals:** Visual intensity reacts to Velocity and Note density.

## 🛠 Architecture Overview

The application runs on two primary execution contexts to ensure audio stability:

1. **The Audio Thread (Real-time priority):**
* Cycles at hardware sample rate (e.g., 44.1kHz).
* Reads from a lock-free Ring Buffer.
* Strictly no memory allocation during playback to avoid pops/clicks.


2. **The Main/Render Thread:**
* Handles Input (Mouse/Keyboard).
* Runs the ECS Systems (Physics, Logic).
* Dispatches Compute Shaders to the GPU.
* Draws the UI overlay via `egui`.



## 📦 Building from Source

**Prerequisites:**

* [Rust Toolchain](https://rustup.rs/) (latest stable)
* Vulkan SDK (Windows/Linux) or Xcode Command Line Tools (macOS)

```bash
# Clone the repository
git clone https://github.com/frangedev/terminal-velocity.git
cd terminal-velocity

# Run in Release mode (CRITICAL for audio performance)
# Debug builds will be too slow for real-time DSP
cargo run --release

```

## 🗺 Roadmap

* [ ] **Core:** Basic WGPU render loop & Windowing.
* [ ] **Audio:** Integration of `cpal` and basic MIDI clock.
* [ ] **Visuals:** Instanced mesh rendering for "Glyphs" (The Rain).
* [ ] **UI:** `egui` integration for track selection.
* [ ] **Editor:** Mouse interaction (Click to add/remove glyphs).

## 👤 Author

**Mehmet T. AKALIN**

* **GitHub:** [makalin](https://github.com/makalin)
* **Company:** [Digital Vision](https://dv.com.tr)
* **LinkedIn:** [Mehmet T. AKALIN](https://www.linkedin.com/in/makalin/)
* **X / Twitter:** [@makalin](https://x.com/makalin)

---

*Licensed under the MIT License.*
