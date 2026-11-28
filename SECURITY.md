# Security policy

## Supported versions

Ferux is in pre-alpha and has no release yet. Security fixes are made on the `main` branch only. This section will list the supported versions once releases exist.

## Reporting a vulnerability

Please do not report security vulnerabilities through public issues, pull requests or discussions.

Report them privately through GitHub: open the [Security tab](https://github.com/Diafyx/ferux/security) of this repository and choose **Report a vulnerability**, or go directly to the [reporting form](https://github.com/Diafyx/ferux/security/advisories/new).

Please include:

- the affected component and the Ferux commit or version;
- a description of the problem and its impact;
- steps to reproduce it, or a proof of concept;
- any known way to avoid or limit the problem.

## What to expect

- You will receive an acknowledgement within 14 days.
- The report is investigated, and you are kept informed of the progress.
- Once a fix is available, a security advisory is published, and you are credited unless you ask not to be.

Please keep the details private until the advisory is published.

## Scope

Examples of security issues in Ferux:

- `unsafe` code that can break memory safety;
- a way for code to gain more privileges than it should have;
- information leaking across isolation boundaries;
- weaknesses in the build or release process, such as a release image that does not match its source.
