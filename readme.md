# SleepShift

> aka. 28-hour days with world clock

Originally created to display the hours of a 28-hour day weekly
schedule, you can fiddle with the hours in SleepShift to display
various sleep schedules that fit evenly within a normal week.

It also displays a world clock. If you host it from a web server,
it will show sunrise and sunset.

![picture of the sleepshift calendar](sleepshift.png)

The settings to display what's in the picture are in `index.html`.

## Usage

If you want to display the default 28-hour day with no extras, init
with your time zone and run the `drawMyCal()` function.

    $(document).ready(function(){

      SleepShift.init({mytimezonename: "Pacific"});
      SleepShift.drawMyCal();

    });

### Customizing the calendar to your sleep schedule

- You can provide arguments to `SleepShift.drawMyCal()` to draw your own
  sleep schedule.

    SleepShift.drawMyCal(totalhours, wakehours, offset)

  - `totalhours`: The total hours in _your_ day. Not necessarily 24.
    Reasonable day lengths that fit evenly in a normal 168 hour week are:
    12, 14, 21, 24, and 28.

  - `wakehours`: Number of hours in _your_ day that you want to be awake.

  - `offset`: Adjust -n/n to the hour -Sun or +Mon that you want your
    week to start. Examples:

    - To start your week at midnight Monday, use 0.
    - To start your week at 8 a.m. on Monday, use 8.
    - To start your week at 7 p.m. on Sunday, use -5.

  A normal person's week ;-)

      SleepShift.drawMyCal(24, 16, 7);

- With a different sleep schedule, you'll want to give your calendar a
  different title.

      SleepShift.init({
        mytimezonename: "Pacific",
        title: "My normal week"
      });

- The default with no arguments is the same as `SleepShift.drawMyCal(28, 20, -6)`.

### Adding time zones

Add [time zone names and offsets][tz] to the `tzhash` init property.

    SleepShift.init({
      mytimezonename: "Pacific",
      tzhash: {
        "Mountain":     -7,
        "Eastern":      -5,
        "+00:30 India":  5,
      }
    });

**Note:** There's no daylight savings feature yet. When the time comes, you
gotta change affected values (along with all the clocks in your house). :O)

### Adding other _non-sleep_ events

To add other events (work hours, etc.), use the `cellstyles` init property.
For each event you want to add to the table, provide its name, its HTML
"#" color value (either 3 or 6 hex digits), and the cell numbers to apply
the event to. For the name, separate words with hyphens. In the color key,
hyphens become spaces and the words are init-capped.

Format of each entry - "name": ["color", [list of cells]]

Example:

    SleepShift.init({
      mytimezonename: "Pacific",
      cellstyles: {
          "workout": ["6af",[37,91,149]],
          "my-work": ["6fd",[0,164,165,166,167]]
      }
    });

"But wait, how do I know what the cell numbers are?" Good question. To see
the cell numbers, turn on debug.

    SleepShift.debug = true;

### Other things you can change

You can change the sleep color if you don't like purple.

    SleepShift.init({mytimezonename: "Pacific", sleepcolor: "777"});




[tz]: https://en.wikipedia.org/wiki/List_of_UTC_time_offsets
