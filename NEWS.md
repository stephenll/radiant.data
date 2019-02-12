# radiant.data 0.9.8.7

* Various fixes to address breaking changes in dplyr 0.8.0
* Added `radiant_` prefix to all attributes, except `description`, to avoid conflicts with other packages (e.g., `vars` in dplyr)

# radiant.data 0.9.8.6

* Use `stringi::stri_trans_general` to replace special symbols in Rmarkdown that may cause problems
* Add empty line before and after code chunks when saving reports to Rmarkdown
* Use `rio` to load `sav`, `dta`, or `sas7bdat` files through the `read files` button in _Report > Rmd_ and _Report > R_.
* Create a `qscatter` plot similar to the function of the same name in Stata
* New radiant icon
* Fix for setting where both `xlim` and `ylim` are set in `visualize` function 
* Use an expandable `shinyAce` input for the R-code log in _Data > Transform_

# radiant.data 0.9.8.0

* Added an "autosave" options. Use `options(radiant.autosave = c(10, 180)); radiant::radiant()` to auto-save the application state to the `~/.radiant.session` folder every 10 minutes for the next 180 minutes. This can be useful if radiant is being used during an exam, for example.
* Emergency backups are now saved to `~/.radiant.session/r_some_id.state.rda`. The files should be automatically loaded when needed but can also be loaded as a regular radiant state file
* Replace option to load an `.rda` from from a URL in _Data > Manage_ to load `.rds` files instead
* Ensure variable and dataset names are valid for R (i.e., no spaces or symbols), "fixing" the input as needed
* Fix to visualize now `ggplot::labs` no longer accepts a list as input
* Add option to generate square and cubed terms for use in linear and logistic regression in `radiant.model`
* Fix for error when trying to save invalid predictions in `radiant.model`. This action now generates a pop-up in the browser interface
* Add a specified description to a data.frame immediately on `register`
* Option to pass additional arguments to `shiny::runApp` when starting radiant such as the port to use. For example, radiant.data::radiant.data("https://github.com/radiant-rstats/docs/raw/gh-pages/examples/demo-dvd-rnd.state.rda", port = 8080) 
* Option for automatic cleanup of deprecated code in both _Report > Rmd_ and _Report > R_
* Avoid attempt to fix deprecated code in _Report > Rmd_ if `pred_data = ""` 
* Fix for download icon linked to downloading of a state file after upgrade to shiny 1.2
* Update documentation for _Data > Combine_
* Fix for `format_df` when the data.frame contains missing values. This fix is relevant for several `summary` functions run in _Report > Rmd_ or _Report > R_
* Fix for directory set when using `Knit report` in _Report > Rmd_ and _Report > R_ **without** an Rstudio project. Will now correctly default to the working directory used in R(studio)
* Added option to change `smooth` setting for histograms with a density plot
* Similar to `pmin` and `pmax`, `pfun` et al. calculate summary statistics elementwise across multiple vectors
* Add `Desktop` as a default directory to show in the `shinyFiles` file browser
* Load a state file on startup by providing a (relative) file path or a url. For example, radiant.data::radiant.data("https://github.com/radiant-rstats/docs/raw/gh-pages/examples/demo-dvd-rnd.state.rda") 
or radiant.data::radiant.data("assignment.state.rda")
* Update example report in _Report > Rmd_
* Add `deregister` function to remove data in radiant from memory and the `datasets` dropdown list
* Fix for invalid column names if used in `Data > Pivot`

# radiant.data 0.9.7.0

