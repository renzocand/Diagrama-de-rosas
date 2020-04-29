# Gráfico de rosas

### component.ts
```

  data
  colors = ['#599ad3', '#727272', '#f1595f']
  private dynamicScriptLoader = new DynamicScriptLoader();

  constructor(private service: RosasOperacionesService) {
    this.dynamicScriptLoader.loadScripts([
      { name: 'd3', src: 'assets/js/d3/v5/d3.v5.min.js ', element: 'script' },
      { name: 'd3-ez', src: 'assets/js/d3/v5/d3-ez.min.js', element: 'script' },
      { name: 'd3-ez-css', src: 'https://raw.githack.com/jamesleesaunders/d3-ez/master/dist/d3-ez.css', element: 'style' },
    ], () => this.iniciarGrafico())

  }

  iniciarGrafico() {

    this.service.getData().subscribe(data => {  

      var colors = ["#599ad3", "#727272", "#f1595f"];

      let width = 400
      let height = width
      // Create chart base
      var myChart = d3v5.ez.chart.roseChart()
        .width(width)
        .height(height)


      function clicked(e) {
        console.log(e)
      }



      d3v5.select("#chartholder")
        .datum(data)
        .call(myChart);


      d3v5.select('svg')
        .attr("width", '100%')
        .attr("height", '100%')
        .attr('viewBox', '0 0 ' + Math.min(width, height) + ' ' + Math.min(width, height))
        .attr('preserveAspectRatio', 'xMinYMin')
        .append("g")
        .attr("transform", "translate(" + Math.min(width, height) / 2 + "," + Math.min(width, height) / 2 + ")");

      d3v5.selectAll('.circularLabels text')
        .attr("fill", "white")

      d3v5.selectAll('.rosePetalGroups .seriesGroup').on('click', clicked)

    })
  }

```
* * *
### Data
```
private data = [
      {
      "key": "Importacion",
      "datetime": "1854-04-01T07:00:00.000Z",
      "values": [
        {
          "key": "SubConcepto B",
          "value": 9
        },

        {
          "key": "SubConcepto c",
          "value": 2
        },
        {
          "key": "SubConcepto E",
          "value": 1
        }
      ]
    },
    {
      "key": "Selectividad",
      "datetime": "1854-05-01T07:00:00.000Z",
      "values": [
        {
          "key": "SubConcepto B",
          "value": 8
        },
        {
          "key": "SubConcepto E",
          "value": 0
        },
        {
          "key": "SubConcepto c",
          "value": 0
        }
      ]
    },
    {
      "key": "Transito",
      "datetime": "1854-06-01T07:00:00.000Z",
      "values": [
        {
          "key": "SubConcepto B",
          "value": 6
        },
        {
          "key": "SubConcepto E",
          "value": 2
        },
        {
          "key": "SubConcepto c",
          "value": 1
        }
      ]
    },
    {
      "key": "Concepto A",
      "datetime": "1854-07-01T07:00:00.000Z",
      "values": [
        {
          "key": "SubConcepto B",
          "value": 8
        },
        {
          "key": "SubConcepto E",
          "value": 3
        },
        {
          "key": "SubConcepto c",
          "value": 1
        }
      ]
    },
    {
      "key": "Concepto B",
      "datetime": "1854-08-01T07:00:00.000Z",
      "values": [
        {
          "key": "SubConcepto E",
          "value": 5
        },
        {
          "key": "SubConcepto B",
          "value": 5
        },
        {
          "key": "SubConcepto c",
          "value": 3
        }
      ]}
  ]


    getData(){
        return of(this.data)
    }
```
