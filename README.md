# r-shinylive-demo

Interested in deploying a Shiny application for R within Quarto? This repository is for you!

We're showing the source code used in Joe Cheng's [posit::conf(2023) demo](https://github.com/jcheng5/posit-conf-2023-shinylive/blob/d385ad18eb0d867f25cc4721d9e8c25aeb2dfb90/slides.qmd#L299)

## Behind the Site

Interested in exploring your own App? 

The first step is to install the `r-shinylive` R package. It's currently on GitHub and can be obtained using in _R_ console:

```r
# install.packages("pak")
pak::pak("posit-dev/r-shinylive")
```

From here, we need to create a Quarto project by typing into Terminal:

```r
quarto create project default
```

![Screenshot showing the `Terminal` tab of RStudio with the command to create a Quarto project.](images/create-quarto-r-shiny-live-project.png)

Note, if you skip this step, there will not be a `_quarto.yml` file and, thus, when you try to render the document below, you'll get the error of: 

```md
ERROR: The shinylive extension must be used in a Quarto project directory (with a _quarto.yml file).
```


Next, we need to install the Quarto extension for `shinylive` by typing into the **Terminal** tab.

```sh
quarto add quarto-ext/shinylive
```

![Screenshot showing the `Terminal` tab of RStudio with the Quarto Extension installation command.](images/install-shinylive-in-terminal.png)


With that, we're now able to progress onto including a Shiny app directly into our Quarto file. Part of this process requires adding to the top of the desired Quarto file (`.qmd`) a filter key for `shinylive`:

```yml
filters:
  - shinylive
```

With that being done, please place the application inside of the desired Quarto file (`.qmd`) using:

````r
---
title: "Our first r-shinylive Quarto document!"
filters:
  - shinylive
---

```{shinylive-r}
#| standalone: true

ui <- ...

server <- function(input, output, session) {
  ...
}

shinyApp(ui, server)
```
````

Once content with the Shiny app, the next step is to Render the document by pressing the Render button.

![Press the render button in RStudio](images/rstudio-render-button.png)


During the render process, the output directory should add one folder `<QmdFileName>_files` and `shinylive-sw.js`. 

The final folder configuration looks like:

```sh
.
├── _extensions
│   └── quarto-ext/shinylive # By quarto add
├── _quarto.yml              # By quarto create
├── R-shinylive-demo.html
├── R-shinylive-demo.qmd
├── R-shinylive-demo_files
│   └── libs
└──  shinylive-sw.js
```


## References:

- [Shinylive R Package](https://github.com/posit-dev/r-shinylive)
- [Shinylive Quarto extension](https://github.com/quarto-ext/shinylive): Static Shiny apps as Quarto code chunks
