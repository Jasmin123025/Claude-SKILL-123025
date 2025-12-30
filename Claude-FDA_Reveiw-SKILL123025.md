<scratchpad>
Now I need to reanalyze the code from an FDA 510(k) reviewer's perspective, focusing on regulatory workflows, domain-specific skills, and practical review capabilities.

**FDA 510(k) Review Context:**
- 510(k) submissions demonstrate substantial equivalence to predicate devices
- Reviewers need to assess: indications for use, technological characteristics, performance data, biocompatibility, sterilization, labeling, risk analysis
- Review process involves: document analysis, predicate comparison, data validation, checklist completion, deficiency identification, report writing
- Multi-disciplinary teams: engineers, scientists, physicians, statisticians

**Skills Categories for FDA Officers:**
1. Document Intelligence & Processing
2. Regulatory Compliance Assessment
3. Comparative Analysis (predicate comparison)
4. Risk Management Evaluation
5. Evidence Synthesis
6. Report Generation
7. Workflow Optimization
8. Quality Assurance
9. Data Validation
10. Collaboration Tools

**30 New Skills (FDA-focused):**
1. Automated predicate device identification
2. Indications for use extraction and validation
3. Technological characteristic comparison
4. Performance testing sufficiency assessment
5. Biocompatibility standard gap analysis
6. Risk management file evaluation
7. Clinical data synthesis
8. Labeling claim verification
9. Substantial equivalence reasoning
10. Deficiency letter generation
11. Multi-version submission tracking
12. FDA guidance alignment checking
13. Standards conformance validation
14. Statistical analysis review
15. Benefit-risk assessment documentation
16. Review milestone tracking
17. Cross-reference verification
18. Expert consultation workflow
19. Decision documentation
20. Quality system inspection readiness
21. Post-market surveillance planning
22. Special controls evaluation
23. Literature review synthesis
24. Testing protocol adequacy assessment
25. Acceptance criteria validation
26. Device classification verification
27. Regulatory precedent search
28. Multi-reviewer collaboration
29. Audit trail maintenance
30. Knowledge base development

Let me structure these properly with FDA-specific context and practical applications.
</scratchpad>

<skill_md>
# SKILL.md for FDA 510(k) Review Officers

## Regulatory Review Skills Demonstrated in Code

### 1. Intelligent Predicate Device Analysis
**Description:** Automatically searching FDA databases (or simulating such searches) to identify relevant predicate devices based on device characteristics, product codes, and technological features, then synthesizing comparison data.
**Relevance:** The `render_510k_tab()` function collects device metadata (name, K-number, sponsor, product code) and generates prompts for the FDA search agent to find predicates and create structured comparison tables, streamlining the substantial equivalence assessment.

### 2. Indications for Use Extraction and Validation
**Description:** Parsing submission documents to extract claimed indications, intended patient populations, and contraindications, then comparing them against predicate device indications to assess equivalence boundaries.
**Relevance:** The summary_entities_agent systematically extracts indications as structured entities with context, enabling reviewers to quickly identify scope changes or indication creep that might affect substantial equivalence determinations.

### 3. Technological Characteristic Matrix Generation
**Description:** Creating comprehensive comparison tables that juxtapose the subject device's technological features against predicate device specifications across multiple dimensions (materials, energy source, mechanism of action, design).
**Relevance:** The agent prompts specifically request "AT LEAST 5 well-structured markdown tables" including technological characteristics, demonstrating how AI can structure complex comparative data that reviewers need for equivalence assessments.

### 4. Performance Testing Sufficiency Assessment
**Description:** Evaluating whether submitted bench, animal, and clinical testing data adequately demonstrate safety and effectiveness for the intended use, identifying gaps in test coverage or acceptance criteria.
**Relevance:** The 510(k) Intelligence tab generates tables covering "Performance testing (bench, animal, clinical) and acceptance criteria," helping reviewers systematically evaluate test design, sample sizes, endpoints, and statistical power.

### 5. Multi-Standard Biocompatibility Gap Analysis
**Description:** Cross-referencing device material contact types and durations against ISO 10993 series requirements to identify missing biocompatibility tests or non-compliant testing protocols.
**Relevance:** The comprehensive summary agent includes "Biocompatibility" as a dedicated section in review memos, enabling automated checking of whether all necessary endpoints (cytotoxicity, sensitization, irritation, etc.) are addressed per risk-based testing matrices.

