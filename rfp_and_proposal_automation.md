# RFP and Proposal Automation


## Solution Objective

Build a RFP & proposal automation platform on top of Salesforce that can collect data from many different sources and generate PDF and Word documents.

## Solution Requirements

### Architecturally Significant Requirements


### Key Functional Requirements

* Ability to collect data from different custom or standard objects in Salesforce. 


### Integration Requirements

* Centralized file storage in a secure cloud storage.


### Security Requirements

* Support for both row-level and object-level security:

* Support for secure file storage


## Solution Architecture

The following diagram shows the overall architecture of the solution.

![Architecture Diagram](./media/architecture-diagram.png)

Azure Data Factory (ADF) orchestrates and Azure Data Lake Storage (ADLS) Gen2 stores the data:

1. The Contoso city parking web service API is available to transfer data from the parking spots.

1. There's an ADF copy job that transfers the data into the Landing schema.

1. Next, Azure Databricks cleanses and standardizes the data. It takes the raw data and conditions it so data scientists can use it.

1. If validation reveals any bad data, it gets dumped into the Malformed schema.

    > [!IMPORTANT]
    > People have asked why the data isn't validated before it's stored in ADLS. The reason is that the validation might introduce a bug that could corrupt the dataset. If you introduce a bug at this step, you can fix the bug and replay your pipeline. If you dumped the bad data before you added it to ADLS, then the corrupted data is useless because you can't replay your pipeline.

1. There's a second Azure Databricks transform step that converts the data into a format that you can store in the data warehouse.

1. Finally, the pipeline serves the data in two different ways:

    1. Databricks makes the data available to the data scientist so they can train models.

    1. Polybase moves the data from the data lake to Azure Synapse Analytics and Power BI accesses the data and presents it to the business user.

## Components

The solution uses these components:

* [SteelHead DocumentHub]()

* [SteelHead CPQHub]()

* [SteelHead ContractHub]()

* [SteelHead CloudStorage]()


## Solution Considerations

The following list summarizes key learnings and best practices demonstrated by this solution:


## Next Steps


## Related Resources

### Solution code samples on GitHub

* [Visit the project page on GitHub]()

