# HD20: a 3D-printable 20:1 harmonic drive actuator

> ### Superseded by the [HDP30](https://github.com/robrotics/hdp30)
>
> The [HDP30](https://github.com/robrotics/hdp30) gets **30:1** out of the same
> NEMA 17 face and the exact same bill of materials, in a thinner stack. If
> you're starting a new build, start there.
>
> **But read this first:** the HD20 is still the only revision we have put on a
> load cell. The HDP30 has no torque, efficiency or backlash data yet. If you
> need a number you can defend, build this one. Nothing here is going away:
> the files, the BOM and the test report all stay up.
>
> Build page: [robrotics.web.app/archive/hd20](https://robrotics.web.app/archive/hd20)


A strain-wave (harmonic) gearbox that bolts onto a standard NEMA 17 stepper,
prints on a bog-standard bed slinger, and costs about **$4 of hardware** per
unit. Tested to **3.3 N·m**.

![HD20, exploded](photos/hd17-exploded.jpeg)

| | |
|---|---|
| **Reduction** | 20:1 |
| **Tooth profile** | Cycloidal, module 0.8 |
| **Measured torque** | 2.1-2.6 N·m @ 0.7 A · 3.0-3.3 N·m @ 1.4 A (peak 3.5 N·m) |
| **Efficiency** | 48-58% |
| **Backlash** | measurement in progress |
| **Motor** | Any NEMA 17 with a 5 mm shaft (tested: [OMC 17HE12-1204S](https://www.omc-stepperonline.com/e-series-nema-17-bipolar-26ncm-36-82oz-in-1-2a-42x42x30mm-4-wires-w-1m-cable-connector-17he12-1204s), 26 N·cm, 1.2 A) |
| **Lubrication** | Super Lube synthetic PTFE grease |
| **Printed parts** | 10 pieces across 9 unique parts, including 2 shear pins |
| **Fasteners** | 8 × M3×0.5 × 6 mm button head screws per drive |
| **Hardware cost** | ~$3.96 per actuator |
| **Version** | v1.0 (RevA, 2026-08-09) |
| **License** | [CC BY-SA 4.0](LICENSE) |

> **Testing is ongoing.** The numbers above come from the load-cell runs in
> [`docs/torque-test-report.html`](docs/torque-test-report.html). We're in the
> middle of revising the test method, so expect these figures to be updated.
> Read the honest caveats in [Known behaviour](#known-behaviour) before you
> build.

---

## How it works

Three parts do the work. A **wave generator**, an ellipse riding on 11 loose
5 mm balls in a printed cage, pushes a flexible toothed ring (the
**flexspline**) into an oval, so its teeth engage a rigid ring (the **circular
spline**) at just two points. The circular spline has two more teeth than the
flexspline, so one turn of the motor walks the output around by two teeth. That
tiny slip per revolution is the 20:1.

New to strain-wave gearing? We wrote a plain-language explainer:
**[robrotics.web.app/learn](https://robrotics.web.app/learn)**.

The tooth profile came out of our own free generator,
**[the harmonic maker](https://robrotics.web.app/gearmaker)**. You can use it
to make profiles for your own drives.

## What you need

**Not included in the BOM, bring your own:**

- A **NEMA 17 stepper with a 5 mm shaft**. We tested with an
  [OMC StepperOnline 17HE12-1204S](https://www.omc-stepperonline.com/e-series-nema-17-bipolar-26ncm-36-82oz-in-1-2a-42x42x30mm-4-wires-w-1m-cable-connector-17he12-1204s)
  (42 × 42 × 30 mm, 26 N·cm, 1.2 A, 4-wire) under closed-loop FOC control; an
  open-loop stepper on a basic driver will behave differently.
- **4 × M3 screws** to bolt the motor to the interface plate. These are
  separate from the 8 × M3×0.5 × 6 mm screws that hold the drive together,
  which are in the BOM.
- A **soldering iron** for the heat-set inserts, and hex keys.

**Filament:** PLA for everything except the flexspline, which must be **PETG**.

> ⚠️ **Do not print the flexspline in PLA.** It flexes on every single
> revolution. PLA has almost no fatigue life in that duty and will crack.

## Bill of materials

Machine-readable source: [`bom.json`](bom.json).

| # | Item | Qty | Pack | Pack cost | Per actuator |
|---|------|-----|------|-----------|--------------|
| 1 | M3 heat-set inserts | 12 | 100 | $9.99 | $1.20 |
| 2 | M3×0.5 × 6 mm button head, stainless | 8 | 100 | $7.69 | $0.62 |
| 3 | 30 × 42 × 7 mm bearing | 1 | 10 | $16.39 | $1.64 |
| 4 | Set screw | 1 | 50 | $5.69 | $0.11 |
| 5 | 5 mm steel bearing balls | 11 | 200 | $7.20 | $0.40 |
| 6 | Super Lube synthetic grease | 1 | - | - | - |
| | | | | **$46.96 buy-in** | **$3.96 each** |

One tube of grease lasts many builds, so it isn't counted in the per-unit cost.

Parts are sold in packs, so the first actuator costs about $47 in hardware and
every one after that costs about $4, and you'll have enough left over for
eight more.

> **Affiliate disclosure:** the purchase links in `bom.json` and on our website
> are Amazon Associates links. If you buy through one, Robrotics earns a small
> commission at no extra cost to you. Every part listed is what we actually
> used; the links don't change the recommendation.

## Printed parts

| Part | Qty | Material | File |
|---|---|---|---|
| Circular spline (base) | 1 | PLA | `hd17-circular-spline-base` |
| Circular spline (output) | 1 | PLA | `hd17-circular-spline-output` |
| Base preloader | 1 | PLA | `hd17-base-preloader` |
| Output preloader | 1 | PLA | `hd17-output-preloader` |
| Interface / motor mount | 1 | PLA | `hd17-interface` |
| Wave generator | 1 | PLA | `hd17-wave-generator` |
| Ball cage | 1 | PLA | `hd17-cage` |
| **Flexspline** | 1 | **PETG** | `hd17-flexspline-petg` |
| Shear pin | **2** | PLA | `hd17-shear-pin` |

**Both shear pins are required.** They carry shear load across the output joint
directly, so the connection doesn't have to rely on friction from the preloaded
screws to resist it. The screws clamp; the pins take the sideways load.

### Print settings

The tested units were printed on a **Bambu Lab P1S** with **Bambu PLA** (and
PETG for the flexspline), using:

- **Arachne** variable-width wall generator
- **One extra wall loop** for strength
- **Seam position: random**, on every part, so a single seam line doesn't stack
  up into a weak spot or a visible ridge on the round surfaces
- **Supports on the output circular spline and the interface.** Everything else
  prints unsupported.

No custom temperatures, no special bed prep.

## Files

```
cad/step/          STEP, for CAD work and remixing
docs/              Load-cell torque test report
photos/            Build photos
bom.json           Bill of materials (source of truth)
```

Grab the packaged bundles from the
[Releases page](https://github.com/robrotics/hd17/releases) rather than
cloning, because the STEP files are large.

## Assembly

📹 **An assembly video is on the way** and it'll be posted to
[youtube.com/@robrotics](https://www.youtube.com/@robrotics) and linked here.

Written step-by-step instructions are being written up alongside it.

## Make your own version

The full parametric model is public on Onshape:

**[Open the HD20 in Onshape →](https://cad.onshape.com/documents/77afb05fe79876b7e72eef9d/w/f63b8b9736de29d04fb7333a/e/ae0695e56e320ee36980ab83)**

Copy it to your own workspace and change what you like: a different motor
face, a different output interface, a different ratio. If you build a variant,
we'd genuinely like to see it: open an issue or tag
[@robrotics](https://www.instagram.com/robrotics).

## Known behaviour

Read this before you conclude you assembled it wrong.

- **Torque drops about 10% after running in.** A freshly printed unit measured
  2.32 N·m; the same unit after further running measured 2.08 N·m at 0.7 A.
  This is expected, so plan around the run-in figure, not the fresh one.
- **Output spline preload changes everything.** Further tightening the output
  spline took one unit from 2.37 to 2.55 N·m. It's the single biggest tuning
  knob you have.
- **Unit-to-unit variation is real.** Two units of the same design differed by
  up to 18% at the same current. Printed gearboxes are not precision parts.
- **Efficiency is 48-58%**, so roughly half your motor torque becomes heat.
  Size the motor accordingly.
- **PLA creeps under sustained load.** Holding a heavy static load for hours
  will slowly deform the circular splines.
- **The 1.4 A figures are above the test motor's rating.** The 17HE12-1204S is
  rated 1.2 A, so the 3.0-3.3 N·m numbers were measured over-driven. Treat them
  as a short-burst ceiling, not a continuous rating. At 1.4 A that motor gets
  hot.

Found something we haven't listed? Please
[open an issue](https://github.com/robrotics/hd17/issues) and include your
version, filament, and printer.

## Test data

[`docs/torque-test-report.html`](docs/torque-test-report.html) is a standalone
page with the full load-cell traces: 7 configurations, ~1500-3000 samples each,
100 mm lever arm, raw counts scaled to N·m, with a no-gearbox baseline for the
efficiency maths. Open it in a browser.

## License

[CC BY-SA 4.0](LICENSE). Use it, change it, sell it. Just credit Robrotics and
share your derivatives under the same license.

**No warranty.** Printed parts fail. Don't put this anywhere a failure could
hurt someone.
