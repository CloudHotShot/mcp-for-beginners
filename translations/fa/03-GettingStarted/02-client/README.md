<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "22afa94e3912cd37af9ff20cf4aebc93",
  "translation_date": "2025-07-22T08:45:34+00:00",
  "source_file": "03-GettingStarted/02-client/README.md",
  "language_code": "fa"
}
-->
# ایجاد یک کلاینت

کلاینت‌ها برنامه‌ها یا اسکریپت‌های سفارشی هستند که به طور مستقیم با سرور MCP ارتباط برقرار می‌کنند تا منابع، ابزارها و درخواست‌ها را دریافت کنند. برخلاف استفاده از ابزار بازرس که یک رابط گرافیکی برای تعامل با سرور فراهم می‌کند، نوشتن کلاینت خودتان امکان تعامل برنامه‌ریزی‌شده و خودکار را فراهم می‌کند. این قابلیت به توسعه‌دهندگان اجازه می‌دهد تا توانایی‌های MCP را در جریان کاری خود ادغام کنند، وظایف را خودکار کنند و راه‌حل‌های سفارشی متناسب با نیازهای خاص ایجاد کنند.

## مرور کلی

این درس مفهوم کلاینت‌ها در اکوسیستم Model Context Protocol (MCP) را معرفی می‌کند. شما یاد خواهید گرفت که چگونه کلاینت خود را بنویسید و آن را به یک سرور MCP متصل کنید.

## اهداف یادگیری

در پایان این درس، شما قادر خواهید بود:

- درک کنید که کلاینت چه کاری می‌تواند انجام دهد.
- کلاینت خود را بنویسید.
- کلاینت را به سرور MCP متصل کنید و آن را آزمایش کنید تا مطمئن شوید که سرور به درستی کار می‌کند.

## چه چیزی در نوشتن یک کلاینت دخیل است؟

برای نوشتن یک کلاینت، باید موارد زیر را انجام دهید:

- **کتابخانه‌های صحیح را وارد کنید**. شما از همان کتابخانه قبلی استفاده خواهید کرد، فقط ساختارهای متفاوتی.
- **یک کلاینت ایجاد کنید**. این شامل ایجاد یک نمونه کلاینت و اتصال آن به روش انتقال انتخابی خواهد بود.
- **تصمیم بگیرید که چه منابعی را لیست کنید**. سرور MCP شما دارای منابع، ابزارها و درخواست‌ها است، شما باید تصمیم بگیرید کدام یک را لیست کنید.
- **کلاینت را در یک برنامه میزبان ادغام کنید**. هنگامی که توانایی‌های سرور را شناختید، باید آن را در برنامه میزبان خود ادغام کنید تا اگر کاربر یک درخواست یا دستور دیگر وارد کرد، ویژگی مربوطه سرور فراخوانی شود.

حالا که به طور کلی فهمیدیم چه کاری قرار است انجام دهیم، بیایید به یک مثال نگاه کنیم.

### یک مثال کلاینت

بیایید به این مثال کلاینت نگاه کنیم:

### TypeScript

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";

const transport = new StdioClientTransport({
  command: "node",
  args: ["server.js"]
});

const client = new Client(
  {
    name: "example-client",
    version: "1.0.0"
  }
);

await client.connect(transport);

// List prompts
const prompts = await client.listPrompts();

// Get a prompt
const prompt = await client.getPrompt({
  name: "example-prompt",
  arguments: {
    arg1: "value"
  }
});

// List resources
const resources = await client.listResources();

// Read a resource
const resource = await client.readResource({
  uri: "file:///example.txt"
});

