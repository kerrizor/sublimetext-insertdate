InsertDate
==========

A plugin for Sublime Text 2 that inserts the current date and/or hour according to the specified
format and supports named timezones (as well as the locale's timezone settings if necessary).


Key Bindings (and Examples)
---------------------------

Browse "Preferences > Package Settings > Insert Date > Key Bindings - Default" for an overview of the default key bindings which are creat examples for usage.


Settings
--------

Browse "Preferences > Package Settings > Insert Date > Settings - Default" for an overview of available settings.


Format Examples
---------------

Python docs: 7.1.8. strftime() and strptime() Behavior:
    http://docs.python.org/py3k/library/datetime.html#strftime-strptime-behavior

Here are some examples on how the values are interpreted.

| Format string            | Parameters                       | Resulting string                   |
|:-------------------------|:---------------------------------|:-----------------------------------|
| `%d/%m/%Y %I:%M %p`      |                                  | 13/05/2012 03:45                   |
| `%d. %b %y`              |                                  | 13. Mai 12                         |
| `%H:%M:%S.%f%z`          |                                  | 15:45:26.598000+0200               |
| `%Y-%m-%dT%H:%M:%S.%f%z` |                                  | 2012-05-13T15:45:26.598000+0200    |
| `iso`                    | `{'tz_out': 'UTC'}`              | 2012-05-13T13:45:26.598000+00:00   |
| `%x %X UTC%z`            | `{'tz_in': 'local'}`             | 13.05.2012 15:45:26 UTC+0200       |
| `%X %Z`                  | `{'tz_in': 'Europe/Berlin'}`     | 15:45:26 CEST                      |
| `%d/%m/%Y %I:%M %Z`      | `{'tz_in': 'America/St_Johns'}`  | 13/05/2012 03:45 NDT               |
| `%x %X %Z (UTC%z)`       | `{'tz_out': 'EST'}`              | 13.05.2012 08:45:26 EST (UTC-0500) |
| `%x %X %Z (UTC%z)`       | `{'tz_out': 'America/New_York'}` | 13.05.2012 09:45:26 EDT (UTC-0400) |

Notes:

- `Europe/Berlin` is my actual timezone.
- `%x` and `%X` are representative for *Locale’s appropriate time representation*.
- `%p` also corresponds to the locale's setting, thus using `%p` e.g. on a German system gives an empty string.


Command Reference
-----------------

**insert_date**

Parameters:

- format (str) - Default: `'%x %X'`

  A format string which is used to display the current time. See below for more information.

- prompt (bool) - Default: `False`

  If `True` a small popup window will be displayed where you can specify the format string manually.
  The string passed in `format` will be used as default text if available.

- tz_in (str) - Default: `'local'`

  Defines in which timezone the current time (read from your system) will be interpreted.
  Required if you want %Z (your timezone's name). May be one of the following values or `'local'`:
  https://github.com/FichteFoll/sublimetext-insertdate/blob/c879a70e12fb38c86a893b2be7979b4f7111b342/pytz/__init__.py#L527-L1101

- tz_out (str) - Default: `None`

  Defines on which timezone the output time should be based.
  Supports the same values as tz_in ('local' does not support %Z yet).
