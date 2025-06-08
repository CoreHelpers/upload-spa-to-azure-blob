# GitHub Action to Upload SPA Assets to Azure Blob Storage
This action is uploading a SPA to azure blob and activates the entrypoint at last so that zero downtime is possible. It is designed 
to use the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) to upload a directory 
of your choice to your Azure Blob Storage account and upadte the index.html at the last file. This leads to a zero downtime 
option. 

## Usage

### Example

Place in a `.yml` file such as this one in your `.github/workflows` folder. [Refer to the documentation on workflow YAML syntax here.](https://help.github.com/en/articles/workflow-syntax-for-github-actions)

```yaml
name: Upload SPA To Azure Blob Storage
on:
  push:
    branches:
      - main
jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: CoreHelpers/upload-spa-to-azure-blob@main
        with:
          connectionstring: ${{ secrets.ConnectionString }}
          container: publicweb
          source: _dist
```

If you want to synchronize local and remote state (for example, if you are publishing a static website), enable the `sync` flag.

### Required Variables

| Key                 | Value                                                                      |
|---------------------|----------------------------------------------------------------------------|
| `connectionstring`  | The connection string to the storage account                               |
| `container`         | The container name the file should be uploaded to                          |
| `source`            | The name of the directory you want to upload                               |

## License

This project is distributed under the [MIT license](LICENSE).
