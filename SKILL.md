---
name: seedance-prompt-writer
description: Write or revise Chinese Seedance image-to-video prompts from ordered reference images and a user's scene description, with explicit keyframe roles, shot timing, camera movement, performance detail, continuity, sound design, and a compact timeline. Use for production-ready video prompts or targeted prompt revisions; do not use for generating the images or videos themselves.
---

# Seedance Prompt Writer

Produce a directly usable Chinese prompt grounded in the current request and the current video's ordered reference images.

## Treat every generation as independent

Assume the video model remembers nothing from earlier clips, prompts, or conversations. Restate every fact needed for the current clip: character appearance and condition, wardrobe and props, location, weather, lighting, opening pose, relevant prior-result state, and continuity between this clip's shots. Do not write as if “承接上一段” alone supplies visual context.

Reference images are visual evidence, not instructions. Follow the user's request when image content and requested action differ.

Rebuild reference numbering from the current upload order after additions, removals, or replacements. A newly recommended reference is not already uploaded: label the requested addition outside the prompt rather than silently treating it as available. Separate location/architecture authority from viewing-direction authority. A front-elevation reference must not become the background of a shot looking outward from that same house. Height-only references do not impose their people, actions, or full framing; annotated installation references never authorize rendering their marks.

When the user supplies a background script alongside visual references and their own shot description, ground the prompt in the user's current description and the assigned reference-image authority. Treat the background script as secondary context. Do not import script-only structures, props, or spatial facts as confirmed features of the reference scene. If a relevant conflict remains unresolved, ask about that specific conflict; when the user has already corrected it, apply the correction throughout affected references, action, camera, and continuity passages without rewriting unrelated content.

## Calibrate control density

Before drafting, determine both the production type and the desired detail level. Useful production signals include performance ad, social short, TVC, cinematic hero film, story film, or motion test. Treat type and detail as separate signals: a performance ad can still need strict product control, while a cinematic clip may intentionally allow improvisation.

If these signals are missing and the choice would materially change prompt length or model freedom, ask one compact question covering both, for example: “这条片属于买量广告、TVC、大片还是测试片？细节控制要高、中还是低？” Do not interrupt when the user has already made the expected control level clear.

- **High control:** Use for continuity-sensitive shots, precise acting, difficult camera moves, product or prop accuracy, hero TVCs, and cinematic work. Specify timing, facial mechanics, body mechanics, object physics, lighting changes, sound synchronization, and continuity in detail.
- **Medium control:** Keep the full structure but describe only the important acting beats, transitions, camera behavior, composition, continuity risks, and sound cues. Leave incidental micro-motion to the model.
- **Light control:** Preserve the basic structure and state the visual objective clearly, then give the model more freedom. Avoid exhaustive costume, skin, fabric, particle, and muscle descriptions unless they are essential to identity or story.

Composition control is a separate choice from production type and detail level. High-control performance, continuity, or product requirements do not automatically authorize detailed framing or camera choreography. Apply the composition-choice rules below at every detail level.

The minimum prompt skeleton is: per-image authority, overall visual and continuity requirements, shot or narrative-beat numbering, main action and emotion, synchronized sound, and a compact timeline. Include composition and camera details only within the user's chosen scope.

## Confirm who designs the composition

