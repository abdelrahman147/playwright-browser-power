# Power Structure

## Directory Layout

```
playwright-browser/
│
├── 📄 Core Files
│   ├── POWER.md              # Main power documentation (19.9 KB)
│   ├── README.md             # Quick start guide (15.2 KB)
│   ├── mcp.json              # MCP server configuration (311 B)
│   └── icon.png              # Power icon (1.1 MB)
│
├── 📚 Documentation
│   ├── INSTALL.md            # Installation guide (8.4 KB)
│   ├── FAQ.md                # Frequently asked questions (12.6 KB)
│   ├── EXAMPLES.md           # Real-world examples (17.4 KB)
│   ├── QUICK-REFERENCE.md    # Command reference card (6.9 KB)
│   ├── CONTRIBUTING.md       # Contribution guidelines (8.1 KB)
│   ├── CHANGELOG.md          # Version history (4.0 KB)
│   ├── SUMMARY.md            # Complete summary (7.2 KB)
│   └── STRUCTURE.md          # This file
│
└── 🎯 Steering Files
    ├── overlay.md            # Visual overlay system
    ├── visual-feedback-loop.md  # Build → see → fix cycle
    ├── ui-stealing.md        # Component extraction
    ├── testing-suite.md      # E2E and testing workflows
    ├── design-thinking.md    # UI design analysis
    ├── quick-recipes.md      # 20+ common workflows
    └── smart-behaviors.md    # Agent intelligence rules
```

## File Purposes

### Core Files

#### POWER.md
**Purpose:** Main documentation for the power  
**Audience:** AI agents and advanced users  
**Contains:**
- Complete feature documentation
- Tool reference
- Agent instructions
- Configuration options
- Troubleshooting

**When to read:** First activation, when learning all features

#### README.md
**Purpose:** User-facing quick start guide  
**Audience:** End users  
**Contains:**
- Quick start examples
- Installation instructions
- Feature overview
- Common use cases
- Links to other docs

**When to read:** First time using the power

#### mcp.json
**Purpose:** MCP server configuration  
**Audience:** System (Kiro)  
**Contains:**
- Server command and args
- Capabilities configuration
- Viewport settings
- Console level

**When to edit:** Changing browser, viewport, or capabilities

#### icon.png
**Purpose:** Visual identity  
**Audience:** Users (in Powers UI)  
**Contains:**
- Ghost with comedy/tragedy masks
- 512x512 PNG format
- Purple background

**When to use:** Displayed in Powers panel

### Documentation Files

#### INSTALL.md
**Purpose:** Comprehensive installation guide  
**Audience:** Users installing the power  
**Contains:**
- Platform-specific instructions
- Prerequisites
- Troubleshooting installation
- Configuration options
- Verification steps

**When to read:** During installation, when having install issues

#### FAQ.md
**Purpose:** Answer common questions  
**Audience:** All users  
**Contains:**
- 50+ Q&A entries
- Organized by category
- Quick solutions
- Links to detailed docs

**When to read:** When you have a question, before asking for help

#### EXAMPLES.md
**Purpose:** Real-world usage examples  
**Audience:** Users learning workflows  
**Contains:**
- 10 complete examples
- Step-by-step walkthroughs
- Expected outputs
- Tips for success

**When to read:** Learning new workflows, seeing practical usage

#### QUICK-REFERENCE.md
**Purpose:** Quick command lookup  
**Audience:** Active users  
**Contains:**
- Common commands
- Keyboard shortcuts
- Tool selection guide
- Troubleshooting quick fixes
- Pro tips

**When to read:** During active use, as a cheat sheet

#### CONTRIBUTING.md
**Purpose:** Guide for contributors  
**Audience:** Contributors  
**Contains:**
- Contribution guidelines
- Code standards
- PR process
- Issue templates
- Community guidelines

**When to read:** Before contributing, when submitting PRs

#### CHANGELOG.md
**Purpose:** Track version history  
**Audience:** Users and contributors  
**Contains:**
- Version history
- New features
- Bug fixes
- Breaking changes
- Upgrade guides

**When to read:** After updates, to see what's new

#### SUMMARY.md
**Purpose:** Overview of v2.0.0 improvements  
**Audience:** All users  
**Contains:**
- What's new
- Key improvements
- Documentation stats
- Learning path
- Success metrics

**When to read:** Understanding v2.0.0 changes

#### STRUCTURE.md
**Purpose:** Explain file organization  
**Audience:** Power builders, contributors  
**Contains:**
- Directory layout
- File purposes
- When to read each file
- File relationships

**When to read:** Understanding power structure, building similar powers

### Steering Files

#### overlay.md
**Purpose:** Visual overlay system documentation  
**Audience:** AI agents  
**Contains:**
- Overlay injection script
- Control API
- Usage patterns
- Customization options

**When to read:** First activation, when using overlay features

