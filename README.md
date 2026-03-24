# openclaw-skills-safe-collaboration

OpenClaw modification safe guard.

This repository provides a production-oriented skill for safe OpenClaw system changes.

## Skill Package

- `openclaw-safe-collaboration/SKILL.md`

## What This Skill Does

This skill enforces dual-role execution for risky OpenClaw operations:

- **Supervisor**: risk analysis, safety constraints, rollback-first mindset
- **Developer**: implementation under Supervisor approval

The workflow is designed to reduce service interruption, config corruption, and unsafe plugin/service operations.

## Supported Scenarios

- Modify `~/.openclaw/openclaw.json`
- Install/remove OpenClaw plugins
- Restart/reload OpenClaw gateway services
- Change channel settings (Feishu, DingTalk, etc.)
- Update agent-level routing/system settings

## Install

Copy the skill folder to your Cursor/OpenClaw skill directory:

```bash
mkdir -p ~/.cursor/skills
cp -R ./openclaw-safe-collaboration ~/.cursor/skills/
```

Then restart your assistant session (or reload skills) to apply.

## Trigger Conditions

The skill should be activated automatically when users request OpenClaw system-level operations, especially:

- Config file edits
- Plugin lifecycle operations
- Service lifecycle operations
- Gateway/channel routing changes

## Enforced Workflow

1. Supervisor risk assessment
2. Developer implementation
3. Supervisor validation
4. Controlled execution and verification

Required checks include:

- Config validity (JSON/schema)
- Dependency/path compatibility
- Service health after changes
- Rollback availability

## Required Response Structure

The skill requires responses in four sections:

1. `Supervisor Analysis`
2. `Developer Implementation`
3. `Supervisor Verification`
4. `Execution Result`

## Example User Requests

- "Upgrade OpenClaw and make sure gateway still runs."
- "Fix Feishu multi-agent routing without breaking current traffic."
- "Install plugin X and verify no config regression."

## Success Criteria

Operations are considered complete only when:

- `openclaw doctor` reports no blocking errors
- Config has no invalid warnings
- Required plugins/channels are configured and healthy
- Gateway/service is running normally

## Notes

- This skill prioritizes service stability over speed.
- It is intended for production-like environments where OpenClaw uptime matters.
