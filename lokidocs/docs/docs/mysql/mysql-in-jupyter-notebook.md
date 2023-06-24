# MYSQL in Jupter Notebook [↗️](https://github.com/Hourout/mysql_kernel)

I Like Jupter Notebook, So I would like to run all the MYSQL Querys in it. So here the setup for Jupter with MYSQL support


```bash
pip install sqlalchemy pandas ipython-sql
pip install jupyterlab_sql
jupyter serverextension enable jupyterlab_sql --py --sys-prefix
jupyter lab build
pip install mysql_kernel

# Add kernel to your jupyter:
python -m mysql_kernel.install
```

#### Connection

```bash
postgres://localhost:5432/postgres
postgres://username:password@localhost:5432/postgres
mysql://localhost/employees
sqlite://
sqlite:///myfile.db
mysql://user:password@host:port
mysql://host:port
```

I am using xampp so i used

```bash
# In 1st line ran
mysql://root:@127.0.0.1:3306
```
