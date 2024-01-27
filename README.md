# mariadb-galera
A headless service is used to provide DNS-based service discovery for the pods controlled by the StatefulSet. Clients can connect to this service to access any of the MariaDB instances.

ports: Exposes the MySQL port (3306) without specifying a cluster IP (set to None), making it a headless service.

selector: Associates the service with pods having the label app: mariadb

