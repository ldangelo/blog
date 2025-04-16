
+++
categories= ["AI"]
tags= ["Claude", "AI", "Linear", "MCP"]
title= "Using Claude and Linear to manage stories and tasks"
date = "2025-03-03"
draft= false
+++

# Introduction

I recently discovered that Claude is an excellent solution for creating user stories and breaking those stories down into smaller tasks. One of the big advantages of using Claude to do this is because it is looking at your code it can determine specific tasks to perform to complete the story. This process greatly reduces sprint overhead as long backlog grooming sessions are greatly reduced.

In order to get this to work you will need to use Claude (I prefer Claude code) and an MCP server connected to your ticketing system (I will demonstrate using Linear).  This same technique should work with any of the other ticketing systems as well (such as jira, github, etc...).  If you would like instructions on installing the Linear MCP server instructions can be found [Linear MCP Setup](/post/linear-mcp-setup/)

# Using the Linear MCP Server

## List your projects

```
List my linear projects
```
### Output from Claude Code

```
⏺ Your Linear projects:
  1. fx-expert (ID: 38ee8702-8c34-4ddf-ac1a-fd6553c5b088)
  2. fx-agents (ID: 27052d98-be4a-4789-943d-8194cb4b8ea9)
```

## List your tasks

```
List my tasks for the project 'fx-expert'
```

### Output from Claude Code

```
⏺ Tasks for fx-expert project:

  In Progress:
  - FOR-16: Update User Profile Information
  - FOR-15: Add Rate information too videoconference

  Backlog:
  - FOR-34: Improve type safety with proper null checks
  - FOR-33: Standardize exception handling across controllers
  - FOR-32: Increase test coverage for core functionality
  - FOR-30: Enhance authentication with proper role-based access
  - FOR-29: Complete partner selection and booking flow
  - FOR-28: Complete Stripe payment processing implementation
  - FOR-27: Complete AI matching engine implementation
  - FOR-26: Remove hardcoded Stripe API key from PaymentService
  - FOR-25: Add navigation and routing for meetings page
  - FOR-24: Integrate meeting data with UI component
  - FOR-23: Implement API endpoint for upcoming meetings
  - [20+ more tasks...]

  Done:
  - FOR-10: Generate unique url for partners to add to e-mail and linkedin
```

## Create a story

Here we are going to add a story and related sub-tasks to protect all API endpoints using JWT tokens.

```
Create a story and sub-tasks to add JWT tokens to all API endpoints.
```
### Output from Claude Code

```
⏺ Created JWT authentication story with subtasks:

  Main story: FOR-35 - Add JWT token authentication to all API endpoints

  Subtasks:
  1. FOR-36 - Configure JWT middleware in EventServer
  2. FOR-37 - Add [Authorize] attributes to all controllers
  3. FOR-38 - Update Blazor client to pass JWT tokens with requests
  4. FOR-39 - Create integration tests for JWT authentication

  All tasks are assigned to you in the Backlog with priority 2.

```

# Conclusion

Because Claude is sitting on the code it can easily create a list of tasks that need to be performed inorder to complete the story.  The advantage to this approach over a more traditional approach is that the story 'refinement' process of an agile methodology is greatly reduced.  All that's really left to do is to size the issues and assign them to a sprint.  
