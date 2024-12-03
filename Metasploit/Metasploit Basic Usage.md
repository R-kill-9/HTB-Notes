## Basic usage
- Run the command `msfconsole` to open Metasploit.
- Use `search <vulnerability>` to find different exploits.
- Choose the one you want to use with `use <number>`.
- Use `show options` to select the payload.
- Choose the payload with `set payload <number>`.
- Set the necessary parameters seen with `show options` using `set <parameter> <value>`. Only the ones marked with **yes** are mandatory.
- To execute, use `run` or `exploit`.

## Workspace
**Workspace** is a feature that allows you to manage multiple sets of data in the Metasploit database. Each workspace acts as a separate container for storing information like host scans, services, vulnerabilities, and credentials, making it easier to organize data from different penetration testing engagements or target environments.

**List Workspaces:**

```bash
workspace
```

**Create a New Workspace:**

```bash
workspace -a <workspace_name>
```

**Switch to a Workspace:**

```bash
workspace <workspace_name>
```

**Delete a Workspace:**

```bash
workspace -d <workspace_name>
```

