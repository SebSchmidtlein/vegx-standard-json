# Veg-X JSON: A revised standard for vegetation data exchange

## Abstract

## 1. Introduction
### 1.1 Vegetation data exchange
### 1.2 History of Veg-X
#### 1.2.1 Origins and objectives
#### 1.2.2 Development of the XML standard
#### 1.2.4 Experience with implementation and adoption
### 1.3 Rationale for a new version

The XML version of Veg-X divided closely related information among many separately defined elements connected by identifiers. For example, interpreting a species cover record could require following links to elements scattered throughout the XML document. This structure made routine records difficult to understand, create, and process. Therefore, implementing import and export tools was time-consuming and error-prone and may have contributed to the limited adoption of the standard. The revision does not remove those elements; it reorganizes them so related information is less dispersed and requires fewer cross-references.

We chose JSON for the revision because its compact data model is well suited to representing nested records. The JSON Veg-X model uses this nesting to keep related information together. For example, XML Veg-X links a plot observation to a separately defined plot by an identifier, whereas JSON Veg-X nests the observation within its plot (Table 1).

Table 1. Minimal example comparing the representation of a plot observation in XML and JSON Veg-X.

| XML Veg-X | JSON Veg-X |
|---|---|
| `<plot id="31">`<br>&nbsp;&nbsp;`<plotName>1</plotName>`<br>`</plot>`<br><br>`<plotObservation>`<br>&nbsp;&nbsp;`<plotID>31</plotID>`<br>&nbsp;&nbsp;`<obsStartDate>2026-08-06</obsStartDate>`<br>`</plotObservation>` | `{`<br>&nbsp;&nbsp;`"plotName": "1",`<br>&nbsp;&nbsp;`"plotObservations": [`<br>&nbsp;&nbsp;&nbsp;&nbsp;`{`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`"obsStartDate": "2026-08-06"`<br>&nbsp;&nbsp;&nbsp;&nbsp;`}`<br>&nbsp;&nbsp;`]`<br>`}` |

JSON’s relatively simple structure and readability by both people and computers have contributed to its widespread use, especially for web-based data exchange [@bourhis_2020]. Like XML Schema, JSON Schema provides machine-readable validation of document structure, required properties, data types, and permitted values [@barbaglia_2017]. 

XML Veg-X was improved over time, but the need to maintain backward compatibility limited opportunities to simplify established concepts and structures. The transition from XML to JSON made direct structural compatibility unnecessary and provided an opportunity to simplify the model rather than translate it directly.

For example, XML Veg-X used different structures for the original identification of a taxon, later determinations, and the currently preferred nomenclatural interpretation. Updating the preferred interpretation therefore required coordinating several linked elements. JSON Veg-X instead represents all determinations using the same structure in a list nested within the observation, with properties identifying the original and preferred determinations. This preserves changes in identification and nomenclature while making their sequence and provenance easier to follow. Appendix S1 provides minimal code examples illustrating the representation of taxon determinations and other concepts. 

Another example concerns cover values. In XML Veg-X, cover was represented as a generic measurement linked to a separate attribute definition. For ordinal cover, each cover class required its own attribute, linked in turn to the cover scale. In JSON Veg-X, the explicit `coverValue` property contains the recorded value and directly names the applicable cover scale.

By making Veg-X records easier to understand, create, and process, we expect the revision to remove some of the practical barriers that limited adoption of the XML standard. The following sections describe in more detail the design principles, the resulting changes to the information model, and the representation of vegetation data in JSON Veg-X.

## 2. Design Principles
### 2.1 Document-oriented organization
### 2.2 Self-contained and intelligible records
### 2.3 A small, approachable core
### 2.4 Interoperability and validation
### 2.5 Preservation of information from XML Veg-X
### 2.6 Extensibility without unnecessary complexity

## 3. Changes from XML Veg-X
### 3.1 From a reference graph to nested documents
### 3.2 Simplification of identifiers and relationships
### 3.3 Explicit representation of common concepts
### 3.4 Concepts retained and reorganized
### 3.5 Concepts omitted or newly introduced
### 3.6 Implications for migration and information preservation

## 4. Representation of Vegetation Data
### 4.1 Information model (Note: only the model overview and relationship)
### 4.2 Taxonomic names, concepts, and determinations
### 4.3 Taxon occurrences and abundance
### 4.4 Individual organisms and repeated observations
### 4.5 Vegetation strata
### 4.6 Plot identity, location, and geometry
### 4.7 Temporal observations and resurveys
### 4.8 Measurements, units, and cover scales
### 4.9 Metadata, provenance, rights, and citations
### 4.10 User-defined information and extensions

## 5. Validation and Evaluation
### 5.1 Validation with JSON Schema
### 5.2 Representative example datasets
### 5.3 Round-trip and interoperability testing
### 5.4 Known limitations

## 6. Discussion
### 6.1 Expected benefits
### 6.2 Design trade-offs
### 6.3 Compatibility and adoption
### 6.4 Future development

## 7. Conclusions

## Acknowledgements

## Author Contributions

## References

# Appendix A: JSON Format Reference
## A.1 Document structure
## A.2 Object and property documentation
## A.3 Required and optional properties
## A.4 Identifiers and references
## A.5 Extension mechanism

# Appendix B: Complete Examples

# Appendix C: XML-to-JSON Concept Mapping

# Appendix D: Open Design Questions