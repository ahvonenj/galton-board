# Galton Board

Simulating a [Galton Board](https://en.wikipedia.org/wiki/Bean_machine) to see what kind of (normal) distributions we can get by changing the number or layers and balls dropped.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/GaltonBoard.png/171px-GaltonBoard.png)

## Code

```javascript
var _LAYERS = 17;
var _BALLS = 3000;

function CalculateDelegate()
{
	Calculate(
		true,
		document.getElementById('layers').value,
		document.getElementById('balls').value
	)
}
function Calculate(recalculate, layers, balls)
{
	layers = layers || _LAYERS;
	balls = balls || _BALLS;
  
	var results = [];
  
	// Balls
	for(var i = 0; i < balls; i++)
	{
		var result = 13;
    
		// Galton layers
		for(var j = 0; j < layers; j++)
		{
			var r = Math.random();
      
			if(r >= 0.5)
				result++;
			else
				result--;
        
			if(result < 0)
			{
				result = 0;
				break;
			}
      
			if(result > 26)
			{
				result = 26;
				break;
			}
		}
    
		if(typeof results[result] === 'undefined' || results[result] === false)
			results[result] = 0;
      
		results[result]++;
	}
  
	if(recalculate)
	{
		myChart.data.datasets[0].data = results;
		myChart.update();
	}
	else
	{
		return results;
	}
}

var ctx = document.getElementById("chart").getContext('2d');

var myChart = new Chart(ctx, {
	type: 'line',
	data: 
	{
		labels: "1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27".split('|'),
		datasets: [
		{
			label: 'Galton Distribution',
			data: Calculate(),
			backgroundColor: 
			[
				'rgba(255, 99, 132, 0.2)',
				'rgba(54, 162, 235, 0.2)',
				'rgba(255, 206, 86, 0.2)',
				'rgba(75, 192, 192, 0.2)',
				'rgba(153, 102, 255, 0.2)',
				'rgba(255, 159, 64, 0.2)'
			],
			borderColor:
			[
				'rgba(255,99,132,1)',
				'rgba(54, 162, 235, 1)',
				'rgba(255, 206, 86, 1)',
				'rgba(75, 192, 192, 1)',
				'rgba(153, 102, 255, 1)',
				'rgba(255, 159, 64, 1)'
			],
			borderWidth: 1,
			fill: true,
			spanGaps: true
		}]
	},
	options:
	{
		maintainAspectRatio: false
	}
});
```
