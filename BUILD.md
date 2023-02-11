
## Build steps

1. Create a build directory:

    ```
    $ mkdir build && cd build
    ```

2. Configure the CMake project (Using Ninja in this example):

    ```
    $ cmake .. -G "Ninja"
    ```

4. Build it:

    ```
    $ cmake --build . --config Release
    ```

5. Run the application:

    ```
    $ ./tinyJSON ../stock_prices.json
    ```
