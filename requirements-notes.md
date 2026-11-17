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
## Mandatory functional requirements

| ID | Functional requirement |
|-----|------------------------|
| FR-01 | The system shall load parcel records from a text file. <br/>|
| FR-02 | The system shall load customer records from a text file. <br/>|
| FR-03 | The system shall store and retrieve parcels by their unique IDs. <br/>|
| FR-04 | The system shall maintain a first-in-first-out customer queue. <br/>|
| FR-05 | The system shall calculate parcel collection fees using the specified formula. <br/>|
| FR-06 | The system shall process customers and update successfully collected parcels. <br/>|
| FR-07 | The system shall handle invalid records and unsuccessful collection attempts. <br/>|
| FR-08 | The system shall log significant operations. <br/>|
| FR-09 | The system shall generate an end-of-day report. <br/>|

## Proposed functional enhancements

| ID | Proposed requirement |
|-----|----------------------|
| PE-01 | The system should create a collection receipt for every successful collection. <br/>|
| PE-02 | Each receipt should reference the parcel, recipient, and collection timestamp. <br/>|
| PE-03 | The system should retain an audit trail of significant operations and collection events. <br/>|
| PE-04 | The system should support an appropriate method of verifying the recipient's identity. <br/>|

# Non-functional requirements

| ID | Requirement |
|-----|-------------|
| NFR-01 | **Maintainability:** The software should separate presentation, business logic, and data responsibilities to simplify future modifications. <br/>|
| NFR-02 | **Scalability:** The architecture should allow future expansion to additional depot operations, potentially including deliveries. <br/>|
| NFR-03 | **Data integrity:** The system should maintain accurate collection status and prevent inconsistent transaction records. <br/>|
| NFR-04 | **Privacy:** The system should minimise the collection and retention of sensitive personal information. <br/>|
| NFR-05 | **Traceability:** Significant collection operations should be attributable and auditable. <br/>|

# Assumptions

| ID | Assumption |
|-----|------------|
| A-01 | The system operates at one depot location. <br/>|
| A-02 | Customers interact with depot workers rather than directly with the software. <br/>|
| A-03 | Parcel and customer records are available in the expected input format. <br/>|
| A-04 | It is assumed that an authorised depot worker records each parcel's arrival and relevant details before the parcel is made available for collection. These records are subsequently loaded into DepotManager. <br/>|
| A-05 | Parcel records contain accurate information, including weight, dimensions, arrival date or days in depot, and any information needed to calculate applicable fees or discounts. <br/>|

# Constraints

| ID | Constraint |
|-----|------------|
| C-01 | The implementation must use Java. <br/>|
| C-02 | The graphical interface must use Java Swing, not JavaFX. <br/>|
| C-03 | The system must follow the required three-tier architecture. <br/>|
| C-04 | The implementation must preserve the provided class names, packages, and public method signatures. <br/>|
| C-05 | The implementation cannot use Maven, Gradle, lambdas, method references, or Java Streams. <br/>|
