# JSP Development Setup: Notepad + Tomcat 10 + Java 21 LTS

## Prerequisites

**Step 1: Install Java 21 LTS**
- Download from: https://www.oracle.com/java/technologies/downloads/#java21
- Choose Windows/Mac/Linux version
- Install and verify: Open Command Prompt/Terminal and run:
  ```
  java -version
  ```

**Step 2: Install Tomcat 10**
- Download from: https://tomcat.apache.org/download-10.cgi
- Download the binary distribution (ZIP file for Windows, TAR.GZ for Linux/Mac)
- Extract to a folder (e.g., `C:\tomcat10` or `/opt/tomcat10`)

**Step 3: Set Environment Variables (Windows)**
- Right-click "This PC" → Properties → Advanced system settings
- Click "Environment Variables"
- Add new System Variable:
  - Variable name: `JAVA_HOME`
  - Variable value: `C:\Program Files\Java\jdk-21` (your Java installation path)
- Add another:
  - Variable name: `CATALINA_HOME`
  - Variable value: `C:\tomcat10` (your Tomcat folder)
- Click OK and restart your computer

**For Mac/Linux:** Add to `~/.bashrc` or `~/.zshrc`:
```bash
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home
export CATALINA_HOME=/opt/tomcat10
```
Then run: `source ~/.bashrc`

---

## Project Structure Setup

Create this folder structure:
```
C:\tomcat10\webapps\myapp\
├── index.jsp
├── WEB-INF\
│   ├── web.xml
│   └── classes\
└── (other JSP files here)
```

---

## Create JSP File

**File: `C:\tomcat10\webapps\myapp\index.jsp`**

```jsp
<%@ page language="java" %>
<html>
<head>
    <title>JSP Example</title>
</head>
<body>

<h3>Numbers from 1 to 10</h3>

<%
    for (int i = 1; i <= 10; i++) {
        out.println(i + "<br>");
    }
%>

</body>
</html>
```

---

## Create web.xml Configuration

**File: `C:\tomcat10\webapps\myapp\WEB-INF\web.xml`**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    
    <display-name>My JSP Application</display-name>
    
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
    
</web-app>
```

---

## Start Tomcat Server

**Windows:**
- Open Command Prompt as Administrator
- Navigate to Tomcat bin folder:
  ```
  cd C:\tomcat10\bin
  ```
- Run:
  ```
  catalina.bat run
  ```
- You should see: "Tomcat started" message

**Mac/Linux:**
- Open Terminal
- Navigate to Tomcat bin:
  ```
  cd /opt/tomcat10/bin
  ```
- Run:
  ```
  ./catalina.sh run
  ```

---

## Run Your JSP Application

1. Make sure Tomcat is running (see above)
2. Open your browser
3. Go to: `http://localhost:8080/myapp/index.jsp`
4. You should see "Numbers from 1 to 10" with numbers 1-10 displayed

---

## Editing JSP Files in Notepad

- Open files with Notepad (right-click → Open with → Notepad)
- Save with `.jsp` extension
- Place files in: `C:\tomcat10\webapps\myapp\`
- Refresh browser to see changes (no restart needed for JSP files)

---

## Common Troubleshooting

| Problem | Solution |
|---------|----------|
| "java is not recognized" | JAVA_HOME not set correctly or system not restarted |
| Port 8080 already in use | Change Tomcat port in `catalina.properties` or stop other apps |
| 404 Not Found | Check file path and spelling of filename |
| JSP not updating | Clear browser cache (Ctrl+Shift+Del) and hard refresh (Ctrl+F5) |
| Tomcat won't start | Check CATALINA_HOME path and file permissions |

---

## Additional JSP Examples to Try

**Simple Variable Example:**
```jsp
<%@ page language="java" %>
<html>
<body>
<% String name = "John"; %>
<h2>Hello <%= name %>!</h2>
</body>
</html>
```

**Loop with Table:**
```jsp
<%@ page language="java" %>
<html>
<body>
<table border="1">
<% for (int i = 1; i <= 5; i++) { %>
    <tr><td><%= i %></td><td><%= i * i %></td></tr>
<% } %>
</table>
</body>
</html>
```

---

## Stop Tomcat

- Press `Ctrl+C` in the Command Prompt/Terminal where Tomcat is running
- Wait for clean shutdown message