### 6. Risk Management File Evaluation Framework
**Description:** Systematically reviewing risk analysis documents (per ISO 14971) to verify that all reasonably foreseeable hazards are identified, risk controls are appropriate, and residual risks are acceptable.
**Relevance:** The Summary & Entities agent extracts at least 20 key entities including "Entity Type: Risk" and "Entity Type: Mitigation," creating a traceable map of hazards to controls that reviewers can audit for completeness.

### 7. Clinical Data Synthesis and Critical Appraisal
**Description:** Aggregating clinical study data, literature reviews, and real-world evidence into coherent summaries that support safety/effectiveness claims, while identifying study limitations or biases.
**Relevance:** The text processing pipeline (PDF → Markdown → Summary) preserves clinical data structure, and the 3000-4000 word summary format ensures clinical evidence is thoroughly analyzed with benefit-risk discussion sections.

### 8. Labeling Claim Verification Against Evidence
**Description:** Cross-checking all claims in proposed labeling (IFU, product labels) against submitted performance data and predicate labeling to ensure claims are supported and not misleading.
**Relevance:** The comprehensive summary includes "outstanding issues" identification, which can flag unsupported labeling claims. The entity extraction with "Reviewer Comment / Considerations" column enables systematic claim-to-evidence mapping.

### 9. Substantial Equivalence Reasoning Documentation
**Description:** Articulating the logical chain from predicate selection through technological comparison to equivalence determination, creating clear documentation of the scientific/regulatory rationale for clearance decisions.
**Relevance:** The review report agent integrates checklist items and review results into "FDA review memo" format with sections for "Benefit-risk assessment" and "Conclusions and recommendations," ensuring defensible decision documentation.

### 10. Deficiency Letter Generation with Specific Citations
**Description:** Identifying incomplete, insufficient, or non-compliant submission elements and generating deficiency letters with specific regulatory citations, guidance references, and clear requests for additional information.
**Relevance:** The diff agent identifies "at least 100 meaningful differences" between document versions, providing the granularity needed to write specific deficiency items. The note keeper can organize deficiency tracking across multiple rounds.

### 11. Multi-Version Submission Tracking and Delta Analysis
**Description:** Managing multiple submission versions (original, amendments, AI responses), tracking what changed between versions, and verifying that all deficiencies were adequately addressed.
**Relevance:** The Comparator tab's dual-version PDF comparison with 100+ difference identification enables systematic verification of amendment completeness, preventing the common issue of sponsors only partially addressing deficiencies.

### 12. FDA Guidance Alignment Verification
**Description:** Loading relevant FDA guidance documents (Special Controls, Recognition documents, Guidance for Industry) and checking submission content against guidance recommendations to ensure compliance.
**Relevance:** The checklist_agent takes guidance documents as input and generates review checklists with "Rationale / Source (section of guidance)" columns, creating direct traceability from review items to regulatory expectations.

### 13. Consensus Standards Conformance Validation
**Description:** Verifying that devices claim conformance to appropriate FDA-recognized consensus standards and that provided test reports actually demonstrate conformance with standard requirements.
**Relevance:** The entity extraction includes "Entity Type: Test" with context fields, allowing reviewers to map claimed standards to actual test evidence and identify conformance gaps or outdated standard versions.

### 14. Statistical Analysis Review and Validation
**Description:** Evaluating statistical methods, sample size justifications, power calculations, and significance testing in performance studies to ensure conclusions are statistically valid.
**Relevance:** The comprehensive summary's "Performance testing" section can highlight statistical methodologies. The 3000-4000 word format ensures sufficient depth to critique study designs and statistical approaches for adequacy.

### 15. Benefit-Risk Assessment Documentation
**Description:** Systematically weighing device benefits (clinical outcomes, patient quality of life) against residual risks (adverse events, failure modes) to support regulatory decision-making.
**Relevance:** The 510(k) review memo structure explicitly includes "Benefit-risk discussion" and "Overall assessment" sections, providing frameworks for documenting how benefits outweigh risks for the intended patient population.

### 16. Review Milestone and Timeline Tracking
**Description:** Monitoring review progress against FDA performance goals (MDUFA timelines), tracking time spent on different review activities, and identifying bottlenecks in the review process.
**Relevance:** The Dashboard tab tracks "Total Runs," "Unique 510(k) Sessions," and timestamps all activities, providing visibility into review workload distribution and helping management optimize resource allocation across submissions.

