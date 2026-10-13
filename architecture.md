# Web Application Security Assessment — Lab Architecture

## 1. Lab Overview

This project uses OWASP Juice Shop as an intentionally vulnerable web application for authorised security testing in a local lab.

The application runs inside Docker on Kali Linux. I use a browser to interact with the application and Burp Suite Community Edition to inspect HTTP traffic.

## 2. Lab Components

* **Host operating system:** Windows
* **Virtualisation software:** Oracle VirtualBox
* **Security testing operating system:** Kali Linux
* **Container platform:** Docker Engine
* **Target application:** OWASP Juice Shop
* **Application address:** `http://localhost:3000`
* **Browser:** Firefox
* **Web testing proxy:** Burp Suite Community Edition
* **Documentation and version control:** Visual Studio Code and Git

## 3. Traffic Flow

1. The user opens OWASP Juice Shop in a browser running inside Kali Linux.
2. The browser sends HTTP requests to the local application.
3. Docker forwards traffic on port 3000 to the Juice Shop container.
4. Burp Suite will be used to inspect selected requests and responses during testing.
5. Findings and sanitised evidence are recorded in the project repository.

## 4. Scope and Safety

Testing is restricted to the local OWASP Juice Shop instance that I control.

Metasploitable 2 belongs to a separate project and is not part of this assessment.

No public websites, real user accounts, or third-party systems are included in the testing scope.

## 5. Verification

The application was started using Docker and opened in Firefox at `http://localhost:3000`.

Further testing and evidence collection will be documented as the assessment progresses.
