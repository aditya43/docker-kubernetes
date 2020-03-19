## How To Run
- Execute following command:
    ```sh
    docker-compose up
    ```
- Visit:
    ```
    http://localhost:8080
    ```
- Follow on screen instructions to setup `drupal`. Under `database config`, specify following connection details:
    ```
    Database Type: postgres
    Database Username: aditya
    Database Password: aditya123
    Database Name: postgres
    Database Host: postgres
    ```

## To Clean Up
- Execute following command:
    ```sh
    docker-compose down -v  # -v to remove Volumes as well.
    ```
    **OR** For complete clean up:
    ```sh
    docker system prune
    docker image prune -a
    docker volume prune
    ```