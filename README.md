# Rust Slurm MCP

### Model Context Protocol (MCP) Server for Slurm Workload Manager

**Bringing AI-powered interaction to High-Performance Computing (HPC) clusters.**

Rust Slurm MCP is an MCP server developed in Rust that connects AI assistants and intelligent agents to HPC environments managed by [Slurm Workload Manager](https://slurm.schedmd.com/).

Through the Slurm REST API (`slurmrestd`), the project provides a standardized interface for AI applications to interact with cluster information, monitor workloads, and understand computing resources.

The goal is to make HPC infrastructure more accessible through natural language interfaces, enabling AI assistants to retrieve and interpret information about jobs, nodes, partitions, and cluster resources.

---

## 🚀 Overview

Managing HPC environments often requires specialized knowledge of Linux, Slurm commands, scheduling policies, and cluster infrastructure.

Rust Slurm MCP introduces a bridge between traditional HPC administration and AI-powered tools.

By implementing the Model Context Protocol (MCP), the server allows compatible AI applications to communicate with Slurm through structured tools rather than executing shell commands directly on the cluster.

### How it works

```text
+---------------------------+
|       AI Assistant        |
|                           |
|  Claude / MCP Compatible  |
|       Applications        |
+-------------+-------------+
              |
              | MCP Protocol
              |
+-------------v-------------+
|      Rust Slurm MCP       |
|                           |
|     MCP Server (Rust)     |
|                           |
|  +---------------------+  |
|  |    MCP Tools        |  |
|  +---------------------+  |
|  |    Slurm Client     |  |
|  +---------------------+  |
+-------------+-------------+
              |
              | HTTP / REST API
              |
+-------------v-------------+
|       slurmrestd          |
|                           |
|    Slurm REST API         |
+-------------+-------------+
              |
+-------------v-------------+
|       HPC Cluster         |
|                           |
|  +---------+ +---------+  |
|  | Nodes   | | Jobs    |  |
|  +---------+ +---------+  |
|  |Partitions| |Resources| |
|  +---------+ +---------+  |
+---------------------------+
```

---

## ✨ Key Features

- **Written in Rust:** Built with Rust for performance, reliability, and memory safety.
- **Model Context Protocol:** Exposes Slurm functionality through the MCP standard.
- **Slurm REST API Integration:** Communicates with Slurm through `slurmrestd`.
- **Structured Data:** Returns structured information that AI assistants can interpret.
- **HPC Oriented:** Designed specifically for environments running Slurm.
- **Read-oriented Architecture:** Focuses on cluster visibility and monitoring rather than executing administrative operations.

## 🛠️ Planned MCP Tools

The project is being developed around the following capabilities:

| Tool | Description |
|---|---|
| `get_cluster_info` | Retrieve general cluster information. |
| `list_nodes` | List compute nodes. |
| `get_node_status` | Retrieve node status and information. |
| `list_jobs` | Retrieve jobs submitted to Slurm. |
| `get_job_info` | Retrieve detailed information about a specific job. |
| `get_job_history` | Retrieve historical job information. |
| `list_partitions` | List available Slurm partitions. |
| `get_cluster_resources` | Retrieve cluster resource information. |

*Note: The toolset is under active development. Not all capabilities listed above are implemented yet.*

---

## 🧠 Example Use Cases

The project aims to enable interactions such as:

**Job Monitoring**

> Show me all running jobs in the cluster.

> How many jobs are currently pending?

> Show me the details of job 12345.

**Node Monitoring**

> Which compute nodes are currently unavailable?

> Show me the status of all cluster nodes.

**Partition Information**

> What partitions are available in this cluster?

> Which partitions are currently accepting jobs?

**Cluster Resources**

> Give me an overview of the cluster resources.

> How many compute nodes are available?

These examples illustrate the intended interaction model as the corresponding MCP tools become available.

---

## 🔐 Authentication

Rust Slurm MCP integrates with the Slurm REST API authentication mechanism.

Communication with `slurmrestd` uses the Slurm authentication headers:

```http
X-SLURM-USER-NAME: username
X-SLURM-USER-TOKEN: token
```

The Slurm REST API must be configured and accessible to the MCP server.

For production environments, use an appropriately restricted Slurm account and follow your organization's credential-management policies.

---

## 📦 Installation

Rust Slurm MCP is distributed as a precompiled executable binary.

You do not need Rust or Cargo installed to run the server.

Download the appropriate binary for your operating system and architecture from the project's GitHub Releases.

**Available distributions:**

| Platform | Architecture | Status |
|---|---|---|
| Linux | x86_64 | Planned |
| Linux | aarch64 | Planned |

### Download

Visit the latest release:

https://github.com/ptarcode/slurm_mcp/releases

Extract the downloaded archive and make the binary executable:

```bash
chmod +x slurm-mcp
```

## ⚙️ Configuration

The MCP server requires access to a running Slurm REST API (`slurmrestd`).

Configuration is managed through a `.env` file located in the same directory as the executable binary.

### Environment Configuration

Create a `.env` file:

```bash
touch .env
```

Add the following configuration:

```env
SLURM_API_URL=http://localhost:6820
SLURM_USER=your_slurm_user
SLURM_TOKEN=your_slurm_token
```

Replace the example values with your Slurm REST API endpoint and authentication credentials.

**Important:**
- Keep the `.env` file in the same directory as the executable.
- Do not commit your `.env` file to version control.
- Protect your authentication token and restrict access to the configuration file.

*Adjust the configuration variables according to the actual environment variables supported by the application.*

## ▶️ Running

Start the MCP server:

```bash
./slurm-mcp
```

The server communicates with compatible MCP clients using its configured transport.

## 📋 Requirements

- Linux operating system (depending on the released binary).
- Accessible Slurm REST API (`slurmrestd`).
- Valid Slurm authentication credentials.
- Compatible MCP client.

Rust and Cargo are not required on the target machine.

---

## 🎯 Project Vision

The long-term vision is to explore how AI and HPC infrastructure can work together.

Rust Slurm MCP aims to provide an integration layer that allows AI assistants to understand and interact with complex computing environments through standardized interfaces.

Potential applications include:

- AI-assisted HPC cluster monitoring.
- Intelligent workload analysis.
- Natural language interfaces for Slurm.
- Research infrastructure observability.
- Integration with AI agents and automation platforms.

The project is also an exploration of the Rust ecosystem, asynchronous programming, MCP architecture, and modern approaches to HPC infrastructure management.

---

## 🤝 Contributing

Contributions, suggestions, and ideas are welcome!

If you are interested in Rust, MCP, Artificial Intelligence, or High-Performance Computing, feel free to explore the project and contribute.

---

## 📄 License

See the repository for licensing information.
