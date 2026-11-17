# System purpose
DepotManager — initial system understanding
A parcel depot needs software to manage parcels, customers waiting to collect them, collection fees, and end-of-day reporting.

Initial functional requirements to verify against the brief
- Load parcel and customer records.
- Store and retrieve parcels using parcel IDs.
- Serve waiting customers in FIFO order.
- Calculate collection fees.
- Mark successfully collected parcels.
- Handle missing parcels and other errors.
- Record significant events in a log.
- Produce an end-of-day report.
# Actors and users
Primary actor: Depot Worker

The depot worker interacts with DepotManager to retrieve parcel information, process customers, calculate collection fees, and record successful collections.

Customer: The customer requests their parcel through the depot worker but does not directly interact with the software. Therefore, the customer is not an actor in this use-case model.
# Functional requirements
## Mandatory funtional requirements
ID	Functional requirement
FR-01	The system shall load parcel records from a text file.
FR-02	The system shall load customer records from a text file.
FR-03	The system shall store and retrieve parcels by their unique IDs.
FR-04	The system shall maintain a first-in-first-out customer queue.
FR-05	The system shall calculate parcel collection fees using the specified formula.
FR-06	The system shall process customers and update successfully collected parcels.
FR-07	The system shall handle invalid records and unsuccessful collection attempts.
FR-08	The system shall log significant operations.
FR-09	The system shall generate an end-of-day report.
## Proposed functional enhancements
ID	Proposed requirement
PE-01	The system should create a collection receipt for every successful collection.
PE-02	Each receipt should reference the parcel, recipient, and collection timestamp.
PE-03	The system should retain an audit trail of significant operations and collection events.
PE-04	The system should support an appropriate method of verifying the recipient's identity.
# Non-functional requirements and assumptions 
ID	Requirement
NFR-01	Maintainability: The software should separate presentation, business logic, and data responsibilities to simplify future modifications.
NFR-02	Scalability: The architecture should allow future expansion to additional depot operations, potentially including deliveries.
NFR-03	Data integrity: The system should maintain accurate collection status and prevent inconsistent transaction records.
NFR-04	Privacy: The system should minimise the collection and retention of sensitive personal information.
NFR-05	Traceability: Significant collection operations should be attributable and auditable.