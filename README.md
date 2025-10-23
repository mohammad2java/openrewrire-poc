

# openrewrire-poc:

### 🧩 **What is OpenRewrite?**

**OpenRewrite** is an **automated refactoring and modernization tool** that helps developers **upgrade, migrate, and clean up codebases** safely and consistently across large projects.

It works by using **predefined or custom recipes** (rules) to automatically modify source code, configuration files, and dependencies — without changing the business logic.

---

### ⚙️ **In simple terms**

It’s a **tool that converts or modernizes legacy applications** to new frameworks, libraries, or language versions (like upgrading from Spring Boot 2.x to 3.x, or Java 8 to Java 17).

---

### 🧠 **Key Features**

* 🪄 **Automated Refactoring** — Applies large-scale code transformations with precision.
* 🔄 **Framework Upgrades** — Helps migrate across framework versions (e.g., Spring, Hibernate, Micronaut).
* 🧰 **Dependency Updates** — Updates `pom.xml` or `build.gradle` automatically.
* 🧼 **Code Cleanup** — Removes unused imports, fixes deprecated APIs, and standardizes formatting.
* 🧱 **Custom Recipes** — You can define your own migration rules.

---

### 💡 **Example Use Cases**

| Use Case                 | Example                                      |
| ------------------------ | -------------------------------------------- |
| Upgrade frameworks       | Spring Boot 2.x → 3.x                        |
| Upgrade Java versions    | Java 8 → Java 17                             |
| Cloud migrations         | Jakarta EE → Spring Boot                     |
| Dependency modernization | Log4j → Logback                              |
| Code style enforcement   | Enforce naming conventions, formatting, etc. |

---

### 🧰 **Supported Environments**

You can run OpenRewrite:

* via **Maven Plugin**
* via **Gradle Plugin**
* via **CLI (Command Line Tool)**
* via **Java API** (for custom automation)
* via **Rewrite Cloud / Hub** (for large-scale or team use)

---

Let’s walk through a **real working example** of running **OpenRewrite (Maven plugin)** to upgrade a Spring Boot project from **2.x → 3.x**.

---

## 🚀 Goal

We’ll use the OpenRewrite recipe
`org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_2`
to automatically upgrade your project’s code and dependencies to **Spring Boot 3.2**.

---

## 🧩 Step 1: Add the OpenRewrite Maven Plugin

Add this inside your project’s `pom.xml` (usually under `<build><plugins>`):

```xml
<plugin>
  <groupId>org.openrewrite.maven</groupId>
  <artifactId>rewrite-maven-plugin</artifactId>
  <version>6.8.0</version>
  <configuration>
    <activeRecipes>
      <!-- Upgrade from Spring Boot 2.x to 3.2 -->
      <recipe>org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_2</recipe>
    </activeRecipes>
  </configuration>
  <dependencies>
    <!-- Add Spring recipes -->
    <dependency>
      <groupId>org.openrewrite.recipe</groupId>
      <artifactId>rewrite-spring</artifactId>
      <version>5.22.0</version>
    </dependency>
  </dependencies>
</plugin>
```

---

## 🧱 Step 2: (Optional) Add to `<pluginManagement>` if you use parent POMs

If your project inherits from another POM, add it in `<pluginManagement>` so it’s available to all modules.

---

## 🧠 Step 3: Check available recipes

Run this command from your terminal to list available Spring-related recipes:

```bash
mvn rewrite:discover
```

You’ll see a large list — including ones like:

* `org.openrewrite.java.spring.boot2.UpgradeSpringBoot_2_7`
* `org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_0`
* `org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_2` ✅

---

## 🧪 Step 4: Preview the changes

Before applying, always dry-run:

```bash
mvn rewrite:dryRun
```

This generates a report (in `target/rewrite/rewrite.patch`) showing what will change, without touching your code yet.

---

## 🧰 Step 5: Apply the recipe

If the dry run looks good, run:

```bash
mvn rewrite:run
```

Now OpenRewrite will:

* Update your `pom.xml` dependencies to Spring Boot 3.2
* Change deprecated Spring Boot APIs to their 3.x equivalents
* Update `javax.*` imports to `jakarta.*` where needed
* Refactor configuration classes, annotations, and method signatures

---

## 📂 Step 6: Review and verify

After running:

1. Check your code changes using `git diff`
2. Run your tests to confirm everything still works:

   ```bash
   mvn clean test
   ```
3. If you’re using Spring Boot parent, make sure the version in your parent `pom.xml` reflects the upgrade:

   ```xml
   <parent>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-parent</artifactId>
     <version>3.2.0</version>
   </parent>
   ```

---

## ✅ Summary

| Step | Command                | Description                     |
| ---- | ---------------------- | ------------------------------- |
| 1    | Add plugin             | Add OpenRewrite plugin + recipe |
| 2    | `mvn rewrite:discover` | List available recipes          |
| 3    | `mvn rewrite:dryRun`   | Preview changes                 |
| 4    | `mvn rewrite:run`      | Apply refactorings              |
| 5    | `mvn clean test`       | Verify functionality            |

-----



## official quick start----------------------
 https://docs.openrewrite.org/running-recipes/getting-started#step-2-add-rewrite-maven-plugin-or-rewrite-gradle-plugin-to-your-project

