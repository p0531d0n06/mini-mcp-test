# Introduction to MCP

## What is an MCP?

An MCP is a communication protocol that allows services like Claude to interact with API calls, providing schemas and functions without having to manually scope out each functional call to the API. Anyone can make an MCP, but certain API service providers may release their own official MCP protocols.

### The MCP Client

The **MCP Client** provides communication between a user's server and an MCP Server.

An MCP Client is **Transport Agnostic**, which means that communication between **Client** and **Server** can be done over many different protocols.

### The MCP Communication

The MCP specification defines the portfolio of message types that can be transferred.

### The Overall Flow

1. User sends request to their server eg. to check for available repositories
2. The server sends the tool requests to the MCP Client, which sends a ListToolsRequest to the MCP Server, and sends a response back to the MCP Client via a ListToolsResult
3. The MCP Client gives the list of available tools to the user's server
4. Now that the tools are defined with the query, both can be shipped off to Claude
5. Claude processes the request and now can use the tools, as defined by the MCP and serves a tool use on the user's server
6. Now the server with the functionality created can call the MCP Client to run the tool which sends a CallToolRequest to the MCP Server and can now process the execution and successfully sends the request to Github (following the example from 1.)
7. The response from Github is brought back to the the MCP Server which then brings it back to the MCP Client via a CallToolResult
8. The user server then sends the toolResult to Claude to transform and Claude responds to the user server and concludes with a neat response to the user

## Resources

- Resources allow the MCP Server to expose data to the client
- Kind of similar to an HTTP Server GET request handler
- Can return any type of data
    - We set the 'mim_type' to give the client a hint to the return data type
- Two types: **Direct** & **Templated** 