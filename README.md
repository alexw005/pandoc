# Pandoc Conversion with Docker Compose

This project provides a Docker Compose setup to convert a Markdown file to various formats using [Pandoc](https://pandoc.org/), a universal document converter. With the included `docker-compose.yml`, you can easily convert files like `README.md` to formats such as `.epub` without needing a local Pandoc installation.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

1. Clone this repository or create a `docker-compose.yml` file using the contents below:

   ```yaml
   version: '3.8'

   services:
     pandoc:
       image: pandoc/core
       volumes:
         - .:/data
       user: "${UID}:${GID}"  # Runs the container with your user permissions
       working_dir: /data
       command: README.md -o outfile.epub
   ```

2. Place the Markdown file you want to convert (`README.md` by default) in the same directory as the `docker-compose.yml`.

## Usage

To convert `README.md` to `outfile.epub`, run:

```bash
docker-compose run --rm pandoc
```

This command will:

- Launch the Pandoc container.
- Mount the current directory to `/data` inside the container.
- Convert `README.md` to `outfile.epub` in the same directory.

### Customizing the Command

To convert other files or change the output format, modify the `command` in `docker-compose.yml`:

```yaml
command: YOUR_FILE.md -o OUTPUT_FILE.pdf
```

### Example Commands

Convert `README.md` to PDF:

```bash
docker-compose run --rm pandoc README.md -o outfile.pdf
```

Convert `README.md` to DOCX (Word document):

```bash
docker-compose run --rm pandoc README.md -o outfile.docx
```

## Notes

- **Permissions**: The container runs with the current user’s UID and GID to avoid permission issues on the generated files.
- **Output**: The converted file will appear in the same directory as `README.md` and `docker-compose.yml`.

## Troubleshooting

If you encounter permission issues, check that Docker has permissions to access your project directory and that UID and GID are set correctly.

## Resources

- [Pandoc Documentation](https://pandoc.org/MANUAL.html)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---

This README provides an overview of setting up and using the Docker Compose configuration to convert Markdown files with Pandoc. Adjust any examples to suit your specific use case or project requirements.