# v9000

An [AIP](http://www.araport.org) Science App created using [Yeoman](http://yeoman.io)
and the [AIP science app generator](https://www.npmjs.org/package/generator-aip-science-app).

## App Code

Your application code is in the `app/` subdirectory:

```
.
+-- app/
|   +-- app.html
|   +-- scripts/
|       +-- app.js
|   +-- styles/
|       +-- app.css

```

## Development

You can interactively develop your app using the built-in test runner. Simply
execute this command from within the base directory of your app:

```bash
$ grunt
```

This will run your application on a local server at
[http://localhost:9000](http://localhost:9000). It will also watch your
app code for changes and automatically reload the browser when it detects
changes.

You can also run the test runner app in "production" mode with the command:

```bash
$ grunt serve:dist
```

This will start the same server, but without source code monitoring (live reload)
and will also permit connections from outside, for example if you wanted to host
the app yourself on a publicly accessible server.

## Deployment

When you are ready you can upload your application to the
[AIP Science Apps Workspace](http://www.araport.org/apps).

** More details coming soon! **

BLAST notes
===========

- [] Database types are now ```nucl``` or ```prot``` to track directly to NCBI nomenclature
- [] Versioned database indexes are stored as **araport.blastdb.index metadata** records. There are more than one. Grab them all, generate the union set of databases from ```value.docker_this.databases```. Consider cacheing the result of these queries in localStorage to make the app more performant. 
- [] The underlying BLAST app now supports provision of a custom database file ```inputs.customDatabase``` at job submission. User can ALSO specify databases from the list when BLASTing. Support choosing from previous uploads, or uploading a new file, like we do for sPARTA
- [] Display ONLY the database types (nucl or prot) appropriate to the type of BLAST selected. May need a filter on this later but not now
- [] Enable user to display previous BLAST outputs - Use preview modal like in Sparta/miFerno apps or Hanlon's file browser
- [] For each blast type, remember the selected databases between sessions. Add button to clear all/check all. 
- [] Support NAMING the job at submit time
- [] BLAST is consolidated to a single Agave app now. The specific program to run is distinguished by ```parameters.blast_application```
- [] Current production version(s) of ncbi-blast app is stored in **araport.ncbi-blast.applist** metadata. It is a list with at least one value. Grab the list, select one at random. This will allow hot swapping the Agave app without redeploying the UI assets.
- [] Create a standalone My BLASTS app with just the history plus extra sugar (share, download, etc)
- [] In Blast Input Sequence, allow select/upload in addition to paste. On paste, allow naming of file.
- [] Under Advanced Options, reorder params by priority (see below)
- [] Rename Job History to "BLAST History"
- [] Enhance the UX around the progress meter: Either a progress bar thing or at least replace the AGAVE STATUS words with human-comprehensible text (I like the former idea BTW)
- [] On job submit, pop open the History panel to highlight that it exists
- [] Replace BLAST app dropdown with Bootstrap-style radio buttons
- [] Disable the Run BLAST button until at least an input sequence and database have been selected
- [] Make the Run BLAST button more evident, either by placement or appearance

## BLAST app via databases to display

| program | dbtype |
| ---- | --------- |
| blastn | nucl |
| blastp | prot |
| blastx | prot |
| tblastn | nucl |
| tblastx | nucl |

## Advanced Blast Options ordering
* Expectation value (E) threshold for saving hits
* Maximum number of aligned sequences to keep
* Format
* _Others in basically any order you want_

## References
* https://github.com/Arabidopsis-Information-Portal/agave-ncbi-blast
* https://github.com/Arabidopsis-Information-Portal/agave-ncbi-blastdb
* https://hub.docker.com/r/araport/
