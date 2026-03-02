# Professional Git Commit Strategy

A messy commit history makes debugging, code reviews, and rollbacks incredibly difficult. Professional engineering teams use strict commit strategies to create a readable, easily searchable project history. 

This guide covers the industry standards for writing perfect Git commits.

## 1. The Principle of Atomic Commits

An atomic commit is a commit that contains **exactly one logical change**. 

* **Do not** mix formatting changes with a bug fix.
* **Do not** commit three different, unrelated features at the same time.
* **Why?** If a bug is introduced, you can easily use `git revert` to undo the single specific commit that caused it without accidentally wiping out other unrelated features you built that same day.

## 2. Conventional Commits Specification



The "Conventional Commits" specification is a lightweight convention on top of commit messages. It provides an easy set of rules for creating an explicit commit history, which makes it easier to write automated tools (like generating automatic changelogs or triggering CI/CD pipelines).

### The Standard Format
`<type>(<optional scope>): <subject>`

### Allowed `<type>` Identifiers
* **`feat`**: A new feature for the user or application.
* **`fix`**: A bug fix for the user.
* **`chore`**: Routine tasks, maintenance, or tooling changes that don't modify production code (e.g., updating dependencies).
* **`ci`**: Changes to your CI/CD configuration files and scripts.
* **`docs`**: Changes restricted strictly to documentation.
* **`refactor`**: A code change that neither fixes a bug nor adds a feature (e.g., renaming variables, restructuring directories).
* **`test`**: Adding missing tests or correcting existing tests.
* **`style`**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc.).

### Real-World Examples
* `feat(workflow): add database-driven tool execution in Django REST Framework`
* `fix(ui): resolve responsive layout issue on portfolio React components`
* `chore(deps): update n8n custom node dependencies`
* `docs(readme): add Docker Compose instructions for ELK stack`
* `refactor(api): extract Redis load balancing logic into separate service`

---

## 3. The 7 Rules of a Great Commit Message

When writing the actual text of your commit, follow these industry-standard rules:

1. **Separate subject from body with a blank line:** This allows Git tools to parse your commit log correctly.
2. **Limit the subject line to 50 characters:** Forces you to be concise and prevents the title from being truncated in UI tools.
3. **Capitalize the subject line:** Treat it like the title of a sentence.
4. **Do not end the subject line with a period:** Space is precious; punctuation is unnecessary here.
5. **Use the imperative mood in the subject line:** Write it as a command. 
   * *Correct:* `Add workflow execution engine`
   * *Incorrect:* `Added workflow execution engine` or `Adding workflow execution engine`
   * *Tip:* A good commit message should always be able to complete the sentence: *"If applied, this commit will __YOUR SUBJECT LINE__"*.
6. **Wrap the body at 72 characters:** Ensures the text is easily readable in standard terminal windows.
7. **Use the body to explain *what* and *why* vs. *how*:** The code itself explains *how* you did it. The commit message should explain *why* you made the change and *what* problem it solves.

---

## 4. Example of a Perfect Commit Message

```text
feat(gateway): implement HAProxy load balancing for local nodes

Set up a round-robin load balancer using HAProxy to distribute 
incoming requests across multiple locally running instances. 

This prevents the primary execution node from timing out 
during heavy concurrent request spikes.
```