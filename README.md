    <script type="text/javascript">

        var url1 = "{% static 'database/salesByMonth' %}";

        var state = ["Alabama", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware", "District of Columbia", "Florida", "Georgia", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky", "Louisiana", "Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi", "Missouri", "Montana", "Nebraska", "Nevada", "New Hampshire", "New Jersey", "New Mexico", "New York", "North Carolina", "Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island", "South Carolina", "South Dakota", "Tennessee"]

        var year = [2014, 2015, 2016, 2017]
        var month = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
        var category = ["Furniture", "Office Supplies", "Technology"]

        var type = ["Tháng", "Năm", "Quý"]
        var select = document.getElementById("selectState");
        var selectYear = document.getElementById("selectYear");
        var select2 = document.getElementById("selectType");

        var select21 = document.getElementById("selectState2");
        var select22 = document.getElementById("selectType2");

        var selectState3 = document.getElementById("selectState3");
        var selectYear3 = document.getElementById("selectYear3");
        var selectCategory3 = document.getElementById("selectCategory3");

        //alert(state[1]);
        for (var i=0; i<state.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = state[i];
            select.add(option, 0);
          //  selectState3.add(option, 0);
        }

        for (var i=0; i<category.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = category[i];
            selectCategory3.add(option, 0);
          //  selectState3.add(option, 0);
        }

        for (var i=0; i<state.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = state[i];
            selectState3.add(option, 0);
          //  selectState3.add(option, 0);
        }

        for (var i=0; i<type.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = type[i];
            select2.add(option, 0);
        }

        for (var i=0; i<state.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = state[i];
            select21.add(option, 0);
        }

        for (var i=0; i<type.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = type[i];
            select22.add(option, 0);
        }

        for (var i=0; i<year.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = year[i];
            selectYear.add(option, 0);
        }

        for (var i=0; i<year.length; i++){
            //dropdown.append($('<option></option>').val(state[i]).html(state[i]));
            var option = document.createElement('option');
            option.text = option.value = year[i];
            selectYear3.add(option, 0);
        }

        var data = {

            labels : [],
            series : [],
            datasets : [
                {
                    label: "First dataset",
                    fillColor : "rgba(128, 222, 234, 0.6)",
                    strokeColor : "#ffffff",
                    pointColor : "#00bcd4",
                    pointStrokeColor : "#ffffff",
                    pointHighlightFill : "#ffffff",
                    pointHighlightStroke : "#ffffff",
                    data: []
                },
            ]
        };

        var data2 = {
            labels : [],
            datasets : [
                {
                    label: "First dataset",
                    fillColor : "rgba(128, 222, 234, 0.6)",
                    strokeColor : "#ffffff",
                    pointColor : "#00bcd4",
                    pointStrokeColor : "#ffffff",
                    pointHighlightFill : "#ffffff",
                    pointHighlightStroke : "#ffffff",
                    data: []
                },
            ]
        };


        function updateDoughnut(year)
        {
            var e = document.getElementById("selectState");
            var state = e.options[e.selectedIndex].value;
            var sales = new Array();
            $.getJSON("{% static 'database/salesByCategoryYear.json' %}", function(json) {
                for(var i=0; i<json.length; i++) {
                    if(json[i].State == state && json[i].year == year) {

                        if(json[i].Category == "Furniture")
                            sales.push(json[i].Sales);
                        if(json[i].Category == "Office Supplies")
                            sales.push(json[i].Sales);
                        if(json[i].Category == "Technology")
                            sales.push(json[i].Sales);
                    }
                }
                var doughnutData2 = [
                    {
                        value: sales[0],
                        color:"#F7464A",
                        highlight: "#FF5A5E",
                        label: "Furniture"
                    },
                    {
                        value: sales[1],
                        color: "#46BFBD",
                        highlight: "#5AD3D1",
                        label: "Office Supplies"
                    },
                    {
                        value: sales[2],
                        color: "#FDB45C",
                        highlight: "#FFC870",
                        label: "Technology"
                    }
                ];
                var doughnutChart = document.getElementById("doughnut-chart").getContext("2d");
                window.myDoughnut = new Chart(doughnutChart).Doughnut(doughnutData2, {
                    segmentStrokeColor : "#fff",
                    tooltipTitleFontFamily: "'Roboto','Helvetica Neue', 'Helvetica', 'Arial', sans-serif",// String - Tooltip title font declaration for the scale label
                    percentageInnerCutout : 50,
                    animationSteps : 15,
                    segmentStrokeWidth : 4,
                    animateScale: true,
                    percentageInnerCutout : 60,
                    responsive : true
                });
            });
        }

        var config = {
                type: 'line',
                data: {
                    labels: [],
                    datasets: [{
 
                        backgroundColor: "#00bcd4",
                        
                        data: [],
                        fill: false,
                    },]
                },
                options: {
                    responsive: true,

                    tooltips: {
                        mode: 'index',
                        intersect: false,
                    },
                    hover: {
                        mode: 'nearest',
                        intersect: true
                    },
                    scales: {
                        xAxes: [{
                            display: true,
                            scaleLabel: {
                                display: true,
                                labelString: 'Quý'
                            },
                            gridLines: {
                                display: false ,
                                color: "#rgba(255,255,255,0.4)"
                            },
                        }],
                        yAxes: [{
                            display: true,
                            scaleLabel: {
                                display: true,
                                labelString: 'Doanh số'
                            },
                            gridLines: {
                                display: false ,
                                color: "#rgba(255,255,255,0.4)"
                            },

                        }]
                    }
                }
            };
        //  $(window).load(function() {
        $.getJSON("{% static 'database/salesByQuarter.json' %}", function(json) {

            var label = new Array();
            var value = new Array();
            var t = new Array();
            for (var i=0; i<json.length; i++) {
                if(json[i].State == 'Alabama') {
                    label.push(json[i].year);
                    value.push(json[i].totalSale);
                }
            }
            config.data.labels = label;
            config.data.datasets[0].data = value;

            var trendingLineChart = document.getElementById("trending-line-chart").getContext("2d");
            
            window.onload = function() {
                var ctx = document.getElementById("trending-line-chart").getContext("2d");
                window.myLine = new Chart(ctx, config);
            };

            var colorNames = Object.keys(window.chartColors);

            /*
            trendingLineChart = new Chart(trendingLineChart).Line(data, {
                scaleYAxesLabel: 'doanh số',
                scaleShowGridLines : true,///Boolean - Whether grid lines are shown across the chart
                scaleGridLineColor : "rgba(255,255,255,0.4)",//String - Colour of the grid lines
                scaleGridLineWidth : 1,//Number - Width of the grid lines
                scaleShowHorizontalLines: true,//Boolean - Whether to show horizontal lines (except X axis)
                scaleShowVerticalLines: false,//Boolean - Whether to show vertical lines (except Y axis)
                bezierCurve : true,//Boolean - Whether the line is curved between points
                bezierCurveTension : 0.4,//Number - Tension of the bezier curve between points
                pointDot : true,//Boolean - Whether to show a dot for each point
                pointDotRadius : 3,//Number - Radius of each point dot in pixels
                pointDotStrokeWidth : 2,//Number - Pixel width of point dot stroke
                pointHitDetectionRadius : 20,//Number - amount extra to add to the radius to cater for hit detection outside the drawn point
                datasetStroke : true,//Boolean - Whether to show a stroke for datasets
                datasetStrokeWidth : 3,//Number - Pixel width of dataset stroke
                datasetFill : true,//Boolean - Whether to fill the dataset with a colour
                animationSteps: 15,// Number - Number of animation steps
                animationEasing: "easeOutQuart",// String - Animation easing effect
                tooltipTitleFontFamily: "'Roboto','Helvetica Neue', 'Helvetica', 'Arial', sans-serif",// String - Tooltip title font declaration for the scale label
                scaleFontSize: 12,// Number - Scale label font size in pixels
                scaleFontStyle: "normal",// String - Scale label font weight style
                scaleFontColor: "#fff",// String - Scale label font colour
                tooltipEvents: ["mousemove", "touchstart", "touchmove"],// Array - Array of string names to attach tooltip events
                tooltipFillColor: "rgba(255,255,255,0.8)",// String - Tooltip background colour
                tooltipTitleFontFamily: "'Roboto','Helvetica Neue', 'Helvetica', 'Arial', sans-serif",// String - Tooltip title font declaration for the scale label
                tooltipFontSize: 12,// Number - Tooltip label font size in pixels
                tooltipFontColor: "#000",// String - Tooltip label font colour
                tooltipTitleFontFamily: "'Roboto','Helvetica Neue', 'Helvetica', 'Arial', sans-serif",// String - Tooltip title font declaration for the scale label
                tooltipTitleFontSize: 14,// Number - Tooltip title font size in pixels
                tooltipTitleFontStyle: "bold",// String - Tooltip title font weight style
                tooltipTitleFontColor: "#000",// String - Tooltip title font colour
                tooltipYPadding: 8,// Number - pixel width of padding around tooltip text
                tooltipXPadding: 16,// Number - pixel width of padding around tooltip text
                tooltipCaretSize: 10,// Number - Size of the caret on the tooltip
                tooltipCornerRadius: 6,// Number - Pixel radius of the tooltip border
                tooltipXOffset: 10,// Number - Pixel offset from point x to tooltip edge
                responsive: true,

                /*
                onAnimationComplete: function () {
                    var sourceCanvas = this.chart.ctx.canvas;
                    // the -5 is so that we don't copy the edges of the line
                    var copyWidth = this.scale.xScalePaddingLeft - 5;
                    // the +5 is so that the bottommost y axis label is not clipped off
                    // we could factor this in using measureText if we wanted to be generic
                    var copyHeight = this.scale.endPoint + 5;
                    var targetCtx = document.getElementById("myChartAxis").getContext("2d");
                    targetCtx.canvas.width = copyWidth;
                    targetCtx.drawImage(sourceCanvas, 0, 0, copyWidth, copyHeight, 0, 0, copyWidth, copyHeight);
                }
                
            });
            */
            
        });

        $.getJSON("{% static 'database/orderByYear.json' %}", function(json) {

            var label = new Array();
            var value = new Array();
            var t = new Array();
            for (var i=0; i<json.length; i++) {
                if(json[i].state == 'Alabama') {
                    label.push(json[i].year);
                    value.push(json[i].totalSell);
                }
            }

            config.data.labels = label;
            config.data.datasets[0].data = value;

            var trendingLineChart2 = document.getElementById("trending-line-chart2").getContext("2d");
            
                var ctx = document.getElementById("trending-line-chart2").getContext("2d");
                window.myLine = new Chart(ctx, config);

        });

        function updateLineChart() {

            var e = document.getElementById("selectState");
            //alert($('#selectState').val());
            var newState = e.options[e.selectedIndex].value;

            var t = document.getElementById("selectType");
            var newType = t.options[t.selectedIndex].value;

            if(newType == "Tháng"){

                var label2 = new Array();
                var value2 = new Array();
                $.getJSON("{% static 'database/salesByMonth.json' %}", function(json) {

                    //alert(json[1].month);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].State == newState) {
                            label2.push(json[i].month);
                            value2.push(json[i].totalSale);
                        }
                    }

                    //alert(value2[1]);

                    var trendingLineChart = document.getElementById("trending-line-chart").getContext("2d");

                    var ctx = document.getElementById("trending-line-chart").getContext("2d");
                    config.data.labels = label2;
                    config.data.datasets[0].data = value2;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Tháng";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }

            else if(newType == "Năm"){
                var label3 = new Array();
                var value3 = new Array();
                $.getJSON("{% static 'database/salesByYear.json' %}", function(json) {

                    //alert(newState);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].State == newState) {
                            label3.push(json[i].year);
                            value3.push(json[i].totalSale);
                        }
                    }
                    alert(label3[1]);
                    data.labels = label3;
                    data.datasets[0].data = value3;

                    var ctx = document.getElementById("trending-line-chart").getContext("2d");
                    config.data.labels = label3;
                    config.data.datasets[0].data = value3;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Năm";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }

            if(newType == "Quý"){
                var label4 = new Array();
                var value4 = new Array();
                $.getJSON("{% static 'database/salesByQuarter.json' %}", function(json) {

                    //alert(newState);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].State == newState) {
                            label4.push(json[i].quarter + "-" + json[i].year);
                            value4.push(json[i].totalSale);
                        }
                    }

                    data.labels = label4;
                    data.datasets[0].data = value4;

                    var ctx = document.getElementById("trending-line-chart").getContext("2d");
                    config.data.labels = label4;
                    config.data.datasets[0].data = value4;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Quý";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }
        }

        function updateLineChart2() {

            var e = document.getElementById("selectState2");
            //alert($('#selectState').val());
            var newState = e.options[e.selectedIndex].value;

            var t = document.getElementById("selectType2");
            var newType = t.options[t.selectedIndex].value;

            //var url = "static/dataset/salesBy" + "Month" + ".json";
            //alert(newType);

            if(newType == "Tháng"){

                var label2 = new Array();
                var value2 = new Array();
                $.getJSON("{% static 'database/orderByMonth.json' %}", function(json) {

                    //alert(newState);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].state == newState) {
                            label2.push(json[i].month);
                            value2.push(json[i].totalSell);
                        }
                    }

                    data2.labels = label2;
                    data2.datasets[0].data = value2;
                    var ctx = document.getElementById("trending-line-chart2").getContext("2d");
                    config.data.labels = label2;
                    config.data.datasets[0].data = value2;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Tháng";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }

            if(newType == "Năm"){
                var label3 = new Array();
                var value3 = new Array();
                $.getJSON("{% static 'database/orderByYear.json' %}", function(json) {

                    //alert(newState);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].state == newState) {
                            label3.push(json[i].year);
                            value3.push(json[i].totalSell);
                        }
                    }
                    
                    var ctx = document.getElementById("trending-line-chart2").getContext("2d");
                    config.data.labels = label2;
                    config.data.datasets[0].data = value2;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Năm";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }

            if(newType == "Quý"){
                var label4 = new Array();
                var value4 = new Array();
                $.getJSON("{% static 'database/orderByQuarter.json' %}", function(json) {

                    //alert(newState);
                    for (var i=0; i<json.length; i++) {
                        if(json[i].State == newState) {
                            label4.push(json[i].quarter + "-" + json[i].year);
                            value4.push(json[i].totalSell);
                        }
                    }

                    var ctx = document.getElementById("trending-line-chart2").getContext("2d");
                    config.data.labels = label2;
                    config.data.datasets[0].data = value2;
                    config.options.scales.xAxes[0].scaleLabel.labelString = "Quý";
                    alert(newState);
                    window.myLine.destroy();
                    window.myLine = new Chart(ctx, config);
                });
            }
        }


