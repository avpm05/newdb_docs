# Directory Overview

This directory contains the source code for the NEWDB API documentation website. It is built using [MkDocs](https://www.mkdocs.org/), a static site generator, and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

The documentation provides information on the REST API, including endpoints for various checks like FSSP, FNS, and MVD passport validation.

## Key Files

*   `mkdocs.yml`: The main MkDocs configuration file. It defines the site structure (`nav`), theme, plugins, and other settings.
*   `docs/`: This directory contains all the documentation content in Markdown format. `index.md` is the homepage, and the `fiz/` subdirectory holds the detailed API endpoint documentation.
*   `requirements.txt`: This file lists the Python packages required to build and serve the documentation locally.

## Usage

### Prerequisites

You need Python and `pip` installed.

### Installation

To install the necessary dependencies, run the following command in your terminal:

```bash
pip install -r requirements.txt
```

### Local Development

To start a live-reloading development server, run:

```bash
mkdocs serve
```

You can then view the documentation in your browser at `http://127.0.0.1:8000`. The server will automatically rebuild the site when you save changes to the documentation files.

### Building the Site

To build the static HTML site for deployment, run:

```bash
mkdocs build
```

The static files will be generated in the `site` directory (which is not present in the initial file listing as it's a build artifact).
