# Chapter 3: Agent Architecture

## The Loop

Every autonomous agent follows the same pattern:

```
while True:
    task = get_next_task()    # From cron or manual trigger
    context = gather_context() # Memory, skills, past sessions
    action = decide(task, context)  # LLM call
    result = execute(action)  # Tool execution
    learn(result)  # Save to memory/skills
    report(result)  # Notify user
    sleep(interval)
```

## Tools Every Agent Needs

1. **Terminal Access** — Run commands, install packages, manage files
2. **Web Access** — API calls, web scraping, content fetching
3. **Browser Automation** — For platforms without APIs
4. **File System** — Read/write configs, data, outputs
5. **Memory** — Remember across sessions
6. **Scheduling** — Cron jobs for recurring tasks

## The Skill System

Instead of hardcoding behavior, use a skill system:
- Each skill is a markdown file with instructions
- Agent loads relevant skills before acting
- Skills can be created/updated by the agent itself
- Self-improving loop: learn → save as skill → better next time