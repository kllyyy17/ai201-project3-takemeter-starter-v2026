# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy on the held-out test split is at least 0.55.

**Why this target:** Four labels means a coin-flip guesser gets about 25%, but `question` is already my largest label (14 of the 34 posts I've labeled so far, about 41%), so a model that just always guesses `question` would clear roughly 0.40 without learning anything. 0.55 has to beat that lazy baseline by a real margin, but with ~200 posts split four ways I don't have the data to responsibly promise 0.70.



---

## 2. Every label has an F1 of at least 0.40 on the held-out test split.

**Why this target:** `personal` and `analysis` are my smallest labels right now (5 and 6 of 34 so far), so they'll end up with the fewest test examples and the jumpiest scores. 0.40 is a floor I think is reachable without pretending a ~6-example test slice will be stable, while still ruling out a model that nails `question` and `opinion` but basically can't find `personal` at all.



---

## 3. No single label makes up more than 45% of the final ~200-post labeled set.

**Why this target:** `question` is the easy label to over-collect because Reddit threads are full of literal questions, and in my 34 labeled so far it's already at 41%. 45% gives me a little room without letting one label dominate the set the README's own 70% cap would still technically allow.



---

## 4. Agreement with the staff-labeled set is at least 70% (21 of 30).

**Why this target:** My hardest boundary, `analysis` vs. `opinion`, turns on whether a "checkable specific" genuinely supports the post's main claim — a judgment call even under my own written rule. I'd expect to legitimately disagree with staff on a handful of the 30 posts that were picked specifically because they're ambiguous, so 100% isn't honest, but 70% is high enough to show the taxonomy is applied consistently.



---

## 5. Among the third of test predictions the model is most confident about (highest predicted-class probability), accuracy is at least 15 percentage points higher than among the third it's least confident about.

**Why this target:** If the model's confidence doesn't track its correctness, the confidence score is decoration, not a signal — and with a taxonomy that has a genuinely fuzzy boundary (`analysis` vs. `opinion`), I expect a real gap between posts it's sure about and posts that sit near that line. 15 points is modest on purpose: with ~200 posts total, each third of the test split is small enough (maybe 13-15 posts) that a huge gap isn't something I can demand with a straight face.



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
