

### What is cAliper?
   
cAliper is cApStAn’s translation management system. cAliper has been designed to be used for managing translation workflows in thte context of large multilingual assessments and questionnaires, from the initial reception of the source materials up to the delivery of translated materials to the client. It exposes an API specifically conceived for integration with survey platforms for the purpose of file exchanges (batch releases and deliveries), although it can also be used independently.

### Purpose and audience

This guide explains how to use cAliper, the translation management system (TMS), to prepare and manage translation workflows. It is intended primarily for National Project Managers (NPMs), with additional instructions for tasks that can only be performed by a Program Administrator (PA), also referred to as a superuser (SU).

The guide covers the management of jobs, language assets, users, workflow types, workflows, project information and version history. It also explains the parts of the OmegaT process that an NPM needs to coordinate. It is not an OmegaT user manual: linguists and other language-task users should consult the separate OmegaT guides for instructions on working in the editor.

### End users

cAliper has two main administrative users:

- **Program Administrator (PA / SU):** has program-wide administrative responsibilities. The PA manages workflow types and defines the user roles and scopes available in the system. The PA can view workflows for all locales.
- **National Project Manager (NPM):** manages the translation work for their country or region. The NPM can prepare language assets, add users within the roles and scopes defined by the PA, create and monitor workflows, and perform permitted workflow transitions. The NPM sees only the locales within their country or region.

In this guide, *Program Administrator*, *Administrator* and *Project Coordinator* refer to the PA role. *Project Manager* refers to the NPM role.

### Key concepts

| Term | Meaning |
| --- | --- |
| **Job** | A batch received by cAliper from the survey platform and made available for workflow creation. |
| **Batch** | A set of files that belong together and are processed as a unit. |
| **Locale** | A specific language variant, such as French (Belgium), `fr-BE`. |
| **Workflow** | The sequence of steps used to process one locale of a job. Each workflow belongs to one locale. |
| **Workflow type** | A reusable template that defines the steps in a workflow. |
| **Project** | The translation project hosted in the version-control server and made available to users for their assigned language task. |
| **Language asset** | A resource used to support language tasks, such as a translation memory (TM) or bilingual glossary. |
| **OmegaT** | The CAT tool used for language tasks configured as OmegaT steps. |

A job may contain several target locales. cAliper does not create one workflow for all of them automatically: the NPM creates each locale's workflow separately.

### Overall process

1. The survey platform sends a batch to cAliper. The batch becomes a queued job.
2. The NPM opens the job and creates a workflow for each locale to be processed, selecting a workflow type and confirming the language assets.
3. Users perform the tasks assigned to them. For steps configured for OmegaT, the assigned user authenticates, downloads the project and works in OmegaT.
4. When an OmegaT user finalises their task, cAliper saves the work, commits the target files and normally advances the workflow to the next step.
5. When the workflow reaches its final state, cAliper notifies the survey platform that the target-language batch is ready to be collected.