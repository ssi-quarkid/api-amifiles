# File Management API for Azure Blob Storage

This project provides an API for uploading and downloading files to Azure Blob Storage with support for single-use tokens and automatic file deletion.

## Requirements

- Docker
- Docker Compose

## Configuration

Ensure the following environment variables are correctly defined in your `docker-compose.yml`:

- `ACCOUNT_NAME`: The name of your Azure storage account.
- `ACCOUNT_KEY`: The access key for your Azure storage account.
- `BLOB_SERVICE_URL`: The URL of the blob service for your Azure storage account.
- `API_SERVICE_URL`: The URL of the API service.

## Usage

## Endpoints

### Upload a file

URL: /upload
Method: POST
Description: Uploads a file to Azure Blob Storage and returns a download URL with a single-use token.

Request example:

```sh
curl -X POST "{API_SERVICE_URL}/upload" -H "accept: application/json" -H "Content-Type: multipart/form-data" -F "file=@path/to/file"
```

Response:

```sh
{
  "message": "File file.pdf successfully uploaded with unique name <unique_id>.pdf.",
  "download_url": "{API_SERVICE_URL}/download/ami/<unique_id>.pdf?token=<token_id>"
}
```

### Download a file

URL: /download/{container_name}/{blob_name}?token={token}
Method: GET
Description: Downloads a file from Azure Blob Storage using a single-use token. The file is deleted after download.

Request example:

```sh
curl -o "{API_SERVICE_URL}/download/ami/<unique_id>.pdf?token=<token_id>"
```
