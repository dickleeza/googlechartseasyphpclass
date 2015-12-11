A quick PHP class for creating Google Charts.

UPDATE: version 1.02 is available.
[Download](http://googlechartseasyphpclass.googlecode.com/files/googlecharts_1.02.php) v1.02.

Changes in 1.02
  * Charts now work with BBCode
  * Can now specify chart bar widths
  * showGrid auto calculation fixed
  * Added negativeMode for negative number datasets


You don't need anything besides this one class file because it creates urls to use google charts. For more complex charts look at the Wiki documentation for this project, if you still want more complex charts then you're free to modify this code.

Here is an example of a usage for a basic chart with 12 points of data:
```
<?php
include ('googlecharts.php');

$chart=new googleChart('4,6,21,7,1,6,17,5,2,1,7,9');
$chart->draw();
?>
```
![http://chart.apis.google.com/chart?chs=150x67&cht=lc&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=lc&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg)
This is it live.

Here is another one just for the fun of it:

![http://chart.apis.google.com/chart?chs=300x125&cht=p&chtt=foods&chl=cake|pie|muffins|cookies|icecream&chco=0088ff,8800ff,4444ff&chd=t:50,12.5,75,100,12.5&chxr.jpg](http://chart.apis.google.com/chart?chs=300x125&cht=p&chtt=foods&chl=cake|pie|muffins|cookies|icecream&chco=0088ff,8800ff,4444ff&chd=t:50,12.5,75,100,12.5&chxr.jpg)

You can also make more advanced charts,
Read the documentation (also including in the .php file) to see examples on customize your chart.