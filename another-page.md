---
layout: default
---

## Welcome to google analytics page

_hello_

[back](./)

<html>

<head>
	<meta charset="utf-8">
	<title>Hello Analytics Reporting API V4</title>
	<meta name="google-signin-client_id" content="436705610339-iv7fudo64feeivnd939pqd6df4nu5suv.apps.googleusercontent.com">
	<meta name="google-signin-scope" content="https://www.googleapis.com/auth/analytics.readonly">
	<script src="https://d3js.org/d3.v5.min.js"></script>
	<script src = "https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.1/Chart.bundle.min.js"></script>
</head>

<body>	
<h1>Hello Analytics Reporting API V4 TEST</h1>
	
<!-- The Sign-in button. This will run `queryReports()` on success. -->
<p class="g-signin2" data-onsuccess="queryReports"></p>
	
<!-- The API response will be printed here. -->
<textarea cols="80" rows="20" id="query-output"></textarea>
	
<script>
//varToSet
var i = 1;
var sessions = [];
sessions[0] = 7;

// Replace with your view ID.
var VIEW_ID1 = '197883945';
var VIEW_ID2 = '198637112';	

// Query the API and print the results to the page.
function queryReports() {
	    console.log('queryReports1 called');
	    gapi.client.request({
	      path: '/v4/reports:batchGet',
	      root: 'https://analyticsreporting.googleapis.com/',
	      method: 'POST',
	      body: {
	        reportRequests: [
	          {
	            viewId: VIEW_ID1,
	            dateRanges: [
	              	{
	               		startDate: '7daysAgo',
	                	endDate: 'yesterday'
	              	}
	            ],
	            metrics: [
	            	//{expression: 'ga:users'},
					{expression: 'ga:sessions'}
	            ],
				dimensions: [
					//{'name':'ga:userType'},
					//{'name':'ga:deviceCategory'}
				]

	          }
	        ]
	      }
	    }).then(displayResults, console.error.bind(console));
	    console.log('finished');

		console.log('queryReports2 called');
	    gapi.client.request({
	      path: '/v4/reports:batchGet',
	      root: 'https://analyticsreporting.googleapis.com/',
	      method: 'POST',
	      body: {
	        reportRequests: [
	          {
	            viewId: VIEW_ID2,
	            dateRanges: [
	              	{
	               		startDate: '7daysAgo',
	                	endDate: 'yesterday'
	              	}
	            ],
	            metrics: [
	            	//{expression: 'ga:users'},
					{expression: 'ga:sessions'}
	            ],
				dimensions: [
					//{'name':'ga:userType'},
					//{'name':'ga:deviceCategory'}
				]

	          }
	        ]
	      }
	    }).then(displayResults, console.error.bind(console));
	    console.log('finished');
	  }

function displayResults(response) {
	    var formattedJson = JSON.stringify(response.result, null, 2);
	    //console.log('Results : ', formattedJson);
	    document.getElementById('query-output').value += formattedJson;

		var obj = JSON.parse(formattedJson);
		console.log('17');
		console.log('a : ', obj.reports[0]);
		//console.log('dimensions: ', obj.reports[0].columnHeader.dimensions);
		//console.log('data.totals: ', obj.reports[0].data.totals);
		//console.log('metricHeaderEntries: ', obj.reports[0].columnHeader.metricHeader.metricHeaderEntries);	
		console.log('metrics: ', obj.reports[0].data.totals[0].values[0]);
		sessions[i] = obj.reports[0].data.totals[0].values[0];
		console.log('test1: ', sessions[i]);
		i++;

		//test(dimensions);
	  }

function test(_dimensions) {
	console.log('test');
	return new Promise(function (resolve, reject) {
		fetch(/*parameters*/).then(function (res) {
			res.json().then(body => {

				var obj = JSON.parse(body)

			}).catch(err => {
				reject("error fetching.")
			});
		});
	})
}

</script>
    <script>
    var myjson={
        "key1": "value1",
        "key2": "value2",
        "key3": "value3",
        "key4": "value4",
        "key5": "value5",
    };
    </script>
<!-- Load the JavaScript API client and Sign-in library. -->
<script src="https://apis.google.com/js/client:platform.js"></script>
	
<div class="chart-grid" style="display: grid; grid-template-columns: 300px;">
    <div class="chart" style="width: 300px; height: 300px;">
        <canvas id="myChart" width="200" height="200"></canvas>
    </div>
    <div class="input">
        1 : <input id="firstChartInput" type="text">
    </div>
</div>

<script>
console.log('확인 : ', sessions[0], ', ', sessions[1], ', ', sessions[2]);
var x = 2;
var ctx = document.getElementById('myChart').getContext('2d');
var myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: '# of Votes',
            data: [sessions[1], sessions[2], x, 5, 2, 3],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
});

</script>

</body>
</html>
