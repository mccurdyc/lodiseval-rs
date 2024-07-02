# Design

## Project Goals

1. Understand when consistency in a system fails
1. Understand when a system falls over
1. Learn about distributed systems
1. Play with local-first software solutions like CRDTs

## Design Goals

1. Single binary
    - Should it be an HTTP server or a CLI? #DECIDE
    - I'm leaning toward HTTP server because realistically folks want to test their
    systems in their production environment.
    - HOWEVER, then you aren't just testing a _system_. You are testing a system in an _environment_.
        - But, isn't this how systems run in production? Often it's not just a
        binary, but an entire architecture to protect the binary e.g., load balancers, etc.
        - This is where we have space. Jepsen doesn't care about the environment.
        Nor should Jepsen because that's not the goals of the project.
    - Give lodiseval-rs a list of addresses
1. Minimal lift to test your system
    - Default set of tests
1. Be able to run in a CI environment
1. Allow you to write your own tests
    - How do read-after writes behave when there is 1000ms of latency on writes
1. Pluggable load-testing? #DECIDE
    - Use `hey`, `vegetta`, etc. bring your own
    - Exec out to one of these load test tools?
1. Nodes: binaries or Docker containers
1. Collect metrics that the orchestrator is aware of
    - Don't try to implement a full metric collection system or interface.

## User Experience

1. Start the lodiseval control plane server
1. HTTP `POST` (Or file watch a YAML file? #DECIDE) a test JSON that includes:
    - target URLs list
    - tests / assertions
        - load
        - read after write
        - concurrent writes
