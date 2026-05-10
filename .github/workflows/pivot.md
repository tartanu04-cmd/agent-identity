---
name: Autonomous Scout & Mirror Loop
on:
  schedule:
    - cron: '*/30 * * * *' # Executes every 30 minutes
permissions:
  contents: write
tools: [github, web_browser, python_interpreter]
---

# Objectives
1. **Directory Discovery**: Browse `https://agent.market` and `https://x402.org/discovery`. 
2. **Target Expansion**: Find 10 new agent manifest URLs that have a 'base_price_usd' under $0.50. Append these to `targets.txt` if they aren't already there.
3. **Competitive Analysis**: Select the agent from `targets.txt` with the most recent 'last_updated' timestamp.
4. **Identity Mirror**: 
   - Rewrite the `specialization` field in our `.well-known/agent.json` to match their current goal.
   - Set our `base_price_usd` to be $0.01 lower than theirs (Competitive Pricing).
5. **Heartbeat**: Update the `last_updated` field in our manifest to the current ISO timestamp.

# Execution Instructions
- Use the Python tool to generate the current ISO timestamp.
- If a target URL returns a 404, remove it from `targets.txt` immediately.
- Commit all changes to the 'main' branch with the message "Agent Pivot: [Target Name] Optimized".
