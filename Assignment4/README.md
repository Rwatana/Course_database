# Assignment 4
## Build a MongoDB environment and a Go environment using Docker Compose
#### Background
When developing the application, you can access a database using languages such as Go instead of directly accessing the database server.

Also, MongoDB is one of NoSQL, unlike MySQL. You can use it to check the difference between NoSQL and RDB in the future.

The steps to build the environment to access the database server using Go are shown below. You can solve the assignment by reading the reference if you don't want to see them.

#### Note
You can use docker compose insteaad of docker-compose. Setting an alias makes things easy.
   
   ```bash:.bashrc
    alias dc='docker compose'
   ```
    
   - [ref](https://qiita.com/yutat93/items/b5bb9c0366f21bcbea62)

#### Deadline
12/5 23:59

<details><summary>Answer</summary>

### Method 1 (with this repository)

- Type the commands
    ```
    $ git clone https://github.com/okuda-seminar/document_links.git 
    or
    $ git pull origin main
    
    $ cd document_links/course_database/Assignment4/mongo-go
    $ make up
    $ make exec_go
    
    /workspace# go run src/main.go
    ```
    
### Method 2 (without this repository)
#### Step 1
- Prepare 

    ```
    $ mkdir mongo-go
    $ cd mongo-go
    $ go mod init mongo-go
    $ go get "go.mongodb.org/mongo-driver/mongo"
    ```
#### Step 2
- Create [Dockerfile](https://github.com/okuda-seminar/document_links/blob/main/course_database/Assignment4/mongo-go/docker/Dockerfile), [docker-compose.yml](https://github.com/okuda-seminar/document_links/blob/main/course_database/Assignment4/mongo-go/docker-compose.yml) and [Makefile](https://github.com/okuda-seminar/document_links/blob/main/course_database/Assignment4/mongo-go/Makefile)
    ```
    $ mkdir docker
    $ touch docker/Dockerfile
    $ touch docker-compose.yml
    $ touch Makefile
    ##############################
    # Edit files 
    ##############################
    ```
#### Step 3
- Run the container

    ```
    $ dc up -d
    ```
    or
    ```
    $ make up
    ```

- Execute the Python container

    ```
    $ dc exec go bash
    ```
    or
    ```
    $ make exec_go
    ```

#### Step 4
- Create a file to check if MongoDB is accessible ([main.go](https://github.com/okuda-seminar/document_links/blob/main/course_database/Assignment4/mongo-go/src/main.go))
    ```
    /workspace# mkdir src
    /workspace# touch src/main.go
    ##############################
    # Edit main.go 
    ##############################
    ```
- Run [main.go](https://github.com/okuda-seminar/document_links/blob/main/course_database/Assignment4/mongo-go/src/main.go)

    ```
    /workspace# go run src/main.go
    ```
    If "Connection to MongoDB" is displayed, it is successful.
    

</details>

## References
- [How to build an environment of Golang and MongoDB](https://selfnote.work/20210914/programming/golang-mongodb-docker-env/)
- [How to build an environment of Golang and MongoDB](https://buzz-server.com/tech/docker-golang-mongodb/)
- [How to build Go image in official documentation](https://docs.docker.com/language/golang/build-images/)
- [How to use Mongo driver](https://qiita.com/daredeshow/items/3c247210e9b06c313c22)
