# Authoring crosswalk for the supplied AutoResearch QA materials

Read this when the task uses the supplied `autoresearch-qa-skills` and *AutoResearch 专家线下标注教程*. It is an authoring checklist, not a replacement for the current source files. Resolve conflicts in this order: explicit user decision and current task card for scope; current tutorial/format rules for submission; installed Harbor schema for machine behavior; version-matched QA policy for review; Example for illustration only. A user decision that departs from a mandatory rubric is a disclosed exception, not silent compliance. The 2026-09-29 *PCA 双镜像对齐版* explicitly changes the earlier tutorial's single-image packaging, Agent view and final handoff while retaining its research-quality/statistical requirements. The older `规范格式.docx`, event-interpolation Example and 2026-09-18 QA Docker-path profile must not override it when the new revision governs. The QA folder's default `implementation` policy and its old `strict` policy also differ; `qa-spec.md` and `report-schema.md` describe that legacy strict mode and must not silently override the current tutorial. Record source revision, installed Harbor version and decisions.

## Stage applicability

This skill stops before the user launches research. Apply G01–G03, B01–B08, scoring, isolation, environment and launch checks now. For QA16/18 and the trajectory/final-method portions of QA21, prepare the later run/collection contract and mark execution evidence `POST_LAUNCH_PENDING`; never fabricate it, claim it passed, or automatically run Agents to close it. Complete the currently measurable annotation and B/R portions now. Full expert acceptance and platform final acceptance remain separate from launch readiness.

## Three content gates before implementation details

| Gate | Build and prove |
|---|---|
| G01 Method surface | The prompt, parser/guard, and actual call path permit a substantive method change. Fixed-task numerical tuning alone is insufficient. Show at least one legal, undisclosed research direction beyond the expert Reference. |
| G02 Fair Baseline | Identify Starter, formal Baseline, and score anchor separately. Confirm labels, loss, optimizer updates, effective training, checkpoint selection, actual budget, data, seed, search opportunity, and method rationale. A simple or old method can be valid; a scaffold needs a separate runnable Baseline. A declared algorithm-debug task also needs a healthy control. |
| G03 Solvability | Use every predeclared paired run with the same protocol and valid quality gates. Recompute raw improvement, sample standard deviation of Baseline (`n−1`), normalized score and headroom. Under the supplied stochastic rubric, use at least three independent runs, require improvement ≥`3σ_B` and Reference score in `[0.15,0.8]`; `3–5σ_B` merits review, `≥5σ_B` is stronger evidence. Deterministic tasks have no universal 5% gate. A user-chosen single seed is a disclosed exception or unmet stochastic gate, never a passed sigma check. |

For maximize, `Δ=mean(R)−mean(B)` and `score(x)=(x−B)/(U−B)`; for minimize, `Δ=mean(B)−mean(R)` and `score(x)=(B−x)/(B−U)`. `B` is the measured formal Baseline aggregate; `U` is a justified attainable estimate or, if that cannot be justified, the metric ceiling. Keep the valid score continuous, monotone, finite, and unclipped. Reference is not `U`. Require U≠B in the improvement direction, and Δ>0 even if σ_B=0. Zero sample variance alone does not establish determinism. Freeze anchors and their provenance before inspecting Reference results; keep revisions/attempts rather than overwriting them.

Under the supplied tutorial, unspecified stochastic protocols use at least three independent runs and at least five when variability is high; predeclare the variability criterion and any additional-run/stopping schedule. The tutorial's summary table allows 3–5σ with review, while its detailed section calls for additional repetitions and platform review: record that difference and use a declared additional-run plan under the detailed rule, retaining all paired attempts, never keep adding seeds only until passing. Remaining headroom toward U should in principle be ≥3σ_B; a smaller value triggers documented risk/QA14 review, not an invented absolute rejection rule. Deterministic tasks still require real positive improvement, the normalized range and any predeclared tolerance.

