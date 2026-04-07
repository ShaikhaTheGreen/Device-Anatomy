# Device Anatomy

**🔗 Live demo:** https://shaikhathegreen.github.io/Device-Anatomy/

An interactive 3D explorer for the inner workings of modern computing devices — laptops, desktops, tablets, and phones — built as a single-file web app using [Three.js](https://threejs.org/).

Designed and used in **ISC230 — IT Infrastructure** at the College of Life Sciences, Department of Information Sciences, Kuwait University. The tool is explicitly aligned with Andrew S. Tanenbaum & Todd Austin, *Structured Computer Organization*, **6th edition** (Pearson). Every component tooltip cites the exact chapter and figure in that book so students can open the explorer alongside the textbook.

## What it does

Pick a real device from the catalog:

- MacBook Air M2 (2022)
- MacBook Pro 14″ M3 Pro
- Dell XPS 13 (2024)
- Dell XPS 15 9530
- ThinkPad X1 Carbon Gen 11
- HP Pavilion 15 (2024)
- HP Spectre x360 14
- ASUS ZenBook 14 UX3405
- Surface Laptop 5
- Acer Swift 3 SF314
- Surface Pro 9 (tablet)
- XOTIC PC GX13 (gaming desktop)
- iPhone 15 Pro

The viewer reconstructs each device with accurate proportions, brand details, and component layout, then lets students:

- **Explode the layers** — separate the bottom case, battery, logic board, CPU/GPU package, thermal system, keyboard, display, and memory units to see what's really inside. (Desktops render a glass tower with a metal base; the "display" layer is hidden for form factors without an internal display.)
- **Zoom through five levels of detail** — Laptop → Board → Chip / SoC → Pipeline (Microarch.) → Cell / Digital Logic. The deepest zoom goes all the way down to a DRAM 1T1C memory cell and, below it, symbolic logic gates (NOT, NAND, AND) and a D flip-flop for Tanenbaum Ch. 3.
- **Trace data flows** — pick a source and destination component (CPU ↔ RAM, CPU ↔ SSD, GPU → Display, Battery → PMIC → CPU, CPU → Thermal, etc.). The matched flow draws a live tube between the actual components, with intermediate hops labeled (PMIC, eDP connector, IHS, etc.) and bandwidth-modulated particles showing relative throughput.
- **Click any component** for an info panel with the component name, what it does, the **Tanenbaum 6e chapter and figure** it maps to, the unit / week / CLO / lab in the ISC230 syllabus, and a real-world analogy.
- **Open the Tanenbaum 6-Layer Model overlay** from the sidebar button to see how the physical 3D view lines up with Tanenbaum's abstraction stack from Ch. 1.1 Fig. 1-2 (Digital Logic → Microarchitecture → ISA → Operating System Machine → Assembly → Problem-Oriented Language).
- **Connect peripherals** (printer, monitor, USB drive, external SSD) and watch the IRQ → CPU → ACK animation that models how an interrupt is serviced.
- **Click any port** (HDMI, SD card slot, 3.5 mm audio jack, USB-A, USB-C / Thunderbolt, MagSafe, Surface Connect, Ethernet) for a port-specific tooltip rather than a generic USB fallback.

## Why it exists

Most students see computing devices as black boxes. This tool turns the abstract block diagrams in Tanenbaum into a thing they can rotate, take apart, and click on — and it ties every component back to the exact CLO, lab, and textbook chapter the syllabus uses to assess it.

## Run it

It's a single HTML file with no build step.

```bash
# Option 1: open directly
open index.html

# Option 2: serve locally (some browsers block file:// for textures)
python3 -m http.server 8000
# then visit http://localhost:8000
```

Modern Chrome / Firefox / Safari / Edge with WebGL2 enabled.

## Controls

| Action | How |
|---|---|
| Orbit | Left-drag |
| Pan | Right-drag *or* on-screen pan pad |
| Zoom | Scroll *or* pinch |
| Explode layers | Sidebar slider, or `Explode All` / `Assemble` |
| Toggle a layer | Click its chip in the Layers row |
| Change zoom level | Sidebar pills (Laptop → Board → Chip/SoC → Pipeline → Cell / Digital Logic) |
| Open Tanenbaum 6-layer overlay | 📚 button under Zoom Level |
| Show a flow | Flow Builder: pick `From` + `To`, click `Show Path` |
| Clear flows | `Clear` button |
| Inspect a part | Click any mesh in the 3D view |
| Connect a peripheral | Drag from the dock (bottom-right) onto the device |
| Resize the sidebar | Drag the vertical handle on its right edge (keyboard: ←/→ nudge, `Home` reset, double-click reset). Width is persisted in `localStorage`. |

## Course mapping

Every component carries metadata for:
- **Tanenbaum chapter and figure** in *Structured Computer Organization*, 6th ed.
- **Unit** in the ISC230 course plan
- **Week** of the semester
- **CLO** (Course Learning Outcome) it supports
- **Lab** it is exercised in
- **Analogy** — a plain-language comparison students can build a mental model around

### Tanenbaum 6e chapter coverage

The explorer is aligned component-by-component with the following chapters:

| Tanenbaum Ch. | Topic | What to open in the tool |
|---|---|---|
| **Ch. 1.1** | Levels of a computer (Fig. 1-2) | 📚 Tanenbaum 6-Layer Model overlay |
| **Ch. 2.1** | Processors — control unit, ALU, registers | Chip / SoC zoom: click Control Unit, ALU, Registers |
| **Ch. 2.2** | Primary memory — main memory, cache hierarchy | Chip / SoC zoom: click Main Memory (RAM), L1/L2/L3 Cache |
| **Ch. 2.3** | Secondary memory — SSD, HDD | Board zoom: click Secondary Storage (NVMe SSD) |
| **Ch. 2.4** | I/O — keyboard, display, ports, NIC | Board zoom: click any port or the NIC |
| **Ch. 3.1–3.3** | Digital logic — gates, flip-flops, memory chips, decoders | Cell / Digital Logic zoom: gates, D flip-flop, DRAM cell, row decoder, sense amps |
| **Ch. 4.1** | Mic-1 data path (Fig. 4-1) | Pipeline zoom: ALU + Register File + inter-stage wiring |
| **Ch. 4.4** | 5-stage pipelining (Fig. 4-34) | Pipeline zoom: IF → ID → EX → MEM → WB |
| **Ch. 6.1** | Virtual memory, paging, TLB | Chip / SoC zoom: click MMU / TLB (on top of the Memory Controller) |

Components that exist in modern hardware but are **not** covered by Tanenbaum 6e (P-cores / E-cores, NPU, PMIC, EC, IHS, BGA, GPU shader cores, MagSafe, Surface Connect) are tagged with a "⚠ Not in Tanenbaum 6e" marker in their tooltip so students don't waste time hunting for them in the index.

This makes the explorer usable as a study aid (students click → see exactly which lecture, lab, and textbook chapter to revisit) and as a lecture prop (instructor opens the relevant device, explodes the relevant layer, traces the relevant flow).

## Status

Actively used as a teaching tool. Built and refined iteratively against student questions and assessment data.

## License

MIT — see [LICENSE](LICENSE).

## Author

**Dr. Shaikhah Alkhadhr**
Faculty, College of Life Sciences — Department of Information Sciences
Kuwait University
