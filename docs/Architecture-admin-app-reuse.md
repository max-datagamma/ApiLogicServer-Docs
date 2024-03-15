!!! pied-piper ":bulb: TL;DR: Admin App Runtime stored in `venv`"

    To save project space, the admin app source (JavaScript, CSS etc) is not stored in each created app.  Instead, it is stored in the `venv`.

    Further, so that admin app changes do not cause unnecessary changes to ApiLogicServer git, these files are not stored in the GitHub project.

    
## Admin App Runtime

Recall that the Admin App is defined by a yaml file.  The actual app is a minified React Admin JavaScript app, [safrs-react-admin](https://github.com/thomaxxl/safrs-react-admin){:target="_blank" rel="noopener"}.

It's about 34MB.  Not huge, but 10X bigger than most API Logic Projects.  So, we want to share it, making it available in the [run-venv](Architecture-venv/#run-venv){:target="_blank" rel="noopener"}.

Moreover, we don't want it to take up space in the ApiLogicServer git repository.

So, when you create the dev project, the [installer places a copy into your source tree](Architecture-Internals.md#admin-app-source), but denotes it as `.gitignore`.

It looks like this in the dev source:

![admin-app-code](images/internals/admin-app-code.png)

It looks like this in the run-venv (though, your project may be using a [shared venv](Project-Env.md#shared-venv){:target="_blank" rel="noopener"}):

![admin-app-code](images/internals/admin-app-created-project.png)

&nbsp;

## Loaded by `admin_loader.py`

This module 

* finds (see `get_sra_directory()`) the minified Admin App,
* returns (see `return_spa()`) the minified Admin App, and
* returns the `admin.yaml` file
