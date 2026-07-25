# Demo Recording Script — Java Spring Boot + Model Context Protocol (MCP) + Copilot

**Demo source:** [microsoft/github-copilot-java-mcp-demo](https://github.com/microsoft/github-copilot-java-mcp-demo)

> **Publication check:** Review every screenshot and screen recording for repository names, local paths, account names, notifications, and other identifying information. Redact or replace any exposed details before publishing.

> **Recording rule:** Treat each `Say` cell as a sequence of timed cues, not as one paragraph to read before the row. Say a sentence immediately before its matching action, perform that action, and then continue with the next sentence. The final sentence in each row should connect the result on screen to the next row. Wait without narration only where the `Do` column explicitly says to wait.

> **Control rule:** Use visible buttons, menus, and links for every demo action. Do not use keyboard shortcuts or function keys. Use the keyboard only to enter text into fields and prompts.

## Episode 1 of 4 — Build and run your first Spring Boot app

### Intro — Talking head (~35s)

> Want to build your first Spring Boot app in Visual Studio Code and understand how the pieces fit together?
>
> In this video, I’ll get the Java and Spring tooling ready, retrace the project setup with Spring Initializr, and explore a finished Todo application. Then I’ll build it, run it from the Spring Boot Dashboard, and verify its add, complete, and delete flow in the browser. Let’s jump right in.

**Do:** End on “let's jump right in,” then cut to screen share.

### Demo — Set up, build & run

**Before recording:** Have Java 25, the Extension Pack for Java, and the Spring Boot Extension Pack installed. Open the completed sample in VS Code, stop any running instance of the application, make sure port 8080 is free, make the Maven Explorer and Spring Boot Dashboard views available, and prepare a browser tab for http://localhost:8080. During the take, show each extension pack's **Installed** state; do not reinstall or update extensions.

**Pacing:** Announce each wait, then let Java import, the Maven build, and application startup finish without narration.

| Where | Do | Say |
|-------|----|-----|
| VS Code — Activity Bar → Extensions | Select the **Extensions** button in the Activity Bar. Search **"Extension Pack for Java"**, open its result, and pause on its **Installed** state. | "I'll open the Extensions view from the Activity Bar and search for the Extension Pack for Java. It is already installed in this setup, giving VS Code Java language support, debugging, Maven, and testing. With the editor tooling confirmed, I'll check which JDK the project uses." |
| VS Code menu → Command Palette | Select **View → Command Palette**, search for **"Java: Configure Java Runtime"**, and select that command from the results. On the Java Runtime page, show Java 25 as the project's JDK, then select the tab's **Close** button. | "The extension pack still needs a JDK, so I'll open the Command Palette from the View menu, search for Java: Configure Java Runtime, and select it from the results. The Java Runtime page shows that this project uses Java 25. I'll close the page, then check the Spring-specific tooling." |
| VS Code — Extensions view | Search **"Spring Boot Extension Pack"**, open its result, and pause on its **Installed** state. | "Back in Extensions, I'll search for the Spring Boot Extension Pack. It is also already installed, adding Spring Initializr, the Spring Boot Dashboard, and Spring configuration support. Those tools are enough to retrace how this sample was created." |
| VS Code menu → Command Palette | Select **View → Command Palette**, search for **"Spring Initializr: Create a Maven Project"**, select that command from the results, and pause at the Spring Boot version picker. | "Now I'll open the Command Palette from the View menu, search for Spring Initializr: Create a Maven Project, and select it from the results. The first picker asks for the Spring Boot version, so this is where the project definition begins." |
| Spring Initializr prompts | Choose Spring Boot 4.1.0 → Java → group `com.example` → artifact `springboot-mcp-demo` → **Jar** → Java 25. | "I'll select Spring Boot 4.1.0 to match the sample, and choose Java as the language. For the project coordinates, I'll enter `com.example` as the group and `springboot-mcp-demo` as the artifact. I'll package it as a Jar and target Java 25. With the project details set, the next picker defines what the application can do." |
| Dependency picker → folder picker | Add **Spring Web**, **Thymeleaf**, **Actuator**, and **Model Context Protocol Server**. Pause with all four selected, select **Selected 4 dependencies**, then select **Cancel** in the folder picker before a project is generated. | "I'll add Spring Web for HTTP handling and Thymeleaf for the server-rendered page. Actuator adds runtime health information, and Model Context Protocol Server adds MCP server support to the application. These four selections match the completed sample. Because that sample is already open, I'll select the `Selected 4 dependencies` entry, then cancel at the folder picker before Initializr generates a duplicate project." |
| Explorer | Expand the `com.example.tododemo` package and `templates` folder in the completed sample already open in the workspace. | "The wizard is closed, so I'm back in the completed sample from the repository linked in the description. This sample uses the base package `com.example.tododemo` for its Todo code. I'll expand that package and the templates folder to show the Java layers and the web page that were added to the generated starter. I'll start at the class that launches all of them." |
| `SpringbootMcpDemoApplication.java` | Show `@SpringBootApplication` and `main`. | "This `@SpringBootApplication` annotation marks the application entry point. The `main` method starts Spring Boot, which scans this package, creates the application components, and wires their dependencies. From here, I'll follow that structure from the data model into the shared application logic." |
| `Todo.java` → `TodoRepository.java` → `TodoService.java` | Show the `Todo` fields, the repository's `@Repository` and in-memory map, then the service's `@Service` and constructor. | "First, `Todo` defines the id, title, completion state, and creation time. Next, `TodoRepository` is a Spring repository that keeps those objects in an in-memory map. Finally, `TodoService` receives that repository through its constructor and provides the operations used by the rest of the app. With the shared operations in place, I can trace how the web page calls one of them." |
| `templates/index.html` → `TodoController.java` | In the template, show the add form's `POST /todos` action and `title` input. Then open the controller and show the matching `@PostMapping`, `service.add(title)`, and redirect. | "In the Thymeleaf template, the add form posts the `title` field to `/todos`. I'll open `TodoController` and find the matching `@PostMapping`, where the controller passes that title to `service.add` and redirects to the home page. The browser, controller, and service now form one complete request path, so I'll build and test it." |
| `pom.xml` | Open the root `pom.xml`. Show the Spring Boot parent version `4.1.0`, the `com.example` group and `springboot-mcp-demo` artifact, the Java 25 property, the four application dependencies selected in Initializr, and the test starter that follows them. | "Before I build, I'll open `pom.xml`, Maven's project definition. The Spring Boot parent is version 4.1.0, the group and artifact match the values I entered in Initializr, and the Java version is 25. The dependencies include WebMVC, which is Spring Boot 4's name for the Spring Web starter, plus Thymeleaf, Actuator, and Spring AI's MCP server starter, matching the four capabilities I selected in the wizard. A test starter follows them. With the project definition connected to the code I just traced, I'll use the Maven view to package the application." |
| Maven Explorer | Expand **springboot-mcp-demo → Lifecycle**, point to **package**, select its **Run** button, and wait for **`BUILD SUCCESS`** in the Maven output. **Do not narrate while Maven builds and runs the tests.** | "I'll open Maven Explorer, expand the project's Lifecycle goals, hover over `package`, and select its Run button. Maven will compile the code, run the tests, and create the application Jar. I'll wait while it works and continue when the output shows `BUILD SUCCESS`." |
| Spring Boot Dashboard | Find **springboot-mcp-demo**, select its **Run** action, and wait for the app to show as running. **Do not narrate while it starts.** | "The successful build confirms the code and tests pass. Now I'll find the same project in the Spring Boot Dashboard and select Run. I'll wait for startup to finish, then use the Dashboard's running state to open the application." |
| Spring Boot Dashboard → browser | Point to the app's running state and port in the Dashboard, then select its **Open** action to open http://localhost:8080. | "The Dashboard now shows the application running on port 8080. I'll select its Open action to launch the page in the browser so I can exercise the request path I just traced." |
| Browser | Enter **Prepare the demo**, select **Add**, mark that item complete, and select its **Delete** button. | "I'll enter `Prepare the demo` and select Add to create a Todo. When the new row appears, I'll select its checkbox to mark it complete. Then I'll select Delete for that same row. All three changes return through the controller and render immediately, so the basic flow is working." |
| Spring Boot Dashboard | Return to the Dashboard and select the app's **Stop** action. | "The add, complete, and delete cycle worked. I'll return to the Dashboard and select Stop to shut the application down cleanly. The project is now built, tested, and verified in Visual Studio Code." |

**The Spring Initializr version picker:**

![Spring Initializr version picker](../docs/images/00-initializr.png)

**The running Todo web app:**

![Todo web app](../docs/images/01-web-app.png)

### Outro — Talking head (~25s)

> And there it is. I set up the Java and Spring extensions, used Spring Initializr to retrace the starter configuration, and explored the finished Todo app from model to controller. Then I built it, ran it from the Spring Boot Dashboard, and verified its core browser flow. That took me from a Java setup to a working Spring Boot application in Visual Studio Code. What would you build first with Java and Spring Boot? Let me know in the comments. Thanks for watching, and happy building.

---

## Episode 2 of 4 — Debug and inspect a Spring Boot request

### Intro — Talking head (~30s)

> Ever wondered what a Spring Boot app is actually doing between a browser click and the Java code that handles it?
>
> In this video, I’ll open a finished Spring Boot Todo app in Visual Studio Code and follow one add request through the Java debugger. I’ll inspect the request data, step from the controller into the service, and then use the Spring Boot Dashboard to check the running app’s endpoint mappings, health, and live memory. Let’s jump right in.

**Do:** End on “let's jump right in,” then cut to screen share.

### Demo

**Prerequisites:** Clone the finished sample from the [GitHub repository](https://github.com/microsoft/github-copilot-java-mcp-demo) and open it in VS Code with Java 25, the Extension Pack for Java, and the Spring Boot Extension Pack installed.

**Before recording:** Stop the Spring Boot app, make sure port 8080 is free, close Copilot Chat, and hide any terminal or output content that exposes local paths, account details, or unrelated notifications.

| Where | Do | Say |
|-------|----|-----|
| Editor — `TodoController.java` | Show the `addForm` method, then click the gutter to set a breakpoint on its `service.add(title)` line. | "I've opened the finished Todo sample, where the web form sends a title to `TodoController`. In `addForm`, the controller passes that title to the shared service. I'll set a breakpoint on that call so the next add request pauses at the boundary between the web layer and the application logic." |
| Spring Boot Dashboard | Select the app's **Debug** action and wait for the debugger to connect. **Do not narrate while the app starts.** | "The breakpoint is ready. In the Spring Boot Dashboard, I'll select Debug for the application. I'll wait for the debugger to connect before inspecting the live views it adds." |
| Spring Boot Dashboard → `TodoController.java` | Show the app's running debug state. Expand the app and point out **Beans**, **Endpoint Mappings**, **Properties**, and **Memory**. Then return to the controller and show the gray URL hints above its mappings. | "The Dashboard now shows the app running with the debugger attached. I'll expand it to reveal live views for its beans, endpoint mappings, properties, and memory. Back in the controller, Spring Tools also adds gray URL hints above the mapped methods. I'll use the root hint to send a request to the breakpoint." |
| Editor → browser | Click the root URL hint, enter **Trace this request** in the form, and select **Add**. Wait for VS Code to stop at the breakpoint. | "I'll open the root page directly from the controller's URL hint. In the form, I'll enter `Trace this request` and select Add. That request should stop in VS Code before the controller calls the service." |
| Debug toolbar + Variables panel | In **Local**, show `title` and its value. Select **Step Into** in the Debug toolbar to enter `TodoService.add`. Select **Step Over** once to execute the `Todo todo = ...` line, then show the new `todo` local with `id` still `null`. | "The breakpoint has paused on the service call. In the Local variables, I'll find `title` and confirm that the controller received `Trace this request`. Next, I'll select Step Into in the Debug toolbar to move from the controller into `TodoService.add`, the shared method behind this operation. I'll select Step Over to execute the line that creates the `Todo`, and the new local has the title, but its id is still null, because the repository assigns that when it saves." |
| Debug toolbar → browser | Select **Continue** in the Debug toolbar, wait for the request to finish, and show **Trace this request** in the browser. Leave the debug session running. | "The service has created the object, so I'll select Continue in the Debug toolbar. The repository can now assign the id, the controller can redirect, and Thymeleaf can render the refreshed list. When `Trace this request` appears in the browser, the end-to-end request is complete. I'll keep the debugger attached for two runtime checks." |
| Spring Boot Dashboard → **Endpoint Mappings** → browser | Expand **Endpoint Mappings**, find `/actuator/health`, and select its **Open** action. In the browser, point to the `status` field showing `UP`; the response may also include a `groups` field. | "First, I'll expand Endpoint Mappings, find `/actuator/health`, and select its Open action. The `UP` status in the browser confirms that the running application is healthy right now. That is a single snapshot, so for something continuous I'll return to the Dashboard's Memory view." |
| Spring Boot Dashboard → running app → **Memory** view | Open **Memory** and show the live heap information updating. | "I'll expand the running app and open Memory. This view updates the application's heap information while the debug process continues to run. That completes the runtime inspection, so I can shut the process down cleanly." |
| Spring Boot Dashboard | Return to the Dashboard and select the app's **Stop** action. Confirm it is no longer running. | "I'll return to the Spring Boot Dashboard and select Stop. The app's running indicator clears, so the request trace and runtime inspection are complete." |

**Actuator health response from the running sample:**

![Actuator health](../docs/images/02-actuator-health.png)

**Spring Boot Dashboard Memory view:**

![Memory view](../docs/images/05-memory-view.png)

### Outro — Talking head (~25s)

> And there it is. I followed a browser request into `TodoController`, inspected its title, stepped into `TodoService`, and watched the completed request return to the page. Then I used the Spring Boot Dashboard to confirm the app’s health and monitor its live heap. That is how Visual Studio Code lets me inspect a running Spring Boot app instead of guessing at what it is doing. What request would you trace first in your own application? Let me know in the comments. Thanks for watching, and happy building.

---

## Episode 3 of 4 — Expose your Java operations to Copilot with MCP

### Intro — Talking head (~25s)

> Did you know GitHub Copilot can call your Spring Boot app’s Java operations directly from Visual Studio Code? In this video, I’ll use Spring AI and the Model Context Protocol, or MCP, to turn parts of the app into tools Copilot can use. Then I’ll invoke those tools through Copilot and verify the result in the web interface. Let’s jump right in.

**Do:** End on “let's jump right in,” then cut to screen share.

**Prerequisites:** Clone the finished sample from the [GitHub repository](https://github.com/microsoft/github-copilot-java-mcp-demo) and open it in VS Code with Java 25, the Extension Pack for Java, the Spring Boot Extension Pack, and GitHub Copilot installed and signed in. Allow MCP tool use when VS Code prompts for trust or confirmation.

**Before recording:** Make sure the five `todo-mcp` tools are disabled in Chat, stop the Spring Boot app and the `todo-mcp` connection, make sure port 8080 is free, and prepare a browser tab at http://localhost:8080. Keep the application's own output view selected so `Registered tools: 5` is visible without scrolling. Trust the repository and workspace before the take so only the MCP connection and tool confirmations described below can appear.

### Demo

| Where | Do | Say |
|-------|----|-----|
| `pom.xml` | Show the `spring-ai-starter-mcp-server-webmvc` dependency. Then show the `spring-ai-bom` import and the `spring-ai.version` value `2.0.0`. | "I've cloned the finished Todo sample from the repository linked in the description and opened it in VS Code with GitHub Copilot signed in. The application already has Todo operations; in this video I'll expose them as MCP tools. In `pom.xml`, I'll first show Spring AI's WebMVC MCP server starter. Then I'll move to the imported Spring AI Bill of Materials and its `2.0.0` version property. The starter supplies the MCP server support, while the BOM keeps its Spring AI dependencies on the same version. With that support on the classpath, I can show the Java methods it publishes." |
| `mcp/TodoTools.java` | Show the class's `@Component`, the five `@McpTool` methods, an `@McpToolParam`, and each method's delegation to `TodoService`. | "`TodoTools` is a Spring component, so the MCP annotation scanner can discover it. I'll move through the five `@McpTool` methods named `list_todos`, `get_todo`, `add_todo`, `complete_todo`, and `delete_todo`. Each annotation gives Copilot a tool name and description, and `@McpToolParam` describes required inputs such as a title or id. The method bodies do not duplicate the application logic; they delegate to the same `TodoService` used by the web page. Now those tools need an HTTP transport that VS Code can connect to." |
| `application.properties` | Highlight `spring.ai.mcp.server.protocol=STREAMABLE`, then point to the server name, version, and instructions. | "In `application.properties`, I'll highlight `spring.ai.mcp.server.protocol=STREAMABLE`. That setting publishes the modern Streamable HTTP endpoint at `/mcp`; without it, this starter uses its older Server-Sent Events transport and a POST to `/mcp` is unavailable. The next properties give the MCP server its name, version, and tool-set instructions. The dependency, tools, and transport are now configured, so I'll start the Java application." |
| Spring Boot Dashboard | Find **springboot-mcp-demo**, select **Run**, and wait for startup without narration. In the app output, show **`Registered tools: 5`**. Leave the app running. | "I'll find `springboot-mcp-demo` in the Spring Boot Dashboard and select Run. I'll wait for startup, then look in the application output for `Registered tools: 5`. That message confirms Spring discovered every annotated method. The Java server is ready; the next step is to give VS Code its endpoint." |
| `.vscode/mcp.json` | Show the `todo-mcp` server's `type` and `url`. Select its **Start** code-lens and wait until VS Code shows the connection as running and its tools as discovered. | "This workspace's `.vscode/mcp.json` defines a server named `todo-mcp`. I'll point out its HTTP type and the URL `http://localhost:8080/mcp`, which targets the application already running in the Dashboard. Now I'll select Start and wait for VS Code to connect and discover the five tools. This Start action connects an MCP client; it does not launch the Java process. With the connection running, I can make those tools available in Chat." |
| Copilot Chat — Agent mode | Open the Chat tools picker, find `todo-mcp`, enable its five tools, and close the picker. | "I'll open Copilot Chat in Agent mode and open the tools picker. Under `todo-mcp`, I can see the same five tool names that Spring registered. I'll enable them and close the picker. Copilot can now choose those application operations, so I'll give it a task that requires two of them in sequence." |
| Copilot Chat — Agent mode | Enter *"Use the todo-mcp tools to add a todo called 'Email the stakeholders', then list all todos."* and select **Send**. If prompted, review the tool name and arguments before choosing **Allow**. Wait for the final response. | "I'll ask Copilot to use `todo-mcp` to add a Todo called `Email the stakeholders`, then list all Todos, and select Send. If prompted, I'll review the tool name and arguments before allowing it. The final response should contain the newly created item, but I also want to verify it in the web page." |
| Copilot Chat → browser | In Chat, point to **Email the stakeholders** in the structured `list_todos` result. Then select **Refresh** in the prepared http://localhost:8080 browser tab and point to the same title in the Todo list. | "The structured tool result contains `Email the stakeholders`, confirming what the MCP call returned. I'll switch to the prepared browser tab and select Refresh. The same title appears there because the MCP tools and the Thymeleaf controller both delegate to one service and one in-memory repository. That shared result completes the test, so I'll shut both sides down." |
| `.vscode/mcp.json` → Spring Boot Dashboard | Select **Stop** for `todo-mcp` in `.vscode/mcp.json`. Then select **Stop** for **springboot-mcp-demo** in the Dashboard and confirm it is no longer running. | "I'll return to `.vscode/mcp.json` and stop the `todo-mcp` connection first, while the server is still running. Then I'll return to the Spring Boot Dashboard and stop the Java application. Because its repository is in memory, stopping the process clears the Todo created during this demo. Both are stopped, and port 8080 is free." |

**Proof it works — a todo created *through MCP* appears in the web interface** (last row):

![Todo added via MCP](../docs/images/03-mcp-added-todo.png)

**Copilot Chat calling the `todo-mcp` tools — the `add_todo` call and its structured result:**

![Copilot Chat todo-mcp tool call](../docs/images/06-copilot-mcp-chat.png)

### Outro — Talking head (~20s)

> And there it is. I used Spring AI to expose Java operations as tools through the Model Context Protocol, connected those tools to GitHub Copilot in Visual Studio Code, and kept the web interface and Copilot using the same service. After I refresh the browser, a change made through Copilot appears in the web app. What part of your own Java application would you turn into a Copilot tool? Let me know in the comments. Thanks for watching, and happy building.

---

## Episode 4 of 4 — Let Copilot test it with Playwright

### Intro — Talking head (~25s)

> Could your Java tests all pass while the web interface is still broken for a real user? In this video, I’ll connect Playwright to GitHub Copilot through the Model Context Protocol, or MCP, and have Copilot verify a complete user journey in a real browser. That gives me confidence in the experience users actually see, not just the code behind it. Let’s jump right in.

**Do:** End on “let's jump right in,” then cut to screen share.

**Prerequisites:** Clone the finished sample from the [GitHub repository](https://github.com/microsoft/github-copilot-java-mcp-demo) and open it in a current version of VS Code with Java 25, the Extension Pack for Java, the Spring Boot Extension Pack, and GitHub Copilot installed and signed in. Allow MCP server installation and tool use when prompted.

**Before recording:** Use a VS Code profile where the Playwright MCP server is not yet installed so the **Install** action is guaranteed to appear. Confirm the `@mcp playwright` gallery result appears before the take; if it does not, add the server to `.vscode/mcp.json` and start it from there instead. Stop the Spring Boot app, free port 8080, close any browser left from an earlier Playwright run, and open the Spring Boot Dashboard.

### Demo

| Where | Do | Say |
|-------|----|-----|
| VS Code — Activity Bar → Extensions | Select the **Extensions** button in the Activity Bar. Search **`@mcp playwright`** and open the Playwright MCP server result. Review its publisher and command configuration. Select **Install**, confirm trust for the server, and wait for its running status. | "I've cloned the finished Todo sample from the repository linked in the description and opened it in VS Code with GitHub Copilot signed in. To test the page through a real browser, Copilot needs browser-control tools, so I'll open Extensions from the Activity Bar, search the MCP server gallery for `@mcp playwright`, and open the Playwright result. Before installing it, I'll review the publisher and the command VS Code will run. I'll select Install, confirm that I trust this server, and wait for its status to show that it is running. With the browser tools in place, I'll look at the page elements they will target." |
| `templates/index.html` | Show `data-testid="new-todo-input"`, `data-testid="add-todo"`, `data-testid="todo-item"`, `th:attr="aria-label='Toggle ' + ${todo.title}"`, and `data-testid="delete-todo"` in the template. | "In `index.html`, the text input has the stable test id `new-todo-input`, and the submit button has `add-todo`. Each rendered row uses `todo-item`, while its checkbox builds an accessible `Toggle` label from that Todo's title. Each delete button uses `delete-todo`. These test ids identify the exact controls without depending on visual styling. With those test ids in place, I'll first confirm the Java test baseline." |
| VS Code — Activity Bar → Testing | Select the **Testing** button in the Activity Bar, select **Run Tests**, and wait until all Java tests pass. **Do not narrate while the tests run.** | "I'll open the Testing view and select Run Tests. I'll wait while the unit and integration tests run, then continue when every test shows as passing. Those tests establish that the service and Spring web flow work underneath the page, but they do not click through the page the way a user would. For that, the browser tools need a live application." |
| Spring Boot Dashboard | Find **springboot-mcp-demo**, select **Run**, and wait without narration until the Dashboard shows it running on port 8080. | "I'll return to the Spring Boot Dashboard, find `springboot-mcp-demo`, and select Run. I'll wait while it starts and continue when the Dashboard shows the app running on port 8080. The app is live, so I can enable Playwright for this Chat session." |
| Copilot Chat — Agent mode | Select **Agent** mode, open the tools picker, confirm the Playwright tools are listed and enabled, and close the picker. | "In Copilot Chat, I'll select Agent mode and open the tools picker. The Playwright tools discovered during installation are listed and enabled, so I'll close the picker. Copilot can now control a browser, but it still needs a precise workflow and observable success conditions." |
| Copilot Chat — Agent mode | Enter *"Use the Playwright tools to open http://localhost:8080 and verify the page title is 'Java TODO Demo'. Add a todo called 'Verify the browser flow', find that todo's row, complete it and verify it is checked, then delete it and verify it is gone."* and select **Send**. If prompted, review the tool name and arguments before choosing **Allow**. | "I'll ask Copilot to open the local app and verify its title, add `Verify the browser flow`, find that exact row, complete it and verify its checkbox, then delete it and verify the text is gone. The prompt specifies both the actions and the assertions, so I'll select Send. If prompted, I'll review the tool name and arguments before allowing it. Copilot can then execute the journey while I watch the visible browser state." |
| Browser window (Playwright) | As Copilot works, show the page open at http://localhost:8080, the input filled with **Verify the browser flow**, the new row after **Add**, the row's checked checkbox after completion, and the row disappearing after deletion. | "The Playwright browser has opened the Java TODO Demo at the requested address. Copilot is filling the input with `Verify the browser flow` and selecting Add. That exact row is now on the page, so it can target that row's checkbox instead of another item. After the toggle, the checkbox is visibly checked. Copilot then deletes the same row, and the title disappears from the page. The visible journey is complete; now I'll inspect the recorded assertions in Chat." |
| Copilot Chat | Return to Chat. Review the completed Playwright tool calls and final response, confirming the page title, added text, checked state, deletion, and absence check. | "Back in Chat, I'll review the completed tool calls rather than trusting only what I just watched in the browser. The trace shows that Playwright loaded `Java TODO Demo`, added the exact title, observed its checkbox as checked, deleted the row, and then found no matching text. Those checks prove the page reached each required state, so the test is finished." |
| Playwright browser → Spring Boot Dashboard | Select **Close** on the Playwright browser page. Return to the Dashboard, select **Stop** for **springboot-mcp-demo**, and confirm it is no longer running. Leave the Playwright MCP server installed in the VS Code user profile. | "I'll select Close on the Playwright browser page and return to the Spring Boot Dashboard. Then I'll select Stop for `springboot-mcp-demo` and confirm its running indicator clears. The application is shut down, while Playwright remains installed in my VS Code user profile for future Chat sessions." |

**Illustrative browser state during a Playwright run; the live Copilot tool calls are shown during the demo:**

![Playwright run](../docs/images/07-playwright-run.png)

### Outro — Talking head (~20s)

> And there it is. I connected Playwright to GitHub Copilot through the Model Context Protocol and had Copilot test the Spring Boot app in a real browser. Combined with the unit and integration tests, that gives me confidence in both the code and the experience a user actually sees. What browser workflow would you ask Copilot to test in your own app? Let me know in the comments. Thanks for watching, and happy building.

---

## Resources (video descriptions / hand-off)

- **Demo source:** https://github.com/microsoft/github-copilot-java-mcp-demo
- **Extension Pack for Java** (Microsoft): https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack
- **Spring Boot Extension Pack:** search “Spring Boot Extension Pack” in the VS Code Marketplace
- **Java in VS Code:** https://code.visualstudio.com/docs/languages/java
- **Spring Boot Actuator:** https://docs.spring.io/spring-boot/
- **Spring AI (Model Context Protocol server):** https://docs.spring.io/spring-ai/reference/
- **Model Context Protocol:** https://modelcontextprotocol.io
- **Model Context Protocol in Visual Studio Code:** https://code.visualstudio.com/docs/copilot/chat/mcp-servers
- **Playwright Model Context Protocol server:** https://github.com/microsoft/playwright-mcp
