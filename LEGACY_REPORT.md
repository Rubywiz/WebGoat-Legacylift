
WebGoat Architecture Analysis
Java Version
Java 25 (line 77 in pom.xml)
This is a very recent Java version, indicating the project is using cutting-edge Java features
Spring Boot Version
Spring Boot 3.5.6 (line 8 in pom.xml)
Core Architecture
WebGoat follows a multi-module Spring Boot architecture with three main components:

Lesson Categories

Data Layer

WebGoat Application

WebWolf Module

WebGoat Module

StartWebGoat
Main Entry Point

ParentConfig
Shared Configuration

WebGoat Application
Port 8080

Container Layer

Lesson Modules

User Management

Assignment System

Core Services

Security Config

WebWolf Application
Port 9090

Email Mailbox

Request Tracker

JWT Tools

File Server

HSQLDB
In-Memory Database

Flyway
Migration

SQL Injection

XSS

CSRF

Authentication

Access Control

Cryptography

Deserialization

Path Traversal

SSRF

XXE

Module Breakdown
1. Server Module (org.owasp.webgoat.server)
StartWebGoat - Main application entry point
ParentConfig - Shared parent configuration
Orchestrates both WebGoat and WebWolf applications
2. Container Module (org.owasp.webgoat.container)
Core framework providing:

Lesson Management: Lesson loading, tracking, and execution
User Management: Authentication, registration, progress tracking
Assignment System: Exercise validation and scoring
i18n Support: Multi-language support (en, fr, de, nl)
AsciiDoc Integration: Dynamic lesson content rendering
Security Configuration: Spring Security setup
3. WebWolf Module (org.owasp.webgoat.webwolf)
Companion application providing:

Email Mailbox: Simulated email server for lessons
Request Tracker: HTTP request inspection
JWT Tools: JWT token manipulation
File Server: File hosting for exercises
4. Lessons Module (org.owasp.webgoat.lessons)
Contains 20+ security lesson categories covering OWASP Top 10 vulnerabilities

Dependency Analysis
🔴 Critical Vulnerabilities & Outdated Dependencies
1. XStream - CRITICAL VULNERABILITY
<xstream.version>1.4.5</xstream.version>

Status: ⚠️ SEVERELY OUTDATED (Current: 1.4.21+)
Risk: Multiple CVEs including remote code execution
Note: Intentionally vulnerable for lesson purposes (line 108-109)
2. JJWT - OUTDATED
<jjwt.version>0.9.1</jjwt.version>

Status: ⚠️ OUTDATED (Current: 0.12.x)
Risk: Missing security patches and features
Recommendation: Update to 0.12.6+
3. jose4j - OUTDATED
<jose4j.version>0.9.3</jose4j.version>

Status: ⚠️ OUTDATED (Current: 0.9.6+)
Risk: Potential JWT vulnerabilities
4. Commons Collections - ANCIENT
<commons-collections.version>3.2.1</commons-collections.version>

Status: ⚠️ SEVERELY OUTDATED (Released 2008)
Risk: Known deserialization vulnerabilities (CVE-2015-6420)
Note: Likely intentional for deserialization lessons
5. JAXB API - OUTDATED
<jaxb.version>2.3.1</jaxb.version>

Status: ⚠️ OUTDATED (Current: 4.0.x for Jakarta EE)
Recommendation: Migrate to Jakarta XML Binding
6. xml-resolver - ANCIENT
<xml-resolver.version>1.2</xml-resolver.version>

Status: ⚠️ SEVERELY OUTDATED (Released 2006)
Risk: Potential XXE vulnerabilities
🟡 Moderately Outdated Dependencies
7. cglib-nodep
<cglib.version>3.3.0</cglib.version>

Status: 🟡 OUTDATED (Current: 3.3.1)
Risk: Low
8. Lombok
<version>1.18.42</version>

Status: 🟡 SLIGHTLY OUTDATED (Current: 1.18.36+)
Risk: Low
✅ Well-Maintained Dependencies
Spring Boot: 3.5.6 (Recent)
Guava: 33.5.0-jre (Recent)
Commons IO: 2.20.0 (Recent)
Commons Text: 1.14.0 (Recent)
Commons Compress: 1.28.0 (Recent)
Jsoup: 1.19.1 (Recent)
Bootstrap: 5.3.5 (Recent)
jQuery: 3.7.1 (Recent)
Playwright: 1.55.0 (Recent)
WireMock: 3.13.1 (Recent)
Security Considerations
Intentionally Vulnerable Components
The project deliberately includes vulnerable dependencies for educational purposes:

XStream 1.4.5 (for deserialization lessons)
Commons Collections 3.2.1 (for deserialization lessons)
These are marked with comments in pom.xml and pom.xml.

OWASP Dependency Check
The project includes OWASP Dependency Check Maven plugin (line 756-774) with:

CVSS threshold: 7
Suppression file: config/dependency-check/project-suppression.xml
Recommendations
Update JJWT to 0.12.6+ for better JWT security
Update jose4j to 0.9.6+ for JWT improvements
Migrate JAXB to Jakarta XML Binding 4.0.x
Update xml-resolver or replace with modern alternative
Keep intentionally vulnerable dependencies isolated and documented
Regular dependency audits using mvn dependency-check:check
The architecture is well-designed for its educational purpose, with clear separation between the vulnerable lesson environment (WebGoat) and the supporting tools (WebWolf).



🎉
Task Completed
I've analyzed the WebGoat repository's build files and source code. Here are the key findings:

Java Version & Build Configuration
Java 25 (cutting-edge version)
Spring Boot 3.5.6
Maven-based build with comprehensive plugin configuration
Architecture Overview
The application uses a multi-module Spring Boot architecture with three main components:

Server Module - Orchestrates WebGoat and WebWolf applications
WebGoat Module (Port 8080) - Main vulnerable web application with 20+ security lessons
WebWolf Module (Port 9090) - Companion app providing email mailbox, request tracking, JWT tools, and file server
Mermaid Architecture Diagram
Lesson Categories

Data Layer

WebGoat Application

WebWolf Module

WebGoat Module

StartWebGoat
Main Entry Point

ParentConfig
Shared Configuration

WebGoat Application
Port 8080

Container Layer

Lesson Modules

User Management

Assignment System

Core Services

Security Config

WebWolf Application
Port 9090

Email Mailbox

Request Tracker

JWT Tools

File Server

HSQLDB
In-Memory Database

Flyway
Migration

SQL Injection

XSS

CSRF

Authentication

Access Control

Cryptography

Deserialization

Path Traversal

SSRF

XXE

Critical Vulnerabilities & Outdated Dependencies
🔴 Intentionally Vulnerable (For Educational Purposes)
XStream 1.4.5 - Severely outdated, multiple RCE CVEs
Commons Collections 3.2.1 - Ancient (2008), deserialization vulnerabilities
⚠️ Should Be Updated
JJWT 0.9.1 → Update to 0.12.6+
jose4j 0.9.3 → Update to 0.9.6+
JAXB 2.3.1 → Migrate to Jakarta XML Binding 4.0.x
xml-resolver 1.2 → Replace with modern alternative (2006 release)
cglib 3.3.0 → Update to 3.3.1
✅ Well-Maintained
Spring Boot 3.5.6, Guava 33.5.0, Commons IO 2.20.0, Jsoup 1.19.1, Bootstrap 5.3.5, jQuery 3.7.1, Playwright 1.55.0
The project includes OWASP Dependency Check plugin with CVSS threshold of 7 and suppression configuration for known intentional vulnerabilities.

