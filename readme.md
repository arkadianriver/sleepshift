# SleepShift

> Display a week of 21, 24, or 28-hour days (with a world clock)

Originally created to display the hours of a 28-hour day weekly
schedule, you can fiddle with the hours in SleepShift to display
various sleep schedules that fit evenly within a normal week.

It also displays a world clock. And, if you host it from a web server,
it will show sunrise and sunset.

![picture of the sleepshift calendar](sleepshift.png)

The settings to display what's in the picture are in `index.html`.

## Usage

If you want to display the default 28-hour day with no extras, init
with your time zone and run the `drawMyCal()` function.

```javascript
$(document).ready(function(){

  SleepShift.init({mytimezonename: "Pacific"});
  SleepShift.drawMyCal();

});
```

### Customizing the calendar to your sleep schedule

You can provide arguments to `SleepShift.drawMyCal()` to draw your own
sleep schedule.

```javascript
SleepShift.drawMyCal(totalhours, wakehours, offset)
```

<dl>
  <dt>totalhours</dt>
  <dd>The total hours in <i>your</i> day. Not necessarily 24.
  Reasonable day lengths that fit evenly in a normal 168 hour week are:
  12, 14, 21, 24, and 28.</dd>
  
  <dt>wakehours</dt>
  <dd>Number of hours in <i>your</i> day that you want to be awake.</dd>

  <dt>offset</dt>
  <dd>Adjust -n/n to the hour -Sun or +Mon that you want your
  week to start. Examples:
  <ul><li>To start your week at midnight Monday, use 0.</li>
      <li>To start your week at 8 a.m. on Monday, use 8.</li>
      <li>To start your week at 7 p.m. on Sunday, use -5.</li>
  </ul></dd>
</dl>

A normal person's week ;-)

```javascript
SleepShift.drawMyCal(24, 16, 7);
```

With a different sleep schedule, you'll want to give your calendar a
different title.

```javascript
SleepShift.init({
  mytimezonename: "Pacific",
  title: "My normal week"
});
```

The default with no arguments is the same as `SleepShift.drawMyCal(28, 20, -6)`.

### Displaying time zones

Add [time zone names and offsets][tz] to the `tzhash` init property.

```javascript
SleepShift.init({
  mytimezonename: "Pacific",
  tzhash: {
    "Mountain":     -7,
    "Eastern":      -5,
    "+00:30 India":  5,
  }
});
```

**Note:** There's no daylight savings feature yet. When the time comes, you
gotta change affected values (along with all the clocks in your house). :O)

### Displaying other _non-sleep_ events

Use the `cellstyles` init property to add other events (work hours, etc.).
For each event you want to add to the table, provide its name, its HTML
"#" color value (either 3 or 6 hex digits), and the cell numbers to apply
the event to. For the name, separate words with hyphens. In the color key
that's displayed below the table, hyphens become spaces and the words are
init-capped.

Format of each entry: `"name": ["color", [list of cells]]`

Example:

```javascript
SleepShift.init({
  mytimezonename: "Pacific",
  cellstyles: {
    "workout": ["6af",[37,91,149]],
    "my-work": ["6fd",[0,164,165,166,167]]
  }
});
```

"But wait, how do I know what the cell numbers are?" Good question. To see
the cell numbers, turn on debug.

```javascript
SleepShift.debug = true;
```

### Other things you can change

You can change the sleep color if you don't like purple.

```javascript
SleepShift.init({mytimezonename: "Pacific", sleepcolor: "777"});
```

## License

[The MIT License (MIT)][lic]


[tz]: https://en.wikipedia.org/wiki/List_of_UTC_time_offsets
[lic]: LICENSE
