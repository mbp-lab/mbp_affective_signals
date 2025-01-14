# Multimodal Behavior Processing: Affective Signals
WiSe 2024/25 Bielefeld University

This is a repository containing jupyter-notebooks that explore different modalities that are used in multimodal analysis of human behaviour. More information about the course can be found [here](https://ekvv.uni-bielefeld.de/kvv_publ/publ/vd?id=395414864)

## Installation Instructions
In this course, you will be analyzing your own videos. To get the environment with all the necessary packages here we are going to use docker. The Docker container will be used as a development environment where you will run all the jupyter-notebooks.  

### Docker compose
The only dependency that you are required to install is Docker and Docker-compose. Please refer to the original instructions provided by docker.
* [Docker](https://docs.docker.com/engine/install/)
* [Docker-compose](https://docs.docker.com/compose/install/)
* WARNING: Running ```docker-compose up -d``` takes quite a bit of time (~15 minutes)
* Check that docker installation was successful using the command ``` docker run hello-world ```

If you run into problems, check the FAQ at the bottom of this README.


## Getting Started with the Notebooks

### Cloning the repository

All notebooks during the semester will be provided through this GitHub repository.  The easiest way to obtain the notebooks is to `clone` this repository, and then perform a `git pull` when we announce that new notebooks are available. Here I will provide terminal instructions to clone and pull the repo, but you are free to use your preferred GUI or Git interface.

1. To `clone` the repository:
	- First make sure you have in a directory where you would like to store the repository
	- `git clone \<LINK TO REPO\>`
	- This will download all the current notebooks and material into a folder named \<REPO NAME\>

2. If we announce a new notebook or repository changes, then `pull` from the repo to get the latest material
	- make sure you are in the cloned directory named \<REPO NAME\>
	- run: `git pull`
	- You should receive a message indicating new files were downloaded

### Running the Notebooks with docker
As mentioned earlier, we will be using docker to run the notebooks.

1. Start Docker:
    - Copy the video that you will analyze into the  \Notebooks folder that is within the cloned directory. (cp video_name.mp4 \<REPO NAME>\Notebooks\)
	- make sure you are in the cloned directory named \<REPO NAME\>.
	- Then run the command below to start the containers.
	
	```bash
	docker-compose up -d 
	```
    
	- You should receive a message indicating that the containers were started. 
	
	```console
	Creating jupyter_notebook ... done
	Creating openface         ... done
	```
    
  	* You can use ```docker ps``` to other details regarding the running containers. 
2. Extracting features using openface
  	- To run openface on the video that you copied, use the command below.
	```bash
	docker exec -it openface FeatureExtraction -f /home/Notebooks/video_file_name -out_dir /home/Notebooks/processed
	```
  	- Note: The video_file_name is just the name of your file and not the whole path, if the name of the file placed in Notebooks folder above was ba_zoom.mp4 you would run the below command :
  
	```bash
	docker exec -it openface FeatureExtraction -f /home/Notebooks/ba_zoom.mp4 -out_dir /home/Notebooks/processed
	```
    
  	- Check the folder \<REPO NAME\>/Notebooks/processed on your local system if you have the processed video with the csv file 
3. Running the jupyter-notebook:
	- To start the jupyter-notebook instance, use the command below:
	``` bash
	docker exec -it jupyter_notebook jupyter-notebook --no-browser --ip="*" --allow-root 
	```
	- Example output to the above command.
    	```console
		To access the notebook, open this file in a browser:
		file:///root/.local/share/jupyter/runtime/nbserver-19-open.html
		Or copy and paste one of these URLs:
		http://04e87b4e4334:8888/?token=0d4b53daa9a1363031bcb1cf3f2b503a6c871d19ef28c21d
		or http://127.0.0.1:8888/?token=0d4b53daa9a1363031bcb1cf3f2b503a6c871d19ef28c21d
		```
	- Copy the link shown on your console to your browser.
	- You should now have a jupyter-notebook running in your browser
4. To stop the Docker:
  	- Run the command below to shut down the docker containers
	``` bash
	docker-compose down
	```
  	- You should get a message in your console indicating the container has stopped
	
	```console
	Stopping openface         ... done
	Stopping jupyter_notebook ... done
	Removing openface         ... done
	Removing jupyter_notebook ... done
	Removing network affectivesignals_default  
	```
Additional Info-

To run the affectiveSignalsHeart.ipynb, run the command below after you start the container (after running ```docker-compose up -d```):
``` bash
docker exec -it -w /home/ jupyter_notebook bash -c "source ~/.bashrc; jupyter-notebook --no-browser --ip="*" --allow-root" 
```
=> on Mac you have to replace the quotes of --ip="*" to single quotes!

## FAQ
* ```docker-desktop : Depends on: docker-ce-cli but is not installable; E: Problems can't be fixed, you have held back broken packages```
	-> make sure the [setup the docker repository] (https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository) first 
* ```ERROR: Couldn't connect to Docker daemon at http+docker://localhost - is it running?```
	-> run command with sudo, or manage docker rights
* ```PermissionError: [Errno 13] Permission denied```
	-> run command with sudo, or manage docker rights

