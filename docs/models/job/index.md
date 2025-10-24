# Job Autobot Documentation

Job Autobot is an AI-powered job search assistant available on Telegram that helps job seekers find opportunities, build professional CVs, and navigate their career development.

---

## Table of Contents
1. [Overview](#overview)
2. [Getting Started](#getting-started)
3. [Commands Reference](#commands-reference)
4. [Features](#features)
5. [For Developers](#for-developers)
6. [Pricing & Limits](#pricing--limits)
7. [Support](#support)
8. [FAQ](#faq)

---

## Overview

Job Autobot leverages AI to streamline the job search process by providing:

- **Smart Job Search**: Find relevant opportunities using natural language queries
- **CV Building**: Create and optimize professional resumes
- **Career Guidance**: Get personalized career path recommendations
- **Application Tools**: Generate cover letters and improve your CV
- **Job Alerts**: Receive notifications for new matching positions

**Target Audience**: Job seekers at all career levels, from entry-level to experienced professionals.

---

## Getting Started

### Accessing Job Autobot

1. **Open Telegram**
   - Search for `@jobautobot` or visit: [t.me/jobautobot](https://t.me/jobautobot)
   
2. **Start Chatting**
   - Send `/start` to begin
   - Use available commands to explore features

3. **Free vs Premium**
   - Free users get 10 job searches per month
   - Upgrade to premium for unlimited access and advanced features

---

## Commands Reference

### 🎯 Core Job Search Commands

#### `/findjobs [keywords] [location] [type]`
Searches for jobs across multiple platforms.

**Parameters:**
- `keywords` (required): Job title, skills, or company names
- `location` (optional): City, country, or "remote"
- `type` (optional): full-time, part-time, contract, internship

**Examples:**
```

/findjobs python developer
/findjobs data scientist london
/findjobs frontend developer remote full-time
/findjobs marketing manager new york

```

#### `/quota`
Shows your remaining job searches for the current month.

**Free Users:** 10 searches per month
**Premium Users:** Unlimited searches

#### `/history`
Displays your saved jobs and search history.

---

### 📝 CV & Profile Management

#### `/build_cv`
Starts an interactive CV creation wizard with the following sections:
- Personal information
- Work experience (multiple positions)
- Education history
- Skills and competencies
- Projects and portfolio
- Certifications and awards
- References

The bot guides you through each section step by step.

#### `/view_cv`
Displays your current CV in a formatted, readable layout.

#### `/cv_review`
Provides AI-powered analysis of your CV with suggestions for:
- Formatting improvements
- Content optimization
- Keyword enhancement for ATS systems
- Section organization

---

### 🔔 Job Alerts System

#### `/setalert`
Creates personalized job alerts based on your criteria:
- Job titles and keywords
- Locations (or remote)
- Salary ranges
- Experience levels
- Company types

**Examples of alert criteria:**
- "Senior software engineer positions in Berlin"
- "Remote marketing jobs paying $80k+"
- "Entry-level data analyst roles"

#### `/myalerts`
Manages your active job alerts:
- View all active alerts
- Edit alert criteria
- Delete alerts
- Pause/resume alerts

---

### 🚀 Career Development

#### `/careerpath [current_role]`
Explores career progression options and potential growth paths.

**Examples:**
```

/careerpath software developer
/careerpath marketing coordinator
/careerpath data analyst

```

**Provides:**
- Next-level positions
- Required skills and experience
- Salary progression data
- Alternative career paths

#### `/practice`
Interactive interview preparation with:
- Common behavioral questions
- Technical questions by field
- STAR method guidance
- Sample answers and feedback

#### `/upskill`
Generates personalized learning recommendations:
- Skill gaps analysis
- Online course suggestions
- Reading materials
- Project ideas
- Certification paths

---

### ✍️ Application Tools

#### `/coverletter Job Title | Company`
Generates tailored cover letters based on:
- Specific job title and company
- Your CV information
- Industry standards and best practices
- Company research and culture fit

**Format:** `/coverletter [Job Title] | [Company Name]`

**Examples:**
```

/coverletter Software Engineer | Google
/coverletter Marketing Manager| Apple
/coverletter Data Scientist| Remote Company

```

**Features:**
- Customized to job requirements
- Highlights relevant experience
- Professional tone and structure
- Editable template output

---

### 💎 Premium Features

#### `/subscribe`
Shows premium plan options and upgrade process.

**Premium Benefits:**
- Unlimited job searches (vs. 10/month free)
- Up to 5 active job alerts (vs. 1 free)
- Advanced CV templates and analytics
- Priority support
- Full search results access
- Enhanced career insights

---

### ℹ️ Help & Information

#### `/start`
Initializes the bot and displays welcome message with overview.

#### `/help`
Lists all available commands with brief descriptions.

---

## Features

### Smart Job Search
- **Natural Language Processing**: Understands complex queries like "senior python jobs in tech startups"
- **Multi-platform Aggregation**: Searches across major job boards and company career pages
- **Advanced Filtering**: Location, salary, experience level, company size, and more
- **Relevance Scoring**: AI-powered matching based on your profile and preferences

### Professional CV Builder
- **Guided Creation**: Step-by-step process for each CV section
- **Industry Templates**: Field-specific formats (tech, marketing, healthcare, etc.)
- **ATS Optimization**: Ensures compatibility with applicant tracking systems
- **Export Options**: Multiple format support

### Intelligent Matching
- **Profile-based Recommendations**: Suggests jobs matching your skills and experience
- **Company Culture Fit**: Considers work environment preferences
- **Growth Opportunities**: Identifies roles with career advancement potential

### Career Analytics
- **Search Tracking**: Monitors your job search activity and patterns
- **Skill Gap Analysis**: Identifies areas for professional development
- **Market Insights**: Provides industry trends and salary data

---

## For Developers

### Technical Architecture
While Job Autobot is currently Telegram-only, the system is built on:

- **Natural Language Processing**: For understanding job search queries and CV content
- **Machine Learning Models**: For job matching and career path recommendations
- **Data Integration**: Aggregating job listings from multiple sources
- **User Profiling**: Building comprehensive candidate profiles

### Future API Considerations
Potential future endpoints may include:
- Job search integration
- CV parsing and analysis
- Career path recommendations
- Application tracking

### Integration Possibilities
- Career platforms
- Educational institutions
- Recruitment agencies
- HR systems

---

## Pricing & Limits

### Free Plan
- ✅ 10 job searches per month
- ✅ Basic CV building
- ✅ 1 active job alert
- ✅ Standard command access
- ✅ Community support

### Premium Plan ($9.99/month)
- ✅ Unlimited job searches
- ✅ Up to 5 active job alerts
- ✅ Advanced CV templates and analytics
- ✅ Priority support
- ✅ Full search results access
- ✅ Enhanced career insights
- ✅ Early access to new features

---

## Support

### Getting Help
- **In-Bot Support**: Use `/help` for command assistance
- **Email**: support@pluggedspace.org
- **Documentation**: [docs.pluggedspace.org/models/job](https://docs.pluggedspace.org/models/job)
- **Website**: [pluggedspace.org/projects/job](https://pluggedspace.org/projects/job)

### Common Issues
- **Search Limits**: Use `/quota` to check remaining searches
- **CV Building**: Use `/build_cv` for step-by-step guidance
- **Job Alerts**: Use `/myalerts` to manage notifications
- **Premium Features**: Use `/subscribe` for upgrade information

---

## FAQ

### 🤔 How accurate are the job matches?
Job Autobot uses advanced AI algorithms to match your profile with relevant positions, considering skills, experience, preferences, and career goals.

### 💼 Which job boards do you search?
We aggregate from multiple sources including major job boards, company career pages, and specialized platforms to provide comprehensive results.

### 📄 Can I export my CV?
Yes, the CV builder allows export in multiple formats suitable for different applications.

### 🔔 How often do job alerts update?
Alerts check for new positions daily and notify you immediately when matches are found.

### 💰 Is there a free trial for premium?
All users start with free access. Premium features are available through subscription with clear benefits outlined.

### 🔒 Is my data secure?
Yes, we take data privacy seriously. Your personal information and CV data are encrypted and stored securely.

### 📱 Is there a mobile app?
Job Autobot runs entirely within Telegram, which is available on all major mobile platforms.

---

*Last updated: January 2025*  
*Version: 2.1*  
*For the latest updates, visit our documentation site.*