// Call a tool
const result = await client.callTool({
  name: "example-tool",
  arguments: {
    arg1: "value"
  }
});
```

در کد بالا:

- کتابخانه‌ها را وارد می‌کنیم.
- یک نمونه کلاینت ایجاد می‌کنیم و آن را با استفاده از stdio برای انتقال متصل می‌کنیم.
- درخواست‌ها، منابع و ابزارها را لیست می‌کنیم و همه آن‌ها را فراخوانی می‌کنیم.

این یک کلاینت است که می‌تواند با یک سرور MCP ارتباط برقرار کند.

بیایید در بخش تمرین بعدی وقت بگذاریم و هر قطعه کد را تجزیه کنیم و توضیح دهیم چه اتفاقی می‌افتد.

## تمرین: نوشتن یک کلاینت

همانطور که گفته شد، بیایید وقت بگذاریم و کد را توضیح دهیم، و اگر می‌خواهید، همراه با کد بنویسید.

### -1- وارد کردن کتابخانه‌ها

بیایید کتابخانه‌هایی که نیاز داریم وارد کنیم. ما به ارجاعاتی به یک کلاینت و پروتکل انتقال انتخابی خود، stdio، نیاز خواهیم داشت. stdio یک پروتکل برای چیزهایی است که قرار است روی ماشین محلی شما اجرا شوند. SSE یک پروتکل انتقال دیگر است که در فصل‌های آینده نشان خواهیم داد، اما این گزینه دیگر شماست. فعلاً، بیایید با stdio ادامه دهیم.

#### TypeScript

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";
```

#### Python

```python
from mcp import ClientSession, StdioServerParameters, types
from mcp.client.stdio import stdio_client
```

#### .NET

```csharp
using Microsoft.Extensions.AI;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;
```

#### Java

برای Java، شما یک کلاینت ایجاد خواهید کرد که به سرور MCP از تمرین قبلی متصل می‌شود. با استفاده از همان ساختار پروژه Java Spring Boot از [شروع کار با سرور MCP](../../../../03-GettingStarted/01-first-server/solution/java)، یک کلاس Java جدید به نام `SDKClient` در پوشه `src/main/java/com/microsoft/mcp/sample/client/` ایجاد کنید و واردات زیر را اضافه کنید:

```java
import java.util.Map;
import org.springframework.web.reactive.function.client.WebClient;
import io.modelcontextprotocol.client.McpClient;
import io.modelcontextprotocol.client.transport.WebFluxSseClientTransport;
import io.modelcontextprotocol.spec.McpClientTransport;
import io.modelcontextprotocol.spec.McpSchema.CallToolRequest;
import io.modelcontextprotocol.spec.McpSchema.CallToolResult;
import io.modelcontextprotocol.spec.McpSchema.ListToolsResult;
```

بیایید به ایجاد کلاینت ادامه دهیم.

### -2- ایجاد کلاینت و انتقال

ما باید یک نمونه از انتقال و یک نمونه از کلاینت خود ایجاد کنیم:

#### TypeScript

```typescript
const transport = new StdioClientTransport({
  command: "node",
  args: ["server.js"]
});

const client = new Client(
  {
    name: "example-client",
    version: "1.0.0"
  }
);

await client.connect(transport);
```

در کد بالا:

- یک نمونه انتقال stdio ایجاد کرده‌ایم. توجه کنید که چگونه دستور و آرگومان‌ها برای پیدا کردن و راه‌اندازی سرور مشخص شده‌اند، زیرا این چیزی است که هنگام ایجاد کلاینت به آن نیاز خواهیم داشت.

    ```typescript
    const transport = new StdioClientTransport({
        command: "node",
        args: ["server.js"]
    });
    ```

- یک کلاینت با نام و نسخه ایجاد کرده‌ایم.

    ```typescript
    const client = new Client(
    {
        name: "example-client",
        version: "1.0.0"
    });
    ```

- کلاینت را به انتقال انتخابی متصل کرده‌ایم.

    ```typescript
    await client.connect(transport);
    ```

#### Python

```python
from mcp import ClientSession, StdioServerParameters, types
from mcp.client.stdio import stdio_client

# Create server parameters for stdio connection
server_params = StdioServerParameters(
    command="mcp",  # Executable
    args=["run", "server.py"],  # Optional command line arguments
    env=None,  # Optional environment variables
)

async def run():
    async with stdio_client(server_params) as (read, write):
        async with ClientSession(
            read, write
        ) as session:
            # Initialize the connection
            await session.initialize()

          

if __name__ == "__main__":
    import asyncio

    asyncio.run(run())
```

در کد بالا:

