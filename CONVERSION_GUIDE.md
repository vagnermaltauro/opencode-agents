# Claude Code to OpenCode Agent Conversion Guide

Quick reference for understanding the conversion from Claude Code to OpenCode format.

## Format Comparison

### Claude Code Format
```yaml
---
name: agent-name
description: Agent description
model: sonnet
---

System prompt content here...
```

### OpenCode Format
```yaml
---
description: Agent description
mode: subagent
tools:
  read: true
  write: true
  bash: true
permission:
  bash: allow
  "git *": allow
---

System prompt content here...
```

## Key Mapping

| Claude Code | OpenCode | Notes |
|-------------|----------|-------|
| `name` | filename | Agent ID comes from filename in OpenCode |
| `model` | (removed) | Model selection not in agent config |
| (none) | `mode` | New: primary/subagent/all |
| (implicit) | `tools` | Explicit tool permissions required |
| (implicit) | `permission` | Granular bash command control |

## Mode Options

- **`subagent`**: Invoked via @mention (most converted agents)
- **`primary`**: Accessible via Tab key
- **`all`**: Works as both primary and subagent

## Tool Permissions

### Common Tool Configurations

**Read-only Agent**:
```yaml
tools:
  read: true
  grep: true
  glob: true
  bash: false
```

**Development Agent**:
```yaml
tools:
  read: true
  write: true
  edit: true
  grep: true
  bash: true
permission:
  bash: allow
  "npm *": allow
  "git *": allow
```

**Analysis Agent**:
```yaml
tools:
  read: true
  grep: true
  glob: true
  bash: true
permission:
  bash: allow
```

## Bash Permission Patterns

### Allow Specific Commands
```yaml
permission:
  bash: ask          # Default requires approval
  "git status *": allow
  "npm test": allow
  "docker ps": allow
```

### Language-Specific Permissions
```yaml
# Python Development
permission:
  bash: allow
  "pip *": allow
  "python *": allow
  "pytest *": allow

# Go Development
permission:
  bash: allow
  "go *": allow

# JavaScript/Node
permission:
  bash: allow
  "npm *": allow
  "yarn *": allow
  "pnpm *": allow
```

### Security-Sensitive Agents
```yaml
permission:
  bash: ask          # Always ask for approval
  "kubectl *": ask   # Kubernetes operations
  "docker *": ask    # Docker operations
```

## Conversion Patterns by Agent Type

### Persona Agents
- **Mode**: `subagent` (invoke when needed)
- **Tools**: Varied based on role
- **Permissions**: Conservative (ask by default)

### Language-Specific Agents
- **Mode**: `subagent`
- **Tools**: Read, Write, Edit, Bash
- **Permissions**: Language toolchain allowed

### Infrastructure Agents
- **Mode**: `subagent`
- **Tools**: Read, Write, Grep, Bash
- **Permissions**: Infrastructure commands require approval

### Analysis Agents
- **Mode**: `subagent`
- **Tools**: Read, Grep, Glob, Bash (optional)
- **Permissions**: Read-only preferred

## Example Conversions

### Before (Claude Code)
```yaml
---
name: python-pro
description: Python expert for modern development
model: sonnet
---
```

### After (OpenCode)
```yaml
---
description: Python expert for modern development
mode: subagent
tools:
  read: true
  write: true
  edit: true
  grep: true
  bash: true
permission:
  bash: allow
  "pip *": allow
  "python *": allow
---
```

## Best Practices

### 1. Start Conservative
Begin with `bash: ask` and relax permissions as needed.

### 2. Match Tools to Role
- **Architects**: Read, Grep, Glob (analysis focus)
- **Developers**: Read, Write, Edit, Bash (implementation focus)
- **Mentors**: Read, Write (educational focus)

### 3. Use Glob Patterns
```yaml
permission:
  "git *": allow        # All git commands
  "npm install *": allow # Only npm install
  "docker ps": allow    # Exact command only
```

### 4. Consider Security
Sensitive operations should use `ask` or `deny`:
- Database operations
- Production deployments
- System administration
- Credential management

### 5. Document Customizations
Add comments to explain non-standard permissions:
```yaml
permission:
  bash: allow
  # Allow Kubernetes read operations only
  "kubectl get *": allow
  "kubectl describe *": allow
  "kubectl logs *": allow
```

## Testing Converted Agents

1. **Invoke in OpenCode**:
   ```
   @agent-name help me with this task
   ```

2. **Verify Tool Access**:
   - Check that agent can use declared tools
   - Confirm bash permissions work as expected

3. **Adjust as Needed**:
   - Add missing tool permissions
   - Refine bash command patterns
   - Change mode if needed

## Common Issues & Solutions

### Issue: Agent can't access files
**Solution**: Add read/write tools
```yaml
tools:
  read: true
  write: true  # if needed
```

### Issue: Bash commands blocked
**Solution**: Add specific permissions
```yaml
permission:
  bash: allow  # or specific patterns
```

### Issue: Agent not appearing
**Solution**: Check filename matches invocation
- File: `python-pro.md`
- Invoke: `@python-pro`

### Issue: Too permissive
**Solution**: Use ask for approval
```yaml
permission:
  bash: ask
  "safe-command *": allow
```

## Migration Checklist

- [ ] Agent file created in `~/.config/opencode/agent/`
- [ ] Description field populated
- [ ] Mode set (subagent/primary/all)
- [ ] Tools permissions configured
- [ ] Bash permissions appropriate for agent role
- [ ] System prompt content preserved
- [ ] Agent tested with @mention invocation
- [ ] Permissions verified and adjusted

---

**Last Updated**: 2026-01-16
**Total Agents Converted**: 19
