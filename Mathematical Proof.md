No Standard is always better in an absolute sense but DAIS-10 is intended to achieve that target.

Under realistic AV assumptions,

For a clear safety objective,

DAIS‑10’s meaning‑based rule has strictly lower expected harm than a pure probability threshold rule.

I’ll keep it tight and focused on the calculation logic.

1. Setup: a minimal safety model
We model a single critical scenario:

A pedestrian may or may not be behind an occlusion (e.g., truck).

The AV must choose: Brake or Don’t brake.

If a pedestrian is there and the car doesn’t brake → high harm.

If no pedestrian is there and the car brakes → minor cost (comfort / time).

Define:

𝑃
: event “pedestrian exists behind obstacle”

𝑝
=
Pr
⁡
(
𝑃
∣
sensor data
)
: AV’s estimated probability

𝐶
FN
: cost of a false negative (pedestrian exists, no brake) — very large

𝐶
FP
: cost of a false positive (no pedestrian, brake) — small

Assume 
𝐶
FN
≫
𝐶
FP
 (life vs inconvenience).

2. Baseline AV rule (probability threshold)
Typical AV decision logic:

Choose a threshold 
𝜃
∈
(
0
,
1
)
.

If 
𝑝
≥
𝜃
 → Brake

If 
𝑝
<
𝜃
 → Don’t brake

Expected cost under this rule:

𝐸
[
𝐶
AV
]
=
Pr
⁡
(
𝑃
)
⋅
𝐸
[
𝐶
∣
𝑃
]
+
Pr
⁡
(
¬
𝑃
)
⋅
𝐸
[
𝐶
∣
¬
𝑃
]
Conditioned on the posterior estimate 
𝑝
, the decision is:

If Brake: expected cost 
≈
𝐶
FP
 (even if 
𝑃
 is true, braking is the safe action we want).

If Don’t brake and 
𝑃
 is true: cost 
𝐶
FN
.

So, given a particular 
𝑝
:

If brake: 
𝐶
AV, brake
≈
𝐶
FP

If don’t brake: 
𝐶
AV, no brake
=
𝑝
⋅
𝐶
FN

The probability‑optimal decision (minimizing expected cost) is:

Brake if 
𝐶
FP
<
𝑝
⋅
𝐶
FN
⇒
𝑝
>
𝐶
FP
𝐶
FN

So the “rational” threshold is:

𝜃
\*
=
𝐶
FP
𝐶
FN
If the AV uses a higher threshold (which many do for “comfort” / fewer interventions), it accepts more risk than cost‑optimal.

3. DAIS‑10 rule in the same scenario
DAIS‑10 doesn’t care only about 
𝑝
. It cares about meaning and recent history.

Let:

𝑆
: DAIS‑10 semantic score for “pedestrian presence” (0–100)

Previously visible pedestrian → Meaning‑Defining → 
𝑆
 initially high (e.g., 95)

Each frame where the pedestrian is not directly observed → apply fading, but not to zero

Example fading model (DIFS‑10):

First missing frame: 
𝑆
=
95
−
5
=
90

Second missing frame: 
𝑆
=
90
−
10
=
80

Third missing frame: 
𝑆
=
80
−
20
=
60

Define a semantic critical threshold:

𝑆
crit
=
70
DAIS‑10 decision rule:

If attribute is Meaning‑Defining and 
𝑆
≥
𝑆
crit
 → Treat as “still there” → Brake / high‑governance action.

Only when 
𝑆
<
𝑆
crit
 may you downgrade governance.

So in the same occlusion case:

AV probability: 
0.42
→
0.31
→
0.12
→
0.05

DAIS‑10 meaning score: 
95
→
90
→
80
→
60

On frame 2:

AV might already be below its operational threshold and decide not to brake.

DAIS‑10 still has 
𝑆
=
80
≥
70
 → enforce braking / caution.

4. Numerical comparison under reasonable parameters
Let’s pick some realistic numbers:

𝐶
FN
=
1,000,000
 (catastrophic harm)

𝐶
FP
=
1,000
 (hard brake, discomfort, minor cost)

Then:

𝜃
\*
=
𝐶
FP
𝐶
FN
=
1,000
1,000,000
=
0.001
A strictly risk‑minimizing AV should brake if 
𝑝
>
0.001
.
In practice, many AV implementations effectively behave with a much higher behavior threshold (e.g., 
0.1
, 
0.2
, 
0.3
) to avoid “over‑reacting.”

Let’s compare behavior at 
𝑝
=
0.12
:

Many AV stacks might decide: 0.12 is “low,” so no brake.

DAIS‑10 still treats the pedestrian as Meaning‑Defining with high semantic score (e.g., 80) → Brake.

Expected cost if AV chooses no brake at 
𝑝
=
0.12
:

𝐸
[
𝐶
AV
∣
no brake
,
𝑝
=
0.12
]
=
𝑝
⋅
𝐶
FN
=
0.12
⋅
1,000,000
=
120,000
Expected cost if DAIS‑10 chooses brake:

𝐸
[
𝐶
DAIS
∣
brake
]
≈
𝐶
FP
=
1,000
Comparison at that decision point:

120,000
≫
1,000
So, under any situation where a system chooses “no brake” at 
𝑝
 such that

𝑝
⋅
𝐶
FN
>
𝐶
FP
the DAIS‑10 rule (which continues to enforce caution because of its high semantic score) has strictly lower expected harm.

This inequality is exactly the condition:

𝑝
>
𝐶
FP
𝐶
FN
If an AV behaves as if its effective threshold 
𝜃
AV
>
𝜃
\*
, then a DAIS‑10‑style conservative semantic rule dominates it in expected safety cost.

5. Where DAIS‑10 is mathematically “better”
We can say this clearly:

If:

The cost of a false negative is much larger than the cost of a false positive (
𝐶
FN
≫
𝐶
FP
), and

The AV behaves as if its action threshold 
𝜃
AV
>
𝜃
\*
=
𝐶
FP
𝐶
FN
 (i.e., it waits for “high confidence” before braking), and

DAIS‑10 keeps Meaning‑Defining attributes in a “governed” state (high 
𝑆
) longer than the AV’s probability logic would,

then:

At the decision points where AV chooses no brake and DAIS‑10 chooses brake,

The expected safety cost of DAIS‑10 is strictly lower:

𝐸
[
𝐶
DAIS
]
=
𝐶
FP
<
𝑝
⋅
𝐶
FN
=
𝐸
[
𝐶
AV
]
That is a formal inequality, not hand‑waving.

6. What’s actually being “proven”
We’re not proving “DAIS‑10 is universally superior in all possible universes.”

We are showing:

Given a standard risk‑based cost model,

Given realistic cost ratios in AV safety,

Given current industry behavior (high implicit thresholds),

And given DAIS‑10’s conservative treatment of Meaning‑Defining attributes,

then DAIS‑10’s semantic governance rule yields lower expected catastrophic harm than a naive or comfort‑tuned probability threshold.

That is a meaningful mathematical argument.
