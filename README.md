# A Tutorial on Using ESP with Lab801 Server

This tutorial provides a step-by-step instruction on how to launch the ESP GUI for SoC configurations with our lab server. 

## ESP From Columbia

> **ESP (Embedded Scalable Paltforms)** is an open-source research platform for heterogeneous system-on-chip design that combines a scalable tile-based architecture and a flexible system-level design methodology.

<div align="center">
<img src="https://i.ibb.co/pjx2mLm/esp-overview.png" alt="esp-overview" border="0">
</div>

In other words, it is a platform that integrates the full design flow of chip development. It provides 3 design flows, including RTL (Chisel, SystemVerilog, VHDL), HLS (High Level Synthesis) with C/C++ or SystemC, and Machine learning frameworks (Keras TensorFLow, Pytorch). You can choose whichever more is more suitable to your scenario.

To prototype your design, ESP also provides a SoC integration flow which automatically generates a tile-based NoC (Network-on-Chip) configured by the desiner. It comes with a GUI which guides designers to configure their own SoC with the choices of CPU, accelerator, memory and auxiliary tiles.

In the end, once your designs are ready, you can use ESP to do either a **Full-system simulation** with each supported FPGA board or real **FPGA prototyping** with supported boards. In the case of FPGA protyping, the generation of the bitstream file, the programming script and the deployment of software are fully automated.

> Full-system RTL simulation is accurate, but it is practical only for the simulation of short programs. Instead,
FPGA prototyping enables the execution of real applications on top of an operating system, while reproducing the complex interactions among all SoC components.

Fore more information, please refer to the official [ESP website](https://www.esp.cs.columbia.edu/ "ESP website") as well as the [overview paper on ESP](https://arxiv.org/pdf/2009.01178.pdf "overview paper on ESP").

In their latest paper "[Accelerator Integration for Open-Source SoC Design](https://sld.cs.columbia.edu/pubs/giri_ieeemicro21.pdf "Accelerator Integration for Open-Source SoC Design")," FPGA prototypes of various SoC designs, featuring the NVIDIA Deep Learning Accelerator and the Ariane RISC-V 64-bit processor core are demonstrated.

## How to Use ESP on Our Server

The ESP docker image based on a CentOS 7 Docker image is installed on our server and it contains:

* The installation of all the software packets required by ESP.
* The installation of utilities like vim, emacs, tmux, socat and minicom, useful when working with ESP.
* Tn environment variables setup script to be customized with the correct CAD tools paths and licenses.
* The ESP repository and all its submodules.
* The installation of the software toolchains for RISC-V and Leon3.

Each lab member is able to start his/her own ESP docker container with his/her user account. Once a contianer is started, you'll be able to use the ESP. Please follow the instructions below to laucnch the ESP GUI for SoC configurations.

1. Run the docker container for ESP.
	
		docker run --rm -it --security-opt label=type:container_runtime_t \
		--network=host -e DISPLAY=$DISPLAY \
		-v "$HOME/.Xauthority:/root/.Xauthority:rw" \
		-v /disk2/others/dsd_309591006/:/home/espuser/user \
		-v /cad/:/home/cad:ro \
		davidegiri/esp:centos7-full \
		/bin/bash
	
	* Explanation on some important arguments:
	
		`--rm` automatically removes the container after you exit it. Otherwise, you'll start a new container everytime you run the docker which will occupy the resource of our workstation.

		`-it` is neccessary for interactive processes. It actually comes from `-i -t`.

		`-e DISPLAY=$DISPLAY` provides the container with a DISPLAY environment variable. This instructs X clients – MobaXterm here – which X server to connect to.

		`-v "$HOME/.Xauthority:/root/.Xauthority:rw"` The volumes commands enable shared filesystems. 

		> What is the .Xauthority file?
		The .Xauthority (not .xAuthority) file can be found in each user home directory and is used to store credentials in cookies used by xauth for authentication of X sessions. Once an X session is started, the cookie is used to authenticate connections to that specific display. You can find more info on X authentication and X authority in the xauth man pages (type man xauth in a terminal).

		`-v /disk2/others/dsd_your_user_ID/:/home/espuser/user` mounts your local directory to the `/home/espuser/user` directory in docker container. Please avoid mounting the volume to `/home/espuser`. This will overwrite the built-in files uder that directory.

		`-v /cad/:/home/cad:ro` mounts the directory of all the CAD tools on our server to the `/home/cad` directory in docker container. To avoid any issue, `:ro` is added to keep it as read-only.

		`davidegiri/esp:centos7-full` specifies the docker image we're going to use `esp:centos7-full`

		`/bin/bash` runs the bash file automatically once we're in the container.


	You might want to put this in a shell script under your directory so that you don't have to look it up everytime and name the file as, say, `esp_docker.sh` Then you can simply run the shell script to run the docker with the command below.
	
		sh esp_docker.sh
	

	Once you logged into the server, do:
	
	`[dsd_your_user_id@icst5050 ~]$ sh esp_docker.sh`
	
	You're now in the container with the directory of `/home/espuser` and should be able to see:
	
	`root@icst5050:/home/espuser$`
	
	You can use `ls` command to see what's in there.
	And you'll find all of your files in `/home/espuser/user`
	
2. Set up the environment variables with Docker.

3. Lauch ESP GUI.

4. Leave the docker.

		exit
