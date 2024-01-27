# mariadb-galera
**1. ConfigMap for MariaDB Configuration (`mariadb-configmap.yaml`):**
This ConfigMap holds the configuration files for MariaDB and Galera Cluster. It is crucial to configure MariaDB and Galera appropriately for synchronization and clustering.
- `my.cnf`: This file contains MariaDB configuration settings. Notable options include setting the binlog format to `ROW` for better replication and specifying the Galera Cluster parameters.
- `galera.cnf`: Configuration file specifically for Galera Cluster. It defines parameters like the cluster name, cluster addresses, and the method used for State Snapshot Transfer (SST). In this example, it uses the `rsync` method.
**2. Secret for MariaDB Root Password (`mariadb-secret.yaml`):**
A Secret is used to securely store sensitive information like passwords. In this case, it stores the root password for MariaDB.
**3. StatefulSet for MariaDB with Galera Cluster (`mariadb-statefulset.yaml`):**
A StatefulSet is used to deploy and manage a set of replicated pods. In this example, it deploys three replicas of MariaDB pods.

- `serviceName`: This specifies the headless service used for DNS-based discovery of pod IP addresses.

- `replicas`: Defines the number of MariaDB replicas (nodes) in the cluster.

- `selector`: Identifies the pods controlled by this StatefulSet.

- `template`: Describes the pods' specification, including labels and containers.

- `initContainers`: An initialization container to set proper permissions on the persistent storage volume.

- `volumeClaimTemplates`: Defines the persistent storage for each MariaDB pod.

**4. Headless Service for MariaDB (`mariadb-service.yaml`):**

A headless service is used to provide DNS-based service discovery for the pods controlled by the StatefulSet. Clients can connect to this service to access any of the MariaDB instances.

- `ports`: Exposes the MySQL port (3306) without specifying a cluster IP (set to `None`), making it a headless service.

- `selector`: Associates the service with pods having the label `app: mariadb`.

**Additional Considerations:**

- **Security:** Ensure proper security measures, such as using secrets for sensitive information, configuring network policies, and setting up authentication and authorization for MariaDB.