- کتابخانه‌های مورد نیاز را وارد کرده‌ایم.
- یک شیء پارامترهای سرور ایجاد کرده‌ایم، زیرا از این برای اجرای سرور استفاده خواهیم کرد تا بتوانیم با کلاینت خود به آن متصل شویم.
- یک متد `run` تعریف کرده‌ایم که به نوبه خود `stdio_client` را فراخوانی می‌کند که یک جلسه کلاینت را شروع می‌کند.
- یک نقطه ورود ایجاد کرده‌ایم که متد `run` را به `asyncio.run` ارائه می‌دهد.

#### .NET

```dotnet
using Microsoft.Extensions.AI;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;

var builder = Host.CreateApplicationBuilder(args);

builder.Configuration
    .AddEnvironmentVariables()
    .AddUserSecrets<Program>();



var clientTransport = new StdioClientTransport(new()
{
    Name = "Demo Server",
    Command = "dotnet",
    Arguments = ["run", "--project", "path/to/file.csproj"],
});

await using var mcpClient = await McpClientFactory.CreateAsync(clientTransport);
```

در کد بالا:

- کتابخانه‌های مورد نیاز را وارد کرده‌ایم.
- یک انتقال stdio و یک کلاینت `mcpClient` ایجاد کرده‌ایم. دومی چیزی است که برای لیست کردن و فراخوانی ویژگی‌ها در سرور MCP استفاده خواهیم کرد.

توجه داشته باشید، در "Arguments"، می‌توانید به *.csproj* یا فایل اجرایی اشاره کنید.

#### Java

```java
public class SDKClient {
    
    public static void main(String[] args) {
        var transport = new WebFluxSseClientTransport(WebClient.builder().baseUrl("http://localhost:8080"));
        new SDKClient(transport).run();
    }
    
    private final McpClientTransport transport;

    public SDKClient(McpClientTransport transport) {
        this.transport = transport;
    }

    public void run() {
        var client = McpClient.sync(this.transport).build();
        client.initialize();
        
        // Your client logic goes here
    }
}
```

در کد بالا:

- یک متد اصلی ایجاد کرده‌ایم که یک انتقال SSE را تنظیم می‌کند که به `http://localhost:8080` اشاره می‌کند، جایی که سرور MCP ما اجرا خواهد شد.
- یک کلاس کلاینت ایجاد کرده‌ایم که انتقال را به عنوان پارامتر سازنده می‌گیرد.
- در متد `run`، یک کلاینت MCP همزمان با استفاده از انتقال ایجاد کرده‌ایم و اتصال را مقداردهی اولیه کرده‌ایم.
- از انتقال SSE (رویدادهای ارسال‌شده توسط سرور) استفاده کرده‌ایم که برای ارتباط مبتنی بر HTTP با سرورهای MCP Java Spring Boot مناسب است.

### -3- لیست کردن ویژگی‌های سرور

حالا، ما یک کلاینت داریم که می‌تواند متصل شود، اگر برنامه اجرا شود. با این حال، هنوز ویژگی‌های آن را لیست نمی‌کند، بنابراین بیایید این کار را انجام دهیم:

#### TypeScript

```typescript
// List prompts
const prompts = await client.listPrompts();

// List resources
const resources = await client.listResources();

// list tools
const tools = await client.listTools();
```

#### Python

```python
# List available resources
resources = await session.list_resources()
print("LISTING RESOURCES")
for resource in resources:
    print("Resource: ", resource)

# List available tools
tools = await session.list_tools()
print("LISTING TOOLS")
for tool in tools.tools:
    print("Tool: ", tool.name)
```

اینجا منابع موجود را با `list_resources()` و ابزارها را با `list_tools` لیست کرده و چاپ می‌کنیم.

#### .NET

```dotnet
foreach (var tool in await client.ListToolsAsync())
{
    Console.WriteLine($"{tool.Name} ({tool.Description})");
}
```

در بالا مثالی از نحوه لیست کردن ابزارها در سرور آورده شده است. برای هر ابزار، سپس نام آن را چاپ می‌کنیم.

#### Java

```java
// List and demonstrate tools
ListToolsResult toolsList = client.listTools();
System.out.println("Available Tools = " + toolsList);

// You can also ping the server to verify connection
client.ping();
```

در کد بالا:

- `listTools()` را فراخوانی کرده‌ایم تا همه ابزارهای موجود از سرور MCP دریافت شوند.
- از `ping()` برای تأیید اینکه اتصال به سرور کار می‌کند استفاده کرده‌ایم.
- `ListToolsResult` شامل اطلاعاتی درباره همه ابزارها از جمله نام‌ها، توضیحات و طرح‌های ورودی آن‌ها است.

