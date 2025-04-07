+++
title = "Musings of a veteran CTO"
author = ["Leo D'Angelo"]
draft = false
+++

-**- org-hugo-base-dir: "~/Documents/blog"; -**-

\#end:


## AI {#ai}


### Setting up linear MCP server with Claude Code {#setting-up-linear-mcp-server-with-claude-code}

I recently installed the linear MCP server in Claude Code and it's a game changer.  Installing it wasn't difficult, however, finding the correct server was.  The one I eventually settled on is: <http://github.com/cosmix/linar-mcp.git>

Below are the steps to install the server.

1.  Clone the repo:

<!--listend-->

```shell
mkdir ~/mcp
cd ~/mcp
git clone http://github.com/cosmix/linear-mcp.git
```

1.  Setup your linear api key

I set my linear api key in my .zshrc.  To do so:

```shell
export LINEAR_API_KEY=your_linear_key
```

1.  Install the mcp server

<!--listend-->

```shell
claude mcp add node ~/mcp/lear/build/index.js -e LINEAR_API_KEY=$LINEAR_API_KEY
```


### Using Claude and Linear to manage stories and tasks {#using-claude-and-linear-to-manage-stories-and-tasks}

I recently discovered that Claude is an excellent solution for creating user stories and breaking those stories down into smaller tasks.  One of the big advantages of using Claude to do this is because it is looking at your code it can determine specific tasks to perform to complete the story.  This process greatly reduces sprint overhead as long backlog grooming sessions are greatly reduced.

In order to get this to work you will need to use Claude (I prefer Claude code) and an MCP server connected to your ticketing system (I will demonstrate using Linear).
