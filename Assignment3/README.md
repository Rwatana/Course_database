# Assignment 3
## Build a MySQL environment using Docker Compose
### Background
If you use a database in application development, data must be persistent to be retained even if the container is stopped. Therefore, you can build a MySQL environment using docker compose.

The steps to build the environment are shown as follows. If you don't want to see them, you can solve the assignment by reading the reference.
- [ref](https://qiita.com/leafeon00000/items/e190cf92af3a487cc749)


#### Note
You can use docker compose insteaad of docker-compose. Setting an alias makes things easy.
   
   ```bash:.bashrc
    alias dc='docker compose'
   ```
    
   - [ref](https://qiita.com/yutat93/items/b5bb9c0366f21bcbea62)
    
#### Deadline
11/28 23:59
<details><summary>Answer</summary>
    
#### The directory architecture
    .
    ├──docker-compose.yml
    ├──docker
    │   └──Dockerfile
    ├──db
    └──sql
        └──world.sql



#### Step 1
- Create files
    - Dockerfile
        ```
        FROM mysql:5.7.34

        ENV WORK_PATH /workspace
        WORKDIR $WORK_PATH
        ```
    - docker-compose.yml
        ```
        version: "3"
        services:
          mysql:
            build:
              context: .
              dockerfile: ./docker/Dockerfile
            volumes:
              - ./:/workspace
              - ./db:/var/lib/mysql
            image: mysql
            container_name: mysql
            environment:
              - MYSQL_ROOT_PASSWORD=rootpass
              - MYSQL_DATABASE=test
              - MYSQL_USER=testuser
              - MYSQL_PASSWORD=testpass
        ```
- Create a dirctory to store files

    ```
    $ mkdir db
    ```

#### Step 2
- Run the container
    ```
    $ docker-compose up -d
    ```
    or
    ```
    $ make up
    ```
- Execute the container
    ```
    $ docker-compose exec mysql bash
    ```
    or
    ```
    make exec
    ```
#### Step 3
- Connect to MySQL server
    ```
    /workspace# mysql -u testuser -p
    ```
- Use MySQL
    ```
    mysql> USE test;
    mysql> CREATE TABLE test_table(id int, name varchar(10))
    ```
- Exit the container
    - [ref](https://www.google.com/search?q=docker+exit+container&oq=docker+exit+container&aqs=chrome..69i57j0i512l3j0i22i30l6.3941j0j9&sourceid=chrome&ie=UTF-8)
- Stop the container
    ```
    docker-compose down
    ```
    or
    ```
    make down
    ```
#### Step 4
- Check if data is persistent
    ```
    $ make up
    $ make exec
    /workspace# mysql -u testuser -p
    mysql> USE test;
    mysql> SHOW TABLES; 
    ```
If test_table is displayed, it is successful.
</details>

## References
- [How to build a MySQL environment usig docker compose](https://qiita.com/leafeon00000/items/e190cf92af3a487cc749)
- [How to set an alias](https://qiita.com/yutat93/items/b5bb9c0366f21bcbea62)
- [How to exit a container](https://www.google.com/search?q=docker+exit+container&oq=docker+exit+container&aqs=chrome..69i57j0i512l3j0i22i30l6.3941j0j9&sourceid=chrome&ie=UTF-8)

