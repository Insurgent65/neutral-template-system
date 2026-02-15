# Neutral TS: The Comprehensive Guide to the Language-Agnostic Web Template Engine

## Table of Contents

1. [Introduction](#introduction)
2. [What is Neutral TS?](#what-is-neutral-ts)
3. [Core Philosophy and Design Principles](#core-philosophy-and-design-principles)
4. [Architecture Overview](#architecture-overview)
5. [Installation and Setup](#installation-and-setup)
6. [BIFs: The Building Blocks of Neutral TS](#bifs-the-building-blocks)
7. [Template Syntax Deep Dive](#template-syntax-deep-dive)
8. [The Schema System](#the-schema-system)
9. [IPC Architecture](#ipc-architecture)
10. [Security Features](#security-features)
11. [Internationalization and Localization](#internationalization-and-localization)
12. [Caching Mechanisms](#caching-mechanisms)
13. [Working with Data](#working-with-data)
14. [Advanced Features](#advanced-features)
15. [Integration with Multiple Languages](#integration-with-multiple-languages)
16. [Best Practices](#best-practices)
17. [Performance Considerations](#performance-considerations)
18. [Comparison with Other Template Engines](#comparison-with-other-template-engines)
19. [Real-World Use Cases](#real-world-use-cases)
20. [Future Directions](#future-directions)
21. [Conclusion](#conclusion)

---

## Introduction

In the ever-evolving landscape of web development, template engines have become indispensable tools for generating dynamic content. From simple variable interpolation to complex conditional rendering and iteration, template engines bridge the gap between raw data and polished HTML output. However, one persistent challenge has plagued developers across the industry: the fragmentation of template solutions across different programming languages and frameworks.

Enter **Neutral TS**, a revolutionary template engine that dares to ask a fundamental question: *What if you could write a template once and use it everywhere, regardless of the programming language your backend employs?*

Neutral TS is a template engine for the Web, designed to work with any programming language (language-agnostic) via IPC/Package and natively as library/crate in Rust. This groundbreaking approach addresses a long-standing pain point in software development, where teams often find themselves maintaining multiple template implementations across different services written in various languages.

This comprehensive guide will explore every facet of Neutral TS, from its foundational principles to advanced usage patterns, providing developers with the knowledge needed to leverage this powerful tool in their projects.

---

## What is Neutral TS?

Neutral TS is a safe, modular, language-agnostic template engine built in Rust. It works as a native Rust library or via IPC for other languages like Python and PHP. With Neutral TS you can reuse the same template across multiple languages with consistent results.

At its core, Neutral TS represents a paradigm shift in how we think about template engines. Traditional template engines are tightly coupled to their host programming language—Jinja2 is for Python, Blade is for PHP, ERB is for Ruby, and so on. While this tight integration offers certain conveniences, it also creates silos that can complicate multi-language architectures and make template reuse virtually impossible across language boundaries.

Similarly, Neutral TS has an IPC server, and each programming language has a client. No matter where you run the template, the result will always be the same. Thanks to this, and to its modular and parameterizable design, it is possible to create utilities or plugins that will work everywhere.

### The Name: Why "Neutral"?

The name "Neutral" perfectly encapsulates the engine's philosophy. It doesn't favor any particular programming language or platform. It maintains neutrality by providing consistent output regardless of the calling environment. This neutrality extends to:

- **Language neutrality**: Works with Rust, Python, PHP, Node.js, Go, and potentially any language capable of TCP/IP communication
- **Platform neutrality**: Runs on Linux, Windows, macOS, and other operating systems
- **Framework neutrality**: Not tied to any specific web framework

### Key Characteristics

Other key features include: Safe Language-agnostic Modular Parameterizable How It Works Neutral TS integrates with other programming languages in two main ways: In Rust: You can use Neutral TS as a library by downloading the crate.

The engine distinguishes itself through several key characteristics:

1. **Safety First**: Built in Rust, one of the safest systems programming languages available
2. **Language Agnostic**: True cross-language compatibility through IPC
3. **Modular Architecture**: Components can be used independently
4. **Parameterizable Design**: Highly configurable to meet various needs
5. **Consistent Output**: Identical templates produce identical results across all supported languages

---

## Core Philosophy and Design Principles

### The Database Analogy

One of the most illuminating ways to understand Neutral TS's architecture is through the database analogy provided by its creators:

Imagine a database. It has a server, and different programming languages access the data through a client. This means that if you run a "SELECT ..." query from any programming language, the result will always be the same.

Just as a database server provides consistent data access regardless of whether you're querying from Python, Java, or Ruby, Neutral TS provides consistent template rendering regardless of your backend language. Just like an SQL query returns the same data from any language, a Neutral TS template returns the same HTML from Python, PHP, Rust… with added security isolation.

### Design by Convention

Neutral TS employs several design principles that make templates predictable and secure:

By design the templates do not have access to arbitrary application data, the data has to be passed to the template in a JSON, then the data that you have not included in the JSON cannot be read by the template.

This explicit data passing mechanism serves multiple purposes:

1. **Security**: Templates cannot access data they shouldn't have
2. **Predictability**: What you pass is what you get
3. **Portability**: The JSON schema is universally readable across languages
4. **Documentation**: The schema serves as implicit documentation of template requirements

### Modularity at Every Level

Thanks to this, and to its modular and parameterizable design, it is possible to create utilities or plugins that will work everywhere. For example, you can develop tools to create forms or form fields and create your own libraries of "snippets" for repetitive tasks.

Modularity permeates every aspect of Neutral TS:

- **Snippets**: Reusable template fragments
- **Schemas**: Composable configuration objects
- **BIFs**: Independent, nestable built-in functions
- **Caching**: Granular cache control at any level

---

## Architecture Overview

### Two Modes of Operation

Neutral TS operates in two distinct modes, each suited to different use cases:

#### 1. Native Rust Library Mode

In Rust: You can use Neutral TS template engine as a library by downloading the crate.

When used directly in Rust applications, Neutral TS operates as a native library without any IPC overhead. This mode offers:

- Maximum performance
- Direct memory access
- Zero network latency
- Simplified deployment (no separate server process)

#### 2. IPC Mode (Cross-Language)

In other programming languages: Inter-Process Communication (IPC) is necessary, similar to how databases like MariaDB work.

For non-Rust languages, Neutral TS uses a client-server architecture:

IPC Server: Universal standalone application (written in Rust) for all languages - download from: IPC Server · IPC Clients: Language-specific libraries to include in your project - available at: IPC Clients

### IPC Server Architecture

Neutral TS IPC Server for template rendering, a TCP/IP interface for Neutral TS template engine.

The IPC server is a standalone Rust application that:

- Listens for template rendering requests over TCP/IP
- Processes requests using the Neutral TS engine
- Returns rendered output to clients
- Manages caching and resource allocation

### Client Libraries

Examples for Rust, Python, PHP, Node.js and Go here: download.

Each supported language has its own client library that:

- Handles TCP/IP communication with the server
- Marshals data into the required JSON format
- Provides a language-idiomatic API
- Handles error responses gracefully

---

## Installation and Setup

### Installing the Rust Crate

For Rust developers, installation is straightforward through Cargo:

```toml
[dependencies]
neutralts = "1.3.0"
```

### Setting Up the IPC Server

For non-Rust languages, you'll need to download and run the IPC server:

IPC Server: Universal standalone application (written in Rust) for all languages - download from: IPC Server

The IPC server can be downloaded from the official releases page and run as a standalone application or as a system service.

### Installing Language-Specific Clients

#### Python

The Python client is available on PyPI as `neutraltemplate`. Installation:

```bash
pip install neutraltemplate
```

#### PHP, Node.js, and Go

Client libraries for these languages are available through their respective package managers or as direct downloads from the IPC Clients repository.

### Basic Configuration

Configuration in Neutral TS is handled through a JSON schema. Here's a minimal configuration:

```json
{
  "config": {
    "comments": "remove",
    "cache_disable": false
  },
  "data": {
    "title": "My Page"
  }
}
```

---

## BIFs: The Building Blocks of Neutral TS

### Understanding BIFs

The main element of Neutral TS is the BIF (Build-in function), would be the equivalent of functions and would display an output, the output is always a string or nothing (empty string).

BIFs (Built-in Functions) are the fundamental building blocks of Neutral TS templates. They encapsulate all template logic, from simple variable display to complex conditional rendering and iteration.

### BIF Syntax Structure

```
    .-- open bif
    |   .-- bif name
    |   |      .-- name separator
    |   |      |     .-- params
    |   |      |     |          .-- params/code separator
    |   |      |     |          |    .-- code
    |   |      |     |          |    |      .-- close bif
    v   v      v     v          v    v      v
   -- -----    -  --------     --  -----   --
   {:snippet; snipname    >>   ...        :}
   ------------------------------
              ^ -------------------
              |          ^
              |          |
              |          `-- source
              `-- Built-in function
```

The general syntax for a BIF is:

```
{:bifname; params >> code :}
```

Where:
- `{:` opens the BIF
- `bifname` is the function name
- `;` separates the name from parameters
- `params` are the function parameters
- `>>` separates parameters from the code block
- `code` is the template content
- `:}` closes the BIF

### Block Structure and Nesting

Neutral TS template engine is based on BIFs with block structure, we call the set of nested BIFs of the same level a block

By design all Bifs can be nested and there can be a Bif anywhere in another Bif except in the name.

This nesting capability is crucial for building complex templates:

```
{:coalesce;
  {:code;
    {:filled; user >>
      Welcome, {:;user->name:}!
    :}
  :}
  {:code;
    Welcome, Guest!
  :}
:}
```

### Short-Circuit Evaluation

Short circuit at block level, if varname is not defined, the following '>>' is not evaluated: 
```
{:defined; varname >> 
    {:code; {:code; ... :} :} 
:}
```

This short-circuit behavior is crucial for performance and safety—expensive operations inside a BIF's code block aren't evaluated if the condition fails.

### Core BIF Categories

#### 1. Variable Display

The simplest BIF displays variable values:

```
{:;variablename:}
{:;user->profile->name:}
```

The arrow syntax (`->`) navigates nested JSON structures.

#### 2. Conditional BIFs

**filled**: Outputs code if a variable has a non-empty value
```
{:filled; varname >> Hello! :}
```

**defined**: Checks if a variable exists
```
{:defined; varname >> Variable exists :}
```

**array**: Checks if a variable is an array/object
{:array; variable >> code :} {:array; varname >> this shown if varname is array :} Note that there is no distinction between objects and arrays.

#### 3. Iteration BIFs

**each**: Iterates over arrays
{:^each; {:param; array-name :} key value >> {:array; value >> {:;:} {:;key:}: {:snippet; iterate-array-next-level :} :}{:else; {:;:} {:;key:}={:;value:} :} :}

#### 4. Control Flow BIFs

**else**: Provides fallback content
{:else; code :} {:;varname:}{:else; shown if varname is empty :}

**coalesce**: Returns the first non-empty block
```
{:coalesce;
  {:code; {:;primary:} :}
  {:code; {:;secondary:} :}
  {:code; Default :}
:}
```

#### 5. Snippets

Snippets are reusable template fragments:

```
{:snippet; header >> 
  <header>
    <h1>{:;site->name:}</h1>
  </header>
:}

{:snippet; header :}
```

"Calling a snippet that does not exist is not an error, it will result in a empty string that we can evaluate with else. {:snippet; option-{:;varname:} :} {:else; {:snippet; option-default :} :}"

#### 6. BIF Negation and Modifiers

BIFs can be modified with prefixes:
{:!array; ... :} {:+array; ... :} {:^array; ...

- `!` - Negation (NOT)
- `+` - Additional modifier
- `^` - Special behavior modifier

---

## Template Syntax Deep Dive

### Comments

Neutral TS supports comments that can be configured to be removed from output:

```
{:* This is a comment *:}
```

The behavior is controlled by the config:
```json
{
  "config": {
    "comments": "remove"
  }
}
```

### Flexible Delimiters

"Any delimiter can be used, but a delimiter is always required, even if only one parameter is used. {:fetch; \"url\" >> ... :} {:fetch; ~url~event~ >> ... :} {:fetch; #url#event# >> ... :} {:fetch; |url|event| >> ... :} {:fetch; 'url'event' >> ... :}"

"The reason you can use different delimiters is to use one that does not appear in the parameter, using / would cause problems with the url so we use \" or any other"

This flexibility prevents escaping nightmares when parameters contain the delimiter character.

### The Fetch BIF

"Neutral TS template engine provides a basic JavaScript to perform simple fetch requests"

{:fetch; |url|event|wrapperId|class|id|name| >> code :} Code is the html that will be displayed before performing the fetch, it can be a message, a button or the fields of a form.

Example:
```html
{:fetch; "/api/user-data" >> 
  <div>Loading user data...</div>
:}
```

### Status Code Handling

"If you use the bif \"exit\" or \"redirect\" it is necessary to manage the status codes in the application... let status_code = template.get_status_code(); // e.g.: 500... let status_text = template.get_status_text(); // e.g.: Internal Server Error... let status_param = template.get_status_param(); // e.g.: template error x"

Templates can control HTTP responses:

```rust
let template = Template::from_file_value("file.ntpl", schema).unwrap();
let content = template.render();
let status_code = template.get_status_code();
let status_text = template.get_status_text();
let status_param = template.get_status_param();
```

---

## The Schema System

### Schema Structure

The schema is a JSON where we define the data that will represent the templates, as well as the configuration and translations, although you can render a template without schema since Neutral TS provides one by default, it will be of little use since it has no data.

A complete schema has several sections:

```json
{
  "config": { ... },
  "inherit": { ... },
  "locale": { ... },
  "data": { ... }
}
```

### Configuration Section

"You need two things, a template file and a json schema: { \"config\": { \"comments\": \"remove\", \"cache_prefix\": \"neutral-cache\", \"cache_dir\": \"\", \"cache_on_post\": false, \"cache_on_get\": true, \"cache_on_cookies\": true, \"cache_disable\": false, \"filter_all\": false, \"disable_js\": false }"

Configuration options include:

| Option | Description | Default |
|--------|-------------|---------|
| `comments` | How to handle comments ("remove", "keep") | "remove" |
| `cache_prefix` | Prefix for cache files | "neutral-cache" |
| `cache_dir` | Directory for cache storage | "" |
| `cache_on_post` | Cache POST requests | false |
| `cache_on_get` | Cache GET requests | true |
| `cache_on_cookies` | Cache when cookies present | true |
| `cache_disable` | Disable caching entirely | false |
| `filter_all` | Apply filters to all output | false |
| `disable_js` | Disable JavaScript generation | false |

### The CONTEXT Object

The schema includes a special CONTEXT object for web request data:

```json
{
  "data": {
    "CONTEXT": {
      "ROUTE": "/users/profile",
      "HOST": "example.com",
      "GET": { "id": "123" },
      "POST": {},
      "HEADERS": {},
      "FILES": {},
      "COOKIES": {},
      "SESSION": {},
      "ENV": {}
    }
  }
}
```

This standardized structure ensures consistent access to request data across all languages.

### Data Section

The data section contains all variables available to templates:

```json
{
  "data": {
    "site_name": "MySite",
    "site": {
      "name": "MySite",
      "url": "https://mysite.com"
    },
    "user": {
      "name": "John",
      "email": "john@example.com"
    }
  }
}
```

---

## IPC Architecture

### Why IPC?

It works as a native Rust library or via IPC for other languages like Python and PHP.

Inter-Process Communication enables Neutral TS to serve as a universal template engine while maintaining its Rust-based core for performance and safety.

### Architecture Benefits

"The IPC architecture provides important security benefits: Sandboxed execution: Templates run in isolated processes · Reduced attack surface: Main application protected from template engine vulnerabilities... Crash containment: Template engine failures don't affect the main application · Zero-downtime updates: IPC server can be updated independently without restarting client applications"

The IPC approach offers significant advantages:

1. **Sandboxed Execution**: Templates run in isolated processes
2. **Reduced Attack Surface**: Main application protected from template engine vulnerabilities
3. **Resource Control**: Memory and CPU limits can be enforced at server level
4. **Crash Containment**: Template engine failures don't affect the main application
5. **Zero-Downtime Updates**: IPC server can be updated independently without restarting client applications

### Performance Considerations

The IPC approach introduces performance overhead due to inter-process communication. The impact varies depending on: ... For most web applications, the security and interoperability benefits compensate for the performance overhead.

Factors affecting IPC performance:

- Network latency (mitigated by local socket communication)
- Serialization/deserialization overhead
- Template complexity
- Caching effectiveness

For performance-critical applications, consider:
- Running the IPC server on the same machine
- Using Unix domain sockets instead of TCP where possible
- Aggressive caching strategies
- Connection pooling in client libraries

### Easy Updates

"Easy updates: No application recompilation needed - simply update the IPC server for engine improvements"

This decoupled architecture means template engine updates don't require redeploying your entire application stack.

---

## Security Features

### Explicit Data Passing

By design the templates do not have access to arbitrary application data, the data has to be passed to the template in a JSON, then the data that you have not included in the JSON cannot be read by the template.

This is perhaps the most fundamental security feature. Unlike some template engines that have access to the entire application context, Neutral TS requires explicit data passing. This means:

- No accidental exposure of sensitive data
- Clear audit trail of what data templates can access
- Easier security reviews

### Process Isolation

"The IPC architecture provides important security benefits: Sandboxed execution: Templates run in isolated processes · Reduced attack surface: Main application protected from template engine vulnerabilities · Resource control: Memory and CPU limits can be enforced at server level · Crash containment: Template engine failures don't affect the main application"

When using IPC mode, templates run in a completely separate process:

- Memory isolation prevents data leaks
- CPU limits prevent denial-of-service
- Crashes are contained to the template server

### Built in Rust

Neutral TS is built in Rust, which provides:

- Memory safety without garbage collection
- No buffer overflows
- No null pointer dereferences
- Thread safety guarantees

### Allow Lists and Restrictions

Declare supports wildcards, see bif "declare" for details. ... {:allow; templates >> file.txt :}{:else; fails :}

The `allow` BIF enables whitelisting:

```
{:allow; templates >> file.ntpl :}{:else; File not allowed :}
{:allow; languages >> es-ES :}{:else; Language not supported :}
```

---

## Internationalization and Localization

### Translation System

"Neutral TS template engine provides powerful and easy-to-use translation utilities… define the translation in a JSON"

Neutral TS has built-in support for multilingual content. Translations are defined in the schema:

```json
{
  "locale": {
    "current": "en",
    "trans": {
      "en": {
        "Hello": "Hello",
        "Welcome": "Welcome"
      },
      "es": {
        "Hello": "Hola",
        "Welcome": "Bienvenido"
      },
      "de": {
        "Hello": "Hallo",
        "Welcome": "Willkommen"
      },
      "fr": {
        "Hello": "Bonjour",
        "Welcome": "Bienvenue"
      }
    }
  }
}
```

### Using Translations in Templates

The `trans` BIF handles translations:

```
{:trans; Hello :}
```

This outputs:
- "Hello" when current locale is "en"
- "Hola" when current locale is "es"
- "Hallo" when current locale is "de"
- "Bonjour" when current locale is "fr"

### Reference-Based Translations

For longer translation keys, you can use references:

```json
{
  "trans": {
    "en": {
      "ref:greeting-nts": "Hello and welcome to our site!"
    },
    "es": {
      "ref:greeting-nts": "¡Hola y bienvenido a nuestro sitio!"
    }
  }
}
```

```
{:trans; ref:greeting-nts :}
```

### Fallback Behavior

If a translation key doesn't exist for the current locale, the original text is returned, making it safe to use `trans` everywhere even if not all text is translated yet.

---

## Caching Mechanisms

### Modular Caching

"The cache is modular, allowing only parts of the template to be included in the cache"

Neutral TS provides fine-grained control over caching at multiple levels.

### Template-Level Caching

Cache an entire template:

```html
{:cache; /120/ >>
<!DOCTYPE html>
<html>
<head>
  <title>Cached Page</title>
</head>
<body>
  <!-- Content cached for 120 seconds -->
</body>
</html>
:}
```

### Partial Caching

Cache specific sections:

```html
<!DOCTYPE html>
<html>
<body>
  {:cache; /3600/ >>
    <nav><!-- Expensive navigation, cached for 1 hour --></nav>
  :}
  
  <main><!-- Dynamic content --></main>
  
  {:cache; /600/ >>
    <aside><!-- Sidebar, cached for 10 minutes --></aside>
  :}
</body>
</html>
```

### Cache Exclusions

"Or exclude parts of the cache, the previous example would be much better like this: {:cache; /120/ >> <!DOCTYPE html> <html>..."

Use `!cache` to exclude sections from parent caches:

```html
{:cache; /120/ >>
<!DOCTYPE html>
<html>
<body>
  <div>Cached content</div>
  {:!cache; {:date; %H:%M:%S :} :}
  <div>More cached content</div>
</body>
</html>
:}
```

The timestamp remains dynamic while surrounding content is cached.

### Cache Configuration

Control caching behavior through configuration:

```json
{
  "config": {
    "cache_prefix": "myapp-neutral-cache",
    "cache_dir": "/tmp/neutralts",
    "cache_on_post": false,
    "cache_on_get": true,
    "cache_on_cookies": true,
    "cache_disable": false
  }
}
```

---

## Working with Data

### JSON Data Types

"The data is defined in a JSON: \"data\": { \"true\": true, \"false\": false, \"hello\": \"hello\", \"zero\": \"0\", \"one\": \"1\", \"spaces\": \" \", \"empty\": \"\", \"null\": null, \"emptyarr\": []..."

Neutral TS handles all standard JSON types:

- **Booleans**: true, false
- **Strings**: Any text value
- **Numbers**: Integer and floating-point
- **Null**: The null value
- **Arrays**: Ordered collections
- **Objects**: Key-value pairs

### Accessing Nested Data

Use arrow syntax for nested structures:

```
{:;user->profile->address->city:}
{:;settings->theme->colors->primary:}
```

### Iterating Over Collections

The `each` BIF iterates over arrays and objects:

```
{:each; users key user >>
  <div class="user">
    <span>{:;key:}</span>: {:;user->name:}
  </div>
:}
```

### Type Checking

Check if data is an array/object:

```
{:array; items >>
  <!-- items is an array/object -->
  {:each; items key item >> ... :}
:}{:else;
  <!-- items is not an array -->
  {:;items:}
:}
```

### Coalescing Values

Get the first non-empty value:

```
{:coalesce;
  {:code; {:;user->nickname:} :}
  {:code; {:;user->name:} :}
  {:code; Anonymous :}
:}
```

---

## Advanced Features

### The Eval BIF

{:eval; {:code; {:code; ... :} :} >> {:code; {:code; ... :} :} :}

The `eval` BIF enables dynamic template generation and execution, allowing templates to build and evaluate other template code.

### External Script Execution

"This feature is experimental. Executes a external script (currently only Python) and processes its output. The script receives parameters and can access the template schema. ... {:obj; { \"engine\": \"Python\", \"file\": \"script.py\", \"params\": {}, \"callback\": \"main\", \"template\": \"template.ntpl\" } :}"

The `obj` BIF allows executing external scripts:

```
{:obj; {
  "engine": "Python",
  "file": "script.py",
  "params": {"id": 123},
  "callback": "main",
  "template": "result.ntpl"
} :}
```

This powerful feature enables:
- Dynamic data fetching
- Complex calculations
- Integration with external services
- Custom business logic

### Dynamic Snippet Names

Build snippet names dynamically:

```
{:snippet; option-foo >> Option A :}
{:snippet; option-bar >> Option B :}
{:snippet; option-baz >> Option C :}

<!-- Call dynamically based on variable -->
{:snippet; option-{:;selectedOption:} :}
```

"This is clearer and less computationally expensive: {:snippet; option-foo >> ... :} {:snippet; option-bar >> ... :} {:snippet; option-{:;varname:} :}"

### Date Formatting

The `date` BIF formats dates:

```
{:date; %Y-%m-%d :}  <!-- 2026-02-13 -->
{:date; %H:%M:%S :}  <!-- 14:30:45 -->
{:date; %A, %B %d, %Y :}  <!-- Thursday, February 13, 2026 -->
```

---

## Integration with Multiple Languages

### Rust Integration

"In Rust it is enough with two methods, create the template with a file and a schema and then render: // Data let schema = json!({ \"data\": { \"hello\": \"Hello, World!\", \"site\": { \"name\": \"My Site\" } } }); // Create template // In file.ntpl use {:;hello:} and {:;site->name:} for show data. let template = Template::from_file_value(\"file.ntpl\", schema).unwrap(); // Render template let content = template.render();"

```rust
use neutralts::Template;
use serde_json::json;

// Create schema
let schema = json!({
    "data": {
        "hello": "Hello, World!",
        "site": {
            "name": "My Site"
        }
    }
});

// Create and render template
let template = Template::from_file_value("file.ntpl", schema).unwrap();
let content = template.render();
```

### Python Integration

Using the neutraltemplate package:

```python
from neutraltemplate import Template

schema = {
    "data": {
        "hello": "Hello, World!",
        "site": {
            "name": "My Site"
        }
    }
}

template = Template.from_file_value("file.ntpl", schema)
content = template.render()
```

### PHP Integration

```php
<?php
use NeutralTS\Template;

$schema = [
    "data" => [
        "hello" => "Hello, World!",
        "site" => [
            "name" => "My Site"
        ]
    ]
];

$template = Template::fromFileValue("file.ntpl", $schema);
$content = $template->render();
```

### Node.js Integration

```javascript
const { Template } = require('neutralts');

const schema = {
    data: {
        hello: "Hello, World!",
        site: {
            name: "My Site"
        }
    }
};

const template = Template.fromFileValue("file.ntpl", schema);
const content = template.render();
```

### Go Integration

```go
package main

import (
    "github.com/neutralts/client-go"
)

func main() {
    schema := map[string]interface{}{
        "data": map[string]interface{}{
            "hello": "Hello, World!",
            "site": map[string]interface{}{
                "name": "My Site",
            },
        },
    }
    
    template := neutralts.FromFileValue("file.ntpl", schema)
    content := template.Render()
}
```

### PWA Examples

All PWA examples use the same template: Neutral templates.

The official documentation includes Progressive Web App examples demonstrating how the same templates work across all supported languages.

Examples for Rust, Python, PHP, Node.js and Go here: download. All PWA examples use the same template: Neutral templates.

---

## Best Practices

### Template Organization

1. **Use Snippets for Reusable Components**
   ```
   {:snippet; button >> <button class="{:;class:}">{:;text:}</button> :}
   ```

2. **Organize Templates by Feature**
   ```
   templates/
   ├── layouts/
   │   ├── base.ntpl
   │   └── admin.ntpl
   ├── components/
   │   ├── header.ntpl
   │   ├── footer.ntpl
   │   └── nav.ntpl
   └── pages/
       ├── home.ntpl
       └── about.ntpl
   ```

3. **Keep Business Logic Out of Templates**
   Templates should display data, not compute it. Process data in your application before passing to templates.

### Schema Design

1. **Use Consistent Naming Conventions**
   ```json
   {
     "data": {
       "user_profile": { ... },
       "site_settings": { ... },
       "page_meta": { ... }
     }
   }
   ```

2. **Group Related Data**
   ```json
   {
     "data": {
       "navigation": {
         "main_menu": [...],
         "footer_links": [...]
       }
     }
   }
   ```

3. **Include Only Necessary Data**
   Don't pass entire database records; select only fields needed by the template.

### Performance Optimization

1. **Use Caching Wisely**
   - Cache static content aggressively
   - Use partial caching for mixed content
   - Exclude truly dynamic elements

2. **Minimize Nested Iterations**
   Deeply nested loops can impact performance.

3. **Preprocess Data**
   Format dates, calculate totals, etc., before passing to templates.

### Security Best Practices

1. **Never Pass Sensitive Data Unnecessarily**
   ```json
   // DON'T
   { "data": { "user": entireUserRecord } }
   
   // DO
   { "data": { "user": { "name": user.name, "avatar": user.avatar } } }
   ```

2. **Validate Input Data**
   Sanitize user-provided data before including in schemas.

3. **Use Allow Lists**
   Restrict which templates and resources can be accessed.

---

## Performance Considerations

### Native vs. IPC Mode

| Aspect | Native (Rust) | IPC |
|--------|--------------|-----|
| Latency | Minimal | Additional network hop |
| Memory | Shared with application | Separate process |
| Scaling | Application scaling | Independent scaling |
| Updates | Requires rebuild | Hot-swappable |

### Optimization Strategies

1. **Connection Pooling**
   Reuse IPC connections instead of creating new ones per request.

2. **Template Precompilation**
   If supported, precompile templates at startup.

3. **Efficient Caching**
   Implement multi-tier caching:
   - In-memory cache for hot templates
   - Disk cache for warm templates
   - Redis/Memcached for distributed caching

4. **Schema Optimization**
   - Keep schemas small
   - Avoid deeply nested structures
   - Use references for repeated data

### Benchmarking

Measure performance in your specific environment:

```rust
use std::time::Instant;

let start = Instant::now();
for _ in 0..1000 {
    let template = Template::from_file_value("test.ntpl", schema.clone()).unwrap();
    let _ = template.render();
}
let duration = start.elapsed();
println!("1000 renders: {:?}", duration);
```

---

## Comparison with Other Template Engines

### vs. Jinja2 (Python)

| Feature | Neutral TS | Jinja2 |
|---------|-----------|--------|
| Language Support | Multiple | Python only |
| Syntax | BIF-based | Django-like |
| Security | Process isolation | Sandboxed |
| Learning Curve | Moderate | Low |
| Ecosystem | Growing | Mature |

### vs. Blade (PHP)

| Feature | Neutral TS | Blade |
|---------|-----------|-------|
| Language Support | Multiple | PHP only |
| Framework Dependency | None | Laravel |
| Compilation | Runtime | Compiled |
| Extensibility | BIFs | Directives |

### vs. Handlebars (JavaScript)

| Feature | Neutral TS | Handlebars |
|---------|-----------|------------|
| Language Support | Multiple | JS (with ports) |
| Logic-less | No | Yes (mostly) |
| Helpers | BIFs | Custom helpers |
| Performance | Rust-speed | V8 speed |

### Unique Advantages of Neutral TS

1. **True Language Independence**: Same template, any backend
2. **Consistent Output**: Guaranteed identical results
3. **Security by Design**: Process isolation, explicit data passing
4. **Modern Architecture**: Built for microservices and polyglot environments
5. **Rust Performance**: Native Rust speed without the complexity

---

## Real-World Use Cases

### 1. Microservices Architecture

In a microservices environment with services written in different languages, Neutral TS allows sharing templates across all services:

```
┌─────────────────────────────────────────────────────────────┐
│                    Shared Templates                         │
│                   (templates/*.ntpl)                        │
└─────────────────────────────────────────────────────────────┘
        │              │              │              │
        ▼              ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ User Service │ │ Product Svc  │ │ Order Service│ │ Admin Panel  │
│   (Python)   │ │    (Go)      │ │    (Rust)    │ │    (PHP)     │
└──────────────┘ └──────────────┘ └──────────────┘ └──────────────┘
        │              │              │              │
        └──────────────┴──────────────┴──────────────┘
                              │
                              ▼
                    ┌──────────────┐
                    │ Neutral TS   │
                    │ IPC Server   │
                    └──────────────┘
```

### 2. Migration Projects

When migrating from one technology stack to another, Neutral TS enables gradual migration:

1. Convert templates to Neutral TS format
2. Run both old and new systems using the same templates
3. Migrate services one at a time
4. Maintain visual consistency throughout

### 3. Multi-Platform Products

Build once, deploy everywhere:

- Main web application (Rust/Actix)
- Admin dashboard (Python/Django)  
- Partner portal (PHP/Laravel)
- All using identical templates

### 4. Template Marketplace

Thanks to this, and to its modular and parameterizable design, it is possible to create utilities or plugins that will work everywhere. For example, you can develop tools to create forms or form fields and create your own libraries of "snippets" for repetitive tasks.

Create shareable template libraries:

- Form component libraries
- UI kit templates
- Email templates
- Report templates

### 5. White-Label Solutions

SaaS products with customizable themes benefit from:

- Consistent theming across all integrations
- Partner-customizable templates
- Safe template execution

---

## Future Directions

### Expanding Language Support

The Neutral TS community continues to develop IPC clients for additional languages. The TCP/IP-based protocol makes it possible to add support for virtually any language capable of network communication.

### Performance Improvements

Ongoing optimization efforts include:
- Template compilation and caching
- Reduced serialization overhead
- Connection pooling improvements
- Parallel rendering capabilities

### Enhanced Security Features

Future versions may include:
- Template signing and verification
- Fine-grained permission controls
- Audit logging
- Content Security Policy integration

### Developer Experience

Improvements to tooling:
- IDE/editor extensions with syntax highlighting
- Template validation tools
- Debugging capabilities
- Performance profiling

### Community Growth

NeutralTS, Template system for the Web backend, language-agnostic via IPC/Package and natively as library/crate in Rust.

The project continues to grow with:
- Expanded documentation
- More examples and tutorials
- Community-contributed snippets and libraries
- Integration guides for popular frameworks

---

## Conclusion

Neutral TS represents a significant evolution in template engine technology. We're developing a new web template engine with a standout feature: it's language-agnostic. This means the same web template will work on any system and with any programming language.

By addressing the fundamental challenge of template portability across programming languages, Neutral TS opens new possibilities for software architecture:

1. **Freedom of Choice**: Choose the best language for each service without template constraints
2. **Reduced Duplication**: Maintain one set of templates instead of multiple language-specific versions
3. **Consistent User Experience**: Guarantee identical output across all services
4. **Enhanced Security**: Benefit from process isolation and Rust's memory safety
5. **Future-Proofing**: Migrate between technologies without rewriting templates

The engine's architecture—built in Rust for performance and safety, accessible via IPC for universal compatibility—strikes an elegant balance between power and practicality. For most web applications, the security and interoperability benefits compensate for the performance overhead.

Whether you're building a monolithic application in Rust or orchestrating a polyglot microservices architecture, Neutral TS provides a solid foundation for template management. Its BIF-based syntax, while requiring some initial learning, offers flexibility and power that simpler template engines cannot match.

As web development continues to embrace diverse technology stacks and architectural patterns, tools like Neutral TS that bridge language boundaries will become increasingly valuable. The ability to share not just data and APIs, but also presentation logic, represents a meaningful step toward truly language-agnostic software development.

For developers and organizations looking to streamline their template management, reduce duplication, and embrace polyglot architectures without sacrificing consistency, Neutral TS offers a compelling solution backed by modern engineering principles and an active community.

---

## Resources and References

### Official Resources

- **GitHub Repository**: [FranBarInstance/neutralts](https://github.com/FranBarInstance/neutralts)
- **Rust Crate**: [neutralts on crates.io](https://crates.io/crates/neutralts)
- **Python Package**: [neutraltemplate on PyPI](https://pypi.org/project/neutraltemplate/)
- **Documentation**: [Neutral TS docs](https://franbarinstance.github.io/neutralts-docs/docs/neutralts/doc/)
- **IPC Server**: [neutral-ipc](https://github.com/FranBarInstance/neutral-ipc)
- **IPC Clients**: [neutral-ipc clients](https://github.com/FranBarInstance/neutral-ipc/tree/master/clients)
- **Examples**: [Examples (neutralts-docs)](https://github.com/FranBarInstance/neutralts-docs/tree/master/examples)

### License

Neutral TS is released under the Apache License 2.0, allowing both personal and commercial use with proper attribution.

---

*This comprehensive guide provides a foundation for understanding and using Neutral TS. As the project evolves, consult the official documentation for the latest features and best practices.*
