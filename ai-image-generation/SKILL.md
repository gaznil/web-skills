---
name: ai-image-generation
displayName: "AI Image Generation Prompting Notes"
description: >
  Prompting technique reference across AI image models — ChatGPT (GPT
  Image), Nano Banana 2/Pro, Midjourney, Ideogram, FLUX 2, Seedream,
  Dreamina, Qwen Image, Wan, Z-Image, and others as they come up. Does
  not select a model automatically — if the user hasn't named one, ask
  which they're using before writing the prompt. Prompt architecture and
  formatting are governed entirely by the user's own project
  instructions where those exist; this file supplies general prompting
  technique and per-model quirks, and never overrides the user's
  face-reference or formatting rules.
license: MIT
---

# AI Image Generation Prompting Notes

Background reference only. This file never picks a model on its own — it exists to describe how to prompt well and how each model responds, not to decide which one to use or to dictate structure when the user already has their own.

## Model selection

If the user has already named a model, use that — don't ask.

If no model was named, ask once before generating. Offer the user's usual models first (ChatGPT, NB2, Midjourney, Ideogram, general) plus an open option for anything else, since new tools show up over time — don't hard-limit the choice to a fixed list. Never silently auto-select "the best model for this kind of image" — that decision belongs to the user.

## General prompting technique (use when the user has no stricter rule of their own)

**Subject first, scene second, modifiers last.** "A small purple cat sitting on a moss-covered stone, golden hour rim light, shallow depth of field, photoreal." Front-load the subject; trail with style/camera directives.

**In-image text** — quote the literal string exactly (`the sign reads exactly "CLOSED"`); without the literal quote, models paraphrase instead of rendering. Name the script for non-Latin text ("Japanese kana", "Cyrillic", "Arabic right-to-left") or it falls back to romanization. Specify layout explicitly ("top-left", "centered", "two-line stacked").

**Photoreal portraits** — lean on lens and lighting vocabulary: focal length ("85mm portrait"), light quality ("soft natural light", "golden hour rim light"), depth of field ("shallow depth of field"). Models respond strongly to camera-language cues.

**Real-world grounded subjects** — if a prompt names a real product, place, or landmark whose appearance must match reality, and the tool offers a web-grounding option, that's fine to use for *objects/places*. Never use it to source a real person's likeness — see Identity rule below.

**Batch ideation / storyboards** — generate multiple variants at low resolution/step-count first, then only re-run the winning concept at full quality. Fix a seed (if the tool exposes one) when iterating small variations on one concept, to keep composition stable across the batch.

**Editing an existing image** — lead with what to preserve, end with what to change: "Keep the subject's face, pose, and clothing unchanged. Convert the background into a rainy neon cyberpunk street." This ordering reduces unwanted drift in parts that weren't supposed to change. (If the user has their own fixed face-reference line, use that verbatim instead of paraphrasing "keep the face unchanged.")

**Anti-patterns to avoid:**
- Conflicting style words ("minimalist + ornate + retro + cyberpunk" cancel each other out) — pick 1–2 style anchors.
- Vague text requests ("with the brand name on it") instead of an exact quoted string — produces unpredictable, often wrong, rendering.
- Re-describing a stable subject/identity from scratch each time instead of using image-to-image with a reference, when the tool supports it.
- Requesting exact hex color codes as embedded text — sometimes renders as literal text in the image instead of being applied as color. Describe color by name/mood instead.

## Notes by model

**ChatGPT (GPT Image)** — Strong in-image text rendering (see quoting rule above). No seed/step controls exposed — don't reference them.

**Nano Banana 2 / Pro (NB2)** — Identity-preserving by default on edits; honors spatial language ("upper-right", "the left object").

**Midjourney / Ideogram / general** — Respond strongly to camera and lighting vocabulary (see photoreal-portraits technique above).

**FLUX 2 (Klein 9B/4B, Pro, Dev, Flash, Turbo, Max)** — Step-distilled variants (Klein) are fast for iteration; higher tiers (Pro/Max) for production polish. Supports multi-reference conditioning on some endpoints — describe each reference's role in the prompt ("subject from ref 1, palette from ref 2").

**Seedream (5 Lite, 4-5)** — Strong photoreal skin tones and natural lighting; good for portraits and product shots.

**Dreamina** — Illustration / concept-art lean rather than photoreal — use for stylized or painterly requests.

**Qwen Image, Wan, Z-Image** — Open-weights models, often LoRA-compatible — relevant if the user is running a custom-trained style/character LoRA rather than a base model.

## Identity rule (applies to all models)

Never suggest sourcing a real person's likeness from web search or general knowledge. If the user has provided a face reference photo, that photo is the only identity source — describe it only via the user's own fixed face-reference line if they have one (otherwise plain, neutral reference language), never supplemented with assumed real-world appearance data.

## Output format

Whatever the user's own instructions specify for prompt format (e.g. single cohesive paragraph, no bullet points, negatives woven in naturally) takes priority over anything in this file. The bullets and sections here are for the assistant's own reference only — never carry that structure into the final prompt text; collapse it into whatever format the user requires.
