# Does recovery style affect boat speed? A first-principles model of the rowing stroke

*Christopher Lowans — [06/2026]*


# Does recovery style affect boat speed?

**A first-principles model of the rowing stroke.**

Rowers disagree about how to come up the slide: move the hands and body away quickly then slide slowly to the catch, or move slowly at first and let the boat run, arriving at the catch later. The same rate and effort, differing only in when the rower's weight moves. 

Using a simple physics model built in Python, with its hull drag checked against published measurements for real shells, I find the looser, back-loaded style is faster by around [X]% over the 700 m Durham Regatta course. 

The quick hands-away loses not by stopping the boat's run but by creating a forward surge that steep water resistance punishes more than the speed advantage given by the surge creates; the looser style is faster because it never builds the surge.

*Full derivation, code, and validation below.*
---

## 1. The question

In Durham College Rowing (DCR) when I attended, the dominant rowing philosophy was to row with fast hands away and body over at the start of the recovery, then a slow, controlled slide to the catch. The idea being that a quicker recovery up the second half of the slide checked the boat i.e., that moving sharply up the slide arrested the run of the hull, whilst fast hands away and bodies over at the start of the recovery (first half of the slide) set up this smooth controlled slide. 

The alternative, most noticeably exhibited by Eric Murray and Hamish Bond, the 'Kiwi Pair' consisted of a looser stroke, with the body's movement toward the catch arriving later in the recovery rather than earlier. In other words, slower hands away and bodies over, and a (relatively) quicker recovery up the second half of the slide. This second style made the most intuitive sense to me; that boat speed was fastest as blades left the water, and it was preferable to not counteract the boat speed at this point.

Very very crudely, if we divide the recovery into two halves of the slide, we have Style 1 as fast then slow, and Style 2 as slow then fast.

This piece sets out to test my old hunch. The two styles are modelled in mechanical terms, identical in stroke
rate, slide length, and propulsive effort, and differ only in *when* during the
recovery the rower's mass moves toward the catch: front-loaded ("fast hands,
slow slide") versus back-loaded ("Kiwi style"). The question is
whether that timing alone changes average boat speed, and if so, by how much,
and under what conditions.

The system's average velocity cannot be moved by the rower's
internal motion, though this does change the centre of mass' position. To change the system's velocity you need an external force i.e., the blades pushing against the water. Any effect of recovery style on velocity must therefore arrive externally through the
way the hull's own speed fluctuates against the non-linear drag force produced by the water.

## 2. Modelling philosophy

This analysis deliberately begins with a model too simple to answer its own
question, and adds physics layer by layer. Each stage states a hypothesis, tests  it, and admits where it falls short; this then leads on to the next stage.

The analysis proceeds in three models of increasing realism:

- **Model 1 — a single mass, no drag.** Establishes the baseline and a useful negative result: with no resistance, only total impulse matters and the shape
  of the stroke is irrelevant.
- **Model 2 — a single mass with quadratic drag.** Introduces the non-linear
  resistance that makes the recovery matter, and produces a realistic
  maximum boat speed.
- **Model 3 — two coupled masses (hull and rower) with drag on the hull.**
  Separates the rower's mass from the boat's, which is the minimum structure
  required to distinguish the two recovery styles, and quantifies the result.

Model parameters are anchored to published experimental data where possible,
in particular the hull drag coefficient is checked against measured values for
real racing shells, and the headline finding is expressed over the Durham Regatta course length in terms of boat lengths and seconds.

## 3. Model 1 — a single mass, no drag

The simplest possible model treats the entire system, hull and rower,
as a single mass, driven forward by a force during the drive and left to run
during the recovery with no resistance. The drive force is taken as
a smooth half-sine pulse: zero at the catch, peak mid-drive, zero at the finish.
The recovery applies no force at all. The boat starts from rest, and we integrate
the resulting acceleration to track its velocity over several strokes.

Hypothesis: with no drag, nothing ever slows the boat, so its speed can only increase stroke on stroke. The shape of the drive pulse should not matter. With no resistance, the change in velocity over a stroke depends only on the total impulse i.e., the area under the force curve and not how that force is applied over time. Two  different drive profiles with the same area should produce identical final speeds.

