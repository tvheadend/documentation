---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Date/Time Format

The date and time are shown in many places within the Web User Interface.  In most places, the format used is based on the default setting of your Browser and Operating System.

If, for example, the date/time format in your 'Upcoming Recordings' looks something like, 'Fri, 02/08/2024 14:05:00' and you wish to shorten it to something like 'Fri, 02-Aug 14:05', you can do the following:

In the WebUI, navigate to Configuration -> General -> Base.

Ensure that your 'Default view level' is set to at least 'Advanced'.

In the 'Web Interface Settings' panel, the 'Custom date Format' field can be used to override the default date/time format by adding '%ddd, %dd-%MMM %hh:%mm'.

Reload your bowser window for this change to be applied.

The following is a list of available formatting code options:

<table><thead><tr><th width="156">Format Code</th><th>Description</th></tr></thead><tbody><tr><td>%d</td><td>Day without zero padding. eg: 1 or 31</td></tr><tr><td>%dd</td><td>Day with zero padding. eg: 01 or 31</td></tr><tr><td>%ddd </td><td>Language-specific abbreviated day name. eg: 'Wed' or 'Mi'.</td></tr><tr><td>%dddd</td><td>Language-specific full day name. eg: 'Wednesday' or 'Mittwoch'.</td></tr><tr><td>%m</td><td>Month without zero padding. eg: 1 or 12</td></tr><tr><td>%mm</td><td>Month with zero padding. eg: 01 or 12</td></tr><tr><td>%mmm</td><td>Language-specific abbreviated month name. eg: 'Dec' or 'déc.'.</td></tr><tr><td>%mmmm</td><td>Language-specific full month name. eg: 'December' or 'décembre'.</td></tr><tr><td>%yy</td><td>Two-digit year without the century. eg: 02 or 97.</td></tr><tr><td>%yyyy</td><td>Four-digit year with the century. eg: 2002 or 1997</td></tr><tr><td>%h</td><td>Hour without zero padding,  eg: 1 or 23.  (Always 24 hour clock)</td></tr><tr><td>%hh</td><td>Hour without zero padding, 12 hour clock. eg: 01 or 23.  (Always 24 hour clock)</td></tr><tr><td>%m</td><td>Minute without zero padding. eg: 1 or 59.</td></tr><tr><td>%mm </td><td>Minute with zero padding. eg: 01 or 59.</td></tr><tr><td>%s</td><td>Seconds without zero padding. eg: 1 or 59.</td></tr><tr><td>%ss</td><td>Seconds with zero padding. eg: 01 or 59.</td></tr></tbody></table>
