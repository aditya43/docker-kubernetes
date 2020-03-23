# How To?
- For `local`:
    * Following command will `compose ` the `docker-compose.yml` file first and then use `docker-compose.override.yml` on top of it as an overlay:
        ```sh
        # This will compose `docker-compose.yml` first and then use `docker-compose.override.yml` on top of .
        docker-compose up -d
        ```
    * For inspecting:
        ```sh
        docker inspect TAB COMPLETION # Select `drupal`.
        ```
    * To clean up:
        ```sh
        docker-compose down
        ```
- For `CI`:
    * Following command will `compose ` the `docker-compose.yml` file first and then use `docker-compose.test.yml` on top of it as an overlay:
        ```sh
        # Order of these files matter.
        docker-compose -f docker-compose.yml -f docker-compose.test.yml up -d
        ```
    * For inspecting:
        ```sh
        docker inspect TAB COMPLETION # Select `drupal`.
        ```
    * To clean up:
        ```sh
        docker-compose down
        ```
- For `Production`:
    * We need to build `output.yml` file by combining outputs of both compose and override compose yaml files:
        ```sh
        # Order of these files matter.
        docker-compose -f docker-compose.yml -f docker-compose.prod.yml config > output.yml
        ```
    * Now, `output.yml` file is what we will be running on `Production`.
