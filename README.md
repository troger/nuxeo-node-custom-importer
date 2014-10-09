# nuxeo-node-custom-importer

This is a fork of [nuxeo-node-importer](https://github.com/troger/nuxeo-node-importer) to show how to customize it to import a custom hierarchy.

We will create documents on the Nuxeo Platform instance according to the filenames of the hierarchy.

Full filename format is:

    Type_source_lifecycestate_dc:valid_dc:creator_filename.doc

The importer can also handle simpler filename format:

    Type_filename.doc

or only:

    filename.doc

If you want to ignore some parts, juste remove it, keeping all the `_`, such as:

    Type__lifecyclestate_dc:valid_dc:creator_filename.doc

With this one, the `dc:source` will be kept empty.

    Type____dc:creator_filename.doc

With this one, only the `dc:creator` property will be field.


Here are some rules the importer will follow:

- If the `Type` is `Note`, instead of uploading the file, we will set the `note:note` field.
- if no `Type` are specified for a directory, we will create a `Folder`.
- if no `Type` are specified for a file, we will create a `File`.


## Installation

    $ npm install -g troger/nuxeo-node-custom-importer

This module is not yet published on npm.

## Usage

    $ nuxeo-importer [options] local-path remote-path

Recursively import the files and directories of `local-path` to the `remote-path` on a Nuxeo Platform instance.

Options are:

- `--baseURL`: the base URL of the Nuxeo Platform instance
- `--username`: the username to use to connect to the server
- `--password`: the password to use to connect to the server
- `--verbose`: verbose output

## Sample

A sample directory / file structure can be found in the `sample_files` folder.

To import it in a Nuxeo Platform instance running on `localhost` (in an existing `ws` Workspace):

    $ nuxeo-importer sample_files /default-domain/workspaces/ws