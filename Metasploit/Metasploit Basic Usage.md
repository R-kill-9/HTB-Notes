## Basic usage
- Run the command `msfconsole` to open Metasploit.
- Use `search <vulnerability>` to find different exploits.
- Choose the one you want to use with `use <number>`.
- Use `show options` to select the payload.
- Choose the payload with `set payload <number>`.
- Set the necessary parameters seen with `show options` using `set <parameter> <value>`. Only the ones marked with **yes** are mandatory.
- To execute, use `run` or `exploit`.

## Efficient search
The `search` command in **Metasploit** allows you to find specific modules based on filters.
- To find modules of a particular type, use the `type` filter.
- To find modules by name or related keywords, use the `name` filter.

```bash
# This example lists auxiliary modules for ftp
search type:auxiliary name:ftp
```

## Setting global variables 
In **Metasploit**, you can use **global variables** to avoid manually setting the same value (like `RHOSTS`) every time you switch between modules.

```bash
setg RHOSTS <target_ip>
```

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

