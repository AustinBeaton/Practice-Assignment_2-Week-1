# Practice-Assignment_2-Week-1
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
  <meta http-equiv="content-type" content="text/html; charset=UTF-8"/>
  <title>Fruit Chart</title>
  <script type="text/javascript" src="jquery.min.js" ></script>
  <script type="text/javascript" src="d3.v3.js"></script>
  <style>
     body {
       font: 10px sans-serif;
       background-color: grey;
     }
     .chart {
       font-family: Impact, sans-serif;
       font-size: 12px;
     }
     .axis path, .axis line {
       fill: none;
       stroke: #000000;
       stroke-width: 1px;
       shape-rendering: crispEdges;
      }
     .grid line {
      fill:none;
      stroke: #AEAEAE;
      stroke-width: 1px;
      shape-rendering: crispEdges;
     }
     .bar {
       z-index: 1000;
      }
     .bar {
       fill: maroon;
      }
     .bar:hover {
       fill: black;
      }
      .chart text {
        fill:maroon;
      }
  </style>

  <script type="text/javascript">
        $(document).ready(function() {
            var data=
              [{"Quantity":"189","class":"1st Year"},
               {"Quantity":"112","class":"2nd Year"},
               {"Quantity":"45","class":"3rd Year"},
               {"Quantity":"15","class":"4th Year"},
               ];
            var margin = {top:40,right:40,bottom:40,left:90},
                width = 600,
                height = 500-margin.left-margin.right;
            var x = d3.scale.linear()
                .domain([0, d3.max(data, function(d) {return +d.Quantity;})])
                .range([0, width - margin.left - margin.right]);
            var y = d3.scale.ordinal()
                .domain(data.map(function(d) {return d.class;}))
                .rangeBands([3,height - margin.top - margin.bottom]);
            var xAxis = d3.svg.axis()
                .scale(x)
                .orient('bottom')
                .tickPadding(6);
            var xAxis1 = d3.svg.axis()
                .scale(x)
                .orient('bottom');
            var yAxis = d3.svg.axis()
                .scale(y)
                .orient('left')
                .ticks(1)
                .tickSize(0)
                .tickPadding(8);
            var svg = d3.select('#bar-demo').append('svg')
                .attr('class', 'chart')
                .attr('width', width)
                .attr('height', height)
                .append('g')
                .attr('transform', 'translate(' + margin.left + ', ' + margin.top + ')');
            svg.append('g')
                .attr("class", 'axis')
                .attr('transform', 'translate(0, ' + (height - margin.top - margin.bottom) + ')') 
                .call(xAxis);
            svg.append('g')
                .attr('class', 'axis')
                .call(yAxis);
            svg.append("g")        
                .attr("class", "grid")
                .attr("transform", "translate(0," + (height - margin.bottom - margin.top)+")")
                .call(xAxis1 
                .ticks(10) 
                .tickSize(-(height-margin.top-margin.bottom), 0, 0)
                .tickFormat("")
                );
            svg.selectAll('.chart')
                .data(data)
                .enter()
                .append('rect')
                .attr('class', 'bar')
                .attr('x', 0)
                .attr('y', function(d,i){return -1 + margin.top + y.rangeBand() * i - margin.top;})
                .attr('height', 60)
                .attr('width', function(d) { return x(d.Quantity) });
            svg.selectAll(".rect")
               .data(data)
               .enter().append("svg:text")
               .attr("y", function(d) { return y(d.class); })
               .attr("x", function(d) { return x(d.Quantity-20); })
               .attr("dx", "1.75em") 
               .attr("dy", "1.70em") 
               .attr("text-anchor", "right") 
               .text(function(d) { return d.Quantity });
            svg.append("text")
                      .attr("x", (width / 2 - margin.left))
                      .attr("y", 0 - (margin.top / 2))
                      .attr("text-anchor", "middle")
                      .style("font-size", "20px")
                      .text("Average Class Size by Year");
    });
  </script>

</head>

<body>
  <div id="bar-demo"  style="position: relative; top: 3px; left: 20px;"></div>
  
</body>
</html>
