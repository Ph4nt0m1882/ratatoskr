# ![ratatoskr](.github/assets/images/ratatoskr.png)

## Ratatoskr - The Local "Omni" AI Orchestrator

Ratatoskr is an advanced Client-Server architecture designed to unify and orchestrate all your Artificial Intelligence models (LLMs, Image Generators, Audio), whether they are hosted in the Cloud (Google AI Studio, Claude API) or running locally (llama.cpp, vLLM).

This main repository acts as a "Superproject" linking the two major components of the architecture via Git Submodules.

### Project Architecture

The project is divided into two distinct modules:

1. **[Ratatoskr Daemon](./ratatoskr_daemon)**: The "Brain". It is a background service written in Python (FastAPI) that manages connections to various APIs, the local database (history, settings), and exposes a unified API. It is designed to run silently on the host machine.
2. **[Ratatoskr Client](./ratatoskr_client)**: The User Interface. A rich graphical application developed in Flutter that connects to the Daemon to provide a unified chat experience, management of AI processes (local/remote RAGs), and a highly customizable administration interface.

### Installation and Development

This project uses a VSCode `workspace` to manage both the client and the server simultaneously.

1. Clone this repository with its submodules:
   ```bash
   git clone --recurse-submodules https://github.com/YOUR_NAME/ratatoskr.git
   ```
2. Open the `ratatoskr.code-workspace` file in VSCode.

*For more information on running and installing each component, please refer to the README of each submodule.*
