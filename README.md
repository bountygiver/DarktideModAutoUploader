### Github Action to automatically pack a darktide mod and publish to nexus mods.

Your mod files must be in the root of your repository, the name of the nesting folder and the zip file will be based on the file name of your `.mod` file.

## Inputs
| **Name** | **Type** | **Required?** | **Details** |
|---|---|---|---|
| file_id | string | true | ID for the file group. [How to find it here](https://github.com/Nexus-Mods/upload-action/tree/v1.0.0-beta.8#how-to-find-the-file-id) |
| mod_version | string | false | The version name to be used when the mod is uploaded. |
| mod_description | string | false | The changelog to be used when the mod is uploaded. |
| checkout_ref | string | true | Checkout reference, can be tag name or commit hash. |                                       |

Secrets for `NEXUSMODS_APIKEY` may be acquired according to instructions [here](https://www.nexusmods.com/settings/api-keys)

## Example
This will automatically publish your mod with version name equal to your release name and changelog equal to your release body.
```
name: upload-nexus-mods

on:
  release:
    types: [ "published" ]


jobs:
  fetch-upload:
    uses: bountygiver/DarktideModAutoUploader/.github/workflows/pack_mod.yml@v3
    with:
      file_id: <replace with your file hroup id>
      mod_version: ${{ github.event.release.name }}
      mod_description: ${{ github.event.release.body }}
      checkout_ref: ${{ github.event.release.tag_name }}
    secrets:
      NEXUSMODS_APIKEY: ${{ secrets.NEXUSMODS_APIKEY }}
```
