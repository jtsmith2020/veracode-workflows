# veracode-workflows

A Command Line Interface for using __Veracode Services__ in a software development environment that uses Git for source control. 
Configuration of the Services is managed via JSON data structures that are stored and managed with the repository in a `veracode.config` file and which are __Branch Aware__.

### Workflows

There are 2 main workflows implemented:

* `scan` workflow initiates whatever types of scan is configured for the current branch. For example, in `main` it might be appropriate to perform a Policy Scan and an SCA Scan but in a feature branch a Pipeline Scan and SCA Scan would be performed. 
* `evaluate` workflow is used to examine the results of any scans that have been performed and perform any actions that are necessary. For example, in main it might be appropriate to fail the build if the Policy Scan doesn't comply with the Policy assigned but in a feature branch Tickets might be created for identified Flaws 

In addition to the main workflowds there is also a `configure` workflow which is used to develop the veracode.config file

### Branch Aware?

The `veracode.config` file is in JSON format and it's root object is a list. Each element in the list is a dictionary of configuration settings for all of the Veracode Services along with a `match_pattern` value. The `match_pattern` is a regular expression and when the `veracode-cli` is executed it will use the current branch name (either passed as an argument or retrieved from the current Git branch) to match against the `match_pattern` values of each dictionary and the first one which matches will be used as the configuration for the Veracode Service and Command that are executed.


