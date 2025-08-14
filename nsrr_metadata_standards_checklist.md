# NSRR (Meta)data Standard and Checklist

Thank you for considering sharing your data - an invaluable contribution that advances research and benefits the entire scientific community. We understand that preparing data for sharing can sometimes feel overwhelming, which is why we’re here to support you every step of the way.

Adopting clear standards for data and metadata not only enhances the FAIR principles - making data more _Findable, Accessible, Interoperable, and Reproducible_ - but also maximizes their long-term value for the research community. While the NSRR provides tools to improve data quality and interoperability, we recognize that data donors and generators play a vital role in ensuring their datasets are accurate, well-documented, and ready for sharing. Ideally, data should be collected with the goal of clearly defining all elements, with ongoing quality assurance during the course of data collection to ensure data are collected per protocol with minimal missing data or erroneous data.

This guide is designed to make the process as smooth as possible, offering practical advice on preferred formats, self-check tips for data quality, and best practices to ensure your data is ready for sharing. Whether you’re new to data sharing or looking to refine your approach, we’re committed to working with you to make your data as accessible, reusable, and impactful as possible. For NIH-funded projects, these recommendations can be incorporated into your Data Management and Sharing Plan before data collection begins. If your data was collected prior to adopting these practices, we encourage you to review your data and metadata documentation to identify potential areas for improvement.

## Preferred file Formats

NSRR currently hosts two main types of data: sleep biometric data (e.g. polysomnography, actigraphy, light exposure, etc.); and other non-biometric data (e.g. demographics, clinical measures, survey questionnaires, etc.)

We encourage data donors to deposit “analytic datasets”, typically structured as one row per subject per time point. If generating an export from a REDCap project, please also include the REDCap data dictionary (`.csv`) and REDCap Codebook (`.pdf`). If the project is longitudinal, please also describe the REDCap events and repeating instruments.

### Tabular Data

* Preferred data format:
   `.csv`, `.sas7bdat`, `.xlsx`, etc.  (open-source data format strongly recommended) 
