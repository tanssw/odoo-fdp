# PowerOS

## Setup

1. Create the `.env` file in the root directory of the project using the `.env.example` as a template.
2. Docker compose up the project:

   ```bash
   docker compose up -d
   ```

   **The `odoo.conf` should be configured yet.**

3. Enter the `http://localhost:8069/` in your browser.
4. Store the master password somewhere safe, It can access only once when the project is started.
5. Define the database, user, and password
6. Add a new config into `./config/odoo.conf` file:

   ```ini
   [options]
   ...
   addons_path = /mnt/extra-addons
   ```

## Python Interpreter

1. Clone the repository from github of [Odoo v18.0](https://github.com/odoo/odoo/tree/18.0)
2. Create a symlink to the `./addons/odoo`

   ```bash
   ln -s /path/to/odoo/odoo ./addons/odoo
   ```

3. Set the `python.analysis.extraPaths` inside `.vscode/settings.json` to the path of the Odoo addons directory:

   ```json
   {
       "python.analysis.extraPaths": [
           "/path/to/odoo/addons"
       ]
   }
   ```

## Odoo CLI

### Create entire database

```bash
docker exec -it {container_name} odoo -c /etc/odoo/odoo.conf -u all --without-demo=all
```

### Update the module

```bash
docker exec -it {container_name} odoo -c /etc/odoo/odoo.conf -u {module_name} --max-cron-threads=0 --stop-after-init --no-xmlrpc
```
