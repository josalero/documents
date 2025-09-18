# Custom Applicant Tracking System (ATS)
## Technical Documentation

---

## Document Tracking

| Document Title | Date Created | Last Updated | Version | Distribution |
|----------------|--------------|--------------|---------|--------------|
| Custom ATS Technical Documentation | September 17, 2025 | September 17, 2025 | 1.0 | Confidential |
| | | | | |
| | | | | |
| | | | | |

---

## Executive Summary

| Aspect | Description |
|--------|-------------|
| **System Type** | Custom Applicant Tracking System (ATS) |
| **Target Market** | Mid-market companies (100-1000 employees) |
| **Key Differentiators** | AI-powered features, Multi-channel distribution, Cost efficiency |
| **Technology Stack** | Java 24, Spring Boot 3.5.5, PostgreSQL, Keycloak |
| **Primary Use Cases** | Job posting, Candidate management, AI resume analysis, Multi-channel notifications |
| **Competitive Position** | Strong in AI features, competitive pricing, unique multi-channel capabilities |

### Key System Capabilities

| Feature Category | Capabilities | Status |
|------------------|--------------|---------|
| **Core ATS** | Job posting, Candidate management, Application tracking | ✅ Complete |
| **AI Features** | Resume parsing, Skill extraction, Candidate matching | ✅ Complete |
| **Multi-Channel** | Email, Telegram, WhatsApp notifications | ✅ Complete |
| **Security** | OAuth2, JWT tokens, Role-based access | ✅ Complete |
| **Reporting** | Basic metrics, PDF generation | ✅ Complete |
| **Planned Features** | Star ratings, Custom questions | 🚧 In Development |

---

## Table of Contents

