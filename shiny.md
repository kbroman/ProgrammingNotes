## R Shiny

- [Mastering Shiny book](https://mastering-shiny.org)
- [shinydashboard](https://rstudio.github.io/shinydashboard/)
- [flexdashboard](https://rmarkdown.rstudio.com/flexdashboard/)

### Inputs

- `textInput`
- `passwordInput`
- `textAreaInput`
- `numericInput`
- `sliderInput` (simple or range; can be dates)
- `dateInput`
- `dateRangeInput`
- `selectInput` (drop-down list; can be multiple)
- `radioButtons`
- `checkboxInput`
- `checkboxGroupInput`
- `fileInput`
- `actionButton`

### Outputs

- `textOutput` and `renderText`
- `verbatimTextOutput` and `renderPrint`
- `tableOutput` and `renderTable`
- `dataTableOutput` and `renderDataTable`
- `plotOutput` and `renderPlot`


### Layouts

- `fluidPage`
- `titlePanel`
- `sidebarLayout`, `sidebarPanel`, `mainPanel`
- `fluidRow` and `column(n, ...)`


### Themes

- `fluidPage(theme=shinythemes(theme), ...)`
- [shinythemes](https://rstudio.github.io/shinythemes/)
- [shinythemes gallery](https://shiny.rstudio.com/gallery/shiny-theme-selector.html)
- [fresh package](https://dreamrs.github.io/fresh/)


### Reactivity and timing

- `reactive()`
- `reactiveTimer()`
- `eventReactive()`
- `observeEvent()`
