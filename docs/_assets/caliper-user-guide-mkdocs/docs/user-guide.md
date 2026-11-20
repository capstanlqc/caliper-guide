# cAliper User Guide

## 1. Introduction

### 1.1. Purpose and audience

This guide explains how to use cAliper, the translation management system (TMS), to prepare and manage translation workflows. It is intended primarily for National Project Managers (NPMs), with additional instructions for tasks that can only be performed by a Program Administrator (PA), also referred to as a superuser (SU).

The guide covers the management of jobs, language assets, users, workflow types, workflows, project information and version history. It also explains the parts of the OmegaT process that an NPM needs to coordinate. It is not an OmegaT user manual: linguists and other language-task users should consult the separate OmegaT guides for instructions on working in the editor.

### 1.2. Roles

cAliper has two administrative roles:

- **Program Administrator (PA / SU):** has program-wide administrative responsibilities. The PA manages workflow types and defines the user roles and scopes available in the system. The PA can view workflows for all locales.
- **National Project Manager (NPM):** manages the translation work for their country or region. The NPM can prepare language assets, add users within the roles and scopes defined by the PA, create and monitor workflows, and perform permitted workflow transitions. The NPM sees only the locales within their country or region.

In this guide, *Program Administrator*, *Administrator* and *Project Coordinator* refer to the PA role. *Project Manager* refers to the NPM role.

### 1.3. Key concepts

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

### 1.4. Overall process

1. The survey platform sends a batch to cAliper. The batch becomes a queued job.
2. The NPM opens the job and creates a workflow for each locale to be processed, selecting a workflow type and confirming the language assets.
3. Users perform the tasks assigned to them. For steps configured for OmegaT, the assigned user authenticates, downloads the project and works in OmegaT.
4. When an OmegaT user finalises their task, cAliper saves the work, commits the target files and normally advances the workflow to the next step.
5. When the workflow reaches its final state, cAliper notifies the survey platform that the target-language batch is ready to be collected.

## 2. Preparing the translation environment

Before creating workflows, the PA and NPM should make sure that the necessary language assets and users are available, and that an appropriate workflow type has been configured. Workflow-type administration is a PA responsibility; language assets can be managed by both the PA and the NPM.

### 2.1. Managing language assets

Language assets include:

- **Translation memories (TMs):** contain validated translations that can be reused during translation.
- **Bilingual glossaries:** contain validated terminology and phraseology.

The asset list shows each asset's file name, type, language, program, tags and available actions. Use **Add asset** to add a resource. Existing assets can be edited or deleted from the list.

![Language asset list](_assets/img/page-08.png)

When creating a workflow, cAliper suggests glossary and TM assets that match the project, language and applicable active tags. Review the suggestions for each locale. You can change the selection or clear it if a suggested asset is not appropriate.

![Selecting language assets when creating a workflow](_assets/img/page-15.png)

**NPM responsibility:** check the suggested assets for every locale before saving its workflow. Do not assume that the same assets are appropriate for every locale in a job.

### 2.2. Managing users

The user list displays the users configured in cAliper, including their username, scope, step and locale restrictions. The scope determines where a user can work; a step or locale restriction can further limit the tasks available to them.

![User list](_assets/img/page-12.png)

The PA defines the roles and scopes that are available in the system. The NPM can add users as needed within that framework, for the NPM's country or region. When adding a user, make sure that the account is associated with the appropriate scope, locale and workflow step.

The exact fields and validation rules in the **Add user** form are not documented in the presentation; follow the labels and validation messages shown in the current cAliper interface.

### 2.3. Managing workflow types (PA)

A workflow type is a template for the sequence of steps that will be used to process a locale. Workflow types can be active or inactive. The PA creates and maintains them; NPMs select an active workflow type when creating a workflow.

The examples shown in the presentation, such as `SINGLE-TRANSLATION` and `TRA-REV-VER-REF`, are examples only. They are not fixed workflow types. The PA should configure workflow types to match the tasks required by the project.

