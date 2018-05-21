---
layout: post
title: "Radiometer"
meta: "radiometer"
permalink: /case-studies/radiometer/
next-case-study-title: "000"
next-case-study-url: /case-studies/000/
hide-hire-me-link: true
---
<strong>Note 2016-01-25: No new data is being collected since Nov 5th, 2015. This is caused by a hardware-related malfunction in the radiometer equipment. Dates before Nov 5th display normally.</strong>
In summer 2015, I joined Shaun Taylor's team at the Clean Energy Institute (Seattle, USA). My job was to completely revolutionize the way his team made sense out of solar panel efficiency data.

ARTIFACTS:
<a href="http://www.cei.washington.edu/education/uw-solar-spectrum-projects/radiometer-data/">Project Website</a>
<a href="http://www.cei.washington.edu/radiometer/graph.html?date=06%2F20%2F2015&calendarsubmit=Submit">Project Graphs</a>
<a href="http://koendecouck.com/resources/radiometer/graph.html">Project Graphs (Demo)</a>
<a href="http://www.cei.washington.edu/education/uw-solar-spectrum-projects/solar-data-widget/">Project Web Widget</a>

<a href="/_post_images/2015/10/IMG_3830b.png"><img src="/_post_images/2015/10/IMG_3830b.png" alt="IMG_3830b" width="540" height="240" class="aligncenter size-full wp-image-6269" /></a>
<em>Roof of the power plant. Here 3 types of solar panels are set up, along with a radiometer sensor (top right corner). Irradiance data is continuously written from the sensor to an (encrypted) log file on a local Windows XP server downstairs.</em>

<a href="/_post_images/2015/10/yesdas_old.png"><img src="/_post_images/2015/10/yesdas_old.png" alt="yesdas_old" width="728" height="401" class="aligncenter size-full wp-image-6270" /></a>
<em>Before: this is the original, online YESDAS interface that came with the sensor. It had quite a lot of issues. Try it for yourself here, hosted by the <a href="http://134.74.16.39/">Tiny College of New York</a></em>

<a href="/_post_images/2015/10/fig-total-irradiance.png"><img src="/_post_images/2015/10/fig-total-irradiance.png" alt="fig-total-irradiance" width="760" height="401" class="aligncenter size-full wp-image-6226" /></a><em>After: I build a javascript-based web interface that reads in the data and dynamically regenerates graphs like these. The different lines represent different wavelengths of sunlight. Try it for yourself here, hosted by the <a href="http://www.cei.washington.edu/radiometer/graph.html?date=06%2F20%2F2015&calendarsubmit=Submit">Clean Energy Institute</a></em>