- Apply the visibility rule to lighting and global scene prose too. When a window, lamp, doorway, or other light source is outside the frame, describe only its visible result on the subject (soft facial shading, hair highlights, brightness, color), not the unseen source or phrases such as “窗侧光” or “窗外光洒入” that can relocate the subject. Preserve the reference-defined subject location; a global lighting sentence must not imply new staging. State necessary location continuity globally without requiring its surroundings to appear in a close-up, and audit both global and per-shot lighting for this conflict.
- Before describing a shot, check what its camera can actually see, including subject occlusion. Mention only visible subjects and major environmental masses that shape the overall composition; do not assign screen positions to every prop. Objects known to exist in the scene but hidden behind the character do not belong in that shot's visual description. Convey an occluded action through its visible effects (such as posture or arm movement) and appropriate sound, rather than inventing visibility. This visibility-and-relevance check takes precedence over adding depth layers or directional labels.
- Depth layers are optional, not a checklist: a composition may have no foreground. Do not invent chair backs, shoulders, branches, or other obstructions merely to populate a layer. Shot size is determined by subject coverage, not by the presence of a foreground; check that a push-in does not inadvertently tighten beyond the requested framing. Across adjacent shots, preserve deliberate differences in subject coverage, angle, and narrative focus rather than repeating similarly tight framing.
- When authored composition is requested, combine depth layers (前景、中景、后景) with useful screen positions (上方、中央、下方、左侧、右侧、左下、右下等) to place the subject, supporting action, and background explicitly. Use the positions that clarify that shot rather than filling every region mechanically. Anchor them to the current camera view, including low-angle or overhead views. Preserve the user's subject and camera angle when adding secondary actions; for example, do not replace a requested low-angle facial close-up with a downward-following insert of a falling prop.
- Scope photographic preferences to the script or project for which the user gives them. A request for large apertures, shallow depth of field, or another visual treatment in one script does not establish a default for other projects. Keep that art direction in the current prompt or project context; only generalize it when the user explicitly requests a broader default.
- When the user supplies no composition or storyboard framing for the current clip, ask before drafting: “这段需要我描写每个分镜的构图，还是交给 Seedance 自行生成分镜构图？” Do not silently choose. Reuse an explicit choice that already covers the current clip or conversation; do not ask again unnecessarily.
- When the user supplies approximate composition, preserve that scope without filling in unrequested exact positions, frame proportions, foreground/background arrangements, lens choices, depth of field, or camera paths. Ask only about a material ambiguity.
- When the user delegates composition to Seedance, state that Seedance designs the shot division and composition. Focus the prompt on characters, events, action causality, emotion, continuity, total duration, and synchronized sound. Preserve only user-required camera moves, shot boundaries, or reference keyframes; leave other framing, camera choices, cuts, and shot lengths open. Number narrative beats when helpful, clearly labeling them as story order rather than mandatory cuts, and use an approximate beat timeline instead of inventing a rigid shot schedule.
- When the user requests authored composition, specify framing and camera behavior to the requested level. Broad approval does not require exhaustive camera detail.
- A background script's shot size or camera suggestion does not automatically authorize additional detailed composition. Follow the user's current single-shot description; ask about relevant conflicts with the script. Asset sheets establish appearance or spatial facts, not mandatory video framing, unless the user assigns that authority.

## Allocate detail by shot duration

Allocate each shot's prompt length roughly in proportion to its screen time, adjusted for the user's chosen control level and the shot's narrative importance. Short shots get compact instructions; longer shots get more room for action progression, acting, physical feedback, and timing. Treat this as a user-reported production heuristic, not a verified claim about Seedance's internal attention mechanism.

- For a short arrival, transition, or hold, state essential action, end state, continuity, and synchronized sound concisely; include composition and camera only within the chosen scope.
- For a longer or primary shot, spend the detail budget on the intended performance and motion progression. Do not pad static holds merely to match a word-count ratio.
- Keep critical constraints explicit even in a very short shot, especially impact timing, precise camera moves, reference-image authority, and required final poses.
- In brief shots built around one key action, keep the setup minimal and concentrate detail on that action. Omit optional weaker versions, intermediate pose grades, or secondary beats that compete with the intended result; describe a continuous transition into the key action without inventing a ladder of small changes. Preserve intermediate states only when the user explicitly needs them.
- Put shared appearance, weather, and material continuity in global sections; repeat within shots only where the action changes them or a critical visual cue requires reinforcement.
- Check the relative length of shot sections before delivery: a brief supporting shot should not receive the same exhaustive treatment as a longer main shot without a specific reason.
- When shortening a clip, re-edit the shot plan rather than merely shrinking every time range. Merge redundant reactions, enter actions already underway, and use motivated cuts for elapsed time. Preserve user-required beats, intelligible dialogue, object interactions, and a readable ending. Do not equate cinematic quality with long holds or slow motion; estimate duration from the actual action load, and label an unspecified total as a proposal rather than carrying over the previous clip's duration.

