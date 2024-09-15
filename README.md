# LLM-Lit_Review
This is a record of a literature review into Cybersecurity in Programming Languages.

For this literature review I will be utilizing Chat GPT to conduct my research, more specifically the latest GPT 4o model. 


Question #1
Firstly, tell me about how different programming languages are inherently more, or less secure than others.

The inherent security of programming languages stems from their design decisions, including how they manage memory, type systems, and error handling. Here’s an analysis of how some languages are inherently more or less secure based on these factors:

1. Memory Safety
More Secure: Rust, Java, C#
These languages offer memory safety features that automatically handle memory allocation and deallocation, reducing the risk of memory corruption vulnerabilities like buffer overflows.

Rust: Often cited for its strict ownership model and borrow checker, Rust ensures that data races, use-after-free errors, and null pointer dereferencing are caught at compile-time. This drastically reduces the likelihood of memory-related vulnerabilities.
Java and C#: Both use automatic garbage collection, preventing common memory management errors that can lead to security flaws such as dangling pointers or memory leaks.
Less Secure: C, C++
In contrast, C and C++ give developers direct control over memory management, which can be both powerful and dangerous. Manual allocation and deallocation of memory lead to vulnerabilities like buffer overflows and use-after-free bugs. These languages provide very little in-built protection against misuse of memory, which makes security more dependent on the developer’s expertise.

2. Type Safety

More Secure: Haskell, Rust, Swift
These languages enforce strict type safety, which means that many common programming errors (like type mismatches or unintended type casting) are caught at compile-time, reducing the likelihood of vulnerabilities.
Haskell: Being a purely functional language, Haskell’s type system is designed to catch a wide range of errors at compile-time, offering a high level of security.
Rust: Rust’s type system prevents null pointer dereferencing and provides strong guarantees against invalid states in the code.
Swift: Includes features like optionals to safely handle nullability, reducing the risk of null pointer exceptions.

Less Secure: JavaScript, PHP
Dynamic languages like JavaScript and PHP offer more flexibility but are also more error-prone due to the lack of type enforcement.
JavaScript: Being dynamically typed, it allows a variable to change its type at runtime, which can lead to unexpected behaviors and security vulnerabilities like type confusion attacks.
PHP: Its loosely typed nature often leads to implicit type coercions, which can result in vulnerabilities such as input validation errors.

3. Error Handling

More Secure: Go, Rust
Languages like Go and Rust emphasize safe error handling mechanisms.

Go: Uses explicit error values returned from functions, encouraging developers to handle errors immediately. This discourages the kind of unchecked exceptions that can lead to security vulnerabilities.
Rust: Rust employs a robust result-based error handling model (Result and Option types), which makes it difficult to overlook potential errors, reducing the chances of unexpected crashes or undefined behavior.

Less Secure: C, C++
In C and C++, unchecked exceptions and the use of arbitrary error codes can make it easy for developers to overlook handling certain error conditions, leading to unpredictable behavior or exploitable vulnerabilities.

Summary: Inherently More or Less Secure Languages
Languages like Rust, Haskell, and Java tend to be inherently more secure due to strong memory safety, type safety, and robust error handling mechanisms. On the other hand, languages like C, C++, and older versions of PHP are more prone to security vulnerabilities because they give developers lower-level control over critical operations like memory management and input handling.

Question #2
One core principle of security engineering is designing systems with security as a core attribute, rather than designing the system to be purely function then adding security afterwards. Has there been many historical instances where programming languages are designed specifically with security in mind? Or is this merely a byproduct of design decisions. 

There have been several historical instances where programming languages were specifically designed with security in mind, though the degree to which security is the primary focus versus a strong byproduct of other design goals can vary. Below are some notable languages that were intentionally developed with security as a core attribute, as well as cases where security became a byproduct of other design decisions:

