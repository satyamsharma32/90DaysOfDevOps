# Day-38 of YML Basic
# Day 38 – YAML Basics

## Objective

Learn YAML syntax, structure, indentation rules, lists, nested objects, multi-line strings, and validation techniques.

---

# Task 1: Key-Value Pairs

## person.yaml

```yaml
name: DevOpsUser
role: DevOps Engineer
experience_years: 2
learning: true
```

### Observation

* YAML uses key-value pairs.
* No tabs should be used.
* Indentation should be done using spaces.

---

# Task 2: Lists

## Updated person.yaml

```yaml
name: DevOpsUser
role: DevOps Engineer
experience_years: 2
learning: true

tools:
  - Docker
  - Kubernetes
  - Jenkins
  - Terraform
  - Git

hobbies: [Reading, Coding, Learning, Gaming]
```

### Two Ways to Write Lists

### Block Style

```yaml
tools:
  - Docker
  - Kubernetes
  - Jenkins
```

### Inline Style

```yaml
tools: [Docker, Kubernetes, Jenkins]
```

---

# Task 3: Nested Objects

## server.yaml

```yaml
server:
  name: app-server
  ip: 192.168.1.10
  port: 8080

database:
  host: db-server
  name: appdb

  credentials:
    user: admin
    password: password123
```

### Observation

* Nested objects use indentation.
* Child keys must be properly aligned.
* YAML is sensitive to spaces.

### Invalid Example (Using Tabs)

```yaml
server:
	name: app-server
	ip: 192.168.1.10
```

### Result

Validation fails because YAML does not allow tabs for indentation.

---

# Task 4: Multi-Line Strings

## Using Pipe (|)

```yaml
startup_script_pipe: |
  echo "Starting application"
  systemctl start nginx
  systemctl start docker
```

### Output

Preserves line breaks exactly as written.

---

## Using Greater Than (>)

```yaml
startup_script_folded: >
  echo "Starting application"
  systemctl start nginx
  systemctl start docker
```

### Output

Converts multiple lines into a single line.

---

### When to Use

| Symbol | Use Case                                          |
| ------ | ------------------------------------------------- |
| |      | Preserve formatting, scripts, configuration files |
| >      | Long descriptions, comments, documentation        |

---

# Task 5: YAML Validation

## Install yamllint

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install yamllint -y
```

Validate files:

```bash
yamllint person.yaml
yamllint server.yaml
```

### Common Error Example

Broken indentation:

```yaml
server:
 name: app-server
    ip: 192.168.1.10
```

Example error:

```text
syntax error: mapping values are not allowed here
```

### Fix

Align indentation correctly and validate again.

---

# Task 6: Spot the Difference

## Correct YAML

```yaml
name: devops

tools:
  - docker
  - kubernetes
```

## Broken YAML

```yaml
name: devops

tools:
- docker
  - kubernetes
```

### What's Wrong?

* List indentation is inconsistent.
* YAML expects all list items at the same indentation level.
* This may cause validation or parsing issues.

### Correct Version

```yaml
name: devops

tools:
  - docker
  - kubernetes
```

---

# What I Learned

1. YAML relies heavily on proper indentation.
2. Lists can be written using block style or inline style.
3. Nested objects help organize structured data.
4. Multi-line strings can use `|` or `>` depending on the requirement.
5. YAML files should always be validated before use in CI/CD pipelines.
6. Tabs should never be used for indentation in YAML files.

---

# Conclusion

YAML is widely used in DevOps tools such as Kubernetes, Docker Compose, GitHub Actions, GitLab CI/CD, Ansible, and Jenkins. Understanding YAML syntax and indentation is essential before working with automation and CI/CD pipelines.

