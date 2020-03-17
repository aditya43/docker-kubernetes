## About This Project
Dockerized Node.JS App.

## Author
Aditya Hajare ([Linkedin](https://in.linkedin.com/in/aditya-hajare)).

## License
Open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

----------------------------------------

## How To
```diff
+ To build an Image:
```
- Execute following command:
    ```sh
    docker image build -t adinodejsappimage .
    ```

```diff
+ To run Image:
```
- Execute following command:
    ```sh
    docker container run --rm -p 80:3000 adinodejsappimage
    ```

```diff
- To publish Image on Docker Hub:
```
- Execute following commands:
    ```sh
    # Tag the Image
    docker tag adinodejsappimage adityahajare/testing-nodejs-app

    # Push to Docker Hub
    docker push adityahajare/testing-nodejs-app
    ```

```diff
- To remove adinodejsappimage from local:
```
- Execute following commands:
    ```sh
    # Remove any existing running container of adinodejsappimage.
    docker container rm adinodejsappimage

    # Remove Image.
    docker image rm adinodejsappimage
    ```

```diff
- To download and run Image 'adityahajare/testing-nodejs-app' from Docker Hub:
```
- Execute following commands:
    ```sh
    docker container run --rm -p 80:3000 adityahajare/testing-nodejs-app
    ```