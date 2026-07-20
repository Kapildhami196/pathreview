# JOURNAL

## Week 7 — Issue Selection

**Issue link:**  
https://github.com/ascherj/pathreview/issues/148

**Issue title:**  
Skill extractor fails to detect JavaScript and TypeScript

**Tier:**  
☑ Tier 1  
☐ Tier 2  
☐ Tier 3

### Problem summary

The skill extractor currently does not recognize JavaScript and TypeScript when scanning repositories. Because these languages are not detected correctly, repositories that use them may produce incomplete or inaccurate skill analysis results. The issue affects the language detection logic in the skill extractor parser. A successful fix updates the detection logic so JavaScript and TypeScript are identified correctly while preserving the existing detection behavior.

### Issue selection reasoning

I selected this Tier 1 issue because it has a clearly defined scope and mainly affects one parser file. It includes existing tests that verify the expected behavior, making it straightforward to reproduce the issue and confirm the fix. Since this is my first contribution to a larger open-source codebase, I wanted an issue with a focused scope that would help me become familiar with the project's structure and contribution workflow without requiring changes across multiple modules.

**Branch name:**  
fix/148-detect-javascript-typescript

**Setup confirmation:**  
☑ App runs locally at localhost:5173

**Cohort ledger:**  
☑ Issue added to cohort ledger