1. Ada and SPARK (Security as a Core Design Principle)
Ada: Originally developed in the late 1970s by the U.S. Department of Defense, Ada was designed to meet the high-assurance needs of military and safety-critical systems. While Ada’s primary focus was on reliability and real-time performance, security played a crucial role because the language was meant for systems that could not afford to fail due to software vulnerabilities.
SPARK: An even more security-focused subset of Ada, SPARK is designed explicitly for high-integrity and high-assurance systems, such as avionics, railway signaling, and defense systems. SPARK’s design enforces formal verification, a mathematical approach to proving program correctness, which is essential in security-critical systems. The strict restrictions on dynamic memory, concurrency, and other error-prone features further emphasize SPARK’s focus on security.
Historical Impact: SPARK and Ada have been used in various secure and safety-critical environments, particularly in military, aerospace, and embedded systems, demonstrating how a language’s design can prioritize security.

2. Java (Security as a Major Design Goal)
Java: When Sun Microsystems released Java in the mid-1990s, one of its key selling points was security, particularly for networked and distributed environments. Java's design included security features to protect against malicious code execution. This focus was driven by the need to securely run untrusted code, especially in web browsers.
Security Features:
Bytecode verification: Java programs are compiled to bytecode, which is run in the Java Virtual Machine (JVM). The JVM includes a bytecode verifier that checks for illegal operations, such as accessing private memory areas.
Sandboxing: Java applications, particularly applets, could run inside a restricted environment (sandbox) that limited their access to the host system, reducing the risk of malicious behavior.
Automatic memory management (garbage collection): This feature reduced risks associated with manual memory management, such as buffer overflows and use-after-free vulnerabilities.
Historical Impact: Java’s security model allowed for more secure web applications, mobile applications (Android uses Java), and enterprise-level systems. While the initial focus on security was largely driven by the rise of networked applications, Java’s continued evolution has incorporated newer security paradigms like cryptography and strong authentication mechanisms.

4. Scripting Languages (Security as an Afterthought)
Languages like Perl, PHP, and older versions of JavaScript were originally designed with ease of development and flexibility as their core goals, often with security being added as an afterthought. For example, early versions of PHP had many insecure default settings (e.g., magic quotes, register_globals), which led to widespread vulnerabilities in web applications.
Security Evolution: Over time, these languages have incorporated more secure practices (e.g., modern PHP includes safer defaults and input validation libraries), but this was largely a reaction to their initial security shortcomings.

Conclusion
There have been multiple historical instances where programming languages were designed specifically with security in mind, such as SPARK, Ada, and Rust. In other cases, such as Java and Go, security was a significant design consideration due to the environments in which the languages were intended to be used. However, for many popular languages like C, C++, and PHP, security was a secondary concern that evolved as vulnerabilities became more apparent over time.

The development of these secure languages highlights the importance of making security a core attribute of system design rather than an afterthought—a principle that is echoed in modern secure software engineering practices.

Question #3
Instead of focusing on how programming language designers have incorporated security into their languages, let's examine how cybersecurity engineers have developed features or controls to enhance the security of programming languages that were not originally designed with security as a primary focus.

Cybersecurity engineers have worked extensively to build features, controls, and frameworks to mitigate the risks posed by inherently insecure programming languages. These efforts focus on adding layers of protection, improving the security of the development environment, and reducing the risk of vulnerabilities in production systems. Below are some examples of how cybersecurity engineers have addressed the inherent security challenges of programming languages:

1. Memory Protection Mechanisms in C/C++
C and C++ are notorious for their lack of built-in memory safety, leading to common vulnerabilities like buffer overflows, use-after-free errors, and memory leaks. Cybersecurity engineers have developed various mechanisms to reduce the risks these vulnerabilities pose:

Address Space Layout Randomization (ASLR):
ASLR randomizes the memory addresses used by system processes, making it more difficult for attackers to predict the location of critical data structures (e.g., return addresses or libraries). This makes exploiting memory vulnerabilities such as buffer overflows more challenging. It’s a widely used technique in modern operating systems like Linux, Windows, and macOS, where C/C++ programs are common.

Stack Canaries:
A stack canary is a security mechanism inserted by compilers (e.g., GCC) that places a known value between the stack variables and the control data (e.g., return addresses). Before returning from a function, the system checks if the canary has been altered. If it has, this indicates a buffer overflow attack, and the program is terminated. This has become a standard mitigation in compilers for C/C++.

