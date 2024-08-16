# Raspberry Pi Pico Life
A Conway's game of life on Pimoroni's Cosmic Unicorn (Pi Pico). If you want a nice-looking piece of hardware which provides ambient light look no further! This project is like a lava lamp and it's intended to nicely blend into your home environment and serve as a point of interest.

![IMG_4013](https://github.com/krucios/pico_life/assets/7770409/a22bc96b-99f0-4d57-87ac-f6f92da315fa)
![IMG_4012](https://github.com/krucios/pico_life/assets/7770409/cefcf953-237a-4bd0-9a79-3ae81f91af1a)

# Features
The main feature of Pico Life is to conduct a Game of Life simulation. The borders are linked to each other (left to right and top to bottom) making it a toroid topology. That means simulation will never go out of viewpoint.
To make it more interesting to play there are a few control options:
- Button A: inserts glider to the left top corner which glides down along the main diagonal.
- Button B: inserts glider to the bottom left corner which glides up along a minor diagonal.
- Button C: randomizes the state of life.
- Button D: inserts randomly selected predefined oscillator pattern. Important to note that it doesn't wipe out the rest of the state so if you want to keep that pattern oscillating forever make sure to clean the state beforehand.
- Button Zzz: clears the state leaving it blank. Useful if you want to start from scratch and insert gliders/patterns.
- Button Vol +: increases the delay between generations making simulation slower.
- Button Vol -: decreases the delay between generations making simulation faster.
- Button Lux +: scrolls through different brightness levels (from super dim to super bright).
- Button Lux -: scrolls through predefined colours.

# Prerequisites
- [Pimoroni Cosmic Unicorn LED matrix with RPi pico W](https://shop.pimoroni.com/products/space-unicorns?variant=40842626596947)
- A prepared pico development environment
  - Up-to-date [Pico SDK](https://github.com/raspberrypi/pico-sdk) with env variables pointing to the installation directory. For more info check [getting started documentation](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)
  - Up-to-date [Pimoroni Pico repo](https://github.com/pimoroni/pimoroni-pico). Make sure your dev env has a `PIMORONI_PICO_PATH` env variable pointing to the installation

# How to build
The exact command might vary depending on your OS. The example below is based on Linux.
1. Clone this repo to a convenient for your location
2. Connect Pi Pico behind the Cosmic Unicorn matrix to your computer with Pico dev environment.
3. `cd <pico_life_repo_location>`
4. `mkdir build && cd build`
5. `cmake ..`
6. `make all`
7. Upload `pico_life.uf2` to Pi Pico using your preferred way. Check Pico documentation for programming guidelines. Personally, I prefer `picotool` so below there is an example of how to use it.
   1. `sudo picotool load pico_life.uf2 -F`
   2. `sudo picotool reboot`

# Ideas for improvement
- Attach the battery and make Pico Life neater and more portable. Easy to implement, just solder Pimoroni SHIM and attach the battery!
  - [Pimoroni LiPo SHIM for Pico](https://shop.pimoroni.com/products/pico-lipo-shim?variant=32369543086163)
  - [LiPo battery with JST connector](https://www.amazon.co.uk/dp/B09DPP5KCF?ref=ppx_yo2ov_dt_b_product_details&th=1)
- Implement a settings menu and provide more options to control simulation
- Add more interesting patterns 

# Contribute!
Feel free to create pull requests for anything you might wish to add to this project. Any of your ideas are welcome!
