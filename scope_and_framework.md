# Scoping Maritime Robotic Simulation, and a Framework for Assessing It

Working discussion document for the OCEANS 2026 Monterey *OCEANSSim* workshop. This is a draft for refinement with co-organizers and contributors.

It has two parts:

1.  **Scope.** What we mean by "maritime robotic simulation," and — just as important — what we *don't* mean. The goal is a clear, defensible bounding box around the discussion so that the roadmap and white paper are about one thing.
2.  **A common description framework.** A shared way to describe and compare past, present, and future projects, so the community builds a common understanding and its priorities become explicit.

------------------------------------------------------------------------

## Part 1 — Scope: what is maritime robotic simulation?

### 1.1 A working definition (proposed)

This is a *working* definition, not a formal one — concrete enough to refine together, and detailed enough that a reader can hold a candidate project up against it and decide whether it is what this workshop is about.

> **Maritime robotic simulation** is development-time software that stands in for a physical marine robot and its environment so that the robot's own autonomy software can be developed, tested, and trained against it. It presents the vehicle's navigation, guidance, control, perception, and planning stack with the same interfaces the real hardware exposes, so the autonomy stack (e.g., sensing, perception, navigation, decision-making) runs unmodified and cannot tell it is not talking to real sensors and actuators. It covers (at least) underwater, water surface, air, and land domains in one shared world. Its purpose is iterative testing of autonomy software to support development: iteratively exercising the surrogate robot and autonomy components under test so that the integrated system can be engineered, tuned, and — where the approach is machine learning — trained.

(By *development-time* we mean the tool is used while the autonomy software is being built, tested, and trained — not fielded alongside the deployed system in operations. Run-time, operational use (digital twins, onboard predictive models) is a different category, drawn out in 1.4.)

The iterative-testing loop is the same whether a human or an algorithm does the learning. In the classical style, developers run the surrogate robot again and again and *they* learn how to engineer, integrate, and tune the system. The machine-learning style (ML/RL) is the same loop run orders of magnitude more times, with the simulator as an online, closed-loop environment (and, offline, a generator of labeled synthetic data). Both need the *same category* of simulation, so we do not split them; learning simply adds one requirement — scaling to large, vectorized environments (e.g., Isaac Lab on Isaac Sim). We carry that as a scale requirement in Part 2 (C2), not a separate kind of simulator.

The scope test has two tiers. The three **gates** are categorical — a project is maritime robotic simulation only if it meets all three. The two **priorities** are not gates: strongly desired and weighted heavily, but treated as matters of degree.

**Gates:**

1.  **For the autonomy developer.** The customer is the team writing the vehicle software — not a naval architect, an acoustician, or an operational planner.
2.  **A stand-in for the robot.** The real autonomy stack runs against it unmodified (software- or hardware-in-the-loop); the sim speaks the robot's own interfaces (e.g., MAVLink, LCM, ROS 2 / DDS, etc.).
3.  **Multi-domain.** It can represent at least underwater, surface, aerial, and terrestrial assets, and ideally lets them coexist and interact in a single world with common robotic conventions (coordinate frame standards, etc.)

**Priorities:**

1.  **A usable, extensible, well-supported project.** A small team can stand it up, extend it, and depend on it: clear documentation and stable APIs, a way to add vehicles, sensors, and scenes without fighting the tool, and dependable support — community, professional, or both.
2.  **Built upon a shared foundation.** It rides the general-purpose robotics and simulation infrastructure that industry and academia already fund; the marine community contributes only a thin marine-specific layer — the pieces no neighbor domain funds for us (hydrodynamics, underwater sensing, long-endurance / faster-than-real-time execution; see Part 2, C2). Maritime budgets cannot build or sustain a bespoke stack, so the viable models ride that larger investment: a foundation-governed open robotics substrate (ROS 2 / Gazebo), free-to-use or source-available industry engines (Unreal, Isaac Sim), and open standards as glue. A maritime silo — government-owned (GOTS) or closed single-vendor — is ruled out, however polished, because we cannot fund its upkeep.

