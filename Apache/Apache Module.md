# Apache Modules:
 Core Modules:
## New functions are in the form of modules
-Every modules has their own directives(syntaxes)
-Easy to download, install and configure
-Define modules, use their syntaxes to use that functions and its ready to use.

## Core/mpm_common -Application Processs handling configuration parameters
->Process handling and worker thread management:
 Event Prefork Worker Mpm_winnt Mpmt_os2 Mpm_netware
   |      |      |       |        |         |
    >>>>> |  <<<<<      Windows  OSx2      Netware
        Linux/Unix

->Modules and their derivatives:
     Modules - Directives
 |        |      |       |            |       |
Command  Status Default  Description  Syntax  Context
          |      value
          |
  core   MPM  Base Extension Experimental 

->context: server config, Virtual Host, Directory, .htaccess

## Application Process Handling Configuration Parameters:
Process Handling and Worker Thread Management: This section refers to how Apache handles processes and workers for managing incoming requests. Apache uses Multi-Processing Modules (MPMs) to determine how requests are handled (in terms of threads, processes, and worker distribution).
MPM Variants:
1. Prefork MPM (Multi-Processing Module)
How it works: It handles each request using a separate process. It creates several child processes to handle incoming requests.
Characteristics:
No threading: Each process handles only one request at a time.
Memory usage: Because each child process is independent, it uses more memory.
Stability: Very stable, as each request is handled by a separate process, so one crashing doesn’t affect others.
Use case: Best for compatibility with non-thread-safe modules (like older PHP versions or certain types of applications).
2. Worker MPM
How it works: It uses a combination of multiple processes and multiple threads per process to handle incoming requests. Each worker process can handle several threads at once.
Characteristics:
Threaded handling: Each process has multiple threads, and each thread can handle a request.
More efficient: Threads consume less memory than processes, which makes it more scalable than the prefork model.
Performance: Typically performs better than prefork in high-traffic scenarios.
Use case: Suitable for modern web applications where threading is supported and threads are safe.
3. Event MPM
How it works: A variation of the worker MPM designed to improve performance by handling keep-alive connections more efficiently.
Characteristics:
Event-driven: It can handle more requests with fewer resources, especially in scenarios where many clients are maintaining persistent connections.
Better at handling long-lived connections: It optimizes the management of HTTP keep-alive connections by using a dedicated thread for handling the connection and passing requests to worker threads only when needed.
Performance: Often the most efficient choice, especially for highly concurrent workloads.
Use case: Ideal for serving content with many persistent connections, such as live chat or WebSocket 
services.MPM_winnt: A version of the worker MPM designed for Windows operating systems. It uses threads but in a way that is compatible with Windows’ threading model.
MPM_OS2: A MPM designed for the OS/2 operating system (an older operating system, rarely used today).
MPM_netware: Used for the Netware operating system (another older system, no longer widely used).
Linux/Unix: Both the Worker and Prefork MPMs are supported on Unix-based systems like Linux and BSD.
2. Modules and Their Derivatives:
Modules: Apache HTTP Server modules are dynamically loaded, each of which extends Apache's functionality (e.g., authentication, URL rewriting, SSL, etc.).
Directives: Configuration parameters used within Apache's configuration files (httpd.conf, for example). These directives control how modules function.
Common Directives include:
Command: The directive itself.
Status: Describes whether the directive is enabled or not.
Default Value: The default setting for the directive if not explicitly configured.
Description: A brief explanation of what the directive does.
Syntax: The expected format for the directive in configuration files.
Context: Defines where the directive can be used (e.g., within server config, Virtual Host, Directory, or .htaccess files).
3. Context:
Server Config: Global settings applied to the entire server.
Virtual Host: Settings that are specific to a particular domain or subdomain. For example, you may have different configurations for www.example.com and api.example.com.
Directory: Configuration settings applied to a particular directory on the server.
.htaccess: A configuration file that allows directory-level settings to be customized without modifying the main server configuration file (usually used for security, redirects, and URL rewriting).
4. Core MPM - Base Extension Experimental:
Core: The essential modules that Apache uses by default, such as the core Apache module itself.
MPM Base: The foundational MPM module, defining how Apache should handle connections, processes, and threads.
Extension: Modules that extend the core functionality, but might not be required for basic operation.
Experimental: Modules or MPMs that are not yet fully tested or stabilized, often included for testing purposes.
__________________ _______________
Example:   Mod_Log_config module
Command   :LogFormat
Synatx    :LogFormat format | nickname
Default Value :LogFormat "%h %l %u %t\"%r\"%>s%b"
Description :Describe a format for use in a log file
Status    :Base
Context   :server config, virtual host