1. [Introduction](#1-introduction)
   - 1.1. [Purpose of the Document](#11-purpose-of-the-document)
   - 1.2. [Brief Overview of the Custom ATS](#12-brief-overview-of-the-custom-ats)
   - 1.3. [Context of the ATS Market](#13-context-of-the-ats-market)
2. [Competitor Overview](#2-competitor-overview)
   - 2.1. [JazzHR](#21-jazzhr)
   - 2.2. [BambooHR](#22-bamboohr)
   - 2.3. [Manatal](#23-manatal)
   - 2.4. [Pricing Comparison & Analysis](#24-pricing-comparison--analysis)
   - 2.5. [Value Proposition Analysis](#25-value-proposition-analysis)
3. [Our Custom ATS](#3-our-custom-ats)
   - 3.1. [System Overview](#31-system-overview)
   - 3.2. [In-Scope Features](#32-in-scope-features)
   - 3.3. [Unique Capabilities](#33-unique-capabilities)
   - 3.4. [Out-of-Scope Features](#34-out-of-scope-features)
4. [Covered Scenarios](#4-covered-scenarios)
   - 4.1. [In-Scope Features Comparison](#41-in-scope-features-comparison)
   - 4.2. [End-to-End Workflows Summary](#42-end-to-end-workflows-summary)
5. [Not Covered Scenarios](#5-not-covered-scenarios)
   - 5.1. [Features Available in Competitors but Not Yet Implemented](#51-features-available-in-competitors-but-not-yet-implemented)
6. [ATS Platform Comparison](#6-ats-platform-comparison)
   - 6.1. [Comprehensive Feature Comparison Matrix](#61-comprehensive-feature-comparison-matrix)
   - 6.2. [Competitive Positioning Summary](#62-competitive-positioning-summary)
7. [Planned Development (Next 2 Months)](#7-planned-development-next-2-months)
   - 7.1. [Upcoming Features](#71-upcoming-features)
   - 7.2. [Technical Requirements](#72-technical-requirements)
   - 7.3. [Success Metrics](#73-success-metrics)

---

## 1. Introduction

### 1.1 Purpose of the Document
This document provides a comprehensive technical overview of our custom-built Applicant Tracking System (ATS), designed to facilitate modern recruitment processes.

### 1.2 Brief Overview of the Custom ATS
Our custom ATS is a modern, cost-effective solution that excels in AI integration and multi-channel distribution while providing solid core ATS functionality.

### 1.3 Context of the ATS Market
The Applicant Tracking System market is highly competitive, with established mid-market players like JazzHR, BambooHR, and Manatal serving the mid-market segment.

---

## 2. Competitor Overview

### 2.1 JazzHR

| Aspect | Details |
|--------|---------|
| **Company** | JazzHR (founded 2009) |
| **Target Market** | Mid-market companies (10-500 employees) |
| **Key Strengths** | User-friendly interface, Advanced reporting, Workflow automation |
| **Notable Features** | Custom report builder, Extensive integrations, Strong customer support |
| **Weaknesses** | Limited AI features, Higher cost, Basic automation |

### 2.2 BambooHR

| Aspect | Details |
|--------|---------|
| **Company** | BambooHR (founded 2008) |
| **Target Market** | Small to mid-market companies (1-1000 employees) |
| **Key Strengths** | Complete HR suite, Compliance features, Employee self-service |
| **Notable Features** | All-in-one HR solution, EEO reporting, Benefits administration |
| **Weaknesses** | Limited ATS features, Higher cost, Limited customization |

### 2.3 Manatal

| Aspect | Details |
|--------|---------|
| **Company** | Manatal (founded 2018) |
| **Target Market** | Small to mid-market companies (1-500 employees) |
| **Key Strengths** | AI-powered features, Social media integration, Affordable pricing |
| **Notable Features** | AI candidate recommendations, LinkedIn integration, Smart matching |
| **Weaknesses** | Limited customization, Smaller ecosystem, Basic reporting |

### 2.4 Pricing Comparison & Analysis

| Platform | Plan | Price | Key Features | Target Users | Pricing Model | Free Trial | User Ratings |
|----------|------|-------|--------------|--------------|---------------|------------|--------------|
| **JazzHR** | Hero | $75/month | 3 active jobs, +$9 per additional job | Small teams | Job-based | ❌ No | 4.4/5 (G2) |
| | Plus | $269/month | 200 active jobs, AI matching | Growing companies | | | |
| | Pro | Custom | 200+ jobs, advanced features | Large organizations | | | |
| **BambooHR** | Core | ~$6/employee/month | Basic HR + ATS features | Small teams | Per employee | ✅ 14 days | 4.6/5 (G2) |
| | Pro | ~$8/employee/month | Full HR suite + ATS | Growing companies | | | |
| | Add-ons | Additional cost | Payroll, Benefits, Time Tracking | All plans | | | |
| **Manatal** | Professional | $15/user/month (annual) | 15 jobs, 10K candidates | Small teams | Per user | ✅ 14 days | 4.6/5 (G2) |
| | Enterprise | $35/user/month (annual) | Unlimited jobs/candidates | Growing companies | | | |
| | Enterprise Plus | $55/user/month (annual) | Advanced features + SSO | Large organizations | | | |
| | Custom | Contact | White-label solutions | Enterprise | | | |
| **Our Custom ATS** | Custom | TBD | AI integration, Multi-channel | Mid-market | Custom | TBD | TBD |

### 2.5 Value Proposition Analysis

| Platform | Key Strengths | Best For | Competitive Advantage |
|----------|---------------|----------|----------------------|
| **JazzHR** | User-friendly interface, Advanced reporting, Workflow automation | Mid-market companies needing comprehensive reporting | Job-focused approach, Strong automation |
| **BambooHR** | Complete HR suite, Compliance features, Employee self-service | Companies needing integrated HR and recruiting | All-in-one solution, Strong compliance |
| **Manatal** | AI-powered features, Social media integration, Affordable pricing | Companies focused on AI-powered recruiting | AI-first approach, Social integration |
| **Our Custom ATS** | AI integration, Multi-channel distribution, Cost efficiency | Mid-market companies seeking AI-powered solutions | Unique multi-channel, Superior AI, Cost advantage |

**Pricing Notes:**
- **BambooHR:** Pricing varies by company size; flat rate for <25 employees, per-employee for 25+ employees
- **Volume discounts** available for larger organizations
- **15% discount** for registered nonprofit organizations
- **Add-ons:** Payroll, Benefits Administration, Time Tracking available for additional cost

**User Ratings Sources:**
- **JazzHR:** 4.4/5 on G2 (426+ reviews) - https://www.g2.com/products/jazzhr/reviews
- **BambooHR:** 4.6/5 on G2 (3,074+ reviews) - https://www.g2.com/products/bamboohr/reviews
- **Manatal:** 4.6/5 on G2 (138+ reviews) - https://www.g2.com/products/manatal/reviews
- **Our Custom ATS:** TBD (New platform, no public ratings yet)

**Pricing Information:**
- **JazzHR:** https://www.jazzhr.com/pricing/
- **BambooHR:** https://www.bamboohr.com/pricing/
- **Manatal:** https://www.manatal.com/pricing/

---

## 3. Our Custom ATS

### 3.1 System Overview

| Aspect | Details |
|--------|---------|
| **System Type** | Custom Applicant Tracking System (ATS) |
| **Technology Stack** | Java 24, Spring Boot 3.5.5, PostgreSQL, Keycloak |
| **Target Market** | Mid-market companies (100-1000 employees) |
| **Key Differentiators** | AI-powered features, Multi-channel distribution, Cost efficiency |
| **Deployment** | Cloud-based, Scalable architecture |
| **Security** | OAuth2, JWT tokens, Role-based access control |

### 3.2 In-Scope Features

| Feature Category | Capabilities |
|------------------|--------------|
| **Job Management** | Multi-platform aggregation, CRUD operations, Advanced filtering, Featured job scheduling |
| **Candidate Management** | Profile management, Resume processing, AI analysis, Application tracking |
| **AI & Automation** | Resume parsing, Skill extraction, Automated matching, Content analysis |
| **Communication** | Email notifications, WhatsApp integration, Telegram distribution, Subscription management |
| **Security** | OAuth2 integration, Role-based access control, Multi-tenant architecture |
| **Reporting** | Basic metrics, PDF generation, Analytics integration |

### 3.3 Unique Capabilities

| Capability | Description | Competitive Advantage |
|------------|-------------|----------------------|
| **AI-Powered Resume Analysis** | DeepSeek/OpenRouter integration for advanced skill extraction | Superior to JazzHR and BambooHR |
| **Multi-Channel Distribution** | Telegram and WhatsApp integration for job posting | Unique in the market |
| **Cost Efficiency** | Significantly lower TCO compared to competitors | Major advantage over all competitors |
| **Customization** | Complete control over features and functionality | More flexible than BambooHR |
| **Modern Technology** | Latest Java 24 and Spring Boot 3.5.5 | Performance and security advantages |

### 3.4 Out-of-Scope Features

| Feature Category | Not Included |
|------------------|--------------|
| **Advanced HR Integrations** | Deep HRIS integrations (BambooHR, ADP, Paychex), Payroll system integration |
| **Advanced Analytics** | Predictive analytics, Advanced reporting dashboards, Custom report builder |
| **Enterprise Features** | Advanced workflow automation, Enterprise SSO, Advanced compliance tools |
| **Social Media Integration** | LinkedIn integration, Social media sourcing, Social recruiting tools |

---

## 4. Covered Scenarios

### 4.1 In-Scope Features Comparison

| Feature Category | Our Custom ATS | JazzHR | BambooHR | Manatal |
|------------------|----------------|--------|----------|---------|
| **Job Management** | ✅ Complete | ✅ Complete | ✅ Complete | ✅ Complete |
| **Candidate Management** | ✅ Complete | ✅ Complete | ✅ Complete | ✅ Complete |
| **Application Tracking** | ✅ Complete | ✅ Complete | ✅ Complete | ✅ Complete |
| **Resume Parsing** | ✅ AI-Powered | ⚠️ Basic | ⚠️ Basic | ✅ AI-Powered |
| **AI Features** | ✅ Advanced | ❌ None | ❌ None | ✅ Advanced |
| **Multi-Channel Distribution** | ✅ Unique | ❌ None | ❌ None | ❌ None |
| **Email Notifications** | ✅ Complete | ✅ Complete | ✅ Complete | ✅ Complete |
| **User Management** | ✅ RBAC* | ✅ RBAC* | ✅ RBAC* | ✅ RBAC* |
| **Reporting** | ✅ Basic | ✅ Advanced | ✅ Basic | ⚠️ Limited |
| **API Integration** | ✅ REST API | ✅ REST API | ✅ REST API | ✅ REST API |
| **Customization** | ✅ High | ⚠️ Limited | ❌ None | ⚠️ Limited |
| **Cost Efficiency** | ✅ High | ⚠️ Moderate | ⚠️ Moderate | ✅ High |

*RBAC = Role-Based Access Control: System that restricts access based on user roles (e.g., Admin, Recruiter, HR Manager) with different permission levels for job management, candidate access, and system configuration.

### 4.2 End-to-End Workflows Summary

| Scenario | Description | Key Features | Technical Components |
|----------|-------------|--------------|---------------------|
| **Job Creation & Publishing** | Complete job posting lifecycle | Multi-channel distribution, Analytics | RBAC, URL shortening, Telegram/WhatsApp |
| **Candidate Application** | Application processing and management | AI analysis, Automated notifications | File upload, AI integration, Multi-channel alerts |
| **AI Resume Analysis** | Automated resume processing | Skill extraction, Job matching, Scoring | DeepSeek/OpenRouter APIs, ML algorithms |
| **Candidate-Job Matching** | Intelligent candidate recommendations | Compatibility scoring, Ranking | Advanced algorithms, Real-time processing |
| **Job Alerts & Subscriptions** | Automated notification system | Personalized alerts, Multi-channel delivery | FreeMarker templates, Scheduled processing |
| **Team Collaboration** | Recruiter workflow management | Role assignment, Communication tools | Multi-tenant architecture, RBAC |
| **Compliance & Auditing** | Regulatory compliance features | Audit trails, EEO reporting, Data protection | Comprehensive logging, Privacy controls |

---

## 5. Not Covered Scenarios

### 5.1 Features Available in Competitors but Not Yet Implemented

| Feature | JazzHR | BambooHR | Manatal | Our ATS |
|---------|--------|----------|---------|---------|
| **Advanced Reporting** | ✅ Custom report builder | ⚠️ Limited | ⚠️ Basic | ❌ Basic only |
| **Workflow Automation** | ✅ Advanced workflows | ⚠️ Limited | ✅ AI workflows | ❌ Limited |
| **Social Media Integration** | ⚠️ Basic | ❌ None | ✅ LinkedIn integration | ❌ None |
| **Advanced Analytics** | ✅ Predictive analytics | ⚠️ Basic | ✅ AI analytics | ❌ Basic only |
| **HR Suite Features** | ❌ None | ✅ Complete HR suite | ❌ None | ❌ None |
| **White-Label Solutions** | ✅ Available | ❌ None | ✅ Available | ❌ None |
| **API Marketplace** | ✅ Extensive | ⚠️ Limited | ⚠️ Limited | ❌ None |
| **Advanced Security** | ✅ Enterprise security | ✅ Good | ⚠️ Basic | ⚠️ Basic |
| **Global Deployment** | ✅ Multi-region | ✅ Available | ⚠️ Limited | ❌ Single region |

---

## 6. ATS Platform Comparison

### 6.1 Comprehensive Feature Comparison Matrix

| Feature Category | Custom ATS | JazzHR | BambooHR | Manatal |
|------------------|------------|--------|----------|---------|
| **Core ATS Features** | | | | |
| Job Posting & Management | ✅ **On Par** | ✅ | ✅ | ✅ |
| Candidate Management | ✅ **On Par** | ✅ | ✅ | ✅ |
| Application Tracking | ✅ **On Par** | ✅ | ✅ | ✅ |
| Resume Parsing | ✅ **Ahead** | ⚠️ Limited | ⚠️ Limited | ✅ |
| **AI & Automation** | | | | |
| AI-Powered Matching | ✅ **Ahead** | ❌ | ❌ | ✅ |
| Skill Extraction | ✅ **Ahead** | ❌ | ❌ | ✅ |
| Automated Workflows | ⚠️ **Behind** | ✅ | ⚠️ Limited | ✅ |
| Predictive Analytics | ⚠️ **Behind** | ❌ | ❌ | ✅ |
| **Communication & Distribution** | | | | |
| Multi-Channel Notifications | ✅ **Ahead** | ❌ | ❌ | ❌ |
| Email Templates | ✅ **On Par** | ✅ | ✅ | ✅ |
| Social Media Integration | ⚠️ **Behind** | ⚠️ Limited | ❌ | ✅ |
| Telegram/WhatsApp | ✅ **Ahead** | ❌ | ❌ | ❌ |
| **Reporting & Analytics** | | | | |
| Basic Metrics | ✅ **On Par** | ✅ | ✅ | ✅ |
| Custom Reports | ⚠️ **Behind** | ✅ | ⚠️ Limited | ⚠️ Limited |
| Real-time Dashboards | ⚠️ **Behind** | ✅ | ✅ | ✅ |
| Export Capabilities | ⚠️ **Behind** | ✅ | ✅ | ⚠️ Limited |
| **Integration & Ecosystem** | | | | |
| REST API | ✅ **On Par** | ✅ | ✅ | ✅ |
| Job Board Integration | ⚠️ **Behind** | ✅ | ⚠️ Limited | ✅ |
| HRIS Integration | ⚠️ **Behind** | ✅ | ✅ | ⚠️ Limited |
| Third-party Apps | ⚠️ **Behind** | ✅ | ✅ | ⚠️ Limited |
| **User Experience** | | | | |
| User Interface | ✅ **On Par** | ✅ | ✅ | ✅ |
| Mobile Responsive | ✅ **On Par** | ✅ | ✅ | ✅ |
| Customization | ✅ **Ahead** | ✅ | ❌ | ✅ |
| Ease of Use | ✅ **On Par** | ✅ | ✅ | ✅ |
| **HR Suite Features** | | | | |
| Employee Onboarding | ❌ **Behind** | ❌ | ✅ | ❌ |
| Performance Management | ❌ **Behind** | ❌ | ✅ | ❌ |
| Time Tracking | ❌ **Behind** | ❌ | ✅ | ❌ |
| Benefits Administration | ❌ **Behind** | ❌ | ✅ | ❌ |
| **Pricing & Value** | | | | |
| Cost Structure | ✅ **Ahead** | ⚠️ Moderate | ⚠️ Moderate | ✅ |
| Implementation Time | ✅ **Ahead** | ✅ | ✅ | ✅ |
| Total Cost of Ownership | ✅ **Ahead** | ❌ | ❌ | ✅ |
| **Target Market** | | | | |
| Small Business (<100 employees) | ✅ **Ahead** | ✅ | ✅ | ✅ |
| Mid-Market (100-1000 employees) | ✅ **On Par** | ✅ | ✅ | ✅ |
| Enterprise (1000+ employees) | ⚠️ **Behind** | ❌ | ⚠️ Limited | ❌ |

### 6.2 Competitive Positioning Summary

| Platform | Strengths | Weaknesses | Best For |
|----------|-----------|------------|----------|
| **Our Custom ATS** | AI integration, Multi-channel distribution, Cost efficiency | Limited reporting, Basic automation | Mid-market companies seeking AI-powered solutions |
| **JazzHR** | User-friendly interface, Advanced reporting, Workflow automation | Limited AI features, Higher cost | Mid-market companies needing comprehensive reporting |
| **BambooHR** | Complete HR suite, Compliance features, Employee self-service | Limited ATS features, Higher cost | Companies needing integrated HR and recruiting |
| **Manatal** | Advanced AI features, Social media integration, Affordable pricing | Limited customization, Basic reporting | Companies focused on AI-powered recruiting |

---

## 7. Planned Development (Next 2 Months)

### 7.1 Upcoming Features

| Feature | Description | Timeline | Business Value |
|---------|-------------|----------|----------------|
| **Candidate Star Rating (1-5)** | Rating system for candidate classification | Sep 20 - Oct 10, 2025 | Improved prioritization, Better tracking |
| **Custom Application Questions** | Optional questions added by recruiters | Oct 15 - Nov 15, 2025 | Better screening, Improved matching |

### 7.2 Technical Requirements

| Component | Changes Required |
|-----------|------------------|
| **Database** | Add `rating` column, Create `job_questions` and `application_answers` tables |
| **API Endpoints** | Rating management, Question management, Answer submission |
| **Frontend** | Star rating component, Dynamic question forms, Response display |

### 7.3 Success Metrics

| Feature | Target Metrics |
|---------|----------------|
| **Star Rating** | 90% adoption rate, Rating distribution tracking |
| **Custom Questions** | 80% job posting usage, Completion rate tracking |

---

## Conclusion

Our custom ATS represents a modern, cost-effective solution that excels in AI integration and multi-channel distribution while providing solid core ATS functionality. The system offers comprehensive recruitment capabilities with unique advantages in AI-powered features, multi-channel communication, and customization.

**Key System Strengths:**
- **AI Integration:** Advanced resume analysis and skill extraction using DeepSeek/OpenRouter APIs
- **Multi-Channel Distribution:** Unique Telegram and WhatsApp integration for job distribution
- **Cost Efficiency:** Significantly lower total cost of ownership compared to competitors
- **Customization:** Complete control over features and functionality
- **Modern Technology:** Built with latest Java 24 and Spring Boot 3.5.5

**Strategic Value:**
The system's strengths in AI-powered features, cost efficiency, and customization provide significant competitive advantages, particularly for mid-market companies seeking modern recruitment solutions. Our strategic focus on the mid-market segment, combined with unique AI capabilities and multi-channel distribution, positions the system well for continued growth and market expansion.

---

**Document End**
