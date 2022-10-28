Mujoco-py
These are the steps to install Mujoco-py on UBUNTU 20.04, 64-bit, python3.8

Step1: Download mujoco200 linux from https://www.roboti.us/download.html
Step2: Create ~/.mujoco directory and extract mujoco200_linux inside the directory
Step3: Rename mujoco200_linux to mujoco200
Step4: Download Activation key (mjkey.txt) from https://www.roboti.us/license.html
Step5: Move the activation key to ~/.mujoco 
	mv mjkey.txt ~/.mujoco
Step4: Build Mujoco-py from source:
	git clone https://github.com/openai/mujoco-py.git
	pip install -r requirements.txt 
	pip install -r requirements.dev.txt 
	sudo python3 setup.py install 
Step5: Put export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/<path>/.mujoco/mujoco200/bin in your ~/.bashrc file
 source ~/.bashrc
 Step6: Run your first program
 	import gym
	import mujoco_py
	env = gym.make('FetchReach-v1')
	env.reset()

	for _ in range(300):
		env.render()
		env.step(env.action_space.sample())
	env.close()
 
Troubleshooting 
1. Permissionerror:[errno 13] permission denied: b'/usr/local/lib/python3.8/dist-packages/mujoco_py-2.0.2.13-py3.8.egg/mujoco_py/generated/mujocopy-buildlock'
	change permission of generated folder
	sudo chmod 777 generated
2. Error: command 'x86_64-linux-gnu-gcc' failed with exit status 1
	Install the following developmental header
	sudo apt-get install libosmesa6-dev
3. Glew initalization error missing gl version
	Install the following package
	sudo apt-get install -y libglew-dev
	Add export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so to ~/bashrc file and source ~/bashrc
4. [Errno 2] No such file or directory: 'patchelf']
	sudo add-apt-repository ppa:jamesh/snap-support
	sudo apt-get update
	sudo apt install patchelf

