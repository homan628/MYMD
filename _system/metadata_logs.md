# AI Processing Logs

> System-wide sequential logs for AI operations.

## Purpose

- **Chronological History**: All actions tracked in time order.
- **Auditing**: Review what changed and why.

## Log File

**File Pattern**: `_system/_logs/YYMMDD_log.md`

All entries are appended to a log file corresponding to the current system date (e.g., `260108_log.md`).

## Log Entry Format

```markdown
## YYYY-MM-DD HH:MM:SS - [Session Title/ID]

**Input**: 
> [Brief summary or preview of input]

**Actions**:
- [Action 1]: [Details]
- [Action 2]: [Details]

**Reasoning**:
[Brief explanation]

---
```

## Maintenance

- Daily splitting prevents massive file sizes.
- No need to archive manually; the date-based naming serves as archiving.
