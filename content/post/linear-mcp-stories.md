
+++
categories= ["AI"]
tags= ["Claude", "AI", "Linear", "MCP"]
title= "Using Claude and Linear to manage stories and tasks"
date = "2025-03-03"
draft= true
+++

# Introduction

I recently discovered that Claude is an excellent solution for creating user stories and breaking those stories down into smaller tasks. One of the big advantages of using Claude to do this is because it is looking at your code it can determine specific tasks to perform to complete the story. This process greatly reduces sprint overhead as long backlog grooming sessions are greatly reduced.

In order to get this to work you will need to use Claude (I prefer Claude code) and an MCP server connected to your ticketing system (I will demonstrate using Linear).  This same technique should work with any of the other ticketing systems as well (such as jira, github, etc...).  If you would like intructions on installing the Linear MCP server instructions can be found [[here]]

