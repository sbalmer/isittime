Isittime
========

The `isittime` script accepts rules on stdin or passed as filename. See the
examples file to get an idea for the format. The script is intended to be used
as part of a logic chain such as
`echo "mon-thu 19:00-21:00" | isittime && open-lock || close-lock`

I'm using this script to drive a door lock from cron:

```
* * * * * root /usr/bin/isittime /etc/opening-hours && /sbin/open-lock || /sbin/close-lock
```

Make sure system time and timezone are set correctly before relying on this script.


Format
------

`isittime` uses a simple schedule format to specify dates, weekdays and times
of day. Example: `mon-wed 13:00-18:00` matches all days between 13:00 and 18:00
except weekends.

The format allows multiple lines, one rule per line. Every rule can have
multiple patterns specified. Each pattern may be a single time-specifier such
as a date (`2016.09.08`), a weekday (`mon`), or a time (`13:00`). A pattern may
also be a range giving two values such as `2016.09.01-2016.10.31`, `sat-sun`, or
`08:00-13:00`.

For a rule to match, at least one of the patterns of each class must match, if
it is specified. So if dates are specified, at least one of the dates must
match, if weekdays are specfied, one must match, same for daytime. Everything
following the pound sign (#) on a line is ignored. Empty lines are ignored.
Lines that don't follow the format are ignored and a warning is printed to
stderr.


Legalese
--------
Copyright 2016 sbalmer

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.
