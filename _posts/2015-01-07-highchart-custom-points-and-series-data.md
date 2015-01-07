---
title: Use custom points and series data on Highcharts
description: HTML5 helps SEO or not and how to improve your blog with it's new syntax? I will give comparisons and guides.
tags: [highcharts, javascript]
category : javascript
---

I cameup with some problem upon using [Highcharts](http://www.highcharts.com/) recently that require me to have data contain in point and series. In this post I'm gonna put some solution up.


## Starting point
Let's take this fiddle straight from Highcharts docs and add some spice to it:

<iframe width="100%" height="300" src="http://jsfiddle.net/taduyducvn/1xLuwqbu/embedded/result,js,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

## Extra series datas

Let's say we have an extra for each of the series here we want to add. For example, I want to have each serie contains a country object.
{% highlight javascript %}
{
	series: [{
	    name: 'Tokyo',
	    data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, 26.5, 23.3, 18.3, 13.9, 9.6],
	    country: 'Japan'
	}, {
	    name: 'New York',
	    data: [-0.2, 0.8, 5.7, 11.3, 17.0, 22.0, 24.8, 24.1, 20.1, 14.1, 8.6, 2.5],
	    country: 'USA'
	}, {
	    name: 'Berlin',
	    data: [-0.9, 0.6, 3.5, 8.4, 13.5, 17.0, 18.6, 17.9, 14.3, 9.0, 3.9, 1.0],
	    country: 'German'
	}, {
	    name: 'London',
	    data: [3.9, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8],
	    country: 'UK'
	}]
}
{% endhighlight %}

After add the variable in serie data, we can use it using `this.series.options.country` in formaters.

Here is an example in a tooltip formater:

{% highlight javascript %}
      tooltip: {
         formatter: function() {
             return 'Country:' + this.series.options.country;
         }
      }
{% endhighlight %}

The good thing is that you can put almost anything in here, including complex JSON Object with some anonymous functions.

<iframe width="100%" height="300" src="http://jsfiddle.net/taduyducvn/j4u5d7pd/1/embedded/result,js,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

## Extra point data

We have extra datas for the whole serie, how about each of the point with another custom value? The reason why I need to work on this solution because the `data: []` in series object is only accept an array of numbers and anything else will be rejected. I tried with array of object but it won't work that way. Instead I use the index and an extra unique ID for each of the serie to map with an object. For the data array, you will need to write some function to output this array from your set of data.

To get the index of a point: `this.series.data.indexOf( this.point )`

Let's say we have this data:
{% highlight javascript %}
var tempDb = {
	'tokyo': [
		{'feellike': -1, 'detail': 'Cloudy'},
		{'feellike': -2, 'detail': 'Sunny'},
		{'feellike': -6, 'detail': 'Cloudy'},
		{'feellike': -7, 'detail': 'Sunny'},
		{'feellike': -8, 'detail': 'Foggy'},
	],
	'newyork': [
		{'feellike': -2, 'detail': 'Sunny'},
		{'feellike': -3, 'detail': 'Foggy'},
		{'feellike': -6, 'detail': 'Cloudy'},
		{'feellike': -7, 'detail': 'Sunny'},
		{'feellike': -8, 'detail': 'Foggy'},
	],
	'berlin': [
		{'feellike': -2, 'detail': 'Sunny'},
		{'feellike': -3, 'detail': 'Foggy'},
		{'feellike': -4, 'detail': 'Funny'},
		{'feellike': -5, 'detail': 'Rainy'},
		{'feellike': -6, 'detail': 'Cloudy'},
	],
	'london': [
		{'feellike': -4, 'detail': 'Funny'},
		{'feellike': -5, 'detail': 'Rainy'},
		{'feellike': -6, 'detail': 'Cloudy'},
		{'feellike': -7, 'detail': 'Sunny'},
		{'feellike': -8, 'detail': 'Foggy'},
	]
};
{% endhighlight %}

Here is the updated tooltip formatter:
{% highlight javascript %}
	tooltip: {
	 formatter: function() {
	     var i = this.series.data.indexOf( this.point ),
	         data = tempDb[this.series.options._id][i];

	     /*
	      * You definitly will want to check for
	      * null / undefine here before output
	      */

	     return '<b>' + this.series.name + '</b>' +
	         '<br />Country: ' + this.series.options.country +
	         '<br />Month: ' + this.x +
	         '<br />Temperature: ' + this.y +'°C' +
	         '<br />Feel like: ' + data.feellike +'°C' +
	         '<br />Detail: ' + data.detail;
	 }
	}
{% endhighlight %}

I also add an id in series option so I can get the id using `this.series.options._id`.

Here's the result:
<iframe width="100%" height="300" src="http://jsfiddle.net/taduyducvn/9cxj13dy/1/embedded/result,js,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

**Note:** You can also set the serie option to contain a set of extra data for points:

{% highlight javascript %}
{
    name: 'London',
    data: [3.9, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8],
    country: 'UK',
    extra: tempDb[_id]
}
{% endhighlight %}

And in tooltips, use the ff. code: `this.series.options.extra[ this.series.data.indexOf( this.point ) ]` to access point value.

Highcharts is a very powerful charting library, I have to admit. Hope you guys enjoy the technique and have a great time with Highcharts. If you have any questions, don't hestitate to give a comment.
