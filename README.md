# Gemini 3.0 Agent Orchestration System 🚀

A simple yet powerful orchestration system for Gemini 3.0 that uses specialized agents to manage complex projects from start to finish, with mandatory human oversight and visual testing.

## 🎯 What Is This?

This is a **custom Gemini orchestration system** that transforms how you build software projects. Gemini itself acts as the orchestrator with its massive context window (2M+ tokens), managing the big picture while delegating individual tasks to specialized subagents:

- **🧠 Gemini (You)** - The orchestrator with huge context managing todos and the big picture
- **✍️ Coder Subagent** - Implements one todo at a time in its own clean context
- **👁️ Tester Subagent** - Verifies implementations using Playwright in its own context
- **🆘 Stuck Subagent** - Human escalation point when ANY problem occurs

## ⚡ Key Features

- **No Fallbacks**: When ANY agent hits a problem, you get asked - no assumptions, no workarounds
- **Visual Testing**: Playwright MCP integration for screenshot-based verification
- **Todo Tracking**: Always see exactly where your project stands
- **Simple Flow**: Gemini creates todos → delegates to coder → tester verifies → repeat
- **Human Control**: The stuck agent ensures you're always in the loop

## 🚀 Quick Start

### Prerequisites

1. **Gemini 3.0 Access** (or equivalent high-context model interface)
2. **Node.js** (for Playwright MCP)

### Installation

```bash
# Clone this repository
git clone https://github.com/IncomeStreamSurfer/claude-code-agents-wizard-v2.git
cd claude-code-agents-wizard-v2

# Configure your agent runner to point to the .gemini directory
# (Implementation depends on your specific Gemini agent runner tool)
```

The agents are defined in the `.gemini/` directory.

## 📖 How to Use

### Starting a Project

When you want to build something, initialize the system with the prompt in `.gemini/GEMINI.md`:

```
You: "Build a todo app with React and TypeScript"
```

Gemini will automatically:
1. Create a detailed todo list using TodoWrite
2. Delegate the first todo to the **coder** subagent
3. The coder implements in its own clean context window
4. Delegate verification to the **tester** subagent (Playwright screenshots)
5. If ANY problem occurs, the **stuck** subagent asks you what to do
6. Mark todo complete and move to the next one
7. Repeat until project complete

### The Workflow

```
USER: "Build X"
    ↓
GEMINI: Creates detailed todos with TodoWrite
    ↓
GEMINI: Invokes coder subagent for todo #1
    ↓
CODER (own context): Implements feature
    ↓
    ├─→ Problem? → Invokes STUCK → You decide → Continue
    ↓
CODER: Reports completion
    ↓
GEMINI: Invokes tester subagent
    ↓
TESTER (own context): Playwright screenshots & verification
    ↓
    ├─→ Test fails? → Invokes STUCK → You decide → Continue
    ↓
TESTER: Reports success
    ↓
GEMINI: Marks todo complete, moves to next
    ↓
Repeat until all todos done ✅
```

## 🛠️ How It Works

### Gemini (The Orchestrator)
**Your 2M+ Context Window**

- Creates and maintains comprehensive todo lists
- Sees the complete project from A-Z
- Delegates individual todos to specialized subagents
- Tracks overall progress across all tasks
- Maintains project state and context

**How it works**: Gemini IS the orchestrator - it uses its huge context to manage everything

### Coder Subagent
**Fresh Context Per Task**

- Gets invoked with ONE specific todo item
- Works in its own clean context window
- Writes clean, functional code
- **Never uses fallbacks** - invokes stuck agent immediately
- Reports completion back to Gemini

**When it's used**: Gemini delegates each coding todo to this subagent

### Tester Subagent
**Fresh Context Per Verification**

- Gets invoked after each coder completion
- Works in its own clean context window
- Uses **Playwright MCP** to see rendered output
- Takes screenshots to verify layouts
- Tests interactions (clicks, forms, navigation)
- **Never marks failing tests as passing**
- Reports pass/fail back to Gemini

**When it's used**: Gemini delegates testing after every implementation

### Stuck Subagent
**Fresh Context Per Problem**

- Gets invoked when coder or tester hits a problem
- Works in its own clean context window
- **ONLY subagent** that can ask you questions
- Presents clear options for you to choose
- Blocks progress until you respond
- Returns your decision to the calling agent
- Ensures no blind fallbacks or workarounds

**When it's used**: Whenever ANY subagent encounters ANY problem

## 🚨 The "No Fallbacks" Rule

**This is the key differentiator:**

Traditional AI: Hits error → tries workaround → might fail silently
**This system**: Hits error → asks you → you decide → proceeds correctly

Every agent is **hardwired** to invoke the stuck agent rather than use fallbacks. You stay in control.

## 📁 Repository Structure

```
.
├── .gemini/
│   ├── GEMINI.md              # Orchestration instructions for main Gemini
│   └── agents/
│       ├── coder.md          # Coder subagent definition
│       ├── tester.md         # Tester subagent definition
│       └── stuck.md          # Stuck subagent definition
├── .mcp.json                  # Playwright MCP configuration
├── .gitignore
└── README.md
```

## 🎓 Learn More

### Resources

- **[Google DeepMind Gemini](https://deepmind.google/technologies/gemini/)** - Learn about the model

### Support

Have questions or want to share what you built?
- Check out [Income Stream Surfers on YouTube](https://www.youtube.com/incomestreamsurfers)

## 🤝 Contributing

This is an open system! Feel free to:
- Add new specialized agents
- Improve existing agent prompts
- Share your agent configurations
- Submit PRs with enhancements

## 📝 How It Works Under the Hood

This system leverages agentic workflows:

1. **GEMINI.md** instructs main Gemini to be the orchestrator
2. **Subagents** are defined in `.gemini/agents/*.md` files
3. **Each subagent** gets its own fresh context window
4. **Main Gemini** maintains the massive context with todos and project state
5. **Playwright MCP** is configured in `.mcp.json` for visual testing

The magic happens because:
- **Gemini (2M context)** = Maintains big picture, manages todos
- **Coder (fresh context)** = Implements one task at a time
- **Tester (fresh context)** = Verifies one implementation at a time
- **Stuck (fresh context)** = Handles one problem at a time with human input
- **Each subagent** has specific tools and hardwired escalation rules

## 🎯 Best Practices

1. **Trust Gemini** - Let it create and manage the todo list
2. **Review screenshots** - The tester provides visual proof of every implementation
3. **Make decisions when asked** - The stuck agent needs your guidance
4. **Don't interrupt the flow** - Let subagents complete their work
5. **Check the todo list** - Always visible, tracks real progress

## 🔥 Pro Tips

- Gemini maintains the todo list in its context - check anytime
- Screenshots from tester are saved and can be reviewed
- Each subagent has specific tools - check their `.md` files
- Subagents get fresh contexts - no context pollution!

## 📜 License

MIT - Use it, modify it, share it!

## 🙏 Credits

Adapted from the Claude Code Agent Orchestration System.
Powered by Gemini 3.0 and Playwright MCP.

---

**Ready to build something amazing?** Feed `GEMINI.md` to your agent runner and tell it what you want to create! 🚀
