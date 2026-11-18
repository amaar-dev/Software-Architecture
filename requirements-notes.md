# System purpose
DepotManager — initial system understanding
A parcel depot needs software to manage parcels, customers waiting to collect them, collection fees, event logging, and end-of-day reporting.

Mandatory system features from the brief
- Customers can join the collection queue at any point.
- Depot workers can process customers one at a time in FIFO order.
- Depot workers can look up parcels using parcel IDs.
- The system calculates collection fees from weight, volume, and time in the depot, with a discount for a particular parcel ID category.
- Depot workers can release collected parcels and add new parcels.
- Depot workers can view outstanding parcels and current processing details.
- Significant events and errors are recorded in one shared event log.
- Depot workers can generate a written end-of-day report showing collected parcels, outstanding parcels, and fees taken.

# Actors and users
Primary actor: Depot Worker

The depot worker interacts with DepotManager to process customers, look up parcels, calculate collection fees, release parcels, add parcels, view system information, and generate the end-of-day report.

Primary actor: Customer

The customer directly interacts with DepotManager to join the collection queue and state the parcel they wish to collect. The Customer must therefore appear as an actor in the use-case diagram.

# Functional requirements
## Mandatory functional requirements

| ID | Functional requirement |
|-----|------------------------|
| FR-01 | The system shall allow a customer to join the collection queue and provide the parcel ID they wish to collect. <br/>|
| FR-02 | The system shall process the next customer from the front of the queue. <br/>|
| FR-03 | The system shall look up a parcel using its unique parcel ID. <br/>|
| FR-04 | The system shall calculate the collection fee using parcel weight, volume, time in the depot, and the specified parcel ID discount. <br/>|
| FR-05 | The system shall release a parcel by marking it as collected and removing it from outstanding stock. <br/>|
| FR-06 | The system shall allow a depot worker to add a new parcel. <br/>|
| FR-07 | The system shall show parcels awaiting collection. <br/>|
| FR-08 | The system shall show the customer and parcel currently being processed. <br/>|
| FR-09 | The system shall generate a written end-of-day report of collected parcels, outstanding parcels, and fees taken. <br/>|
| FR-10 | The system shall record significant events, state changes, and errors in one shared event log. <br/>|

## Mandatory use cases

| Actor | Use case |
|-------|----------|
| Customer | Join Collection Queue |
| Depot Worker | Process Next Customer |
| Depot Worker | Look Up Parcel |
| Depot Worker | Calculate Collection Fee |
| Depot Worker | Release Parcel |
| Depot Worker | Add New Parcel |
| Depot Worker | View Parcels Awaiting Collection |
| Depot Worker | View Current Processing Details |
| Depot Worker | Generate End-of-Day Report |
| System-level | Record Event to Log |

Record Event to Log is an included system responsibility and is not initiated directly by an actor.

## Proposed optional or exceptional use case

| ID | Proposed requirement |
|-----|----------------------|
| PE-01 | Handle Parcel Not Found may extend Look Up Parcel when the requested parcel ID cannot be located. The error is shown and recorded in the shared event log. <br/>|

This is an interpretation of the brief's stated error scenario, not one of the ten mandatory named use cases.

# Use-case relationship notes
- Join Collection Queue `<<include>>` Record Event to Log.
- Process Next Customer `<<include>>` Record Event to Log.
- Release Parcel `<<include>>` Record Event to Log.
- Add New Parcel `<<include>>` Record Event to Log.
- Generate End-of-Day Report `<<include>>` Record Event to Log.
- Handle Parcel Not Found `<<include>>` Record Event to Log.
- Handle Parcel Not Found `<<extend>>` Look Up Parcel because it happens only when a parcel cannot be found.
- An `<<include>>` arrow points from the main use case to the included use case.
- An `<<extend>>` arrow points from the optional or exceptional use case to the base use case.

The read-only use cases do not need to include logging unless the final design deliberately treats viewing or calculating as a significant logged event. Avoid adding relationships only to make the diagram look connected.

# Non-functional requirements

The brief does not explicitly specify named non-functional requirements. The following are design assumptions or quality goals, not mandatory brief requirements.

| ID | Requirement |
|-----|-------------|
| NFR-01 | **Maintainability:** The software should separate presentation, business logic, and data responsibilities to simplify future modifications. <br/>|
| NFR-02 | **Data integrity:** The system should maintain accurate parcel status, queue order, and fee totals. <br/>|
| NFR-03 | **Traceability:** Significant operations and errors should be recorded in the single shared event log. <br/>|

# Assumptions

| ID | Assumption |
|-----|------------|
| A-01 | The system operates at one depot location. <br/>|
| A-02 | The Customer actor uses the system only to join the queue; the depot worker completes the collection process. <br/>|
| A-03 | Parcel and customer data are stored in a format that the Part 2 implementation can load and save. <br/>|
| A-04 | An authorised depot worker records each parcel's details before it is made available for collection. <br/>|
| A-05 | Parcel records contain accurate weight, dimensions, days in the depot, and parcel ID information needed to calculate fees and discounts. <br/>|
| A-06 | Payment processing is outside the current scope; the system calculates and totals fees taken. <br/>|

# Constraints and deliverables

| ID | Constraint |
|-----|------------|
| C-01 | Part 1 must contain a UML use-case diagram, class diagram, and three-tier architecture model. <br/>|
| C-02 | The use-case diagram must contain a labelled DepotManager system boundary, both actors, all ten mandatory use cases, at least one `<<include>>`, and at least one `<<extend>>`. <br/>|
| C-03 | The class diagram must show key attributes and methods, relationships, multiplicities, container classes, and a justified list, map, or set choice. <br/>|
| C-04 | Every class in the class diagram must appear in exactly one of the Presentation, Business Logic, or Data tiers. <br/>|
| C-05 | The architecture explanation must be 150–250 words and connect the three tiers to MVC. <br/>|
| C-06 | Part 1 must be submitted as one PDF using the required student-number and surname filename pattern. <br/>|

Java, Swing, required class names and packages, and restrictions on build tools or language features are not stated in this Part 1 brief. They should only be treated as constraints if they are specified separately in the Part 2 brief or supplied starter code.
