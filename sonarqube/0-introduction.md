# SonarQube - Simple Explanation for DevOps

* SonarQube is a tool used to analyze code programmatically and check whether the code follows certain quality and security standards. These standards are either predefined or configured by developers. SonarQube is integrated into CI/CD pipelines, and if issues are found, developers are responsible for fixing them.


## ✅ What is SonarQube?

SonarQube is a **tool that checks the quality of your code**.

It looks for:
- Bugs
- Code smells (bad coding practices)
- Security issues
- Duplicate code
- Test coverage (optional)

It does **static code analysis**, which means it checks the code **without running** it.

---

## 🔍 What Does SonarQube Do?

- It checks if the code is following **good practices and standards**.
- These checks are based on **rules**.
- You can use default rules or create **custom rules** as per your project needs.

---

## 👨‍💻 Who Sets These Rules?

- Some rules are already provided by SonarQube.
- Your **team or company** can also add or change rules.
- These rules are grouped into something called a **quality profile**.

---

## ⚙️ How is SonarQube Used in DevOps?

- SonarQube is added into **CI/CD pipelines** (like Jenkins, GitHub Actions, GitLab CI).
- When code is pushed, SonarQube scans it automatically.
- If there are serious issues, it can even **fail the build**.
- This helps catch problems **early** in the development process.

---

## 🛠️ Who Fixes the Issues?

- The **developers** are responsible for fixing any issues found by SonarQube.
- This improves the overall **code quality and security**.

---

## 📝 Simple Summary (Interview-Ready)

> SonarQube is a tool used in CI/CD pipelines to **automatically check the code for bugs, bad practices, and security issues**. It follows a set of rules which can be default or custom. If any issues are found, developers need to fix them.

---

## 📌 Example Use Case

1. Developer writes code and pushes to Git.
2. CI pipeline starts and SonarQube runs.
3. SonarQube scans the code and finds a security bug.
4. The pipeline fails and alerts the developer.
5. Developer fixes the issue and pushes again.

---

