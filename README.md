# 🧑‍💻 Graduate Trainee Program (DevOps) – Assessment Submission

## 🚀 Task Overview
This project demonstrates the setup and configuration of a **self-hosted GitHub Actions runner** on my local PC. The goal was to enable GitHub workflows to execute jobs directly on my machine rather than GitHub’s cloud-hosted runners.

As a **bonus**, I also created and ran a **test pipeline** successfully using the self-hosted runner.

---

## 🛠️ Step-by-Step Implementation

### **1. Repository Setup**
- Created a new GitHub repository named `self-hosted-runner-setup`.
- Initialized it with a basic GitHub Actions workflow file `.github/workflows/test.yml`.

### **2. Setting Up the Self-Hosted Runner**
1. Navigated to **Settings → Actions → Runners** on the repository.
2. Clicked **“Add runner”** and selected my operating system (Windows/Linux).
3. Followed the on-screen instructions to:
   - Download the runner package using `curl` or browser.
   - Extract it and configure it using my repository’s unique token:
     ```bash
     ./config.sh --url https://github.com/<username>/<repo> --token <generated_token>
     ```
   - Started the runner service:
     ```bash
     ./run.sh
     ```
4. Confirmed that the runner appeared as **“online”** in my GitHub repository settings.

---

### **3. Bonus: Running a Test Pipeline**
Created a simple workflow file `.github/workflows/test.yml` to verify the runner:

```yaml
name: Test Self-Hosted Runner

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: self-hosted
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run a simple test
        run: echo "✅ Self-hosted runner is working successfully!"
```

✅ **Result:** The workflow executed successfully, confirming the self-hosted runner was configured and functional.

---

## 🧩 Challenges Faced & Solutions

| **Challenge** | **Description** | **Solution** |
|----------------|----------------|---------------|
| Runner Registration Issues | Initially, the runner failed to authenticate with GitHub. | Re-generated the token from GitHub Actions settings and reconfigured the runner. |
| Permission Errors | Some scripts required elevated permissions. | Ran the setup with administrative privileges (Linux: `sudo`, Windows: Admin CMD). |
| Firewall Restrictions | Local firewall blocked GitHub connection. | Allowed outgoing connections to GitHub Actions domains. |

---

## 🧠 What I Would Do Differently in Production

- **Use a Dedicated Server or VM:** Instead of a local PC, I’d deploy runners on a secure, dedicated cloud instance (AWS EC2, Azure VM, or GCP Compute Engine).
- **Implement Auto-Scaling:** Integrate multiple runners and enable auto-scaling for concurrent workflows.
- **Monitoring & Logging:** Use tools like **Prometheus** and **Grafana** to monitor runner performance and job success rates.
- **Containerization:** Run self-hosted runners inside Docker containers for better isolation and portability.

---

## 🔒 Security Considerations

- **Restricted Permissions:** Used repository-level tokens, not organization-wide tokens.
- **Local Isolation:** Runner was configured in a sandboxed environment to prevent system-wide access.
- **Secret Management:** No plain-text secrets were stored — environment variables and GitHub Secrets were used instead.
- **Network Security:** Verified that all communications occurred over HTTPS to ensure data integrity.

---

## 📎 Repository Link
🔗 [GitHub Repository – Self-Hosted Runner Setup](https://github.com/ajalaadetola/self-hosted-runner-setup.git)

---

## 🏁 Conclusion
This assessment provided hands-on experience with **GitHub Actions**, **runner configuration**, and **CI/CD pipeline testing**. It also strengthened my understanding of **automation**, **security best practices**, and **production-grade DevOps workflows**.
