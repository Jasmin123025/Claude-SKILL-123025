<scratchpad>
This is a comprehensive request to create:
1. A technical specification for an FDA Agentic AI Review platform
2. Deployment architecture for Hugging Face Spaces with Streamlit
3. Complete agents.yaml configuration
4. Enhanced SKILL.md with advanced FDA review skills
5. 20 follow-up questions
I need to design:

System architecture for Hugging Face deployment
File upload/paste workflows for 510(k) materials
Skill selection interface
Agent orchestration system
Review report generation
Data persistence
Security considerations
Advanced FDA-specific skills (beyond the previous 30)

Let me structure this comprehensively:
Architecture Components:

Frontend: Streamlit UI with upload/paste interfaces
Backend: Agent orchestration engine
Storage: Session state + optional persistent storage
LLM Integration: Multi-provider support
Document Processing: PDF/text extraction
Review Workflow: Multi-stage pipeline
Report Generation: Template-based output

Advanced Skills to Add:

Comparative effectiveness analysis
Manufacturing process validation review
Software verification and validation assessment
Clinical endpoint adjudication
Real-world evidence integration
Post-market surveillance design
Human factors engineering evaluation
Electromagnetic compatibility assessment
Packaging and shelf-life validation
Reprocessing/sterilization validation
Combination product assessment
Pediatric considerations evaluation
Health equity analysis
Cybersecurity threat modeling
Interoperability assessment
Artificial intelligence/machine learning validation
3D printing/additive manufacturing review
Nanotechnology safety assessment
Patient preference information integration
Environmental assessment screening
</scratchpad>


FDA Agentic AI Review Platform - Comprehensive Technical Specification
Executive Summary
This document specifies a cloud-deployed FDA 510(k) Agentic AI Review Platform that enables FDA officers to upload submission materials, leverage AI-powered review agents, and generate comprehensive review reports. The platform will be deployed on Hugging Face Spaces using Streamlit, with a modular agent architecture defined in agents.yaml.

Table of Contents

System Architecture
Deployment Specification
User Workflows
Technical Components
agents.yaml Configuration
Enhanced SKILL.md
Security and Compliance
Implementation Roadmap
Follow-up Questions


1. System Architecture
1.1 High-Level Architecture
Copy┌─────────────────────────────────────────────────────────────┐
│                    Hugging Face Space                        │
│  ┌───────────────────────────────────────────────────────┐  │
│  │              Streamlit Frontend                        │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐    │  │
│  │  │ Upload   │  │ Skill    │  │ Review Report    │    │  │
│  │  │ Manager  │  │ Selector │  │ Generator        │    │  │
│  │  └──────────┘  └──────────┘  └──────────────────┘    │  │
│  └────────────────────┬──────────────────────────────────┘  │
│                       │                                      │
│  ┌────────────────────▼──────────────────────────────────┐  │
│  │          Agent Orchestration Engine                   │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │  │
│  │  │ Document    │  │ Skill       │  │ Context     │  │  │
│  │  │ Processor   │  │ Executor    │  │ Manager     │  │  │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │  │
│  └────────────────────┬──────────────────────────────────┘  │
│                       │                                      │
│  ┌────────────────────▼──────────────────────────────────┐  │
│  │           Data & State Management                     │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │  │
│  │  │ Session     │  │ File        │  │ Review      │  │  │
│  │  │ State       │  │ Storage     │  │ Cache       │  │  │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │  │
│  └────────────────────┬──────────────────────────────────┘  │
│                       │                                      │
│  ┌────────────────────▼──────────────────────────────────┐  │
│  │              LLM Provider Layer                       │  │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐ │  │
│  │  │ OpenAI  │  │ Anthropic│  │ Gemini  │  │  Grok   │ │  │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘ │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              External FDA Systems (Future)                   │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │ 510(k) DB   │  │ MAUDE       │  │ Guidance Library    │ │
│  └─────────────┘  └─────────────┘  └─────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
1.2 Component Descriptions
Frontend Layer (Streamlit)

Upload Manager: Multi-file upload interface for PDFs, Word docs, text files
Paste Interface: Direct text/markdown pasting for quick analysis
Skill Selector: Dynamic UI for selecting and chaining review skills
Review Dashboard: Real-time progress tracking and results visualization
Report Generator: Template-based review memo generation

Agent Orchestration Engine

Document Processor: Extracts text, tables, images from various formats
Skill Executor: Runs selected skills in sequence or parallel
Context Manager: Maintains review context across multiple agent invocations
Result Aggregator: Combines outputs from multiple skills

Data & State Management

Session State: Maintains user session data during active review
File Storage: Temporary storage for uploaded documents (auto-cleanup)
Review Cache: Caches intermediate results for performance

LLM Provider Layer

Multi-provider support with fallback mechanisms
Token usage tracking and optimization
Rate limiting and error handling


2. Deployment Specification
2.1 Hugging Face Space Configuration
File Structure:
Copyfda-agentic-review/
├── app.py                          # Main Streamlit application
├── requirements.txt                # Python dependencies
├── packages.txt                    # System dependencies (poppler, etc.)
├── .streamlit/
│   └── config.toml                # Streamlit configuration
├── agents.yaml                     # Agent definitions
├── config/
│   ├── settings.yaml              # Application settings
│   ├── fda_guidance_library.yaml  # FDA guidance documents mapping
│   └── review_templates.yaml      # Review report templates
├── src/
│   ├── __init__.py
│   ├── agents/
│   │   ├── __init__.py
│   │   ├── orchestrator.py        # Agent orchestration logic
│   │   ├── executor.py            # Individual agent execution
│   │   └── skill_registry.py      # Skill registration and management
│   ├── document_processing/
│   │   ├── __init__.py
│   │   ├── pdf_extractor.py       # PDF text/table extraction
│   │   ├── text_processor.py      # Text cleaning and preprocessing
│   │   └── table_parser.py        # Table structure parsing
│   ├── llm/
│   │   ├── __init__.py
│   │   ├── provider_manager.py    # LLM provider routing
│   │   ├── prompt_templates.py    # Reusable prompt templates
│   │   └── token_optimizer.py     # Token usage optimization
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── upload_interface.py    # File upload components
│   │   ├── skill_selector.py      # Skill selection UI
│   │   ├── progress_tracker.py    # Review progress visualization
│   │   └── report_viewer.py       # Report display and export
│   ├── storage/
│   │   ├── __init__.py
│   │   ├── session_manager.py     # Session state management
│   │   └── file_handler.py        # File upload/storage handling
│   └── utils/
│       ├── __init__.py
│       ├── validators.py          # Input validation
│       ├── formatters.py          # Output formatting
│       └── logger.py              # Logging utilities
├── templates/
│   ├── review_memo.md             # Review memo template
│   ├── deficiency_letter.md       # Deficiency letter template
│   └── summary_report.md          # Summary report template
├── tests/
│   ├── test_agents.py
│   ├── test_document_processing.py
│   └── test_llm_integration.py
├── docs/
│   ├── USER_GUIDE.md
│   ├── ADMIN_GUIDE.md
│   └── API_DOCUMENTATION.md
├── SKILL.md                        # Skills documentation
├── README.md                       # Project overview
└── LICENSE                         # License information
2.2 requirements.txt
txtCopy# Core framework
streamlit==1.31.0
python-dotenv==1.0.0

# Document processing
pypdf==4.0.1
python-docx==1.1.0
pdfplumber==0.10.3
pytesseract==0.3.10
pillow==10.2.0
camelot-py[cv]==0.11.0

# LLM providers
openai==1.12.0
anthropic==0.18.1
google-generativeai==0.3.2
httpx==0.26.0

# Data processing
pandas==2.2.0
numpy==1.26.3
pyyaml==6.0.1

# Visualization
altair==5.2.0
plotly==5.18.0

# Text processing
nltk==3.8.1
spacy==3.7.2
markdown==3.5.2
beautifulsoup4==4.12.3

# Utilities
tqdm==4.66.1
python-dateutil==2.8.2
tenacity==8.2.3

# Testing
pytest==8.0.0
pytest-cov==4.1.0

