## Environment Variables: JAVA_HOME and PATH

After installing the JDK, your operating system doesn't automatically know where Java lives. You need to tell it — and you do that through two environment variables: `JAVA_HOME` and `PATH`.

**`JAVA_HOME`** is a variable that points to the root directory of your JDK installation (e.g., `C:\Program Files\Java\jdk-25` on Windows). It does not point to the `bin` folder — just the root. Many tools, frameworks, and IDEs (like Maven, Gradle, IntelliJ IDEA, and Spring Boot) read this variable to locate Java. Without it, they won't know where to find the compiler, the runtime, or the libraries they depend on.

**`PATH`** is a system variable that tells your terminal where to find executable programs. By adding `%JAVA_HOME%\bin` (Windows) or `$JAVA_HOME/bin` (Mac/Linux) to the `PATH`, you make commands like `java` and `javac` available from any directory in the terminal — without typing the full path every time.

In short: `JAVA_HOME` tells tools where Java is installed. `PATH` tells your terminal where to find Java's commands.

### Quick Setup

**Windows:**
1. Press the Windows key and type `variables`, then click on the option **Edit the system environment variables** or **Edit environment variables for your account**.
2. Click **Environment Variables**.
3. Under **System variables**, click **New**:
   - **Variable name:** `JAVA_HOME`
   - **Variable value:** the path to your JDK root (e.g., `C:\Program Files\Java\jdk-25`)
4. Find the **Path** variable in the same section, click **Edit**, then **New**, and add: `%JAVA_HOME%\bin`
5. Click **OK** on all dialogs. **Close and reopen** any terminal window for the changes to take effect.

**Mac/Linux:**

Open your shell config file (`~/.bashrc`, `~/.zshrc`, or `~/.bash_profile`) in any text editor and add:
```bash
export JAVA_HOME=/path/to/your/jdk
export PATH=$JAVA_HOME/bin:$PATH
```
Save the file, then run `source ~/.bashrc` (or the equivalent) to apply the changes immediately.

**Verify (any OS):**
```bash
java -version
javac -version
echo %JAVA_HOME%      # Windows (CMD)
echo $JAVA_HOME       # Mac/Linux or PowerShell
```

If `java -version` returns a version number and `javac -version` does the same, you're good. If either one says `'not recognized'` or `'command not found'`, double-check your `JAVA_HOME` path and make sure the `bin` folder was added to `PATH` correctly.

> **Tip:** Some modern JDK installers (like Eclipse Temurin) offer an option to set `JAVA_HOME` and update `PATH` automatically during installation. If you see that checkbox, check it — it saves time.