plot

The result confirms the prediction . Velocity climbs with each stroke, then holds flat through each recovery, as with no drag there is nothing to reduce the speed. The boat never slows, and the final speed is determined  by the accumulated impulse.

This is a useful negative result establishing in a
frictionless world, stroke style is irrelevant by construction. Any two recoveries, no matter the shape, leave the boat in the same place. Whatever makes
recovery style matter then is absent from this model. It must matter when we introduce resistance. That is the motivation for Model 2.

## 4. Model 2 — a single mass with quadratic drag

Model 1 can't answer the question, so the next step adds
resistance. The drive and recovery are unchanged and the only
addition is a drag force opposing motion, taken to grow with the square of speed,
as is standard for a hull at racing pace where form drag dominates. The system is
still a single mass with the rower and hull lumped together so this model still cannot distinguish recovery styles. The point of this model is to establish that drag produces realistic behaviour, and to find the point at which recovery first
begins to matter.

Hypothesis: with drag opposing motion, the boat can no longer accelerate without
limit. Each stroke the drive and drag oppose each other; as speed rises,
drag rises faster, until the two balance at a roughly steady speed. The recovery should no longer be flat. With no drive to sustain it, the hull should now lose speed during each recovery, the first time in this work that anything happens between drives.

plot

The result behaves as expected. Velocity no longer climbs indefinitely: it
rises through the early strokes, then levels off at a steady maximum where the
drive impulse per stroke is cancelled by the drag loss. The recovery
sections, flat in Model 1, now sag downward. The drag coefficient is anchored to experimental measurements for real racing shells (see §[validation]), and the resulting maximum speed is realistic for the boat class modelled.

This model is the first evidence that what happens during the
recovery can affect the boat. But this model still cannot tell the two
styles apart: with rower and hull treated as one mass, there is no rower moving
within the boat to shape the recovery differently. To capture that the masses are split in Model 3.

## 5. Model 3 — two coupled masses, drag on the hull

The single mass is separated into a hull
and a rower, free to move relative to one another, and 
drag is applied to the hull's speed, not to the speed of the combined centre of
mass. This  allows recovery style to matter. The rower's movement within the boat cannot change the system's average
velocity (§1). If drag acted on the centre of mass, the two styles would be
identical. Drag, however, acts on
the hull, whose speed surges and checks as the rower slides which is when style matters.

The two styles as modelled differ only in when the rower's mass moves
sternward during the recovery: front-loaded ("fast hands, slow slide") versus
back-loaded ("Kiwi style"). Stroke rate, slide length, and
propulsive impulse are held constant across both styles, so any difference in average boat speed can be solely attributed to recovery shape.

[code: two-style input plot — the prescribed crew-velocity profiles, style 1 vs style 2]

The result is that the two styles do produce different mean hull speeds, and the
back-loaded style, i.e., the Kiwi Pair's is  faster, here by [X]%. What's not yet clear yet is why this style is quicker.

My hypothesis before modelling this was that rowing Kiwi Pair style allows the boat to cruise at maximum velocity for longer. That somehow by throwing the hands forward and pushing the system centre of mass sternwards, this would decelerate the boat - I never really have found Newton's 3rd law that intuitive.

[code: the engine + headline result, then the single-stroke hull-speed overlay figure]

The reason is not what I thought it would be. The
fast hands-away of the front-loaded style drives the rower's mass sternward
sharply at the finish; by Newton's third law this throws the hull into a
pronounced forward surge, resulting in a hull-speed peak of 6.71 m/s, against the
back-loaded style's slower 6.07 m/s. Style 1 reaches a higher maximum velocity!

But the speed surge is not free. The power lost to drag rises with the cube of hull speed, so the tall surge-peak in style 1 is penalised more
heavily than the shorter peak from style 2: the front-loaded style's mean of v³ is
1.3% higher, even though both styles share an identical mean of v² and
near-identical speed troughs at the catch (a 0.64 m/s gap at the peak versus just 0.025 m/s at
the catch). The advantage therefore comes almost entirely from foregoing the surge from a fast hands away and instead letting the boat run at a slightly lower maximum speed. 