عالی، حالا همه ویژگی‌ها را ثبت کرده‌ایم. حالا سوال این است که چه زمانی از آن‌ها استفاده کنیم؟ خوب، این کلاینت بسیار ساده است، ساده به این معنا که باید ویژگی‌ها را به طور صریح فراخوانی کنیم. در فصل بعدی، یک کلاینت پیشرفته‌تر ایجاد خواهیم کرد که به مدل زبان بزرگ خود (LLM) دسترسی دارد. فعلاً، بیایید ببینیم چگونه می‌توان ویژگی‌ها را در سرور فراخوانی کرد:

### -4- فراخوانی ویژگی‌ها

برای فراخوانی ویژگی‌ها باید مطمئن شویم که آرگومان‌های صحیح و در برخی موارد نام چیزی که می‌خواهیم فراخوانی کنیم را مشخص کرده‌ایم.

#### TypeScript

```typescript

// Read a resource
const resource = await client.readResource({
  uri: "file:///example.txt"
});

// Call a tool
const result = await client.callTool({
  name: "example-tool",
  arguments: {
    arg1: "value"
  }
});

// call prompt
const promptResult = await client.getPrompt({
    name: "review-code",
    arguments: {
        code: "console.log(\"Hello world\")"
    }
})
```

در کد بالا:

- یک منبع را خوانده‌ایم، منبع را با فراخوانی `readResource()` و مشخص کردن `uri` فراخوانی می‌کنیم. این چیزی است که احتمالاً در سمت سرور به این شکل خواهد بود:

    ```typescript
    server.resource(
        "readFile",
        new ResourceTemplate("file://{name}", { list: undefined }),
        async (uri, { name }) => ({
          contents: [{
            uri: uri.href,
            text: `Hello, ${name}!`
          }]
        })
    );
    ```

    مقدار `uri` ما `file://example.txt` با `file://{name}` در سرور مطابقت دارد. `example.txt` به `name` نگاشت خواهد شد.

- یک ابزار را فراخوانی کرده‌ایم، ابزار را با مشخص کردن `name` و `arguments` فراخوانی می‌کنیم، به این شکل:

    ```typescript
    const result = await client.callTool({
        name: "example-tool",
        arguments: {
            arg1: "value"
        }
    });
    ```

- یک درخواست را دریافت کرده‌ایم، برای دریافت درخواست، `getPrompt()` را با `name` و `arguments` فراخوانی می‌کنیم. کد سرور به این شکل است:

    ```typescript
    server.prompt(
        "review-code",
        { code: z.string() },
        ({ code }) => ({
            messages: [{
            role: "user",
            content: {
                type: "text",
                text: `Please review this code:\n\n${code}`
            }
            }]
        })
    );
    ```

    و کد کلاینت شما برای مطابقت با چیزی که در سرور اعلام شده است به این شکل خواهد بود:

    ```typescript
    const promptResult = await client.getPrompt({
        name: "review-code",
        arguments: {
            code: "console.log(\"Hello world\")"
        }
    })
    ```

#### Python

```python
# Read a resource
print("READING RESOURCE")
content, mime_type = await session.read_resource("greeting://hello")

# Call a tool
print("CALL TOOL")
result = await session.call_tool("add", arguments={"a": 1, "b": 7})
print(result.content)
```

در کد بالا:

- یک منبع به نام `greeting` را با استفاده از `read_resource` فراخوانی کرده‌ایم.
- یک ابزار به نام `add` را با استفاده از `call_tool` فراخوانی کرده‌ایم.

#### .NET

1. بیایید کدی برای فراخوانی یک ابزار اضافه کنیم:

  ```csharp
  var result = await mcpClient.CallToolAsync(
      "Add",
      new Dictionary<string, object?>() { ["a"] = 1, ["b"] = 3  },
      cancellationToken:CancellationToken.None);
  ```

1. برای چاپ نتیجه، این کد را برای مدیریت آن اضافه کنید:

  ```csharp
  Console.WriteLine(result.Content.First(c => c.Type == "text").Text);
  // Sum 4
  ```