![Workflow type list](_assets/img/page-09.png)

#### 2.3.1. Fixed and configurable steps

Every workflow type includes three system-defined steps, which cannot be removed or moved:

1. **pending** — the initial step.
2. **setup** — the step immediately after `pending`.
3. **closed** — the final step.

The PA can add, remove and reorder the steps between `setup` and `closed`.

For each configurable step, the PA can:

- set its name;
- decide its position in the sequence;
- mark it as **required**;
- indicate whether it is an **OmegaT** step;
- activate or deactivate the workflow type as a whole.

A step marked **required** cannot be skipped manually by the NPM in the TMS. It must be completed in OmegaT, or the PA must move it forward manually in the TMS.

Select the **OmegaT** option for every step that represents a language task to be performed in OmegaT. This may include translation, review, verification, adjudication or another editing task. Steps that are administrative and do not involve an OmegaT task should not be marked as OmegaT steps.

![Workflow steps, including OmegaT and required settings](_assets/img/page-10.png)

#### 2.3.2. Creating and maintaining a workflow type

1. Open the workflow-type management area.
2. Select **Add workflow type** to create a new template, or open the details of an existing type.
3. Define the workflow type's identifying information and status.
4. Configure the steps between the fixed `pending`, `setup` and `closed` steps. Add, remove or reorder the configurable steps as required.
5. For each language-task step, select **OmegaT**. Mark a step **required** when the NPM must not be able to skip it manually.
6. Save the workflow type and ensure that it is active if it should be available for new workflows.

![Adding a workflow type](_assets/img/page-11.png)

The exact field names in the workflow-type creation form may vary with the current interface. The important configuration decisions are the sequence of steps, their OmegaT setting, their required status and whether the workflow type is active.

## 3. Managing jobs

### 3.1. Understanding incoming jobs

When a batch is released by the survey platform, it is sent to cAliper with its target locales and associated information. cAliper registers it as a job with a status indicating that it is available for processing.

The incoming-jobs list provides an overview of the jobs and includes information such as the job ID, external ID, request date, program, batch, number of locales, status and available actions.

![Incoming jobs](_assets/img/page-13.png)

### 3.2. Viewing job details

Open **Details** to inspect a job before creating its workflows. The job details include identifying information such as the program, batch, callback URL and status. The locale list shows each target language and its current state; the files section lists the files included in the batch.

![Job details and queued locales](_assets/img/page-14.png)

Use the job details to confirm that you are working on the intended batch and to see which locales remain queued.

## 4. Creating workflows

### 4.1. Create one workflow per locale

The NPM processes the locales in a job one by one. A separate workflow must be created explicitly for each locale. This allows the NPM to confirm or customise the language assets for that particular project.

You can skip a locale and move to the next queued locale. Skipping a locale in this workflow-creation sequence does not create its workflow; return to it later if it needs to be processed.

To start, select **Create workflows** from the incoming-jobs list, or open the job details and select **Create workflows** there.

![Starting workflow creation from the jobs list](_assets/img/page-13.png)

### 4.2. Configure each locale

For each queued locale:

1. Check the locale currently displayed. Make sure it is the intended target language.
2. Select the appropriate **Workflow type**.
3. Review the suggested **Glossary assets**.
4. Review the suggested **Translation memory assets**.
5. Change or clear the suggested assets if necessary.
6. Select **Save workflow / Next language** to save the workflow for this locale and continue to the next queued locale.
7. Repeat until all locales that should be processed have a workflow.

![Configuring a locale and saving its workflow](_assets/img/page-15.png)

When no queued locales remain, cAliper indicates that there are no queued languages left for the job. The language-progress area shows the state of the locales processed so far.

![Job after processing the queued locales](_assets/img/page-16.png)

**Important:** creating a workflow for one locale does not create workflows for the other locales in the same job. Check the language-progress list to ensure that every locale requiring work has been handled.

## 5. Monitoring workflows

### 5.1. Workflow list and filters

Open **Workflows** to monitor the workflows available within your scope. The list can be filtered by fields such as:

