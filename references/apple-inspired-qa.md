# Final-video QA against the agreed direction

Read after rendering and before final delivery. Compare the actual `<output-dir>/presentation-video.mp4` with the direction, plan, and composition brief; write `<output-dir>/video-qa.md`.

## Review evidence

1. Confirm the file is readable and its dimensions/duration match the chosen format and duration. Identify the reviewed file with its modification time and SHA-256 when available, so the report cannot silently refer to an older render.
2. Play the final MP4 through the available media review tool, or inspect decoded final-video frames plus adjacent-frame sequences for motion and listen to the extracted audio. Use existing local tools such as FFmpeg where available; Hyperframes preview and composition snapshots are useful supplements but do not prove the MP4 matches.
3. Review the hook, every product scene, transition boundaries, settled reading holds, and the outro. Decode frames from the MP4 at those times into `<output-dir>/qa/`. For movement, inspect a short sequence around the action and arrival; one still cannot establish smoothness or audio timing.
4. Compare every applicable direction ID with the planned scene/time mapping. Include timestamped evidence and actual asset paths. Check source fidelity, the primary message, readability, intended movement, shot continuity, separation of layers, and the selected sound/delivery choices.
5. Listen for the planned audio arc, harsh or crowded cues, visible-action alignment, and clean endings. Honor `--no-music`, `--no-sfx`, intentional silence, and optional narration choices. If audio cannot be heard or motion cannot be reviewed, record those items as unverified.

For text, count only fully visible settled time, not entrance/exit time. Use the existing floors: about 0.8s for a short label; about 0.3s per word, minimum about 1.2s, for a sentence. Check the planned target display size rather than relying on a zoomed image.

## Decision and corrections

Use one status per criterion: **pass**, **fail**, **unverified**, or **not applicable** with a reason. A filmed gesture can pass its visible-action criterion but cannot certify live input latency, interruptibility, gesture recognition, or accessibility compliance.

Overall **pass** requires every applicable agreed criterion to pass and the technical validation/render checks to be complete. An intentional user-requested exception is assessed against the agreed alternative. A failed criterion is not repaired by reducing its score or changing the direction after the fact just to match the render.

When a material deviation is fixable, update the composition (and plan/brief if the chosen solution changes scene timing), rerun the relevant Hyperframes checks, rerender, and review the new MP4. Keep the original intent and record the correction. After two unsuccessful correction cycles, report the remaining blocker and the artifact as needing review instead of looping indefinitely. Respect existing render authorization; this QA step adds no new approval requirement.

If review tools are unavailable or evidence is incomplete, use overall **needs review**, state the exact limitation and remaining checks, and provide the available artifact without presenting it as approved. Never claim playback, listening, or a visual pass that did not occur.

## QA report structure

- **Reviewed render:** MP4 path, file identity, format, duration, and review method.
- **Creative target:** direction/plan/brief paths and the agreed tone or exceptions.
- **Criterion results:** a table with ID, expected result, observed result, scene/timestamp, evidence path, status, and corrective action where relevant.
- **Technical and audio results:** applicable Hyperframes checks, playback/decoding result, and audio listening findings or limitations.
- **Corrections and rereview:** what changed and which render was checked afterward.
- **Outcome:** pass or needs review, with unresolved failures/unverified items named explicitly.

Link only evidence that exists. A written expectation or a successful lint result is not visual evidence. Regenerate this report after any change to the final MP4.