### 1.2 Overview

"Simulation" is a huge word, and several things wear the name without being the subject of this workshop. The rest of Part 1 draws the workshop's bounding box by placing our category against its neighbors along **three axes of distinction**. On each axis the same machinery can sit on either side — so it is the axis (the *question being asked*), not the technology, that decides what belongs in our category:

- **Subject axis** — *what is modeled, and for whom?* (1.3)
- **Timing axis** — *when does the model run?* (1.4)
- **Decision axis** — *what is the result used to decide?* (1.5)

Section 1.6 then collects the exclusions these axes imply.

### 1.3 The subject axis: What is modeled and for whom?

The first axis is *what is modeled, and for whom.* It places autonomy simulation between two neighbors often confused with it, because each answers a different question for a different person — a spectrum from *deep models of few physical domains* to *broad models of many aggregated entities*.

|   | **Engineering / domain simulation** | **Autonomy / robotics simulation** *(us)* | **Mission / campaign simulation** |
|------------------|------------------|------------------|------------------|
| Question it answers | "Will this physical design or phenomenon behave as predicted?" | "Will this autonomy *software* behave correctly on the real robot?" | "Which force mix, resource allocation, or CONOPS wins?" |
| Primary user | Domain engineer (naval architect, acoustician, RF/network engineer) | Autonomy developer (the software team) | Operational analyst, planner, warfighter |
| Fidelity focus | One or a few physical domains, modeled deeply and validated | The *whole robot* — dynamics, sensors, environment — with "enough" fidelity in each | Aggregated platforms, behaviors, and C2; low physical fidelity |
| Validation target | Agreement with physics / tank / field measurement | Sim-to-real: the same software transfers to hardware | Plausible force-on-force / campaign outcomes |
| Scale (space, time) | Component to single vehicle; seconds to hours of physics | Vehicle to small team; a mission's duration | Many platforms, theater-wide; hours to a campaign |
| Runs the real autonomy stack? | No — it *models* a subsystem | **Yes — unmodified, SITL/HITL** | No — behaviors are surrogate models |
| Typical output | An engineering design decision or a validated model | Tested and tuned autonomy software; trained ML/RL policies; synthetic data | Resource allocation; CONOPS / CONEMPS |
| Maritime examples | LAMP, NavaSim, WEC-Sim (seakeeping/hydro); Bellhop/acoustic; ns-3/network; CFD | VRX, DAVE, HoloOcean, OceanSim, Stonefish, MBARI LRAUV sim | Campaign / wargaming models, AFSIM-class tools |
| Cross-domain analogues | Ansys, Simulink plant models | CARLA, AirSim, Isaac Sim | Constructive military simulations |

Two clarifications that keep this from being a false trichotomy:

- **The boundary is about purpose and the "for whom," not fidelity.** A very high-fidelity sonar model is engineering simulation when its purpose is to design a transducer, and autonomy simulation when its purpose is to let a perception stack run unmodified. The same physics can appear in more than one category.
- **The categories are not mutually exclusive.** An autonomy simulator *consumes* engineering models as components — a hydrodynamics model, a sonar model, an acoustic-propagation model can each be a plugin inside the autonomy sim. And an autonomy simulator can in turn *feed* a mission simulation (as a higher-fidelity model of one platform).

For orientation within the defense M&S vocabulary: the DoD's [Live / Virtual / Constructive taxonomy](https://en.wikipedia.org/wiki/Live,_virtual,_and_constructive) cuts a different way (how much real hardware and how many real humans are in the loop). Our category spans **virtual** (human-in-the-loop operator/dev use) and **constructive** (headless, automated CI and ML training) but is defined by *the autonomy developer as the customer*, which LVC does not capture. We mention LVC only so the white paper can be bilingual with sponsors.

### 1.4 The timing axis: When does the model run? (twins vs. cousins)

