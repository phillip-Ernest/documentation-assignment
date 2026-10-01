# Exercise A: User Manual Procedure

## Setting Up a GitHub Repository and Making a First Commit

### Prerequisites

Before starting, the reader needs:

1. A computer connected to the internet.
2. A GitHub account.
3. Git installed on the computer.
4. A web browser such as Google Chrome or Microsoft Edge.
5. Basic knowledge of using a computer terminal.
6. A project folder containing at least one file.

### Procedure

#### Step 1: Open GitHub

**Action:** Open a web browser and visit GitHub.

**Expected result:** The GitHub website opens.

#### Step 2: Sign in to GitHub

**Action:** Sign in to your GitHub account.

**Expected result:** Your GitHub account dashboard appears.

#### Step 3: Open the new repository page

**Action:** Click the **New repository** option.

**Expected result:** The repository creation page appears.

#### Step 4: Enter the repository name

**Action:** Enter `my-first-project` as the repository name.

**Expected result:** The repository name appears in the repository name field.

#### Step 5: Select the repository visibility

**Action:** Select **Public** as the repository visibility.

**Expected result:** The repository is configured as a public repository.

#### Step 6: Create the repository

**Action:** Click **Create repository**.

**Expected result:** The new repository page appears.

#### Step 7: Open Git Bash

**Action:** Open Git Bash on the computer.

**Expected result:** A Git Bash terminal window appears.

#### Step 8: Navigate to the project folder

**Action:** Use the `cd` command to enter the project folder.

**Expected result:** The terminal prompt shows that the project folder is the current directory.

#### Step 9: Initialize Git

**Action:** Run `git init`.

**Expected result:** Git initializes the project folder as a local Git repository.

#### Step 10: Stage the project files

**Action:** Run `git add .`.

**Expected result:** The project files are added to Git's staging area.

#### Step 11: Create the first commit

**Action:** Run `git commit -m "Initial commit"`.

**Expected result:** Git creates the first commit containing the staged files.

#### Step 12: Connect the local repository to GitHub

**Action:** Run `git remote add origin <repository-url>` using the URL of the GitHub repository.

**Expected result:** The local repository is connected to the GitHub repository.

#### Step 13: Rename the branch

**Action:** Run `git branch -M main`.

**Expected result:** The current branch is named `main`.

#### Step 14: Push the project

**Action:** Run `git push -u origin main`.

**Expected result:** The project files are uploaded to GitHub.

#### Step 15: Verify the repository

**Action:** Refresh the GitHub repository page.

**Expected result:** The project files and the `Initial commit` message appear in the repository.

### Screenshot Description

A suitable screenshot should show the GitHub repository page after the first push. It should clearly display the repository name, the `main` branch, the uploaded project files, and the latest commit message, such as **Initial commit**.

### Troubleshooting

**Common error:** `src refspec main does not match any`

This error usually occurs when the local repository does not contain a commit.

To solve the problem, stage the files and create a commit by running:


git add .
git commit -m "Initial commit"


Then rename the branch and push it using:


git branch -M main
git push -u origin main

# Exercise B: API Reference Entry

## Create a New Task

### Endpoint

**HTTP Method:** `POST`

**Endpoint Path:**

`/projects/{projectId}/tasks`

### Description

This endpoint allows an authenticated user to create a new task inside a specified project in a project management application.

The task must have a title, an assignee, a due date, and a priority level. The description is optional.

## Path Parameters

| Parameter   | Data Type | Required | Description                                                      |
| ----------- | --------- | -------- | ---------------------------------------------------------------- |
| `projectId` | String    | Yes      | The unique ID of the project where the new task will be created. |

## Query Parameters

This endpoint does not require any query parameters.

## Request Body Parameters

| Parameter     | Data Type | Required | Description                                                                     |
| ------------- | --------- | -------- | ------------------------------------------------------------------------------- |
| `title`       | String    | Yes      | The name or title of the task.                                                  |
| `description` | String    | No       | Additional information about the task.                                          |
| `assigneeId`  | String    | Yes      | The unique ID of the user assigned to the task.                                 |
| `dueDate`     | String    | Yes      | The date by which the task should be completed, using the `YYYY-MM-DD` format.  |
| `priority`    | String    | Yes      | The priority level of the task. Accepted values are `low`, `medium`, or `high`. |

## Required Request Headers

| Header          | Required | Description                                                                |
| --------------- | -------- | -------------------------------------------------------------------------- |
| `Authorization` | Yes      | Contains the authentication token used to identify and authorize the user. |
| `Content-Type`  | Yes      | Specifies that the request body is formatted as JSON.                      |

### Authentication

The authentication token is provided using the Bearer authentication scheme:

`Authorization: Bearer <access_token>`

## Example Request

### HTTP Request


POST /projects/proj-1001/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
Content-Type: application/json


### JSON Request Body

```json
{
  "title": "Prepare project presentation",
  "description": "Create the slides and prepare the final presentation for the project meeting.",
  "assigneeId": "user-2045",
  "dueDate": "2026-10-15",
  "priority": "high"
}
```

## HTTP Response Codes

### 201 Created

The task was successfully created.

### 400 Bad Request

The request contains invalid or missing information, such as a missing required field or an invalid priority value.

### 401 Unauthorized

The request does not contain valid authentication credentials.

### 403 Forbidden

The authenticated user does not have permission to create tasks in the specified project.

### 404 Not Found

The specified project or assignee does not exist.

### 409 Conflict

The request conflicts with an existing resource or project rule.

### 422 Unprocessable Entity

The request contains valid JSON, but one or more values fail the application's validation rules.

### 500 Internal Server Error

An unexpected error occurred on the server while processing the request.

## Successful Response

**HTTP Status:** `201 Created`

### Example Response Body

```json
{
  "id": "task-78342",
  "projectId": "proj-1001",
  "title": "Prepare project presentation",
  "description": "Create the slides and prepare the final presentation for the project meeting.",
  "assigneeId": "user-2045",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "pending",
  "createdAt": "2026-10-01T09:15:00Z",
  "updatedAt": "2026-10-01T09:15:00Z"
}


## Response Field Descriptions

| Field         | Data Type | Description                                                           |
| ------------- | --------- | --------------------------------------------------------------------- |
| `id`          | String    | Unique identifier assigned to the newly created task.                 |
| `projectId`   | String    | Identifier of the project containing the task.                        |
| `title`       | String    | Title of the task.                                                    |
| `description` | String    | Optional additional information about the task.                       |
| `assigneeId`  | String    | Identifier of the user assigned to the task.                          |
| `dueDate`     | String    | Date by which the task should be completed.                           |
| `priority`    | String    | Task priority: `low`, `medium`, or `high`.                            |
| `status`      | String    | Current status of the task. A newly created task starts as `pending`. |
| `createdAt`   | String    | Date and time when the task was created.                              |
| `updatedAt`   | String    | Date and time when the task was last updated.                         |