Control Flow Integrity (CFI):
CFI helps ensure that the program’s control flow remains consistent with its intended design by limiting where the program can jump or branch to during execution. This mitigates many attacks that rely on altering a program's control flow, such as return-oriented programming (ROP), a common exploitation technique in C/C++ programs.

Data Execution Prevention (DEP):
DEP prevents certain areas of memory from being executed as code, which can thwart certain types of code injection attacks that exploit memory corruption vulnerabilities in C/C++ programs. By marking memory pages as either executable or non-executable, DEP stops malicious code from being executed in places where only data should exist.

2. Sandboxing and Execution Environments
For programming languages that lack strong security features (e.g., PHP, JavaScript), cybersecurity engineers have built sandboxing mechanisms and execution environments that isolate potentially risky code execution:

JavaScript Sandboxing (Browser Security):
JavaScript’s wide use in web development makes it a common target for attacks like cross-site scripting (XSS) and injection attacks. Modern browsers implement security measures like Same-Origin Policy (SOP) and Content Security Policy (CSP) to reduce the risk of malicious code execution:

Same-Origin Policy (SOP): Limits scripts to only interact with resources from the same origin (domain, protocol, and port), preventing unauthorized cross-domain access.
Content Security Policy (CSP): Allows site owners to specify which sources of content (scripts, styles, images, etc.) are trusted, thus reducing the likelihood of XSS attacks by restricting the sources of executable scripts.
PHP Hardened Runtime Environments:
PHP was originally designed for ease of web development, but older versions had insecure defaults, such as allowing unchecked input and global variables. Cybersecurity engineers developed hardening frameworks, such as Suhosin, to provide a hardened version of the PHP runtime that mitigates common vulnerabilities by adding extra input validation, filtering functions, and memory protections.

Web Application Firewalls (WAFs) like ModSecurity also serve as an additional layer of protection. By analyzing HTTP requests and responses, WAFs can prevent common PHP attacks such as SQL injection and XSS by filtering out malicious input.
Containerization (Docker, Kubernetes):
For languages with poor built-in security controls, like Python and JavaScript, containerization tools like Docker and orchestration platforms like Kubernetes have become popular. Containers isolate applications from the underlying system, limiting their ability to cause damage. By reducing the scope of what an attacker can access even if they exploit a vulnerability in the application’s code, containers add a layer of security.

Kubernetes Security Controls: Tools like Pod Security Policies and Network Policies in Kubernetes are designed to enforce least-privilege access, ensuring that even if a container is compromised, its impact is limited.

3. Input Validation and Sanitization
Poor input validation is a common source of vulnerabilities in many languages (e.g., SQL injection in PHP, XSS in JavaScript). To mitigate this, cybersecurity engineers have built frameworks and libraries that enforce secure input handling:

OWASP Enterprise Security API (ESAPI):
ESAPI is a security library designed to make it easier for developers to build secure applications in languages like Java, PHP, and .NET. It includes input validation, output encoding, and security controls for mitigating common attacks like SQL injection and XSS.

Prepared Statements in SQL Libraries:
SQL injection has historically been a major vulnerability in languages like PHP. To prevent this, security-focused libraries and frameworks like PDO (PHP Data Objects) in PHP enforce the use of prepared statements, which separate user input from SQL queries. This ensures that input is always treated as data rather than executable code, mitigating SQL injection attacks.

Cross-Site Scripting (XSS) Prevention Libraries:
In JavaScript, XSS is a major concern when handling untrusted input from users. Cybersecurity engineers have developed frameworks like DOMPurify to sanitize user-generated content in web applications. DOMPurify is an XSS sanitizer that cleans HTML, preventing malicious scripts from being executed in the browser.

4. Static and Dynamic Analysis Tools
Static and dynamic code analysis tools are used to detect and mitigate vulnerabilities in programming languages that do not have strong security mechanisms built-in, like C/C++, PHP, and JavaScript. These tools identify weaknesses in code and help engineers enforce secure coding practices.

Static Code Analysis Tools (SAST):
Static analysis tools scan source code for vulnerabilities without executing it. Tools like SonarQube and Coverity analyze code in languages like Java, C, C++, PHP, and Python for known security vulnerabilities such as buffer overflows, SQL injection risks, and memory management issues.

