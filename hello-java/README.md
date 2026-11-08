# Hello Java with Jenkins and Docker

A tiny Java project that Jenkins can fetch from GitHub, compile, and run inside a Docker Java environment.

## Files

- `src/HelloWorld.java` — prints `Hello, World!`.
- `Jenkinsfile` — tells Jenkins to use the `eclipse-temurin:21-jdk` Docker image, compile the class, and run it.

## Run locally

From this folder, with Java 21 installed:

```sh
javac -d out src/HelloWorld.java
java -cp out HelloWorld
```

Expected output:

```text
Hello, World!
```

## Jenkins setup overview

1. Create a new **public** GitHub repository named `hello-java` (leave the README, `.gitignore`, and license options unchecked so the repository starts empty).
2. Add and push these project files to the repository's `main` branch.
3. In Jenkins, create a **Pipeline** job and select **Pipeline script from SCM**.
4. Select **Git**, enter the repository's HTTPS URL, and set the branch to `*/main`.
5. Set **Script Path** to `Jenkinsfile`, save, then choose **Build Now**.
6. In the build's **Console Output**, look for `Hello, World!`.

The Docker Pipeline plugin must be installed in Jenkins, and Jenkins must be able to use the Docker daemon on the machine that runs the job. The Docker agent is temporary; Jenkins may remove its container when the build finishes.
