

### What is cAliper?
   
cAliper is cApStAn’s translation management system. cAliper has been designed to manage translation workflows in the context of large multilingual assessments and questionnaires, from the initial reception of the source materials up to the delivery of translated materials to the client. It exposes an API specifically conceived for integration with survey platforms for the purpose of file exchanges (batch releases and deliveries. It can also be used independently.

### Purpose and audience

This guide explains how to use cAliper, [cApStAn](https://www.capstan.be)'s translation management system (TMS), to prepare and manage translation workflows. It is intended primarily for National Project Managers (NPMs), with additional instructions for tasks that can only be performed by a Program Administrator (PA), also referred to as a superuser (SU).

The guide covers the management of jobs, language assets, users, workflow types, workflows, project information and version history. It also explains the parts of the OmegaT process that an NPM needs to coordinate. It is not an OmegaT user manual: linguists and other language-task users should consult the separate OmegaT guides for instructions on working in the editor.

### End users

cAliper has two main administrative users:

- **Program Administrator (PA / SU):** has program-wide administrative responsibilities. The PA manages workflow types and defines the user roles and scopes available in the system. The PA can view workflows for all locales and may perform any of the actions that NPM can do.
- **National Project Manager (NPM):** manages the translation work for their country or region. The NPM can prepare language assets, add users within the roles and scopes defined by the PA, create and monitor workflows, and perform permitted workflow transitions. The NPM sees only the locales within their country or region.

In this guide, *Program Administrator*, *Administrator* and *Project Coordinator* refer to the PA role. *Project Manager* refers to the NPM role.

### Key concepts

| Term | Meaning |
| --- | --- |
| **Job** | A batch received by cAliper (e.g. submitted by a survey platform or a user) and made available for workflow creation. |
| **Batch** | A set of files that belong together and are processed as a whole. |
| **Locale** | A specific language variant, such as French (Belgium), i.e. `fr-BE`. |
| **Workflow** | The sequence of steps used to process one locale of a job/batch. Each workflow corresponds to a locale+combination. |
| **Workflow type** | A reusable template that defines the steps in a workflow and other properties. |
| **Project** | The translation project hosted in the version-control server and made available to users for their assigned language task. |
| **Language asset** | A resource used to support language tasks, such as a translation memory (TM) or bilingual glossary. |
| **OmegaT** | The CAT tool used for language tasks configured as OmegaT steps. |



### Overall process

1. The survey platform submits a batch to cAliper, as well as the list of expected locales. The batch becomes a queued job.
2. The NPM opens the job and creates a workflow for that batch and for each requested locale, selecting a workflow type and confirming the language assets.
3. Users perform the tasks assigned to them. For steps configured for OmegaT, the assigned user authenticates, downloads the project and works in OmegaT.
4. When an OmegaT user finalises their task, cAliper saves the work, commits the target files and advances the workflow to the next step.
5. When the workflow reaches its final step, cAliper notifies the survey platform that the target-language batch is ready to be collected.


[Next: Preparation :material-arrow-right:](01_preparation.md){ .md-button .md-button-right}