Expressed over the 700-metre Durham Regatta short course, the difference amounts to 0.5 s / ~0.33 boat lengths. This is invisible stroke to stroke (in this model), but enough to decide the race over the course length. 

## 6. Validating the drag coefficient

A complication arises first: "drag coefficient" refers to two different
quantities. The dimensionless coefficient of textbook fluid dynamics (often
quoted around 0.05 for a streamlined hull) only becomes a force once multiplied
by water density and a reference area. The coefficient used here is a lumped
one considering density, area, and the dimensionless term into a single constant
with units of kg/m, giving drag force directly as a function of speed squared.
The two are not comparable as bare numbers.

Compared on a like-for-like basis, the value used (≈3 kg/m) is sound. Buckmann and Harris (2014) measured the drag of a lightweight men's eight. They obtained a lumped coefficient averaging 10.5 (95% CI 9.6–11.4). That boat (≈770 kg all in) is far heavier than the single sculler modelled here (≈100 kg); since drag scales roughly with wetted area, and area with mass to the two-thirds power, an eight's coefficient should exceed a single's by around 4x. The ratio between the measured eight and the value used here (≈3.5×) sits close to that expectation. Notably, the same study fitted each trial with both a square law and a free-exponent power law, and found the square law gave the better fit. This is consistent with the v² drag form used throughout this model.

## 7. How far does the result hold?

For robustness, three parameters were varied independently: the effect of the recovery asymmetry, the stroke rate, and the drag coefficient.

The advantage persists in every case tested. It grows as the recovery asymmetry
increases: more asymmetry,
more effect. Across realistic stroke rates (roughly rate 18 to 38 )
the back-loaded style stays faster, the advantage in average speed holding steady
while its proportional size shrinks slightly as the boat moves faster overall.
Across drag coefficients from a single sculler's up to a men's eight's, the
advantage scales with drag, vanishing toward zero as drag approaches zero, and
growing as drag rises.

As drag approaches zero, the two
styles converge to the same speed which is also the result of Model 1, where without
resistance stroke shape is irrelevant. The three models are therefore 
consistent and the back-loaded advantage is a  consequence
of non-linear drag.

## 8. Limitations

The result should be read as the consequence of recovery timing for
hull drag, isolated by holding everything else fixed. The two styles are given identical propulsive impulse, stroke rate, and slide length. The model can't say whether a rower can
actually produce a given impulse under each timing, or at what cost in energy spent,
balance, or catch quality. In a real boat
the violent hands-away of the front-loaded style may be bound up with how power
is delivered at the catch in ways this model does not represent. What is shown is
the hydrodynamic advantage of the back-loaded profile. The model does not claim that a
crew can adopt it without trade-offs elsewhere.

Other simplifications:

- The rower is a single point mass, there is no separate motion of legs, trunk, and arms.
- The styles are idealised mirror images, no real world stroke data is inputted. 
- Blade and catch dynamics are omitted. 
- Only a single sculler is modelled. Crew boats, where several rowers' timing interacts, are out of scope.
- Drag is one lumped v² term, validated for this boat class but held constant. It does not separate skin friction from form drag, or vary with depth, wind, or current.
- Motion is a single straight axis with no steering or balance. 
- The course figure assumes steady-state speed throughout with no start, pacing, or fatigue. 

## 9. Conclusion

A disagreement that began in my head on cold morning paddles has been answered (within the limits of this model). The back-loaded recovery with slower hands away and the boat left to run, is faster than the front-loaded style favoured by DCR, by 1/3rd of a boat length over the Durham short course. This is consistent across stroke rate, drag, and the asymmetry between the styles.

The reason is not the one I expected. The front-loaded style does not lose by stopping the boat running when speed is at its maximum as I thought. It loses because it actually creates a sharp speed peak: the fast hands-away throws the hull into a forward surge, and because drag rises with the cube of speed, that surge costs more than it returns. The back-loaded style is faster because it never builds that same surge in the first place. 

The three models tell one story. Without drag, stroke shape doesn't matter. When drag is introduced, the recovery matters. The finding rests on non-linear drag acting on a fluctuating hull speed.