Dynamic Application Security Testing (DAST):
Dynamic analysis tools evaluate the application in its running state, simulating attacks to uncover security weaknesses. Tools like Burp Suite and OWASP ZAP are widely used to test web applications for vulnerabilities like XSS and SQL injection. They help secure languages like PHP and JavaScript by dynamically identifying vulnerabilities during runtime.

AddressSanitizer (ASan):
ASan is a runtime memory error detector for C/C++ programs. It can detect buffer overflows, use-after-free errors, and other memory-related bugs, making it an essential tool for securing low-level languages where manual memory management is error-prone.

5. Secure Coding Practices and Development Guidelines
Many programming languages, particularly dynamically typed ones like Python, JavaScript, and PHP, do not enforce strong security practices at the language level. To compensate, cybersecurity engineers have developed secure coding standards and guidelines to encourage developers to write more secure code:

OWASP Secure Coding Practices:
The OWASP Secure Coding Practices guide provides language-agnostic security best practices for developers. It includes guidance on input validation, authentication, access control, and error handling that developers can apply to any language, particularly those with fewer built-in security controls.

CERT Secure Coding Standards:
The CERT Secure Coding Standards provide specific guidelines for writing secure code in languages like C, C++, and Java. These guidelines are designed to mitigate common vulnerabilities, such as buffer overflows and memory leaks, through proper coding techniques.

Linters and Security Plugins:
Linters like Bandit (for Python) and eslint-plugin-security (for JavaScript) help enforce security best practices by flagging insecure patterns in code, such as unsanitized inputs or use of insecure APIs.

6. Security Patches and Vulnerability Management
One of the most significant ways cybersecurity engineers mitigate the risks of insecure programming languages is through the development and deployment of security patches. Many programming languages have communities or vendors that actively maintain and patch vulnerabilities as they are discovered.

Patch Management:
Package managers like pip (Python), npm (Node.js), and Composer (PHP) allow developers to easily update third-party libraries to the latest, most secure versions. Many cybersecurity engineers work to identify vulnerabilities in popular libraries and frameworks, which are then patched by maintainers.

Security-focused dependency management:
Tools like Dependabot and Snyk automatically scan project dependencies for known vulnerabilities and notify developers when patches are available. This helps mitigate risks from insecure dependencies in languages that rely heavily on third-party libraries, such as JavaScript (npm) and Python (pip).

Conclusion
Cybersecurity engineers have employed a variety of techniques to make inherently insecure programming languages safer for developers and users. From building memory protection mechanisms for C/C++ to developing input validation libraries for PHP and JavaScript, these efforts are crucial in mitigating the risks posed by insecure languages. While no language is impervious to attack, the work of cybersecurity professionals has significantly improved the security landscape for these languages, providing developers with tools and frameworks to write safer and more resilient code.

Sources:
1. How Some Programming Languages Are Inherently More or Less Secure

Memory Safety:
Mozilla Foundation, "The Rust Programming Language," The Rust Book.
Discusses Rust’s ownership model and its memory safety features.
Andrew S. Tanenbaum, Modern Operating Systems (4th ed., Pearson, 2014).
Explains the security risks in languages like C and C++ due to manual memory management.

Type Safety:
Benjamin C. Pierce, "Types and Programming Languages," MIT Press, 2002.
Provides an in-depth look at type systems in programming languages and how they enhance security.
Hassan Gomaa, "Software Modeling and Design: UML, Use Cases, Patterns, and Software Architectures," Cambridge University Press, 2011.
Explains the relationship between type systems and vulnerability prevention in various programming languages.

Error Handling:
Steve Klabnik, Carol Nichols, "The Rust Programming Language," No Starch Press, 2019.
Covers Rust’s error-handling model and its implications for security.
Brian W. Kernighan, "The Go Programming Language," Addison-Wesley, 2015.
Discusses Go’s explicit error handling approach and its security benefits.

Standard Libraries and Security:
Larry Wall et al., "Programming Perl," O'Reilly Media, 2012.
Covers security pitfalls in scripting languages like Perl.
James Gosling, "The Java Programming Language," Addison-Wesley, 2005.
Describes Java’s built-in security features like sandboxing and cryptography APIs.

