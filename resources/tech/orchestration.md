# Orchestration & Workflows 
----------------------------------------------------------------

The problem we are trying to solve here is, manage dependencies across
different operations.

This operations will be defined as "tasks" and the can be anything:

- Writing to a storage service (database, file system, object store, cache)
- Calling an API
- Compute

Commonly, these are managed with a Directed Acyclic Graph (DAG), which is a
graph with an established direction that contains no loops and has two
components:

- Vertices (Objects): Could be referred as the tasks in this context
- Edges (Relationships): Could be referred as the dependencies in this context

The best solution in this case should be to completely separate the compute of
the tasks from the orchestration service.

The orchestration service should have one responsibility:

Coordinate the execution of tasks. 

Should provide:
- Retry policies
- Graphs diverging based on tasks results

Should not:
- Perform any computation

----------------------------------------------------------------

# Existing Services 
----------------------------------------------------------------

## AWS Step functions

Orchestration tool with native integrations with AWS Services

- Learn how to write Amazon State Language
- Custom integrations seem to be non-existent. You would need to wrap, for
  example, an HTTP call within a lambda
- It does not have an scheduler. Something else has to do that.
- Communicating results between tasks is very simple with json
- Does not use DAGs. They are directed graphs, but they can loop

### Definitions

- Steps -> Tasks

### Pricing

Standard: Long running (up to a year)
- First 4000 transitions are free
- Costs $0.025 cents per 1000 transitions 

Express: Up to 5 mins 
- Costs $1 per million requests
- Duration is charged at $0.06 per GB-hour

----------------------------------------------------------------

## Airflow

Open source Workflow management platform

- DAGs are defined with their python module
- AWS has a managed version. The "native" version is very hard to mantain
- Communicating results between tasks is more complex as it needs XCom

### Definitions

- Operator -> Tasks

### Pricing

- Small: Up to 50 DAGs - $364.56 
- Medium: Up to 250 DAGs - $550.56 
- Large: Up to 1000 DAGs - $736.56

----------------------------------------------------------------

## DAGster