# Security
cryptography==42.0.2
2.3 packages.txt
txtCopypoppler-utils
tesseract-ocr
ghostscript
2.4 .streamlit/config.toml
tomlCopy[server]
maxUploadSize = 500
enableXsrfProtection = true
enableCORS = false

[browser]
gatherUsageStats = false

[theme]
primaryColor = "#0066CC"
backgroundColor = "#FFFFFF"
secondaryBackgroundColor = "#F0F2F6"
textColor = "#262730"
font = "sans serif"

[runner]
magicEnabled = true
fastReruns = true
2.5 Environment Variables (Hugging Face Secrets)
bashCopy# LLM API Keys
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
GEMINI_API_KEY=AIza...
GROK_API_KEY=xai-...

# Application Configuration
FDA_ADMIN_PASSWORD=<secure_password>
ENABLE_AUDIT_LOGGING=true
MAX_FILE_SIZE_MB=500
SESSION_TIMEOUT_MINUTES=120

# Optional: External Database
DATABASE_URL=postgresql://...
REDIS_URL=redis://...

3. User Workflows
3.1 Primary Workflow: Complete 510(k) Review
mermaidCopygraph TD
    A[FDA Officer Login] --> B[Create New Review Session]
    B --> C[Upload Submission Materials]
    C --> D{Material Type?}
    D -->|Device Description| E[Parse Device Info]
    D -->|Technical Files| F[Extract Technical Data]
    D -->|Test Reports| G[Process Test Results]
    E --> H[Review Dashboard]
    F --> H
    G --> H
    H --> I[Select Review Skills]
    I --> J{Skill Type?}
    J -->|Predicate Analysis| K[Run Skill #1]
    J -->|Risk Assessment| L[Run Skill #6]
    J -->|Testing Evaluation| M[Run Skill #4]
    K --> N[Aggregate Results]
    L --> N
    M --> N
    N --> O[Generate Review Report]
    O --> P{Report Complete?}
    P -->|No| Q[Select Additional Skills]
    Q --> I
    P -->|Yes| R[Export Final Report]
    R --> S[Close Review Session]
3.2 Workflow Details
Step 1: Session Initialization
pythonCopy# FDA officer creates new review session
session_id = create_review_session(
    k_number="K241234",
    device_name="CardioStent Pro",
    reviewer_id="FDA-12345",
    submission_date="2024-01-15"
)
Step 2: Material Upload

Upload Options:

Drag-and-drop multiple PDFs (device description, test reports, clinical data)
Paste text directly (for email correspondence, notes)
Import from URL (for public guidance documents)


Automatic Processing:

PDF text extraction with page numbers
Table detection and structured parsing
Image extraction for diagrams/charts
Metadata extraction (dates, authors, document types)



Step 3: Skill Selection Interface
pythonCopy# UI presents categorized skills
skill_categories = {
    "Initial Assessment": [
        "Skill #1: Predicate Device Analysis",
        "Skill #2: Indications Extraction",
        "Skill #26: Device Classification Verification"
    ],
    "Technical Review": [
        "Skill #4: Performance Testing Assessment",
        "Skill #5: Biocompatibility Gap Analysis",
        "Skill #31: Software V&V Assessment"
    ],
    "Risk & Safety": [
        "Skill #6: Risk Management Evaluation",
        "Skill #34: Cybersecurity Threat Modeling",
        "Skill #37: EMC Assessment"
    ],
    "Clinical & Regulatory": [
        "Skill #7: Clinical Data Synthesis",
        "Skill #9: Substantial Equivalence Documentation",
        "Skill #15: Benefit-Risk Assessment"
    ]
}
Step 4: Agent Execution

Sequential Execution: Skills run in order, each using previous results
Parallel Execution: Independent skills run simultaneously for speed
Interactive Mode: Officer reviews each skill output before proceeding

Step 5: Report Generation

Select report template (review memo, deficiency letter, clearance summary)
System aggregates all skill outputs into structured report
Officer edits/annotates report sections
Export to PDF, Word, or markdown


4. Technical Components
4.1 Upload Manager (src/ui/upload_interface.py)
pythonCopyimport streamlit as st
from typing import List, Dict, Optional
import mimetypes
from pathlib import Path

class UploadManager:
    """Manages document upload and parsing for FDA review sessions."""
    
    SUPPORTED_FORMATS = {
        'application/pdf': 'PDF',
        'application/vnd.openxmlformats-officedocument.wordprocessingml.document': 'Word',
        'text/plain': 'Text',
        'text/markdown': 'Markdown'
    }
    
    MAX_FILE_SIZE = 500 * 1024 * 1024  # 500 MB
    
    def __init__(self, session_id: str):
        self.session_id = session_id
        self.uploaded_files: Dict[str, Dict] = {}
        
    def render_upload_interface(self) -> None:
        """Render the file upload UI with categorization."""
        st.subheader("📁 Upload 510(k) Submission Materials")
        
        # Create tabs for different material types
        tab1, tab2, tab3, tab4 = st.tabs([
            "📋 Device Description",
            "🔬 Technical Files",
            "📊 Test Reports",
            "📝 Paste Text"
        ])
        
        with tab1:
            self._render_category_upload(
                "device_description",
                "Upload device description documents",
                ["Summary document", "Indications for Use", "Device diagram"]
            )
        
        with tab2:
            self._render_category_upload(
                "technical_files",
                "Upload technical documentation",
                ["Design specifications", "Materials list", "Manufacturing process"]
            )
        
        with tab3:
            self._render_category_upload(
                "test_reports",
                "Upload performance test reports",
                ["Bench testing", "Biocompatibility", "Clinical studies"]
            )
        
        with tab4:
            self._render_paste_interface()
    
    def _render_category_upload(
        self, 
        category: str, 
        description: str,
        expected_docs: List[str]
    ) -> None:
        """Render upload interface for a specific document category."""
        st.markdown(f"**{description}**")
        
        # Show expected documents
        with st.expander("📌 Expected documents"):
            for doc in expected_docs:
                st.markdown(f"- {doc}")
        
        # File uploader
        files = st.file_uploader(
            f"Upload files for {category}",
            type=['pdf', 'docx', 'txt', 'md'],
            accept_multiple_files=True,
            key=f"upload_{category}"
        )
        
        if files:
            self._process_uploads(files, category)
    
    def _process_uploads(
        self, 
        files: List, 
        category: str
    ) -> None:
        """Process uploaded files and extract content."""
        from src.document_processing.pdf_extractor import PDFExtractor
        from src.document_processing.text_processor import TextProcessor
        
        extractor = PDFExtractor()
        processor = TextProcessor()
        
        for file in files:
            # Validate file
            if file.size > self.MAX_FILE_SIZE:
                st.error(f"❌ {file.name} exceeds {self.MAX_FILE_SIZE / 1024 / 1024}MB limit")
                continue
            
            # Process based on type
            file_type = mimetypes.guess_type(file.name)[0]
            
            if file_type == 'application/pdf':
                content = extractor.extract_text_with_metadata(file)
                tables = extractor.extract_tables(file)
            elif file_type == 'text/plain':
                content = file.read().decode('utf-8')
                tables = []
            else:
                st.warning(f"⚠️ {file.name} format not fully supported")
                content = file.read().decode('utf-8', errors='ignore')
                tables = []
            
            # Store processed content
            file_id = f"{category}_{len(self.uploaded_files)}"
            self.uploaded_files[file_id] = {
                'name': file.name,
                'category': category,
                'type': file_type,
                'size': file.size,
                'content': content,
                'tables': tables,
                'metadata': {
                    'page_count': content.count('\n\n---PAGE') if 'PAGE' in content else None
                }
            }
            
            # Save to session state
            if 'uploaded_documents' not in st.session_state:
                st.session_state['uploaded_documents'] = {}
            st.session_state['uploaded_documents'][file_id] = self.uploaded_files[file_id]
            
            # Display success
            st.success(f"✅ Processed: {file.name} ({file.size / 1024:.1f} KB)")
            
            # Show preview
            with st.expander(f"Preview: {file.name}"):
                st.markdown(content[:2000] + "..." if len(content) > 2000 else content)
                if tables:
                    st.markdown(f"**Found {len(tables)} tables**")
    
    def _render_paste_interface(self) -> None:
        """Render text paste interface for quick input."""
        st.markdown("**Paste text content directly**")
        
        text_input = st.text_area(
            "Paste submission text, correspondence, or notes",
            height=300,
            key="paste_text_input"
        )
        
        col1, col2 = st.columns([3, 1])
        with col1:
            doc_name = st.text_input("Document name", value="Pasted Text")
        with col2:
            doc_category = st.selectbox(
                "Category",
                ["device_description", "technical_files", "test_reports", "notes"]
            )
        
        if st.button("💾 Save Pasted Text") and text_input:
            file_id = f"pasted_{len(self.uploaded_files)}"
            self.uploaded_files[file_id] = {
                'name': doc_name,
                'category': doc_category,
                'type': 'text/plain',
                'size': len(text_input),
                'content': text_input,
                'tables': [],
                'metadata': {'source': 'paste'}
            }
            
            if 'uploaded_documents' not in st.session_state:
                st.session_state['uploaded_documents'] = {}
            st.session_state['uploaded_documents'][file_id] = self.uploaded_files[file_id]
            
            st.success(f"✅ Saved: {doc_name}")
4.2 Skill Selector (src/ui/skill_selector.py)
pythonCopyimport streamlit as st
from typing import List, Dict, Set, Optional
import yaml

class SkillSelector:
    """Interactive skill selection and sequencing interface."""
    
    def __init__(self, agents_config_path: str = "agents.yaml"):
        with open(agents_config_path, 'r') as f:
            self.agents_config = yaml.safe_load(f)
        
        self.available_skills = self._load_skills()
        self.selected_skills: List[str] = []
        self.skill_sequence: List[Dict] = []
    
    def _load_skills(self) -> Dict[str, Dict]:
        """Load all available skills from agents.yaml."""
        skills = {}
        for agent_id, agent_config in self.agents_config['agents'].items():
            skill_id = agent_config.get('skill_number')
            if skill_id:
                skills[skill_id] = {
                    'agent_id': agent_id,
                    'name': agent_config.get('name'),
                    'description': agent_config.get('description'),
                    'category': agent_config.get('category'),
                    'difficulty': agent_config.get('difficulty', 'medium'),
                    'dependencies': agent_config.get('dependencies', []),
                    'estimated_tokens': agent_config.get('estimated_tokens', 5000),
                    'recommended_model': agent_config.get('default_model')
                }
        return skills
    
    def render_skill_selector(self) -> None:
        """Render the skill selection interface."""
        st.subheader("🎯 Select Review Skills")
        
        # Display uploaded documents summary
        self._render_document_summary()
        
        # Skill selection modes
        mode = st.radio(
            "Selection Mode",
            ["🎓 Guided (Recommended)", "🔧 Advanced (Custom)", "⚡ Quick Templates"],
            horizontal=True
        )
        
        if mode == "🎓 Guided (Recommended)":
            self._render_guided_selection()
        elif mode == "🔧 Advanced (Custom)":
            self._render_advanced_selection()
        else:
            self._render_template_selection()
        
        # Display selected skills
        self._render_selected_skills()
    
    def _render_document_summary(self) -> None:
        """Show summary of uploaded documents."""
        docs = st.session_state.get('uploaded_documents', {})
        if not docs:
            st.warning("⚠️ No documents uploaded yet. Please upload submission materials first.")
            return
        
        with st.expander(f"📚 Uploaded Documents ({len(docs)} files)"):
            for file_id, doc in docs.items():
                st.markdown(
                    f"- **{doc['name']}** ({doc['category']}) - "
                    f"{doc['size'] / 1024:.1f} KB"
                )
    
    def _render_guided_selection(self) -> None:
        """Guided skill selection based on review stage."""
        st.markdown("**Select your current review stage:**")
        
        stage = st.selectbox(
            "Review Stage",
            [
                "1️⃣ Initial Screening & Triage",
                "2️⃣ Technical Assessment",
                "3️⃣ Risk & Safety Evaluation",
                "4️⃣ Clinical & Performance Review",
                "5️⃣ Deficiency Identification",
                "6️⃣ Final Report Generation"
            ]
        )
        
        # Get recommended skills for stage
        recommended = self._get_recommended_skills_for_stage(stage)
        
        st.markdown("**Recommended skills for this stage:**")
        
        for skill_id in recommended:
            skill = self.available_skills[skill_id]
            
            col1, col2, col3 = st.columns([4, 1, 1])
            
            with col1:
                st.markdown(
                    f"**Skill #{skill_id}: {skill['name']}**\n\n"
                    f"{skill['description']}"
                )
            
            with col2:
                st.caption(f"~{skill['estimated_tokens']} tokens")
            
            with col3:
                if st.button("Add", key=f"add_skill_{skill_id}"):
                    self._add_skill_to_sequence(skill_id)
    
    def _render_advanced_selection(self) -> None:
        """Advanced skill selection with filtering and dependencies."""
        # Category filter
        categories = list(set(s['category'] for s in self.available_skills.values()))
        selected_categories = st.multiselect(
            "Filter by category",
            categories,
            default=categories
        )
        
        # Difficulty filter
        difficulty = st.radio(
            "Show skills",
            ["All", "Beginner", "Intermediate", "Advanced"],
            horizontal=True
        )
        
        # Search
        search = st.text_input("🔍 Search skills", "")
        
        # Filter skills
        filtered_skills = self._filter_skills(
            selected_categories,
            difficulty,
            search
        )
        
        # Display filtered skills in expandable sections
        for category in selected_categories:
            category_skills = [
                s_id for s_id, s in filtered_skills.items() 
                if s['category'] == category
            ]
            
            if category_skills:
                with st.expander(f"**{category}** ({len(category_skills)} skills)"):
                    for skill_id in sorted(category_skills):
                        self._render_skill_card(skill_id)
    
    def _render_template_selection(self) -> None:
        """Quick template selection for common review scenarios."""
        st.markdown("**Select a review template:**")
        
        templates = {
            "Standard Class II Device": [1, 2, 3, 4, 5, 6, 9, 15],
            "Software/AI-Enabled Device": [1, 2, 31, 34, 35, 46],
            "High-Risk Implantable Device": [1, 2, 4, 5, 6, 7, 33, 36],
            "IVD/Diagnostic Device": [1, 2, 4, 14, 43],
            "Combination Product": [1, 2, 4, 5, 41, 42]
        }
        
        selected_template = st.selectbox(
            "Template",
            list(templates.keys())
        )
        
        if st.button("📋 Load Template Skills"):
            st.session_state['skill_sequence'] = []
            for skill_id in templates[selected_template]:
                self._add_skill_to_sequence(skill_id)
            st.success(f"✅ Loaded {len(templates[selected_template])} skills")
            st.rerun()
    
    def _render_skill_card(self, skill_id: int) -> None:
        """Render individual skill card with details."""
        skill = self.available_skills[skill_id]
        
        col1, col2 = st.columns([5, 1])
        
        with col1:
            st.markdown(f"**Skill #{skill_id}: {skill['name']}**")
            st.caption(skill['description'])
            
            # Show dependencies
            if skill['dependencies']:
                deps = ", ".join([f"#{d}" for d in skill['dependencies']])
                st.caption(f"⚠️ Requires: {deps}")
        
        with col2:
            if st.button("➕", key=f"add_{skill_id}"):
                self._add_skill_to_sequence(skill_id)
    
    def _render_selected_skills(self) -> None:
        """Display and manage selected skill sequence."""
        sequence = st.session_state.get('skill_sequence', [])
        
        if not sequence:
            st.info("No skills selected yet. Select skills above to build your review workflow.")
            return
        
        st.markdown("---")
        st.subheader(f"📋 Selected Skills ({len(sequence)})")
        
        # Execution options
        col1, col2, col3 = st.columns([2, 2, 1])
        
        with col1:
            execution_mode = st.radio(
                "Execution",
                ["Sequential", "Parallel (where possible)"],
                horizontal=True
            )
        
        with col2:
            total_tokens = sum(
                self.available_skills[s['skill_id']]['estimated_tokens'] 
                for s in sequence
            )
            st.metric("Estimated Tokens", f"{total_tokens:,}")
        
        with col3:
            if st.button("🗑️ Clear All"):
                st.session_state['skill_sequence'] = []
                st.rerun()
        
        # Display sequence with reordering
        for idx, skill_item in enumerate(sequence):
            skill_id = skill_item['skill_id']
            skill = self.available_skills[skill_id]
            
            col1, col2, col3, col4 = st.columns([1, 5, 1, 1])
            
            with col1:
                st.markdown(f"**{idx + 1}.**")
            
            with col2:
                st.markdown(f"**Skill #{skill_id}: {skill['name']}**")
            
            with col3:
                if idx > 0 and st.button("⬆️", key=f"up_{idx}"):
                    sequence[idx], sequence[idx-1] = sequence[idx-1], sequence[idx]
                    st.session_state['skill_sequence'] = sequence
                    st.rerun()
            
            with col4:
                if st.button("❌", key=f"remove_{idx}"):
                    sequence.pop(idx)
                    st.session_state['skill_sequence'] = sequence
                    st.rerun()
        
        # Execute button
        st.markdown("---")
        if st.button("▶️ Execute Selected Skills", type="primary"):
            self._execute_skill_sequence(execution_mode)
    
    def _add_skill_to_sequence(self, skill_id: int) -> None:
        """Add skill to execution sequence with dependency check."""
        skill = self.available_skills[skill_id]
        
        # Check dependencies
        if skill['dependencies']:
            current_skill_ids = [
                s['skill_id'] for s in st.session_state.get('skill_sequence', [])
            ]
            missing_deps = [
                d for d in skill['dependencies'] 
                if d not in current_skill_ids
            ]
            
            if missing_deps:
                st.warning(
                    f"⚠️ Skill #{skill_id} requires skills: "
                    f"{', '.join([f'#{d}' for d in missing_deps])}. "
                    f"Add dependencies first."
                )
                return
        
        # Add to sequence
        if 'skill_sequence' not in st.session_state:
            st.session_state['skill_sequence'] = []
        
        st.session_state['skill_sequence'].append({
            'skill_id': skill_id,
            'agent_id': skill['agent_id'],
            'name': skill['name'],
            'model': skill['recommended_model']
        })
        
        st.success(f"✅ Added Skill #{skill_id}")
    
    def _get_recommended_skills_for_stage(self, stage: str) -> List[int]:
        """Get recommended skills for a review stage."""
        stage_mapping = {
            "1️⃣ Initial Screening & Triage": [1, 2, 26, 27],
            "2️⃣ Technical Assessment": [3, 4, 24, 25],
            "3️⃣ Risk & Safety Evaluation": [5, 6, 11, 34],
            "4️⃣ Clinical & Performance Review": [7, 8, 14, 15],
            "5️⃣ Deficiency Identification": [10, 17, 23],
            "6️⃣ Final Report Generation": [9, 19, 29]
        }
        return stage_mapping.get(stage, [])
    
    def _filter_skills(
        self, 
        categories: List[str], 
        difficulty: str,
        search: str
    ) -> Dict[int, Dict]:
        """Filter skills based on criteria."""
        filtered = {}
        
        for skill_id, skill in self.available_skills.items():
            # Category filter
            if skill['category'] not in categories:
                continue
            
            # Difficulty filter
            if difficulty != "All" and skill['difficulty'].title() != difficulty:
                continue
            
            # Search filter
            if search and search.lower() not in skill['name'].lower():
                continue
            
            filtered[skill_id] = skill
        
        return filtered
    
    def _execute_skill_sequence(self, execution_mode: str) -> None:
        """Execute the selected skill sequence."""
        from src.agents.orchestrator import AgentOrchestrator
        
        orchestrator = AgentOrchestrator()
        
        st.session_state['execution_mode'] = execution_mode
        st.session_state['execution_started'] = True
        
        # Trigger rerun to show execution interface
        st.rerun()
4.3 Agent Orchestrator (src/agents/orchestrator.py)
pythonCopyimport asyncio
from typing import List, Dict, Optional, Any
from concurrent.futures import ThreadPoolExecutor
import streamlit as st
from src.agents.executor import AgentExecutor
from src.llm.provider_manager import LLMProviderManager

class AgentOrchestrator:
    """Orchestrates execution of multiple agents in sequence or parallel."""
    
    def __init__(self):
        self.executor = AgentExecutor()
        self.llm_manager = LLMProviderManager()
        self.execution_results: Dict[int, Dict] = {}
    
    def execute_sequence(
        self, 
        skill_sequence: List[Dict],
        execution_mode: str = "sequential"
    ) -> Dict[str, Any]:
        """Execute a sequence of skills."""
        
        if execution_mode == "sequential":
            return self._execute_sequential(skill_sequence)
        else:
            return self._execute_parallel(skill_sequence)
    
    def _execute_sequential(self, skill_sequence: List[Dict]) -> Dict[str, Any]:
        """Execute skills one at a time, passing results forward."""
        
        # Get uploaded documents
        documents = st.session_state.get('uploaded_documents', {})
        
        # Initialize context with all document content
        context = self._build_initial_context(documents)
        
        # Progress tracking
        progress_bar = st.progress(0)
        status_text = st.empty()
        
        results = {}
        
        for idx, skill_item in enumerate(skill_sequence):
            skill_id = skill_item['skill_id']
            agent_id = skill_item['agent_id']
            
            # Update progress
            progress = (idx + 1) / len(skill_sequence)
            progress_bar.progress(progress)
            status_text.markdown(
                f"**Executing: Skill #{skill_id} - {skill_item['name']}** "
                f"({idx + 1}/{len(skill_sequence)})"
            )
            
            # Create expandable section for this skill
            with st.expander(f"Skill #{skill_id}: {skill_item['name']}", expanded=True):
                # Execute skill
                result = self.executor.execute_agent(
                    agent_id=agent_id,
                    context=context,
                    model=skill_item.get('model'),
                    skill_id=skill_id
                )
                
                # Store result
                results[skill_id] = result
                self.execution_results[skill_id] = result
                
                # Update context with this result
                context['previous_results'][skill_id] = result['output']
                
                # Display result
                self._display_result(skill_id, result)
        
        progress_bar.progress(1.0)
        status_text.markdown("✅ **All skills executed successfully!**")
        
        return {
            'execution_mode': 'sequential',
            'total_skills': len(skill_sequence),
            'results': results,
            'final_context': context
        }
    
    def _execute_parallel(self, skill_sequence: List[Dict]) -> Dict[str, Any]:
        """Execute independent skills in parallel."""
        
        # Analyze dependencies to group skills
        dependency_groups = self._group_by_dependencies(skill_sequence)
        
        documents = st.session_state.get('uploaded_documents', {})
        context = self._build_initial_context(documents)
        
        results = {}
        
        # Execute each group sequentially, but skills within group in parallel
        for group_idx, group in enumerate(dependency_groups):
            st.markdown(f"### Execution Group {group_idx + 1}")
            
            # Execute group in parallel
            with ThreadPoolExecutor(max_workers=len(group)) as executor:
                futures = []
                
                for skill_item in group:
                    future = executor.submit(
                        self.executor.execute_agent,
                        agent_id=skill_item['agent_id'],
                        context=context.copy(),
                        model=skill_item.get('model'),
                        skill_id=skill_item['skill_id']
                    )
                    futures.append((skill_item['skill_id'], future))
                
                # Collect results
                for skill_id, future in futures:
                    result = future.result()
                    results[skill_id] = result
                    self.execution_results[skill_id] = result
                    
                    # Update context
                    context['previous_results'][skill_id] = result['output']
                    
                    # Display result
                    with st.expander(f"Skill #{skill_id}", expanded=False):
                        self._display_result(skill_id, result)
        
        return {
            'execution_mode': 'parallel',
            'total_skills': len(skill_sequence),
            'dependency_groups': len(dependency_groups),
            'results': results,
            'final_context': context
        }
    
    def _build_initial_context(self, documents: Dict) -> Dict[str, Any]:
        """Build initial context from uploaded documents."""
        
        # Organize documents by category
        categorized_docs = {
            'device_description': [],
            'technical_files': [],
            'test_reports': [],
            'notes': []
        }
        
        for doc_id, doc in documents.items():
            category = doc.get('category', 'notes')
            categorized_docs[category].append({
                'name': doc['name'],
                'content': doc['content'],
                'tables': doc.get('tables', []),
                'metadata': doc.get('metadata', {})
            })
        
        # Extract key metadata if available
        metadata = {
            'k_number': st.session_state.get('k_number', 'Unknown'),
            'device_name': st.session_state.get('device_name', 'Unknown'),
            'reviewer_id': st.session_state.get('reviewer_id', 'Unknown'),
            'submission_date': st.session_state.get('submission_date', 'Unknown')
        }
        
        return {
            'documents': categorized_docs,
            'metadata': metadata,
            'previous_results': {},
            'session_id': st.session_state.get('session_id')
        }
    
    def _group_by_dependencies(
        self, 
        skill_sequence: List[Dict]
    ) -> List[List[Dict]]:
        """Group skills into execution groups based on dependencies."""
        # Simple grouping: skills without dependencies in first group,
        # then subsequent groups for skills that depend on previous groups
        
        groups = []
        remaining = skill_sequence.copy()
        completed_skill_ids = set()
        
        while remaining:
            current_group = []
            
            for skill_item in remaining[:]:
                skill_id = skill_item['skill_id']
                dependencies = self.executor.get_skill_dependencies(skill_id)
                
                # Check if all dependencies are completed
                if all(dep in completed_skill_ids for dep in dependencies):
                    current_group.append(skill_item)
                    remaining.remove(skill_item)
                    completed_skill_ids.add(skill_id)
            
            if current_group:
                groups.append(current_group)
            else:
                # Circular dependency or error - add remaining to last group
                groups.append(remaining)
                break
        
        return groups
    
    def _display_result(self, skill_id: int, result: Dict) -> None:
        """Display execution result for a skill."""
        
        # Status indicator
        status = result.get('status', 'unknown')
        status_emoji = {
            'success': '✅',
            'error': '❌',
            'warning': '⚠️'
        }.get(status, '❓')
        
        st.markdown(f"{status_emoji} **Status:** {status}")
        
        # Execution details
        col1, col2, col3 = st.columns(3)
        with col1:
            st.metric("Tokens Used", f"{result.get('tokens_used', 0):,}")
        with col2:
            st.metric("Duration", f"{result.get('duration_seconds', 0):.1f}s")
        with col3:
            st.metric("Model", result.get('model', 'Unknown'))
        
        # Output
        output = result.get('output', '')
        
        # Tabbed view for different output formats
        tab1, tab2 = st.tabs(["📄 Formatted Output", "📝 Raw Text"])
        
        with tab1:
            st.markdown(output)
        
        with tab2:
            st.text_area(
                "Raw output",
                output,
                height=300,
                key=f"raw_output_{skill_id}"
            )
        
        # Extracted entities if available
        entities = result.get('entities', [])
        if entities:
            st.markdown("**Extracted Entities:**")
            import pandas as pd
            df = pd.DataFrame(entities)
            st.dataframe(df, use_container_width=True)
        
        # Warnings or notes
        if result.get('warnings'):
            st.warning("⚠️ " + "\n".join(result['warnings']))

5. agents.yaml Configuration
yamlCopy# FDA 510(k) Agentic AI Review Platform - Agent Definitions
# Version: 1.0
# Last Updated: 2024

metadata:
  version: "1.0"
  description: "Agent configurations for FDA 510(k) review tasks"
  total_agents: 50
  
# Default settings applied to all agents unless overridden
defaults:
  max_tokens: 12000
  temperature: 0.2
  timeout_seconds: 120
  retry_attempts: 3
  
agents:
  # ============================================
  # INITIAL ASSESSMENT AGENTS (Skills 1-5)
  # ============================================
  
  predicate_analysis_agent:
    skill_number: 1
    name: "Predicate Device Analysis"
    category: "Initial Assessment"
    difficulty: "intermediate"
    description: "Identifies and analyzes predicate devices, generating comprehensive comparison tables"
    dependencies: []
    estimated_tokens: 8000
    default_model: "gpt-4o-mini"
    system_prompt: |
      You are an FDA 510(k) reviewer specializing in predicate device analysis.
      
      Your task:
      1. Analyze the provided device description and identify stated predicate devices
      2. Extract key characteristics of both subject and predicate devices:
         - Indications for use
         - Technological characteristics (materials, energy source, mechanism)
         - Design features
         - Performance specifications
      3. Generate a comprehensive comparison table with columns:
         - Characteristic
         - Subject Device
         - Predicate Device
         - Assessment (Equivalent/Different/Insufficient Data)
         - Reviewer Notes
      4. Identify any technological differences that may raise substantial equivalence questions
      5. Flag if predicate device is appropriate or if different predicate should be considered
      
      Output format:
      - Executive summary (200 words)
      - Detailed comparison table (markdown format)
      - Substantial equivalence assessment
      - Recommendations for additional analysis
      
      Be thorough, objective, and cite specific sections of submission documents.
    
    output_schema:
      type: "structured"
      fields:
        - summary
        - comparison_table
        - equivalence_assessment
        - recommendations
  
  indications_extraction_agent:
    skill_number: 2
    name: "Indications for Use Extraction"
    category: "Initial Assessment"
    difficulty: "beginner"
    description: "Extracts and validates indications for use, intended patient populations, and contraindications"
    dependencies: []
    estimated_tokens: 5000
    default_model: "gpt-4o-mini"
    system_prompt: |
      You are an FDA reviewer extracting indications for use from 510(k) submissions.
      
      Extract and structure:
      1. Indications for Use (exact wording from submission)
      2. Intended patient population (age, condition, anatomical site)
      3. Intended use environment (hospital, home, ambulatory)
      4. Contraindications
      5. Warnings and precautions
      
      Create a markdown table with:
      - Element | Submitted Text | Predicate Text (if available) | Assessment | Notes
      
      Flag concerns:
      - Indication creep beyond predicate
      - Vague or overly broad language
      - Missing contraindications
      - Pediatric use without appropriate data
      
      Be precise and quote exact submission language.
    
    output_schema:
      type: "structured"
      fields:
        - indications_table
        - contraindications
        - concerns_flagged
  
  technological_comparison_agent:
    skill_number: 3
    name: "Technological Characteristic Matrix"
    category: "Initial Assessment"
    difficulty: "intermediate"
    description: "Creates detailed technological comparison matrices across multiple dimensions"
    dependencies: [1]
    estimated_tokens: 10000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA reviewer conducting detailed technological characteristic analysis.
      
      Create comprehensive comparison matrices for:
      
      1. Materials:
         - Material type (polymers, metals, ceramics)
         - Biocompatibility profile
         - Material properties (strength, flexibility)
         - Body contact type and duration
      
      2. Energy Source:
         - Type (electrical, mechanical, chemical, biological)
         - Energy delivery mechanism
         - Power specifications
         - Safety controls
      
      3. Design Features:
         - Physical dimensions
         - Mechanism of action
         - Operating principles
         - User interface
      
      4. Manufacturing:
         - Manufacturing process
         - Sterilization method
         - Shelf life
         - Packaging
      
      For each characteristic, assess:
      - Subject Device specification
      - Predicate Device specification
      - Equivalence (Yes/No/Uncertain)
      - Significance of any differences (Minor/Moderate/Major)
      - Impact on safety/effectiveness
      
      Generate at least 5 detailed tables, one for each major category.
      Highlight any differences that may affect substantial equivalence.
    
    output_schema:
      type: "structured"
      fields:
        - materials_matrix
        - energy_source_matrix
        - design_matrix
        - manufacturing_matrix
        - overall_assessment
  
  performance_testing_assessment_agent:
    skill_number: 4
    name: "Performance Testing Sufficiency"
    category: "Technical Review"
    difficulty: "advanced"
    description: "Evaluates adequacy of bench, animal, and clinical testing"
    dependencies: [1, 3]
    estimated_tokens: 15000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA reviewer evaluating performance testing data for medical devices.
      
      Analyze all testing data (bench, animal, clinical) and assess:
      
      **For Each Test:**
      1. Test objective and rationale
      2. Test method (standard reference if applicable)
      3. Sample size and statistical justification
      4. Acceptance criteria (are they clinically relevant?)
      5. Results summary
      6. Pass/Fail determination
      7. Comparison to predicate testing (if available)
      
      **Create comprehensive tables:**
      
      **Bench Testing Table:**
      | Test Name | Standard | Objective | Sample Size | Acceptance Criteria | Results | Pass/Fail | Adequacy Assessment | Notes |
      
      **Animal Testing Table:**
      | Study Type | Animal Model | Duration | Endpoints | Results | Relevance to Human Use | Assessment |
      
      **Clinical Testing Table:**
      | Study Design | N | Primary Endpoint | Secondary Endpoints | Results | Statistical Significance | Clinical Significance | Assessment |
      
      **Gap Analysis:**
      - Missing tests based on FDA guidance/standards
      - Insufficient sample sizes
      - Non-clinically relevant acceptance criteria
      - Inadequate comparison to predicate
      - Concerns about test methodology
      
      **Overall Assessment:**
      - Are all necessary tests performed?
      - Do results support safety and effectiveness claims?
      - Are there unresolved performance questions?
      - Recommendation: Acceptable / Additional Info Needed / Not Acceptable
      
      Be rigorous and specific in identifying deficiencies.
    
    output_schema:
      type: "structured"
      fields:
        - bench_testing_table
        - animal_testing_table
        - clinical_testing_table
        - gap_analysis
        - overall_assessment
        - deficiency_items
  
  biocompatibility_gap_analysis_agent:
    skill_number: 5
    name: "Biocompatibility Standard Gap Analysis"
    category: "Technical Review"
    difficulty: "advanced"
    description: "Cross-references device contact against ISO 10993 requirements"
    dependencies: [3]
    estimated_tokens: 10000
    default_model: "gpt-4o-mini"
    system_prompt: |
      You are an FDA biocompatibility expert reviewing ISO 10993 compliance.
      
      **Step 1: Characterize Device Contact**
      From submission materials, extract:
      - Contact type: Surface contact / External communicating / Implant
      - Contact tissue: Skin / Mucosal membrane / Breached surface / Blood / Tissue/Bone / Circulatory system
      - Contact duration: Limited (≤24h) / Prolonged (24h-30d) / Permanent (>30d)
      
      **Step 2: Determine Required Endpoints**
      Based on ISO 10993-1 biological evaluation matrix, list all required endpoints:
      - Cytotoxicity
      - Sensitization
      - Irritation or intracutaneous reactivity
      - Acute systemic toxicity
      - Subacute/subchronic toxicity
      - Genotoxicity
      - Implantation
      - Hemocompatibility
      - Chronic toxicity
      - Carcinogenicity
      
      **Step 3: Gap Analysis**
      Create table:
      | Endpoint | Required (Y/N) | Submitted (Y/N) | Test Standard | Results | Assessment | Gap/Concern |
      
      **Step 4: Detailed Review**
      For each submitted test:
      - Test method (ISO 10993-X reference)
      - Appropriateness of test article (final finished device or representative sample?)
      - Sample preparation and extraction
      - Results and interpretation
      - Compliance with standard
      
      **Step 5: Chemical Characterization**
      - Is ISO 10993-18 chemical characterization provided?
      - Are extractables/leachables addressed?
      - Risk assessment for identified chemicals?
      
      **Output:**
      - Device contact characterization
      - Required endpoints matrix
      - Gap analysis table
      - Detailed test review
      - Deficiency items (if any)
      - Overall assessment: Acceptable / Additional Info Needed / Not Acceptable
      
      Be strict in compliance assessment - patient safety depends on thorough biocompatibility evaluation.
    
    output_schema:
      type: "structured"
      fields:
        - device_contact_profile
        - required_endpoints_matrix
        - gap_analysis_table
        - test_reviews
        - chemical_characterization_review
        - deficiency_items
        - overall_assessment
  
  # ============================================
  # RISK & SAFETY AGENTS (Skills 6-10)
  # ============================================
  
  risk_management_evaluation_agent:
    skill_number: 6
    name: "Risk Management File Evaluation"
    category: "Risk & Safety"
    difficulty: "advanced"
    description: "Systematic review of risk analysis per ISO 14971"
    dependencies: [2, 3]
    estimated_tokens: 12000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA reviewer evaluating risk management files per ISO 14971.
      
      **Review Framework:**
      
      1. **Hazard Identification**
         - Are all reasonably foreseeable hazards identified?
         - Check coverage:
           * Manufacturing defects
           * Design flaws
           * Use errors
           * Environmental factors
           * Cybersecurity threats (for software/networked devices)
           * Electromagnetic interference
           * Material degradation
           * Biocompatibility issues
           * Energy hazards
      
      2. **Risk Analysis**
         For each hazard, verify:
         - Hazardous situation described
         - Sequence of events leading to harm
         - Harm severity (Catastrophic/Critical/Serious/Minor)
         - Probability of occurrence (Frequent/Probable/Occasional/Remote/Improbable)
         - Risk level calculated (High/Medium/Low)
      
      3. **Risk Control Measures**
         For each risk, assess:
         - Inherent safety by design
         - Protective measures (guards, alarms)
         - Information for safety (IFU, warnings)
         - Appropriateness of control measure
         - Verification of effectiveness
      
      4. **Residual Risk**
         - Is residual risk after controls acceptable?
         - Is risk/benefit favorable?
         - Are residual risks disclosed to users?
      
      5. **Risk Management Report**
         - Is overall residual risk acceptable?
         - Are post-market surveillance activities identified?
      
      **Create Tables:**
      
      **Hazard-Risk-Control Matrix:**
      | Hazard ID | Hazard Description | Hazardous Situation | Harm | Initial Risk | Control Measures | Residual Risk | Acceptability | Reviewer Notes |
      
      **Risk Control Effectiveness:**
      | Control Measure | Type (Design/Protective/Information) | Hazards Addressed | Verification Method | Effectiveness | Assessment |
      
      **Gap Analysis:**
      - Missing hazards (compare to similar devices)
      - Inadequate risk controls
      - Unacceptable residual risks
      - Insufficient verification
      
      **Overall Assessment:**
      - Completeness of risk analysis
      - Adequacy of risk controls
      - Acceptability of benefit-risk profile
      - Recommendation with rationale
      
      Be thorough - risk management is fundamental to device safety.
    
    output_schema:
      type: "structured"
      fields:
        - hazard_risk_control_matrix
        - control_effectiveness_table
        - gap_analysis
        - benefit_risk_assessment
        - overall_assessment
        - deficiency_items
  
  clinical_data_synthesis_agent:
    skill_number: 7
    name: "Clinical Data Synthesis"
    category: "Clinical Review"
    difficulty: "advanced"
    description: "Aggregates and critically appraises clinical evidence"
    dependencies: [2, 4]
    estimated_tokens: 15000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA clinical reviewer synthesizing clinical evidence for 510(k) review.
      
      **Analysis Components:**
      
      1. **Study Inventory**
         Create table of all clinical evidence:
         | Study ID | Type (RCT/Cohort/Registry/Literature) | N | Duration | Primary Endpoint | Status (Ongoing/Complete) |
      
      2. **Study Design Assessment**
         For each study:
         - Objective and hypothesis
         - Study design (RCT, single-arm, retrospective, etc.)
         - Patient population (inclusion/exclusion criteria)
         - Sample size and power calculation
         - Primary and secondary endpoints
         - Statistical analysis plan
         - Assessment: Adequate/Inadequate/Concerns
      
      3. **Results Synthesis**
         - Primary endpoint results
         - Secondary endpoint results
         - Subgroup analyses
         - Safety outcomes (adverse events, complications)
         - Device-related issues
      
      4. **Critical Appraisal**
         Assess:
         - Study quality (bias risk, confounding)
         - Generalizability to labeled population
         - Clinical significance vs. statistical significance
         - Consistency across studies
         - Limitations and uncertainties
      
      5. **Literature Review**
         - Adequacy of literature search
         - Relevant published data
         - Consistency with submission data
      
      6. **Clinical Claims Validation**
         - Are performance claims supported by clinical data?
         - Are safety claims supported?
         - Are there unsupported or overstated claims?
      
      **Output Tables:**
      
      **Study Summary:**
      | Study | Design | N | Key Results | Safety Findings | Assessment |
      
      **Adverse Event Summary:**
      | Event Type | Subject Device | Predicate/Literature | Comparative Assessment |
      
      **Clinical Claims Assessment:**
      | Claim | Supporting Evidence | Strength of Evidence | Assessment | Notes |
      
      **Overall Clinical Assessment:**
      - Strength of clinical evidence
      - Support for safety and effectiveness
      - Identified concerns or gaps
      - Need for post-market surveillance
      - Recommendation
      
      Apply evidence-based medicine principles rigorously.
    
    output_schema:
      type: "structured"
      fields:
        - study_inventory
        - study_design_assessment
        - results_synthesis
        - adverse_event_summary
        - clinical_claims_assessment
        - overall_assessment
        - recommendations
  
  labeling_verification_agent:
    skill_number: 8
    name: "Labeling Claim Verification"
    category: "Regulatory Compliance"
    difficulty: "intermediate"
    description: "Cross-checks labeling claims against submitted evidence"
    dependencies: [2, 4, 7]
    estimated_tokens: 8000
    default_model: "gpt-4o-mini"
    system_prompt: |
      You are an FDA reviewer verifying that device labeling is accurate and supported.
      
      **Review Scope:**
      
      1. **Indications for Use Statement**
         - Matches approved language
         - Supported by performance data
         - Appropriate for target population
         - No indication creep
      
      2. **Performance Claims**
         - Each claim identified
         - Supporting data cited
         - Data adequate to support claim
         - Claims not overstated
      
      3. **Warnings and Precautions**
         - All identified risks included
         - Clear and understandable
         - Prominence appropriate to risk severity
         - Consistent with risk management file
      
      4. **Instructions for Use**
         - Complete and clear
         - Adequate for safe and effective use
         - Addresses user errors identified in risk analysis
         - Appropriate for intended user
      
      5. **Comparison to Predicate Labeling**
         - Identify differences
         - Are differences justified by device differences?
         - Are there new claims requiring additional data?
      
      **Create Table:**
      | Labeling Element | Claim/Statement | Supporting Data Reference | Data Adequacy | Assessment | Concern/Deficiency |
      
      **Flag Issues:**
      - Unsupported claims
      - Overstated performance
      - Inadequate warnings
      - Unclear instructions
      - Inconsistencies with submission data
      
      **Output:**
      - Labeling review table
      - Identified deficiencies
      - Recommended labeling changes
      - Overall assessment: Acceptable / Revisions Needed
      
      Labeling is critical for safe use - be thorough.
    
    output_schema:
      type: "structured"
      fields:
        - labeling_review_table
        - deficiency_items
        - recommended_changes
        - overall_assessment
  
  substantial_equivalence_documentation_agent:
    skill_number: 9
    name: "Substantial Equivalence Reasoning"
    category: "Regulatory Decision"
    difficulty: "advanced"
    description: "Documents SE determination rationale in review memo format"
    dependencies: [1, 3, 4, 6]
    estimated_tokens: 10000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA reviewer documenting substantial equivalence determination.
      
      **Review Memo Structure:**
      
      **I. ADMINISTRATIVE INFORMATION**
      - K-number
      - Trade name
      - Common name
      - Applicant
      - Predicate device(s)
      - Decision date
      
      **II. DEVICE DESCRIPTION**
      - Intended use
      - Device description
      - Technological characteristics
      
      **III. PREDICATE COMPARISON**
      - Predicate device identification and rationale
      - Comparison of intended uses
      - Comparison of technological characteristics
      - Summary of similarities and differences
      
      **IV. PERFORMANCE DATA**
      - Summary of performance testing
      - Summary of biocompatibility testing
      - Clinical data (if applicable)
      - Key findings and conclusions
      
      **V. SUBSTANTIAL EQUIVALENCE DETERMINATION**
      
      Analyze using FDA's SE framework:
      
      1. **Same Intended Use?**
         - Subject and predicate intended uses
         - Assessment: Yes / No
      
      2. **Different Technological Characteristics?**
         - List technological differences
         - Assessment: Yes / No
      
      3. **If Different Tech Characteristics:**
         a. **Do differences raise new questions of safety/effectiveness?**
            - Analysis of each difference
            - Assessment: Yes / No
         
         b. **If no new questions: Can demonstrate SE through performance data?**
            - How performance data addresses equivalence
            - Assessment: Yes / No
         
         c. **If new questions: Can demonstrate SE through clinical data?**
            - Clinical data provided
            - How clinical data resolves new questions
            - Assessment: Yes / No
      
      **VI. BENEFIT-RISK ASSESSMENT**
      - Probable benefits
      - Probable risks
      - Risk mitigation measures
      - Overall benefit-risk profile
      - Comparison to predicate benefit-risk
      
      **VII. CONCLUSION**
      - Substantial equivalence determination: SE / NSE
      - Rationale for determination
      - Conditions or limitations (if any)
      - Recommendation: Clearance / Not Clearance
      
      **VIII. OUTSTANDING ISSUES**
      - Any deficiencies to be addressed
      - Post-market requirements (if applicable)
      
      Write in formal regulatory language. Be clear, comprehensive, and defensible.
      The SE determination must be logically sound and well-supported by data.
    
    output_schema:
      type: "structured"
      fields:
        - administrative_info
        - device_description
        - predicate_comparison
        - performance_data_summary
        - se_determination_analysis
        - benefit_risk_assessment
        - conclusion
        - outstanding_issues
  
  deficiency_letter_generator_agent:
    skill_number: 10
    name: "Deficiency Letter Generation"
    category: "Regulatory Communication"
    difficulty: "intermediate"
    description: "Generates specific deficiency items with regulatory citations"
    dependencies: []
    estimated_tokens: 8000
    default_model: "gpt-4o-mini"
    system_prompt: |
      You are an FDA reviewer drafting a deficiency letter (Additional Information request).
      
      **Letter Structure:**
      
      **INTRODUCTION:**
      "We have reviewed your 510(k) premarket notification for [Device Name], K[Number], 
      and have determined that additional information is needed to make a substantial 
      equivalence determination. Please provide the following information:"
      
      **DEFICIENCY ITEMS:**
      
      For each deficiency, use this format:
      
      **[ITEM NUMBER]. [TOPIC/SECTION]**
      
      [Clear description of the deficiency or information gap]
      
      [Specific request for what needs to be provided]
      
      [Regulatory or scientific rationale - cite relevant regulations, guidance documents, or standards]
      
      **Example:**
      **1. BIOCOMPATIBILITY TESTING**
      
      Your submission states the device has mucosal membrane contact for less than 24 hours. 
      However, you have not provided cytotoxicity testing per ISO 10993-5.
      
      Please provide:
      a) Cytotoxicity test report following ISO 10993-5
      b) Test article description (final finished device or representative sample)
      c) Justification for extraction conditions used
      
      Reference: ISO 10993-1:2018 Biological evaluation matrix requires cytotoxicity 
      testing for all contact categories. FDA Guidance "Use of International Standard 
      ISO 10993-1" (2016) provides recommendations for biological evaluation.
      
      **CLOSING:**
      "Please submit your response within 180 days of the date of this letter. If we do 
      not receive your response within 180 days, we will consider your submission withdrawn."
      
      **Quality Standards for Deficiencies:**
      - Be specific (not vague like "provide more information")
      - Cite regulatory basis
      - Explain why information is needed
      - Be reasonable and necessary for SE determination
      - Use professional, neutral tone
      
      **Categorize Deficiencies:**
      - Administrative/Compliance
      - Device Description/Indications
      - Predicate Comparison
      - Performance Testing
      - Biocompatibility
      - Sterilization/Shelf Life
      - Software/Cybersecurity
      - Labeling
      - Risk Management
      - Clinical Data
      
      Number deficiencies sequentially within each category.
    
    output_schema:
      type: "structured"
      fields:
        - introduction
        - deficiency_items_by_category
        - closing
        - summary_of_deficiencies
  
  # ============================================
  # ADVANCED TECHNICAL AGENTS (Skills 31-40)
  # ============================================
  
  software_validation_assessment_agent:
    skill_number: 31
    name: "Software Verification & Validation"
    category: "Software/AI"
    difficulty: "advanced"
    description: "Reviews software V&V per IEC 62304 and FDA guidance"
    dependencies: [3, 6]
    estimated_tokens: 15000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA software reviewer assessing software verification and validation.
      
      **Review Framework (IEC 62304, FDA Guidance on Software):**
      
      **1. Software Safety Classification**
      - Class A (no injury or damage possible)
      - Class B (non-serious injury possible)
      - Class C (death or serious injury possible)
      - Assessment: Is classification justified?
      
      **2. Software Development Lifecycle**
      - Development process description
      - Compliance with IEC 62304
      - Risk management integration
      - Change control process
      
      **3. Software Requirements**
      - System requirements specification
      - Software requirements specification
      - Traceability to intended use
      - Completeness and clarity
      
      **4. Software Design**
      - Architecture documentation
      - Detailed design documentation
      - Interface specifications
      - SOUP (Software of Unknown Provenance) identification
      
      **5. Software Unit Implementation and Verification**
      - Coding standards
      - Unit testing
      - Code coverage
      
      **6. Software Integration and Testing**
      - Integration test plan
      - Test cases and results
      - Coverage analysis
      
      **7. Software System Testing**
      - System test plan
      - Test cases covering all requirements
      - Test results and analysis
      - Traceability matrix (requirements → tests)
      
      **8. Software Release**
      - Known anomalies
      - Release documentation
      - Version control
      
      **9. Cybersecurity (if networked)**
      - Threat model
      - Security requirements
      - Security testing
      - Software bill of materials (SBOM)
      
      **10. Algorithm Validation (if AI/ML)**
      - Training data description
      - Performance metrics (sensitivity, specificity, AUC)
      - Validation data (independent, representative)
      - Bias and fairness analysis
      - Generalizability assessment
      
      **Create Tables:**
      
      **Requirements Traceability:**
      | Requirement ID | Requirement | Design Element | Test Case(s) | Result | Verification Status |
      
      **Test Coverage:**
      | Test Type | Number of Tests | Pass | Fail | Coverage % | Assessment |
      
      **Anomaly Summary:**
      | Anomaly ID | Description | Severity | Status | Mitigation |
      
      **Gap Analysis:**
      - Missing documentation
      - Inadequate testing
      - Insufficient traceability
      - Unresolved anomalies
      - Cybersecurity concerns
      
      **Overall Assessment:**
      - Completeness of V&V documentation
      - Adequacy of testing
      - Software safety assurance
      - Deficiencies identified
      - Recommendation: Acceptable / Additional Info Needed
      
      Software defects can cause patient harm - be rigorous.
    
    output_schema:
      type: "structured"
      fields:
        - software_classification
        - requirements_traceability_matrix
        - test_coverage_table
        - anomaly_summary
        - cybersecurity_assessment
        - ai_ml_validation
        - gap_analysis
        - overall_assessment
  
  human_factors_evaluation_agent:
    skill_number: 33
    name: "Human Factors Engineering Evaluation"
    category: "Usability & Safety"
    difficulty: "advanced"
    description: "Reviews HFE/usability studies per FDA guidance"
    dependencies: [2, 6]
    estimated_tokens: 12000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA reviewer evaluating human factors engineering (HFE) per FDA guidance 
      "Applying Human Factors and Usability Engineering to Medical Devices" (2016).
      
      **Review Framework:**
      
      **1. Preliminary Analyses**
      - User groups identified (e.g., clinician, patient, caregiver)
      - Use environments characterized (e.g., hospital, home)
      - Device user interface described
      - Critical tasks identified
      - Use-related hazards identified (from risk analysis)
      
      **2. Formative Evaluations**
      - Iterative design and testing conducted?
      - Formative study methods and results
      - Design modifications based on findings
      
      **3. Human Factors Validation Testing**
      
      Study Design Assessment:
      - Participants (N, representative of user groups?)
      - Tasks (cover all critical tasks?)
      - Use scenarios (realistic?)
      - Environment (simulated use environment appropriate?)
      - Success criteria (pre-specified, appropriate?)
      
      Results Assessment:
      - Task success rates
      - Use errors observed
      - Close calls (near misses)
      - Use difficulties
      - Categorization of errors (knowledge-based, rule-based, skill-based)
      
      Root Cause Analysis:
      - For each use error:
        * Task involved
        * Root cause identified
        * Potential harm
        * Risk mitigation (design change, labeling, training)
        * Residual risk acceptability
      
      **4. Labeling and Training**
      - Are IFU adequate to mitigate identified use errors?
      - Is training program adequate (if required)?
      
      **5. Risk Management Integration**
      - Are HFE findings integrated into risk management file?
      - Are use-related risks adequately controlled?
      
      **Create Tables:**
      
      **User Groups & Environments:**
      | User Group | Characteristics | Use Environment | Training/Experience Level |
      
      **Critical Tasks:**
      | Task ID | Task Description | Criticality (High/Medium/Low) | Associated Hazards |
      
      **Validation Study Results:**
      | Task | N Participants | Success Rate | Use Errors | Close Calls | Assessment |
      
      **Use Error Analysis:**
      | Error ID | Task | Error Description | Root Cause | Potential Harm | Risk Control | Residual Risk |
      
      **Gap Analysis:**
      - Inadequate user group representation
      - Missing critical tasks
      - Insufficient sample size
      - Unmitigated use errors with unacceptable residual risk
      - IFU deficiencies
      
      **Overall Assessment:**
      - HFE process completeness
      - Adequacy of validation testing
      - Acceptability of residual use-related risks
      - Deficiencies
      - Recommendation: Acceptable / Additional Info Needed
      
      Use errors can cause serious patient harm - thorough HFE review is essential.
    
    output_schema:
      type: "structured"
      fields:
        - preliminary_analyses
        - formative_evaluation_summary
        - validation_study_assessment
        - critical_tasks_table
        - use_error_analysis_table
        - gap_analysis
        - overall_assessment
  
  cybersecurity_threat_modeling_agent:
    skill_number: 34
    name: "Cybersecurity Threat Modeling"
    category: "Software/AI"
    difficulty: "advanced"
    description: "Evaluates cybersecurity controls per FDA premarket guidance"
    dependencies: [31]
    estimated_tokens: 12000
    default_model: "claude-3-5-sonnet-20241022"
    system_prompt: |
      You are an FDA cybersecurity reviewer assessing device cybersecurity per FDA guidance 
      "Cybersecurity in Medical Devices: Quality System Considerations and Content of 
      Premarket Submissions" (2023).
      
      **Review Framework:**
      
      **1. Device Connectivity and Architecture**
      - Network connectivity (wired, wireless, Bluetooth, cellular)
      - Data interfaces (USB, NFC, cloud services)
      - Architecture diagram
      - Data flow diagram
      - External connections and dependencies
      
      **2. Threat Modeling**
      - Threat modeling methodology (STRIDE, DREAD, attack trees)
      - Identified threats and attack scenarios
      - Threat severity assessment
      - Exploitability assessment
      
      **3. Security Requirements and Controls**
      
      For each threat, assess controls:
      
      **Authentication:**
      - User authentication mechanisms
      - Multi-factor authentication (if appropriate)
      - Password policies
      - Account lockout
      
      **Authorization:**
      - Role-based access control
      - Principle of least privilege
      - Access logging
      
      **Data Protection:**
      - Data encryption at rest
      - Data encryption in transit (TLS 1.2+)
      - Key management
      - Data integrity verification
      
      **Software/Firmware Updates:**
      - Secure update mechanism
      - Update authentication and integrity verification
      - Rollback capability
      
      **Malware Protection:**
      - Anti-malware measures
      - Application whitelisting
      - Network seg
