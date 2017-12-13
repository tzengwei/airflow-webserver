Airflow-Webserver
--------------------------------------------------------------

NOTE: This is work-in-progress repository for the migration of [Airflow](https://github.com/apache/incubator-airflow)'s webserver from Flask-Admin to [Flask-AppBuilder (FAB)](https://github.com/dpgaspar/Flask-AppBuilder).

The goal of this Airflow Webserver fork is to leverage FAB's build-in security features to introduce the following capabilities in the UI:
- role-based access control
- dag-level permissions
- support for various authentications backends (OAuth, OpenID, Database, LDAP, etc.)

See [this link](http://104.209.38.171:8080) for a demo Airflow instance (username: admin, password: admin)

Airflow-Webserver will potentially be merged back into Airflow's source code in the near future.

Contributions are welcome!

Setup
--------------------------------------------------------------

Airflow-Webserver is written on top of Airflow 1.9.0, which is not currently in PyPI. Make sure you have airflow 1.9.0 installed before attempting the setup below.

- To install Flask-AppBuilder

        `pip install flask-appbuilder`

- To set up the database object, modify the SQLALCHEMY_DATABASE_URI variable in config.py to your Airflow db.
  Note this will generate new tables which FAB uses for its security model.
  
        `cd flask-appbuilder`
        `fabmanager create-db`

- To create an admin account

        `fabmanager create-admin`

- To start the webserver

        `fabmanager run --app airflow_webserver`

Caveats
--------------------------------------------------------------

- I am actively contributing to Flask-Appbuilder to support backward-compatibility with existing Airflow features, and some of these features have not been rolled out to the latest release, including support for models with binary-type column and composite primary key. There are open PRs that are addressing these issues.

Work-in-progress
--------------------------------------------------------------

- Verification of integrations with 3rd-party authentication backends
- FAB features including support for [composite primary key](https://github.com/dpgaspar/Flask-AppBuilder/pull/639) and [on_model_change](https://github.com/dpgaspar/Flask-AppBuilder/pull/661)
- DAG-level access control
- Tests