* Recommendations for best practices:
  - **Rectangular layout**: maintain consistent rows (observations) and columns (variables) and avoid merging cells which disrupt machine readability [[1]](https://data.research.cornell.edu/data-management/archiving-and-preservation/preparing-tabular-data-for-description-and-archiving/)
  - **Atomic Data Points**: store one value per cell. Consider split composite fields like “5 PM” into (5:00 and PM) [[2]](https://pmc.ncbi.nlm.nih.gov/articles/PMC11602091/)
  - **Avoid Excel special formatting**: remove merged cells and color coding; store formulas separately from raw data; change cell type to "Text" before input to prevent reformatting. 
  - **Descriptive headers**: use concise, machine-readable column names, start with letters and avoid special characters or spaces (use underscores or dashes instead)
  - **Consistent and standardized codes**: apply the same conventions for (1) date (`YYYY-MM-DD`) and time (`HH:MM:SS`) [[3]](https://datamanagement.hms.harvard.edu/collect-analyze/analysis-ready-datasets), and (2) missing data with explicit codes (e.g., `na`) across all variables, and specify in metadata [[4]](https://guides.library.stanford.edu/data-best-practices/manage-spreadsheets)
    


## Polysomnography/Home Sleep Apnea Test Data

* Preferred data format:  
  - **Signals**: `.edf`, `.edf+`
  - **Annotations**: preferred in `.xml` and `.edf+`; also acceptable in `.txt`, `.csv`, `.tsv`, etc. 
* Recommendations for best practices:  
   Below is a brief description of essential key requirements. We advise potential data donors to review [NSRR Signal and Annotations Conventions][signal_convention] for the full list of requirements and recommendations in details.
   1. Fill out the polysomnography tab from the [NSRR Metadata Intake Form][mif].
   2. Submit **Manuals of Procedure (MOP)** which includes **signal collection protocol and procedures**.
   3. Submit **montage and sampling rates**.
   4. Submit **event annotations and scoring criteria**:
       The annotation files should have at least the following columns: _event name_, _event start time_, and _event end time_ (or _event duration_).
   5. When submit **sleep staging data**:
      a. Staging and annotations can be combined or separate. If the staging annotations are separate, please make sure the whole recording is annotated with breaks defined. 
      b. When possible, please include explicit `LightsOn` and `LightsOff` annotations.
      c. Provide a legend if using non-standard terms
   6. Submit **signal quality assurance metrics** (if available)  
   7. Consider conducting some **QC/QA steps** following the [NSRR Signal and Annotations Conventions][signal_convention]. Here are some examples:
      a. Sample rates should be kept as high as possible, e.g., for EEG, EMG, ECG, etc. And ideally at least 200 Hz
      b. Avoid EDFs with identical channel names
      c. Name signal files to match the IDs of the corresponding study/individual/recording, with a single extension specifying the type of file (e.g., `test1.xml` or `test1-nsrr.xml` correspond to `test1.edf`).
      d. Raw data with no filtering applied is required
      e. Please list what signals can be ignored (if any)
      f. Consistent signal names, frequencies, and units across all collected data is highly recommended
    8. Optional but highly recommended:  
        To increase the visibility, discoverability and reusability of your data, we recommend providing a reference table to map channel names used in your signal files to the [NSRR "canonical signal channel names"](https://gitlab-scm.partners.org/zzz-public/nsrr/-/tree/master/common) or [NSRR Dataset Discovery](matrix.sleepdata.org), which will likely decrease the turnaround time for publishing the signal data. (If not submitted, please submit a list of signal channel labels and short descriptions.)



## Actigraphy Data

* Preferred data format:
   `.csv`, `.bin`, `.awd`, etc.   
* Recommendations for best practices:
  1. Fill out the actigraphy tab from the [NSRR Metadata Intake Form][mif].
  2. Submit **Manuals of Procedure (MOP)** which includes data collection protocol and procedures.


# Data and Metadata Quality Checklist

Evaluate your dataset using the criteria below before submission.

## Completeness

Data donors are encouraged to evaluate the completeness of the metadata at three levels: study level, file level, and variable level.

| Level                                                                      | Requirements                                                                                                                                                                                                                                | Common Issues & Solutions                                                                                                                                                                                                                                        |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Study-Level                                                                | Protocol documents describing the overall protocol (which includes sections such as the purpose of study, study design, sample studied, data collection procedures, etc.) ,README ([NSRR template](https://sleepdata.org/datasets/apples)), publications, [NSRR Metadata Intake Form][mif]. | **- Missing scoring criteria**: Document respiratory event definitions (e.g., flow reduction, desaturation threshold and arousal condition for hypopneas) in the MOP.<br>**- Undocumented device variations**: Document all devices used at different sites.                 |
| File-Level (individual data files such as raw signal and annotation files) | Clear naming conventions, file hierarchy, and documentation.                                                                                                                                                                                | **- Unwanted space and special characters in filenames**: Use alphanumeric characters, underscore or dash only.<br>**- Unclear file hierarchy or naming convention**: Add a manifest explaining file relationships (e.g., file names encoding subject treatment).            |
| Variable-Level                                                             | Data dictionary/codebook for all variables.                                                                                                                                                                                                 | **- Undocumented variables**: Ensure 1:1 mapping between dataset headers and data dictionary.<br>**- Unexplained missing codes**: Fully document the usage of missing code (e.g., -9, 99, M, R, etc.) for any numeric or categorical values in the data dictionary/codebook. |

## Consistency

Within a given study, procedures for data collection and processing may vary (e.g., by time, across study entities, etc.). Any such differences should be documented prospectively (e.g., using a “change log” and reflected in study documentation. Before data are shared, any variation in measurement or processing should be documented fully in the study-level and file-level metadata.

**Common issues:**

- Different units (e.g., kg, lb, inch, cm) used across sites/visits/individuals.

- Different data collection (e.g., device), calibration and processing procedures across sites/visits/individuals

- Inconsistent signal channel labels across sites/visits/individuals

**Actions**:

- Standardize units, labels, and procedures in the data management plan.

- Document exceptions in metadata.

- Consider mapping variables to CDEs

  - e.g., <https://sleepdata.org/datasets/answers/variables/psqi_10>

- For PSG data, consider adopting the [NSRR Signal Data Conventions](https://gitlab-scm.partners.org/zzz-public/nsrr/-/blob/master/common/uploads.md)

## Integrity

Underlying quality issues and errors can manifest as unlikely values. Therefore, we strongly encourage potential data donors to validate data distributions and file integrity. Here are some common data issues we have seen in the past:

**Common issues:**

- Corrupt files

- Outliers or implausible values for commonly used variables (i.e., age, sex, BMI)

- Duplicated IDs among signal files

- IDs in phenotype data and signal files do not match

- Dataset headers and data dictionary entries do not match

- Multiple signal files per subject and/or night

**Action**:

- Use validation scripts or manual audits to flag anomalies. If clear errors are confirmed, these should be corrected (and documented to provide an audit trail) prior to data transfer.

## Confidentiality/Privacy

All shared study data at NSRR must be de-identified using the [HIPAA Safe Harbor method](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html) and must adhere to the data sharing language stated in the participant informed consent. However, NSRR will provide guidance and/or assistance for de-identification when necessary. Each data set needs to identify appropriate Data Use Limitations (DULs). Examples of DULs include General Research Use and Commercial vs. Non-commercial use Data contributors should ensure that DULs for shared data are in line with applicable ethics review, consent, and organizational requirements. This includes the potential for mixed data usage restrictions (e.g., commercial/non-commercial usage restrictions that differ across participants or sites).

Before submitting data to NSRR, please review the steps outlined in the [NHLBI guidelines](https://www.nhlbi.nih.gov/grants-and-training/policies-and-guidelines/guidelines-for-preparing-clinical-study-data-sets-for-submission-to-the-nhlbi-data-repository) regarding de-identification.

**Common issues:**

- Data contains PHIs (names, addresses, medical record numbers, etc.)

- Dates in filenames (if dates are not approved for ingestion to NSRR)

**Action**

- Remove/recode obvious identifiers and those considered to be protected health information (PHI)/personally identifiable information (PII) (e.g., name, addresses, social security numbers, place of birth, city of birth, contact data).

- As possible recode all dates to a specific reference point (i.e., index date).

- Multiple versions of datasets maybe needed, or alternatively, variables specifying the consent level for each participant (and the informed consent files) should be submitted.


[mif]:(https://www.dropbox.com/scl/fi/ke844q6p8juqz68svsud5/Meta-data-cohort-info-intake-form_06_09_2025.xlsx?rlkey=xqu8r6wvouktesvgvzgfs5nbb&st=ckw7kbwg&dl=0)
[signal_convention]:(https://gitlab-scm.partners.org/zzz-public/nsrr/-/blob/master/common/uploads.md)