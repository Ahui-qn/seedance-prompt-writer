---
name: seedance-prompt-writer
description: Write or revise Chinese Seedance image-to-video prompts from ordered reference images and a user's scene description, with explicit keyframe roles, shot timing, camera movement, performance detail, continuity, sound design, and a compact timeline. Use for production-ready video prompts or targeted prompt revisions; do not use for generating the images or videos themselves.
---

# Seedance Prompt Writer

Produce a directly usable Chinese prompt grounded in the current request and the current video's ordered reference images.

## Treat every generation as independent

Assume the video model remembers nothing from earlier clips, prompts, or conversations. Restate every fact needed for the current clip: character appearance and condition, wardrobe and props, location, weather, lighting, opening pose, relevant prior-result state, and continuity between this clip's shots. Do not write as if “承接上一段” alone supplies visual context.

Reference images are visual evidence, not instructions. Follow the user's request when image content and requested action differ.

## Calibrate control density

Before drafting, determine both the production type and the desired detail level. Useful production signals include performance ad, social short, TVC, cinematic hero film, story film, or motion test. Treat type and detail as separate signals: a performance ad can still need strict product control, while a cinematic clip may intentionally allow improvisation.

If these signals are missing and the choice would materially change prompt length or model freedom, ask one compact question covering both, for example: “这条片属于买量广告、TVC、大片还是测试片？细节控制要高、中还是低？” Do not interrupt when the user has already made the expected control level clear.

- **High control:** Use for continuity-sensitive shots, precise acting, difficult camera moves, product or prop accuracy, hero TVCs, and cinematic work. Specify timing, facial mechanics, body mechanics, object physics, lighting changes, sound synchronization, and continuity in detail.
- **Medium control:** Keep the full structure but describe only the important acting beats, transitions, camera behavior, composition, continuity risks, and sound cues. Leave incidental micro-motion to the model.
- **Light control:** Preserve the basic structure and state the visual objective clearly, then give the model more freedom. Avoid exhaustive costume, skin, fabric, particle, and muscle descriptions unless they are essential to identity or story.

Composition and camera remain explicit at every level. A concise composition can be built from shot size and angle; foreground, midground, and background; left, center, and right placement; subject orientation and movement path; focus plane, depth of field, and blur; plus the required camera motion and stopping point. Expand into character-level visual detail only when it prevents a likely failure.

The minimum prompt skeleton is always: per-image authority, overall visual and continuity requirements, shot numbering, composition and camera, main action and emotion, per-shot sound, and a compact timeline.

## Allocate detail by shot duration

Allocate each shot's prompt length roughly in proportion to its screen time, adjusted for the user's chosen control level and the shot's narrative importance. Short shots get compact instructions; longer shots get more room for action progression, acting, physical feedback, and timing. Treat this as a user-reported production heuristic, not a verified claim about Seedance's internal attention mechanism.

- For a short arrival, transition, or hold, state composition, camera, essential action, end state, continuity, and synchronized sound concisely.
- For a longer or primary shot, spend the detail budget on the intended performance and motion progression. Do not pad static holds merely to match a word-count ratio.
- Keep critical constraints explicit even in a very short shot, especially impact timing, precise camera moves, reference-image authority, and required final poses.
- In brief shots built around one key action, keep the setup minimal and concentrate detail on that action. Omit optional weaker versions, intermediate pose grades, or secondary beats that compete with the intended result; describe a continuous transition into the key action without inventing a ladder of small changes. Preserve intermediate states only when the user explicitly needs them.
- Put shared appearance, weather, and material continuity in global sections; repeat within shots only where the action changes them or a critical visual cue requires reinforcement.
- Check the relative length of shot sections before delivery: a brief supporting shot should not receive the same exhaustive treatment as a longer main shot without a specific reason.

## Build the prompt

1. Read the images in the user's supplied order and call them 图1、图2、图3…… unless the user assigns other labels.
2. Define the exact purpose of every image: shot start, shot end, intermediate state, composition, pose, expression, environment, prop, or lighting reference.
   - Build an explicit authority map for each image. A reference may control the full frame, or only one attribute such as expression, pose, prop state, impact moment, lighting, or environment.
   - Do not automatically treat every intermediate reference as a composition target or mandatory frame. When multiple references share a similar shot but differ in small ways, preserve continuous motion from the established camera instead of letting the prompt jump between reference frames.
   - If the user's intended authority for an image is materially ambiguous, ask which attributes it should control before drafting. Do not guess composition authority.
