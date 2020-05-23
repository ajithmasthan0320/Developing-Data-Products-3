Generating plot of random numbers

========================================================
author: Ajith Masthan
date: 23-May-2020
autosize: true

Introduction
========================================================

- This peer assessed assignment has two parts. First, you will create a Shiny application and deploy it on Rstudio's servers. Second, you will use Slidify or Rstudio Presenter to prepare a reproducible pitch presentation about your application.



About App
========================================================
This App generates a plot of Random numbers with X,Y coordinates

The app has following functionalities or options
- Number of Random numbers to be generated
- Minimum & Maximum of X Values
- Minimum & Maximum of Y Values
- Options to hide/show X/Y Axis labels
- Option to hide/show Title

ui.R
========================================================


```r
library(shiny)
shinyUI(fluidPage(
  titlePanel("Plot Random Numbers"),
  sidebarLayout(
    sidebarPanel(
      numericInput("numeric", "How Many Random Numbers Should be Plotted?",
                   value = 1000, min = 1, max = 1000, step = 1),
      sliderInput("sliderX", "Pick Minimum and Maximum X Values",
                  -100, 100, value = c(-50, 50)),
      sliderInput("sliderY", "Pick Minimum and Maximum Y Values",
                  -100, 100, value = c(-50, 50)),
      checkboxInput("show_xlab", "Show/Hide X Axis Label", value = TRUE),
      checkboxInput("show_ylab", "Show/Hide Y Axis Label", value = TRUE),
      checkboxInput("show_title", "Show/Hide Title")
    ),
    mainPanel(
      h3("Graph of Random Points"),
      plotOutput("plot1")
    )
  )
))
```

<!--html_preserve--><div class="container-fluid">
<h2>Plot Random Numbers</h2>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label class="control-label" for="numeric">How Many Random Numbers Should be Plotted?</label>
<input id="numeric" type="number" class="form-control" value="1000" min="1" max="1000" step="1"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="sliderX">Pick Minimum and Maximum X Values</label>
<input class="js-range-slider" id="sliderX" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="sliderY">Pick Minimum and Maximum Y Values</label>
<input class="js-range-slider" id="sliderY" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_xlab" type="checkbox" checked="checked"/>
<span>Show/Hide X Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_ylab" type="checkbox" checked="checked"/>
<span>Show/Hide Y Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_title" type="checkbox"/>
<span>Show/Hide Title</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<h3>Graph of Random Points</h3>
<div id="plot1" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
</div>
</div>
</div><!--/html_preserve-->

server.R
========================================================


```r
library(shiny)
shinyServer(function(input, output) {
  output$plot1 <- renderPlot({
    set.seed(2016-05-25)
    number_of_points <- input$numeric
    minX <- input$sliderX[1]
    maxX <- input$sliderX[2]
    minY <- input$sliderY[1]
    maxY <- input$sliderY[2]
    dataX <- runif(number_of_points, minX, maxX)
    dataY <- runif(number_of_points, minY, maxY)
    xlab <- ifelse(input$show_xlab, "X Axis", "")
    ylab <- ifelse(input$show_ylab, "Y Axis", "")
    main <- ifelse(input$show_title, "Title", "")
    plot(dataX, dataY, xlab = xlab, ylab = ylab, main = main,
         xlim = c(-100, 100), ylim = c(-100, 100))
  })
})
```

Link to Git Hub Repository
========================================================
- The app developed and the entire presentation is located in Github Repository:
https://github.com/ajithmasthan0320/Developing-Data-Products-3
