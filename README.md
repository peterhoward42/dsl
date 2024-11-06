
# A DSL for Designing and Executing Data Storage Provision

I designed a DSL which let you express the designs for new data storage 
platforms for projects, in the context of a very large international bank's IT
department. I also created the runtime interpreter for it, as a dockerized Go 
service.

It is used by storage subject matter experts (SMEs), to design new storage provisioning
services, and have the bank's projects access these operations on a 
self-service basis from a web portal. Note the SME's were not expected to have 
programming skills in the conventional sense.

The most important characterisics of the DSL were:

- To express the "programming intent" of the SME to implement policy best 
  practices and regulatory needs.
- To be the machine-readable lingua franca and source of truth for the wider 
  distributed system of which it formed part.
- To form the input to an interpreter that orchestrated deployment and
  configuration
- To be highly amenable to a purely UI editing experience that hid the actual DSL
  under the hood.
- The DSL supported the notion of being run in three sequential
  phases, with hours or days between each:
	-  Preprocessing for logical decision making, and reasoning capture.
	-  Feeding foward the conclusions from pre-processing into an async execution
	   phase (which did the infrastructure deployment)
	-  And finally a post-processing phase to wrap up the audit trail
- A sister, job-runner service, orchestrated and recorded those 3 phases.
- The "calls to action" for provisioning were delegated by the interpreter 
  asyncrounously to Ansible or custom Python scripts.


## Example DSL Scripts

These will make it much clearer what the generalised description above is 
describing.  As they are designed to illusrate each capability of the DSL 
language, and also formed part of the test suite.

You will see that the scripts are written in YAML according to a schema that
mandated language keywords and a nested block structure.

With the knowledge of the expected schema, the interpreter was able to infer the
"programming intent", but crucially also, by being simply "data", it was highly
amenable to design a rich UI to help SME's edit their "programming intent"
without ever seeing the DSL under the hood.

See examples in ./scripts.

