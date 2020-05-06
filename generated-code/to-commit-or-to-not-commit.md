# To commit or to not commit

- Control the environment with Docker, thereby controlling the version of a tool
used to generate code. 
- Source control the command invocation (including the cli options) by 
scriptifying the build process 

Assuming code generation takes a reasonably short amount of time, it's senseless
to check in the generated sources.

The single source of truth comes from reproducibility through environment control
and a source controlled build system.