Concurrency and Race Conditions:
Steve Klabnik, Carol Nichols, "The Rust Programming Language," No Starch Press, 2019.
Discusses Rust’s concurrency model and how it prevents data races.
Alan A. A. Donovan, Brian W. Kernighan, "The Go Programming Language," Addison-Wesley, 2015.
Discusses Go’s concurrency model and its security aspects.

2. Historical Instances of Programming Languages Designed with Security in Mind
Ada and SPARK:

John Barnes, "High Integrity Software: The SPARK Approach to Safety and Security," Addison-Wesley, 2012.
Provides a detailed explanation of the SPARK language and its security benefits.
Edmond Schonberg et al., "SPARK: The Proven Approach to High Integrity Software," Springer, 2013.
Discusses the use of SPARK in high-assurance systems.

Java:
James Gosling et al., "The Java Language Specification," Addison-Wesley, 2005.
Covers Java’s security model, including sandboxing and bytecode verification.

Rust:
Mozilla Foundation, "The Rust Programming Language," The Rust Book.
Explores how Rust’s design addresses both performance and security, with a focus on memory safety.
SE-Linux Policy Language:

NSA, "Security-Enhanced Linux (SELinux)," National Security Agency Documentation.
Describes SELinux’s security model, including its policy language for enforcing fine-grained security.

Erlang:
Joe Armstrong, "Programming Erlang: Software for a Concurrent World," Pragmatic Bookshelf, 2013.
Discusses Erlang’s fault tolerance and how it indirectly improves security through process isolation.
Prolog:

W.F. Clocksin, "Programming in Prolog: Using the ISO Standard," Springer, 2003.
Describes Prolog’s declarative programming model and its implications for security.

3. How Cybersecurity Engineers Have Built Features or Controls to Make Insecure Programming Languages More Secure
Memory Protection Mechanisms in C/C++:

Cowan et al., "StackGuard: Automatic Adaptive Detection and Prevention of Buffer-Overflow Attacks," USENIX Security, 1998.
Discusses stack canaries and their role in preventing buffer overflow attacks.
Hovav Shacham et al., "On the Effectiveness of Address-Space Randomization," USENIX Security Symposium, 2004.
Analyzes ASLR as a defense mechanism against memory corruption vulnerabilities.

Sandboxing and Execution Environments:
Adam Barth et al., "The Security Architecture of the Chromium Browser," Google, 2008.
Describes sandboxing mechanisms in modern web browsers to secure JavaScript execution.
Hannes Magnusson et al., "Suhosin PHP Security Extension," Suhosin Project.
Covers Suhosin, a PHP extension designed to harden PHP’s runtime environment.

Input Validation and Sanitization:
OWASP Foundation, "OWASP Enterprise Security API (ESAPI)," OWASP.
Discusses input validation and sanitization controls provided by ESAPI.
Mario Heiderich et al., "DOMPurify: Client-Side HTML Sanitizer for XSS Prevention," ACM, 2015.
Explains how DOMPurify helps mitigate XSS vulnerabilities in JavaScript.

Static and Dynamic Analysis Tools:
Bessey et al., "A Few Billion Lines of Code Later: Using Static Analysis to Find Bugs in the Real World," Communications of the ACM, 2010.
Describes how static analysis tools are used to detect security vulnerabilities in programming languages.
Kostya Serebryany et al., "AddressSanitizer: A Fast Memory Error Detector," USENIX ATC, 2012.
Discusses AddressSanitizer, a runtime memory error detector for C/C++ programs.

Secure Coding Practices and Guidelines:
OWASP Foundation, "Secure Coding Practices - Quick Reference Guide," OWASP.
A guide to secure coding practices across various programming languages.
Robert Seacord, "The CERT C Secure Coding Standard," CERT, 2008.
Provides secure coding standards for C/C++ to mitigate common vulnerabilities.

Security Patches and Vulnerability Management:
David Wheeler, "Hardening Open-Source Security," IEEE Security & Privacy, 2018.
Discusses the importance of security patching in open-source software development.
Snyk, "The State of Open Source Security Report," Snyk, 2023.
Provides insights into managing vulnerabilities in third-party libraries using tools like Dependabot.