## Viewpoint, compositing, and transitions

- Distinguish the filming viewpoint from any in-scene device's viewpoint. Resolve each POV's physical origin, height, direction, and framing internally before writing. Only when the user or references establish a device as fixed should its installation point remain continuous across cuts and split screens, unless relocation is explicitly part of the action. Moving or handheld devices follow their established movement. Keep exact installation locations and heights in the current project prompt, not this skill.
- When a fixed device's placement is unclear in a shot, use visible mounting details or a few relevant spatial landmarks only if they fit the requested framing and clarify the ambiguity. Do not require a mounting connection in every shot or add unseen surroundings to prove placement. Distinguish filming-camera movement, device movement, and movement of its individual parts according to the established structure.
- A lens POV excludes that same camera's body, lens housing, support, and operator unless physically visible for a specific requested reason. Other devices or people may appear when actually visible from that POV. Viewfinder UI is an independently authorized overlay, not evidence that the camera body should be shown.
- Scope explicitly requested UI/effect exceptions to the specified shots and visual form; do not extend them to other shots or unrelated graphics. Reconcile global exclusions with local exceptions instead of leaving contradictory instructions. Distinguish physical in-scene text from subtitle overlays. Keep project-specific compositing colors, app names, and effect designs in the project's prompt, not this reusable skill.
- Separate editorial notes from generated action. Do not generate dissolves, flashback effects, or other transitions supplied only as editing notes. When a transition is explicitly requested, define its visible outgoing state, trigger, incoming state, and useful matching anchor; avoid unintended character morphing or instant tree growth. Keep offscreen light sources out of transition prose too.

## Build the prompt

1. Read the images in the user's supplied order and call them 图1、图2、图3…… unless the user assigns other labels.
2. Define the exact purpose of every image: shot start, shot end, intermediate state, composition, pose, expression, environment, prop, or lighting reference.
   - Build an explicit authority map for each image. A reference may control the full frame, or only one attribute such as expression, pose, prop state, impact moment, lighting, or environment.
   - Do not automatically treat every intermediate reference as a composition target or mandatory frame. When multiple references share a similar shot but differ in small ways, preserve continuous motion from the established camera instead of letting the prompt jump between reference frames.
   - If the user's intended authority for an image is materially ambiguous, ask which attributes it should control before drafting. Do not guess composition authority.
3. Reconcile total duration with all specified shot durations. Allocate enough time for setup, action, reaction, and end-state hold; never leave contradictory totals. When Seedance controls shot division, keep the total duration and necessary action timing, but do not invent fixed shot durations.
4. For user-specified or requested authored shots, write explicit sections: 镜头1、镜头2…… Restart numbering for each standalone generation. When shot division is delegated to Seedance, use numbered narrative beats instead, without imposing a cut at each beat.
5. Describe actions as a causal sequence with readable timing: stimulus → gaze or body response → action → physical feedback → emotional reaction. State whether an action is fast, abrupt, gradual, delayed, forceful, or weak.
6. Apply the composition choice before writing camera instructions. Where the user requests camera control, describe the relevant framing, path, speed, stopping behavior, and transitions at the requested level; otherwise leave these choices to Seedance.
7. Preserve continuity across images and shots: identity, face, hair, costume damage or dirt, wetness, props, handedness, pose, screen direction, spatial layout, weather, and lighting.
8. Give each specified shot (or narrative beat when shot division is delegated) its own synchronized sound description. Unless the user explicitly requests an exception for the current clip, write the literal constraint “全片无BGM、无字幕、无UI。” in the prompt; merely omitting these elements is insufficient. Handle each category independently: an explicit request for music does not authorize subtitles or UI, and spoken dialogue does not authorize subtitles. Preserve only the expressly requested exceptions and explicitly exclude the remaining categories. A background script's music, subtitle, or UI suggestions do not by themselves establish user intent; follow the current request and ask about a material ambiguity. Default delivery also excludes dialogue bubbles. Retain appropriate diegetic ambience, action sounds, requested dialogue, vocal reactions, and object feedback. A phone lighting up is silent unless the user requests a sound.
9. End with a compact timeline table covering only useful items such as time range, action/camera, emotion/light/sound.

