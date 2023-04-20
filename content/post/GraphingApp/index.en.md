---
title: "Graphing App"
author: 'shortjij'
date: 2023
categories: ["4PL3 Final Project"]
tags: ["R Markdown", "plot", "regression"]
---



# Interactive Graphing

I made my first [shinyApp](https://shortjij.shinyapps.io/Graphing_App/)! Feel free to check it out and use the csv file found in the corresponding folder on github called TEST.csv

Here is the code I used for this app:

```{r library(shiny)

library(shiny)
library(languageR)
library(ggplot2)
library(stringr)
# Define UI for application that draws a histogram
ui <- fluidPage(
  fluidPage(
    theme = bslib::bs_theme(bootswatch = "minty"),
    titlePanel("Graph Your Data"),
    h5("This app is intended to be a quick and easy way for linguists or researchers to graph data from a csv file"),
    tabsetPanel(
      tabPanel("Upload File", 
               h5("please upload a CSV file. Only csv files will be accepted at the moment"),
               fileInput("file1", "Choose CSV File",
                accept = c(
                  "text/csv",
                  "text/comma-separated-values,text/plain",
                  ".csv")),
      tags$hr(),
      checkboxInput("header", "Header", TRUE),
      tableOutput("contents"),
      h5("Instructions for choosing variables here")),
      selectInput('xcol', 'X Variable', ""),
      selectInput('ycol', 'Y Variable', "", selected = ""),
      plotOutput('MyPlot'))
    ))


# Define server logic required to show the previews
server <- function(input, output, session) {

#IMPORT FILES
  output$contents <- renderTable({
    # input$file1 will be NULL initially. After the user selects and uploads a file, it will be a data frame with 'name', 'size', 'type', and
    #'datapath' columns. The 'datapath' column will contain the local filenames where the data can be found.
    inFile <- input$file1
    if (is.null(inFile))
      return(NULL)
    read.csv(inFile$datapath, header = input$header)
  })
  
#HOW TO CONVERT/GRAPH THE DATA
  data <- reactive({ 
    req(input$file1) ## ?req #  require that the input is available
    inFile <- input$file1 # tested with a following dataset: write.csv(mtcars, "mtcars.csv") and write.csv(iris, "iris.csv")
    df <- read.csv(inFile$datapath, header = input$header)
    # Update inputs (you could create an observer with both updateSel...)
    # You can also constraint your choices. If you wanted select only numeric
    # variables you could set "choices = sapply(df, is.numeric)"
    # It depends on what do you want to do later on.
    updateSelectInput(session, inputId = 'xcol', label = 'X Variable',
                      choices = names(df), selected = names(df))
    updateSelectInput(session, inputId = 'ycol', label = 'Y Variable',
                      choices = names(df), selected = names(df)[2])
    return(df)
  })
  output$contents <- renderTable({
    data()
  })

  output$MyPlot <- renderPlot({ ggplot(x, aes(input$xcol, input$ycol)) + geom_point()
    # for a histogram: remove the second variable (it has to be numeric as well):
    # x    <- data()[, c(input$xcol, input$ycol)]
    # bins <- nrow(data())
    # hist(x, breaks = bins, col = 'darkgray', border = 'white')
    
    # Correct way:
    # x    <- data()[, input$xcol]
    # bins <- nrow(data())
    # hist(x, breaks = bins, col = 'darkgray', border = 'white')
    
    
    # I Since you have two inputs I decided to make a scatterplot
    x <- data()[, c(input$xcol, input$ycol)]

  })
}

# Run the application 
shinyApp(ui = ui, server = server)

```
