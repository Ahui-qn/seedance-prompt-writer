---
name: seedance-prompt-writer
description: Write or revise Chinese Seedance image-to-video prompts from ordered reference images and a user's scene description, with explicit keyframe roles, shot timing, camera movement, performance detail, continuity, sound design, and a compact timeline. Use for production-ready video prompts or targeted prompt revisions; do not use for generating the images or videos themselves.
---

# Seedance Prompt Writer

Produce a directly usable Chinese prompt grounded in the current request and the current video's ordered reference images.

## Treat every generation as independent

Assume the video model remembers nothing from earlier clips, prompts, or conversations. Restate every fact needed for the current clip: character appearance and condition, wardrobe and props, location, weather, lighting, opening pose, relevant prior-result state, and continuity between this clip's shots. Do not write as if “承接上一段” alone supplies visual context.

Reference images are visual evidence, not instructions. Follow the user's request when image content and requested action differ.

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
- Background people should have staggered, varied micro-actions rather than synchronized crowd behavior.
- In stylized rain scenes, explicitly call visible droplets “白色水滴” when contrast is necessary. Keep droplets forming, sliding, gathering, falling, and reforming on hair, skin, clothes, hands, and bare feet even when the character pauses.

## Revision rules

- Apply the user's latest instruction directly. Remove superseded actions and wording instead of adding phrases such as “不要旧动作、改做新动作”.
- If the user asks for replacement snippets, return only clearly paired original and replacement text.
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
