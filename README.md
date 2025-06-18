# Puch AI MCP Server for Resume Submission

This project implements a Multi-Channel Protocol (MCP) server designed to interact with the Puch AI platform. The primary goal was to create a server that could serve a resume and handle a validation request from Puch AI, facilitating an automated application process.

## Original Task

The main objective was to build an MCP server that could:
1.  **Serve a resume**: Provide the user's resume in Markdown format when requested by Puch AI.
2.  **Validate connection**: Respond to a validation call from Puch AI by returning a specific piece of information (initially a phone number).

This involved setting up a local server, exposing it to the internet, and configuring it to communicate correctly with the Puch AI system.

## Technologies Used

*   **Python**: Core programming language.
*   **FastAPI**: Modern, fast (high-performance) web framework for building APIs.
*   **FastMCP**: Library for building MCP-compliant servers.
*   **Uvicorn**: ASGI server for running FastAPI applications.
*   **Ngrok**: Tool to expose local servers to the internet via secure tunnels.

## Server Setup and Running

1.  **Prerequisites**:
    *   Python 3.x
    *   Pip (Python package installer)
    *   Ngrok account and CLI installed.

2.  **Installation**:
    *   Clone the repository (if applicable) or ensure `mcp_server.py` and `resume.md` are in the same directory.
    *   Install dependencies from `requirements.txt`:
        ```bash
        pip install -r requirements.txt
        ```

3.  **Configuration**:
    *   The server token is hardcoded in `mcp_server.py` (`TOKEN = "d784c2954f43"`).
    *   The resume content is read from `resume.md`.

4.  **Running the Server**:
    *   Start the Uvicorn server:
        ```bash
        uvicorn mcp_server:http_app --reload --port 8000
        ```

5.  **Exposing with Ngrok**:
    *   In a new terminal, run Ngrok to forward to port 8000:
        ```bash
        ngrok http 8000
        ```
    *   Note the forwarding URL provided by Ngrok (e.g., `https://xxxx-xxxx.ngrok-free.app`).

6.  **Connecting Puch AI**:
    *   Within the Puch AI application, use the `/mcp connect` command with the Ngrok URL (appending `/mcp`) and the server token:
        ```
        /mcp connect YOUR_NGROK_URL/mcp d784c2954f43
        ```

## Key Features Implemented

*   **`resume` tool**: An MCP tool that reads `resume.md` and returns its content.
*   **`validate` tool**: An MCP tool that (initially) returned a phone number for validation. This was later modified as personal information was removed.
*   **Authentication**: A simple bearer token authentication was implemented.

## Modifications Made (for privacy/sharing)

To prepare this project for sharing or as a template, the following modifications were made to the original files:

*   **In `resume.md`**:
    *   Phone number was removed.
    *   Email address was changed to a generic one (`rishabhgusain.6@gmail.com`).
    *   The entire "EDUCATION" section was removed.
*   **In `mcp_server.py`**:
    *   The `MY_NUMBER` constant (which held the phone number) was commented out.
    *   The `validate` tool's dependency on `MY_NUMBER` means its behavior for actual validation would need to be reconsidered if this specific validation is still required by Puch AI without a phone number.

This README provides an overview of the project's purpose, setup, and the journey to successfully connect it with Puch AI.