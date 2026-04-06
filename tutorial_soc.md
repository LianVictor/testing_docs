---
title: Deployment of Tutorial Binary to PolarFire SoC Video Kit
layout: default
nav_order: 50
---

# Deployment of Tutorial Binary to PolarFire SoC Video Kit

Before continuing to this stage, make sure that the steps from [HW Setup] have been run

## Transfer tutorial binary from SDK to PolarFire SoC Video Kit

1. Check to see if your computer can communicate with the PolarFire SoC Video Kit via ping request:

    ```
    ping <SOC_IP>
    ```

    *The SOC_IP should be the IP Address of the PolareFire SoC Video Kit, this is obtained from the [HW Setup] stage

2. Copy the tutorial binary `yolov5n_512x288_V1000_ncomp.vnnx` and the tutorial image over to the Video Kit via SCP command:

    ```
    scp yolov5n_512x288_V1000_ncomp.vnnx root@<SOC_IP>:~/samples_V1000_NCOMP_3.0/
    scp $VBX_SDK/tutorials/test_images/dog.jpg root@<SOC_IP>:~
    ```

## Run tutorial binary on PolarFire SoC Video kit and verify results with C simulation from previous stage

1. Login to the PolarFire SoC Video Kit via ssh:

    ```
    ssh root@<SOC_IP>
    ```

2. Navigate and compile the soc-c directory on the PolareFire SoC Video Kit:

    ```
    cd VectorBlox-SDK-release-v3.0/example/soc-c
    make
    ```

3. Run the model through compiled soc-c:

    ```
    ./run-model ~/samples_V1000_NCOMP_3.0/yolov5n_512x288_V1000_ncomp.vnnx ~/dog.jpg YOLOV5
    ```
    
    Check if the results obtained from this matches the results obtained from the previous [stage](tutorial_run) in the c simulation section.
    (ie: checksums and the outputs should match)
 

## Adding tutorial binary to demo list for video demo

1. Change directories to the video demo:

    ```
    cd ~/VectorBlox-SDK-release-v3.0/example/soc-video-c
    make clean
    ```

2. Modify the following `demo_models.h` file within that directory and change the following `struct model_Descr_t models[]` list via:
    
    ```
    grep -rF "yolov5n_512x288_V1000_ncomp" demo_models.h || \
    sed -i '\|{"Midas V2", "/home/root/samples_V1000_NCOMP_3.0/Midas-V2-Quantized_V1000_ncomp.vnnx", 0, "PIXEL"},|a {"Yolov5n", "/home/root/samples_V1000_NCOMP_3.0/yolov5n_512x288_V1000_ncomp.vnnx", 0, "YOLOV5"},' demo_models.h
    ```
    *Note this step can be done manually or using the above command. If using the above command it is recommended to copy it via browser and paste into CLI

3. Verify that the modification is done by checking if the Yolov5N model is inserted in to the last set of structs using 

    ```
    cat demo_models.h
    ```

## Recompiling and running the demo

1. Run the make command

    ```
    make
    ```

2. Run the video demo

    ```
    ./run-video-demo
    ```

## Exiting the demo and returning to the SDK

1. Type `q` and `ENTER` to exit the video demo.

2. Type `exit` after quitting the video demo to terminate the SSH connection and return to the SDK


----
[HW Setup]:hw_setup