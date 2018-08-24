
Motivation:

Jupyter is a complicated system with many options.

Configuration is how we figure out what needs to happen in the face of so many options.

Because the system is complicated, configuration inherits that complication.

We're trying to make that complication less imposing.

Topics:

- hierarchical config system
  - ref: jupyter_core paths
  - local file 
  - per user (JUPYTER_CONFIG_DIR)
    - if testing, set JUPYTER_CONFIG_DIR and use a user install
  - environment (also called sys-prefix)
  - system (user installable has higher priority)
  - cascading files
    - merged across files, but same traitlets on the same class are overwritten
    - class specificity comes before file priority:
      - example: quick, A B + pre-written system files
- config files
  - name conventions
    - ref: traitlets.config.application 
  - two kinds:
    - json
      - static
      - they are declarative
    - python
      - interpreted (they can have logic)
      - recommended approach for humans
- command line apps
  - ref: traitlets.config.application traitlets.config.loader
  - `-h` or `--help` common options
  - `--help-all` all the things you can configure
  - convenience options are just conveniences
  
- traitlets 
  - tag(config=True)
  - To make most classes configurable you can add the Configurable super class
  - Some classes cannot inherit from Configurable… e.g., notebook's APIHandler
    - to solve this create another Configurable class near by it
- programmatically
  - __init__ conventions:
    - Instantiate configurable object use `MyConfigurable(config=Config())`; top of cascade
    - If you are already inside a Configurable object, `MyConfigurable(parent=self)`
    - default `Configurable`s include `**kwargs`
      - enables setting traits in __init__ as keywords
      - also enables the `parent=self`
    

- extensions
  - add code to modify the behaviour of applications
    - notebook has 2 pieces
    - nbextensions: extend code to the front-end (javascript)
    - serverextensions: extend code to the server (python)
      - front-end agnostic
  - autoinstalls with datafiles
    - doesn't work with editable installs
    - `jupyter_notebook_config.d`
    - `notebook.d`, `edit.d`, `tree.d`, `terminal.d` + `common.d` (applies to them all)
      - any files in these directories will be used as a config file 
  - disabling 
    - `jupyter nbextension uninstall --py <name of extension>`
  - uninstalling extensions:
    - uninstall nbextensions first!
      - `jupyter nbextension uninstall --py <name of extension>`
      - `pip uninstall <name of extension> `
      
      
