## Build

- Modify `bin/cluster/velox_deploy.py:60` and `veloxms-core/src/main/scala/edu/berkeley/veloxms/VeloxApplication.scala:48` to etcd port 2379. 

- Modify `pom.xml:160` from `<artifactId>keystone_2.10</artifactId>` to `<artifactId>keystoneml_2.10</artifactId>`. Modify `veloxms-examples/pom.xml:31` from `<artifactId>keystone_2.10</artifactId>` to `<artifactId>keystoneml_2.10</artifactId>`.

- Add `<type>pom</type>` to `.../.m2/repository/edu/berkeley/cs/amplab/mlmatrix_2.10/0.1/mlmatrix_2.10-0.1.pom` as follows.

```xml
        <dependency>
            <groupId>com.github.fommil.netlib</groupId>
            <artifactId>all</artifactId>
            <version>1.1.2</version>
            <type>pom</type>
        </dependency>
```

```xml
        <dependency>
            <groupId>com.github.fommil.netlib</groupId>
            <artifactId>all</artifactId>
            <version>1.1.2</version>
        </dependency>
```

- Execute `fab install_velox_local:<etcd_installation_dir>` to install velox. 


## Run

- Modify `config['sparkDataLocation']` in `velox_config.py`.

- Modify the order of instructions listed in README as follows.

```
curl -H "Content-Type: application/json" -d '{"context": 4, "uid":1000}' http://localhost:8080/predict/matrixfact
curl http://localhost:8080/retrain/matrixfact
curl -H "Content-Type: application/json" -d '{"context": 4, "uid":4, "score":1.3}' http://localhost:8080/observe/matrixfact
```
