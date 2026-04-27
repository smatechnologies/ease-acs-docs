---
title: PowerShell Ease to ACS Ease migration
description: How to migrate existing PowerShell Ease tasks to the ACS Ease environment using the conversion utilities.
tags: [type/procedural, role/automation-engineer, feature/ease-acs]
sidebar_label: 'Migration'
---

# PowerShell Ease to ACS Ease migration

**Theme:** Build  
**Who Is It For?** Automation Engineer

## What is it?

The conversion program migrates existing PowerShell Ease tasks to the ACS Ease environment.

Ease bundle tasks are converted from a single task to a sub-schedule of separate tasks run in sequence. The sub-schedules are installed on the local OpCon system and triggered by a BUNDLE-* task type, which injects a container job into **EASE-LOCAL**.

- Use this process to convert existing Windows embedded script Ease tasks to ACS Ease tasks without modifying frequencies, dependencies, or events.
- Use this process when Ease bundle tasks need to be converted to the sub-schedule structure required by ACS Ease.

## Install conversion utilities
Download the ACS Ease migration software (`ACSEaseMigration.zip`) from the FTP site `/OpCon Releases/Integrations/Ease/Migration Utility` and extract it into a directory on a Windows system.

Edit `Conversion.config`, setting the required values and encrypting passwords and tokens with `Encrypt.exe`.

```
[GENERAL]
DEBUG=OFF

[OPCON]
OPCON_API_ADDRESS=DESKTOP-QMQS7D3:443
OPCON_API_TOKEN=5a4459795a4749335a4749744e6a41354f433030595441344c546868596d51744d6a6b794d32457a4e4445345a574a6b
OPCON_PROFILE_NAME=OPCONXPS
OPCON_DB_SERVER=DESKTOP-QMQS7D3
OPCON_DB=opconxps
OPCON_DB_USER=sa
OPCON_DB_USER_PASSWORD=4d4842444d4735346343513d
OPCON_USER=ocadm
OPCON_USER_PASSWORD=6233426a6232353463484d3d

```

where

| Property | What It Does | Default | Notes |
|---|---|---|---|
| **DEBUG** | Enables or disables debug logging for the conversion utilities | OFF | Set in the `[GENERAL]` section |
| **[OPCON]** | Section header identifying the target OpCon system | — | The header name must match the `-opc` argument used in the utilities |
| **OPCON_API_ADDRESS** | Address and port number of the OpCon Rest-API | — | Required |
| **OPCON_API_TOKEN** | OpCon application token | — | Must be encrypted using `Encrypt.exe`. Required |
| **OPCON_PROFILE_NAME** | Profile name for the OpCon connection | OPCONXPS | — |
| **OPCON_DB_SERVER** | Address of the OpCon database server | — | Required |
| **OPCON_DB** | OpCon database name | — | Required |
| **OPCON_DB_USER** | Database user with required privileges to interact with the OpCon database | — | Required |
| **OPCON_DB_USER_PASSWORD** | Password of the database user | — | Must be encrypted using `Encrypt.exe`. Required |
| **OPCON_USER** | OpCon user with required privileges to interact with schedules | — | Required |
| **OPCON_USER_PASSWORD** | Password of the OpCon user | — | Must be encrypted using `Encrypt.exe`. Required |

## Encrypt.exe utility
The `Encrypt.exe` utility uses 64-bit encryption to encrypt text strings. Use it to encrypt all passwords and tokens in `Conversion.config`.

| Argument | What It Does | Default | Notes |
|---|---|---|---|
| **-v** | The text string to encrypt | — | Enclose strings with special characters in double quotes. Required |

To encrypt the value `abcdefg`, run:

```
Encrypt.exe -v "abcdefg"

```

### CreateEaseAgent.exe utility
The `CreateEaseAgent.exe` utility creates the ACS Ease agent definition used by the converted tasks.

It extracts the encrypted Ease connection property from the target OpCon system and uses the decrypted values to configure the Ease DataCenter settings.

| Argument | What It Does | Default | Notes |
|---|---|---|---|
| **-mn** | Name of the ACS Ease agent to create | — | Required |
| **-opc** | Name of the target OpCon system | — | Must match a section header in `Conversion.config`. Required |
| **-id** | Customer Ease ID | — | Required |
| **-p** | Name of the encrypted property containing the Ease connection information | — | Required |
| **-lapi** | Address of the local OpCon Rest-API server | — | Format: `server:port`. Required |
| **-lusr** | Local user name for Rest-API access | — | Required |
| **-lpwd** | Password of the local user | — | Required |

To create agent EASE001, run:

```
CreateEaseAgent.exe -opc OPCON -mn EASE001 -id 999 -p  EaseConnection -lapi OPCON:443 -lusr apiusr -lpwd opconxps

```

### ConvertEaseTasks.exe utility

The `ConvertEaseTasks.exe` utility converts Windows embedded script Ease tasks to ACS Ease tasks. It scans each schedule for Windows tasks with an embedded script name starting with `EASE`. For each matching task, the utility copies the Windows properties, resets the job to a null job, sets the task type to ACS / Ease, and converts the script arguments to an ACS Ease job definition. If the script has no `-Identifier` argument, the utility inserts a default value of `0001`.

Existing definitions — frequencies, dependencies, and events — are not modified. Only the task data type changes. Definitions are case-sensitive.

| Argument | What It Does | Default | Notes |
|---|---|---|---|
| **-jf** | Job filter for tasks to convert | — | Supports wildcards. Use `ALL` to convert all matching Ease embedded script tasks. Required |
| **-mn** | Name of the ACS agent to associate with converted tasks | — | Required |
| **-opc** | Name of the target OpCon system | — | Must match a section header in `Conversion.config`. Required |
| **-sf** | Schedule filter for schedules to convert | — | Supports wildcards. Use `ALL` to convert all matching schedules. Required |

To convert all Ease tasks in schedules matching `EASETEST??V`, run:

```
ConvertEaseTasks.exe -opc OPCON  -mn EASE001 -sf EASETEST??V -jf ALL

```

## General conversion process

Before starting the conversion, make a copy of the OpCon database and the schedules to be converted.

To complete the migration, complete the following steps:

1. Edit the `Conversion.config` file and populate the required OpCon connection values.
2. Run `CreateEaseAgent.exe` with the required arguments to create the ACS Ease agent. See the [CreateEaseAgent.exe utility](#createeaseagentexe-utility) section for argument details.
3. Run `ConvertEaseTasks.exe` with the required arguments to convert the Ease tasks. See the [ConvertEaseTasks.exe utility](#converteasetasksexe-utility) section for argument details.

The utility processes each selected schedule and converts matching Ease embedded script jobs. No other OpCon objects such as frequencies, dependencies, or events are modified. For each matching job, the utility:

- Retrieves the Windows job properties.
- Resets the job to a null job.
- Sets the machine definition.
- Sets the ACS Ease task properties.
- Converts the script arguments to an ACS Ease job definition.
- Commits the job changes.
