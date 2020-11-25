# ChartsJS add-on

![image](image.png)

## Data Structure: 

For a pie chart, datasets need to contain an array of data points. The data points should be a number, Chart.js will total all of the numbers and calculate the relative proportion of each.

You also need to specify an array of labels so that tooltips appear correctly.

• Enter data manually:
```
	Click "Settings" icon.
	Click "Get Started" button.
	Click "Data" tab.
	Select Data Import Method.
```

• Import data using script to set "BZ_CHARTJS_PIE::data" and "BZ_CHARTJS_PIE::labels" fields:
```
	Create a relationship between "YOUR_SOLUTION" and "BZ_CHARTJS_PIE" Table.
	Set Variable : [ $_data ; Value: "List(YOUR_SOLUTION:DATA_FIELD)" ]
	Set Variable : [ $_labels ; Value: "List(YOUR_SOLUTION:LABEL_FIELD" ]
	Set Field [ BZ_CHARTJS_PIE::data ; $_data ]
	Set Field [ BZ_CHARTJS_PIE::labels ; $_labels ]
	Commit Records/Requests [ With dialog: Off ]
```

• Import data using Execute FileMaker Data API script step:
```
	Create a relationship between "DATA" and "BZ_CHARTJS_PIE" Table.
	Table where your data lives MUST have fields called "DATA" and "LABELS".
	Create separate layout for data api calls. Place "DATA" and "LABEL" field on visible part of layout.
	Go to "Scripts -> Script Workspace -> BZ_CHARTJS_PIE -> getData".
	Edit variable $_query to point to you data table.
	Edit variable $_req. Point "layouts" key to you data api layout.
```

• Import data using data from related fields:
```
	Create a relationship between "DATA" and "BZ_CHARTJS_PIE" Table.
	Open File -> Manage -> Database.
	Select "BZ_CHARTJS_PIE" table. Click on "CHART_OBJECT" field. Select Options.
	Edit Line "~json = If ( IsEmpty ( YourRelatedFieldName ) ; ~json ; JSONSetElement ( ~json ; "data.datasets[0].data"  ; charts.ListToArray ( YourRelatedFieldName ) ; 4 ));"
	Edit Line "~json = If ( IsEmpty ( DATA::LABEL ) ; ~json ; JSONSetElement ( ~json ; "data.labels"  ; charts.ListToArray ( DATA::LABEL ) ; 4 ));
	Save.
```