#### Java

```java
// Call various calculator tools
CallToolResult resultAdd = client.callTool(new CallToolRequest("add", Map.of("a", 5.0, "b", 3.0)));
System.out.println("Add Result = " + resultAdd);

CallToolResult resultSubtract = client.callTool(new CallToolRequest("subtract", Map.of("a", 10.0, "b", 4.0)));
System.out.println("Subtract Result = " + resultSubtract);

CallToolResult resultMultiply = client.callTool(new CallToolRequest("multiply", Map.of("a", 6.0, "b", 7.0)));
System.out.println("Multiply Result = " + resultMultiply);

CallToolResult resultDivide = client.callTool(new CallToolRequest("divide", Map.of("a", 20.0, "b", 4.0)));
System.out.println("Divide Result = " + resultDivide);

CallToolResult resultHelp = client.callTool(new CallToolRequest("help", Map.of()));
System.out.println("Help = " + resultHelp);
```

در کد بالا:

- چندین ابزار ماشین‌حساب را با استفاده از متد `callTool()` و اشیاء `CallToolRequest` فراخوانی کرده‌ایم.
- هر فراخوانی ابزار نام ابزار و یک `Map` از آرگومان‌های مورد نیاز توسط آن ابزار را مشخص می‌کند.
- ابزارهای سرور انتظار پارامترهای خاصی (مانند "a"، "b" برای عملیات ریاضی) دارند.
- نتایج به عنوان اشیاء `CallToolResult` بازگردانده می‌شوند که پاسخ سرور را شامل می‌شوند.

### -5- اجرای کلاینت

برای اجرای کلاینت، دستور زیر را در ترمینال تایپ کنید:

#### TypeScript

ورودی زیر را به بخش "scripts" در *package.json* اضافه کنید:

```json
"client": "tsx && node build/client.js"
```

```sh
npm run client
```

#### Python

کلاینت را با دستور زیر فراخوانی کنید:

```sh
python client.py
```

#### .NET

```sh
dotnet run
```

#### Java

ابتدا مطمئن شوید که سرور MCP شما روی `http://localhost:8080` اجرا می‌شود. سپس کلاینت را اجرا کنید:

```bash
# Build you project
./mvnw clean compile

# Run the client
./mvnw exec:java -Dexec.mainClass="com.microsoft.mcp.sample.client.SDKClient"
```

به طور جایگزین، می‌توانید پروژه کامل کلاینت ارائه‌شده در پوشه راه‌حل `03-GettingStarted\02-client\solution\java` را اجرا کنید:

```bash
# Navigate to the solution directory
cd 03-GettingStarted/02-client/solution/java

# Build and run the JAR
./mvnw clean package
java -jar target/calculator-client-0.0.1-SNAPSHOT.jar
```

## تکلیف

در این تکلیف، شما از آنچه در ایجاد یک کلاینت یاد گرفته‌اید استفاده خواهید کرد، اما کلاینت خود را ایجاد خواهید کرد.

در اینجا یک سرور وجود دارد که باید از طریق کد کلاینت خود فراخوانی کنید، ببینید آیا می‌توانید ویژگی‌های بیشتری به سرور اضافه کنید تا آن را جالب‌تر کنید.

### TypeScript

```typescript
import { McpServer, ResourceTemplate } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// Create an MCP server
const server = new McpServer({
  name: "Demo",
  version: "1.0.0"
});

// Add an addition tool
server.tool("add",
  { a: z.number(), b: z.number() },
  async ({ a, b }) => ({
    content: [{ type: "text", text: String(a + b) }]
  })
);

// Add a dynamic greeting resource
server.resource(
  "greeting",
  new ResourceTemplate("greeting://{name}", { list: undefined }),
  async (uri, { name }) => ({
    contents: [{
      uri: uri.href,
      text: `Hello, ${name}!`
    }]
  })
);

// Start receiving messages on stdin and sending messages on stdout

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("MCPServer started on stdin/stdout");
}

main().catch((error) => {
  console.error("Fatal error: ", error);
  process.exit(1);
});
```

### Python