The separate Baseline-quality skill expands G02 into eight checks: **B01** task-appropriate method and provenance; **B02** actual implementation, training and checkpoint health; **B03** fair shared resource budget while allowing declared research variables; **B04** configuration and search-opportunity fairness; **B05** complete paired seeds without selection; **B06** applicable simple sanity anchors; **B07** attribution of improvement without undisclosed data/resource/protocol changes; **B08** explicit choice and limitations. Judge observable evidence, not presumed intent. Old or simple methods are not automatically weak, and a large Reference gain does not alone condemn Baseline.

## QA01–QA21: translate checks into construction work

| ID | Authoring action under the supplied default policy |
|---|---|
| QA01 | Write the eight meaningful `instruction.md` sections; omit paper title, arXiv/repository identity and answer hints when this rubric requires anonymity. |
| QA02 | Implement and test the continuous, monotone, unclipped normalized score; Baseline→0, justified `U`→1, invalid outcome separate. |
| QA03 | Provide runnable private Reference plus complete declared-run results, raw logs and training artifacts/reload evidence when applicable; check target score range. |
| QA04 | For stochastic evaluation, recompute paired raw means and `σ_B` from all independent runs and apply the current 3σ rule; mark deterministic tasks only with a reason. |
| QA05 | Connect every hard prohibition/limit in the prompt to an environment restriction, guard, or trusted verifier path. Text alone is insufficient. |
| QA06 | Provide a single documented evaluator entry that computes a trusted finite scalar and classifies invalid submission, timeout/resource, evaluator, and infrastructure errors. |
| QA07 | Keep final-test answers out of `instruction.md`; separately verify actual delivery isolation rather than claiming this narrow static check proves it. |
| QA08 | Keep Reference code/config/results out of `instruction.md`; separately verify image, mounts, caches and Git exposure. |
| QA09 | Clear a candidate-prewritten reward and write trusted result through a temporary file and atomic replacement. |
| QA10 | Restore or independently pin frozen evaluator, guard, metric, schema and data; prevent candidate import/path shadowing of the trusted implementation. |
| QA11 | Ensure all eight sections contain the task's actual input/output, data visibility, formula, scope, constraints, submission, iteration and completion details. |
| QA12 | Inspect and clean shipping Git history, refs and answer-bearing metadata, or ship without `.git` after preserving provenance elsewhere. |
| QA13 | Demonstrate a valid, nontrivial Baseline and actual Reference improvement under the same formal protocol; retain failed runs. |
| QA14 | Preserve at least one legal, discoverable direction after Reference; neither saturate the score nor tell the Agent that direction. |
| QA15 | The default static QA skips this ID. Still implement resource and one-score limits required by the active task card/tutorial and verify them on the platform. |
| QA16 | When final expert trajectories are required, account for **each** Agent's effective method time separately. Current tutorial default is each ≥10h; each ≥7h only for a non-training task with short iterations and all exception evidence. A 12h container soak is separate. |
| QA17 | Verify Harbor task root, installed-version `separate` and `artifacts` behavior, both image builds, provider paths, actual verifier reward, invocation configuration when supplied, and same-Trial transfer/runtime evidence when supplied (H01–H06 below). The older QA helper may still assume a task-root build context; classify that as a policy-version mismatch and review the active contract independently. |
| QA18 | Preserve two independent, task-matching Agent method trajectories and a real progression analysis when the current tutorial requires them; B/R runs are not Agent trajectories. |
| QA19 | Explain seed and effective-improvement rule in the prompt for stochastic evaluation; preserve the complete formal run protocol in expert evidence even if this narrow QA item does not require every detail in the prompt. |
| QA20 | State editable/readable scope, network and tool policy, and how the Agent reaches public jobs; implement the relevant restrictions without confusing command access with submitted-code access. |
| QA21 | Make `trajectory_codex.json`, `trajectory_seed.json`, `expert_annotation.json`, and `run_summary.json` parse and agree with real runs. The latest supplied tutorial specifies eight per-round fields; the older QA static policy may accept only `round` and `method_summary`, which is insufficient for a fresh package governed by the tutorial. Do not confuse Seed the Agent model with a training seed. |

## Harbor H01–H06