#### visual-feedback-loop.md
**Purpose:** Core visual development workflow  
**Audience:** AI agents  
**Contains:**
- Build → see → fix → verify cycle
- Hot reload integration
- Screenshot strategies
- Error detection

**When to read:** Building UI with visual feedback

#### ui-stealing.md
**Purpose:** Component extraction workflow  
**Audience:** AI agents  
**Contains:**
- Extraction process
- CSS computation
- Recreation strategies
- Adaptation techniques

**When to read:** Stealing UI from websites

#### testing-suite.md
**Purpose:** Comprehensive testing workflows  
**Audience:** AI agents  
**Contains:**
- E2E testing
- Visual regression
- Accessibility audits
- Performance testing
- API testing

**When to read:** Running tests

#### design-thinking.md
**Purpose:** UI design analysis  
**Audience:** AI agents  
**Contains:**
- Design principles
- Visual hierarchy
- Color theory
- Typography
- Layout analysis

**When to read:** Analyzing or improving design

#### quick-recipes.md
**Purpose:** Common task workflows  
**Audience:** AI agents  
**Contains:**
- 20+ ready-to-go workflows
- Step-by-step instructions
- Common patterns
- Quick solutions

**When to read:** Performing common tasks

#### smart-behaviors.md
**Purpose:** Agent intelligence rules  
**Audience:** AI agents  
**Contains:**
- Auto-detection rules
- Error recovery
- Proactive suggestions
- Best practices

**When to read:** Optimizing agent behavior

## File Relationships

```
README.md (Entry Point)
    ├─→ INSTALL.md (Installation)
    ├─→ FAQ.md (Questions)
    ├─→ EXAMPLES.md (Learning)
    ├─→ QUICK-REFERENCE.md (Quick lookup)
    └─→ POWER.md (Complete docs)
            ├─→ Steering Files (Advanced workflows)
            ├─→ CONTRIBUTING.md (Contributing)
            └─→ CHANGELOG.md (History)

mcp.json ←─ INSTALL.md (Configuration)
         ←─ POWER.md (Reference)

icon.png ←─ README.md (Visual)
         ←─ POWER.md (Visual)
```

## Reading Order

### For New Users
1. **README.md** - Get overview
2. **INSTALL.md** - Install the power
3. **Quick Start** (in README) - Try examples
4. **FAQ.md** - Answer questions
5. **EXAMPLES.md** - Learn workflows

### For Active Users
1. **QUICK-REFERENCE.md** - Quick commands
2. **EXAMPLES.md** - Specific workflows
3. **FAQ.md** - Troubleshooting
4. **POWER.md** - Advanced features

### For Contributors
1. **CONTRIBUTING.md** - Guidelines
2. **STRUCTURE.md** - File organization
3. **POWER.md** - Complete reference
4. **CHANGELOG.md** - Version history

### For Power Builders
1. **STRUCTURE.md** - Organization
2. **POWER.md** - Documentation style
3. **Steering Files** - Workflow patterns
4. **CONTRIBUTING.md** - Best practices

## File Size Summary

| Category | Files | Total Size |
|----------|-------|------------|
| Core | 4 | ~1.1 MB |
| Documentation | 8 | ~92 KB |
| Steering | 7 | ~50 KB |
| **Total** | **19** | **~1.2 MB** |

## Maintenance

### When to Update

**POWER.md:**
- New features added
- Tool changes
- Configuration changes
- Agent instructions change

**README.md:**
- Quick start changes
- Installation process changes
- Major feature additions

**INSTALL.md:**
- Installation process changes
- New platform support
- Troubleshooting additions

**FAQ.md:**
- Common questions arise
- New issues discovered
- User feedback

**EXAMPLES.md:**
- New workflows developed
- Better examples found
- User requests

**QUICK-REFERENCE.md:**
- New commands added
- Common patterns change
- User feedback

**CONTRIBUTING.md:**
- Process changes
- New guidelines
- Community feedback

**CHANGELOG.md:**
- Every version release
- Bug fixes
- New features

**Steering Files:**
- Workflow improvements
- New patterns discovered
- Agent behavior changes

## Best Practices

### Documentation
- Keep README concise
- Put details in specific docs
- Link between related docs
- Update CHANGELOG with changes

### Steering Files
- Focus on specific workflows
- Include complete examples
- Explain the "why"
- Keep under 500 lines

### Examples
- Show complete workflows
- Include expected outputs
- Explain edge cases
- Provide tips

### Maintenance
- Update CHANGELOG first
- Keep docs in sync
- Test examples
- Review links

---

**This structure makes the power:**
- Easy to learn (progressive disclosure)
- Easy to use (quick reference)
- Easy to contribute (clear guidelines)
- Easy to maintain (organized structure)

**Version:** 2.0.0 | **Last Updated:** May 1, 2026
