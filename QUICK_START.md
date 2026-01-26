# Quick Start Guide - OpenCode Agents

Get started with your converted agents in OpenCode.

## 📁 Location
Your agents are in: `~/.config/opencode/agent/`

## 🚀 Using Agents

### Invoke with @mention
```
@architect help me design a microservices system
@frontend build a responsive navigation component
@backend create a REST API for user management
@ai-engineer implement a RAG system with vector search
```

### Common Workflows

**Code Review**:
```
@analyzer investigate this performance issue
@security review this authentication code
@qa suggest test cases for this feature
```

**Development**:
```
@golang-pro optimize this concurrent code
@rust-pro help with memory management
@fastapi-pro design this async API endpoint
```

**Infrastructure**:
```
@kubernetes-architect design this deployment
@terraform-specialist create infrastructure modules
@devops setup CI/CD pipeline
```

**Documentation**:
```
@scribe write API documentation
@mentor explain this concept step-by-step
```

## 🎯 Agent Categories

### Persona Agents (Domain Experts)
- `@architect` - System design & architecture
- `@frontend` - React/Next.js & UI development
- `@backend` - APIs & backend services
- `@analyzer` - Root cause analysis & debugging
- `@security` - Security & threat modeling
- `@performance` - Performance optimization
- `@qa` - Quality assurance & testing
- `@mentor` - Educational guidance
- `@refactorer` - Code quality & refactoring
- `@devops` - Infrastructure & deployment
- `@scribe` - Documentation & writing

### Language Specialists
- `@golang-pro` - Go development
- `@rust-pro` - Rust systems programming
- `@fastapi-pro` - Python FastAPI

### Infrastructure Specialists
- `@kubernetes-architect` - K8s & cloud-native
- `@terraform-specialist` - Infrastructure as Code
- `@database-optimizer` - Database performance

### AI Specialists
- `@ai-engineer` - LLM applications & RAG
- `@prompt-engineer` - Prompt optimization

## ⚙️ Customization

### Change Agent Mode
Edit the agent file to change accessibility:

**Make Primary** (Tab-accessible):
```yaml
mode: primary
```

**Make Available Both Ways**:
```yaml
mode: all
```

### Adjust Permissions

**Allow More Commands**:
```yaml
permission:
  bash: allow
  "docker *": allow
  "npm *": allow
```

**Restrict Commands**:
```yaml
permission:
  bash: ask  # Requires approval
  "rm *": deny  # Blocked
```

## 📝 Best Practices

### 1. Be Specific
❌ `@frontend help`
✅ `@frontend create a responsive navbar with mobile menu`

### 2. Choose the Right Agent
- **Architecture** → @architect
- **Implementation** → Language specialist (@golang-pro, @rust-pro, etc.)
- **Testing** → @qa
- **Debugging** → @analyzer
- **Documentation** → @scribe

### 3. Combine Agents
```
@architect design the system
# Review architecture
@security review this design
# Implement
@golang-pro implement the service
# Test
@qa create test strategy
```

## 🔧 Troubleshooting

### Agent Not Found
- Check filename matches: `python-pro.md` → `@python-pro`
- Verify file is in `~/.config/opencode/agent/`

### Permission Denied
- Check `permission` section in agent file
- Add specific bash command permissions
- Change `bash: deny` to `bash: ask` or `bash: allow`

### Agent Can't Read/Write Files
Add tools to agent file:
```yaml
tools:
  read: true
  write: true
  edit: true
```

## 📚 Next Steps

1. **Try an agent**: `@frontend help me build a component`
2. **Review README.md**: Detailed conversion info
3. **Check CONVERSION_GUIDE.md**: Format reference
4. **Customize**: Adjust permissions and modes to your workflow

## 🆘 Need Help?

- **OpenCode Docs**: https://opencode.ai/docs/agents/
- **Agent Files**: `~/.config/opencode/agent/`
- **Conversion Guide**: `CONVERSION_GUIDE.md`
- **Full README**: `README.md`

---

**Tip**: Start with persona agents (@architect, @frontend, @backend) - they're the most versatile and cover common development tasks!
