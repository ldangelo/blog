
+++
categories= ["AI"]
tags= ["Claude", "AI", "Linear", "MCP"]
title = "Setting up Claude and Linear MCP"
date = "2025-03-01"
draft= false
slug="linear-mcp-setup"
+++


# Overview

I recently installed the linear MCP server in Claude Code and it's a game changer. Installing it wasn't difficult, however, finding the correct server was. The one I eventually settled on is: <http://github.com/cosmix/linar-mcp.git>

Below are the steps to install the server.

##  Clone the github repository:


```shell
mkdir ~/mcp
cd ~/mcp
git clone http://github.com/cosmix/linear-mcp.git
```

##  Setup your linear api key

I set my linear api key in my .zshrc. To do so:

```shell
export LINEAR_API_KEY=your_linear_key
```

##  Install the mcp server


```shell
claude mcp add node ~/mcp/lear/build/index.js -e LINEAR_API_KEY=$LINEAR_API_KEY
```

## Test the integration

```shell
claude

list my tasks from linear for project fx-expert

```



