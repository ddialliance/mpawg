# Recommendation for Publishing and Accessing DDI Metadata via OAI-PMH

## Recommendation of the DDI Alliance for repository operators and metadata harvesters – DRAFT

# Minimal Use Case

A harvesting agent can retrieve through the OAI-PMH protocol all publicly accessible DDI metadata records in order to determine the total number of available records.  
The process consists of two steps: (1) discovering all publicly accessible OAI-PMH endpoints that expose DDI metadata, and (2) accessing each endpoint to count the total number of available DDI records.

Note: While additional use cases could be defined, this minimal use case serves as a baseline reference for implementing and evaluating OAI-PMH-based access to DDI metadata.

# Discovery

Two registries can be used to discover OAI-PMH endpoints that provide DDI metadata: the DDI Registry (https\://registry.ddialliance.org/) and re3data.org. The DDI Alliance recommends registering in the DDI Registry. re3data.org is currently the most widely used registry of research data repositories. At the time of writing, 340 repositories listed there report using DDI, 241 of them report OAI-PMH support, and nearly 200 actually provide DDI metadata via OAI-PMH. Entries in re3data.org can be suggested or updated by repository operators or third parties and are reviewed by the re3data.org editorial team. The information on supported standards and APIs is self-reported, however, and is not checked against the actual endpoint.  
For automated discovery, re3data.org offers an API, and the DDI Registry provides a regularly updated data dump here: https\://registry.ddialliance.org/data. Harvesters should use both sources and deduplicate endpoints by their base URL. As URLs in re3data.org are recorded inconsistently, normalize them first, e.g. by removing any query, trailing slashes and differences between http and https.  
Repositories that publish DDI metadata should:

- register in the DDI Registry, providing the full Identify URL (base URL followed by `?verb=Identify`);  
- if listed in re3data.org, make sure the entry states DDI as metadata standard and OAI-PMH as API, using the same full Identify URL.

Examples of valid Identify URLs:

* [https\://services.fsd.tuni.fi/v0/oai?verb=Identify](https://services.fsd.tuni.fi/v0/oai?verb=Identify)  
* [https\://dataverse.harvard.edu/oai?verb=Identify](https://dataverse.harvard.edu/oai?verb=Identify)

Both return a valid Identify response. Some servers attach a stylesheet, so that browsers display a formatted page; others show the raw XML. Both are fine.

## Checklist

Meet the following conditions:

- **OAI-PMH endpoint is operational and accessible**  
  - If the repository uses Dataverse or Colectica Repository, OAI-PMH is enabled.  
- **The repository is listed in the DDI Registry:**  
  - in section „Http Resolvers“, Resolution type „OaiPmhIdentify“ contains the full Identify URL.  
- **If the repository is listed in re3data.org, the entry indicates:**  
  - **DDI metadata standard is in use.** (The specific version cannot be indicated.)  
  - **OAI-PMH endpoint is provided as full Identify URL.** 

## Common problems

- The repository uses Dataverse with OAI-PMH enabled and does not provide a valid endpoint URL: Access the endpoint you want to provide in your browser. You should get a meaningful response, see examples above.  
- The repository uses Dataverse and does not state that it is using DDI. Dataverse has built-in support for DDI-Codebook. Select DDI as metadata standard in the re3data.org entry.  
- A new repository can be suggested to re3data.org: https\://www\.re3data.org/suggest  
- If the DDI Registry and [re3data.org](http://re3data.org) are no options for registration: Contact Knut Wenzig ([kwenzig@diw.de](mailto:kwenzig@diw.de)) as he publishes regularly a list of OAI-PMH endpoints, which provide DDI metadata, and will add your endpoint to this list.

# Retrieval

With the request ListMetadataFormats, an OAI-PMH server informs harvesters which metadata formats are available. For each format, a metadataPrefix, a schema and a metadataNamespace must be specified. ListMetadataFormats is therefore the authoritative source for the DDI standards and versions an endpoint offers – independent of what registries report.

The following overview shows the recommended attributes for the different products of the DDI Alliance:

DDI-Codebook 2.5

- metadataPrefix:ddi-codebook\_2.5  
- schema: https\://ddialliance.org/Specification/DDI-Codebook/2.5/XMLSchema/codebook.xsd  
- metadataNamespace: ddi:codebook:2\_5

DDI-Codebook 2.6

- metadataPrefix:ddi-codebook\_2.6  
- schema: https\://ddialliance.org/Specification/DDI-Codebook/2.6/XMLSchema/codebook.xsd  
- metadataNamespace: ddi:codebook:2\_6 

DDI-Codebook (see note below)

- metadataPrefix:ddi-codebook  
- schema: use one of the schemas for DDI-Codebook listed above  
- metadataNamespace: use one of the metadataNamespaces for DDI-Codebook listed above

DDI-Lifecycle 3.1

- metadataPrefix: ddi-lifecycle\_3.1  
- schema: https\://ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/instance.xsd  
- metadataNamespace: ddi:instance:3\_1

DDI-Lifecycle 3.2

- metadataPrefix: ddi-lifecycle\_3.2  
- schema: https\://ddialliance.org/Specification/DDI-Lifecycle/3.2/XMLSchema/instance.xsd  
- metadataNamespace: ddi:instance:3\_2

DDI-Lifecycle 3.3

- metadataPrefix: ddi-lifecycle\_3.3  
- schema: https\://ddialliance.org/Specification/DDI-Lifecycle/3.3/XMLSchema/instance.xsd  
- metadataNamespace: ddi:instance:3\_3

DDI-Lifecycle (see note below)

- metadataPrefix: ddi-lifecycle  
- schema: use one of the schemas for DDI-Lifecycle listed above  
- metadataNamespace: use one of the metadataNamespaces for DDI-Lifecycle listed above

DDI-CDI 1.0

- metadataPrefix: ddi-cdi\_1.0  
- schema: http\://www\.ddialliance.org/Specification/DDI-CDI/1.0/XMLSchema/ddi-cdi.xsd  
- metadataNamespace: http\://ddialliance.org/Specification/DDI-CDI/1.0/XMLSchema/

DDI-CDI (see note below)

- metadataPrefix: ddi-cdi  
- schema: use the schema for DDI-CDI listed above  
- metadataNamespace: use the metadataNamespace for DDI-CDI listed above


  
Note: When the metadataPrefix does not include a version, the repository chooses one version of the format. The schema and metadataNamespace declared in ListMetadataFormats identify this version, and all records disseminated with this prefix must conform to it. For a given version of a format, use either the versioned or the unversioned metadataPrefix, not both.

As many existing endpoints use other prefixes, harvesters should identify DDI formats by the declared metadataNamespace, not by the metadataPrefix.

The response to ListIdentifiers (e.g. `?verb=ListIdentifiers&metadataPrefix=ddi-codebook_2.5`) can report the total number of records in the attribute completeListSize of the resumptionToken element. This is optional in OAI-PMH but recommended here, as it allows harvesters to determine the number of records without paging through all identifiers. If all identifiers fit into a single response, no resumptionToken is returned and the records can be counted directly.

## Checklist

Meet the following conditions:

- **metadataNamespace matches the official DDI namespace** (see above)  
- **Official DDI XML schema URLs are used** (recommended)  
- **metadataPrefix follows the recommendation above**  (optional)
- **OAI-PMH server exposes the number of available metadata records as attribute in element resumptionToken** (recommended)

## Common problems

- Validate your records against the schema before publishing.  
- Some use cases require publishing several variants of records in the same standard, e.g. DDI-Codebook records with study-level information only and records that also include variable-level information. In this case, add a suffix to the metadataPrefix, separated by an underscore.