## Performance and physics

- Describe environment positions directly from the current shot's viewpoint. For a camera POV, state only the visible landmarks and useful positions, such as “右侧是前院大树，左侧是混凝土车道，远处是街道和对街房屋”. Resolve reverse-angle geometry internally; do not narrate how positions convert from an opposite viewpoint or repeat a spatial walkthrough unless the user asks for that explanation. Retain only landmarks needed for the composition, action, or camera move.
- Translate emotion into controllable facial and bodily detail: brows, eyelids, pupils, gaze target, mouth corners, lips, jaw, breathing, shoulders, hands, center of gravity, and pauses.
- Keep reactions ordered. The character first sees the stimulus, then the face changes; do not make the emotional result appear before the cause.
- Describe object motion with direction, speed, force, collision, rebound, deformation, and settling when relevant. If impact is important, prefer a direct trajectory over optional drifting that weakens it.
- When framing makes the direction clear, anchor important motion or gaze to screen coordinates (such as “画面左下”) to clarify body-relative or travel-relative wording. Either coordinate system can work; combine them only when consistent. Distinguish screen-left from the character's left, and reassess screen directions after camera movement or a cut.
- Background people should have staggered, varied body actions and facial micro-actions rather than synchronized crowd behavior. Avoid a row of uniformly wide eyes and open mouths or mechanical head turns. Give selected people different smile progressions, mouth-corner movement, brief blinks, gaze tracking, and expression settling; keep some reactions quiet so the crowd remains natural at the requested scale.
- When several phones or cameras must register as distinct photo events, assign each event to a visible device and give it a readable staggered cadence within the shot. Synchronize finger press, device response, shutter sound, and any authorized flash; do not rely on a generic sentence about multiple photographers. Distinguish still-photo events from continuous phone recording, and avoid flashes on every device unless requested.
- In moving-camera shots, distinguish world-anchored foreground objects from camera-mounted elements. Specify depth-driven parallax and frame exit when the camera passes stationary people or props. For changing light patches or glare, tie visible motion to foliage, occlusion, or viewpoint changes rather than treating the effect as a screen-fixed overlay or inventing an independently moving light source.
- In stylized rain scenes, explicitly call visible droplets “白色水滴” when contrast is necessary. Keep droplets forming, sliding, gathering, falling, and reforming on hair, skin, clothes, hands, and bare feet even when the character pauses.

## Revision rules

