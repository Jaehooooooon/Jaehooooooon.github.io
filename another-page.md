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
</head>

<body>	
<h1>Hello Analytics Reporting API V4 TEST</h1>
	
<!-- The Sign-in button. This will run `queryReports()` on success. -->
<p class="g-signin2" data-onsuccess="queryReports"></p>
	
<!-- The API response will be printed here. -->
<textarea cols="80" rows="20" id="query-output"></textarea>
	
<script>
// Replace with your view ID.
var VIEW_ID = '197883945';
	
// Query the API and print the results to the page.
function queryReports() {
	    console.log('queryReports called');
	    gapi.client.request({
	      path: '/v4/reports:batchGet',
	      root: 'https://analyticsreporting.googleapis.com/',
	      method: 'POST',
	      body: {
	        reportRequests: [
	          {
	            viewId: VIEW_ID,
	            dateRanges: [
	              {
	                startDate: '7daysAgo',
	                endDate: 'yesterday'
	              }
	            ],
	            metrics: [
	              {
	                expression: 'ga:users'
	              }
	            ]
				,dimensions: expression: 'ga:deviceCategory'
	          }
	        ]
	      }
	    }).then(displayResults, console.error.bind(console));
	    console.log('finished');
	  }
	
function displayResults(response) {
	    var formattedJson = JSON.stringify(response.result, null, 2);
	    console.log('Results : ', formattedJson);
	    document.getElementById('query-output').value = formattedJson;

		var obj = JSON.parse(formattedJson);
		console.log('10');
		console.log('a : ', obj);
		console.log('b : ', obj.reports);
		console.log('c : ', obj.reports[0]);
		console.log('d : ', obj.reports[0].columnHeader.metricHeader.metricHeaderEntries[0].name);
	  }
</script>
	
<!-- Load the JavaScript API client and Sign-in library. -->
<script src="https://apis.google.com/js/client:platform.js"></script>
	
</body>
</html>
