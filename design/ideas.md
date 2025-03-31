# AI-Powered Log Triage and Security Alert Aggregator for Fedora: A Comprehensive Approach

---

# AI-Powered Log Triage and Security Alert Aggregator for Fedora: A Comprehensive Approach

Before diving into the main report, this proposal offers a unique hybrid architecture combining multi-tier classification with resource-aware processing, leveraging the strengths of regex, traditional ML, and LLMs. It introduces MITRE ATT\&CK framework integration, explainable AI features, and a human feedback loop—all packaged into a lightweight, efficient solution focused on real-world admin usability.

## Project Overview

System administrators on Fedora systems face an overwhelming volume of logs from SELinux, systemd journal, audit logs, and applications. This deluge makes it nearly impossible to manually identify critical security events buried within routine messages. This project aims to develop an intelligent, resource-efficient system that automatically collects, parses, classifies, and prioritizes security-related logs using AI techniques.

### Problem Statement

The key challenges addressed by this project include:

- **Information Overload**: Fedora systems generate thousands of log entries daily
- **Security Visibility**: Critical security events are often lost in noise
- **Manual Analysis Burden**: Administrators lack time to review all logs
- **Resource Constraints**: Solutions must work efficiently on standard hardware


### Project Goals

1. Create a modular, plugin-based log collection system for multiple sources
2. Implement a multi-tier classification pipeline (regex → ML → LLM)
3. Develop adaptive anomaly detection using ensemble techniques
4. Provide actionable security insights with MITRE ATT\&CK mapping
5. Deliver a resource-efficient solution packaged as a Fedora RPM

## System Architecture

The proposed system follows a modular, pipeline-based architecture with six core components:

### Log Collection Module

- **Plugin-based collectors** for different log sources
    - SELinux logs (audit.log)
    - Systemd journal (via journalctl)
    - Audit logs (auditd)
    - Application logs (/var/log)
- **Collection methods**:
    - Realtime monitoring via inotify
    - Scheduled polling with configurable intervals
    - On-demand collection via CLI
- **Filtering options** to focus on security-relevant sources


### Preprocessing \& Normalization Engine

- **Log template extraction** using Drain3 algorithm
- **Field extraction** with regex and structured parsing
- **Entity recognition** for security-relevant information:
    - IP addresses, usernames, file paths, process IDs
    - Actions (login, access, modify, execute)
- **Standardization** of timestamps, severity levels, and formats
- **JSON schema** for consistent internal representation


### Multi-Level Classification Pipeline

- **Level 1: Pattern Matching**
    - Fast regex-based classification for known patterns
    - Pre-defined rules for common security events
    - Zero computational overhead for routine logs
- **Level 2: ML Classification**
    - Lightweight models: Random Forest, Gradient Boosting
    - Features: TF-IDF vectors, extracted entities, message patterns
    - Offline processing without external API dependencies
- **Level 3: Contextual Analysis**
    - Quantized LLMs for semantic understanding
    - Used only for high-importance or ambiguous logs
    - BERT-based models optimized for on-device inference


### Anomaly Detection Engine

- **Ensemble approach** combining multiple detection algorithms:
    - **Isolation Forest**: Detect rare, isolated anomalies
    - **Variational Autoencoder (VAE)**: Learn normal patterns
    - **LSTM Autoencoders**: Capture sequential anomalies
    - **DBSCAN**: Identify clusters of related anomalies
- **Confidence scoring** to prioritize detection results
- **Adaptive thresholds** that learn from the environment


### Threat Intelligence \& Correlation

- **MITRE ATT\&CK mapping** to contextualize security events
- **Cross-source correlation** to detect multi-step attack patterns
- **Temporal analysis** to identify related events across time
- **Severity ranking algorithm** based on:
    - Historical frequency
    - Security impact
    - Context information
    - Correlation with other events


### Presentation \& Action Layer

- **CLI dashboard** for real-time monitoring
- **Prioritized alerts** with severity scoring and explanations
- **Remediation suggestions** for common security issues
- **Integration options** with desktop notifications (GNOME)


## Technical Approach

### Log Collection \& Preprocessing

The system will collect logs using native APIs and command-line utilities, normalizing them into a consistent JSON structure:

```json
{
  "timestamp": "2025-03-30T14:22:10Z",
  "source": "auditd",
  "hostname": "fedora-server",
  "process": "sshd",
  "pid": 3021,
  "message": "Failed password for root from 192.168.1.10",
  "extracted_entities": {
    "user": "root",
    "ip_address": "192.168.1.10",
    "action": "failed_login"
  },
  "classification": {
    "category": "authentication",
    "severity": "warning",
    "confidence": 0.92,
    "mitre_ttp": "T1110"
  }
}
```

The preprocessing will extract meaningful features using:

- **Named Entity Recognition** for security-relevant entities
- **Semantic Feature Extraction** with TF-IDF and word embeddings
- **Contextual Enrichment** with system and temporal context


### Multi-Level Classification Approach

The tiered classification approach balances speed, accuracy, and resource consumption:

1. **Fast-Path Classification**: Regex patterns for known log types (70-80% of logs)
2. **ML-Based Classification**: Lightweight models for more complex patterns (15-20%)
3. **Deep Contextual Analysis**: Quantized LLMs for ambiguous logs (1-5%)

This approach ensures most logs are processed efficiently while reserving detailed analysis for important or unusual events.

### Anomaly Detection \& Scoring

The system will implement an ensemble of complementary models:

- **Isolation Forest**: Efficient detection of outliers
- **Variational Autoencoder**: Pattern-based anomaly detection
- **LSTM Autoencoder**: Temporal anomaly detection
- **DBSCAN**: Clustering to identify related anomalies

Each model produces a confidence score, combined using a weighted ensemble approach with adaptive thresholds to reduce false positives over time.

### Innovative Features

#### Adaptive Learning System with Human Feedback

- **Active Learning**: Flag uncertain classifications for review
- **Feedback Integration**: Update models based on administrator input
- **Continuous Improvement**: Periodic retraining with new data


#### Resource-Aware Processing Pipeline

- **Dynamic Resource Allocation**: Scale based on available resources
- **Tiered Processing**: Reserve intensive analysis for high-risk logs
- **Batch Processing Option**: Defer analysis to idle periods


#### Explainable AI for Security Events

- **SHAP (SHapley Additive exPlanations)** for model transparency
- **Evidence Highlighting** in log entries
- **Confidence Scoring** with explanation


#### Zero-Shot Detection for Unknown Threats

- **Transfer Learning** from general security knowledge
- **Semantic Similarity** for detecting variants
- **Anomaly-Based Detection** without prior examples


## Implementation Timeline

### Weeks 1-2: Research \& Setup

- Review Fedora log sources and formats
- Set up development environment
- Create project structure
- Begin developing data collection scripts


### Weeks 3-4: Log Collection \& Preprocessing

- Implement collectors for all log sources
- Develop preprocessing pipeline
- Create entity extraction module
- Build normalized JSON schema


### Weeks 5-6: Basic Classification \& ML Models

- Implement regex classification rules
- Train lightweight ML models
- Develop feature extraction pipeline
- Create evaluation framework


### Weeks 7-8: Anomaly Detection \& Analysis

- Implement ensemble anomaly detection
- Integrate MITRE ATT\&CK mapping
- Develop correlation engine
- Build severity scoring system


### Weeks 9-10: UI \& Notification System

- Develop CLI dashboard
- Implement alerting system
- Create visualization components
- Build query interface


### Weeks 11-12: Packaging \& Testing

- Create RPM package
- Conduct comprehensive testing
- Complete documentation
- Create demonstration setup


## Deliverables

### Source Code Repository

- Complete Python/Bash codebase on GitHub
- Well-structured architecture with clear documentation
- Comprehensive test suite
- CI/CD pipeline integration


### Packaged RPM

- Fedora-compliant RPM package
- Proper dependencies and installation scripts
- Systemd service for background operation
- Configuration files with sensible defaults


### Documentation

- Installation and usage guide
- Configuration reference
- Developer documentation
- API documentation for extensibility


### Demonstration \& Prototype

- Working CLI dashboard
- Example configurations
- Demo script for key features
- Sample dataset for evaluation


### Testing \& Evaluation Results

- Performance benchmarks
- Accuracy metrics for classification and detection
- False positive/negative analysis
- Scalability testing


## Evaluation Strategy

The success of this project will be measured using several key metrics:

### Performance Metrics

- **Processing Speed**: Logs processed per second
- **Resource Utilization**: CPU, memory usage (target: <200MB RAM)
- **Latency**: Time from log generation to alert
- **Scalability**: Performance with increasing log volume


### Detection Metrics

- **Accuracy**: Correct classifications / total classifications
- **Precision**: True positives / (true positives + false positives)
- **Recall**: True positives / (true positives + false negatives)
- **F1 Score**: Harmonic mean of precision and recall


## Conclusion

This proposal presents a comprehensive approach to building an AI-powered log triage system for Fedora. By combining traditional pattern matching with modern ML techniques in a resource-efficient architecture, the system will provide significant value to system administrators while maintaining performance on standard hardware.

The multi-tiered classification approach, along with adaptive anomaly detection and MITRE ATT\&CK integration, will enable accurate identification of security events while minimizing false positives. The modular design ensures extensibility, allowing the system to evolve with changing security needs and log formats.

Through this project, I aim to deliver a practical, efficient, and reliable tool that enhances security monitoring capabilities on Fedora systems while reducing the burden on administrators.