```apache
%h: Client's IP address.
%l: The "remote logname" of the client (if available). It's usually a hyphen (-) unless identd is configured and accessible.
%u: The authenticated user (if any). If there's no authenticated user, it will display a hyphen (-).
%t: The time the request was received, in the format [day/month/year:hour:minute:second zone]. For example, [10/Feb/2025:14:30:00 +0000].
\"%r\": The request line from the client, including the HTTP method, the requested resource (URL), and the protocol version (e.g., "GET /index.html HTTP/1.1"). The quotes are escaped to ensure they appear literally in the log.
%>s: The HTTP status code sent to the client (e.g., 200, 404, etc.).
%b: The size of the response body sent to the client, in bytes. If no body is sent, it will be -.
_________________________ _____________________________
## Directives of core /Common :
CoreDumpDirectory :Directory where Apache HTTP Server attempts to switch before dumping core
EnableException: Enables a hook that runs exception handlers after a crash
GracefulShutdownTimeout: Specify a timeout after which a gracefully shutdown server will exit
Listen :IP address and ports that the server listen to
Listenbacklog: maximum length of the queue of pending connections.
ListenCoresBucketsRatio: ratio btw the number of cpu cores and the number of listeners buckets
MaxConnectionsPerChild: Limit on the number of connections that an individual child server will handle during its life.
MaxMemfree: maximum amount of memory that the main allocator is allowed to hold without calling free
MaxRequestWorker: Maximum no. of connections that will be processed simultaneously
MaxSpareThreads: maximum number of idle threads available to handle request spikes
MinSpareThreads: Minimum no. of idle threads available to handle the request spikes
PidFile :File where the server records the process id of the daemon
ReceiveBuffersize: Tcp receive buffer size
ScoreBoardFile: Location of the file used to store coordination data for the child processes
SendBufferSize: TCP Buffer size
ServerLimit: Upper Limit on configuration number of processes
StartServer: Number of child server process created at startup
StartThreads: Number of threads created on startup
ThreadLimit: Sets the upper limit on the configurable number of threads per child process
ThreadsPerChild: Number of threads created by each child process
ThreadStackSize: The size in bytes of the stack used by threads handling client connections
 _________________________________ __________________________
Apache HTTPD -Module Journey:
-New functions are in the form of modules
-Every modules has their own directives/syntax
-Easy to Install/download
->Core modules:
  core, mpm_common, event, mpm_netware, mpmt os2, prefork, mpm winnet, worker
_______________________________ ____________________________
# There are about 125 modules in Apache which have their own unique set of fuctions:
-Mod_alias: Directives:
    Alias, AliasMatch, Redirect, Redirectmatch, RedirectPermanent, Redirecttemp, ScriptAlias
 ScriptAliasMatch: Maps a url to a filesystem location using a regular expression 
 Syntax : ScriptAliasMatch regex file-path | directory-path
 context: server_config, virtual host
 status : base
 Module : mod_alias

-Mod_auth_file: AuthuserFile: 
 Description: Sets the name of a text file containing the list of users and password for authentication
 syntax: AuthUserFile fle-path
 context: directory, .htaccess 
-Mod_dir:Directives:DirectoryCheckerHandler, DirectoryIndex, DirectoryIndexRedirect, Directoryslash, 
Fallbackresource:Define a default URL for request that dont map to a file.
 Sytntax: fallbackresource disabled | local-url
 Deafult: disabled-http will return 404

The AuthUserFile directive is part of mod_auth_file, which handles basic authentication using a flat file (a plain text file containing username and password pairs). Here's the breakdown:

Description: This directive defines the location of a file that contains user credentials for authentication. This is typically a .htpasswd file.
Syntax: AuthUserFile file-path
file-path: Path to the password file on the server. This file contains username-password pairs, which are used for HTTP authentication.
Context: It can be used in Directory or .htaccess contexts. For example:
In .htaccess: You can specify authentication for a specific directory or site.
In Directory: You can specify authentication for a directory in the server configuration.
Example:

AuthUserFile /path/to/.htpasswd

This would specify the location of the .htpasswd file where Apache will look for usernames and their corresponding passwords.

mod_dir: Directives
The mod_dir module is responsible for handling requests for directories. Some of the directives related to it are:

DirectoryIndex: This directive sets the default file that Apache will serve when a directory is requested. For example, if you go to https://example.com/ and there is no specific file requested, Apache might serve index.html or index.php by default.

Syntax: DirectoryIndex index.html index.htm index.php
In this example, Apache will look for index.html, then index.htm, then index.php in the directory.
Context: It can be used in Directory, VirtualHost, or .htaccess contexts.
DirectoryIndexRedirect: This is a directive used to set up a redirection for the directory index. It’s less commonly used but can be helpful in certain use cases.

DirectorySlash: This directive controls whether or not a trailing slash is appended to the directory URL when a directory is accessed.

Syntax: DirectorySlash On | Off
On: Appends a slash to the URL if a directory is requested without one.
Off: Prevents appending a slash.
Example:

DirectoryIndex index.html index.php

This will tell Apache to serve index.html (if it exists) when a directory is accessed. If not, it will serve index.php.

FallbackResource
The FallbackResource directive is part of the mod_dir module and defines a default resource to serve when the requested URL doesn’t map to a file or directory. This can be useful for applications like single-page apps (SPAs) where all routes need to point to an index.html file.

Description: This directive allows you to define a URL to be served when a requested resource doesn't exist. Instead of returning a 404 error, Apache will serve the fallback resource.

Syntax: FallbackResource disabled | local-url

disabled: Disables the fallback resource, and Apache will return a 404 error if no file is found.
local-url: A URL or file path to be served as the fallback. Typically, this would be a resource like index.html for SPAs.
Default: By default, FallbackResource is set to disabled, meaning requests to non-existent files return a 404 error.

Example:

FallbackResource /index.html

This would serve index.html as the fallback resource when a request doesn't map to an actual file.
