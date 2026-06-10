# Contribution #1: [JENKINS-42816] Agent Terminology Cleanup

**Contribution Number:** 1  
**Student:** Rajiv Ranjan Sahu  
**Issue:** https://github.com/jenkinsci/jenkins/issues/21944  
**PR Link:** https://github.com/jenkinsci/jenkins/pull/26907
**Status:** Phase II — Awaiting Review

---

## Why I Chose This Issue

I chose JENKINS-42816 because it is a well-structured EPIC in Jenkins core that directly matches my Java and CI/CD background. I have 7+ years of professional experience building and maintaining CI/CD pipelines using Jenkins at Motorola Solutions and Siemens Healthineers — I have monitored Jenkins build pipelines, managed artifact repositories, and written developer documentation as part of my daily work. Contributing to Jenkins core feels like a natural extension of that experience.

The issue involves replacing deprecated "slave" and "master" terminology with the modern "agent" and "controller" equivalents across Jenkins plugins, UI, and documentation. This is exactly the kind of precise, high-care work I have done professionally — reading code I didn't write, understanding its context, and making targeted changes without breaking existing behavior. The issue is explicitly newcomer-friendly, with maintainers providing clear scope rules and a GitHub search query to find affected files.

"Fixed" is clearly defined: all occurrences of "slave" in the targeted module are replaced with "agent" (where appropriate), all occurrences of "master" are replaced with "controller" (where appropriate), existing tests pass, and the PR follows Jenkins contribution guidelines.

---

## Understanding the Issue

### Problem Description

Jenkins deprecated the terms "slave" and "master" in Jenkins 2.0, replacing them with "agent" and "controller" respectively. However, many occurrences of the old terminology still exist across Jenkins core, plugins, UI strings, comments, and documentation. This EPIC tracks the ongoing cleanup effort.

### Expected Behavior

All user-facing strings, internal variable names (where safe to rename), comments, and documentation should use "agent" and "controller" instead of "slave" and "master."

### Current Behavior

Occurrences of "slave" and "master" still exist in parts of Jenkins core and its plugin ecosystem, inconsistent with the project's official terminology decision.

### Affected Components

- Jenkins core (`jenkinsci/jenkins`) — UI strings, Jelly views, Java source files, documentation
- Scope to be narrowed to one specific module or plugin in Phase II

---

## Reproduction Process

### Environment Setup

No local environment needed for this change. The issue targets user-visible UI text in a .jelly template file. The fix was made entirely via the GitHub web interface as suggested in the issue description.

### Steps to Reproduce

1. Navigate to any Jenkins agent's System Information page (e.g. http://<jenkins-url>/computer/<agent-name>/systemInfo)
2. The page header displays the Remoting version using the deprecated term slaveVersion
3. Expected: should use agentVersion to match the modern "agent" terminology
4. Actual: displays ${it.slaveVersion} which is outdated "slave" terminology

### Branch Link:
https://github.com/rajivranjan7/jenkins/tree/fix-issue-21944-slave-terminology

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/rajivranjan7/jenkins/commit/fix-issue-21944-slave-terminology
- **Screenshots/logs:** Change visible in systemInfo.jelly at line 46
- **My findings:** Confirmed `${it.slaveVersion}` still present in the file before fix; replaced with `${it.agentVersion}`

---

## Solution Approach

### Analysis

1. Identified `systemInfo.jelly` in `core/src/main/resources/hudson/slaves/SlaveComputer/` as containing deprecated `slaveVersion` reference on line 46
2. Replaced `${it.slaveVersion}` with `${it.agentVersion}` in the user-visible heading
3. No public API or persistence model changed — safe trivial change per issue scope rules
4. Files changed: `core/src/main/resources/hudson/slaves/SlaveComputer/systemInfo.jelly`

### Proposed Solution

Target one specific module within Jenkins core, identify all occurrences of deprecated terminology, apply safe renames following the project's scope rules, and submit a focused PR.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** Replace deprecated "slave"/"master" terms with "agent"/"controller" in a scoped, safe, and reviewable way.

**Match:** Review recently merged terminology cleanup PRs in the Jenkins repo to match their style, commit format, and PR description pattern.

**Plan:**
1. Use the GitHub search query `org:jenkinsci slave` to identify affected files
2. Pick one module or plugin with a manageable number of occurrences
3. Apply renames following the project's scope rules (avoid public API and persistence model changes)
4. Verify existing tests still pass
5. Submit a focused PR referencing JENKINS-42816

**Implement:** [Link to branch/commits — to be added in Phase III]

**Review:** [Self-review checklist — to be completed before PR]

**Evaluate:** All existing tests pass; no public API or persistence model changed; PR description references the EPIC

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: Existing tests pass after terminology changes
- [ ] Test case 2: No public API signatures changed
- [ ] Test case 3: UI strings render correctly with new terminology

### Integration Tests

- [ ] Jenkins builds and starts successfully after changes
- [ ] Affected plugin loads without errors

### Manual Testing

[To be completed in Phase III]

---

## Implementation Notes

### Week 1 Progress

Selected issue JENKINS-42816. Confirmed it is an active, newcomer-friendly EPIC in Jenkins core with clear scope rules provided by maintainers. Forked the jenkinsci/jenkins repository and set up this Contribution README. Will identify specific target module and set up local development environment in Week 2.

### Week 2 Progress
Identified specific target file `systemInfo.jelly`. Fixed directly via GitHub web interface on branch `fix-issue-21944-slave-terminology`. Ready to open PR.

### Code Changes

- **Files modified:** [To be added in Phase III]
- **Key commits:** [To be added in Phase III]
- **Approach decisions:** [To be added in Phase III]

---

## Pull Request

**PR Link:** [To be added in Phase IV]

**PR Description:** [To be drafted in Phase IV]

**Maintainer Feedback:**
- [Pending]

**Status:** Not yet submitted

---

## Learnings & Reflections

### Technical Skills Gained

[To be completed]

### Challenges Overcome

[To be completed]

### What I'd Do Differently Next Time

[To be completed]

---

## AI Usage Log

[To be completed as I use AI tools during the contribution]

---

## Resources Used

- [Jenkins Contribution Guidelines](https://github.com/jenkinsci/jenkins/blob/master/CONTRIBUTING.md)
- [JENKINS-42816 EPIC on GitHub](https://github.com/jenkinsci/jenkins/issues/21944)
- [Jenkins Terminology Discussion](https://groups.google.com/forum/#!topic/jenkinsci-dev/CLR55wMZwZ8)