```python
# server.py
from mcp.server.fastmcp import FastMCP

# Create an MCP server
mcp = FastMCP("Demo")


# Add an addition tool
@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b


# Add a dynamic greeting resource
@mcp.resource("greeting://{name}")
def get_greeting(name: str) -> str:
    """Get a personalized greeting"""
    return f"Hello, {name}!"

```

### .NET

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);
builder.Logging.AddConsole(consoleLogOptions =>
{
    // Configure all logs to go to stderr
    consoleLogOptions.LogToStandardErrorThreshold = LogLevel.Trace;
});

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithToolsFromAssembly();
await builder.Build().RunAsync();

[McpServerToolType]
public static class CalculatorTool
{
    [McpServerTool, Description("Adds two numbers")]
    public static string Add(int a, int b) => $"Sum {a + b}";
}
```

این پروژه را ببینید تا ببینید چگونه می‌توانید [درخواست‌ها و منابع اضافه کنید](https://github.com/modelcontextprotocol/csharp-sdk/blob/main/samples/EverythingServer/Program.cs).

همچنین، این لینک را بررسی کنید برای نحوه فراخوانی [درخواست‌ها و منابع](https://github.com/modelcontextprotocol/csharp-sdk/blob/main/src/ModelContextProtocol/Client/).

## راه‌حل

پوشه **راه‌حل** شامل پیاده‌سازی‌های کامل و آماده اجرا کلاینت است که تمام مفاهیم پوشش داده‌شده در این آموزش را نشان می‌دهد. هر راه‌حل شامل کد کلاینت و سرور است که به صورت جداگانه و پروژه‌های مستقل سازماندهی شده‌اند.

### 📁 ساختار راه‌حل

دایرکتوری راه‌حل بر اساس زبان برنامه‌نویسی سازماندهی شده است:

```text
solution/
├── typescript/          # TypeScript client with npm/Node.js setup
│   ├── package.json     # Dependencies and scripts
│   ├── tsconfig.json    # TypeScript configuration
│   └── src/             # Source code
├── java/                # Java Spring Boot client project
│   ├── pom.xml          # Maven configuration
│   ├── src/             # Java source files
│   └── mvnw            # Maven wrapper
├── python/              # Python client implementation
│   ├── client.py        # Main client code
│   ├── server.py        # Compatible server
│   └── README.md        # Python-specific instructions
├── dotnet/              # .NET client project
│   ├── dotnet.csproj    # Project configuration
│   ├── Program.cs       # Main client code
│   └── dotnet.sln       # Solution file
└── server/              # Additional .NET server implementation
    ├── Program.cs       # Server code
    └── server.csproj    # Server project file