### 17. Cross-Reference Verification and Document Integrity
**Description:** Validating that all internal document cross-references are correct, that summary tables match detailed sections, and that referenced attachments actually exist and contain claimed information.
**Relevance:** The entity extraction with "Location / Section" fields enables automated mapping of claims to evidence locations. The PDF page extraction function allows targeted verification of specific sections without manual navigation.

### 18. Expert Consultation Workflow Management
**Description:** Identifying when specialized expertise is needed (e.g., physician review of clinical data, statistician review of study design), documenting consultation requests, and integrating expert feedback into review decisions.
**Relevance:** The Note Keeper with "AI Action Items" magic can identify review items requiring expert input. The event logging tracks which agents/analyses were performed, creating audit trails of who reviewed what.

### 19. Decision Rationale Documentation and Audit Trail
**Description:** Creating comprehensive documentation of all review decisions (substantial equivalence determination, deficiency identification, special controls recommendations) with clear scientific and regulatory justifications.
**Relevance:** The review report generation integrates checklist completion with review results into formal memo format, ensuring all decisions are documented. The history logging creates timestamps for all review activities, supporting FOIA responses.

### 20. Quality System Inspection Readiness Assessment
**Description:** Evaluating whether manufacturing quality systems described in submissions align with 21 CFR Part 820 requirements and identifying potential inspection findings.
**Relevance:** The comprehensive summary can include "Design controls," "Process validation," and "Quality system" sections when processing quality system-related documents, helping reviewers assess QSR compliance during premarket review.

### 21. Post-Market Surveillance Planning Integration
**Description:** Identifying device characteristics that warrant post-market surveillance studies or conditions of clearance, and documenting recommendations for post-market requirements.
**Relevance:** The entity extraction with "Reviewer Comment / Considerations" enables reviewers to flag novel devices, new patient populations, or limited clinical data that might warrant post-market surveillance as a clearance condition.

### 22. Special Controls Evaluation and Recommendation
**Description:** Determining when Class II devices require special controls beyond general controls, recommending appropriate special controls (performance standards, post-market surveillance, specific labeling), and documenting the rationale.
**Relevance:** The comprehensive summary's risk management section and the "outstanding issues" identification help reviewers determine if general controls are sufficient or if special controls are needed to provide reasonable assurance of safety/effectiveness.

### 23. Scientific Literature Review and Synthesis
**Description:** Aggregating relevant peer-reviewed literature, clinical guidelines, and published performance data to supplement submission review, particularly for novel technologies or rare indications.
**Relevance:** The PDF processing pipeline can handle literature PDFs. The summary agent synthesizes multiple documents into coherent narratives, helping reviewers integrate literature evidence with submission data for comprehensive evaluations.

### 24. Testing Protocol Adequacy Assessment
**Description:** Evaluating whether test protocols (bench testing, animal studies, clinical trials) use appropriate methods, controls, sample sizes, and endpoints to answer relevant safety/effectiveness questions.
**Relevance:** The performance testing tables generated by agents include "acceptance criteria" columns, enabling systematic evaluation of whether pass/fail criteria are clinically relevant, statistically justified, and aligned with predicate device performance.

### 25. Acceptance Criteria Validation Against Clinical Relevance
**Description:** Verifying that test acceptance criteria are clinically meaningful (not just statistically significant), appropriate for the intended use, and aligned with or superior to predicate device performance.
**Relevance:** The entity extraction captures test results with context, allowing reviewers to assess if acceptance criteria thresholds are justified by clinical outcomes, user needs, or comparative predicate data rather than arbitrary values.

### 26. Device Classification and Product Code Verification
**Description:** Confirming that devices are classified in the appropriate regulatory class (I, II, III) and assigned correct product codes based on intended use and technological characteristics.
**Relevance:** The 510(k) Intelligence tab specifically collects and validates "Product Code" and "regulation number," and the agent can cross-check these against FDA device databases to ensure correct classification before proceeding with review.

### 27. Regulatory Precedent Search and Analysis
**Description:** Searching FDA databases for similar devices, past clearance decisions, warning letters, or recall events to inform current review decisions and ensure consistency in regulatory interpretation.
**Relevance:** The FDA search agent simulates database searches for similar devices and K-numbers, helping reviewers identify regulatory precedents, predicate clearance rationales, and historical review approaches for comparable technologies.

### 28. Multi-Reviewer Collaboration and Consensus Building
**Description:** Facilitating collaboration among multidisciplinary review team members (engineers, scientists, physicians, compliance officers), tracking review contributions, and building consensus on clearance decisions.
**Relevance:** The session state persistence and history logging enable multiple reviewers to work on the same submission. The note keeper and AI magics help consolidate insights from different team members into unified review memos.

