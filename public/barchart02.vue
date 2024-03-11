let echartsObj = echarts.init(document.querySelector('#canvas'));

series = [{
    name: 'Server #1',
    data: [100, 115, 165, 107, 67]
}, {
    name: 'Server #2',
    data: [85, 106, 129, 161, 123]
}, {
    name: 'Server #3',
    data: [67, 87, 86, 167, 157]
}, {
    name: 'Server #3',
    data: [0,0,0,0,0]
}]

genFormatter = (series) => {
    return (param) => {
        console.log(param);
        let sum = 0;
        series.forEach(item => {
            sum += item.data[param.dataIndex];
        });
        return sum
    }
};

function isLastSeries(index) {
    return index === series.length - 1
}
option = {
    color: ['#b8d6f2', '#c6e19a', '#f3b879' ],
    legend: {
        data: series.map(item => item.name),
        right: 'right',
        
    },
    xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']
    },
   
    yAxis: {
        type: 'value'
    },
    series: series.map((item, index) => Object.assign(item, {
        type: 'bar',
        stack: true,
        label: {
            show: true,
            formatter: isLastSeries(index) ? genFormatter(series) : null,
            fontSize:  isLastSeries(index) ? 20 : 15,
            color: 'black',
            position: isLastSeries(index) ? 'top' : 'inside'
        },
    }))
};
echartsObj.setOption(option)

<html>
      <header>
        <script src="https://cdn.bootcss.com/echarts/4.1.0.rc2/echarts-en.min.js"></script>
      </header>
      <body>
        <div id="canvas" style="width: 70%; height: 400px">
        </div>
      </body>
    </html>