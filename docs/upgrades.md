# Upgrades

Now that all the necessary programs for the HTPC are installed, lets upgrade some of the system components to more recent versions. This will result in better performance in games and also enable support for newer hardware.

## Linux kernel

Xubuntu Core is a [Long Term Release](https://en.wikipedia.org/wiki/Long-term_support). This means that it is supported with security and software updates for five years. However, this also means that the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel) shipped with the distribution will become outdated and your system will not support hardware released after the LTS version was published.

To solve the problem described above, newer Linux kernels are back-ported to the LTS version through the hardware hardware enablement stack. To enable HWE and install the latest available Linux kernel, enter the command below into the terminal emulator.

```sh
sudo apt install --install-recommends linux-generic-hwe-20.04 
```

## Graphics drivers

Time to install the latest graphics driver. Install the PPA repository matching your graphics hardware to install the latest driver on your HTPC.

=== "AMD/Intel"
    ```sh
    sudo add-apt-repository ppa:kisak/turtle
    sudo apt update
    sudo apt full-upgrade
    ```

=== "Nvidia"
    ```sh
    sudo add-apt-repository ppa:graphics-drivers/ppa
    sudo apt update
    sudo apt full-upgrade
    ```

To enable the latest, recommended graphics driver for your hardware enter the command below into the terminal emulator.

```sh
sudo ubuntu-drivers autoinstall
```

You should also install the [Vulkan Graphics Library](https://en.wikipedia.org/wiki/Vulkan_(API)). Vulkan offers better performance in games that support it compared to [OpenGL](https://en.wikipedia.org/wiki/OpenGL) which is the Xubuntu default graphics library.

=== "AMD/Intel"
    ```sh
    sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
    ```

=== "Nvidia"
    ```sh
    sudo apt install vulkan-utils
    ```

--8<-- "docs/abbreviations.md"