| ID | Evidence to prepare |
|---|---|
| H01 | Complete selected platform task root, Agent `environment/` context and private `tests/` context; `tests/test.sh` is the normal Linux final verifier entry. A source-tree `solution/` is not required by the active dual-image tutorial. |
| H02 | Valid TOML **and** `artifacts` and `verifier.environment_mode="separate"` accepted and effective in the installed Harbor version or a delivered adapter; the PCA sample's schema version is not universal. |
| H03 | Build Agent from `environment/` and separate Verifier from `tests/` when the 2026-09-29 tutorial governs. Reconcile each context's `COPY`, workdir, runtime `/workspace/solution`, public scoring, private `/tests` and only the declared artifact transfer. Older task-root/one-image profiles are historical for this revision. |
| H04 | After the Agent exits, trusted `/tests/test.sh` in the separate Verifier actually scores the transferred candidate and writes finite `/logs/verifier/reward.txt` or numeric `reward.json`; pytest-only success or stdout score is insufficient. Probe candidate access to private labels/reference, `/tests` and reward. |
| H05 | If a Job/Trial or CLI config is supplied, check selected task, both image providers, agent, `separate`/artifact overrides, network/resources and enabled verifier. It is not mandatory to invent job.yaml for a single-task CLI. |
| H06 | For launch readiness, retain one bounded non-search Trial's config, both image IDs, transfer manifest, verifier result/reward and logs, reconciling values and isolation on the same run. Without it, report runtime handoff unverified; official Hidden still belongs to later platform acceptance. |

## Scope of security and runtime checks

For the exact failure-state mapping, secure deliverables and post-launch evidence schemas, use [package and readiness](package-and-readiness.md). The legacy `strict` QA document adds adversarial checks. It is not the default 21-item implementation policy, but use it as a threat model for a final release:

| ID | Probe or prevent |
|---|---|
| EX01 | Sandbagged Baseline, including deliberate slow paths, wrong preprocessing or unequal budget. |
| EX02 | Anchors or Reference selected after seeing results to force a favorable normalized score. |
| EX03 | Final-test oracle use through repeated adaptive queries or detailed feedback. |
| EX04 | Fabricated, copied or stale logs, hashes, run identities and selected-code records. |
| EX05 | Side-channel answer hints in filenames, prompts, test traces or error messages. |
| EX06 | Docker layer, history, build cache or `COPY .` leaks, including secrets deleted only in later layers. |
| EX07 | Verifier takeover via path traversal, symlink, unsafe deserialization, import shadowing or result ambiguity. |
| EX08 | Benchmark gaming through order, timing, persistent state, cached outputs or background work. |
| EX09 | Unsafe archive paths, duplicate names, special files, nested archives or expansion bombs. |
| EX10 | Dependency, runtime, base-image, model revision or license drift. |
| EX11 | Public/final data overlap or leakage through seeds, ordering, IDs and metadata. |
| EX12 | Process, disk, GPU, timeout, log-flood or concurrency escape beyond resource controls. |
| EX13 | Hollow tests: skipped/overwritten cases or assertions that never reach the trusted path. |
| EX14 | Unproven final Agent view; compare an explicit allowlist with final image and mounts. |
| EX15 | Excess final-test diagnostics, including per-case names, raw metrics or traceback details. |
| EX16 | Statistical cherry-picking, optional stopping, non-independent replicates or mismatched hardware. |

Perform relevant dynamic probes before claiming production readiness: final-image/layer scan, real Agent UID mount and permission probe, hidden/reference absence in environment/process/log channels, clean Baseline/Reference reruns, adversarial submissions, stochastic repetition, scheduler/cgroup enforcement, split contamination check, and required long soak. The active rubric decides which are mandatory; do not report a default QA static pass as proof of them. A manifest of Agent-visible files is a claim until checked against the final image and mounts as the real Agent UID.

For each failed or pending check, report `fact and file → why the criterion is unmet → concrete repair → evidence needed to accept the repair`. Distinguish confirmed failure from missing evidence and from an explicitly approved protocol exception.
