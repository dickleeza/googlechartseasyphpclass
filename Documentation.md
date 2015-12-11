# My google charts php class #

## Here are the excerpts from inside the class file ##
> @author Jeck Lamnent

> @version 1.02

> @GNU public dec 2007

> modify it and change it as much as you'd like
I made it quickly for what I needed so its not optimized for a 15,000 charts per second server

### You can skip all the explanations and go to the examples section below ###
Examples after these quick field/function descriptions

The chart is displayed as an image. The style sheet class is class="googleChart"

If your new to using classes then look at the examples section.
For the below "var something;" entries, instance is a references to
the $blah variable in $blah=new googleChart();

Google charts require supplied data to be separated using commas and | pipes so I
keep the commas and pipes in check inside the functions. If things don't work
right then look at the examples so see what to do.

If the supplied data is negative numbers then set negativeMode=true and load the data using ->loadData();.

data/labels can be arrays or strings.
```
var $barWidth=null; 					//sets the width of the bars for vert/horiz bar charts.
	instance->barWidth=10;
var $negativeMode;						//Set to true if data is negative data
	instance->negativeMode=true;
var $dimensions;						//dimensions are width x height
	instance->dimensions='300x100';
var $colors; 							//colors are separated by commas
	instance->colors='8888ff,4444ff'; 	//used to colour charts, can be 1 or many colour sets separated by commas
var $legend; 							//legend items are separated by pipes
	instance->legend='Cows|Dogs|Buffalo';
var $title;								//title is plane text
	instance->title='My chart';
var $fillColor;							//colors don't have # preceeding them
	instance->fillcolor='76A4FB';
var $showGrid;							//if 1 tries to auto calc grid. If > 1 then show this many grid lines
	instance->showGrid=1;
	instance->showGrid=30;
```
f googleChart($data=null,$type=null,$title=null,$dimensions=null);
> -data is an array or a comma separated string.

f setLabels(string or array,string); default 'left'
> -sets labels on the chart, 2nd param is 'top' 'left' 'bottom' or 'right'

f draw(boolean,$append='&chxr.png'); default (true,'&chxr.png')
> -prints an img tag with the chart, if set to false, returns the chart url.
> -The value of $append is append to the chart url. By default it will append &chxr.png so the url is detected as an image

f smartDataLabel($data);
> -Adds a legend and data based on array keys
```
	$data=array(
		'cows'=>array(4,5,6,7,9),
		'dogs'=>array(6,1,4,2,6),
		'peas'=>array(5.4,9,1,6,2)
	);
```
f simpleDataMode()
> -for 0..61 different plottable values. Default options can plot 1000 values
f setLabelsMinMax(integer=3,string='left'); default (3,'left')
> -auto creates labels for you on the left side of chart, goes from 0 to max value
> use setLabels('0|100|200|300|400'); if you want your own number sequences

f setType(string) default ('line')
> -sets the type of chart (pie,pie3d,barx,bary,line)

## EXAMPLES ##
The charts you see are the live results of the below examples. Their sizes are
scaled down though

