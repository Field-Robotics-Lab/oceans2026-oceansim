# Maritime Robotic Simulation — Project Description Rubric

The purpose of this document is to define a common rubric for characterizing the various maritime robotic simulation projects. There is a set of questions and measurements intended to describe each project based on common, objective aspects of the project. There are both quantitative measures (we can automate many of these) and qualitative descriptions. The goal is explicitly *not* assessment — we recognize that each of these projects fills an ecological niche in the community for compelling historical, technological, programmatic, and proprietary/sensitivity reasons. The purpose of this exercise is to define the landscape of tools, projects, and techniques in order to identify opportunities.

We can collect this information in a variety of ways: by examination (looking at the project and its materials), by looking at metadata (see https://github.com/knmcguire/best-of-robot-simulators), from review papers, etc.

## Projects and Frameworks

We need to set some terminology here so that we can use specific terms for the purposes of this workshop. (These are often cloudy and, if not settled, lead to miscommunication.)

Context-specific glossary:

- Project: A past or present effort to build a cohesive set of simulation capabilities for a particular set of use-cases (missions) and users. A simulation project supports a specific set of decisions. Examples: VRX — a project designed for autonomy developers working on the multi-domain (USV primary, with UAV and UUV additions) mission set described in the RobotX competition guide; it is intended to support the design decisions associated with fielding a complete system of UxS vessels in RobotX-like missions. DAVE — two users: companies developing UUV autonomy to support developer decisions, and the project sponsor who used the tool to support decisions based on the relative technical maturity of their portfolio of performers.  

- Framework: Most (perhaps all?) projects rest on one or more frameworks. VRX and others rest on Gazebo; HoloOcean rests on Unreal.

A common confusion and confound is to mix projects and frameworks when doing these comparisons. Wherever an item below can be asked at either level, tag it [P] for project or [F] for framework.

## Background

* See oceans2026-oceansim/literature_review/lit_review.tex
* [Best of Robot Simulators](https://github.com/knmcguire/best-of-robot-simulators) — automated criteria. Take with a grain of salt. Doesn't differentiate between Project and Framework.

## Rubric brainstorm

The goal here is to outline a series of things we can measure, evaluate independently (assessing source code), or ask the project leads. For descriptions we generate, always run them past project leads for verification. For each item, give a succinct example or two. I've demonstrated (roughly) below. Start with brainstorming lots of discrete ideas and then we can cluster into categories/themes.

This is a seed for discussion, not a finished product. 

How we'd collect each item (tag): **[examine]** inspect the source and docs · **[auto]** automatable from repo metadata (GitHub, best-of) · **[ask]** ask the project leads · **[papers]** available from review papers. And **[P]** / **[F]** = asked at the project or framework level.

---

### Theme: Is it a "Maritime Robotic Simulation"? (per [scope_and_framework.md](../scope_and_framework.md))

Place the effort against the scope document before comparing details — several tools that come up in conversation are neighbors, not our category.

- **Category** Autonomy sim vs engineering/domain sim vs mission/campaign sim. Only autonomy sims are the subject; the rest are recorded as references. *E.g., VRX = autonomy; WEC-Sim = engineering (hydro); an AFSIM-class tool = mission.* [examine, papers]
- **For the autonomy developer (primarily)?** Is the customer (not necessarily the sponsor) the team writing the vehicle software (not a naval architect, acoustician, or planner)? [ask]
- **Stand-in for the robot?** Does the *real* autonomy stack run against it unmodified (SITL/HITL), and through which interfaces? *E.g., VRX via ROS 2/Gazebo; HoloOcean via its ROS 2 bridge.* [examine]
- **Project vs framework.** Name the project and the framework(s) it rests on; keep every item below straight about which level it describes. *E.g., VRX [P] on Gazebo [F]; HoloOcean [P] on Unreal [F]; OceanSim [P] on Isaac Sim [F].* [examine]

### Theme: Purpose — users, decisions, missions

Understand what roles and decisions drive the design; MRS is for autonomy developers, not for the many other roles a simulator *could* serve.

- **Users / roles.** Who is the tool designed for? Distinguish the *user* community from the *developer* community — sometimes the same, often not. 
- **Decisions & decision-makers supported** (may be several). *E.g., DAVE supported both performer engineering decisions (how to build the autonomy) and a government program office making relative assessments of performers' technical maturity toward a fieldable hardware solution.* [ask]
- **Missions / operational envelope.** What mission(s) and operating conditions is it built around and how did that prioritize feature development? 

### Theme: Domains & environment coverage

- **Domains represented.** Underwater / surface / air / land — and can they coexist and *interact* in one shared world? [examine] 
- **Environmental phenomena modeled.** Currents, waves/sea state, wind, bathymetry/terrain, turbidity, acoustics — and the harder ones (biofouling, nets/ropes, ship noise, debris) that Shaw et al. flag as future work. [examine, ask]
- **Spatial & temporal scale.** Mission extent (km), duration (minutes → weeks), and whether it runs faster-than-real-time. *E.g., long-endurance AUV surveys stress this where short UAV flights do not.* [examine, ask]


### Theme: Integration & interoperability

- **Middleware / interfaces.** ROS 1, ROS 2 / DDS, MAVLink, LCM, native API, Python. [examine]
- **Autopilot / stack integration.** PX4, ArduPilot, MOOS-IvP, custom; SITL/HITL support. [examine]
- **Standards & formats.** Vehicle/sensor/scene description (SDF, URDF, USD), scenario formats. Portability across ecosystems . [examine]

### Theme: Extensibility & architecture

To be an MRS, a tool must be extensible — the point is to anticipate *new* missions and environments. Extensibility can be achieved several ways, each with tradeoffs that map to priorities, budgets, and sensitivity.

- **Extension mechanism.** Documented plugin/extension architecture, asset pipeline, API surface — can a small team (not the original developers) add a vehicle, sensor, environment, or behavior *without forking the core*? [examine]
- **Core vs mission/zone-specific separation.** Are general capabilities (e.g., a DVL sensor model, underwater buoyancy) cleanly separable from mission- or operating-area-specific ones (e.g., a data-driven 3-D flow model for estuaries)? [examine, ask] Note this presumes an agreed set of *core* capabilities — which may itself be a central workshop question. A candidate outcome: a process to identify the core capabilities the community systematically supports and maintains, leaving mission-specific additions to the individual application, project, or program. (See Governance below.)
- **Openness as leverage (framework × project).** Openness is not a virtue in itself here — it is the main way a small, niche maritime community leverages the much larger robotics community's investment, public and private, instead of paying for a full stack it cannot sustain. A large consumer market — self-driving cars, say — can support a fully proprietary full stack because the market demands one and funds its maintenance; maritime cannot. So how a framework's and a project's licenses combine bounds both how much outside investment a project can ride on and how extensible it is for others. (Below, "open" means *permissively* open source unless noted — check GPL vs permissive, and closed-engine EULAs inherited at runtime.)
  - Open framework + open project — *e.g., Gazebo + VRX; OpenGL + Stonefish (GPL, note).*
  - Open framework + proprietary project — *e.g., Gazebo + [Volans](https://www.metsci.com/what-we-do/products-tools/volans/).*
  - Proprietary framework + open project — *e.g., Unreal + HoloOcean (MIT layer, Unreal EULA at runtime); Unity + MARUS.*
  - Proprietary framework + proprietary project — *(examples? — group to fill).*
  [examine]

### Theme: Performance & execution modes

- **Execution modes supported.** The four use cases from the scope doc: interactive in-the-loop, headless CI regression, vectorized ML training, and faster-than-real-time mission-plan validation. Which does it actually support? [examine, ask]
- **Compute footprint.** CPU / GPU / VRAM / RAM and supported OS — largely automatable, and the one thing Shaw et al. Table 3 already tabulates. [auto, examine]

### Theme: Community & project health

- **Community size — users vs developers.** Stars, forks, contributors, external citations, forum/chat activity. Aldhaheri et al. hand-classified 240+ downstream studies as a traction proxy (raw counts reward age — read with care). [auto, papers]
- **Maintenance signals.** Last release, commit cadence, current-OS/ROS support, packaging (binaries/Docker), CI. Shaw et al. Table 3 records an active/partial/inactive status per tool. [auto]
- **Governance & sustainment.** Single lab vs foundation vs vendor; funding model; bus factor. And *how are priorities set* — including the maritime pieces of a shared framework? Today they are often set independently by each project's own needs, which can be myopic for the community; a governance model that sets shared priorities (tied to the *core capabilities* question above) is one candidate workshop outcome. [ask, examine]
- **Documentation quality.** Can a new team stand it up *without reading the source*? This is a very high bar.   I've never used a simulation project that with that level of documentation and have rarely use framwork where the lack of source was an impediment to progress [examine]

### Theme: Development process & code quality

This is going to get very hard to assess with AI. 

- **Engineering practices.** Version control, CI/CD, test suites, issue tracking, release process, code review. [auto, examine]
- **Code quality signals.** Structure/modularity, test coverage, static-analysis and dependency health. [auto, examine]
- **Contribution process.** How an outsider contributes, and whether outside contributions are reviewed promptly. Responsiveness says a lot about how the project is *supported*: project-specific (grant/program) support often can't spare time to bring in non-critical-path features, even ones that would help the core and make the tool more useful to the community. [examine, ask] 

### Theme: Validation & real-world grounding

- **Sim-to-real evidence.** Published/demonstrated transfer to hardware, and which real vehicles it has been validated against (Shaw et al. Table 6 tabulates exactly this). [papers, ask]
- **Benchmarks / reference scenarios.** Any standard tasks/metrics — trajectory error, task success, robustness, compute efficiency (Shaw et al. Table 5). The field's missing "marine KITTI/Gym." [papers, examine]
- **Model provenance.** Is a given model validated against measurement, or plausible-but-unvalidated? Any stated error bounds? [ask]


### Theme: Machine-learning support *(to-do — stub for the group)*

Does it expose an RL-style environment API (Gym/Gymnasium), vectorized/parallel environments with deterministic resets, and framework hooks (e.g., Isaac Lab)? Does it generate labeled synthetic datasets and support domain randomization? Overlaps use-case (c) under Performance. [examine, ask] *(Expand later.)*
