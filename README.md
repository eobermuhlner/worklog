# worklog
Timetracking command line tool

# Help

```
NAME
    worklog : keep a worklog and analyze it.


SYNOPSIS
    worklog -help
         Prints this help text.

    worklog [options] category [project [task [...]]]
         Adds a new entry using the current date-time to the worklogfile.

    worklog [options] off [project [task [...]]]
         Adds a special 'off' entry to the worklogfile.

    worklog [options]
         Prints worklogfile entries of the selected date-range.

    worklog [options] -statistics
         Prints a statistical analysis of the
         categories/projects/tasks of the selected date-range.

    worklog [options] -check
         Checks the selected date-range for wrong or improbable entries.

    worklog [options] -categories
         Prints sorted categories of the selected date-range.

    worklog [options] -projects
         Prints sorted projects of the selected date-range.

    worklog [options] -tasks
         Prints sorted projects of the selected date-range.


DESCRIPTION
    worklog creates timestamped entries in a worklogfile and
    gives the possibility to analyze the worklogfile.
    The goal is to provide a timereporting tool that is very simple to use
    but still powerful enough to satisfy most needs.


OPTIONS
    -help       Prints this help information.
    -?
    -h

    -version    Print version of worklog.

    -f file     Set the worklog file to a specific file.
                Default is \'/c/Users/EricObermuhlner/.worklog\'.

    -check      Check for improbable entries in the selected date-range.
    -c          Currently this option prints messages for syntax errors,
                missing categories and projects and unreasonably long
                timeslices (over  hours).

    -year num   Set the year of the selected date-range for further processing.
    -y num      The format is "yyyy".
                Example: -y 1997

    -month num  Set the month of the selected date-range for further processing.
    -m num      The format is "mm".
                Example: -m 02

    -day num    Set the day of the selected date-range for further processing.
    -d num      The format is "dd".
                Example: -d 24
                The componenents for the date need to be give in the
                order 'year', 'month', 'day'.
                Default is the current date.

    -all        Set the selected date-range to all valid entries in the
    -a          worklogfile.

    -statistics Print the complete analysis over categories/projects/tasks
    -s          over the selected date-range.

    -categories Print the categories (field 1) of the selected date-range.
                The output is sorted alphabetically.
                This is useful to check for consistent naming.

    -projects   Print the projects (field 2) of the selected date-range.
                The output is sorted alphabetically.
                This is useful to check for consistent naming.

    -tasks      Print the tasks (field 3) of the selected date-range.
                The output is sorted alphabetically.
                This is useful to check for consistent naming.

    -entries    Print the entries (field 1,2,3) of the selected date-range.
                The output is sorted alphabetically.
                This is useful to check for consistent naming.

    -timeslices Prints the entries in the selected date-range in a form
    -t          that is easier to process by other tools.
                Each line contains start and end time, the duration
                            (in seconds) and all fields.
                This is the same format that is also used internally
                by worklog for analysis and checking.

    -notpresent Only the time not present is processed.
                The category 'off' is reserved to mark non-presence.
                This option only affect timeslices output or
                any option that processes timeslices (-analyze, -check).


USAGE
    Most of the time you will call worklog in its simples form;
    no options, just arguments:
    $ worklog category [project [task [...]]]

    This creates a timestamped entry in your
    default worklogfile /c/Users/EricObermuhlner/.worklog
    Do this whenever you start a new task.

    There is a special category 'off' used to start the not-present time
    (like lunch, unpaid breaks or when your going home)

    $ worklog off [project [task [...]]]

    To have a look at the entries of today just type:
    $ worklog

    If want to see the entries of another date-range than today use:
    $ worklog [-year num] [-month num] [-day num]

    Note: The date-range options have to be in this order (ymd).

    The selected date-range effects not only the entry-output described above,
    but all outputs of worklog.

    To simplify processing the entries worklog uses an internal format
    called timeslices. You can view the timeslices with:
    $ worklog [date_range_options] -timeslices

    The timeslices option shows start- and end-time of every timeslice
    and the duration in seconds.
    There are two options available for further processing of the timeslices.
    Note: worklog implicitely appends an entry with the current time and
    the category 'now'. This is necessary to get a timeslice for the time
    between the last entry and now.
    This behaviour is very useful in most cases but might give strange results
    in a few special cases.

    To do a simple plausability check over the entries use:
    $ worklog [date_range_options] -check

    To print a statistical analysis of the timeslices use:
    $ worklog [date_range_options] -statistics

    The statistics option prints different sums over date, categories,
    projects, tasks and some useful combinations (categories/projects
    and projects/tasks) as well as a grand total.
    The sums are given in hours and minutes.

    All this timeslice commands process the present-time (when you are working
    and hopefully paid).
    To process the not-present-time use:
    $ worklog [date_range_options] -notpresent timeslice_option

    Last but not least you can always edit your worklogfile by hand and do only
    the analysis with worklog.
    Manual editing is also useful to correct, insert or move entries,
    because worklog does not provide any features to do this.
    worklog always appends new entries at the end of the worklogfile.


EXIT CODES
    0   if successfully terminated.
    1   if -check option found improbable entries
    2   if corrupt entries prevented successful processing
    255 if illegal commandline arguments where given.


EXAMPLES
    $ worklog hello
        Adds a new entry to the default worklogfile
        which is /c/Users/EricObermuhlner/.worklog
        The category is 'hello' all other fields are empty.
        If the file does not yet exist it is created.

    $ worklog test worklog "testing examples in help"
        Adds a new entry.
        The category is 'test', the project is 'worklog',
        the description is all other fields.

    $ worklog off lunch
        Marks non-presence. The time from now on until the next entry
        is not processed by the statistical analysis.

    $ worklog
        Prints the entries of today.

    $ worklog -categories
        Prints a sorted list of all categories used today.

    $ worklog -projects
        Prints a sorted list of all projects worked on today.

    $ worklog -tasks
        Prints a sorted list of all tasks worked on today.

    $ worklog -entries
        Prints a sorted list of all entries worked on today.

    $ worklog -statistics
        Prints a statistical analysis of today.

    $ worklog -statistics -m 02
        Prints a statistical analysis of february this year.

    $ worklog -statistics -y 1998
        Prints a statistical analysis of the year 1998.

    $ worklog -statistics -y 1998 -m 02 -d 24
        Prints a statistical analysis of the february 24,1998.

    $ worklog -statistics -notpresent -m 02
        Prints a statistical analysis of the non-present time of february.

    $ worklog -statistics -all
        Prints a statistical analysis of all entries in the worklogfile.


KNOWN BUGS
    - 1998/03/06
      Error message are printed over stdout instead of stderr.


COPYRIGHT
    (c) 1998 by Eric Obermuhlner

    Special thanks to Thomas Kofler who teached me shell-scripting by
    providing very professionally written scripts as examples and answering
    hundreds of beginners questions.
```
