# Device Anatomy

**🔗 Live demo:** https://shaikhathegreen.github.io/Device-Anatomy/

An interactive 3D explorer for the inner workings of modern computing devices — laptops, desktops, tablets, and phones — built as a single-file web app using [Three.js](https://threejs.org/).

Designed and used in **ISC230 — IT Infrastructure** at the College of Life Sciences, Department of Information Sciences, Kuwait University.

## What it does

Pick a real device from the catalog (MacBook Air M2, MacBook Pro M3 Pro, Dell XPS 13, ThinkPad X1 Carbon, HP Pavilion 15, HP Spectre x360, ASUS ZenBook 14, Surface Laptop 5, Acer Swift 3, Xotic GX13, Surface Pro 9, custom desktop tower, iPhone 15 Pro). The viewer reconstructs each device with accurate proportions, brand details, and component layout, then lets students:

- **Explode the layers** — separate the bottom case, battery, logic board, CPU/GPU package, thermal system, keyboard, display, and memory units to see what's really inside.
- **Zoom through five levels of detail** — from the whole device → board → chip / SoC → CPU pipeline → individual memory cell.
- **Trace data flows** — pick a source and destination component (CPU ↔ RAM, CPU ↔ SSD, GPU → Display, Battery → PMIC → CPU, CPU → Thermal, etc.). The matched flow draws a live tube between the actual components, with intermediate hops labeled (PMIC, eDP connector, IHS, etc.) and bandwidth-modulated particles showing relative throughput.
- **Click any component** for an info panel with the textbook name, what it does, units, the chapter / week / CLO it maps to, the lab it appears in, and a real-world analogy.
- **Connect peripherals** (printer, monitor, USB drive, external SSD) and watch the IRQ → CPU → ACK animation that models how an interrupt is serviced.

## Why it exists

Most students see computing devices as black boxes. This tool turns the abstract block diagrams in the lecture slides into a thing they can rotate, take apart, and click on — and it ties every component back to the exact CLO and lab the syllabus uses to assess it.

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
| Change zoom level | Sidebar pills (Laptop → Board → Chip/SoC → Pipeline → Memory Cell) |
| Show a flow | Flow Builder: pick `From` + `To`, click `Show Path` |
| Clear flows | `Clear Flows` button |
| Inspect a part | Click any mesh in the 3D view |
| Connect a peripheral | Drag from the dock (bottom-right) onto the device |

## Course mapping

Every component carries metadata for:
- **Chapter** in the assigned textbook
- **Week** of the semester
- **CLO** (Course Learning Outcome) it supports
- **Lab** it is exercised in
- **Analogy** — a plain-language comparison students can build a mental model around

This makes the explorer usable as a study aid (students click → see exactly which lecture and lab to revisit) and as a lecture prop (instructor opens the relevant device, explodes the relevant layer, traces the relevant flow).

## Status

Actively used as a teaching tool. Built and refined iteratively against student questions and assessment data.

## License

MIT — see [LICENSE](LICENSE).

## Author

**Dr. Shaikhah Alkhadhr**
Faculty, College of Life Sciences — Department of Information Sciences
Kuwait University
