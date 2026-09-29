# From paper benchmark to an AutoResearch protocol

Use this when deciding which paper experiment becomes the task or auditing fidelity.

## Read and trace the sources

Inspect the original paper, appendix, released code at a recorded commit, configs, dataset card/files, and current task card. Capture exact table/figure/section, config key, file path, version, and data hash. When paper prose, tables, and code disagree, write down the conflict and selected interpretation. Prefer the user's stated benchmark target; otherwise choose the smallest coherent benchmark slice with a valid evaluation signal and enough research headroom. Do not claim exact paper reproduction when any consequential setting differs or is unknown.

If the active program labels tasks S1/S2/S3, preserve its supplied constraints: S1 begins from a candidate paper/repository, S2 from a direction and allowed assets, S3 from an approved proposal. A requested variant must change a substantive method, objective, Starter or search restriction and needs its own Baseline/Reference/protocol evidence; a new title or seed alone is not a variant. Check that one legal Public/Dev iteration can return feedback within the task's budget (the supplied tutorial targets roughly two hours per score); if it cannot, document the measured bottleneck and seek a protocol-level decision rather than silently changing the benchmark.

Record at least:

| Item | Questions to settle |
|---|---|
| Scientific target | What input, output, prediction horizon or subgroup, and original benchmark question? |
| Data | Which released files, licensing/access, train/dev/test boundaries, preprocessing, leakage or overlap, and immutable hashes? |
| Evaluation | Raw metric and direction, subgroup reporting, aggregation, inference path, checkpoint selection, and public versus final feedback? |
| Training | Initialization/pretraining, optimizer, steps or epochs, batch, sampling, random seeds, model capacity, time and hardware budget? |
| Comparators | What is the paper baseline, a reasonable runnable task Baseline, and an expert-only Reference? Which are exact replications versus adaptations? |
| Deviations | Which choices change the paper protocol, why, and how will the result be described without calling it the paper's number? |

For each row of the actual alignment record, use columns such as `setting | paper source/value | released code or data source/value | task choice | identical/adapted/unknown | reason and consequence`. Record the original paper hardware as provenance; choose task hardware for feasible, fair execution rather than assuming exact hardware matching is required. Disclose changes that affect comparability.

## Fix a fair protocol before scoring

Make the research variable explicit. Keep every non-variable input, split, preprocessing rule, scoring implementation, and resource rule stable across Baseline, Reference, and candidate. The Baseline must be a plausible method with a real training budget; do not weaken it to manufacture headroom. A paper's author method can be a Reference after adaptation and execution under the task protocol, but it need not be the only winning path.

The public signal should help the Agent select methods for the stated objective. If public feedback uses a different split, length regime, or metric from the final score, state the gap and assess whether it still guides improvement. A final evaluation based on already published data is still public in origin even when its files are withheld from the Agent's container. Isolation prevents direct file access; it does not make the benchmark newly hidden.

Define the raw metric first. If a normalized reward is needed, write its formula, direction, measured Baseline anchor, chosen upper/attainable anchor or bound, clipping policy, and invalid value. Distinguish a task-specific macro average or reward from metrics the paper actually reported. Anchor files may live near the trusted evaluator even when computation runs on another machine; their location follows the implemented architecture.

Use the number of seeds required by the current task card and user. Match actual seeds and evaluation rules between methods. Multiple independent seeds permit an estimate of between-run variability; a single seed gives only one observed comparison. Do not silently apply a sigma gate to one run, rename repeated evaluations as independent training seeds, or replace failed seeds with selected good runs. Separate time budget for one score, one platform job, the Agent's search, and any evidence trajectories.

Before claiming the optimization surface is viable, compare real Baseline and Reference outputs under the same frozen protocol when training/evaluation is authorized. Preserve per-run metrics, commands, logs, source hashes, runtime, and reloadable artifacts as required. If that evidence is not yet run, call the improvement and anchors unverified, not passed.