```

### 🚀 هر راه‌حل شامل چه چیزی است

هر راه‌حل خاص زبان ارائه می‌دهد:

- **پیاده‌سازی کامل کلاینت** با تمام ویژگی‌های آموزش
- **ساختار پروژه کاری** با وابستگی‌ها و پیکربندی مناسب
- **اسکریپت‌های ساخت و اجرا** برای راه‌اندازی و اجرا آسان
- **README دقیق** با دستورالعمل‌های خاص زبان
- **نمونه‌های مدیریت خطا** و پردازش نتایج

### 📖 استفاده از راه‌حل‌ها

1. **به پوشه زبان مورد نظر خود بروید**:

   ```bash
   cd solution/typescript/    # For TypeScript
   cd solution/java/          # For Java
   cd solution/python/        # For Python
   cd solution/dotnet/        # For .NET
   ```

2. **دستورالعمل‌های README را دنبال کنید** در هر پوشه برای:
   - نصب وابستگی‌ها
   - ساخت پروژه
   - اجرای کلاینت

3. **خروجی نمونه** که باید ببینید:

   ```text
   Prompt: Please review this code: console.log("hello");
   Resource template: file
   Tool result: { content: [ { type: 'text', text: '9' } ] }
   ```

برای مستندات کامل و دستورالعمل‌های گام به گام، ببینید: **[📖 مستندات راه‌حل](./solution/README.md)**

## 🎯 مثال‌های کامل

ما پیاده‌سازی‌های کامل و کاری کلاینت را برای تمام زبان‌های برنامه‌نویسی پوشش داده‌شده در این آموزش ارائه کرده‌ایم. این مثال‌ها عملکرد کامل توضیح داده‌شده در بالا را نشان می‌دهند و می‌توانند به عنوان پیاده‌سازی‌های مرجع یا نقاط شروع برای پروژه‌های خودتان استفاده شوند.

### مثال‌های کامل موجود

| زبان | فایل | توضیحات |
|------|------|---------|
| **Java** | [`client_example_java.java`](../../../../03-GettingStarted/02-client/client_example_java.java) | کلاینت کامل Java با استفاده از انتقال SSE با مدیریت خطای جامع |
| **C#** | [`client_example_csharp.cs`](../../../../03-GettingStarted/02-client/client_example_csharp.cs) | کلاینت کامل C# با استفاده از انتقال stdio و راه‌اندازی خودکار سرور |
| **TypeScript** | [`client_example_typescript.ts`](../../../../03-GettingStarted/02-client/client_example_typescript.ts) | کلاینت کامل TypeScript با پشتیبانی کامل از پروتکل MCP |
| **Python** | [`client_example_python.py`](../../../../03-GettingStarted/02-client/client_example_python.py) | کلاینت کامل Python با استفاده از الگوهای async/await |

هر مثال کامل شامل موارد زیر است:

- ✅ **ایجاد اتصال** و مدیریت خطا
- ✅ **کشف سرور** (ابزارها، منابع، درخواست‌ها در صورت وجود)
- ✅ **عملیات ماشین‌حساب** (جمع، تفریق، ضرب، تقسیم، کمک)
- ✅ **پردازش نتایج** و خروجی قالب‌بندی‌شده
- ✅ **مدیریت خطای جامع**
- ✅ **کد تمیز و مستند** با توضیحات گام به گام

### شروع کار با مثال‌های کامل

1. **زبان مورد نظر خود را از جدول بالا انتخاب کنید**
2. **فایل مثال کامل را بررسی کنید** تا پیاده‌سازی کامل را درک کنید
3. **مثال را اجرا کنید** با دنبال کردن دستورالعمل‌ها در [`complete_examples.md`](./complete_examples.md)
4. **مثال را تغییر دهید و گسترش دهید** برای مورد استفاده خاص خود

برای مستندات دقیق درباره اجرای و سفارشی‌سازی این مثال‌ها، ببینید: **[📖 مستندات مثال‌های کامل](./complete_examples.md)**

### 💡 راه‌حل در مقابل مثال‌های کامل

| **پوشه راه‌حل** | **مثال‌های کامل** |
|----------------|------------------|
| ساختار کامل پروژه با فایل‌های ساخت | پیاده‌سازی‌های تک‌فایلی |
| آماده اجرا با وابستگی‌ها | مثال‌های کد متمرکز |
| تنظیمات شبیه به تولید | مرجع آموزشی |
| ابزارهای خاص زبان | مقایسه بین زبان‌ها |
هر دو رویکرد ارزشمند هستند - از **پوشه‌ی پروژه** برای پروژه‌های کامل استفاده کنید و از **نمونه‌های کامل** برای یادگیری و مرجع.

## نکات کلیدی

نکات کلیدی این فصل درباره‌ی کلاینت‌ها به شرح زیر است:

- می‌توان از آن‌ها برای کشف و فراخوانی قابلیت‌های سرور استفاده کرد.
- می‌توانند هنگام شروع به کار خود، یک سرور را نیز راه‌اندازی کنند (مانند این فصل)، اما کلاینت‌ها می‌توانند به سرورهای در حال اجرا نیز متصل شوند.
- در کنار ابزارهایی مانند Inspector که در فصل قبل توضیح داده شد، راهی عالی برای آزمایش قابلیت‌های سرور هستند.

## منابع اضافی

- [ساخت کلاینت‌ها در MCP](https://modelcontextprotocol.io/quickstart/client)

## نمونه‌ها

- [ماشین حساب جاوا](../samples/java/calculator/README.md)
- [ماشین حساب .Net](../../../../03-GettingStarted/samples/csharp)
- [ماشین حساب جاوااسکریپت](../samples/javascript/README.md)
- [ماشین حساب تایپ‌اسکریپت](../samples/typescript/README.md)
- [ماشین حساب پایتون](../../../../03-GettingStarted/samples/python)

## مرحله بعد

- بعدی: [ایجاد یک کلاینت با LLM](../03-llm-client/README.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.