<strong>SOLUTION</strong>
<strong>CODEFRAGMENT POWERSHELL 'csv.ps1'</strong>
This Powershell script takes the raw txt dumps and turns them into useable csv files. It adds a header, removes junk, changes the log's serialdate timestamp to UTC, adds a useful metric called 'cumulative kWh' and backups the data on MongoDB. The diagnostics is basically just a stopwatch to help me debug any problems. This is a back-end script running server-side.
--
<code>
    $sw = [Diagnostics.Stopwatch]::StartNew()
    
    #INPUT-OUTPUT
    ###############
    $file = gci C:\Program` Files\YESINC\YESDAS\My` YESDAS` Network\Power` Plant` Roof\YESDAS1\ChannelProfile1\*.txt | sort LastWriteTime | select -last 1
    $header = @('date(PST),time(PST),serialtime,cos,temp(°C),HTRV(V),tot(W/m^2),tot414((W/m^2)/nm),tot496((W/m^2)/nm),tot613((W/m^2)/nm),tot670((W/m^2)/nm),tot869((W/m^2)/nm),tot937((W/m^2)/nm),diffuse(W/m^2),diffuse414((W/m^2)/nm),diffuse496((W/m^2)/nm),diffuse613((W/m^2)/nm),diffuse670((W/m^2)/nm),diffuse869((W/m^2)/nm),diffuse937((W/m^2)/nm),dirnorm(W/m^2),dirnorm414((W/m^2)/nm),dirnorm496((W/m^2)/nm),dirnorm613((W/m^2)/nm),dirnorm670((W/m^2)/nm),dirnorm869((W/m^2)/nm),dirnorm937((W/m^2)/nm),cumulativekWh(kWh)')

    $f= gc $file |select -Skip 25;
    $outputfile = $file.name -replace '.txt','.csv';
    $outputfilePath="C:\Program` Files\YESINC\YESDAS\My` YESDAS` Network\Power` Plant` Roof\YESDAS1\public\csv\"+$outputfile;

    #Delete existing file
    If (Test-Path $outputfilePath){
    	Remove-Item $outputfilePath
    }

    #ADD A UTC DATE
    ##################
    #Set current daylight savings time (DST) offset
    $dst = [decimal]$f[0].substring(6,7);

    for($i=0;$i -lt $f.Length;$i++){
    	$serialdate = $f[$i].substring(0,5)+'.'+$f[$i].substring(8,5);
    	$serialstart='01/01/1900' | Get-Date; $utc=$serialstart.AddDays($serialdate-(1+$dst));
    	$utc = $utc.addseconds(1);
    	$f[$i]=[string]$utc+','+$f[$i]
    }; 



    #CLEANING
    #################
    #You could also do this through a pipeline (but that just kept complaining)
    #keep adding pipeline components by |%{...}`
    #use ` to split code over multiple lines without breaking
    #$f[0..($f.count-1)]`
    #|%{$_.Trim()-replace'\s+',','}`
    #|%{$_.Insert(25,'&')}|%{$_.Trim()-replace'&,0',''}`
    #|%{$_.Trim()-replace'\*5','0'}

    #remove blank spaces
    $f = $f[0..($f.count-1)] -replace'\s+',','

    #combine serial date and serial time
    $f = for($i=0;$i -lt $f.Length;$i++){$f[$i].Insert(25,'&');};
    $f = $f[0..($f.count-1)] -replace'&,0',''

    #don't show seconds
    $f = for($i=0;$i -lt $f.Length;$i++){$f[$i].Insert(19,'&');};
    $f = $f[0..($f.count-1)] -replace':01&',''
    $f = $f[0..($f.count-1)] -replace':00&',''

    #replace *5's by zeros
    $f = $f[0..($f.count-1)] -replace'\*5','0'

    #insert the header
    $f= $header + $f

    #ADD Cumulative kWh
    ##################
    #Save total irradiance in separate array in preparation for cum.kWh calculation.
    $totals= $f.Clone();
    for($i=1;$i -lt $f.Length;$i++){
    	If ($f[$i].substring(29,1) -like '-')
    		{
    		$totals[$i]='0'
    		}
    	If ($f[$i].substring(51,1) -like ',')
    		{
    		$totals[$i]='0'
    		}
    	If ($f[$i].substring(51,1) -like '.')
    		{
    		$totals[$i]=$f[$i].substring(50,6)
    		}
    	If ($f[$i].substring(52,1) -like '.')
    		{
    		$totals[$i]=$f[$i].substring(50,7)
    		}
    	If ($f[$i].substring(53,1) -like '.')
    		{
    		$totals[$i]=$f[$i].substring(50,8)
    		}
    	If ($f[$i].substring(54,1) -like '.')
    		{
    		$totals[$i]=$f[$i].substring(50,9)
    		}
    };

    #Calculate cumulative kWh's...
    #Note: (the if's fix format glitches for '0' and '.xxxx')
    $totals[1]= '0'
    for($i=2;$i -lt $f.Length;$i++){
    	$totals[$i]=[decimal]$totals[$i-1] + [decimal]$totals[$i]/60000
    	$totals[$i]=$totals[$i] | % {$_.ToString("#.####")}
    	If ($f[$i].substring(29,1) -like '-')
    		{
    		$totals[$i]=$totals[$i-1]
    		}
    	If ($totals[$i] -lt 1)
    		{
    		$totals[$i]=0 + $totals[$i]
    		}
    };

    #Paste calculated cumulative kWh's at end of each dataline.
    for($i=1;$i -lt $f.Length;$i++){
    	$f[$i]=$f[$i]+','+$totals[$i];
    };


    #############################
    #WRITE FILE
    #############################
    $f| out-file -filepath $outputfilePath -encoding utf8

    #IMPORT DATA IN MONGODB
    #########################
    $dbcollectiondrop = "db."+$filename+".drop()"
    $collection = $file.name -replace '.txt','';
    $dayfile = "C:\Program Files\YESINC\YESDAS\My YESDAS Network\Power Plant Roof\YESDAS1\public\csv\"+$outputfile
    cd C:\Program` Files\YESINC\YESDAS\My` YESDAS` Network\Power` Plant` Roof\YESDAS1\mongodb-win32-i386-2.0.6\bin
    .\mongo radiometer --eval $dbcollectiondrop
    .\mongoimport -d radiometer -c $collection --type csv --file $dayfile --headerline
    cd C:\Program` Files\YESINC\YESDAS\My` YESDAS` Network\Power` Plant` Roof\YESDAS1\public\csv\

    #DIAGNOSTICS
    ################
    write-output “done”
    $sw.Stop()
    $sw.Elapsed</code>
    --
    <strong>CODEFRAGMENT JAVASCRIPT 'drawTotal.js'</strong>
    This particular function generates the 'Total Irradiance per Wavelength' graph as seen above. It draws on a parent function 'drawChart' to do most of the hard work. This 
    --
    <code>google.setOnLoadCallback(drawTotals);
    function drawTotals(csv) {
        var data = new google.visualization.DataTable();
        data.addColumn('number', 'Item');
        data.addColumn('number', '414 nm');
        data.addColumn('number', '496 nm');
        data.addColumn('number', '613 nm');
        data.addColumn('number', '670 nm');
        data.addColumn('number', '869 nm');
        data.addColumn('number', '937 nm');;
        var ymax = [];
        for (var i = 1; i < csv.length-1; i++) {
        	data.addRows([[i, csv[i][7], csv[i][8], csv[i][9], csv[i][10], csv[i][11], csv[i][12]],]);
        	if (ymax < csv[i][8]){ymax = csv[i][8]};
            if (ymax < csv[i][9]){ymax = csv[i][9]};
            if (ymax < csv[i][10]){ymax = csv[i][10]};
            if (ymax < csv[i][11]){ymax = csv[i][11]};
            if (ymax < csv[i][12]){ymax = csv[i][12]};
    	};

        var view = new google.visualization.DataView(data);
        var seriesColors = ['blue', 'green', 'orange', 'red', 'brown', 'grey']; 
        var chart = new google.visualization.LineChart($('#chart_totals')[0]);
        chart.draw(view, { //options on load
        	title: csv[1][0],
        	//width: 900,
       		//height: 400,
       		lineWidth: 1,
            'chartArea': {'width': '80%', 'height': '80%'},
            strictFirstColumnType: true,
            vAxis: {title: "Total irradiance (W/m^2)/nm",viewWindowMode:'explicit',viewWindow:{max:ymax,min:0}},
             hAxis: {title: "Time (PST)", slantedText:false, ticks: [{v:1, f:"00:00"},{v:61, f:""},{v:121, f:""},{v:181, f:""},{v:241, f:"04:00"},{v:301, f:""},{v:361, f:""},{v:421, f:""},{v:481, f:"08:00"},{v:541, f:""},{v:601, f:""},{v:661, f:""},{v:721, f:"12:00"},{v:781, f:""},{v:841, f:""},{v:901, f:""},{v:961, f:"16:00"},{v:1021, f:""},{v:1081, f:""},{v:1141, f:""},{v:1201, f:"20:00"},{v:1261, f:""},{v:1321, f:""},{v:1381, f:""},{v:1440, f:"00:00"}]},
            colors: seriesColors,
            legend: 'none'
        });

        $('#totals').find(':checkbox').change(function () {
            var cols = [0];
            var colors = [];   
            $('#totals').find(':checkbox:checked').each(function () {
                console.log(this);
                var value = parseInt($(this).attr('value'));
                cols.push(value);
                colors.push(seriesColors[value - 1]);
                console.log(value, 'colors: ', colors);
            });
            view.setColumns(cols);
            
            chart.draw(view, {//options on refresh
            	title: csv[1][0],
            	//width: 900,
       			//height: 400,
       			lineWidth: 1,
                'chartArea': {'width': '80%', 'height': '80%'},
                strictFirstColumnType: true,
            	vAxis: {title: "Total irradiance (W/m^2)/nm",viewWindowMode:'explicit',viewWindow:{max:ymax,min:0}},
            	hAxis: {title: "Time (PST)", slantedText:false, ticks: [{v:1, f:"00:00"},{v:61, f:""},{v:121, f:""},{v:181, f:""},{v:241, f:"04:00"},{v:301, f:""},{v:361, f:""},{v:421, f:""},{v:481, f:"08:00"},{v:541, f:""},{v:601, f:""},{v:661, f:""},{v:721, f:"12:00"},{v:781, f:""},{v:841, f:""},{v:901, f:""},{v:961, f:"16:00"},{v:1021, f:""},{v:1081, f:""},{v:1141, f:""},{v:1201, f:"20:00"},{v:1261, f:""},{v:1321, f:""},{v:1381, f:""},{v:1440, f:"00:00"}]},
                colors: colors,
                legend: 'none'
            });
        });   
    }
</code>
--

---

{% include promo-next.html %}