- program;
- batch;
- language/locale;
- workflow type;
- current step.

You can also select how many rows to display before applying the filters. The table shows the workflow ID, program, batch, locale, workflow type, current step and available actions.

The PA can view all locales. The NPM sees only the locales belonging to their country or region.

![Workflow list and filters](_assets/img/page-17.png)

### 5.2. Understanding workflow status and progress

The **Current step** column indicates where each workflow is in its sequence. The step sequence is also displayed in the workflow details, with the current step highlighted.

Open **Details** to inspect an individual workflow. The details view identifies the program, batch, locale, workflow type, current step, version and associated job ID.

![Workflow monitoring list with current steps](_assets/img/page-22.png)

![Workflow details and step sequence](_assets/img/page-23.png)

Use the current-step information to identify workflows that are waiting for a user task, have not yet moved beyond setup, or have reached a later stage. The workflow list is also where you can select workflows for bulk actions.

### 5.3. Bulk actions

The workflow list supports selecting multiple visible rows and applying a bulk transition. The selection applies only to the rows currently visible in the list. The interface also indicates that the **Set step** operation requires the selected workflows to have a uniform workflow type.

Before applying a bulk action, check the selected rows carefully, including their locales, workflow types and current steps. Do not assume that selecting workflows on one page selects matching workflows on other pages or outside the current filtered view.

![Bulk workflow transitions](_assets/img/page-20.png)

## 6. Managing workflow transitions

### 6.1. Automatic transitions after OmegaT tasks

For a step configured as an OmegaT language task, the normal way to complete the step is for the assigned user to finalise the task in OmegaT. cAliper then performs the transition to the next step.

When an OmegaT user finalises a task, cAliper:

1. synchronises/saves the translations remotely and commits the target files;
2. marks the current step as completed and advances the workflow to the next step;
3. revokes the previous user's access rights so that they can no longer modify the translations;
4. grants access rights to the user assigned to the next step, who can then authenticate and download the project.

![OmegaT task finalisation advances the workflow](_assets/img/page-39.png)

The presentation illustrates this sequence for translation, review and verification. The same principle applies to other steps configured as OmegaT language tasks.

### 6.2. Moving a workflow forward manually

The NPM can move a workflow forward manually from the cAliper interface when necessary, provided the current step is not marked **required**.

A required step cannot be skipped manually by the NPM. It can be advanced only when the assigned user finalises the task in OmegaT, or when the PA performs the manual transition in the TMS.

To move a workflow forward from its details page, use **Next step**. The workflow list also provides a **Next step** action for an individual row. For multiple workflows, use the bulk action after checking the selection.

![Next-step action in workflow details](_assets/img/page-18.png)

![Workflow list with individual next-step actions](_assets/img/page-17.png)

Use manual forward transitions only when the work required at the current step has been completed or when the applicable project procedure explicitly allows the step to be bypassed. Do not use the control as a substitute for an OmegaT user's task finalisation when that task is required.

### 6.3. Moving a workflow backwards

A backward transition is intended for correcting an omission or problem from an earlier step. For example, if something that should have been completed during translation was missed and is discovered during review, return the workflow to the earlier step so that the issue can be amended before the next task is performed.

Use **Previous step** only when there is a specific reason to return work to an earlier stage. Identify what needs to be corrected and coordinate with the user responsible for that step. Once the correction is complete, the workflow can proceed through the normal process again.

![Previous-step and next-step controls](_assets/img/page-18.png)

### 6.4. Completion and handback

When the final language-task step is finalised, cAliper saves the translations remotely, commits the target files, completes the final step and closes the workflow. It also revokes the final user's access rights and sends a callback to the survey platform to indicate that a new target-language version of the batch is ready.

The survey platform can then collect the target files. This completion and handback process applies to each locale's workflow; a job containing multiple locales is not fully processed merely because one locale has been completed.

![Final task closes the workflow and triggers the callback](_assets/img/page-46.png)

