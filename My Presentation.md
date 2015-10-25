My Presentation
========================================================
author: winnie
date: Sun Oct 25 21:47:51 2015
transition:rotate

My feeling for R programming
========================================================
transition:rotate
font-family: 'Helvetica' 
- It is goddamn hard!!  

- I think the difficulty is $hard^n$!!

- Every minute I want to cry for **Help~~~~~~**   
***  
However, I can just do the following things:

- **Spending my whole day finishing the assignments**
- **Crying**
- **Serching for help on the Internet**

Introduction of What I Create Using R
========================================================
transition:linear
font-family: 'Helvetica'
- I use R to create a little app called   
*"BMI calculator"*  

- It can be used to calculate your **BODY MASS INDEX** which made from the formula $weight/height^2$  

- What's more, the calculator will give you the resault of your health condition according to the BMI official accessing criteria.

What It LOOKS LIKE 
=====================================================
[CLICK ME](https://winnie92.shinyapps.io/BMIcalculator)  
- **You can go to the link above try my app**  
- It was made by the following code:  

```r
library(shiny)
shinyServer(
  function(input, output) {
    output$houtput<-renderPrint({input$height})
    output$woutput<-renderPrint({input$weight})
    output$bmi <- renderPrint({
      round(input$weight/(input$height/100)^2,2)
      })
   
    output$result <-renderText({
      if(input$weight/(input$height/100)^2 < 18.5) "malnutrition"
      else if(input$weight/(input$height/100)^2>=18.5 & input$weight/(input$height/100)^2<=24.99) "healthy" 
      else  "overweight"
    })
  }
)
```
How Does It BE MADE 
========================================================
- the code in "ui.R":  

```r
library(shiny)
shinyUI(pageWithSidebar(
  headerPanel("Calculating your BMI"),
  sidebarPanel(
    h5("The body mass index (BMI) is a measure of relative weight based on an individual's mass and heigh, which is also commonly used to measure if you are overweight by the health insituations."),
    numericInput("height","Please enter your Height:cm",160,min=50,max=250,step=1),
    numericInput("weight","Please enter your Weight:kg",50,min=30,max=90,step=1),
    submitButton("submit")
    
  ),
  mainPanel(
    
    p("you entered a height of"),
    verbatimTextOutput("houtput"),    
    p("you entered a weight of"),
    verbatimTextOutput("woutput"),
    p("Your Body Mass Index"),
    verbatimTextOutput("bmi"),
    p("result"),
    verbatimTextOutput("result")
  )
))
```

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Calculating your BMI</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<h5>The body mass index (BMI) is a measure of relative weight based on an individual's mass and heigh, which is also commonly used to measure if you are overweight by the health insituations.</h5>
<div class="form-group shiny-input-container">
<label for="height">Please enter your Height:cm</label>
<input id="height" type="number" class="form-control" value="160" min="50" max="250" step="1"/>
</div>
<div class="form-group shiny-input-container">
<label for="weight">Please enter your Weight:kg</label>
<input id="weight" type="number" class="form-control" value="50" min="30" max="90" step="1"/>
</div>
<div>
<button type="submit" class="btn btn-primary">submit</button>
</div>
</form>
</div>
<div class="col-sm-8">
<p>you entered a height of</p>
<pre id="houtput" class="shiny-text-output"></pre>
<p>you entered a weight of</p>
<pre id="woutput" class="shiny-text-output"></pre>
<p>Your Body Mass Index</p>
<pre id="bmi" class="shiny-text-output"></pre>
<p>result</p>
<pre id="result" class="shiny-text-output"></pre>
</div>
</div>
</div><!--/html_preserve-->