The subject axis (1.3) sorts by *what is modeled*. The **timing axis** sorts by *when the model runs*, and it separates our development-time category from operational digital twins and the predictive uses built on them — very similar machinery, but run at operational run time. Our own tools sit on the development side; their internal models are digital *cousins* (below). This axis matters especially to naval audiences, who tend to reach for the twins first.

- **Digital twins.** A high-fidelity, instance-specific model kept in step with a real asset — this hull, this vehicle, often the surrounding environment too (an *environmental twin* of currents, weather, acoustics) — for monitoring, diagnostics, prognostics, and lifecycle management. One level down is a specific use: running the twin *forward* to predict, so a shared predicted picture (the environmental twin optionally assimilating fleet data) can substitute for scarce inter-vehicle communication — the Ferrell-and-Sheridan predictive-display lineage (IEEE Spectrum, 1967; [predictive displays for delayed links](https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2020.578805/full)), where the model stands in for missing *communication*, not missing *hardware*. General or predictive, the defining feature is a live tie to specific real units at run time, its customer the operator or fleet — exactly what an autonomy-development sim does not need. A neighbor, not our tool.
- **Digital cousins.** Autonomy development deliberately does *not* use twins. It uses *digital cousins*: simplified, generic, often deliberately varied models that are "good enough" to exercise the autonomy components and, crucially, are not bound to one physical unit. They are cheaper, they generalize, and diversity across many of them is what makes autonomy robust — the same instinct as domain randomization ([Dai et al., "Automated Creation of Digital Cousins," CoRL 2024](https://arxiv.org/abs/2410.07408) shows policies trained on cousins out-transferring those trained on twins). The target is fidelity-to-purpose, not a faithful twin — which shapes the fidelity discussion in Part 2.

Naming these keeps the scope clear and gives Navy stakeholders a clean map of where our tool sits relative to the twins and predictive models they already invest in. The one-line summary: we build development-time sims whose internal models are digital *cousins*; we are not building operational twins or the predictive, fleet-informed uses built on them.

### 1.5 The decision axis: What is the result used to decide? (T&E / V&V / RDT&E)

Where the subject axis (1.3) sorts by *what is modeled* and the timing axis (1.4) by *when the model runs*, the **decision axis** sorts by *what the result is used to decide*. Our category is a development tool — it helps a team build and tune autonomy. A different, acquisition-facing use of simulation is as evidence in the Test & Evaluation and Verification & Validation of a **system or capability**: does this system or capability meet its requirements well enough to certify, buy, or field? The same machinery can appear on both sides, but the customer and the burden of proof are different.

- **Different customer.** The audience is the program office, the operational test authority, or the capability sponsor — not the autonomy developer. That alone puts it outside Gate 1 of the scope test in 1.1.
- **A higher burden of proof.** To stand as acquisition evidence, the simulation itself has to be *accredited* (the VV&A discipline): characterized fidelity with known error bounds, traceability to requirements, coverage of the operational envelope, statistical rigor, and independence from the developers. That is the opposite pressure from our good-enough digital-cousin philosophy (1.4) — assurance has to know exactly *how wrong* the model is.
- **Usually several sim categories, composed.** Capability-level V&V typically stitches together accredited engineering models (subsystem performance), a development/robotics sim like ours (autonomy behavior), and mission / campaign sims (operational effectiveness), plus instrumented live / hardware-in-the-loop and threat representation. It reaches across the whole 1.3 spectrum, not just our slice.

So acquisition T&E/V&V is a *consumer* of simulation that can incorporate *robotic* simulation as one contributing model, but it also needs credibility features outside this scope.

### 1.6 What is explicitly out of scope

The in-scope test is the three gates and two priorities in 1.1. Its mirror image is the set of neighbors we deliberately exclude — while still depending on some of them as *components* or *references*:

- Single-domain **engineering codes** — naval-architecture / seakeeping suites, standalone acoustic or CFD or RF/network simulators. These matter to us as validation references and as plug-in physics, not as the tool under discussion.
- **Mission / campaign / wargaming** simulations — important for CONOPS and resource decisions, a different audience and altitude.
- **Acquisition T&E / V&V of systems and capabilities** — simulation used as accredited evidence in RDT&E / acquisition decisions (Part 1.5). Our development sim can feed it but is not itself that tool; same machinery, different customer, a much higher burden of proof.
- **Digital twins (and their predictive, fleet-informed uses)** — high-fidelity operational replicas, and the predictions run forward from them for fleet situational awareness (Part 1.4). Same machinery, different customer, different moment (run time, not development time).
- One-off academic **prototypes** with no sustained user base (already excluded by the proposal's criteria; noted in the lit review's "excluded and adjacent").

------------------------------------------------------------------------

## Part 2 — A common description framework

The purpose of the framework is to give workshop participants a common rubric and a shared understanding, and to help project leads describe their projects in a common framing. Concretely, it does two things:

- **Categorize** a project (what kind of simulation is this, and what does it cover?), and
- **Evaluate** it against the capabilities the community needs, so that priorities become explicit.

The framework has two layers: a short **descriptive profile** (Part 2.1) and a **capability rubric** (Part 2.2) scored on a common maturity scale.

### 2.1 Descriptive profile (place the project)

Neutral, factual axes — no judgment, just where the project sits. These mirror the comparison axes used in the recent [underwater-simulator survey (Aldhaheri et al., 2025)](https://arxiv.org/abs/2504.06245) and the [open-source autonomous-driving simulator review (Li et al., 2023)](https://arxiv.org/abs/2311.11056), adapted to our multi-domain scope.

- **Category** — autonomy sim / engineering sim / mission sim (from Part 1). We only consider the autonomy sims; the others are recorded as references.
- **Substrate / engine** — Gazebo, Unreal, Unity, Isaac Sim / Omniverse, standalone, etc.; physics engine and rendering engine.
- **Domains covered** — underwater / surface / air / land, and whether they can coexist and interact in one world.
- **Middleware / interface** — LCM, ROS 1, ROS 2 / DDS, YARP, native API, Python.
- **Autopilot / stack integration** — PX4, ArduPilot, MOOS-IvP, custom; SITL/HITL support.
- **License** — and, for closed-engine tools, whether the *marine-specific layer* is itself open.
- **Sensor suite** — camera, depth, IMU/INS, DVL, GPS/GNSS, imaging/multibeam/side-scan sonar, acoustic comms/USBL, lidar, event/thermal, etc.
- **Maintenance signal** — last release, commit cadence, releases on current OS / ROS, packaging (binaries, Docker), CI.
- **Adoption signal** — stars, citations, external user base, whether use extends beyond maritime.

### 2.2 Capability rubric (evaluate the project)

Six capability areas, each scored on the same maturity scale. These are written as *what an autonomy developer needs from the tool*, so a project's scores double as a statement of the community's priorities.

Maturity scale for every item:

| Score | Meaning |
|------------------------------------|------------------------------------|
| **0 — Absent** | Not supported. |
| **1 — Partial** | Present but limited, undocumented, or requires source-diving / forking to use. |
| **2 — Working** | Supported and documented well enough for a new small team to use as-is. |
| **3 — Mature** | Robust, validated/tested, and relied on in production by users outside the originating group. |

#### C1 — Multi-domain coverage

Can it represent underwater, surface, terrestrial, and aerial assets — and can they operate and interact in a single shared world?

#### C2 — Fidelity-to-purpose across the use cases

Fidelity is not one number; it is "enough fidelity in the right places for the job." We track it against the four use cases the tool has to serve — the same four named in the literature review — because each stresses it differently, with (d) the maritime staple worth calling out:

- **(a) In-the-loop development & operator training** — rendering, asset availability, ergonomics; interactive.
- **(b) Headless CI regression testing** — deterministic, reproducible, fast enough to gate merges, stable across OS/dependency upgrades, packaged.
- **(c) Vectorized ML training** — steps per wall-second across many parallel worlds, GPU acceleration, deterministic resets, Python-native.
- **(d) Mission-plan validation** — running a full mission end to end to catch faults in the *plan* (grounding, collision, energy- or time-budget blowouts, contingency-logic errors, missed comms windows) *before* it goes in the water. Its signature requirement is faster-than-real-time, long-horizon, deterministic execution.

Use case (d) exposes a broader pattern: some requirements are generic robotics (the shared substrate provides them), and some are maritime-distinctive (the thin marine layer must add them — the shared-foundation bargain of Priority 2). Marine missions run tens of hours to weeks and range over tens to hundreds of kilometers, where aerial and most ground missions run minutes to hours over short ranges. So faster-than-real-time execution, long-horizon numerical stability, and streaming very large environmental datasets (bathymetry, terrain, current fields too big to hold in memory) are ours to own — as are the hard underwater sensors below (sonar, DVL, acoustics). These are the burdens the short-range neighbor domains largely avoid.

And across three fidelity sub-axes, scored per relevant domain:

- **Dynamics / hydrodynamics** (added mass, damping, currents, waves, contact).
- **Sensors** (esp. the maritime-hard ones: sonar, DVL, acoustic comms).
- **Environment / rendering** (water column, optical attenuation, sea state, bathymetry/terrain). Note the maritime inversion of the usual priority: photorealistic rendering of optical-camera imagery matters far less here than in ground or aerial sim — optical cameras are short-range underwater and only modestly useful at the surface, so fidelity effort belongs with acoustic and range-based sensing, not with photorealism.

#### C3 — Autonomy-stack integration & interoperability

Does the *real* autonomy software run against it unmodified (SITL/HITL), through standard interfaces (ROS 2 / DDS) and standard autopilots (PX4, ArduPilot, MOOS-IvP)?

**The interoperability principle (a proposed community stance):** maritime robotics should *not* build simulation tooling that is usable only for maritime. It should ride on the same substrate the ground, aerial, and manipulation communities use (ROS 2, Gazebo/Isaac, PX4/ArduPilot, standard message and scene formats), and contribute the marine-specific pieces (hydrodynamics, acoustics, underwater sensors) *upstream* into that shared substrate. Reinventing general-purpose robotics infrastructure with a maritime-only flavor is how the community has repeatedly paid for very expensive wheels twice. A common core also assists our community workforce as maritime is another application on equal footing with bipedal robots, self-driving vehicles, etc.; by adapting common tools developer talent can move more smoothly across domains, enabling more talent to delve into maritime.

#### C4 — Extensibility & modifiability

Can a small team (not associated with the developers) add vehicles (ocean, terrestrial, and aerial), a sensor, an environment, or a behavior *without forking the core*? Look for a documented plugin/extension architecture, open and standard formats for vehicles/sensors/scenes (SDF, URDF, USD, OpenSCENARIO-class scenario description), and an asset pipeline. Extensibility is what lets a shared tool serve many groups instead of one.

#### C5 — Project health & usability by small teams

The proposal's core inclusion test, expressed as a capability. Can a small independent team adopt and sustain the tool with the resources it has?

- **Open license** usable for the community's downstream needs (note GPL vs permissive; note closed-engine EULAs inherited at runtime).
- **Documentation** good enough to stand the tool up *without reading the source*.
- **Active support** — maintained forum/chat, responsive maintainers, release cadence.
- **Packaging & CI** — binaries/Docker, reproducible installs, tests.
- **Governance / sustainability** — is there a path beyond a single grant or a single lab? (This is the crux of the white-paper argument about federated one-off funding.)

#### C6 — Sim-to-real evidence & validation

Is there published or demonstrated evidence that autonomy developed against the sim transfers to hardware, and are there benchmarks / reference scenarios to measure the gap? The surveys are consistent that the field's biggest missing piece is standardization and benchmarking — the same gap that recent community efforts such as the [AQ²UASIM workshop (ICRA 2025)](https://sites.google.com/view/aq2uasim/) set out to close.