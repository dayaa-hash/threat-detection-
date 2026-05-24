![ost_logo](https://user-images.githubusercontent.com/44299200/210261186-1f0486a7-79e8-41b6-85f1-9e69915123aa.png)

# OSINT Toolkit

> **⚠️ Warning**
> OSINT Toolkit is not production ready yet. This is an early prototype that still needs some work to be done.

## A Full-Stack Web Application Built for Security Analysts

OSINT Toolkit is a self-hostable, on-demand analysis platform designed for security specialists. It consolidates various security tools into a single, easy-to-use environment, streamlining everyday tasks. Optimized for single-user operation, OSINT Toolkit runs locally in a Docker container and is not intended for long-term data storage or management. Instead, it focuses on accelerating daily workflows, such as news aggregation and analysis, IOC and email investigations, and the creation of threat detection rules. To further enhance efficiency, OSINT Toolkit integrates generative AI capabilities, providing additional support for analysis and decision-making.

---

## 📋 Table of Contents

- [Features](#features)
- [Integrated Services](#integrated-services)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [API Keys Setup](#api-keys-setup)
- [Usage](#usage)
- [Development](#development)
- [License](#license)
- [Contributing](#contributing)

---

## ✨ Features

### 1. Newsfeed
The Newsfeed module keeps you up to date about the latest cybersecurity news by aggregating articles from trusted sources such as Wired, The Hacker News, Security Magazine, Threatpost, TechCrunch Security, and Dark Reading. Stay up-to-date with industry trends and potential threats without having to visit multiple websites or subscribe to numerous newsletters. The module extracts IOCs automatically from the news articles and lets you analyze news in no time using AI.

![newsfeed](https://github.com/user-attachments/assets/0c23cc14-4a1a-4c34-9fb8-5064a0f23889)

**Key Capabilities:**
- RSS feed aggregation from multiple security news sources
- Automatic IOC extraction from articles
- AI-powered news analysis
- Keyword-based filtering
- Scheduled news updates

---

### 2. IOC Tools
The IOC Tools module helps you analyze different types of indicators of compromise (IOCs) such as IP addresses, hashes, email addresses, domains, and URLs. It leverages services like VirusTotal, AlienVault, AbuseIPDB, and social media platforms like Reddit and Twitter to gather information about the IOCs. The module automatically detects the type of IOC being analyzed and utilizes the appropriate services to provide relevant information, enabling you to identify potential threats and take necessary actions to protect your organization.

![ioc_lookup](https://github.com/user-attachments/assets/40b1e656-ba6c-4f36-b8dd-beee0dca3fdd)

**Sub-modules:**
- **Single Lookup** - Analyze individual IOCs
- **Bulk Lookup** - Analyze multiple IOCs at once
- **Extractor** - Extract IOCs from text or files
- **Defang/Fang** - Safely format IOCs for sharing

---

### 3. Email Analyzer
The Email Analyzer module allows you to analyze `.eml` files for potential threats. Simply drag and drop an `.eml` file into the module, and it will parse the file, perform basic security checks, extract indicators of compromise (IOCs), and analyze messages with the help of AI.

**Key Capabilities:**
- EML file parsing
- Header analysis
- Security checks (SPF, DKIM, DMARC)
- IOC extraction (URLs, IPs, domains, hashes)
- Email routing/hop analysis
- Attachment analysis
- AI-powered message analysis

---

### 4. Domain Finder (Domain Monitoring)
The Domain Finder module helps you protect your organization from phishing attacks by searching for recently registered domains that match specific patterns. By utilizing the URLScan.io API, you can view screenshots of websites associated with domains without visiting them directly. Additionally, you can check each domain and its resolved IP against multiple threat intelligence services.

**Key Capabilities:**
- Domain search by patterns/keywords
- URLScan.io integration for screenshots
- Multi-service threat intelligence lookup
- Historical domain analysis
- IP reputation checking

---

### 5. AI Templates
The AI Templates module provides powerful AI-based solutions for log data analysis, email text analysis, and source code explanation. It lets you create templates for AI tasks and supports you in the prompt engineering process.

![ai_templates](https://github.com/user-attachments/assets/42c52c8c-7d2d-4b70-b25c-666d6993832c)

**Key Capabilities:**
- Custom AI prompt templates
- Log analysis
- Email text analysis
- Source code explanation
- Multiple LLM provider support (OpenAI, Anthropic, Google Gemini)
- Template management and sharing

---

### 6. CVSS Calculator
The CVSS Calculator module allows you to calculate the CVSS 3.1 score of a vulnerability and export the calculation as a markdown or JSON file.

**Key Capabilities:**
- CVSS 3.1 base score calculation
- Environmental score adjustment
- Temporal score adjustment
- Export to Markdown/JSON
- Visual score display

---

### 7. Detection Rules
The Detection Rules module is a GUI for creating Sigma, YARA and Snort/Suricata rules.

**Key Capabilities:**
- Sigma rule creation
- YARA rule creation
- Snort/Suricata rule creation
- Rule validation
- Rule templates

---

## 🔌 Integrated Services

OSINT Toolkit integrates with over 20+ threat intelligence and security services:

| IPs | Domains | URLs | Emails | Hashes | CVEs |
|-----|---------|------|--------|--------|------|
| AbuseIPDB | AlienVault | AlienVault | Emailrep.io | AlienVault | GitHub |
| AlienVault | CheckPhish.ai | CheckPhish.ai | GitHub | GitHub | NIST NVD |
| CheckPhish.ai | GitHub | GitHub | Hunter.io | Maltiverse | |
| CrowdSec | Maltiverse | Google Safe Browsing | Have I Been Pwned | Pulsedive | |
| GitHub | Pulsedive | Maltiverse | Reddit | Reddit | |
| IPQualityScore | Shodan | Pulsedive | Twitter | ThreatFox | |
| Maltiverse | ThreatFox | Shodan | | Twitter | |
| Pulsedive | Reddit | ThreatFox | | Virustotal | |
| Shodan | Twitter | Reddit | | | |
| Reddit | URLScan | Twitter | | | |
| ThreatFox | Virustotal | URLScan | | | |
| Twitter | | Virustotal | | | |
| Virustotal | | | | | |

### Service Categories

- **Threat Intelligence**: AlienVault OTX, Maltiverse, Pulsedive, ThreatFox, VirusTotal, CrowdSec, URLhaus, MalwareBazaar
- **Security Scanning**: CheckPhish.ai, Google Safe Browsing, IPQualityScore, URLScan.io
- **Network Infrastructure**: Shodan, BGPView
- **Social Media**: Reddit, Twitter/X
- **Email Identity**: EmailRep.io, Have I Been Pwned, Hunter.io
- **Development/Research**: GitHub, NIST NVD

---

## 🛠 Tech Stack

### Backend
- **Framework**: FastAPI
- **Database**: SQLAlchemy (SQLite)
- **AI/ML**: LangChain (OpenAI, Anthropic, Google Gemini)
- **Task Scheduling**: APScheduler
- **HTTP Client**: aiohttp
- **RSS Parsing**: Feedparser

### Frontend
- **Framework**: React 18
- **UI Library**: Material UI (MUI)
- **State Management**: Recoil
- **Routing**: React Router
- **Charts**: Recharts, Nivo
- **Markdown**: React Markdown, React MD Editor

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **Web Server**: Nginx (Frontend)
- **ASGI Server**: Uvicorn (Backend)

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     OSINT Toolkit                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────┐    ┌─────────────────────────┐   │
│  │     Frontend        │    │       Backend           │   │
│  │   (React + MUI)     │◄──►│    (FastAPI)            │   │
│  │                     │    │                         │   │
│  │  - React Router     │    │  - API Routes           │   │
│  │  - Recoil State     │    │  - SQLAlchemy ORM       │   │
│  │  - Recharts/Nivo    │    │  - LangChain LLM        │   │
│  │  - Nginx            │    │  - APScheduler          │   │
│  └─────────────────────┘    └───────────┬─────────────┘   │
│                                         │                  │
│  ┌──────────────────────────────────────▼────────────────┐ │
│  │              Data Layer (SQLite)                      │ │
│  │  - Settings, API Keys, Templates, Newsfeed Cache      │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 📦 Prerequisites

- Docker Engine 20.10+
- Docker Compose 2.0+
- 4GB RAM minimum
- 10GB disk space

---

## 🚀 Installation

### Quick Start

1. **Clone or download the repository**
   ```bash
   git clone https://github.com/trickest/osint-toolkit.git
   cd osint-toolkit
   ```

2. **Start the application**
   ```bash
   docker-compose up -d
   ```

3. **Access the application**
   - Open your browser to: `http://localhost:4000`

### Manual Build (Optional)

```bash
# Build and start containers
docker-compose up -d --build

# View logs
docker-compose logs -f

# Stop containers
docker-compose down
```

---

## ⚙️ Configuration

### Environment Variables

The application uses default configurations. For production use, you may want to customize:

| Variable | Description | Default |
|----------|-------------|---------|
| `BACKEND_PORT` | Backend port | `8000` |
| `FRONTEND_PORT` | Frontend port | `4000` |
| `DATA_DIR` | Data directory | `./data` |

### Data Persistence

All data is stored in the `./data` directory:
- SQLite database
- Uploaded files
- Cached data

---

## 🔑 API Keys Setup

OSINT Toolkit requires API keys for full functionality. Configure keys through the web interface:

1. Navigate to **Settings** → **API Keys** in the sidebar
2. Enter your API keys for the services you want to use
3. Save your configuration

### Required Keys by Feature

| Feature | Required Services |
|---------|-------------------|
| Newsfeed | OpenAI (optional for AI analysis) |
| IOC Lookup | VirusTotal, AlienVault, AbuseIPDB, etc. |
| Email Analyzer | OpenAI (optional for AI analysis) |
| Domain Finder | URLScan.io |
| AI Templates | OpenAI, Anthropic, or Google Gemini |

### Getting API Keys

- **VirusTotal**: https://www.virustotal.com/gui/join-us
- **AlienVault OTX**: https://otx.alienvault.com/api
- **AbuseIPDB**: https://www.abuseipdb.com/account/api
- **Shodan**: https://account.shodan.io/
- **URLScan.io**: https://urlscan.io/docs/api/
- **OpenAI**: https://platform.openai.com/api-keys
- **Anthropic**: https://console.anthropic.com/
- **Google Gemini**: https://aistudio.google.com/app/apikey

> **Note**: Many services offer free tiers. Start with free services and add paid keys as needed.

---

## 📖 Usage

### Getting Started

1. **Configure API Keys** - Set up at least one threat intelligence service
2. **Explore Features** - Try each module from the sidebar
3. **Customize Settings** - Adjust modules, keywords, and CTI profile

### Feature Workflows

#### IOC Analysis
1. Go to **IOC Tools** → **Single Lookup**
2. Enter an IOC (IP, domain, hash, URL, email)
3. View results from multiple services

#### Email Analysis
1. Go to **Email Analyzer**
2. Drag and drop an `.eml` file
3. Review extracted IOCs and security checks

#### Domain Monitoring
1. Go to **Domain Finder**
2. Enter domain patterns to search
3. Review screenshots and threat intelligence

---

## 🔧 Development

### Project Structure

```
osint-toolkit/
├── backend/
│   ├── app/
│   │   ├── core/           # Core functionality
│   │   │   ├── database/   # Database models
│   │   │   ├── settings/   # Configuration
│   │   │   ├── alerts/     # Alerting system
│   │   │   └── scheduler/  # Task scheduling
│   │   ├── features/       # Feature modules
│   │   │   ├── newsfeed/
│   │   │   ├── ioc_tools/
│   │   │   ├── email_analyzer/
│   │   │   ├── domain_lookup/
│   │   │   └── llm_templates/
│   │   └── utils/          # Utilities
│   ├── main.py             # Application entry
│   └── requirements.txt    # Python dependencies
│
├── frontend/
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── api.js          # API client
│   │   ├── App.js          # Main app
│   │   └── sidebarConfig.js
│   ├── package.json        # Node dependencies
│   └── nginx.conf          # Nginx config
│
├── data/                   # Data persistence
├── docker-compose.yaml     # Docker orchestration
└── README.md              # This file
```

### Local Development

```bash
# Backend (requires Python 3.10+)
cd backend
pip install -r requirements.txt
uvicorn main:app --reload

# Frontend (requires Node.js 18+)
cd frontend
npm install
npm start
```

---

## 📄 License

See [LICENSE.md](LICENSE.md) for details.

---

## 🤝 Contributing

Contributions are welcome! Please read our [contributing guidelines](CONTRIBUTING.md) before submitting PRs.

### Ways to Contribute

- Report bugs
- Suggest new features
- Improve documentation
- Add new integrations
- Fix issues

---

## 📞 Support

- **Issues**: https://github.com/trickest/osint-toolkit/issues
- **Discussions**: https://github.com/trickest/osint-toolkit/discussions

---

## 🔗 Links

- [Documentation](https://github.com/trickest/osint-toolkit#readme)
- [Docker Hub](https://hub.docker.com/r/trickest/osint-toolkit)
- [GitHub Repository](https://github.com/trickest/osint-toolkit)

---

*Built with ❤️ for the security community*


### CVSS Calculator
The CVSS Calculator module allows you to calculate the CVSS 3.1 score of a vulnerability and export the calculation as a markdown or JSON file.


### Detection Rules
The Detection Rules module is a GUI for creating Sigma, Yara and Snort/Suricate rules.



## Deploy with docker
1. Download the repository and extract the files
2. Navigate to the directory where the `docker-compose.yaml` file is located
3. Run the following command: `docker-compose up -d`
4. Once the container is running, you can access the application in your browser at http://localhost:4000
