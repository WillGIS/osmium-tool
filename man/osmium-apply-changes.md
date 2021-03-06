
# NAME

osmium-apply-changes - apply OSM change file(s) to OSM data file


# SYNOPSIS

**osmium apply-changes** \[*OPTIONS*\] *OSM-DATA-FILE* *OSM-CHANGE-FILE*...
**osmium apply-changes** \[*OPTIONS*\] *OSM-HISTORY-FILE* *OSM-CHANGE-FILE*...


# DESCRIPTION

Merges the content of all OSM change files and applies those changes to the OSM
data or history file.

Objects in the data or history file must be sorted by type, ID, and version.
Objects in change files need not be sorted, so it doesn't matter in what order
the change files are given or in what order they contain the data.

Changes can be applied to normal OSM data files or OSM history files with this
command. File formats will be autodetected from the file name suffixes, see
the **--with-history** option if that doesn't work.

This commands reads its input file(s) only once and writes its output file
in one go so it can be streamed, ie. it can read from STDIN and write to
STDOUT.


# OPTIONS

-H, --with-history
:   Update an OSM history file (instead of a normal OSM data file). Both
    input and output must be history files. This option is usually not
    necessary, because history files will be detected from their file name
    suffixes, but if this detection doesn't work, you can force this mode
    with this option. Can not be used together with the **--locations-on-ways**
    option.

--locations-on-ways
:   Input has and output should have node locations on ways. Can be used
    to update files created by the **osmium-add-locations-to-ways**. See
    there for details on the format. Can not be used together with the
    **--with-history**,**-H** option.

-r, --remove-deleted
:   Deprecated. Remove deleted objects from the output. This is now the
    default if your input file is a normal OSM data file ('.osm').

-s, --simplify
:   Deprecated. Only write the last version of any object to the output.
    This is now the default if your input file is a normal OSM data file
    ('.osm').


@MAN_COMMON_OPTIONS@
# INPUT OPTIONS

-F, --input-format=FORMAT
:   The format of the OSM-DATA-FILE or OSM-HISTORY-FILE. Can be used to set
    the input format if it can't be autodetected from the file name.
    See **osmium-file-formats**(5) or the libosmium manual for details.

--change-file-format=FORMAT
:   The format of the OSM-CHANGE-FILE(s). Can be used to set the input format
    if it can't be autodetected from the file name(s). This will set the format
    for all change files, there is no way to set the format for some change
    files only. See **osmium-file-formats**(5) or the libosmium manual for
    details.


@MAN_OUTPUT_OPTIONS@

# DIAGNOSTICS

**osmium apply-changes** exits with exit code

0
  ~ if everything went alright,

1
  ~ if there was an error processing the data, or

2
  ~ if there was a problem with the command line arguments.


# MEMORY USAGE

**osmium apply-changes** keeps the contents of all the change files in main
memory. This will take roughly 10 times as much memory as the files take on
disk in *.osm.bz2* format.


# EXAMPLES

Apply changes in `362.osc.gz` to planet file and write result to `new.osm.pbf`:

    osmium apply-changes --output=new.osm.pbf planet.osm.pbf 362.osc.gz


# SEE ALSO

* **osmium**(1), **osmium-file-formats**(5), **osmium-merge-changes**(1), **osmium-derive-changes**(1)
* [Osmium website](http://osmcode.org/osmium-tool/)

