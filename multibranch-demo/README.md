```md
# Jenkins Multibranch Pipeline – Hands-on Guide

This project demonstrates how to create, configure, and trigger a Jenkins Multibranch Pipeline using Git branches.

---

## Repository Structure

```

jenkins/
├── multibranch-demo/
│   ├── Jenkinsfile
│   └── README.md
│
└── README.md

```

The `Jenkinsfile` is stored inside the repository so Jenkins can automatically detect and execute it for each branch.

---

## Branches Used

This demo uses the following branches:

- `main` – production-ready branch
- `dev` – development branch
- `feature` – feature development branch

Each branch runs the same Jenkinsfile but as a separate pipeline.

---

## Step 1: Create Jenkins Multibranch Pipeline Job

1. Open Jenkins UI
2. Click **New Item**
3. Enter job name (example: `multibranch-demo`)
4. Select **Multibranch Pipeline**
5. Click **OK**

---

## Step 2: Configure Branch Source

In **Branch Sources**:

- Source: **Git**
- Repository URL:
```

[https://github.com/](https://github.com/)<username>/<repo>.git

```
- Credentials:
- `None` (for public repo)
- GitHub PAT (for private repo)

---

## Step 3: Enable Branch Discovery

In **Behaviors** section:

1. Click **Add**
2. Select **Discover branches**

> In newer Jenkins versions, adding “Discover branches” automatically means all branches will be discovered.

(Optional)
You may also add:
- Filter by name (with wildcard)
```

main dev feature*

```

---

## Step 4: Configure Jenkinsfile Path

In **Build Configuration**:

- Mode: `by Jenkinsfile`
- Script Path:
```

multibranch-demo/Jenkinsfile

````

This tells Jenkins where the Jenkinsfile exists inside the repo.

---

## Step 5: Save and Scan

1. Click **Save**
2. Click **Scan Multibranch Pipeline Now**

Jenkins will automatically:
- Detect all branches
- Create separate jobs for `main`, `dev`, and `feature`
- Run the pipeline for each branch

---

## Step 6: Trigger Builds (Ways to Trigger)

### Method 1: Push Code (Recommended)

Any commit pushed to a branch triggers its pipeline:

```bash
git checkout feature
git commit -m "Feature update"
git push origin feature
````

---

### Method 2: Jenkins UI Scan

From Jenkins:

* Open the multibranch job
* Click **Scan Multibranch Pipeline Now**

This triggers all branch pipelines.

---

### Method 3: Empty Commit (Manual Trigger)

```bash
git checkout main
git commit --allow-empty -m "Trigger build"
git push origin main
```

## Jenkins Multibranch Behavior

* Each branch has its own pipeline
* Same Jenkinsfile, different execution context
* Build history is maintained per branch
* Failures in feature branch do not affect main branch