### 29. Comprehensive Audit Trail Maintenance
**Description:** Automatically logging all review activities, document versions reviewed, agents executed, prompts used, and timestamps to support transparency, FOIA compliance, and quality assurance audits.
**Relevance:** The `log_event()` function captures tab, agent, model, token usage, and timestamp for every action. The Dashboard aggregates this into activity reports, providing complete audit trails for management oversight and external accountability.

### 30. Institutional Knowledge Base Development
**Description:** Building searchable repositories of review precedents, common deficiencies, testing strategies, and regulatory interpretations to improve review consistency and training for new reviewers.
**Relevance:** The agents.yaml configuration system and the extensible agent architecture enable agencies to codify institutional knowledge into reusable review agents, checklists, and prompts that encode best practices for future reviews.

</skill_md>

<use_cases>
## Use Cases for FDA 510(k) Review Officers

### Use Case 1: Accelerated Initial Assessment and Triage
**Scenario:** An FDA review branch receives 30-50 new 510(k) submissions per month. Branch chiefs need to quickly assess submission quality, identify straightforward vs. complex reviews, and assign submissions to appropriate reviewers based on technical expertise requirements. Traditional initial assessment requires 4-8 hours per submission of manual document review.

**Application:** Using the AI review platform for rapid triage:
1. **Intake Processing (30 minutes per submission):** Upload the 510(k) PDF to the PDF→Markdown tab, extract first 50 pages covering administrative info, device description, indications, and predicate comparison
2. **Automated Summary Generation:** Run the Summary & Entities agent to create a structured 3000-word executive summary with key entities table (indications, risks, tests, predicates)
3. **Complexity Scoring:** Review the generated entity table to count novel risks, new patient populations, significant technological differences from predicates, and missing standard tests
4. **Reviewer Assignment:** Use the entity tags (software, clinical data, statistical analysis) to match submissions with reviewers who have relevant expertise
5. **Initial Flag Identification:** The "Reviewer Comment/Considerations" column auto-generates preliminary concerns (e.g., "Limited clinical data for pediatric population," "No comparative bench testing with predicate")

