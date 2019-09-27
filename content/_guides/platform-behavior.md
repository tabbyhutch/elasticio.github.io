---
title: Platform Behavior
layout: article
section: Building integration flows
order: 1
since: 20190924
---

This document provides information on the peculiarities of the Platform behavior, including [Flow suspension and stopping](#flow-suspended-vs-stopped), different [Platform limits](#default-limits) and common errors.

## Flow Suspended vs. Stopped
If a Flow gets `5` errors in `5` minutes, it is going to be suspended. Suspension is more of a pause, than a stop. All non-processed messages in a suspended Flow are saved in RabbitMQ queue for 14 days. Then they get dropped if the user did not fix the issues and did not resume the Flow. In [limited workspaces](/getting-started/contracts-and-workspaces.html), Flows are stopped instead of being suspended. A stopped Flow doesn't save any non-processed messages - everything is dropped. You can stop a Flow manually by pressing the *Stop* button.   

## Default Limits
The table below contains configurable Platform limits and their default values:

| **Limit**      | **Default value** | **Description**                                                                  |
|--------------------|--------------|----------------------------------------------------------------------------------|
| Sample retrieval timeout                 | `1 minute `        | If debug sample is not received within this time limit, it will be terminated. |
| Message quantity in RabitMQ queue               | `75000`         |  Component gets suspended if RabbitMQ queue stacks more than the set number of messages.                                                      |
| RabitMQ queue size limit | `200 MB`         | Component gets suspended if RabbitMQ queue exceeds the set size.                            |

## Common Errors
In general, the Platform is not error-prone, but there are a few issues you may encounter. The most common are:

- [Component failed to start](#component-failed-to-start)

- [Component run out of memory and terminated](#component-run-out-of-memory)

- [Syntax errors, human factor](#syntax-errors)

### Component Failed to Start
The error text here prompts you to check Component logs for details and see what caused the error. You can see how it is done [here](managing-flow-errors).   

### Component Run Out of Memory
This error appears if the Component exceeds the set memory limit, which is `256 MB` by default:

![](/assets/img/integrator-guide/behavior/Screenshot_1.png)

You can check Component logs the same way as shown [here](managing-flow-errors), to see the exit code for details:

![](/assets/img/integrator-guide/behavior/Screenshot_2.png)  

### Syntax Errors
This is not a Platform error per se, but it happens quite a lot. Just be sure to enter all the data correctly, and your Flows won't suffer from this issue. Most likely, you will still see the problem in Component logs and be able to fix it. Otherwise, escalate the issue to the platform vendor via support. You can find info on applying for support [here](general-troubleshooting-guide).