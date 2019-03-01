## Context
Conductor enforces barriers on the size of workflow and task payloads for both input and output. These barriers are used as safeguards to prevent the usage of conductor as a data persistence system and to reduce the pressure on its datastore.


## Barriers
Conductor typically applies two kinds of barriers:
* Soft Barrier
* Hard Barrier


#### Soft Barrier
The soft barrier is used to alleviate pressure on the conductor datastore. In some special workflow use-cases, the size of the payload is warranted enough to be stored as part of the workflow execution.  
In such cases, conductor externalizes the storage of such payloads to S3 and uploads/downloads to/from S3 as needed during the execution. This process is completely transparent to the user/worker process.  

!!!warning "Note"
    The task input and output payload soft barriers are set to 3MB.
    The workflow input and output payload soft barriers are set to 5MB.


#### Hard Barrier
The hard barriers are enforced to safeguard the conductor backend from the pressure of having to persist and deal with voluminous data which is not essential for workflow execution.
In such cases, conductor will reject such payloads and will terminate/fail the workflow execution with the reasonForIncompletion set to an appropriate error message detailing the payload size.

!!!warning "Note"
    The hard barriers for task and workflow payloads are set to 10MB.
