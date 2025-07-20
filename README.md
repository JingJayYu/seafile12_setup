# Seafile v12 Setup Tutorial

This guide will walk you through setting up **Seafile v12** using Docker. It is recommended to use **Portainer** for managing your containers.

## Prerequisites
- Docker installed on your server
- Portainer (optional but recommended)
- Basic knowledge of terminal commands

## Steps to Set Up Seafile v12

### 1. Start the Docker Container
Use the following command to start the Seafile container:

```bash
docker-compose up -d
```

### 2. Initial Configuration
After the container is up and running, some initial settings are required.

#### Set Admin Account
Due to a bug in Seafile v12, the admin account must be manually set. Run the following commands:

```bash
docker exec seafile-container bash
seafile-server-latest/reset-admin.sh
```

This script will prompt you to set the admin username and password. Make sure to keep these credentials secure.

### 3. Enable WebDAV (Optional)
To enable WebDAV, edit the `seafdav.conf` file:

```bash
nano ./conf/seafdav.conf
```

Add or modify the following line:

```ini
enabled = true
```

Save and exit the file.

### 4. Configure HTTPS for Domain Hosting (Optional)
If you are hosting Seafile on a domain name, ensure the service URLs are set to HTTPS. Edit the `seahub_settings.py` file:

```bash
nano ./conf/seahub_settings.py
```

Update the following settings:

```python
SERVICE_URL = 'https://your-domain.com'
FILE_SERVER_ROOT = 'https://your-domain.com/seafhttp'
```

Save and exit the file.

## Notes
- If you encounter issues during setup, refer to the [Seafile Documentation](https://manual.seafile.com/) for additional guidance.
- Restart the container after making changes to configuration files:

  ```bash
  docker-compose restart
  ```

## Recommended Tools
- [Portainer](https://www.portainer.io/) for managing Docker containers
- [Nano](https://www.nano-editor.org/) for editing configuration files

## Contributing
Feel free to contribute to this tutorial by opening a pull request or submitting issues.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
**Seafile v12** is a powerful file syncing and sharing solution. With this guide, you can quickly set up and configure your own instance. Enjoy!
