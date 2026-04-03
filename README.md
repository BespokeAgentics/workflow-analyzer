# bespokeagentics:workflow-analyzer

End-to-end client workflow analysis pipeline. Takes a video recording and produces comprehensive workflow documentation with application inventory, challenge mapping, and Claude/AI agent automation recommendations.

## Install

Copy the `.claude/` directory into your target project:

```bash
cp -r .claude/ /path/to/your/project/.claude/
```

## Usage

```bash
/bespokeagentics:workflow-analyzer './recording.mp4' 'Client Name' 'workflow-label' [interval] [--skip-dedup] [--skip-transcribe] [--force]
```

### Arguments

| Argument | Required | Description |
|----------|----------|-------------|
| `video-path` | Yes | Path to video file (MP4, MOV, etc.) |
| `client-name` | Yes | Client's name (quoted if spaces) |
| `workflow-label` | Yes | Short workflow identifier (e.g., `email-workflow`) |
| `interval` | No | Frame extraction interval in seconds (default: 5) |

### Flags

| Flag | Description |
|------|-------------|
| `--skip-dedup` | Skip perceptual frame deduplication |
| `--skip-transcribe` | Skip ElevenLabs audio transcription |
| `--force` | Re-run all phases, ignoring existing outputs |

### Example

```bash
/bespokeagentics:workflow-analyzer './recording.mp4' 'Dejon' 'email-workflow' 5
```

## Pipeline

```
Phase 0: Preprocessing (extract frames -> dedup || transcribe)
Phase 1: Parallel Frame Analysis (N chunks -> synthesis)
Phase 2: Workflow Documentation (transcript analysis || automation mapping -> final report)
```

## Deliverables

- `{client}-workflow-analysis.md` — Full workflow analysis report
- `{client}-workflow-summary.md` — Executive summary
- `application-inventory.md` — Complete application/tool catalog
- `workflow-timeline.md` — Chronological workflow map
- `friction-catalog.md` — Challenges and pain points
- `automation-opportunities.md` — AI automation opportunity map

## Dependencies

- `ffmpeg` — Frame extraction
- `extract-video-frames` skill — Frame extraction script
- `dedupe-frames` skill — Perceptual frame deduplication
- `elevenlabs-transcribe` skill — Audio transcription (optional)

## Repo Structure

```
workflow-analyzer/
├── README.md
└── .claude/
    ├── skills/
    │   └── bespokeagentics:workflow-analyzer/
    │       ├── SKILL.md
    │       ├── references/
    │       └── templates/
    ├── commands/
    │   └── bespokeagentics:workflow-analyzer.md
    └── agents/
        └── workflow-analyzer.md
```

---

Part of [BespokeAgentics](https://github.com/bespokeagentics)