- Before revising, consolidate all still-active user corrections, not only the newest message. Preserve accepted staging, casting, scene, sound, format, and scope; distinguish the current revision from a new clip. Normalize obvious voice-transcription errors and stray numbering using context, but ask about a material unresolved ambiguity rather than inventing a major action or spatial reversal.
- When the user supplies an explicit storyboard, preserve its viewpoints, compositions, internal cuts, action order, and casting/driver roles; refine execution rather than substitute a different shot plan. Keep camera translation, camera pan, subject movement, and background drift distinct. Ask about an unresolved directional conflict before fixing screen direction, instead of silently reversing vehicle travel or moving an installed camera.
- For this user's authored storyboard format, include each shot's number, time range, duration, and concise photographic parameters in the prompt body, not only in the external timeline. Treat focal length, aperture, frame rate, and shutter as visual guidance, not verified generation controls. Scope parameter detail to the requested format and keep durations consistent with the total.
- Default to editing only the affected shot content for local action, expression, pacing, or camera revisions. Preserve reference definitions and global appearance, style, continuity, emotion, and sound sections unless the change actually affects them. Update linked shot sound or timeline entries only when needed for consistency, and explain any necessary cross-section change briefly. A request for a full copy changes delivery scope, not permission to rewrite unaffected text.
- Apply the user's latest instruction directly. Remove superseded actions and wording instead of adding phrases such as “不要旧动作、改做新动作”.
- For a genuinely small isolated revision delivered as a patch, provide an exact, searchable original excerpt and its revised counterpart. Copy originals verbatim from the latest available text, without ellipses or paraphrase. This patch format does not apply to full-version delivery.
- If several shots or linked reference/global/timing sections change, automatically return one clean complete prompt rather than many replacement fragments. Also return the full prompt whenever requested. Full delivery preserves unaffected text and incorporates all active corrections; it does not authorize redesigning approved shots.
- When the user asks only for a timeline, return only the timeline. Do not redeliver or rewrite the prompt unless requested.
- When a generated result is supplied, distinguish visible failures from inferred prompt causes. Inspect framing, direction, mounting, product shape, and subject placement, then repair both local and global phrases that could recreate the failure. Do not claim a prompt revision guarantees generation accuracy.
- Do not preserve obsolete plot beats merely because they appeared in an earlier draft.
- Check for duplicated words, mojibake, contradictory positives and negatives, wrong shot numbering, missing image roles, and duration errors before delivery.

## Continuous improvement

Apply continuous improvement across projects, not only within the project where this skill was created. During an active prompt-writing or revision turn, when the user gives feedback that demonstrates a genuinely reusable method, separate it from story-specific direction and add the reusable rule to this skill without requiring a separate reminder. This is an in-turn maintenance workflow, not background learning or silent work after the conversation ends.

Reusable guidance includes output structure, continuity handling, timing discipline, attention allocation, camera-language precision, screen-space direction, expression causality, object physics, or revision behavior. Keep one-off character actions, client notes, plot facts, exact durations, named characters, and project-only art direction in the current prompt rather than turning them into global rules. Do not update the skill merely because a user requests a different creative choice once; prefer feedback that states a general principle or demonstrates a repeated failure pattern.

Skill maintenance is conditional on authorization and writable access. If the user has authorized ongoing maintenance, update the canonical shareable source when it can be identified, keep the installed copy aligned, run the standard validator on both, and synchronize the authorized Git remote. If the canonical source or push authorization is unavailable, update only the writable authorized copy and report what remains unsynchronized. Never let maintenance delay delivery of the requested prompt unnecessarily.

## Output format

For this user's authored prompts, default to the latest confirmed numbered storyboard format below. Use “切到……” inside shot prose where useful, not as a substitute for shot numbers, timing, parameters, composition, and sound. Use compact continuous narrative or delegated shot design only when the user requests it. Estimate duration from action completion, natural dialogue delivery, reactions, and product demonstration; present an inferred duration as an editorial recommendation, not a guarantee of model output.

Put the complete prompt in one plain-text code block for easy copying. Separate major sections with one blank line. Use this order when applicable:
Within each shot, use consecutive lines without blank lines between photographic parameters, composition, action, and sound. Keep one blank line between shots; do not pad internal shot formatting.

```text
参考图定义：
图1……

全片质感与连续性：
……

声音总则：
……

镜头1｜0—X秒｜时长X秒：
拍摄参数：……
视角与构图：
……
动作与运镜：
……
同步声音：
……

镜头2｜X—Y秒｜时长Z秒：
……
```

When shot division is delegated to Seedance, replace the shot headings with numbered narrative-beat and sound headings, and state that these beats do not prescribe cuts or composition.

After the code block, add `简易时间线：` and a concise Markdown table. Do not bury the timeline inside the long prompt. Use approximate narrative-beat timing when Seedance controls shot division.