* Use `summarytools` to generate summary information for datasets in _Data > Manage_
* Show modal with warning about non-writable working directory when saving reports in _Report > Rmd_ or _Report > R_
* Apply `radiant.data::fix_names` to files loaded into radiant to ensure valid R-object names
* Use the content of the `Store filtered data as` input to name the csv download in _Data > View_ 
* Add "txt" as a recognized file type for `Read files` in _Report > Rmd_ and _Report > R_
* Allow multiple `lines` or `loess` curves based on a selected `color` variable for scatter plots in _Data > Visualize_
* Indicate that a plot in _Data > Visualize_ should be updated when plot labels are changed
* Fix for [#81](https://github.com/radiant-rstats/radiant/issues/81) when variables used in _Data > Pivot_ contain dots
* Fix for `radiant.project_dir` when no Rstudio project is used which could cause incorrect relative paths to be used
* Fix code formatting for _Report > Rmd_ when arguments include a list (e.g., ggplot labels)
* On Linux use a modal to show code in Report > Rmd and Report > R when reporting is set to "manual" 
* Use `is_double` to ensure dates are not treated as numeric variables in _Data > View_
* Make sort and filter state of tables in Data > Explore and Data > Pivot available in Report > Rmd
* Fix names for data sets loaded using the `Read files` button in Report > Rmd or Report > R
* Cleanup environment after closing app
* Fix column names with spaces, etc. when reading csv files
* Additional styling and labeling options for _Data > Visualize_ are now available in the browser interface
* Fix for code generation related to DT filters

# radiant.data 0.9.6.14

## Major changes

* Using [`shinyFiles`](https://github.com/thomasp85/shinyFiles) to provide convenient access to data located on a server
* Avoid `XQuartz` requirement

## Minor changes

* Load `data(...)` into the current environment rather than defaulting only to the global environment
* `file.rename` failed using docker on windows when saving a report. Using `file.copy` instead 
* Fix for `sf_volumes` used to set the root directories to load and save files
* Set default locale to "en_US.UTF-8" when using shiny-server unless `Sys.getlocale(category = "LC_ALL")` what set to something other than "C"
* Modal shown if and Rmd (R) file is not available when using "To Rstudio (Rmd)" in _Report > Rmd_ or "To Rstudio (R)" in _Report > R_
* Track progress loading (state) files
* Fix for `radiant.sf_volumes` used for the `shinyFiles` file browser
* Improvements for sending code from Radiant to Rstudio
* Better support for paths when using radiant on a server (i.e., revert to home directory using `radiant.data::find_home()`)
* Revert from `svg` to `png` for plots in `_Report > Rmd_ and _Report > R_. `svg` scatter plots with many point get to big for practical use on servers that have to transfer images to a local browser
* Removed dependency on `methods` package

# radiant.data 0.9.5.3

* Fix smart comma's in data descriptions
* Search and replace `desc(n)` in reports and replace by `desc(n_obs)`
* Revert to storing the r_data environment as a list on stop to avoid reference problems (@josh1400)
* Fix for plot type in _Data > Pivot_ in older state files (@josh1400)
* Used all declared imports (CRAN)

# radiant.data 0.9.5.0

* Fix for `radiant.data::explore` when variable names contain an underscore 
* Fix for `find_gdrive` when drive is not being synched
* Fixes in _Report > Rmd_ and _Report > R_ to accomodate for pandoc > 2 

# radiant.data 0.9.4.6

* Don't update a reactive binding for an object if the binding already exists. See issue  https://github.com/rstudio/shiny/issues/2065
* Fix to accomodate changes in `deparse` in R 3.5
* Fix for saving data in _Data > Manage_ and generating the relevant R-code

# radiant.data 0.9.3.5

## Minor changes

* Use `dev = "svg"` for plots in _Report > Rmd_ and _Report > R_

# radiant.data 0.9.3.4

## Minor changes

* Add argument to `dtab.data.frame` to format specified columns as a percentage

## Bug fixes

* Round to the specified number of decimal places even if input if not of type integer (e.g., 2.0)

# radiant.data 0.9.3.3

## Major changes

* When using radiant with Rstudio Viewer or in an Rstudio Window, loading and saving data through _Data > Manage_ generates R-code the user can add to _Report > Rmd_ or _Report > R_. Clicking the `Show R-code` checkbox displays the R-code used to load or save the current dataset
* Various changes to the code to accomodate the use of `shiny::makeReactiveBinding`. The advantage is that the code generated for _Report > Rmd_ and _Report > R_ will no longer have to use a list (`r_data`) to store and access data. This means that code generated and used in the Radiant browser interface will be directly usable without the browser interface as well
* Removed `loadr`, `saver`, `load_csv`, `loadcsv_url`, `loadrds_url`, and `make_funs` functions as they are no longer needed
* Deprecated `mean_rm`, `median_rm`, `min_rm`, `max_rm, `sd_rm`, `var_rm, and `sum_rm` functions as they are no longer needed 

## Minor changes

* Added `load_clip` and `save_clip` to load and save data to the clipboard on Windows and macOS
* Improved auto completion in _Report > Rmd_ and _Report > R_
* Maintain, store, and clean the settings of the interactive table in _Data > View_
* Address closing Rstudio Window issue (https://github.com/rstudio/shiny/issues/2033)

# radiant.data 0.9.2.3

## Major changes

* _Report > Rmd_ and _Report > R_ will now be evaluated the `r_data` environment. This means that the return value from `ls()` will be much cleaner

## Minor changes

* Add option to load files with extension .rdata or .tsv using `loadr` which add that data to the Datasets dropdown
* `visualize` will default to a scatter plot if `xvar` and `yvar` are specified but no plot `type` is provided in the function call
* Improvements to `read_files` function to interactively generate R-code (or Rmarkdown code-chunks) to read files in various format (e.g., SQLite, rds, csv, xlsx, css, jpg, etc.). Supports relative paths and uses `find_dropbox()` and `find_gdrive()` when applicable

# radiant.data 0.9.2.2

## Minor changes

* Require `shinyAce` 0.3.0
* Export `read_files` function to interactively generate R-code or Rmarkdown code-chunks to read files in various format (e.g., SQLite, rds, csv, xlsx, css, jpg, etc.). Supports relative paths and uses `find_dropbox()` and `find_gdrive()` when applicable

# radiant.data 0.9.2.0

## Minor changes

* Addins option to start app in Rstudio window
* Upload and download data using the Rstudio file browser. Allows using relative paths to files (e.g., data or images inside an Rstudio project)

# CHANGES IN radiant.data 0.9.0.22

## Bug fixes

* Fix for [#43](https://github.com/radiant-rstats/radiant/issues/43) where scatter plot was not shown for a dataset with less than 1,000 rows
* Fix for _Report > Rmd_ and _Report > R_ when R-code or Rmarkdown is being pulled from the Rstudio editor

## Minor changes

* Updated equation example in _Report > Rmd_

# radiant.data 0.9.0.17

## Minor changes

* Use thousand separator for `summary.pivotr` and `summary.explore`
* Fix in code-generation for `table2data`

# radiant.data 0.9.0.16

## Minor changes

* Changed license for help files and images for radiant.data to [CC-BY-SA](https://creativecommons.org/licenses/by-sa/4.0/legalcode)

# radiant.data 0.9.0.15

## Minor changes

* Allow all textarea inputs and multi-select inputs to be resized manually by the user
* Use 200 dpi for plots in _Report > Rmd_ and _Report > R_
* _Data > Vizualize_ now has an option to select a sample of data for scatter plots (e.g., 1K, 5K, 10K, or All)

## Bug fixes

* Fix for `rounddf` to ignore dates

# radiant.data 0.9.0.13

## Minor changes

* Apply `fixMS` to replace curly quotes, em dash, etc. when using _Data > Transform > Create_
* Option to set number of decimals to show in _Data > View_ 
* Improved number formatting in interactive tables in _Data > View_, _Data > Pivot_, and _Data > Explore_
* Option to include an interactive view of a dataset in _Report > Rmd_. By default, the number of rows is set to 100 as, most likely, the user will not want to embed a large dataset in save HTML report
* _Data > Transform_ will leave variables selected, unless switching to `Create` or `Spread`
* Switch focus to editor in _Report > Rmd_ and _Report > R_ when no other input has focus

## Bug fixes

* Fix for decimals to show in interactive tables _Report > Rmd_ and saved HTML reports
* Better error messages for `xtile` and when binning data with too many groups
* Fix for variable type warnings in _Data > Pivot_ when filtering the table
* Fix for \ in equations in _Report > Rmd_

# radiant.data 0.9.0.7

## Minor changes

* Allow response variables with NA values in _Model > Logistic regression_ and other classification models
* Support logicals in code generation from _Data > View_
* Track window size using `input$get_screen_width`
* Focus on editor when switching to _Report > Rmd_ or _Report > R_ so generated code is shown immediately and the user can navigate and type in the editor without having to click first
* Add information about the first level when plotting a bar chart with a categorical variable on the Y-axis (e.g., mean(buyer {yes}))

## Bug fixes 

* Cleanup now also occurs when the stop button is used in Rstudio to close the app
* Fix to include `DiagrammeR` based plots in Rmarkdown reports
* Fix in `read_files` for SQLite data names
* De-activate spellcheck autocorrection in `selectizeInput` in Rstudio Viewer [shiny #1916](https://github.com/rstudio/shiny/issues/1916)
* Fix to allow selecting and copying text output from _Report > Rmd_ and _Report > R_
* Remove "fancy" quotes from filters
* Known issue: The Rstudio viewer may not always close the viewer window when trying to stop the application with the `Stop` link in the navbar. As a work-around, use Rstudio's stop buttons instead. 

# radiant.data 0.9.0.0

## Major changes

* If Rstudio project is used _Report > Rmd_ and _Report > R_ will use the project directory as base. This allows users to use relative paths and making it easier to share (reproducible) code
* Specify options in .Rprofile for upload memory limit and running _Report > Rmd_ on server
* `find_project` function based on `rstudioapi`
* _Report > Rmd_ Read button to generate code to load various types of data (e.g., rda, rds, xls, yaml, feather)
* _Report > Rmd_ Read button to generate code to load various types of files in report (e.g., jpg, png, md, Rmd, R). If Radiant was started from an Rstudio project, the file paths used will be relative to the project root. Paths to files synced to local Dropbox or Google Drive folder will use the `find_dropbox` and `find_gdrive` functions to enhances reproducibility.
* _Report > Rmd_ Load Report button can be used to load Rmarkdown file in the editor. It will also extract the source code from Notebook and HTML files with embedded Rmarkdown
* _Report > Rmd_ will read Rmd directly from Rstudio when "To Rstudio (Rmd)" is selected. This will make it possible to use Rstudio Server Pro's _Share project_ option for realtime collaboration in Radiant
* Long lines of code generated for _Report > Rmd_ will be wrapped to enhance readability 
* _Report > R_ is now equivalent to _Report > Rmd_ but in R-code format
* _Report > Rmd_ option to view Editor, Preview, or Both
* Show Rstudio project information in navbar if available

## Minor changes

* Overflow `pre` and `code` blocks in HTML reports generated in _Report > Rmd_
* Read rdata files through _Data > Manage_
* Enhanced keyboard shortcuts
* Enhanced editing features in _Report > Rmd_ and _Report > R_ based on updates to `shinyAce`

# radiant.data 0.8.7.8

## Minor changes

* Added preview options to _Data > Manage_ based on https://github.com/radiant-rstats/radiant/issues/30
* Add selected dataset name as default table download name in _Data > View_, _Data > Pivot_, and _Data > Explore_
* Use "stack" as the default for histograms and frequency charts in _Data > Visualize_
* Cleanup `Stop & Report` option in navbar
* Upgraded tidyr dependency to 0.7
* Upgraded dplyr dependency to 0.7.1

## Bug fixes

* Fix for large numbers in _Data > Explore_ that could cause an integer overflow

# radiant.data 0.8.6.0

## Minor changes

* Export `ggplotly` from `plotly` for interactive plots in _Report > Rmd_
* Export `subplot` from `plotly` for grids of interactive plots in _Report > Rmd_
* Set default `res = 96` for `renderPlot` and `dpi = 96` for `knitr::opts_chunk`
* Add `fillcol`, `linecol`, and `pointcol` to `visualize` to set plot colors when no `fill` or `color` variable has been selected
* Reverse legend ordering in _Data > Visualize_ when axes are flipped using `coor_flip()`
* Added functions to choose.files and choose.dir. Uses JavaScript on Mac, utils::choose.files and utils::choose.dir on Windows, and reverts to file.choose on Linux
* Added `find_gdrive` to determine the path to a user's local Google Drive folder if available
* `fixMs` for encoding in reports on Windows

## Bug fixes

* Chi-sqaure results were not displayed correctly in _Data > Pivot_
* Fix for `state_multiple`

# radiant.data 0.8.1.0

## Minor changes

* Specify the maximum number of rows to load for a csv and csv (url) file through _Data > Manage_
* Support for loading and saving feather files, including specifying the maximum number of rows to load through _Data > Manage_
* Added author and year arguments to help modals in inst/app/radiant.R (thanks @kmezhoud)
* Added size argument for scatter plots to create bubble charts (thanks @andrewsali)
* Example and CSS formatting for tables in _Report > Rmd_
* Added `seed` argument to `make_train`
* Added `prop`, `sdprop`, etc. for working with proportions
* Set `ylim` in `visualize` for multiple plots
* Show progress indicator when saving reports from _Report > Rmd_
* `copy_attr` convenience function
* `refactor` function to keep only a subset of levels in a factor and recode the remaining (and first) level to, for example, other
* `register` function to add a (transformed) dataset to the dataset dropdown
* Remember name of state files loaded and suggest that name when re-saving the state
* Show dataset name in output if dataframe passed directly to analysis function
* R-notebooks are now the default option for output saved from _Report > Rmd_ and _Report > R_
* Improved documentation on how to customize plots in _Report > Rmd_
* Keyboard short-cut to put code into _Report > Rmd_ (ALT-enter)

## Bug fixes

* When clicking the `rename` button, without changing the name, the dataset was set to NULL (thanks @kmezhoud, https://github.com/radiant-rstats/radiant/issues/5)
* Replace ext with .ext in `mutate_each` function call
* Variance estimation in Data > Explore would cause an error with unit cell-frequencies (thanks @kmezhoud, https://github.com/radiant-rstats/radiant/issues/6)
* Fix for as_integer when factor levels are characters
* Fix for integer conversion in explore
* Remove \\r and special characters from strings in r_data and r_state 
* Fix sorting in _Report > Rmd_ for tables created using _Data > Pivot_ and _Data > Explore_ when column headers contain symbols or spaces (thanks @4kammer)
* Set `error = TRUE` for rmarkdown for consistency with knitr as used in _Report > Rmd_
* Correctly handle decimal indicators when loading csv files in _Data > Manage_
* Don't overwrite a dataset to combine if combine generates an error when user sets the the name of the combined data to that of an already selected dataset
* When multiple variables were selected, data were not correctly summarized in Data > Transform
* Add (function) lable to bar plot when x-variable is an integer
* Maintain order of variables in Data > Visualize when using "color", "fill", "comby", or "combx"
* Avoid warning when switching datasets in Data > Transform and variables being summarized do not exists in the new dataset
* which.pmax produced a list but needed to be integer
* To customized predictions in radiant.model indexr must be able to customize the prediction dataframe
* describe now correctly resets the working directory on exit
* removed all calls to summarise_each and mutate_each from dplyr

## Deprecated
* varp_rm has been deprecated in favor of varpop 
* sdp_rm has been deprecated in favor of sdpop 
* mutate_each has been deprecated in favor of mutate_at, mutate_all, and radiant.data::mutate_ext
