//How to display sum stack bar in echarts

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
            show: index == series.length - 1 ? true : false,
            formatter: genFormatter(series),
            fontSize: 20,
            color: 'black',
            position: 'top'
        },
    }))
};
echartsObj.setOption(option)


<html>
      <header>
        <script src="https://cdn.bootcss.com/echarts/4.1.0.rc2/echarts-en.min.js"></script>
      </header>
      <body>
        <div id="canvas" style="width: 70%; height: 300px">
        </div>
      </body>
</html>