**Impact:** Branch chiefs can complete initial triage in 30 minutes instead of 4+ hours, enabling same-day reviewer assignments. The Dashboard tracks triage completeness across all incoming submissions, ensuring nothing falls through the cracks. The knowledge base (Skill #30) captures common device types and triage patterns for continuous improvement.

### Use Case 2: Systematic Deficiency Review and Amendment Verification
**Scenario:** A medical device manufacturer submits a 510(k) for a Class II cardiovascular device. After initial review, FDA issues a deficiency letter with 15 specific requests for additional information covering biocompatibility testing gaps, insufficient predicate comparison data, and unclear labeling. The sponsor submits a 300-page amendment addressing the deficiencies. The reviewer must verify that all 15 items were adequately addressed before proceeding.

**Application:** Using the platform for systematic amendment review:
1. **Baseline Documentation:** The original review used the Checklist & Report tab to generate a 15-item deficiency checklist from FDA cardiovascular device guidance. Each item includes specific questions, regulatory citations (21 CFR 870.x, ISO 10993-1), and blank response fields.
2. **Amendment Upload:** Upload both the original submission PDF and the amendment PDF to the Comparator tab
3. **Delta Analysis (Skill #11):** Run the diff_agent to identify 100+ specific changes between versions, organized by document section with before/after summaries
4. **Deficiency Mapping:** Use the Note Keeper to paste the original 15 deficiency items, then run the "AI Action Items" magic to cross-reference each deficiency against the delta analysis
5. **Gap Identification:** The system highlights that Deficiency #7 (ISO 10993-5 cytotoxicity testing) shows no changes in the relevant section—likely not addressed
6. **Verification Report:** Run the review_report_agent with inputs: (a) original deficiency checklist, (b) diff analysis results, (c) reviewer notes on amendment completeness. This generates a formal memo documenting which deficiencies were resolved vs. which require follow-up.

**Impact:** Amendment review time reduces from 16-20 hours to 4-6 hours. The systematic approach ensures no deficiency items are overlooked. The audit trail (Skill #29) documents exactly what changed and when reviewer verified it, supporting defensible regulatory decisions if challenged.

### Use Case 3: Multi-Reviewer Collaboration on Complex De Novo Pathway Devices
**Scenario:** A novel AI-powered diagnostic device is submitted via the De Novo pathway (later reclassified for 510(k) review). The review requires coordination among: (1) software/cybersecurity specialist, (2) clinical reviewer/physician, (3) statistician for algorithm validation, (4) biocompatibility specialist. Each team member needs to review different sections, document findings, and contribute to the final review memo.

**Application:** Using the platform as a collaborative review workspace:
1. **Document Preparation:** Lead reviewer uploads the 800-page submission PDF and uses PDF→Markdown to extract relevant sections:
   - Pages 50-150: Software documentation → `software_section.md`
   - Pages 200-350: Clinical validation study → `clinical_section.md`
   - Pages 400-500: Biocompatibility testing → `biocomp_section.md`
   - Pages 600-700: Statistical analysis plan → `statistics_section.md`

2. **Parallel Review (Skill #28):**
   - **Software Reviewer:** Uploads `software_section.md` to Summary tab, uses custom prompt focused on IEC 62304 compliance, cybersecurity controls per FDA guidance, and algorithm transparency. Generates 4000-word software review memo with 25+ extracted entities (security risks, validation datasets, failure modes).
   - **Clinical Reviewer:** Processes `clinical_section.md` with prompts emphasizing clinical endpoints, patient selection criteria, adverse events, and benefit-risk for target population. Uses AI Magics "Concept Map" to visualize study design and primary/secondary endpoints.
   - **Statistician:** Reviews `statistics_section.md` focusing on sensitivity/specificity calculations, ROC curve analysis, sample size justification, and subgroup analyses. The Note Keeper organizes statistical concerns and recommendations.
   - **Biocompatibility Specialist:** Analyzes `biocomp_section.md` against ISO 10993 testing matrix, identifies missing endpoints for 24-hour skin contact device, generates deficiency language.

3. **Integration Phase:** Lead reviewer uses the Checklist & Report tab to:
   - Load the custom De Novo checklist (created from FDA guidance + Special Controls recommendations)
   - Paste each specialist's findings into the "Review Results" field
   - Run the report_agent to integrate all findings into a unified 8000-word review memo with sections for software, clinical, statistics, biocompatibility, and overall recommendation

4. **Consensus Building:** Team meets to discuss the AI-generated integrated memo, uses the Note Keeper to document consensus decisions on contentious issues (e.g., whether clinical data are sufficient or post-market surveillance is needed)

5. **Decision Documentation (Skill #19):** Final memo includes: (a) each reviewer's assessment, (b) areas of agreement/disagreement, (c) Special Controls recommendations, (d) post-market requirements, (e) rationale for De Novo clearance decision

**Impact:** Review coordination overhead decreases from weeks of email/meeting scheduling to days of focused parallel work. Each reviewer works in their area of expertise with AI assistance, then contributions are systematically integrated. The audit trail shows exactly who reviewed what sections with which agents/models, supporting regulatory accountability. The knowledge base captures successful multi-disciplinary review patterns for training new review teams.

</use_cases>

<follow_up_questions>
## 20 Comprehensive Follow-up Questions for FDA Review Officers

### Regulatory Process Understanding (Beginner)

1. **The code generates "3000-4000 word" summaries as default. From your experience as an FDA reviewer, is this length appropriate for different types of 510(k) submissions (e.g., Traditional vs. Abbreviated vs. Special)? How would you adjust the prompt to optimize for submission type?**

2. **The `render_510k_tab()` collects product code, K-number, sponsor, and device name. What other metadata fields should FDA reviewers capture during initial intake to improve downstream review efficiency? How would you modify the UI to collect these additional fields?**

3. **Skill #2 focuses on "Indications for Use Extraction." In your review experience, what are the most common ways sponsors attempt to expand indications beyond their predicates, and how could you modify the entity extraction prompts to automatically flag these potential issues?**

4. **The checklist agent generates review checklists from FDA guidance documents. Which specific FDA guidance documents should be prioritized for different device types (cardiovascular, orthopedic, IVD, etc.), and how would you organize a library of guidance-to-checklist mappings?**

5. **Explain how the "substantial equivalence reasoning documentation" (Skill #9) generated by this system would be used in actual FDA decision-making. What regulatory or legal requirements govern how substantial equivalence determinations must be documented?**

### Practical Application and Workflow Integration (Intermediate)

6. **The Comparator tab identifies "100 meaningful differences" between document versions. In practice, when reviewing a sponsor's amendment to a deficiency letter, how do you differentiate between (a) meaningful changes that address deficiencies, (b) cosmetic changes that don't address issues, and (c) new changes that introduce additional concerns? How would you train the AI agent to make these distinctions?**

7. **Skill #15 describes "Benefit-Risk Assessment Documentation." FDA's benefit-risk framework considers multiple dimensions (analysis of condition, current treatment options, benefit evidence, risk evidence, risk management). How would you modify the agent prompts to ensure all framework dimensions are systematically addressed in generated review memos?**

8. **The application tracks "tokens processed" in the dashboard. From a regulatory efficiency perspective, how would you translate token usage into meaningful productivity metrics for FDA management (e.g., hours saved, submissions processed, deficiency cycles reduced)? What baseline data would you need to collect?**

9. **Skill #17 addresses "Cross-Reference Verification." In complex submissions with 50+ appendices and hundreds of internal cross-references, what specific verification checks are most critical to perform? How would you design an agent specifically to validate that summary claims are supported by detailed test reports in appendices?**

10. **The multi-LLM architecture allows selecting different models for different tasks. Based on your review experience, which review tasks would benefit most from more powerful (expensive) models like GPT-4 or Claude Sonnet, and which tasks could use faster (cheaper) models like GPT-4o-mini? How would you optimize the cost-accuracy tradeoff?**

### Regulatory Compliance and Risk Management (Intermediate-Advanced)

11. **Skill #6 describes "Risk Management File Evaluation Framework" based on ISO 14971. FDA expects risk analysis to cover use errors, cybersecurity threats, and electromagnetic compatibility in addition to traditional hazards. How would you modify the entity extraction to ensure all risk categories required by FDA guidance are captured and evaluated?**

12. **The code includes a "magic" for generating glossaries. In 510(k) review, inconsistent terminology across submission sections often indicates quality issues or copy-paste errors. How would you design an agent that identifies terminology inconsistencies (e.g., "catheter" vs. "delivery system" referring to same component) and flags them as potential submission quality concerns?**

13. **Skill #22 addresses "Special Controls Evaluation." Special controls can include device-specific performance standards, post-market surveillance, or specific labeling. When reviewing a potentially novel device, how would you program an agent to recommend appropriate special controls based on identified risks that aren't adequately mitigated by general controls?**

14. **The application logs all reviewer activities with timestamps for audit trails (Skill #29). Under 21 CFR Part 11 (electronic records), what additional metadata, validation, or security controls would be required to make this system's outputs acceptable as official FDA review documentation? What changes would you need to implement?**

15. **Skill #12 describes "FDA Guidance Alignment Verification." Some FDA guidance documents are decades old and may not reflect current technological approaches. When an AI agent identifies that a submission doesn't follow old guidance because it uses newer, arguably better methods, how should the agent flag this for reviewer judgment rather than automatically calling it a deficiency?**

### Advanced Integration and System Design (Advanced)

16. **The current system processes one submission at a time. Design a queue-based architecture where multiple reviewers can work on different submissions simultaneously, with workload balancing, priority handling for high-risk devices, and management dashboards showing branch-wide review status. What technical components and data structures would you need?**

17. **Skill #27 describes "Regulatory Precedent Search." FDA has decades of 510(k) clearance decisions, warning letters, and recall data. How would you integrate this system with FDA's internal databases (e.g., MAUDE for adverse events, 510(k) database for clearance history) to automatically pull relevant precedent data during review? What API or data warehouse architecture would be required?**

18. **The application uses YAML files for agent configuration (Skill #30 - Knowledge Base Development). Propose a governance model for how FDA would maintain, version control, and update these agent configurations as regulatory science evolves, new guidance is published, and reviewers learn from experience. Who should have authority to modify agent prompts?**

19. **Skill #28 addresses multi-reviewer collaboration. Design a feature where multiple reviewers can independently review the same submission section using different AI agents, and the system automatically identifies where reviewers agree vs. disagree, highlighting items requiring team discussion. What consensus algorithms or voting mechanisms would you implement?**

20. **The system generates review memos that integrate checklist results with reviewer findings. In actual FDA practice, review memos undergo supervisory review, branch chief approval, and potential ODE/CDRH senior leadership review. Design a review approval workflow system that tracks document versions, approval status, reviewer/supervisor comments, and revision history while maintaining complete audit trails for each approval level. How would you implement this within the Streamlit architecture?**

</follow_up_questions>