![http://chart.apis.google.com/chart?chs=150x67&cht=lc&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=lc&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg)
BASIC CHART:
```
	$data=array('4,6,21,7,1,6,17,5,2,1,7,9'); //note arrays don't have | pipes in them
	$moo=new googleChart($data);
	$moo->draw();
```

![http://chart.apis.google.com/chart?chs=150x67&cht=lc&chxt=x&chxl=0:|june|july|aug&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=lc&chxt=x&chxl=0:|june|july|aug&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg)
CHART WITH LABEL:
```
	$moo= new googleChart('4,6,21,7,1,6,17,5,2,1,7,9');
	$moo->setLabels('june|july|aug','bottom');
	$moo->draw();
```

![http://chart.apis.google.com/chart?chs=100x67&cht=p&chtt=foods&chl=cake|pie|muffins|cookies|icecream&chco=0088ff,8800ff,4444ff&chd=t:50,12.5,75,100,12.5&chxr.jpg](http://chart.apis.google.com/chart?chs=100x67&cht=p&chtt=foods&chl=cake|pie|muffins|cookies|icecream&chco=0088ff,8800ff,4444ff&chd=t:50,12.5,75,100,12.5&chxr.jpg)
CHART BASIC WITH LABELS
```
	$chart1= new googleChart('4,1,6,8,1','pie','foods','300x200');
	$chart1->setLabels('cake|pie|muffins|cookies|icecream');
	$chart1->draw();
```

![http://chart.apis.google.com/chart?chs=150x67&cht=lc&chxt=r,x&chxl=0:|0|5|10|15|20|1:|june|july|aug&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=lc&chxt=r,x&chxl=0:|0|5|10|15|20|1:|june|july|aug&chco=0088ff,8800ff,4444ff&chd=t:19,28.6,100,33.3,4.8,28.6,81,23.8,9.5,4.8,33.3,42.9&chxr.jpg)
CHART WITH LABEL AND MIN/MAX VALUES ON RIGHT
```
	$moo= new googleChart('4,6,21,7,1,6,17,5,2,1,7,9');
	$moo->setLabelsMinMax(5,'right'); //call before other funcs that make labels
	$moo->setLabels('june|july|aug','bottom');
	$moo->draw();
```

![http://chart.apis.google.com/chart?chs=150x67&cht=p&chl=cows|dogs|peas&chco=0088ff,8800ff,4444ff&chd=t:6.2,35.4,100&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=p&chl=cows|dogs|peas&chco=0088ff,8800ff,4444ff&chd=t:6.2,35.4,100&chxr.jpg)
PIE CHART WITH LABELS
```
	$data='4,23,65';
	$moo= new googleChart($data,'pie');
	$moo->setLabels('cows|dogs|peas');
	$moo->draw(true);
```

> //or an alternative to above 'pie' you can use $moo->setType('pie');

![http://chart.apis.google.com/chart?chs=150x67&cht=lc&chdl=cows|dogs|peas&chxt=y&chxl=0:|0|2|4|6|8&chco=0088ff,8800ff,4444ff&chd=t:44.4,55.6,66.7,77.8,100|66.7,11.1,44.4,22.2,66.7|60,100,11.1,66.7,22.2|44.4,55.6,66.7,77.8,100|66.7,11.1,44.4,22.2,66.7|60,100,11.1,66.7,22.2&chxr.jpg](http://chart.apis.google.com/chart?chs=150x67&cht=lc&chdl=cows|dogs|peas&chxt=y&chxl=0:|0|2|4|6|8&chco=0088ff,8800ff,4444ff&chd=t:44.4,55.6,66.7,77.8,100|66.7,11.1,44.4,22.2,66.7|60,100,11.1,66.7,22.2|44.4,55.6,66.7,77.8,100|66.7,11.1,44.4,22.2,66.7|60,100,11.1,66.7,22.2&chxr.jpg)
CHART WITH 3 DIFFERENT DATA SETS using smartDataLabel(), A LEGEND AND MINMAX LABELS
```
	$data=array(
		'cows'=>array(4,5,6,7,9),
		'dogs'=>array(6,1,4,2,6),
		'peas'=>array(5.4,9,1,6,2)
	);
	$moo= new googleChart();
	$moo->smartDataLabel($data);
	$moo->setLabelsMinMax(5,'left'); 
	$moo->draw(true);
```

![http://chart.apis.google.com/chart?chs=300x100&cht=lc&chdl=Ammount%20of%20cookies|Raisens&chxt=y,x,y&chxl=0:|0|4|8|1:|jan|feb|march|apr|may|2:|+low|mid|top&chm=B,76A4FB,0,0,0&chg=20,50,1&chco=0088ff,8800ff,4444ff&chd=t:12.5,50,75,100,25|37.5,87.5,100,37.5,25&chxr.jpg](http://chart.apis.google.com/chart?chs=300x100&cht=lc&chdl=Ammount%20of%20cookies|Raisens&chxt=y,x,y&chxl=0:|0|4|8|1:|jan|feb|march|apr|may|2:|+low|mid|top&chm=B,76A4FB,0,0,0&chg=20,50,1&chco=0088ff,8800ff,4444ff&chd=t:12.5,50,75,100,25|37.5,87.5,100,37.5,25&chxr.jpg)
CHART WITH LOTS OF OPTIONS, data sets are supplied in a string
```
	$data='1,4,6,8,2|3,7,8,3,2';
	$chart1=new googleChart($data);
	$chart1->dimensions='400x125';
	$chart1->fillColor='76A4FB';
	$chart1->setLabelsMinMax();
	$chart1->legend='Ammount of cookies|Raisens';
	$chart1->setLabels('jan|feb|march|apr|may','bottom');
	$chart1->setLabels('+low|mid|top','left');
	$chart1->showGrid=1;
	$chart1->draw();
```

![http://chart.apis.google.com/chart?chs=450x150&cht=lc&chtt=Expenses&chbh=10&chxt=y,x,x&chxl=0:|0|6155|12310|1:|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|28|29|30|31|2:|May&chg=3.33,50,1&chco=0088ff,8800ff,4444ff&chd=t:0,0,0.9,0,0,0,100,3.9,0,0,3.8,0,0,0,3.2,0,0,0,0,0,1.1,12.3,0,0,3.7,0,0,0,0,10.2,18.2&chxr=&chxr.png](http://chart.apis.google.com/chart?chs=450x150&cht=lc&chtt=Expenses&chbh=10&chxt=y,x,x&chxl=0:|0|6155|12310|1:|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|28|29|30|31|2:|May&chg=3.33,50,1&chco=0088ff,8800ff,4444ff&chd=t:0,0,0.9,0,0,0,100,3.9,0,0,3.8,0,0,0,3.2,0,0,0,0,0,1.1,12.3,0,0,3.7,0,0,0,0,10.2,18.2&chxr=&chxr.png)
CHART USING NEGATIVE NUMBERS AND AUTO-GRID	$month='May';
	$daysInMonth=31;
	$chartDates='';
	for ($i=1;$i<=$daysInMonth;$i++) {
		if ($chartDates) $chartDates.='|';
		$chartDates.=$i;
	}
	$chartData='0,0,-109.9,0,0,0,-12310.58,-478.5,0,0,-473.38,0,0,0,-398,0,0,0,0,0,-134.6,-1513.1,0,0,-454.26,0,0,0,0,-1258.04,-2237.8';

	$chart=new googleChart(null,'line','Expenses','700x250');
	$chart->negativeMode=true; //values are negative
	$chart->loadData($chartData);
	$chart->barWidth=10; //makes bars thinner
	$chart->setLabelsMinMax();
	$chart->setLabels($chartDates,'bottom');
	$chart->setLabels($month,'bottom');
	$chart->showGrid=1;
	$chart->draw();
	
TO ADD A LEGEND MANUALLY:
{{{
$moo->legend='cows|dogs|carrots|rubber';
}}}

CHART WITH OTHER FUNCTIONS

To convert data to simple mode (for smaller urls I guess)
{{{
	$moo->simpleDataMode();
}}}
	
To changes some colors (you can supply more than needed)
{{{
	$moo->colors='8888ff,4444ff,670032';
}}}```