![Survey-platform callback and retrieval of target files](_assets/img/page-48.png)

## 7. Project details and version control

### 7.1. Project details

From a workflow's details page, use the tabs to inspect the workflow's steps, project and credentials, files, history and (when available) the diff report.

The **Project & credentials** tab displays the project URL and the repository credentials associated with the project. Credentials are listed individually and can be downloaded using the corresponding **Download** control.

![Project URL and downloadable repository credentials](_assets/img/page-21.png)

Treat repository credentials as access credentials. Download or share them only with the intended user and in accordance with the project's access procedures.

### 7.2. Files and history

The workflow details view includes **Files** and **History** tabs. Use these tabs when you need to inspect the files associated with the project or review its recorded history. The presentation identifies these tabs but does not document their full contents or all available actions; consult the current interface for the information displayed there.

### 7.3. Version number and diff reports

A workflow's details include a version number. When a diff report is available, the **Diff** tab provides a link to the report comparing translation versions at different workflow stages (the presentation shows a translation-versus-review comparison).

The example diff report presents the filename and segment identifier alongside the source text, original translation and edited translation. This allows the NPM to inspect what changed between the compared versions without opening the translation project in OmegaT.

![Diff report link in workflow details](_assets/img/page-40.png)

![Example diff report](_assets/img/page-41.png)

## 8. OmegaT: information for NPMs

This section covers only the OmegaT actions that affect workflow coordination. It does not explain how to translate, review or edit content. Users performing language tasks should refer to the separate OmegaT guides for those instructions.

### 8.1. User authentication and project access

When a workflow reaches an OmegaT step, cAliper grants access to the user assigned to that step. The user must import or manage the credentials provided for the project in OmegaT before accessing the repository. The presentation shows the **Manage Credentials** command in OmegaT.

![OmegaT Manage Credentials command](_assets/img/page-24.png)

The user then downloads the team project using **Project > Download Team Project**. After the project has been downloaded, the user performs the assigned task using the relevant OmegaT guide.

![OmegaT Download Team Project command](_assets/img/page-25.png)

When a previous step is finalised, cAliper revokes the previous user's access and grants access to the next assigned user. If a user cannot authenticate or download the project, check that the workflow is at the expected step and that the user's account is assigned to that step.

### 8.2. Finalising a task

When the language task is complete, the OmegaT user selects **Project > Workflow > Finalize Task**. The user can enter a comment in the finalisation dialog and then confirm by selecting **Finalize**.

![OmegaT Finalize Task command](_assets/img/page-34.png)

![Finalisation dialog and comment field](_assets/img/page-35.png)

OmegaT displays a confirmation when the task has been finalised successfully.

![OmegaT task-finalised confirmation](_assets/img/page-36.png)

The successful finalisation triggers the cAliper transition described in [Automatic transitions after OmegaT tasks](#61-automatic-transitions-after-omegat-tasks). The NPM should verify that the workflow has advanced to the expected next step and that the next user can access the project.

## 9. Operational checks for NPMs

Before creating workflows:

- Confirm that the correct job and batch have arrived.
- Check which locales need to be processed.
- Confirm that the necessary language assets are available.
- Check that the users needed for the workflow exist and have the appropriate scope, locale and step assignments.
- Confirm with the PA that an appropriate active workflow type is available.

When creating each workflow:

- Confirm the locale displayed on the creation page.
- Select the appropriate workflow type.
- Review and, where necessary, customise the suggested glossary and TM assets.
- Save the workflow before moving to the next locale.
- Check the language-progress list to ensure that all required locales have been handled.

When monitoring and transitioning workflows:

- Check the current step before taking action.
- Allow OmegaT users to finalise their own language-task steps whenever possible.
- Do not manually skip a required step as an NPM.
- Use backward transitions only to return work for a specific correction or omission.
- Before using bulk actions, verify the visible selection and ensure the selected workflows meet the operation's requirements.
- After a task is finalised, verify that the workflow advanced and that the next assigned user has access.
- After the final step, verify that the workflow is closed.
