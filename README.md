nprapps' Project Template
=========================

Copying the template
--------------------

```
git clone git@github.com:nprapps/app-template.git $NEW_PROJECT_NAME
cd $NEW_PROJECT_NAME
git remote rm origin
git remote add origin https://github.com/nprapps/$NEW_PROJECT_NAME.git
git push -u origin master
```

Configure the project
---------------------

* Update ``app_config.py`` with the name of the new project.

Install requirements
--------------------

Node.js is required for the JST compiler. If you don't already have it, get it like this:

```
brew install node
```

Then install the project requirements:

```
npm install universal-jst
mkvirtualenv $NEW_PROJECT_NAME
pip install -r requirements.txt
```

Generating index.html
---------------------

* Run ``fab make_index`` to generate a blank index page.
* <strong>Or</strong>, for a table, run ``fab make_table:data/example.csv`` to use the table template.
* Uncomment and update the ad code and Facebook tags at the top of ``www/index.html`` (or make yourself a ticket to do it later).

Running the project locally
---------------------------

```
workon $NEW_PROJECT_NAME
fab build_assets
cd www
python -m SimpleHTTPServer
```

Visit ``localhost:8000`` in your browser.

Working with CSS, Javascript and JST 
------------------------------------

The asset pipeline is complicated and will require running several shells. 

To automatically regenerate javascript templates, run the following:

```
workon $NEW_PROJECT_NAME
fab watch_jst
```

To automatically regenerate CSS and JS packages, open another terminal and run:

```
workon $NEW_PROJECT_NAME
fab watch_assets
```

Using [tmux](http://tmux.sourceforge.net/) and [teamocil](https://github.com/remiprev/teamocil) will allow you to automatically start these services. An example teamocil config is found in ``.teamocil``.

Deploying the project
---------------------

```
fab staging master deploy
```

Deploying to a server
---------------------

The current configuration is for running cron jobs only. Web server configuration is not yet included.

* In ``fabfile.py`` set ``env.deploy_to_servers`` to ``True``.
* Run ``fab staging master setup`` to configure the server.
* Run ``fab staging master deploy`` to deploy the app. 
