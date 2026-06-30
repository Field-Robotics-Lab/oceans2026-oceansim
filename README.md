# oceans2026-oceansim

Working repository for a proposed half-day workshop at **IEEE OCEANS 2026 Monterey** on open-source, multi-domain simulation for ocean robotics.

**Status:** **accepted.** The workshop has been accepted for OCEANS 2026 Monterey and is scheduled for **Monday, 21 September 2026**. We are now **soliciting co-organizers, speakers, and contributors** and building out the workshop website. If you maintain or use one of the active open-source ocean-simulation stacks (Gazebo-based, game-engine-based, or otherwise), we would like to hear from you: open an issue, send a pull request, or email Brian.

## Key dates

| Date | Item |
| --- | --- |
| 2 July 2026 (EOD PST) | Confirm participation with the organizing committee |
| 10 July 2026 (EOD) | Post the workshop website and send the link to the OCEANS organizers |
| 21 September 2026 | Workshop day (half day) at OCEANS 2026 Monterey |

After the website link is submitted, registration will include the workshop and we can begin recruiting pre-registrants. The workshop requires a minimum number of pre-registrants (indicating their preference for it during OCEANS registration) in order to be held.

## What the workshop is about

In short: ground and aerial autonomy have CARLA, AirSim, and Isaac Sim as common ground. Ocean robotics does not yet have an equivalent. Several open-source projects each cover part of the problem (VRX, DAVE, HoloOcean, OceanSim, Stonefish, MBARI LRAUV simulation, WEC-Sim), but federated one-off funding for individual tools has slowed convergence. The goal of the workshop is to refine what we collectively mean by "ocean sim", summarize the state of the art and state of practice, and draft a short community roadmap and a white paper aimed at funding agencies (ONR, DARPA, NSF).

See [proposal/proposal.tex](proposal/proposal.tex) for the current draft proposal and [literature_review/lit_review.tex](literature_review/lit_review.tex) for the working annotated literature review that the proposal builds on.

## How to get involved

We need help on several fronts. None of these slots are filled yet, and we are happy to add more.

- **Co-organizers.** Especially representatives of the projects listed in the proposal — please reach out so we can add you to the organizing committee (each organizer gets a short bio in the proposal).
- **Invited speakers.** One representative per active project is the current plan; named individuals will be finalized before the camera-ready submission.
- **Contributed posters / user-experience reports.** A coffee-and-posters slot is in the schedule. The formal call will go up on the workshop site closer to the event.
- **Reviewers for the literature review.** The annotated literature review has four contributor slots (underwater perception, hydrodynamics and surface dynamics, ML training infrastructure, and overall editing). Three of the four are open.

The fastest way to engage right now is to **open an issue** with your name, affiliation, and which of the above you would like to help with, or to email Brian directly.

## Layout

```
proposal/              OCEANS 2026 workshop proposal (LaTeX, 3-page limit)
literature_review/     Annotated literature review of open-source ocean simulators (LaTeX)
```

## Building the documents

Both documents are plain LaTeX. From inside each folder, e.g.l, 

```bash
latexmk -pdf proposal.tex
```


## Contact

Brian Bingham, Naval Postgraduate School — [bbingham@nps.edu](mailto:bbingham@nps.edu) / [briansbingham@gmail.com](mailto:briansbingham@gmail.com).