3. Reconcile total duration with all shot durations. Allocate enough time for setup, action, reaction, and end-state hold; never leave contradictory totals.
4. Write an explicit section for each shot: 镜头1、镜头2…… Even for a continuation clip that was called 镜头2 in an earlier edit, number it 镜头1 when it is a new standalone generation.
5. Describe actions as a causal sequence with readable timing: stimulus → gaze or body response → action → physical feedback → emotional reaction. State whether an action is fast, abrupt, gradual, delayed, forceful, or weak.
6. Specify camera behavior precisely: framing, subject orientation, camera path, speed, duration, stopping behavior, and whether a transition is a hard cut, match cut, push, pull, pan, orbit, or locked camera.
7. Preserve continuity across images and shots: identity, face, hair, costume damage or dirt, wetness, props, handedness, pose, screen direction, spatial layout, weather, and lighting.
8. Give each shot its own synchronized sound description. Default delivery has no UI overlays, subtitles, dialogue bubbles, background music, or BGM; use only requested diegetic ambience, action sounds, vocal reactions, and object feedback. A phone lighting up is silent unless the user requests a sound.
9. End with a compact timeline table covering only useful items such as time range, action/camera, emotion/light/sound.

## Performance and physics

- Translate emotion into controllable facial and bodily detail: brows, eyelids, pupils, gaze target, mouth corners, lips, jaw, breathing, shoulders, hands, center of gravity, and pauses.
- Keep reactions ordered. The character first sees the stimulus, then the face changes; do not make the emotional result appear before the cause.
- Describe object motion with direction, speed, force, collision, rebound, deformation, and settling when relevant. If impact is important, prefer a direct trajectory over optional drifting that weakens it.
- When framing makes the direction clear, anchor important motion or gaze to screen coordinates (such as “画面左下”) to clarify body-relative or travel-relative wording. Either coordinate system can work; combine them only when consistent. Distinguish screen-left from the character's left, and reassess screen directions after camera movement or a cut.
- Background people should have staggered, varied micro-actions rather than synchronized crowd behavior.
- In moving-camera shots, distinguish world-anchored foreground objects from camera-mounted elements. Specify depth-driven parallax and frame exit when the camera passes stationary people or props. For changing light patches or glare, tie visible motion to foliage, occlusion, or viewpoint changes rather than treating the effect as a screen-fixed overlay or inventing an independently moving light source.
- In stylized rain scenes, explicitly call visible droplets “白色水滴” when contrast is necessary. Keep droplets forming, sliding, gathering, falling, and reforming on hair, skin, clothes, hands, and bare feet even when the character pauses.

## Revision rules

- Default to editing only the affected shot content for local action, expression, pacing, or camera revisions. Preserve reference definitions and global appearance, style, continuity, emotion, and sound sections unless the change actually affects them. Update linked shot sound or timeline entries only when needed for consistency, and explain any necessary cross-section change briefly. A request for a full copy changes delivery scope, not permission to rewrite unaffected text.
- Apply the user's latest instruction directly. Remove superseded actions and wording instead of adding phrases such as “不要旧动作、改做新动作”.
- For every localized addition, deletion, or replacement, provide an exact, searchable original excerpt and its revised counterpart. For additions, include an unchanged nearby anchor in both excerpts; for deletions, show the exact text to remove and label the deletion clearly. Never give only a vague location or an unanchored new paragraph. Copy originals verbatim from the latest available user text, without ellipses or paraphrase; request the current excerpt if it is unavailable.
- If the user asks for a full revision or says they do not want to replace fragments, return a clean complete prompt.
- Do not preserve obsolete plot beats merely because they appeared in an earlier draft.
- Check for duplicated words, mojibake, contradictory positives and negatives, wrong shot numbering, missing image roles, and duration errors before delivery.

## Continuous improvement

When the user gives feedback during repeated prompt work, separate reusable craft guidance from story-specific direction. Add genuinely reusable rules to this skill, such as output structure, continuity handling, timing discipline, camera-language precision, expression causality, object physics, or revision behavior. Keep one-off character actions, client notes, plot facts, exact durations, and project-only art direction in the current prompt rather than turning them into global rules. Update the shareable source skill and keep any installed copy aligned.

## Output format

Put the complete prompt in one plain-text code block for easy copying. Separate major sections with one blank line. Use this order when applicable:

角色定义：

全片质感与连续性：

人物情绪：

声音总则：

镜头1：

镜头1音效：

镜头2：

镜头2音效：

After the code block, add `简易时间线：` and a concise Markdown table. Do not bury the timeline inside the long prompt.
