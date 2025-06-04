## Generally the workflow of deployment is
* App-code –Build----> artifact----->Deploy

## What is an Application Build?

An **application build** is the process of converting source code into a deployable software artifact. This build artifact can then be deployed across various environments such as:

- Development (`dev`)
- Testing (`test`)
- Production (`prod`)
- Pre-Production (`pre-prod`)
- User Acceptance Testing (`uat`)
- Demonstration (`demo`)

### Typical Steps in the Build Process (Java Example)

- Ensure proper **project folder structure**.
- Download all required **dependencies**.
- Copy those dependencies into the project.
- **Compile** the source code.
- **Execute** unit/integration tests.
- Package the code into an artifact (e.g., `.jar`, `.war`, etc.).
- Optionally, **deploy** the artifact to a target environment.

---

## Common Build Tools

| Language / Platform | Build Tools                  |
|---------------------|------------------------------|
| Java                | Ant, Maven, Gradle           |
| .NET                | NAnt, MSBuild                |
| Node.js             | npm (with scripts), Webpack  |

---
