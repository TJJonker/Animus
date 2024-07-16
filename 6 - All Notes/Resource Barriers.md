2024-07-16 | 20:52  
**Status:** #alpha
**Tags:** [[DirectX12]]

Resource barriers are a structure that allow a program to track which data is currently accessed/used and synchronize state, allowing for multi-threading safe functionality and reduced CPU usage. Most often, resource barriers are created in the [[Command List]]. 

There are a couple of barriers:
- **Transition barrier -** This barrier describes the state of a (sub)resource when it's transitioning between two states. I.e. transitioning from a copy destination to a vertex and constant buffer. (This state will change after the copy command is finished).

## Format


## Example


## References

https://learn.microsoft.com/en-us/windows/win32/direct3d12/using-resource-barriers-to-synchronize-resource-states-in-direct3d-12